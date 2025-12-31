---
title: "SSH Behind the Scene"
date: 2025-12-31T22:32:10+08:00
categories: ["Program"]
tags: ["linux", "ssh"]
draft: false
---

What happens when you ssh to a remote machine? This blog will not analyze from a cryptographic way but from a engineering way. We will touch different components on linux and how they interact. This blog is a brief introduction. We sacrifice precision for sake of clarity without compromising the core message.

# A Quick Tour

```text
systemd                                                      < root
  ├─sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups  < root
  │   └─sshd: username [priv]                                < root
  │       └─sshd: username@pts/0                             < user
  │           └─-fish                                        < user
  │               └─ other commands
  └─systemd --user                                           < user
      ├─(sd-pam)
      └─other services
```

1. A root process `sshd` listens on the configured port (usually 22). Upon connection, it forks a child.
2. This child becomes a privileged monitor process, `sshd: <username> [priv]`, to handle cleanup and audit logs.
3. The monitor forks a net-child that handles network traffic, key exchange, and package parsing as a sandbox user (usually `sshd`).
4. The net-child receives the key or password and passes it to the privileged root process via a pipe. The monitor runs the PAM stack (`/etc/pam.d/sshd`) as root, which handles auth, session setup and `pam_systemd.so`.
5. `pam_systemd.so` notifies `systemd-logind ` via D-Bus that a new session is opening.
6. `systemd-logind` maintains its own database in `/run/systemd/sessions` and checks if `user@<uid>.service` is running, If not, it asks PID 1 (system-level systemd) to start it.
7. PID 1 forks a new process to run the service.
8. Because `user@.service` has `PAMName=systemd-user`, this new service process initializes the PAM stack (`/etc/pam.d/systemd-user`), which gathers environment variables and limits.
9. To keep the PAM session alive independent of the service payload, the service process creates a `(sd-pam)` helper. `(sd-pam)`'s only job is to wait for the service to die and then call `pam_close_session` using the parent death signal `prctl(PR_SET_PDEATHSIG, SIGTERM)`.
10. The service process sets its UID to the user and execs the `systemd --user` binary, passing the PAM-generated environment variables directly. (This explains why we need `(sd-pam)`: after execing the binary, the process that knew how to run `pam_close_session()` is gone.)
11. Back at step 4, after finishing `pam_authenticate`, `net-child` terminates.
12. The `sshd` monitor calls `pam_open_session` to gather the environment like step 8 and forks a new child, `sshd: <username>@pts/233`.
13. The child then sets its UID to the user and forks a new child that sets itself as a session leader using `setsid` and execs the user's shell.
14. The shell attaches its IO to the respective `pts`. This explains why we need the login shell to be a session leader because only a session leader can attach to `pts`
15. When the user logs out, the ssh monitor detects via `SIGCHLD`. The monitor performs the final cleanup (recording logout time in `wtmp`, removing `utmp` entry, and tearing down the `PTY`).

