---
title: "A Problem on `va_list` in C Language"
date: 2023-11-11T15:52:59+08:00
draft: false
tags: ["programming", "C", "engineering"]
---

What's the output of the following codes? And Why?

```c
#include <stdio.h>
int main(int argc, char *argv[]) {
  printf("%#018llx\n", (char)0x80);
  printf("%#018llx\n", (unsigned char)0x80);
  return 0;
}
```
(You might encounter warnings informing you of the inconsistency between the
specified format and the given arguments. Let's neglect them.)

The answer is
```bash
0x00000000ffffff80
0x0000000000000080

```

## Questions

We have two questions:
1. Is it overloading that contributes to different behaviors when different
   types of arguments are passed.
2. Why is the first output `0x00000000ffffff80` instead of `0xffffffffffffff80`?

## Answers

The analysis is based on the `printf` implementation in [x86 linux
boot](https://github.com/torvalds/linux/blob/master/arch/x86/boot/printf.c)

1. Is it overloading that contributes to different behaviors when different
   types of arguments are passed.

Answer: No. In the generated assembly, there is only one `printf` function.
However, the engagement of `va_list` in compile time enables the distinguishment
of types. As shown in the code, the signature of `printf` is `int printf(const
char *fmt, ...)`. And more importantly, `va_list` is exploited to capture all
the variadic arguments in the code. 

The following code block gives an outline of the implementation.

```c
int vsprintf(char *buf, const char *fmt, va_list args)
{
	char *str;
    /* other variables */
    /* blah blah blah */

	for (str = buf; *fmt; ++fmt) {
		if (*fmt != '%') {
			*str++ = *fmt;
			continue;
		}

		/* parse the format */
        /* blah blah blah */

		switch (*fmt) {
		case 'c':
			*str++ = (unsigned char)va_arg(args, int); // Important
			continue;

        /* other cases */
        /* blah blah blah */
	}
	*str = '\0';
	return str - buf;
}

int printf(const char *fmt, ...)
{
	char printf_buf[1024];
	va_list args;
	int printed;

	va_start(args, fmt); // `fmt` indicates the symbol 
                         // of the last positional variable
	printed = vsprintf(printf_buf, fmt, args);
	va_end(args);

	puts(printf_buf);

	return printed;
}
```

To understand this, we may first try to implement `va_start`, `va_end`, `va_arg`
with our own codes. However, there is an issue that the second argument of
`va_start` is the name of a symbol which we cannot get through writing an
implementation of `va_start` in C language. Therefore, intervention in compile
time is required.

Actually, those functions related with variable arguments are built in compilers.
For example, in `clang/15.0.6/include/stdarg.h`, we have

```c
typedef __builtin_va_list va_list;
#define _VA_LIST
#endif
#define va_start(ap, param) __builtin_va_start(ap, param)
#define va_end(ap)          __builtin_va_end(ap)
#define va_arg(ap, type)    __builtin_va_arg(ap, type)
```

Distinct compilers implement these functions in different ways. However, System
V ABI dictates some standards that are widely accepted. As stated in [System V
Application Binary Interface AMD64 Architecture Processor Supplement (With LP64
and ILP32 Programming Models) Version
1.0](https://raw.githubusercontent.com/wiki/hjl-tools/x86-psABI/x86-64-psABI-1.0.pdf)
,

> The `va_start` macro initializes the structure as follows:
> 
> **reg_save_area** The element points to the start of the register save area.
>
> **overflow_arg_area** This pointer is used to fetch arguments passed on the
stack. It is initialized with the address of the first argument passed on the
stack, if any, and then always updated to point to the start of the next
argument on the stack.
>
> **gp_offset** The element holds the offset in bytes from reg_save_area to the
place where the next available general-purpose argument register is saved.
In case all argument registers have been exhausted, it is set to the value 48
(6 ∗ 8).
>
>**fp_offset** The element holds the offset in bytes from reg_save_area to the
place where the next available floating-point argument register is saved. In
case all argument registers have been exhausted, it is set to the value 304
(6 ∗ 8 + 16 ∗ 16).

**Explanation**: In System V ABI, the first six integer arguments prefer passing
in registers in the order of `rdi`, `rsi`, `rdx`, `rcx`, `r8`, `r9` and the
first 8 floating point arguments prefer passing in registers in the order of
`XMM0`, `XMM1`, ..., `XMM7`. If registers are exhausted, further arguments are
passed on the stack. That's why we need `reg_save_area` to store register values
and `overflow_arg_area` to store the arguments on the stack. Both `gp_offset`
and `fp_offset` reminds `va_arg` where to fetch the next value depending on the
second argument of `va_arg`. No matter how many registers are used, the prologue
of a variadic function always saves the value of its general purpose registers
`rdi`, `rsi`, `rdx`, `rcx`, `r8`, `r9` on the stack. So you can always see
something like this at the beginning of a variadic function.

```asm
	movq	%r9, -184(%rbp)
	movq	%r8, -192(%rbp)
	movq	%rcx, -200(%rbp)
	movq	%rdx, -208(%rbp)
	movq	%rsi, -216(%rbp)
	movl	%edi, -4(%rbp)
```

If I toss away the signature of `va_list`, is it possible to implement variadic
functionality in pure C language? Of course. Just pass in `char*` storing
all your arguments. But since the compilers have optimized this
scheme in assembly, why not use it?

2. Why is the first output `0x00000000ffffff80` instead of `0xffffffffffffff80`?

Answer: When a `char` or `bool` argument is passed in a variadic function, the
compiler is implicitly promoted to `long` or `unsigned long` (depending
on whether the variable is signed or unsigned) to fit the size of a register for
32-bit historical reasons. Then the promoted immediate literal is moved to a
64-bit general purpose register using the command `movl` which clears the upper
32 bits of the register as a result. That's why we get `0x00000000ffffff80`.

```asm
movl	$4294967168, %esi               # imm = 0xFFFFFF80
```

For detailed explanations, please read [this post](https://stackoverflow.com/a/28054417)


