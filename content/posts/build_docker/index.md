---
title: "Build Singularity/Docker Image on a Singularity Server without `sudo` Privileges"
date: 2023-07-31T16:28:08+08:00
draft: false
tags: ["virtualization", "docker", "singularity"]
categories: ["System"]
cover:
  image: "posts/build_docker/img/exploit.png"
---

In a docker container, you have full privileges to build the image of
[singularity](https://sylabs.io/singularity/) or
[docker](https://www.docker.com/) in it. But if only singularity is installed on
the server and the root user sets up neither `--fakeroot` nor `proot` and you
have exhausted your [remote
build](https://docs.sylabs.io/guides/latest/user-guide/build_a_container.html#remote-builds)
minutes, what trick can you play to work around those restrictions?


# Software Selection

To solve the problem, we need a virtual machine under control on the server for
enough privileges to execute `singularity build`(or `docker build`) which
requires `sudo` if you meet such a tough condition as mentioned before. Then an
OS is run on the virtual machine. Finally, we could build the image.

So we need to choose two things:

1. a virtual machine and
2. an OS to run singularity or docker.

QEMU is an open-source virtualization solution that supports both
software-based acceleration and hardware-based acceleration(requiring `KVM`).
And it is highly flexible and customizable. So I choose QEMU as my
virtualization software.

Any OS supporting docker/singularity is available. So I arbitrarily installed
Debian on the virtual machine.

# Practice

1. **Pull singularity image containing QEMU and enter it.**

```bash
# On the remote machine
singularity pull qemu.sif docker://tianon/qemu:latest
singularity exec qemu.sif bash
```

2. **Download Debian installation iso and allocate space.** The allocated
space is where our debian would be installed. Change 50G to another size if you
want. Also, Feel free to choose another OS or Debian with a newer version.

```bash
# In singularity QEMU
wget https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-12.1.0-amd64-netinst.iso -O debian_inst.iso 
qemu-img create -f qcow2 debian.img 50G 
```

The format of `debian.img` is `qcows`, a disk image format used by QEMU.

2.5. **Check KVM supports.** Before going further, we first check if the server
supports [Kernel-based Virtual
Machine(KVM)](https://www.redhat.com/en/topics/virtualization/what-is-KVM). If
we have KVM, enable the corresponding flag of QEMU significantly accelerates
virtualization.

```bash
# On the remote machine
lsmod | grep kvm
```

If it outputs something, congratulations! You can append `-accel kvm` to any
commands that start a virtual machine below. If no output, you can still run
QEMU, but at a lower speed.

3. **Run QEMU to install Debian.** Since the remote server does not have an
   desktop environment. We shall run QEMU without a new window of the virtual
machine. We have at least two ways to connect with the virtual machine: `-vnc`
or `-nographic`. `-nographic` uses your current terminal as the terminal of
Debian. However, the communication between our terminal and the QEMU backend is
so slow that you cannot input characters fast, otherwise some characters may be
neglected. You cannot paste long texts as well because it is another form of
"input characters fast". Moreover, when receiving characters from QEMU or
sending characters to QEMU, there may be encoding issues. So I recommend using
`-vnc`.

VNC, Virtual Network Computing, is a cross-platform screen-sharing system using
Remote Frame Buffer protocol (RFB). With it, we can connect to the screen of
Debian via a VNC client end. I choose [TigerVNC](https://tigervnc.org/) as my
VNC viewer implementation. Install it simply by 

```bash
# Local Machine

# for Debian-based distros
sudo apt install tigervnc-viewer

# for RedHat-based distros
sudo yum install tigervnc-viewer
```

But if you are a software-minimalist, you may also try `-nographic`.


```bash
# In singularity QEMU
qemu-system-x86_64 \
  -drive file=debian_inst.iso,media=disk,format=raw \
  -drive file=debian.img,media=disk,format=raw \
  -m 8G \
  -smp $(nproc) \
  -vnc :1
```

| Flag      | Explain                   |
| ---       | ---                       |
| `-m`      | memory allocation         |
| `-smp`    | core number of the guest  |
| `nproc`   | core number of the host   |
| `-vnc :x` | *x+5900* as VNC server port |

For example, `-vnc :1` means listen to port 5901. VNC server port is 5900 by
default. But if it is blocked by the firewall, try another port.

**NOTE**: Since everyone can connect to the VNC server now via this port, you
may want to limit the access for security. Check [VNC security of
QEMU](https://qemu-project.gitlab.io/qemu/system/vnc-security.html)

Anyway, we have launched the VNC server on the remote. Then on your machine and
```bash
# On the local machine
vncviewer remoteIP:5901
```
to connect to QEMU (5901 = 1 + 5900, see explanation above) and install Debian
to `debian.img`

4. **Start sshd service of Debian.** The aforementioned VNC connection is not
   secure and we cannot copy and paste text in a VNC window. So we need `ssh`.
We reboot QEMU removing the installation media and forward port 11022 of the
host to port 22 of the guest.

*Why using 11022 instead of 22? 22 occupied by sshd of the remote machine.*

```bash
# On the remote machine
qemu-system-x86_64 \
        -device e1000,netdev=net0 \
        -netdev user,id=net0,hostfwd=tcp::11022-:22 \
        -drive file=Image.img,media=disk,format=raw \
        -m 8G \
        -smp $(nproc) \
        -vnc :1
```

```bash
# In singularity QEMU, virtual Debian
sudo apt install openssh-server
sudo systemctl enable ssh
sudo systemctl start ssh
```

*A kind reminder: if ssh port is blocked by the firewall, try another port.*

As long as setup the ssh server, we can close VNC and connect to Debian via ssh:

```bash
# On the remote machine
qemu-system-x86_64 \
        -device e1000,netdev=net0 \
        -netdev user,id=net0,hostfwd=tcp::11022-:22 \
        -drive file=Image.img,media=disk,format=raw \
        -m 8G \
        -smp $(nproc) \
```

5. **Install singulariy/docker.** 

6. **Transfer the built image to the remote server by `scp`**

For more information, check QEMU network documentation
[(i)](https://wiki.qemu.org/Documentation/Networking),
[(ii)](https://en.wikibooks.org/wiki/QEMU/Networking),
[(iii)](http://bsdwiki.reedmedia.net/wiki/networking_qemu_virtual_bsd_systems.html)
and singularity network documentation
[(iv)](https://docs.sylabs.io/guides/main/user-guide/networking.html)