**Note**: There is a terminology overload on the word `session`. The POSIX session (kernel session) is used to manage all the process belonging to a specific terminal. It can be set using `setsid` by the process itself. On the other hand, the PAM session in `pam_open_session` mainly concerns environment and policy management for the convinience of the admin. (Read the following section if you don't understand.)

# Questions

The main design concept has actually been explained above. This section is mainly to provide some relevant background knowledge for those who are unfamiliar with the concepts as mentioned above.

1. What's tty, pty, ptm, pts?

At first, a large box with lights and switches on it is used to control the huge computer and display output. That large box is called **console**(because it is used to control) or **terminal**(because it is IO handler at the user's end). Then a device that can both type and print characters is invented to remotely control that computer. That is teletype(**tty**), a.k.a. teleprinter and teletypewriter.

But with the burgeon of personal computers and GUI, we need another way to create a **simulated terminal** in the desktop environment. On modern Linux, this is done by the **pseudo tty**(`pty`) framework. The desktop reads your keystroke and write to the master side (`ptm`) of the pty. And the shell, like bash and fish, reads from the slave side (`pts`) of the `pty`. So your input is passed to the shell. When the shell outputs some content, it write to `pts` and your desktop environment reads `ptm` and display the content on your screen. 

When you run `find /dev -name ptm* && ls /dev/pts`, you'll find only one device related to `ptm` with a strange name `ptmx` but a lot of `pts` devices. According to the tty's one-to-one described above, shouldn't the number of `ptm` and `pts` the same? Actually, `x` means multiplexer here. Different programs openning `ptmx` will connect to different `pts`s. For more information about how the terminal multiplexer works, check [this repo](https://github.com/deadpixi/mtm)  and [this linux man](https://linux.die.net/man/4/ptmx) please.

```txt
                      +----------------------------------------------------------+
  User Space          |                   Kernel Space                           |
                      |                                                          |
Desktop Environment <-+-> /dev/ptmx <---> line discipline <---> /dev/pts/<num> <-+-> Shell
                      |                                                          |
                      +----------------------------------------------------------+
```

(How the desktop environment reads your keystrokes and passes your keycodes to the terminal simulator which writes ASCII characters to ptmx is another interesting story. But it does not have much to do with the topic of this post. So they are neglected.)

You may have noticed there is a `line discipline` between `ptmx` and `pts`. So the next question is

2. What's the line disipline?

When you press `ctrl-c` to kill a process, you write the ETX character (0x03) in ASCII to ptmx. This special character is caught by the line discipline instead of passing to the fish shell because it does not understand this special character. The kernel then sends the `SIGINT` to the foreground processes in the current session.

(What to learn more about those special characters/sequences like ^H, ^[[A, ^[[B, \033[0m? Check [this](https://askubuntu.com/questions/1190460/delete-key-not-working-in-terminal), [this](https://askubuntu.com/questions/592119/arrows-do-not-work-all-i-see-is-a-b-c-d) and [this](https://en.wikipedia.org/wiki/ANSI_escape_code).)

2. What's a POSIX session?

Every terminal has a session ID (sid). Every process running in the terminal has the same sid. sid equals to the process id (pid) of the login shell. You can run `sleep 99 &; ps -o pid,sid,cmd` to verify. When you close the terminal, the system needs to send a signal `SIGHUP`. The default behavior of a process after receiving the signal is termination. But `nohup` can make the process ignore this signal, thus making it a permanent process. `&` only makes the process run in the background, but it still receives `SIGHUP` when the session is closed. So `&` on its own will still terminate a process after you log out. `setsid` is a command to create a new session irrelavant to the current session. So `setsid` can also make permanent processes. Not every session is associated with a tty/pty. The session created by `setsid` is an example. (You can check which tty/pty your current session is attached by `tty` command.)

3. What's PAM?

`sudo`, `su`, `ssh` and more, all of them require your password. It is so dangerous if they implements the authentication separately. It would be better if we have a library to deal with all these sensitive operations. That's where the Linux Pluggable Authentication Modules (PAM) comes.

Sensitive operations are not limited to authentication. For example, auditing when you create a new session in the machine is also a dangerous operation. You shouldn't be given too much permission to fabricate the record. But you should also have the permission to write the record. Designate the task to PAM is a good option. This corresponds to the `session` policy in PAM. Besides, PAM's session policies can also handle mounting per-user volumes, creating home directory, setting ulimit. That's why we always need to invoke the PAM stack when creating a new session.

(On Linux, you can modify authentication methods easily by editing `/etc/pam.d`. For more information, check [fprint](https://wiki.archlinux.org/title/Fprint) for fingerprint unlocking and [howdy](https://github.com/boltgolt/howdy) for face unlocking)

4. Why does sshd fork a new privileged monitor process for every ssh connection instead of reusing the same sshd process to handle cleanup and audit logs that should have been done by the monitor process?

It follows the principle of least privilege to contain the blast radius of a potential compromise. If a single sshd process handled multiple connections or if the unprivileged worker retained too much access, a vulnerability triggered by one user could compromise the entire server or other users' sessions.
