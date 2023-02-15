---
title: "Help_of_MIPS"
date: 2023-02-15T23:57:51+08:00
draft: true
---

### Basic Instructions
|Command|Explanation|
|---|---|
|abs.d \$f2,\$f4|Floating point absolute value double precision : Set \$f2 to absolute value of \$f4, double precision|
|abs.s \$f0,\$f1|Floating point absolute value single precision : Set \$f0 to absolute value of \$f1, single precision|
|add \$t1,\$t2,\$t3|Addition with overflow : set \$t1 to (\$t2 plus \$t3)|
|add.d \$f2,\$f4,\$f6|Floating point addition double precision : Set \$f2 to double-precision floating point value of \$f4 plus \$f6|
|add.s \$f0,\$f1,\$f3|Floating point addition single precision : Set \$f0 to single-precision floating point value of \$f1 plus \$f3|
|addi \$t1,\$t2,-100|Addition immediate with overflow : set \$t1 to (\$t2 plus signed 16-bit immediate)|
|addiu \$t1,\$t2,-100|Addition immediate unsigned without overflow : set \$t1 to (\$t2 plus signed 16-bit immediate), no overflow|
|addu \$t1,\$t2,\$t3|Addition unsigned without overflow : set \$t1 to (\$t2 plus \$t3), no overflow|
|and \$t1,\$t2,\$t3|Bitwise AND : Set \$t1 to bitwise AND of \$t2 and \$t3|
|andi \$t1,\$t2,100|Bitwise AND immediate : Set \$t1 to bitwise AND of \$t2 and zero-extended 16-bit immediate|
|bc1f 1,label|Branch if specified FP condition flag false (BC1F, not BCLF) : If Coprocessor 1 condition flag specified by immediate is false (zero) then branch to statement at label's address|
|bc1f label|Branch if FP condition flag 0 false (BC1F, not BCLF) : If Coprocessor 1 condition flag 0 is false (zero) then branch to statement at label's address|
|bc1t 1,label|Branch if specified FP condition flag true (BC1T, not BCLT) : If Coprocessor 1 condition flag specified by immediate is true (one) then branch to statement at label's address|
|bc1t label|Branch if FP condition flag 0 true (BC1T, not BCLT) : If Coprocessor 1 condition flag 0 is true (one) then branch to statement at label's address|
|beq \$t1,\$t2,label|Branch if equal : Branch to statement at label's address if \$t1 and \$t2 are equal|
|bgez \$t1,label|Branch if greater than or equal to zero : Branch to statement at label's address if \$t1 is greater than or equal to zero|
|bgezal \$t1,label|Branch if greater then or equal to zero and link : If \$t1 is greater than or equal to zero, then set \$ra to the Program Counter and branch to statement at label's address|
|bgtz \$t1,label|Branch if greater than zero : Branch to statement at label's address if \$t1 is greater than zero|
|blez \$t1,label|Branch if less than or equal to zero : Branch to statement at label's address if \$t1 is less than or equal to zero|
|bltz \$t1,label|Branch if less than zero : Branch to statement at label's address if \$t1 is less than zero|
|bltzal \$t1,label|Branch if less than zero and link : If \$t1 is less than or equal to zero, then set \$ra to the Program Counter and branch to statement at label's address|
|bne \$t1,\$t2,label|Branch if not equal : Branch to statement at label's address if \$t1 and \$t2 are not equal|
|break|Break execution : Terminate program execution with exception|
|break 100|Break execution with code : Terminate program execution with specified exception code|
|c.eq.d \$f2,\$f4|Compare equal double precision : If \$f2 is equal to \$f4 (double-precision), set Coprocessor 1 condition flag 0 true else set it false|
|c.eq.d 1,\$f2,\$f4|Compare equal double precision : If \$f2 is equal to \$f4 (double-precision), set Coprocessor 1 condition flag specified by immediate to true else set it to false|
|c.eq.s \$f0,\$f1|Compare equal single precision : If \$f0 is equal to \$f1, set Coprocessor 1 condition flag 0 true else set it false|
|c.eq.s 1,\$f0,\$f1|Compare equal single precision : If \$f0 is equal to \$f1, set Coprocessor 1 condition flag specied by immediate to true else set it to false|
|c.le.d \$f2,\$f4|Compare less or equal double precision : If \$f2 is less than or equal to \$f4 (double-precision), set Coprocessor 1 condition flag 0 true else set it false|
|c.le.d 1,\$f2,\$f4|Compare less or equal double precision : If \$f2 is less than or equal to \$f4 (double-precision), set Coprocessor 1 condition flag specfied by immediate true else set it false|
|c.le.s \$f0,\$f1|Compare less or equal single precision : If \$f0 is less than or equal to \$f1, set Coprocessor 1 condition flag 0 true else set it false|
|c.le.s 1,\$f0,\$f1|Compare less or equal single precision : If \$f0 is less than or equal to \$f1, set Coprocessor 1 condition flag specified by immediate to true else set it to false|
|c.lt.d \$f2,\$f4|Compare less than double precision : If \$f2 is less than \$f4 (double-precision), set Coprocessor 1 condition flag 0 true else set it false|
|c.lt.d 1,\$f2,\$f4|Compare less than double precision : If \$f2 is less than \$f4 (double-precision), set Coprocessor 1 condition flag specified by immediate to true else set it to false|
|c.lt.s \$f0,\$f1|Compare less than single precision : If \$f0 is less than \$f1, set Coprocessor 1 condition flag 0 true else set it false|
|c.lt.s 1,\$f0,\$f1|Compare less than single precision : If \$f0 is less than \$f1, set Coprocessor 1 condition flag specified by immediate to true else set it to false|
|ceil.w.d \$f1,\$f2|Ceiling double precision to word : Set \$f1 to 32-bit integer ceiling of double-precision float in \$f2|
|ceil.w.s \$f0,\$f1|Ceiling single precision to word : Set \$f0 to 32-bit integer ceiling of single-precision float in \$f1|
|clo \$t1,\$t2|Count number of leading ones : Set \$t1 to the count of leading one bits in \$t2 starting at most significant bit position|
|clz \$t1,\$t2|Count number of leading zeroes : Set \$t1 to the count of leading zero bits in \$t2 starting at most significant bit positio|
|cvt.d.s \$f2,\$f1|Convert from single precision to double precision : Set \$f2 to double precision equivalent of single precision value in \$f1|
|cvt.d.w \$f2,\$f1|Convert from word to double precision : Set \$f2 to double precision equivalent of 32-bit integer value in \$f1|
|cvt.s.d \$f1,\$f2|Convert from double precision to single precision : Set \$f1 to single precision equivalent of double precision value in \$f2|
|cvt.s.w \$f0,\$f1|Convert from word to single precision : Set \$f0 to single precision equivalent of 32-bit integer value in \$f2|
|cvt.w.d \$f1,\$f2|Convert from double precision to word : Set \$f1 to 32-bit integer equivalent of double precision value in \$f2|
|cvt.w.s \$f0,\$f1|Convert from single precision to word : Set \$f0 to 32-bit integer equivalent of single precision value in \$f1|
|div \$t1,\$t2|Division with overflow : Divide \$t1 by \$t2 then set LO to quotient and HI to remainder (use mfhi to access HI, mflo to access LO)|
|div.d \$f2,\$f4,\$f6|Floating point division double precision : Set \$f2 to double-precision floating point value of \$f4 divided by \$f6|
|div.s \$f0,\$f1,\$f3|Floating point division single precision : Set \$f0 to single-precision floating point value of \$f1 divided by \$f3|
|divu \$t1,\$t2|Division unsigned without overflow : Divide unsigned \$t1 by \$t2 then set LO to quotient and HI to remainder (use mfhi to access HI, mflo to access LO)|
|eret|Exception return : Set Program Counter to Coprocessor 0 EPC register value, set Coprocessor Status register bit 1 (exception level) to zero|
|floor.w.d \$f1,\$f2|Floor double precision to word : Set \$f1 to 32-bit integer floor of double-precision float in \$f2|
|floor.w.s \$f0,\$f1|Floor single precision to word : Set \$f0 to 32-bit integer floor of single-precision float in \$f1|
|j target|Jump unconditionally : Jump to statement at target address|
|jal target|Jump and link : Set \$ra to Program Counter (return address) then jump to statement at target address|
|jalr \$t1|Jump and link register : Set \$ra to Program Counter (return address) then jump to statement whose address is in \$t1|
|jalr \$t1,\$t2|Jump and link register : Set \$t1 to Program Counter (return address) then jump to statement whose address is in \$t2|
|jr \$t1|Jump register unconditionally : Jump to statement whose address is in \$t1|
|lb \$t1,-100(\$t2)|Load byte : Set \$t1 to sign-extended 8-bit value from effective memory byte address|
|lbu \$t1,-100(\$t2)|Load byte unsigned : Set \$t1 to zero-extended 8-bit value from effective memory byte address|
|ldc1 \$f2,-100(\$t2)|Load double word Coprocessor 1 (FPU)) : Set \$f2 to 64-bit value from effective memory doubleword address|
|lh \$t1,-100(\$t2)|Load halfword : Set \$t1 to sign-extended 16-bit value from effective memory halfword address|
|lhu \$t1,-100(\$t2)|Load halfword unsigned : Set \$t1 to zero-extended 16-bit value from effective memory halfword address|
|ll \$t1,-100(\$t2)|Load linked : Paired with Store Conditional (sc) to perform atomic read-modify-write.  Treated as equivalent to Load Word (lw) because MARS does not simulate multiple processors.|
|lui \$t1,100|Load upper immediate : Set high-order 16 bits of \$t1 to 16-bit immediate and low-order 16 bits to 0|
|lw \$t1,-100(\$t2)|Load word : Set \$t1 to contents of effective memory word address|
|lwc1 \$f1,-100(\$t2)|Load word into Coprocessor 1 (FPU) : Set \$f1 to 32-bit value from effective memory word address|
|lwl \$t1,-100(\$t2)|Load word left : Load from 1 to 4 bytes left-justified into \$t1, starting with effective memory byte address and continuing through the low-order byte of its word|
|lwr \$t1,-100(\$t2)|Load word right : Load from 1 to 4 bytes right-justified into \$t1, starting with effective memory byte address and continuing through the high-order byte of its word|
|madd \$t1,\$t2|Multiply add : Multiply \$t1 by \$t2 then increment HI by high-order 32 bits of product, increment LO by low-order 32 bits of product (use mfhi to access HI, mflo to access LO)|
|maddu \$t1,\$t2|Multiply add unsigned : Multiply \$t1 by \$t2 then increment HI by high-order 32 bits of product, increment LO by low-order 32 bits of product, unsigned (use mfhi to access HI, mflo to access LO)|
|mfc0 \$t1,\$8|Move from Coprocessor 0 : Set \$t1 to the value stored in Coprocessor 0 register \$8|
|mfc1 \$t1,\$f1|Move from Coprocessor 1 (FPU) : Set \$t1 to value in Coprocessor 1 register \$f1|
|mfhi \$t1|Move from HI register : Set \$t1 to contents of HI (see multiply and divide operations)|
|mflo \$t1|Move from LO register : Set \$t1 to contents of LO (see multiply and divide operations)|
|mov.d \$f2,\$f4|Move floating point double precision : Set double precision \$f2 to double precision value in \$f4|
|mov.s \$f0,\$f1|Move floating point single precision : Set single precision \$f0 to single precision value in \$f1|
|movf \$t1,\$t2|Move if FP condition flag 0 false : Set \$t1 to \$t2 if FPU (Coprocessor 1) condition flag 0 is false (zero)|
|movf \$t1,\$t2,1|Move if specified FP condition flag false : Set \$t1 to \$t2 if FPU (Coprocessor 1) condition flag specified by the immediate is false (zero)|
|movf.d \$f2,\$f4|Move floating point double precision : If condition flag 0 false, set double precision \$f2 to double precision value in \$f4|
|movf.d \$f2,\$f4,1|Move floating point double precision : If condition flag specified by immediate is false, set double precision \$f2 to double precision value in \$f4|
|movf.s \$f0,\$f1|Move floating point single precision : If condition flag 0 is false, set single precision \$f0 to single precision value in \$f1|
|movf.s \$f0,\$f1,1|Move floating point single precision : If condition flag specified by immediate is false, set single precision \$f0 to single precision value in \$f1e|
|movn \$t1,\$t2,\$t3|Move conditional not zero : Set \$t1 to \$t2 if \$t3 is not zero|
|movn.d \$f2,\$f4,\$t3|Move floating point double precision : If \$t3 is not zero, set double precision \$f2 to double precision value in \$f4|
|movn.s \$f0,\$f1,\$t3|Move floating point single precision : If \$t3 is not zero, set single precision \$f0 to single precision value in \$f1|
|movt \$t1,\$t2|Move if FP condition flag 0 true : Set \$t1 to \$t2 if FPU (Coprocessor 1) condition flag 0 is true (one)|
|movt \$t1,\$t2,1|Move if specfied FP condition flag true : Set \$t1 to \$t2 if FPU (Coprocessor 1) condition flag specified by the immediate is true (one)|
|movt.d \$f2,\$f4|Move floating point double precision : If condition flag 0 true, set double precision \$f2 to double precision value in \$f4|
|movt.d \$f2,\$f4,1|Move floating point double precision : If condition flag specified by immediate is true, set double precision \$f2 to double precision value in \$f4e|
|movt.s \$f0,\$f1|Move floating point single precision : If condition flag 0 is true, set single precision \$f0 to single precision value in \$f1e|
|movt.s \$f0,\$f1,1|Move floating point single precision : If condition flag specified by immediate is true, set single precision \$f0 to single precision value in \$f1e|
|movz \$t1,\$t2,\$t3|Move conditional zero : Set \$t1 to \$t2 if \$t3 is zero|
|movz.d \$f2,\$f4,\$t3|Move floating point double precision : If \$t3 is zero, set double precision \$f2 to double precision value in \$f4|
|movz.s \$f0,\$f1,\$t3|Move floating point single precision : If \$t3 is zero, set single precision \$f0 to single precision value in \$f1|
|msub \$t1,\$t2|Multiply subtract : Multiply \$t1 by \$t2 then decrement HI by high-order 32 bits of product, decrement LO by low-order 32 bits of product (use mfhi to access HI, mflo to access LO)|
|msubu \$t1,\$t2|Multiply subtract unsigned : Multiply \$t1 by \$t2 then decrement HI by high-order 32 bits of product, decement LO by low-order 32 bits of product, unsigned (use mfhi to access HI, mflo to access LO)|
|mtc0 \$t1,\$8|Move to Coprocessor 0 : Set Coprocessor 0 register \$8 to value stored in \$t1|
|mtc1 \$t1,\$f1|Move to Coprocessor 1 (FPU) : Set Coprocessor 1 register \$f1 to value in \$t1|
|mthi \$t1|Move to HI registerr : Set HI to contents of \$t1 (see multiply and divide operations)|
|mtlo \$t1|Move to LO register : Set LO to contents of \$t1 (see multiply and divide operations)|
|mul \$t1,\$t2,\$t3|Multiplication without overflow  : Set HI to high-order 32 bits, LO and \$t1 to low-order 32 bits of the product of \$t2 and \$t3 (use mfhi to access HI, mflo to access LO)|
|mul.d \$f2,\$f4,\$f6|Floating point multiplication double precision : Set \$f2 to double-precision floating point value of \$f4 times \$f6|
|mul.s \$f0,\$f1,\$f3|Floating point multiplication single precision : Set \$f0 to single-precision floating point value of \$f1 times \$f3|
|mult \$t1,\$t2|Multiplication : Set hi to high-order 32 bits, lo to low-order 32 bits of the product of \$t1 and \$t2 (use mfhi to access hi, mflo to access lo)|
|multu \$t1,\$t2|Multiplication unsigned : Set HI to high-order 32 bits, LO to low-order 32 bits of the product of unsigned \$t1 and \$t2 (use mfhi to access HI, mflo to access LO)|
|neg.d \$f2,\$f4|Floating point negate double precision : Set double precision \$f2 to negation of double precision value in \$f4|
|neg.s \$f0,\$f1|Floating point negate single precision : Set single precision \$f0 to negation of single precision value in \$f1|
|nop|Null operation : machine code is all zeroes|
|nor \$t1,\$t2,\$t3|Bitwise NOR : Set \$t1 to bitwise NOR of \$t2 and \$t3|
|or \$t1,\$t2,\$t3|Bitwise OR : Set \$t1 to bitwise OR of \$t2 and \$t3|
|ori \$t1,\$t2,100|Bitwise OR immediate : Set \$t1 to bitwise OR of \$t2 and zero-extended 16-bit immediate|
|round.w.d \$f1,\$f2|Round double precision to word : Set \$f1 to 32-bit integer round of double-precision float in \$f2|
|round.w.s \$f0,\$f1|Round single precision to word : Set \$f0 to 32-bit integer round of single-precision float in \$f1|
|sb \$t1,-100(\$t2)|Store byte : Store the low-order 8 bits of \$t1 into the effective memory byte address|
|sc \$t1,-100(\$t2)|Store conditional : Paired with Load Linked (ll) to perform atomic read-modify-write.  Stores \$t1 value into effective address, then sets \$t1 to 1 for success.  Always succeeds because MARS does not simulate multiple processors.|
|sdc1 \$f2,-100(\$t2)|Store double word from Coprocessor 1 (FPU)) : Store 64 bit value in \$f2 to effective memory doubleword address|
|sh \$t1,-100(\$t2)|Store halfword : Store the low-order 16 bits of \$t1 into the effective memory halfword address|
|sll \$t1,\$t2,10|Shift left logical : Set \$t1 to result of shifting \$t2 left by number of bits specified by immediate|
|sllv \$t1,\$t2,\$t3|Shift left logical variable : Set \$t1 to result of shifting \$t2 left by number of bits specified by value in low-order 5 bits of \$t3|
|slt \$t1,\$t2,\$t3|Set less than : If \$t2 is less than \$t3, then set \$t1 to 1 else set \$t1 to 0|
|slti \$t1,\$t2,-100|Set less than immediate : If \$t2 is less than sign-extended 16-bit immediate, then set \$t1 to 1 else set \$t1 to 0|
|sltiu \$t1,\$t2,-100|Set less than immediate unsigned : If \$t2 is less than  sign-extended 16-bit immediate using unsigned comparison, then set \$t1 to 1 else set \$t1 to 0|
|sltu \$t1,\$t2,\$t3|Set less than unsigned : If \$t2 is less than \$t3 using unsigned comparision, then set \$t1 to 1 else set \$t1 to 0|
|sqrt.d \$f2,\$f4|Square root double precision : Set \$f2 to double-precision floating point square root of \$f4|
|sqrt.s \$f0,\$f1|Square root single precision : Set \$f0 to single-precision floating point square root of \$f1|
|sra \$t1,\$t2,10|Shift right arithmetic : Set \$t1 to result of sign-extended shifting \$t2 right by number of bits specified by immediate|
|srav \$t1,\$t2,\$t3|Shift right arithmetic variable : Set \$t1 to result of sign-extended shifting \$t2 right by number of bits specified by value in low-order 5 bits of \$t3|
|srl \$t1,\$t2,10|Shift right logical : Set \$t1 to result of shifting \$t2 right by number of bits specified by immediate|
|srlv \$t1,\$t2,\$t3|Shift right logical variable : Set \$t1 to result of shifting \$t2 right by number of bits specified by value in low-order 5 bits of \$t3|
|sub \$t1,\$t2,\$t3|Subtraction with overflow : set \$t1 to (\$t2 minus \$t3)|
|sub.d \$f2,\$f4,\$f6|Floating point subtraction double precision : Set \$f2 to double-precision floating point value of \$f4 minus \$f6|
|sub.s \$f0,\$f1,\$f3|Floating point subtraction single precision : Set \$f0 to single-precision floating point value of \$f1  minus \$f3|
|subu \$t1,\$t2,\$t3|Subtraction unsigned without overflow : set \$t1 to (\$t2 minus \$t3), no overflow|
|sw \$t1,-100(\$t2)|Store word : Store contents of \$t1 into effective memory word address|
|swc1 \$f1,-100(\$t2)|Store word from Coprocesor 1 (FPU) : Store 32 bit value in \$f1 to effective memory word address|
|swl \$t1,-100(\$t2)|Store word left : Store high-order 1 to 4 bytes of \$t1 into memory, starting with effective byte address and continuing through the low-order byte of its word|
|swr \$t1,-100(\$t2)|Store word right : Store low-order 1 to 4 bytes of \$t1 into memory, starting with high-order byte of word containing effective byte address and continuing through that byte address|
|syscall|Issue a system call : Execute the system call specified by value in \$v0|
|teq \$t1,\$t2|Trap if equal : Trap if \$t1 is equal to \$t2|
|teqi \$t1,-100|Trap if equal to immediate : Trap if \$t1 is equal to sign-extended 16 bit immediate|
|tge \$t1,\$t2|Trap if greater or equal : Trap if \$t1 is greater than or equal to \$t2|
|tgei \$t1,-100|Trap if greater than or equal to immediate : Trap if \$t1 greater than or equal to sign-extended 16 bit immediate|
|tgeiu \$t1,-100|Trap if greater or equal to immediate unsigned : Trap if \$t1 greater than or equal to sign-extended 16 bit immediate, unsigned comparison|
|tgeu \$t1,\$t2|Trap if greater or equal unsigned : Trap if \$t1 is greater than or equal to \$t2 using unsigned comparision|
|tlt \$t1,\$t2|Trap if less than: Trap if \$t1 less than \$t2|
|tlti \$t1,-100|Trap if less than immediate : Trap if \$t1 less than sign-extended 16-bit immediate|
|tltiu \$t1,-100|Trap if less than immediate unsigned : Trap if \$t1 less than sign-extended 16-bit immediate, unsigned comparison|
|tltu \$t1,\$t2|Trap if less than unsigned : Trap if \$t1 less than \$t2, unsigned comparison|
|tne \$t1,\$t2|Trap if not equal : Trap if \$t1 is not equal to \$t2|
|tnei \$t1,-100|Trap if not equal to immediate : Trap if \$t1 is not equal to sign-extended 16 bit immediate|
|trunc.w.d \$f1,\$f2|Truncate double precision to word : Set \$f1 to 32-bit integer truncation of double-precision float in \$f2|
|trunc.w.s \$f0,\$f1|Truncate single precision to word : Set \$f0 to 32-bit integer truncation of single-precision float in \$f1|
|xor \$t1,\$t2,\$t3|Bitwise XOR (exclusive OR) : Set \$t1 to bitwise XOR of \$t2 and \$t3|
|xori \$t1,\$t2,100|Bitwise XOR immediate : Set \$t1 to bitwise XOR of \$t2 and zero-extended 16-bit immediate|
### Extended(Pseudo) Instructions
<details><summary>File format</summary>File format:
  Each line contains specification for one pseudo-op, including optional description.
  First item is source statement syntax, specified in same "example" parser format used for regular instructions.
  Source statement specification ends with a tab.  It is followed by a tab-separated list of basic instruction
  templates to complete and substitute for the pseudo-op.
  Format for specifying syntax of templates is different from specifying syntax of source statement:
     (n=0,1,2,3,...) is token position in source statement (operator is token 0, parentheses are tokens but commas aren't)
     RGn means substitute register found in n'th token of source statement
     NRn means substitute next higher register than the one in n'th token of source code
     OPn means substitute n'th token of source code as is
     LLn means substitute low order 16-bits from label address in source token n.
     LLnU means substitute low order 16-bits (unsigned) from label address in source token n.
     LLnPm (m=1,2,3,4) means substitute low order 16-bits from label address in source token n, after adding m.
     LHn means substitute high order 16-bits from label address in source token n. Must add 1 if address bit 15 is 1. 
     LHnPm (m=1,2,3,4) means substitute high order 16-bits from label address in source token n, after adding m. Must then add 1 if bit 15 is 1. 
     VLn means substitute low order 16-bits from 32-bit value in source token n.
     VLnU means substitute low order 16-bits (unsigned) from 32-bit value in source token n.
     VLnPm (m=1,2,3,4) means substitute low order 16-bits from 32-bit value in source token n, after adding m to value.
     VLnPmU (m=1,2,3,4) means substitute low order 16-bits(unsigned) from 32-bit value in source token n, after adding m to value.
     VHLn means substitute high order 16-bits from 32-bit value in source token n.  Use this if later combined with low order 16-bits using "ori \$1,\$1,VLnU". See logical and branch operations.
     VHn means substitute high order 16-bits from 32-bit value in source token n, then add 1 if value's bit 15 is 1.  Use this only if later instruction uses VLn(\$1) to calculate 32-bit address.  See loads and stores.
     VHLnPm (m=1,2,3,4) means substitute high order 16-bits from 32-bit value in source token n, after adding m.  See VHLn.
     VHnPm (m=1,2,3,4) means substitute high order 16-bits from 32-bit value in source token n, after adding m. Must then add 1 if bit 15 is 1. See VHn.
     LLP is similar to LLn, but is needed for "label+100000" address offset. Immediate is added before taking low order 16. 
     LLPU is similar to LLn, but is needed for "label+100000" address offset. Immediate is added before taking low order 16 (unsigned). 
     LLPPm (m=1,2,3,4) is similar to LLP except m is added along with immediate before taking low order 16. 
     LHPA is similar to LHn, but is needed for "label+100000" address offset. Immediate is added before taking high order 16.
     LHPN is similar to LHPA, used only by "la" instruction. Address resolved by "ori" so do not add 1 if bit 15 is 1.
     LHPAPm (m=1,2,3,4) is similar to LHPA except value m is added along with immediate before taking high order 16.
     LHL means substitute high order 16-bits from label address in token 2 of "la" (load address) source statement.
     LAB means substitute textual label from last token of source statement.  Used for various branches.
     S32 means substitute the result of subtracting the constant value in last token from 32.  Used by "ror", "rol".
     DBNOP means Delayed Branching NOP - generate a "nop" instruction but only if delayed branching is enabled.  Added in 3.4.1 release.
     BROFFnm means substitute n if delayed branching is NOT enabled otherwise substitute m.  n and m are single digit numbers indicating constant branch offset (in words).  Added in 3.4.1 release.
     COMPACT is a marker to separate the default template from a second template optimized for 16-bit addresses.  See loads and stores having (data) label operands.
</details>

|Command|Explanation|Expand|
|---|---|---|
|abs \$t1,\$t2|ABSolute value : Set \$t1 to absolute value of \$t2 (algorithm from Hacker's Delight) |sra \$1, RG2, 31 xor RG1, \$1, RG2 subu RG1, RG1, \$1 |
|add \$t1,\$t2,-100|ADDition : set \$t1 to (\$t2 plus 16-bit immediate)|addi RG1, RG2, VL3 |
|add \$t1,\$t2,100000|ADDition : set \$t1 to (\$t2 plus 32-bit immediate)|lui \$1, VHL3 ori \$1, \$1, VL3U add RG1, RG2, \$1 |
|addi \$t1,\$t2,100000|ADDition Immediate : set \$t1 to (\$t2 plus 32-bit immediate)|lui \$1, VHL3 ori \$1, \$1, VL3U add RG1, RG2, \$1 |
|addiu \$t1,\$t2,100000|ADDition Immediate Unsigned: set \$t1 to (\$t2 plus 32-bit immediate), no overflow|lui \$1, VHL3 ori \$1, \$1, VL3U addu RG1, RG2, \$1 |
|addu \$t1,\$t2,100000|ADDition Unsigned : set \$t1 to (\$t2 plus 32-bit immediate), no overflow|lui \$1, VHL3 ori \$1, \$1, VL3U addu RG1, RG2, \$1 |
|and \$t1,\$t2,100|AND : set \$t1 to (\$t2 bitwise-AND 16-bit unsigned immediate)|andi RG1, RG2, VL3U |
|and \$t1,100|AND : set \$t1 to (\$t1 bitwise-AND 16-bit unsigned immediate)|andi RG1, RG1, VL2U |
|andi \$t1,\$t2,100000|AND Immediate : set \$t1 to (\$t2 bitwise-AND 32-bit immediate)|lui \$1, VHL3 ori \$1, \$1, VL3U and RG1, RG2, \$1 |
|andi \$t1,100|AND Immediate : set \$t1 to (\$t1 bitwise-AND 16-bit unsigned immediate)|andi RG1, RG1, VL2U |
|andi \$t1,100000|AND Immediate : set \$t1 to (\$t1 bitwise-AND 32-bit immediate)|lui \$1, VHL2 ori \$1, \$1, VL2U and RG1, RG1, \$1 |
|b label|Branch : Branch to statement at label unconditionally|bgez \$0, LAB |
|beq \$t1,-100,label|Branch if EQual : Branch to statement at label if \$t1 is equal to 16-bit immediate|addi \$1, \$0, VL2 beq \$1, RG1, LAB |
|beq \$t1,100000,label|Branch if EQual : Branch to statement at label if \$t1 is equal to 32-bit immediate |lui \$1, VHL2 ori \$1, \$1, VL2U beq \$1, RG1, LAB |
|beqz \$t1,label|Branch if EQual Zero : Branch to statement at label if \$t1 is equal to zero|beq RG1, \$0, LAB |
|bge \$t1,\$t2,label|Branch if Greater or Equal : Branch to statement at label if \$t1 is greater or equal to \$t2|slt \$1, RG1, RG2 beq \$1, \$0, LAB |
|bge \$t1,-100,label|Branch if Greater or Equal : Branch to statement at label if \$t1 is greater or equal to 16-bit immediate |slti \$1, RG1, VL2 beq \$1, \$0, LAB |
|bge \$t1,100000,label|Branch if Greater or Equal : Branch to statement at label if \$t1 is greater or equal to 32-bit immediate |lui \$1, VHL2 ori \$1, \$1, VL2U slt \$1, RG1, \$1 beq \$1, \$0, LAB |
|bgeu \$t1,\$t2,label|Branch if Greater or Equal Unsigned : Branch to statement at label if \$t1 is greater or equal to \$t2 (unsigned compare)|sltu \$1, RG1, RG2 beq \$1, \$0, LAB |
|bgeu \$t1,-100,label|Branch if Greater or Equal Unsigned : Branch to statement at label if \$t1 is greater or equal to 16-bit immediate (unsigned compare)|sltiu \$1, RG1, VL2 beq \$1, \$0, LAB |
|bgeu \$t1,100000,label|Branch if Greater or Equal Unsigned : Branch to statement at label if \$t1 is greater or equal to 32-bit immediate (unsigned compare)|lui \$1, VHL2 ori \$1, \$1, VL2U sltu \$1, RG1, \$1 beq \$1, \$0, LAB |
|bgt \$t1,\$t2,label|Branch if Greater Than : Branch to statement at label if \$t1 is greater than \$t2|slt \$1, RG2, RG1 bne \$1, \$0, LAB |
|bgt \$t1,-100,label|Branch if Greater Than : Branch to statement at label if \$t1 is greater than 16-bit immediate |addi \$1, \$0, VL2 slt \$1, \$1, RG1 bne \$1, \$0, LAB |
|bgt \$t1,100000,label|Branch if Greater Than : Branch to statement at label if \$t1 is greater than 32-bit immediate|lui \$1, VHL2P1 ori \$1, \$1, VL2P1U slt \$1, RG1, \$1 beq \$1, \$0, LAB |
|bgtu \$t1,\$t2,label|Branch if Greater Than Unsigned: Branch to statement at label if \$t1 is greater than \$t2 (unsigned compare)|sltu \$1, RG2, RG1 bne \$1, \$0, LAB |
|bgtu \$t1,-100,label|Branch if Greater Than Unsigned: Branch to statement at label if \$t1 is greater than 16-bit immediate (unsigned compare)|addi \$1, \$0, VL2 sltu \$1, \$1, RG1 bne \$1, \$0, LAB |
|bgtu \$t1,100000,label|Branch if Greater Than Unsigned: Branch to statement at label if \$t1 is greater than 16-bit immediate (unsigned compare)|lui \$1, VHL2 ori \$1, \$1, VL2U sltu \$1, \$1, RG1 bne \$1, \$0, LAB |
|ble \$t1,\$t2,label|Branch if Less or Equal : Branch to statement at label if \$t1 is less than or equal to \$t2|slt \$1, RG2, RG1 beq \$1, \$0, LAB |
|ble \$t1,-100,label|Branch if Less or Equal : Branch to statement at label if \$t1 is less than or equal to 16-bit immediate|addi \$1, RG1, -1 slti \$1, \$1, VL2 bne \$1, \$0, LAB |
|ble \$t1,100000,label|Branch if Less or Equal : Branch to statement at label if \$t1 is less than or equal to 32-bit immediate |lui \$1, VHL2P1 ori \$1, \$1, VL2P1U slt \$1, RG1, \$1 bne \$1, \$0, LAB |
|bleu \$t1,\$t2,label|Branch if Less or Equal Unsigned : Branch to statement at label if \$t1 is less than or equal to \$t2 (unsigned compare)|sltu \$1, RG2, RG1 beq \$1, \$0, LAB |
|bleu \$t1,-100,label|Branch if Less or Equal Unsigned : Branch to statement at label if \$t1 is less than or equal to 16-bit immediate (unsigned compare)|addi \$1, \$0, VL2 sltu \$1, \$1, RG1 beq \$1, \$0, LAB |
|bleu \$t1,100000,label|Branch if Less or Equal Unsigned : Branch to statement at label if \$t1 is less than or equal to 32-bit immediate (unsigned compare)|lui \$1, VHL2 ori \$1, \$1, VL2U sltu \$1, \$1, RG1 beq \$1, \$0, LAB |
|blt \$t1,\$t2,label|Branch if Less Than : Branch to statement at label if \$t1 is less than \$t2|slt \$1, RG1, RG2 bne \$1, \$0, LAB |
|blt \$t1,-100,label|Branch if Less Than : Branch to statement at label if \$t1 is less than 16-bit immediate|slti \$1, RG1, VL2 bne \$1, \$0, LAB |
|blt \$t1,100000,label|Branch if Less Than : Branch to statement at label if \$t1 is less than 32-bit immediate|lui \$1, VHL2 ori \$1, \$1, VL2U slt \$1, RG1, \$1 bne \$1, \$0, LAB |
|bltu \$t1,\$t2,label|Branch if Less Than Unsigned : Branch to statement at label if \$t1 is less than \$t2|sltu \$1, RG1, RG2 bne \$1, \$0, LAB |
|bltu \$t1,-100,label|Branch if Less Than Unsigned : Branch to statement at label if \$t1 is less than 16-bit immediate |sltiu \$1, RG1, VL2 bne \$1, \$0, LAB |
|bltu \$t1,100000,label|Branch if Less Than Unsigned : Branch to statement at label if \$t1 is less than 32-bit immediate|lui \$1, VHL2 ori \$1, \$1, VL2U sltu \$1, RG1, \$1 bne \$1, \$0, LAB |
|bne \$t1,-100,label|Branch if Not Equal : Branch to statement at label if \$t1 is not equal to 16-bit immediate|addi \$1, \$0, VL2 bne \$1, RG1, LAB |
|bne \$t1,100000,label|Branch if Not Equal : Branch to statement at label if \$t1 is not equal to 32-bit immediate |lui \$1, VHL2 ori \$1, \$1, VL2U bne \$1, RG1, LAB |
|bnez \$t1,label|Branch if Not Equal Zero : Branch to statement at label if \$t1 is not equal to zero|bne RG1, \$0, LAB |
|div \$t1,\$t2,\$t3|DIVision : Set \$t1 to (\$t2 divided by \$t3, integer division)|bne RG3, \$0, BROFF12 DBNOP break div RG2, RG3 mflo RG1 |
|div \$t1,\$t2,-100|DIVision : Set \$t1 to (\$t2 divided by 16-bit immediate, integer division)|addi \$1, \$0, VL3 div RG2, \$1 mflo RG1 |
|div \$t1,\$t2,100000|DIVision : Set \$t1 to (\$t2 divided by 32-bit immediate, integer division)|lui \$1, VHL3 ori \$1, \$1, VL3U div RG2, \$1 mflo RG1 |
|divu \$t1,\$t2,\$t3|DIVision Unsigned :  Set \$t1 to (\$t2 divided by \$t3, unsigned integer division)|bne RG3, \$0, BROFF12 DBNOP break divu RG2, RG3 mflo RG1 |
|divu \$t1,\$t2,-100|DIVision Unsigned :  Set \$t1 to (\$t2 divided by 16-bit immediate, unsigned integer division)|addi \$1, \$0, VL3 divu RG2, \$1 mflo RG1 |
|divu \$t1,\$t2,100000|DIVision Unsigned :  Set \$t1 to (\$t2 divided by 32-bit immediate, unsigned integer division)|lui \$1, VHL3 ori \$1, \$1, VL3U divu RG2, \$1 mflo RG1 |
|l.d \$f2,(\$t2)|Load floating point Double precision : Set \$f2 and \$f3 register pair to 64-bit value at effective memory doubleword address|ldc1 RG1,0(RG3) |
|l.d \$f2,-100|Load floating point Double precision : Set \$f2 and \$f3 register pair to 64-bit value at effective memory doubleword address|ldc1 RG1,VL2(\$0) |
|l.d \$f2,100000|Load floating point Double precision : Set \$f2 and \$f3 register pair to 64-bit value at effective memory doubleword address|lui \$1, VH2 ldc1 RG1,VL2(\$1) |
|l.d \$f2,100000(\$t2)|Load floating point Double precision : Set \$f2 and \$f3 register pair to 64-bit value at effective memory doubleword address|lui \$1, VH2 addu \$1, \$1, RG4 ldc1 RG1, VL2(\$1) |
|l.d \$f2,label|Load floating point Double precision : Set \$f2 and \$f3 register pair to 64-bit value at effective memory doubleword address|lui \$1, LH2 ldc1 RG1, LL2(\$1) COMPACT ldc1 RG1, LL2(\$0) |
|l.d \$f2,label(\$t2)|Load floating point Double precision : Set \$f2 and \$f3 register pair to 64-bit value at effective memory doubleword address|lui \$1, LH2 addu \$1, \$1, RG4 ldc1 RG1, LL2(\$1) COMPACT ldc1 RG1, LL2(RG4) |
|l.d \$f2,label+100000|Load floating point Double precision : Set \$f2 and \$f3 register pair to 64-bit value at effective memory doubleword address|lui \$1, LHPA ldc1 RG1, LLP(\$1) |
|l.d \$f2,label+100000(\$t2)|Load floating point Double precision : Set \$f2 and \$f3 register pair to 64-bit value at effective memory doubleword address|lui \$1, LHPA addu \$1, \$1, RG6 ldc1 RG1, LLP(\$1) |
|l.s \$f1,(\$t2)|Load floating point Single precision : Set \$f1 to 32-bit value at effective memory word address|lwc1 RG1,0(RG3) |
|l.s \$f1,-100|Load floating point Single precision : Set \$f1 to 32-bit value at effective memory word address|lwc1 RG1,VL2(\$0) |
|l.s \$f1,100000|Load floating point Single precision : Set \$f1 to 32-bit value at effective memory word address|lui \$1, VH2 lwc1 RG1,VL2(\$1) |
|l.s \$f1,100000(\$t2)|Load floating point Single precision : Set \$f1 to 32-bit value at effective memory word address|lui \$1, VH2 addu \$1, \$1, RG4 lwc1 RG1, VL2(\$1) |
|l.s \$f1,label|Load floating point Single precision : Set \$f1 to 32-bit value at effective memory word address|lui \$1, LH2 lwc1 RG1, LL2(\$1) COMPACT lwc1 RG1, LL2(\$0) |
|l.s \$f1,label(\$t2)|Load floating point Single precision : Set \$f1 to 32-bit value at effective memory word address|lui \$1, LH2 addu \$1, \$1, RG4 lwc1 RG1, LL2(\$1) COMPACT lwc1 RG1, LL2(RG4) |
|l.s \$f1,label+100000|Load floating point Single precision : Set \$f1 to 32-bit value at effective memory word address|lui \$1, LHPA lwc1 RG1, LLP(\$1) |
|l.s \$f1,label+100000(\$t2)|Load floating point Single precision : Set \$f1 to 32-bit value at effective memory word address|lui \$1, LHPA addu \$1, \$1, RG6 lwc1 RG1, LLP(\$1) |
|la \$t1,(\$t2)|Load Address : Set \$t1 to contents of \$t2|addi RG1, RG3, 0 |
|la \$t1,-100|Load Address : Set \$t1 to 16-bit immediate (sign-extended) |addiu RG1, \$0, VL2 |
|la \$t1,100|Load Address : Set \$t1 to 16-bit immediate (zero-extended) |ori RG1, \$0, VL2U |
|la \$t1,100(\$t2)|Load Address : Set \$t1 to sum (of \$t2 and 16-bit immediate)|ori \$1, \$0, VL2U add RG1, RG4, \$1 |
|la \$t1,100000|Load Address : Set \$t1 to 32-bit immediate|lui \$1, VHL2 ori RG1, \$1, VL2U |
|la \$t1,100000(\$t2)|Load Address : Set \$t1 to sum (of \$t2 and 32-bit immediate)|lui \$1, VHL2 ori \$1, \$1, VL2U add RG1, RG4, \$1 |
|la \$t1,label|Load Address : Set \$t1 to label's address|lui \$1, LHL ori RG1, \$1, LL2U COMPACT addi RG1, \$0, LL2 |
|la \$t1,label(\$t2)|Load Address : Set \$t1 to sum (of \$t2 and label's address)|lui \$1, LHL ori \$1, \$1, LL2U add RG1, RG4, \$1 COMPACT addi RG1, RG4, LL2 |
|la \$t1,label+100000|Load Address : Set \$t1 to sum (of label's address and 32-bit immediate)|lui \$1, LHPN ori RG1, \$1, LLPU |
|la \$t1,label+100000(\$t2)|Load Address : Set \$t1 to sum (of label's address, 32-bit immediate, and \$t2)|lui \$1, LHPN ori \$1, \$1, LLPU add RG1, RG6, \$1 |
|lb \$t1,(\$t2)|Load Byte : Set \$t1 to sign-extended 8-bit value from effective memory byte address|lb RG1,0(RG3) |
|lb \$t1,-100|Load Byte : Set \$t1 to sign-extended 8-bit value from effective memory byte address|lb RG1, VL2(\$0) |
|lb \$t1,100|Load Byte : Set \$t1 to sign-extended 8-bit value from effective memory byte address|ori \$1, \$0, VL2U lb RG1, 0(\$1) |
|lb \$t1,100(\$t2)|Load Byte : Set \$t1 to sign-extended 8-bit value from effective memory byte address|ori \$1, \$0, VL2U addu \$1, \$1, RG4 lb RG1, 0(\$1) |
|lb \$t1,100000|Load Byte : Set \$t1 to sign-extended 8-bit value from effective memory byte address|lui \$1, VH2 lb RG1,VL2(\$1) |
|lb \$t1,100000(\$t2)|Load Byte : Set \$t1 to sign-extended 8-bit value from effective memory byte address|lui \$1, VH2 addu \$1, \$1, RG4 lb RG1, VL2(\$1) |
|lb \$t1,label|Load Byte : Set \$t1 to sign-extended 8-bit value from effective memory byte address|lui \$1, LH2 lb RG1, LL2(\$1) COMPACT lb RG1, LL2(\$0) |
|lb \$t1,label(\$t2)|Load Byte : Set \$t1 to sign-extended 8-bit value from effective memory byte address|lui \$1, LH2 addu \$1, \$1, RG4 lb RG1, LL2(\$1) COMPACT lb RG1, LL2(RG4) |
|lb \$t1,label+100000|Load Byte : Set \$t1 to sign-extended 8-bit value from effective memory byte address|lui \$1, LHPA lb RG1, LLP(\$1) |
|lb \$t1,label+100000(\$t2)|Load Byte : Set \$t1 to sign-extended 8-bit value from effective memory byte address|lui \$1, LHPA addu \$1, \$1, RG6 lb RG1, LLP(\$1) |
|lbu \$t1,(\$t2)|Load Byte Unsigned : Set \$t1 to zero-extended 8-bit value from effective memory byte address|lbu RG1,0(RG3) |
|lbu \$t1,-100|Load Byte Unsigned : Set \$t1 to zero-extended 8-bit value from effective memory byte address|lbu RG1,VL2(\$0) |
|lbu \$t1,100|Load Byte Unsigned : Set \$t1 to zero-extended 8-bit value from effective memory byte address|ori \$1, \$0, VL2U lbu RG1, 0(\$1) |
|lbu \$t1,100(\$t2)|Load Byte Unsigned : Set \$t1 to zero-extended 8-bit value from effective memory byte address|ori \$1, \$0, VL2U addu \$1, \$1, RG4 lbu RG1, 0(\$1) |
|lbu \$t1,100000|Load Byte Unsigned : Set \$t1 to zero-extended 8-bit value from effective memory byte address|lui \$1, VH2 lbu RG1,VL2(\$1) |
|lbu \$t1,100000(\$t2)|Load Byte Unsigned : Set \$t1 to zero-extended 8-bit value from effective memory byte address|lui \$1, VH2 addu \$1, \$1, RG4 lbu RG1, VL2(\$1) |
|lbu \$t1,label|Load Byte Unsigned : Set \$t1 to zero-extended 8-bit value from effective memory byte address|lui \$1, LH2 lbu RG1, LL2(\$1) COMPACT lbu RG1, LL2(\$0) |
|lbu \$t1,label(\$t2)|Load Byte Unsigned : Set \$t1 to zero-extended 8-bit value from effective memory byte address|lui \$1, LH2 addu \$1, \$1, RG4 lbu RG1, LL2(\$1) COMPACT lbu RG1, LL2(RG4) |
|lbu \$t1,label+100000|Load Byte Unsigned : Set \$t1 to zero-extended 8-bit value from effective memory byte address|lui \$1, LHPA lbu RG1, LLP(\$1) |
|lbu \$t1,label+100000(\$t2)|Load Byte Unsigned : Set \$t1 to zero-extended 8-bit value from effective memory byte address|lui \$1, LHPA addu \$1, \$1, RG6 lbu RG1, LLP(\$1) |
|ld \$t1,(\$t2)|Load Doubleword : Set \$t1 and the next register to the 64 bits starting at effective memory word address|lw RG1, 0(RG3) lw NR1, 4(RG3) |
|ld \$t1,-100(\$t2)|Load Doubleword : Set \$t1 and the next register to the 64 bits starting at effective memory byte address|lw RG1, VL2(RG4) lui \$1, VH2P4 addu \$1, \$1, RG4 lw NR1, VL2P4(\$1) |
|ld \$t1,100000|Load Doubleword : Set \$t1 and the next register to the 64 bits starting at effective memory word address|lui \$1, VH2 lw RG1, VL2(\$1) lui \$1, VH2P4 lw NR1, VL2P4(\$1) |
|ld \$t1,100000(\$t2)|Load Doubleword : Set \$t1 and the next register to the 64 bits starting at effective memory word address|lui \$1, VH2 addu \$1, \$1, RG4 lw RG1, VL2(\$1) lui \$1, VH2P4 addu \$1, \$1, RG4 lw NR1, VL2P4(\$1) |
|ld \$t1,label|Load Doubleword : Set \$t1 and the next register to the 64 bits starting at effective memory word address|lui \$1, LH2 lw RG1, LL2(\$1) lui \$1, LH2P4 lw NR1, LL2P4(\$1) |
|ld \$t1,label(\$t2)|Load Doubleword : Set \$t1 and the next register to the 64 bits starting at effective memory word address|lui \$1, LH2 addu \$1, \$1, RG4 lw RG1, LL2(\$1) lui \$1, LH2P4 addu \$1, \$1, RG4 lw NR1, LL2P4(\$1) |
|ld \$t1,label+100000|Load Doubleword : Set \$t1 and the next register to the 64 bits starting at effective memory word address|lui \$1, LHPA lw RG1, LLP(\$1) lui \$1, LHPAP4 lw NR1, LLPP4(\$1) |
|ld \$t1,label+100000(\$t2)|Load Doubleword : Set \$t1 and the next register to the 64 bits starting at effective memory word address|lui \$1, LHPA addu \$1, \$1, RG6 lw RG1, LLP(\$1) lui \$1, LHPAP4 addu \$1, \$1, RG6 lw NR1, LLPP4(\$1) |
|ldc1 \$f2,(\$t2)|Load Doubleword Coprocessor 1 : Set \$f2 and \$f3 register pair to 64-bit value at effective memory doubleword address|ldc1 RG1,0(RG3) |
|ldc1 \$f2,-100|Load Doubleword Coprocessor 1 : Set \$f2 and \$f3 register pair to 64-bit value at effective memory doubleword address|ldc1 RG1,VL2(\$0) |
|ldc1 \$f2,100000|Load Doubleword Coprocessor 1 : Set \$f2 and \$f3 register pair to 64-bit value at effective memory doubleword address|lui \$1, VH2 ldc1 RG1,VL2(\$1) |
|ldc1 \$f2,100000(\$t2)|Load Doubleword Coprocessor 1 : Set \$f2 and \$f3 register pair to 64-bit value at effective memory doubleword address|lui \$1, VH2 addu \$1, \$1, RG4 ldc1 RG1, VL2(\$1) |
|ldc1 \$f2,label|Load Doubleword Coprocessor 1 : Set \$f2 and \$f3 register pair to 64-bit value at effective memory doubleword address|lui \$1, LH2 ldc1 RG1, LL2(\$1) COMPACT ldc1 RG1, LL2(\$0) |
|ldc1 \$f2,label(\$t2)|Load Doubleword Coprocessor 1 : Set \$f2 and \$f3 register pair to 64-bit value at effective memory doubleword address|lui \$1, LH2 addu \$1, \$1, RG4 ldc1 RG1, LL2(\$1) COMPACT ldc1 RG1, LL2(RG4) |
|ldc1 \$f2,label+100000|Load Doubleword Coprocessor 1 : Set \$f2 and \$f3 register pair to 64-bit value at effective memory doubleword address|lui \$1, LHPA ldc1 RG1, LLP(\$1) |
|ldc1 \$f2,label+100000(\$t2)|Load Doubleword Coprocessor 1 : Set \$f2 and \$f3 register pair to 64-bit value at effective memory doubleword address|lui \$1, LHPA addu \$1, \$1, RG6 ldc1 RG1, LLP(\$1) |
|lh \$t1,(\$t2)|Load Halfword : Set \$t1 to sign-extended 16-bit value from effective memory halfword address|lh RG1,0(RG3) |
|lh \$t1,-100|Load Halfword : Set \$t1 to sign-extended 16-bit value from effective memory halfword address|lh RG1, VL2(\$0) |
|lh \$t1,100|Load Halfword : Set \$t1 to sign-extended 16-bit value from effective memory halfword address|ori \$1, \$0, VL2U lh RG1, 0(\$1) |
|lh \$t1,100(\$t2)|Load Halfword : Set \$t1 to sign-extended 16-bit value from effective memory halfword address|ori \$1, \$0, VL2U addu \$1, \$1, RG4 lh RG1, 0(\$1) |
|lh \$t1,100000|Load Halfword : Set \$t1 to sign-extended 16-bit value from effective memory halfword address|lui \$1, VH2 lh RG1,VL2(\$1) |
|lh \$t1,100000(\$t2)|Load Halfword : Set \$t1 to sign-extended 16-bit value from effective memory halfword address|lui \$1, VH2 addu \$1, \$1, RG4 lh RG1, VL2(\$1) |
|lh \$t1,label|Load Halfword : Set \$t1 to sign-extended 16-bit value from effective memory halfword address|lui \$1, LH2 lh RG1, LL2(\$1) COMPACT lh RG1, LL2(\$0) |
|lh \$t1,label(\$t2)|Load Halfword : Set \$t1 to sign-extended 16-bit value from effective memory halfword address|lui \$1, LH2 addu \$1, \$1, RG4 lh RG1, LL2(\$1) COMPACT lh RG1, LL2(RG4) |
|lh \$t1,label+100000|Load Halfword : Set \$t1 to sign-extended 16-bit value from effective memory halfword address|lui \$1, LHPA lh RG1, LLP(\$1) |
|lh \$t1,label+100000(\$t2)|Load Halfword : Set \$t1 to sign-extended 16-bit value from effective memory halfword address|lui \$1, LHPA addu \$1, \$1, RG6 lh RG1, LLP(\$1) |
|lhu \$t1,(\$t2)|Load Halfword Unsigned : Set \$t1 to zero-extended 16-bit value from effective memory halfword address|lhu RG1,0(RG3) |
|lhu \$t1,-100|Load Halfword Unsigned : Set \$t1 to zero-extended 16-bit value from effective memory halfword address|lhu RG1,VL2(\$0) |
|lhu \$t1,100|Load Halfword Unsigned : Set \$t1 to zero-extended 16-bit value from effective memory halfword address|ori \$1, \$0, VL2U lhu RG1, 0(\$1) |
|lhu \$t1,100(\$t2)|Load Halfword Unsigned : Set \$t1 to zero-extended 16-bit value from effective memory halfword address|ori \$1, \$0, VL2U addu \$1, \$1, RG4 lhu RG1, 0(\$1) |
|lhu \$t1,100000|Load Halfword Unsigned : Set \$t1 to zero-extended 16-bit value from effective memory halfword address|lui \$1, VH2 lhu RG1,VL2(\$1) |
|lhu \$t1,100000(\$t2)|Load Halfword Unsigned : Set \$t1 to zero-extended 16-bit value from effective memory halfword address|lui \$1, VH2 addu \$1, \$1, RG4 lhu RG1, VL2(\$1) |
|lhu \$t1,label|Load Halfword Unsigned : Set \$t1 to zero-extended 16-bit value from effective memory halfword address|lui \$1, LH2 lhu RG1, LL2(\$1) COMPACT lhu RG1, LL2(\$0) |
|lhu \$t1,label(\$t2)|Load Halfword Unsigned : Set \$t1 to zero-extended 16-bit value from effective memory halfword address|lui \$1, LH2 addu \$1, \$1, RG4 lhu RG1, LL2(\$1) COMPACT lhu RG1, LL2(RG4) |
|lhu \$t1,label+100000|Load Halfword Unsigned : Set \$t1 to zero-extended 16-bit value from effective memory halfword address|lui \$1, LHPA lhu RG1, LLP(\$1) |
|lhu \$t1,label+100000(\$t2)|Load Halfword Unsigned : Set \$t1 to zero-extended 16-bit value from effective memory halfword address|lui \$1, LHPA addu \$1, \$1, RG6 lhu RG1, LLP(\$1) |
|li \$t1,-100|Load Immediate : Set \$t1 to 16-bit immediate (sign-extended)|addiu RG1, \$0, VL2 |
|li \$t1,100|Load Immediate : Set \$t1 to unsigned 16-bit immediate (zero-extended)|ori RG1, \$0, VL2U |
|li \$t1,100000|Load Immediate : Set \$t1 to 32-bit immediate|lui \$1, VHL2 ori RG1, \$1, VL2U |
|ll \$t1,(\$t2)|Load Linked : Paired with Store Conditional (sc) to perform atomic read-modify-write.  Treated as equivalent to Load Word (lw) because MARS does not simulate multiple processors.|ll RG1,0(RG3) |
|ll \$t1,-100|Load Linked : Paired with Store Conditional (sc) to perform atomic read-modify-write.  Treated as equivalent to Load Word (lw) because MARS does not simulate multiple processors.|ll RG1,VL2(\$0) |
|ll \$t1,100|Load Linked : Paired with Store Conditional (sc) to perform atomic read-modify-write.  Treated as equivalent to Load Word (lw) because MARS does not simulate multiple processors.|ori \$1, \$0, VL2U ll RG1, 0(\$1) |
|ll \$t1,100(\$t2)|Load Linked : Paired with Store Conditional (sc) to perform atomic read-modify-write.  Treated as equivalent to Load Word (lw) because MARS does not simulate multiple processors.|ori \$1, \$0, VL2U addu \$1, \$1, RG4 ll RG1, 0(\$1) |
|ll \$t1,100000|Load Linked : Paired with Store Conditional (sc) to perform atomic read-modify-write.  Treated as equivalent to Load Word (lw) because MARS does not simulate multiple processors.|lui \$1, VH2 ll RG1,VL2(\$1) |
|ll \$t1,100000(\$t2)|Load Linked : Paired with Store Conditional (sc) to perform atomic read-modify-write.  Treated as equivalent to Load Word (lw) because MARS does not simulate multiple processors.|lui \$1, VH2 addu \$1, \$1, RG4 ll RG1, VL2(\$1) |
|ll \$t1,label|Load Linked : Paired with Store Conditional (sc) to perform atomic read-modify-write.  Treated as equivalent to Load Word (lw) because MARS does not simulate multiple processors.|lui \$1, LH2 ll RG1, LL2(\$1) COMPACT ll RG1, LL2(\$0) |
|ll \$t1,label(\$t2)|Load Linked : Paired with Store Conditional (sc) to perform atomic read-modify-write.  Treated as equivalent to Load Word (lw) because MARS does not simulate multiple processors.|lui \$1, LH2 addu \$1, \$1, RG4 ll RG1, LL2(\$1) COMPACT ll RG1, LL2(RG4) |
|ll \$t1,label+100000|Load Linked : Paired with Store Conditional (sc) to perform atomic read-modify-write.  Treated as equivalent to Load Word (lw) because MARS does not simulate multiple processors.|lui \$1, LHPA ll RG1, LLP(\$1) |
|ll \$t1,label+100000(\$t2)|Load Linked : Paired with Store Conditional (sc) to perform atomic read-modify-write.  Treated as equivalent to Load Word (lw) because MARS does not simulate multiple processors.|lui \$1, LHPA addu \$1, \$1, RG6 ll RG1, LLP(\$1) |
|lw \$t1,(\$t2)|Load Word : Set \$t1 to contents of effective memory word address|lw RG1,0(RG3) |
|lw \$t1,-100|Load Word : Set \$t1 to contents of effective memory word address|lw RG1, VL2(\$0) |
|lw \$t1,100|Load Word : Set \$t1 to contents of effective memory word address|ori \$1, \$0, VL2U lw RG1, 0(\$1) |
|lw \$t1,100(\$t2)|Load Word : Set \$t1 to contents of effective memory word address|ori \$1, \$0, VL2U addu \$1, \$1, RG4 lw RG1, 0(\$1) |
|lw \$t1,100000|Load Word : Set \$t1 to contents of effective memory word address|lui \$1, VH2 lw RG1,VL2(\$1) |
|lw \$t1,100000(\$t2)|Load Word : Set \$t1 to contents of effective memory word address|lui \$1, VH2 addu \$1, \$1, RG4 lw RG1, VL2(\$1) |
|lw \$t1,label|Load Word : Set \$t1 to contents of memory word at label's address|lui \$1, LH2 lw RG1, LL2(\$1) COMPACT lw RG1, LL2(\$0) |
|lw \$t1,label(\$t2)|Load Word : Set \$t1 to contents of effective memory word address|lui \$1, LH2 addu \$1, \$1, RG4 lw RG1, LL2(\$1) COMPACT lw RG1, LL2(RG4) |
|lw \$t1,label+100000|Load Word : Set \$t1 to contents of effective memory word address |lui \$1, LHPA lw RG1, LLP(\$1) |
|lw \$t1,label+100000(\$t2)|Load Word : Set \$t1 to contents of effective memory word address|lui \$1, LHPA addu \$1, \$1, RG6 lw RG1, LLP(\$1) |
|lwc1 \$f1,(\$t2)|Load Word Coprocessor 1 : Set \$f1 to 32-bit value from effective memory word address|lwc1 RG1,0(RG3) |
|lwc1 \$f1,-100|Load Word Coprocessor 1 : Set \$f1 to 32-bit value from effective memory word address|lwc1 RG1,VL2(\$0) |
|lwc1 \$f1,100000|Load Word Coprocessor 1 : Set \$f1 to 32-bit value from effective memory word address|lui \$1, VH2 lwc1 RG1,VL2(\$1) |
|lwc1 \$f1,100000(\$t2)|Load Word Coprocessor 1 : Set \$f1 to 32-bit value from effective memory word address|lui \$1, VH2 addu \$1, \$1, RG4 lwc1 RG1, VL2(\$1) |
|lwc1 \$f1,label|Load Word Coprocessor 1 : Set \$f1 to 32-bit value from effective memory word address|lui \$1, LH2 lwc1 RG1, LL2(\$1) COMPACT lwc1 RG1, LL2(\$0) |
|lwc1 \$f1,label(\$t2)|Load Word Coprocessor 1 : Set \$f1 to 32-bit value from effective memory word address|lui \$1, LH2 addu \$1, \$1, RG4 lwc1 RG1, LL2(\$1) COMPACT lwc1 RG1, LL2(RG4) |
|lwc1 \$f1,label+100000|Load Word Coprocessor 1 : Set \$f1 to 32-bit value from effective memory word address|lui \$1, LHPA lwc1 RG1, LLP(\$1) |
|lwc1 \$f1,label+100000(\$t2)|Load Word Coprocessor 1 : Set \$f1 to 32-bit value from effective memory word address|lui \$1, LHPA addu \$1, \$1, RG6 lwc1 RG1, LLP(\$1) |
|lwl \$t1,(\$t2)|Load Word Left : Load from 1 to 4 bytes left-justified into \$t1, starting with effective memory byte address and continuing through the low-order byte of its word|lwl RG1,0(RG3) |
|lwl \$t1,-100|Load Word Left : Load from 1 to 4 bytes left-justified into \$t1, starting with effective memory byte address and continuing through the low-order byte of its word|lwl RG1,VL2(\$0) |
|lwl \$t1,100|Load Word Left : Load from 1 to 4 bytes left-justified into \$t1, starting with effective memory byte address and continuing through the low-order byte of its word|ori \$1, \$0, VL2U lwl RG1, 0(\$1) |
|lwl \$t1,100(\$t2)|Load Word Left : Load from 1 to 4 bytes left-justified into \$t1, starting with effective memory byte address and continuing through the low-order byte of its word|ori \$1, \$0, VL2U addu \$1, \$1, RG4 lwl RG1, 0(\$1) |
|lwl \$t1,100000|Load Word Left : Load from 1 to 4 bytes left-justified into \$t1, starting with effective memory byte address and continuing through the low-order byte of its word|lui \$1, VH2 lwl RG1,VL2(\$1) |
|lwl \$t1,100000(\$t2)|Load Word Left : Load from 1 to 4 bytes left-justified into \$t1, starting with effective memory byte address and continuing through the low-order byte of its word|lui \$1, VH2 addu \$1, \$1, RG4 lwl RG1, VL2(\$1) |
|lwl \$t1,label|Load Word Left : Load from 1 to 4 bytes left-justified into \$t1, starting with effective memory byte address and continuing through the low-order byte of its word|lui \$1, LH2 lwl RG1, LL2(\$1) COMPACT lwl RG1, LL2(\$0) |
|lwl \$t1,label(\$t2)|Load Word Left : Load from 1 to 4 bytes left-justified into \$t1, starting with effective memory byte address and continuing through the low-order byte of its word|lui \$1, LH2 addu \$1, \$1, RG4 lwl RG1, LL2(\$1) COMPACT lwl RG1, LL2(RG4) |
|lwl \$t1,label+100000|Load Word Left : Load from 1 to 4 bytes left-justified into \$t1, starting with effective memory byte address and continuing through the low-order byte of its word|lui \$1, LHPA lwl RG1, LLP(\$1) |
|lwl \$t1,label+100000(\$t2)|Load Word Left : Load from 1 to 4 bytes left-justified into \$t1, starting with effective memory byte address and continuing through the low-order byte of its word|lui \$1, LHPA addu \$1, \$1, RG6 lwl RG1, LLP(\$1) |
|lwr \$t1,(\$t2)|Load Word Right : Load from 1 to 4 bytes right-justified into \$t1, starting with effective memory byte address and continuing through the high-order byte of its word|lwr RG1,0(RG3) |
|lwr \$t1,-100|Load Word Right : Load from 1 to 4 bytes right-justified into \$t1, starting with effective memory byte address and continuing through the high-order byte of its word|lwr RG1,VL2(\$0) |
|lwr \$t1,100|Load Word Right : Load from 1 to 4 bytes right-justified into \$t1, starting with effective memory byte address and continuing through the high-order byte of its word|ori \$1, \$0, VL2U lwr RG1, 0(\$1) |
|lwr \$t1,100(\$t2)|Load Word Right : Load from 1 to 4 bytes right-justified into \$t1, starting with effective memory byte address and continuing through the high-order byte of its word|ori \$1, \$0, VL2U addu \$1, \$1, RG4 lwr RG1, 0(\$1) |
|lwr \$t1,100000|Load Word Right : Load from 1 to 4 bytes right-justified into \$t1, starting with effective memory byte address and continuing through the high-order byte of its word|lui \$1, VH2 lwr RG1,VL2(\$1) |
|lwr \$t1,100000(\$t2)|Load Word Right : Load from 1 to 4 bytes right-justified into \$t1, starting with effective memory byte address and continuing through the high-order byte of its word|lui \$1, VH2 addu \$1, \$1, RG4 lwr RG1, VL2(\$1) |
|lwr \$t1,label|Load Word Right : Load from 1 to 4 bytes right-justified into \$t1, starting with effective memory byte address and continuing through the high-order byte of its word|lui \$1, LH2 lwr RG1, LL2(\$1) COMPACT lwr RG1, LL2(\$0) |
|lwr \$t1,label(\$t2)|Load Word Right : Load from 1 to 4 bytes right-justified into \$t1, starting with effective memory byte address and continuing through the high-order byte of its word|lui \$1, LH2 addu \$1, \$1, RG4 lwr RG1, LL2(\$1) COMPACT lwr RG1, LL2(RG4) |
|lwr \$t1,label+100000|Load Word Right : Load from 1 to 4 bytes right-justified into \$t1, starting with effective memory byte address and continuing through the high-order byte of its word|lui \$1, LHPA lwr RG1, LLP(\$1) |
|lwr \$t1,label+100000(\$t2)|Load Word Right : Load from 1 to 4 bytes right-justified into \$t1, starting with effective memory byte address and continuing through the high-order byte of its word|lui \$1, LHPA addu \$1, \$1, RG6 lwr RG1, LLP(\$1) |
|mfc1.d \$t1,\$f2|Move From Coprocessor 1 Double : Set \$t1 to contents of \$f2, set next higher register from \$t1 to contents of next higher register from \$f2|mfc1 RG1, RG2 mfc1 NR1, NR2 |
|move \$t1,\$t2|MOVE : Set \$t1 to contents of \$t2|addu RG1, \$0, RG2 |
|mtc1.d \$t1,\$f2|Move To Coprocessor 1 Double : Set \$f2 to contents of \$t1, set next higher register from \$f2 to contents of next higher register from \$t1|mtc1 RG1, RG2 mtc1 NR1, NR2 |
|mul \$t1,\$t2,-100|MULtiplication : Set HI to high-order 32 bits, LO and \$t1 to low-order 32 bits of the product of \$t2 and 16-bit signed immediate (use mfhi to access HI, mflo to access LO)|addi \$1, \$0, VL3 mul RG1, RG2, \$1 |
|mul \$t1,\$t2,100000|MULtiplication : Set HI to high-order 32 bits, LO and \$t1 to low-order 32 bits of the product of \$t2 and 32-bit immediate (use mfhi to access HI, mflo to access LO)|lui \$1, VHL3 ori \$1, \$1, VL3U mul RG1, RG2, \$1 |
|mulo \$t1,\$t2,\$t3|MULtiplication with Overflow : Set \$t1 to low-order 32 bits of the product of \$t2 and \$t3|mult RG2, RG3 mfhi \$1 mflo RG1 sra RG1, RG1, 31 beq \$1, RG1, BROFF12 DBNOP break mflo RG1 |
|mulo \$t1,\$t2,-100|MULtiplication with Overflow : Set \$t1 to low-order 32 bits of the product of \$t2 and signed 16-bit immediate|addi \$1, \$0, VL3 mult RG2, \$1 mfhi \$1 mflo RG1 sra RG1, RG1, 31 beq \$1, RG1, BROFF12 DBNOP break mflo RG1 |
|mulo \$t1,\$t2,100000|MULtiplication with Overflow : Set \$t1 to low-order 32 bits of the product of \$t2 and 32-bit immediate|lui \$1, VHL3 ori \$1, \$1, VL3U mult RG2, \$1 mfhi \$1 mflo RG1 sra RG1, RG1, 31 beq \$1, RG1, BROFF12 DBNOP break mflo RG1 |
|mulou \$t1,\$t2,\$t3|MULtiplication with Overflow Unsigned : Set \$t1 to low-order 32 bits of the product of \$t2 and \$t3|multu RG2, RG3 mfhi \$1 beq \$1,\$0, BROFF12 DBNOP break mflo RG1 |
|mulou \$t1,\$t2,-100|MULtiplication with Overflow Unsigned : Set \$t1 to low-order 32 bits of the product of \$t2 and signed 16-bit immediate|addi \$1, \$0, VL3 multu RG2, \$1 mfhi \$1 beq \$1,\$0, BROFF12 DBNOP break mflo RG1 |
|mulou \$t1,\$t2,100000|MULtiplication with Overflow Unsigned : Set \$t1 to low-order 32 bits of the product of \$t2 and 32-bit immediate|lui \$1, VHL3 ori \$1, \$1, VL3U multu RG2, \$1 mfhi \$1 beq \$1,\$0, BROFF12 DBNOP break mflo RG1 |
|mulu \$t1,\$t2,\$t3|MULtiplication Unsigned : Set HI to high-order 32 bits, LO and \$t1 to low-order 32 bits of (\$t2 multiplied by \$t3, unsigned multiplication)|multu RG2, RG3 mflo RG1 |
|mulu \$t1,\$t2,-100|MULtiplication Unsigned :  Set HI to high-order 32 bits, LO and \$t1 to low-order 32 bits of (\$t2 multiplied by 16-bit immediate, unsigned multiplication)|addi \$1, \$0, VL3 multu RG2, \$1 mflo RG1 |
|mulu \$t1,\$t2,100000|MULtiplication Unsigned :  Set HI to high-order 32 bits, LO and \$t1 to low-order 32 bits of (\$t2 multiplied by 32-bit immediate, unsigned multiplication)|lui \$1, VHL3 ori \$1, \$1, VL3U multu RG2, \$1 mflo RG1 |
|neg \$t1,\$t2|NEGate : Set \$t1 to negation of \$t2|sub RG1, \$0, RG2 |
|negu \$t1,\$t2|NEGate Unsigned : Set \$t1 to negation of \$t2, no overflow|subu RG1, \$0, RG2 |
|not \$t1,\$t2|Bitwise NOT (bit inversion)|nor RG1, RG2, \$0 |
|or \$t1,\$t2,100|OR : set \$t1 to (\$t2 bitwise-OR 16-bit unsigned immediate)|ori RG1, RG2, VL3U |
|or \$t1,100|OR : set \$t1 to (\$t1 bitwise-OR 16-bit unsigned immediate)|ori RG1, RG1, VL2U |
|ori \$t1,\$t2,100000|OR Immediate : set \$t1 to (\$t2 bitwise-OR 32-bit immediate)|lui \$1, VHL3 ori \$1, \$1, VL3U or RG1, RG2, \$1  |
|ori \$t1,100|OR Immediate : set \$t1 to (\$t1 bitwise-OR 16-bit unsigned immediate)|ori RG1, RG1, VL2U |
|ori \$t1,100000|OR Immediate : set \$t1 to (\$t1 bitwise-OR 32-bit immediate)|lui \$1, VHL2 ori \$1, \$1, VL2U or RG1, RG1, \$1 |
|rem \$t1,\$t2,\$t3|REMainder : Set \$t1 to (remainder of \$t2 divided by \$t3)|bne RG3, \$0, BROFF12 DBNOP break div RG2, RG3 mfhi RG1 |
|rem \$t1,\$t2,-100|REMainder : Set \$t1 to (remainder of \$t2 divided by 16-bit immediate)|addi \$1, \$0, VL3 div RG2, \$1 mfhi RG1 |
|rem \$t1,\$t2,100000|REMainder : Set \$t1 to (remainder of \$t2 divided by 32-bit immediate)|lui \$1, VHL3 ori \$1, \$1, VL3U div RG2, \$1 mfhi RG1 |
|remu \$t1,\$t2,\$t3|REMainder : Set \$t1 to (remainder of \$t2 divided by \$t3, unsigned division)|bne RG3, \$0, BROFF12 DBNOP break divu RG2, RG3 mfhi RG1 |
|remu \$t1,\$t2,-100|REMainder : Set \$t1 to (remainder of \$t2 divided by 16-bit immediate, unsigned division)|addi \$1, \$0, VL3 divu RG2, \$1 mfhi RG1 |
|remu \$t1,\$t2,100000|REMainder : Set \$t1 to (remainder of \$t2 divided by 32-bit immediate, unsigned division)|lui \$1, VHL3 ori \$1, \$1, VL3U divu RG2, \$1 mfhi RG1 |
|rol \$t1,\$t2,\$t3|ROtate Left : Set \$t1 to (\$t2 rotated left by number of bit positions specified in \$t3)|subu \$1, \$0, RG3 srlv \$1, RG2, \$1 sllv RG1, RG2, RG3 or RG1, RG1, \$1 |
|rol \$t1,\$t2,10|ROtate Left : Set \$t1 to (\$t2 rotated left by number of bit positions specified in 5-bit immediate)|srl \$1, RG2, S32 sll RG1, RG2, OP3 or RG1, RG1, \$1 |
|ror \$t1,\$t2,\$t3|ROtate Right : Set \$t1 to (\$t2 rotated right by number of bit positions specified in \$t3)|subu \$1, \$0, RG3 sllv \$1, RG2, \$1 srlv RG1, RG2, RG3 or RG1, RG1, \$1 |
|ror \$t1,\$t2,10|ROtate Right : Set \$t1 to (\$t2 rotated right by number of bit positions specified in 5-bit immediate)|sll \$1, RG2, S32 srl RG1, RG2, OP3 or RG1, RG1, \$1 |
|s.d \$f2,(\$t2)|Store floating point Double precision : Store 64 bits from \$f2 and \$f3 register pair to effective memory doubleword address|sdc1 RG1,0(RG3) |
|s.d \$f2,-100|Store floating point Double precision : Store 64 bits from \$f2 and \$f3 register pair to effective memory doubleword address|sdc1 RG1,VL2(\$0) |
|s.d \$f2,100000|Store floating point Double precision : Store 64 bits from \$f2 and \$f3 register pair to effective memory doubleword address|lui \$1, VH2 sdc1 RG1,VL2(\$1) |
|s.d \$f2,100000(\$t2)|Store floating point Double precision : Store 64 bits from \$f2 and \$f3 register pair to effective memory doubleword address|lui \$1, VH2 addu \$1, \$1, RG4 sdc1 RG1, VL2(\$1) |
|s.d \$f2,label|Store floating point Double precision : Store 64 bits from \$f2 and \$f3 register pair to effective memory doubleword address|lui \$1, LH2 sdc1 RG1, LL2(\$1) COMPACT sdc1 RG1, LL2(\$0) |
|s.d \$f2,label(\$t2)|Store floating point Double precision : Store 64 bits from \$f2 and \$f3 register pair to effective memory doubleword address|lui \$1, LH2 addu \$1, \$1, RG4 sdc1 RG1, LL2(\$1) COMPACT sdc1 RG1, LL2(RG4) |
|s.d \$f2,label+100000|Store floating point Double precision : Store 64 bits from \$f2 and \$f3 register pair to effective memory doubleword address|lui \$1, LHPA sdc1 RG1, LLP(\$1) |
|s.d \$f2,label+100000(\$t2)|Store floating point Double precision : Store 64 bits from \$f2 and \$f3 register pair to effective memory doubleword address|lui \$1, LHPA addu \$1, \$1, RG6 sdc1 RG1, LLP(\$1) |
|s.s \$f1,(\$t2)|Store floating point Single precision : Store 32-bit value from \$f1 to effective memory word address|swc1 RG1,0(RG3) |
|s.s \$f1,-100|Store floating point Single precision : Store 32-bit value from \$f1 to effective memory word address|swc1 RG1,VL2(\$0) |
|s.s \$f1,100000|Store floating point Single precision : Store 32-bit value from \$f1 to effective memory word address|lui \$1, VH2 swc1 RG1,VL2(\$1) |
|s.s \$f1,100000(\$t2)|Store floating point Single precision : Store 32-bit value from \$f1 to effective memory word address|lui \$1, VH2 addu \$1, \$1, RG4 swc1 RG1, VL2(\$1) |
|s.s \$f1,label|Store floating point Single precision : Store 32-bit value from \$f1 to effective memory word address|lui \$1, LH2 swc1 RG1, LL2(\$1) COMPACT swc1 RG1, LL2(\$0) |
|s.s \$f1,label(\$t2)|Store floating point Single precision : Store 32-bit value from \$f1 to effective memory word address|lui \$1, LH2 addu \$1, \$1, RG4 swc1 RG1, LL2(\$1) COMPACT swc1 RG1, LL2(RG4) |
|s.s \$f1,label+100000|Store floating point Single precision : Store 32-bit value from \$f1 to effective memory word address|lui \$1, LHPA swc1 RG1, LLP(\$1) |
|s.s \$f1,label+100000(\$t2)|Store floating point Single precision : Store 32-bit value from \$f1 to effective memory word address|lui \$1, LHPA addu \$1, \$1, RG6 swc1 RG1, LLP(\$1) |
|sb \$t1,(\$t2)|Store Byte : Store the low-order 8 bits of \$t1 into the effective memory byte address|sb RG1,0(RG3) |
|sb \$t1,-100|Store Byte : Store the low-order 8 bits of \$t1 into the effective memory byte address|sb RG1, VL2(\$0) |
|sb \$t1,100|Store Byte : Store the low-order 8 bits of \$t1 into the effective memory byte address|ori \$1, \$0, VL2U sb RG1, 0(\$1) |
|sb \$t1,100(\$t2)|Store Byte : Store the low-order 8 bits of \$t1 into the effective memory byte address|ori \$1, \$0, VL2U addu \$1, \$1, RG4 sb RG1, 0(\$1) |
|sb \$t1,100000|Store Byte : Store the low-order 8 bits of \$t1 into the effective memory byte address|lui \$1, VH2 sb RG1,VL2(\$1) |
|sb \$t1,100000(\$t2)|Store Byte : Store the low-order 8 bits of \$t1 into the effective memory byte address|lui \$1, VH2 addu \$1, \$1, RG4 sb RG1, VL2(\$1) |
|sb \$t1,label|Store Byte : Store the low-order 8 bits of \$t1 into the effective memory byte address|lui \$1, LH2 sb RG1, LL2(\$1) COMPACT sb RG1, LL2(\$0) |
|sb \$t1,label(\$t2)|Store Byte : Store the low-order 8 bits of \$t1 into the effective memory byte address|lui \$1, LH2 addu \$1, \$1, RG4 sb RG1, LL2(\$1) COMPACT sb RG1, LL2(RG4) |
|sb \$t1,label+100000|Store Byte : Store the low-order 8 bits of \$t1 into the effective memory byte address|lui \$1, LHPA sb RG1, LLP(\$1) |
|sb \$t1,label+100000(\$t2)|Store Byte : Store the low-order 8 bits of \$t1 into the effective memory byte address|lui \$1, LHPA addu \$1, \$1, RG6 sb RG1, LLP(\$1) |
|sc \$t1,(\$t2)|Store Conditional : Paired with Load Linked (ll) to perform atomic read-modify-write.  Treated as equivalent to Store Word (sw) because MARS does not simulate multiple processors.|sc RG1,0(RG3) |
|sc \$t1,-100|Store Conditional : Paired with Load Linked (ll) to perform atomic read-modify-write.  Treated as equivalent to Store Word (sw) because MARS does not simulate multiple processors.|sc RG1,VL2(\$0) |
|sc \$t1,100|Store Conditional : Paired with Load Linked (ll) to perform atomic read-modify-write.  Treated as equivalent to Store Word (sw) because MARS does not simulate multiple processors.|ori \$1, \$0, VL2U sc RG1, 0(\$1) |
|sc \$t1,100(\$t2)|Store Conditional : Paired with Load Linked (ll) to perform atomic read-modify-write.  Treated as equivalent to Store Word (sw) because MARS does not simulate multiple processors.|ori \$1, \$0, VL2U addu \$1, \$1, RG4 sc RG1, 0(\$1) |
|sc \$t1,100000|Store Conditional : Paired with Load Linked (ll) to perform atomic read-modify-write.  Treated as equivalent to Store Word (sw) because MARS does not simulate multiple processors.|lui \$1, VH2 sc RG1,VL2(\$1) |
|sc \$t1,100000(\$t2)|Store Conditional : Paired with Load Linked (ll) to perform atomic read-modify-write.  Treated as equivalent to Store Word (sw) because MARS does not simulate multiple processors.|lui \$1, VH2 addu \$1, \$1, RG4 sc RG1, VL2(\$1) |
|sc \$t1,label|Store Conditional : Paired with Load Linked (ll) to perform atomic read-modify-write.  Treated as equivalent to Store Word (sw) because MARS does not simulate multiple processors.|lui \$1, LH2 sc RG1, LL2(\$1) COMPACT sc RG1, LL2(\$0) |
|sc \$t1,label(\$t2)|Store Conditional : Paired with Load Linked (ll) to perform atomic read-modify-write.  Treated as equivalent to Store Word (sw) because MARS does not simulate multiple processors.|lui \$1, LH2 addu \$1, \$1, RG4 sc RG1, LL2(\$1) COMPACT sc RG1, LL2(RG4) |
|sc \$t1,label+100000|Store Conditional : Paired with Load Linked (ll) to perform atomic read-modify-write.  Treated as equivalent to Store Word (sw) because MARS does not simulate multiple processors.|lui \$1, LHPA sc RG1, LLP(\$1) |
|sc \$t1,label+100000(\$t2)|Store Conditional : Paired with Load Linked (ll) to perform atomic read-modify-write.  Treated as equivalent to Store Word (sw) because MARS does not simulate multiple processors.|lui \$1, LHPA addu \$1, \$1, RG6 sc RG1, LLP(\$1) |
|sd \$t1,(\$t2)|Store Doubleword : Store contents of \$t1 and the next register to the 64 bits starting at effective memory word address|sw RG1, 0(RG3) sw NR1, 4(RG3) |
|sd \$t1,-100(\$t2)|Store Doubleword : Store contents of \$t1 and the next register to the 64 bits starting at effective memory byte address|sw RG1, VL2(RG4) lui \$1, VH2P4 addu \$1, \$1, RG4 sw NR1, VL2P4(\$1) |
|sd \$t1,100000|Store Doubleword : Store contents of \$t1 and the next register to the 64 bits starting at effective memory word address|lui \$1, VH2 sw RG1, VL2(\$1) lui \$1, VH2P4 sw NR1, VL2P4(\$1) |
|sd \$t1,100000(\$t2)|Store Doubleword : Store contents of \$t1 and the next register to the 64 bits starting at effective memory word address|lui \$1, VH2 addu \$1, \$1, RG4 sw RG1, VL2(\$1) lui \$1, VH2P4 addu \$1, \$1, RG4 sw NR1, VL2P4(\$1) |
|sd \$t1,label|Store Doubleword : Store contents of \$t1 and the next register to the 64 bits starting at effective memory word address|lui \$1, LH2 sw RG1, LL2(\$1) lui \$1, LH2P4 sw NR1, LL2P4(\$1) |
|sd \$t1,label(\$t2)|Store Doubleword : Store contents of \$t1 and the next register to the 64 bits starting at effective memory word address|lui \$1, LH2 addu \$1, \$1, RG4 sw RG1, LL2(\$1) lui \$1, LH2P4 addu \$1, \$1, RG4 sw NR1, LL2P4(\$1) |
|sd \$t1,label+100000|Store Doubleword : Store contents of \$t1 and the next register to the 64 bits starting at effective memory word address|lui \$1, LHPA sw RG1, LLP(\$1) lui \$1, LHPAP4 sw NR1, LLPP4(\$1) |
|sd \$t1,label+100000(\$t2)|Store Doubleword : Store contents of \$t1 and the next register to the 64 bits starting at effective memory word address|lui \$1, LHPA addu \$1, \$1, RG6 sw RG1, LLP(\$1) lui \$1, LHPAP4 addu \$1, \$1, RG6 sw NR1, LLPP4(\$1) |
|sdc1 \$f2,(\$t2)|Store Doubleword Coprocessor 1 : Store 64 bits from \$f2 and \$f3 register pair to effective memory doubleword address|sdc1 RG1,0(RG3) |
|sdc1 \$f2,-100|Store Doubleword Coprocessor 1 : Store 64 bits from \$f2 and \$f3 register pair to effective memory doubleword address|sdc1 RG1,VL2(\$0) |
|sdc1 \$f2,100000|Store Doubleword Coprocessor 1 : Store 64 bits from \$f2 and \$f3 register pair to effective memory doubleword address|lui \$1, VH2 sdc1 RG1,VL2(\$1) |
|sdc1 \$f2,100000(\$t2)|Store Doubleword Coprocessor 1 : Store 64 bits from \$f2 and \$f3 register pair to effective memory doubleword address|lui \$1, VH2 addu \$1, \$1, RG4 sdc1 RG1, VL2(\$1) |
|sdc1 \$f2,label|Store Doubleword Coprocessor 1 : Store 64 bits from \$f2 and \$f3 register pair to effective memory doubleword address|lui \$1, LH2 sdc1 RG1, LL2(\$1) COMPACT sdc1 RG1, LL2(\$0) |
|sdc1 \$f2,label(\$t2)|Store Doubleword Coprocessor 1 : Store 64 bits from \$f2 and \$f3 register pair to effective memory doubleword address|lui \$1, LH2 addu \$1, \$1, RG4 sdc1 RG1, LL2(\$1) COMPACT sdc1 RG1, LL2(RG4) |
|sdc1 \$f2,label+100000|Store Doubleword Coprocessor 1 : Store 64 bits from \$f2 and \$f3 register pair to effective memory doubleword address|lui \$1, LHPA sdc1 RG1, LLP(\$1) |
|sdc1 \$f2,label+100000(\$t2)|Store Doubleword Coprocessor 1 : Store 64 bits from \$f2 and \$f3 register pair to effective memory doubleword address|lui \$1, LHPA addu \$1, \$1, RG6 sdc1 RG1, LLP(\$1) |
|seq \$t1,\$t2,\$t3|Set EQual : if \$t2 equal to \$t3 then set \$t1 to 1 else 0|subu RG1, RG2, RG3 ori \$1, \$0, 1 sltu RG1, RG1, \$1 |
|seq \$t1,\$t2,-100|Set EQual : if \$t2 equal to 16-bit immediate then set \$t1 to 1 else 0|addi \$1, \$0, VL3 subu RG1, RG2, \$1 ori \$1, \$0, 1 sltu RG1, RG1, \$1 |
|seq \$t1,\$t2,100000|Set EQual : if \$t2 equal to 32-bit immediate then set \$t1 to 1 else 0|lui \$1, VHL3 ori \$1, \$1, VL3U subu RG1, RG2, \$1 ori \$1, \$0, 1 sltu RG1, RG1, \$1 |
|sge \$t1,\$t2,\$t3|Set Greater or Equal : if \$t2 greater or equal to \$t3 then set \$t1 to 1 else 0|slt RG1, RG2, RG3 ori \$1, \$0, 1 subu RG1, \$1, RG1 |
|sge \$t1,\$t2,-100|Set Greater or Equal : if \$t2 greater or equal to 16-bit immediate then set \$t1 to 1 else 0|addi \$1, \$0, VL3 slt RG1, RG2, \$1 ori \$1, \$0, 1 subu RG1, \$1, RG1 |
|sge \$t1,\$t2,100000|Set Greater or Equal : if \$t2 greater or equal to 32-bit immediate then set \$t1 to 1 else 0|lui \$1, VHL3 ori \$1, \$1, VL3U slt RG1, RG2, \$1 ori \$1, \$0, 1 subu RG1, \$1, RG1 |
|sgeu \$t1,\$t2,\$t3|Set Greater or Equal Unsigned : if \$t2 greater or equal to \$t3 (unsigned compare) then set \$t1 to 1 else 0|sltu RG1, RG2, RG3 ori \$1, \$0, 1 subu RG1, \$1, RG1 |
|sgeu \$t1,\$t2,-100|Set Greater or Equal Unsigned : if \$t2 greater or equal to 16-bit immediate (unsigned compare) then set \$t1 to 1 else 0|addi \$1, \$0, VL3 sltu RG1, RG2, \$1 ori \$1, \$0, 1 subu RG1, \$1, RG1 |
|sgeu \$t1,\$t2,100000|Set Greater or Equal Unsigned : if \$t2 greater or equal to 32-bit immediate (unsigned compare) then set \$t1 to 1 else 0|lui \$1, VHL3 ori \$1, \$1, VL3U sltu RG1, RG2, \$1 ori \$1, \$0, 1 subu RG1, \$1, RG1 |
|sgt \$t1,\$t2,\$t3|Set Greater Than : if \$t2 greater than \$t3 then set \$t1 to 1 else 0|slt RG1, RG3, RG2 |
|sgt \$t1,\$t2,-100|Set Greater Than : if \$t2 greater than 16-bit immediate then set \$t1 to 1 else 0|addi \$1, \$0, VL3 slt RG1, \$1, RG2 |
|sgt \$t1,\$t2,100000|Set Greater Than : if \$t2 greater than 32-bit immediate then set \$t1 to 1 else 0|lui \$1, VHL3 ori \$1, \$1, VL3U slt RG1, \$1, RG2 |
|sgtu \$t1,\$t2,\$t3|Set Greater Than Unsigned : if \$t2 greater than \$t3 (unsigned compare) then set \$t1 to 1 else 0|sltu RG1, RG3, RG2 |
|sgtu \$t1,\$t2,-100|Set Greater Than Unsigned : if \$t2 greater than 16-bit immediate (unsigned compare) then set \$t1 to 1 else 0|addi \$1, \$0, VL3 sltu RG1, \$1, RG2 |
|sgtu \$t1,\$t2,100000|Set Greater Than Unsigned : if \$t2 greater than 32-bit immediate (unsigned compare) then set \$t1 to 1 else 0|lui \$1, VHL3 ori \$1, \$1, VL3U sltu RG1, \$1, RG2 |
|sh \$t1,(\$t2)|Store Halfword : Store the low-order 16 bits of \$t1 into the effective memory halfword address|sh RG1,0(RG3) |
|sh \$t1,-100|Store Halfword : Store the low-order 16 bits of \$t1 into the effective memory halfword address|sh RG1, VL2(\$0) |
|sh \$t1,100|Store Halfword : Store the low-order 16 bits of \$t1 into the effective memory halfword address|ori \$1, \$0, VL2U sh RG1, 0(\$1) |
|sh \$t1,100(\$t2)|Store Halfword : Store the low-order 16 bits of \$t1 into the effective memory halfword address|ori \$1, \$0, VL2U addu \$1, \$1, RG4 sh RG1, 0(\$1) |
|sh \$t1,100000|Store Halfword : Store the low-order 16 bits of \$t1 into the effective memory halfword address|lui \$1, VH2 sh RG1,VL2(\$1) |
|sh \$t1,100000(\$t2)|Store Halfword : Store the low-order 16 bits of \$t1 into the effective memory halfword address|lui \$1, VH2 addu \$1, \$1, RG4 sh RG1, VL2(\$1) |
|sh \$t1,label|Store Halfword : Store the low-order 16 bits of \$t1 into the effective memory halfword address|lui \$1, LH2 sh RG1, LL2(\$1) COMPACT sh RG1, LL2(\$0) |
|sh \$t1,label(\$t2)|Store Halfword : Store the low-order 16 bits of \$t1 into the effective memory halfword address|lui \$1, LH2 addu \$1, \$1, RG4 sh RG1, LL2(\$1) COMPACT sh RG1, LL2(RG4) |
|sh \$t1,label+100000|Store Halfword : Store the low-order 16 bits of \$t1 into the effective memory halfword address|lui \$1, LHPA sh RG1, LLP(\$1) |
|sh \$t1,label+100000(\$t2)|Store Halfword : Store the low-order 16 bits of \$t1 into the effective memory halfword address|lui \$1, LHPA addu \$1, \$1, RG6 sh RG1, LLP(\$1) |
|sle \$t1,\$t2,\$t3|Set Less or Equal : if \$t2 less or equal to \$t3 then set \$t1 to 1 else 0|slt RG1, RG3, RG2 ori \$1, \$0, 1 subu RG1, \$1, RG1 |
|sle \$t1,\$t2,-100|Set Less or Equal : if \$t2 less or equal to 16-bit immediate then set \$t1 to 1 else 0|addi \$1, \$0, VL3 slt RG1, \$1, RG2 ori \$1, \$0, 1 subu RG1, \$1, RG1 |
|sle \$t1,\$t2,100000|Set Less or Equal : if \$t2 less or equal to 32-bit immediate then set \$t1 to 1 else 0|lui \$1, VHL3 ori \$1, \$1, VL3U slt RG1, \$1, RG2 ori \$1, \$0, 1 subu RG1, \$1, RG1 |
|sleu \$t1,\$t2,\$t3|Set Less or Equal Unsigned: if \$t2 less or equal to \$t3 (unsigned compare) then set \$t1 to 1 else 0|sltu RG1, RG3, RG2 ori \$1, \$0, 1 subu RG1, \$1, RG1 |
|sleu \$t1,\$t2,-100|Set Less or Equal Unsigned: if \$t2 less or equal to 16-bit immediate (unsigned compare) then set \$t1 to 1 else 0|addi \$1, \$0, VL3 sltu RG1, \$1, RG2 ori \$1, \$0, 1 subu RG1, \$1, RG1 |
|sleu \$t1,\$t2,100000|Set Less or Equal Unsigned: if \$t2 less or equal to 32-bit immediate (unsigned compare) then set \$t1 to 1 else 0|lui \$1, VHL3 ori \$1, \$1, VL3U sltu RG1, \$1, RG2 ori \$1, \$0, 1 subu RG1, \$1, RG1 |
|sne \$t1,\$t2,\$t3|Set Not Equal : if \$t2 not equal to \$t3 then set \$t1 to 1 else 0|subu RG1, RG2, RG3 sltu RG1, \$0, RG1 |
|sne \$t1,\$t2,-100|Set Not Equal : if \$t2 not equal to 16-bit immediate then set \$t1 to 1 else 0|addi \$1, \$0, VL3 subu RG1, RG2, \$1 sltu RG1, \$0, RG1 |
|sne \$t1,\$t2,100000|Set Not Equal : if \$t2 not equal to 32-bit immediate then set \$t1 to 1 else 0|lui \$1, VHL3 ori \$1, \$1, VL3U subu RG1, RG2, \$1 sltu RG1, \$0, RG1 |
|sub \$t1,\$t2,-100|SUBtraction : set \$t1 to (\$t2 minus 16-bit immediate)| addi \$1, \$0, VL3 sub RG1, RG2, \$1 |
|sub \$t1,\$t2,100000|SUBtraction : set \$t1 to (\$t2 minus 32-bit immediate)|lui \$1, VHL3 ori \$1, \$1, VL3U sub RG1, RG2, \$1 |
|subi \$t1,\$t2,-100|SUBtraction Immediate : set \$t1 to (\$t2 minus 16-bit immediate)| addi \$1, \$0, VL3 sub RG1, RG2, \$1 |
|subi \$t1,\$t2,100000|SUBtraction Immediate : set \$t1 to (\$t2 minus 32-bit immediate)|lui \$1, VHL3 ori \$1, \$1, VL3U sub RG1, RG2, \$1 |
|subiu \$t1,\$t2,100000|SUBtraction Immediate Unsigned : set \$t1 to (\$t2 minus 32-bit immediate), no overflow|lui \$1, VHL3 ori \$1, \$1, VL3U subu RG1, RG2, \$1 |
|subu \$t1,\$t2,100000|SUBtraction Unsigned : set \$t1 to (\$t2 minus 32-bit immediate), no overflow|lui \$1, VHL3 ori \$1, \$1, VL3U subu RG1, RG2, \$1 |
|sw \$t1,(\$t2)|Store Word : Store \$t1 contents into effective memory word address|sw RG1,0(RG3) |
|sw \$t1,-100|Store Word : Store \$t1 contents into effective memory word address|sw RG1, VL2(\$0) |
|sw \$t1,100|Store Word : Store \$t1 contents into effective memory word address|ori \$1, \$0, VL2U sw RG1, 0(\$1) |
|sw \$t1,100(\$t2)|Store Word : Store \$t1 contents into effective memory word address|ori \$1, \$0, VL2U addu \$1, \$1, RG4 sw RG1, 0(\$1) |
|sw \$t1,100000|Store Word : Store \$t1 contents into effective memory word address|lui \$1, VH2 sw RG1,VL2(\$1) |
|sw \$t1,100000(\$t2)|Store Word : Store \$t1 contents into effective memory word address|lui \$1, VH2 addu \$1, \$1, RG4 sw RG1, VL2(\$1) |
|sw \$t1,label|Store Word : Store \$t1 contents into memory word at label's address|lui \$1, LH2 sw RG1, LL2(\$1) COMPACT sw RG1, LL2(\$0) |
|sw \$t1,label(\$t2)|Store Word : Store \$t1 contents into effective memory word address|lui \$1, LH2 addu \$1, \$1, RG4 sw RG1, LL2(\$1) COMPACT sw RG1, LL2(RG4) |
|sw \$t1,label+100000|Store Word : Store \$t1 contents into effective memory word address|lui \$1, LHPA sw RG1, LLP(\$1) |
|sw \$t1,label+100000(\$t2)|Store Word : Store \$t1 contents into effective memory word address|lui \$1, LHPA addu \$1, \$1, RG6 sw RG1, LLP(\$1) |
|swc1 \$f1,(\$t2)|Store Word Coprocessor 1 : Store 32-bit value from \$f1 to effective memory word address|swc1 RG1,0(RG3) |
|swc1 \$f1,-100|Store Word Coprocessor 1 : Store 32-bit value from \$f1 to effective memory word address|swc1 RG1,VL2(\$0) |
|swc1 \$f1,100000|Store Word Coprocessor 1 : Store 32-bit value from \$f1 to effective memory word address|lui \$1, VH2 swc1 RG1,VL2(\$1) |
|swc1 \$f1,100000(\$t2)|Store Word Coprocessor 1 : Store 32-bit value from \$f1 to effective memory word address|lui \$1, VH2 addu \$1, \$1, RG4 swc1 RG1, VL2(\$1) |
|swc1 \$f1,label|Store Word Coprocessor 1 : Store 32-bit value from \$f1 to effective memory word address|lui \$1, LH2 swc1 RG1, LL2(\$1) COMPACT swc1 RG1, LL2(\$0) |
|swc1 \$f1,label(\$t2)|Store Word Coprocessor 1 : Store 32-bit value from \$f1 to effective memory word address|lui \$1, LH2 addu \$1, \$1, RG4 swc1 RG1, LL2(\$1) COMPACT swc1 RG1, LL2(RG4) |
|swc1 \$f1,label+100000|Store Word Coprocessor 1 : Store 32-bit value from \$f1 to effective memory word address|lui \$1, LHPA swc1 RG1, LLP(\$1) |
|swc1 \$f1,label+100000(\$t2)|Store Word Coprocessor 1 : Store 32-bit value from \$f1 to effective memory word address|lui \$1, LHPA addu \$1, \$1, RG6 swc1 RG1, LLP(\$1) |
|swl \$t1,(\$t2)|Store Word Left : Store high-order 1 to 4 bytes of \$t1 into memory, starting with effective memory byte address and continuing through the low-order byte of its word|swl RG1,0(RG3) |
|swl \$t1,-100|Store Word Left : Store high-order 1 to 4 bytes of \$t1 into memory, starting with effective memory byte address and continuing through the low-order byte of its word|swl RG1,VL2(\$0) |
|swl \$t1,100|Store Word Left : Store high-order 1 to 4 bytes of \$t1 into memory, starting with effective memory byte address and continuing through the low-order byte of its word|ori \$1, \$0, VL2U swl RG1, 0(\$1) |
|swl \$t1,100(\$t2)|Store Word Left : Store high-order 1 to 4 bytes of \$t1 into memory, starting with effective memory byte address and continuing through the low-order byte of its word|ori \$1, \$0, VL2U addu \$1, \$1, RG4 swl RG1, 0(\$1) |
|swl \$t1,100000|Store Word Left : Store high-order 1 to 4 bytes of \$t1 into memory, starting with effective memory byte address and continuing through the low-order byte of its word|lui \$1, VH2 swl RG1,VL2(\$1) |
|swl \$t1,100000(\$t2)|Store Word Left : Store high-order 1 to 4 bytes of \$t1 into memory, starting with effective memory byte address and continuing through the low-order byte of its word|lui \$1, VH2 addu \$1, \$1, RG4 swl RG1, VL2(\$1) |
|swl \$t1,label|Store Word Left : Store high-order 1 to 4 bytes of \$t1 into memory, starting with effective memory byte address and continuing through the low-order byte of its word|lui \$1, LH2 swl RG1, LL2(\$1) COMPACT swl RG1, LL2(\$0) |
|swl \$t1,label(\$t2)|Store Word Left : Store high-order 1 to 4 bytes of \$t1 into memory, starting with effective memory byte address and continuing through the low-order byte of its word|lui \$1, LH2 addu \$1, \$1, RG4 swl RG1, LL2(\$1) COMPACT swl RG1, LL2(RG4) |
|swl \$t1,label+100000|Store Word Left : Store high-order 1 to 4 bytes of \$t1 into memory, starting with effective memory byte address and continuing through the low-order byte of its word|lui \$1, LHPA swl RG1, LLP(\$1) |
|swl \$t1,label+100000(\$t2)|Store Word Left : Store high-order 1 to 4 bytes of \$t1 into memory, starting with effective memory byte address and continuing through the low-order byte of its word|lui \$1, LHPA addu \$1, \$1, RG6 swl RG1, LLP(\$1) |
|swr \$t1,(\$t2)|Store Word Right : Store low-order 1 to 4 bytes of \$t1 into memory, starting with high-order byte of word containing effective memory byte address and continuing through that byte address|swr RG1,0(RG3) |
|swr \$t1,-100|Store Word Right : Store low-order 1 to 4 bytes of \$t1 into memory, starting with high-order byte of word containing effective memory byte address and continuing through that byte address|swr RG1,VL2(\$0) |
|swr \$t1,100|Store Word Right : Store low-order 1 to 4 bytes of \$t1 into memory, starting with high-order byte of word containing effective memory byte address and continuing through that byte address|ori \$1, \$0, VL2U swr RG1, 0 |
|swr \$t1,100(\$t2)|Store Word Right : Store low-order 1 to 4 bytes of \$t1 into memory, starting with high-order byte of word containing effective memory byte address and continuing through that byte address|ori \$1, \$0, VL2U addu \$1, \$1, RG4 swr RG1, 0(\$1) |
|swr \$t1,100000|Store Word Right : Store low-order 1 to 4 bytes of \$t1 into memory, starting with high-order byte of word containing effective memory byte address and continuing through that byte address|lui \$1, VH2 swr RG1,VL2(\$1) |
|swr \$t1,100000(\$t2)|Store Word Right : Store low-order 1 to 4 bytes of \$t1 into memory, starting with high-order byte of word containing effective memory byte address and continuing through that byte address|lui \$1, VH2 addu \$1, \$1, RG4 swr RG1, VL2(\$1) |
|swr \$t1,label|Store Word Right : Store low-order 1 to 4 bytes of \$t1 into memory, starting with high-order byte of word containing effective memory byte address and continuing through that byte address|lui \$1, LH2 swr RG1, LL2(\$1) COMPACT swr RG1, LL2(\$0) |
|swr \$t1,label(\$t2)|Store Word Right : Store low-order 1 to 4 bytes of \$t1 into memory, starting with high-order byte of word containing effective memory byte address and continuing through that byte address|lui \$1, LH2 addu \$1, \$1, RG4 swr RG1, LL2(\$1) COMPACT swr RG1, LL2(RG4) |
|swr \$t1,label+100000|Store Word Right : Store low-order 1 to 4 bytes of \$t1 into memory, starting with high-order byte of word containing effective memory byte address and continuing through that byte address|lui \$1, LHPA swr RG1, LLP(\$1) |
|swr \$t1,label+100000(\$t2)|Store Word Right : Store low-order 1 to 4 bytes of \$t1 into memory, starting with high-order byte of word containing effective memory byte address and continuing through that byte address|lui \$1, LHPA addu \$1, \$1, RG6 swr RG1, LLP(\$1) |
|ulh \$t1,(\$t2)|Unaligned Load Halfword : Set \$t1 to the 16 bits, sign-extended, starting at effective memory byte address|lb RG1, 1(RG3) lbu \$1, 0(RG3) sll RG1, RG1, 8 or RG1, RG1, \$1  |
|ulh \$t1,-100(\$t2)|Unaligned Load Halfword : Set \$t1 to the 16 bits, sign-extended, starting at effective memory byte address|lui \$1, VH2P1 addu \$1, \$1, RG4 lb RG1, VL2P1(\$1) lbu \$1, VL2(RG4) sll RG1, RG1, 8 or RG1, RG1, \$1 |
|ulh \$t1,100000|Unaligned Load Halfword : Set \$t1 to the 16 bits, sign-extended, starting at effective memory byte address|lui \$1, VH2P1 lb RG1, VL2P1(\$1) lui \$1, VH2 lbu \$1, VL2(\$1) sll RG1, RG1, 8 or RG1, RG1, \$1 |
|ulh \$t1,100000(\$t2)|Unaligned Load Halfword : Set \$t1 to the 16 bits, sign-extended, starting at effective memory byte address|lui \$1, VH2P1 addu \$1, \$1, RG4 lb RG1, VL2P1(\$1) lui \$1, VH2 addu \$1, \$1, RG4 lbu \$1, VL2(\$1) sll RG1, RG1, 8 or RG1, RG1, \$1 |
|ulh \$t1,label|Unaligned Load Halfword : Set \$t1 to the 16 bits, sign-extended, starting at effective memory byte address|lui \$1, LH2P1 lb RG1, LL2P1(\$1) lui \$1, LH2 lbu \$1, LL2(\$1) sll RG1, RG1, 8 or RG1, RG1, \$1 |
|ulh \$t1,label(\$t2)|Unaligned Load Halfword : Set \$t1 to the 16 bits, sign-extended, starting at effective memory byte address|lui \$1, LH2P1 addu \$1, \$1, RG4 lb RG1, LL2P1(\$1) lui \$1, LH2 addu \$1, \$1, RG4 lbu \$1, LL2(\$1) sll RG1, RG1, 8 or RG1, RG1, \$1 |
|ulh \$t1,label+100000|Unaligned Load Halfword : Set \$t1 to the 16 bits, sign-extended, starting at effective memory byte address|lui \$1, LHPAP1 lb RG1, LLPP1(\$1) lui \$1, LHPA lbu \$1, LLP(\$1) sll RG1, RG1, 8 or RG1, RG1, \$1 |
|ulh \$t1,label+100000(\$t2)|Unaligned Load Halfword : Set \$t1 to the 16 bits, sign-extended, starting at effective memory byte address|lui \$1, LHPAP1 addu \$1, \$1, RG6 lb RG1, LLPP1(\$1) lui \$1, LHPA addu \$1, \$1, RG6 lbu \$1, LLP(\$1) sll RG1, RG1, 8 or RG1, RG1, \$1 |
|ulhu \$t1,(\$t2)|Unaligned Load Halfword : Set \$t1 to the 16 bits, zero-extended, starting at effective memory byte address|lbu RG1, 1(RG3) lbu \$1, 0(RG3) sll RG1, RG1, 8 or RG1, RG1, \$1  |
|ulhu \$t1,-100(\$t2)|Unaligned Load Halfword : Set \$t1 to the 16 bits, zero-extended, starting at effective memory byte address|lui \$1, VH2P1 addu \$1, \$1, RG4 lbu RG1, VL2P1(\$1) lbu \$1, VL2(RG4) sll RG1, RG1, 8 or RG1, RG1, \$1 |
|ulhu \$t1,100000|Unaligned Load Halfword : Set \$t1 to the 16 bits, zero-extended, starting at effective memory byte address|lui \$1, VH2P1 lbu RG1, VL2P1(\$1) lui \$1, VH2 lbu \$1, VL2(\$1) sll RG1, RG1, 8 or RG1, RG1, \$1 |
|ulhu \$t1,100000(\$t2)|Unaligned Load Halfword : Set \$t1 to the 16 bits, zero-extended, starting at effective memory byte address|lui \$1, VH2P1 addu \$1, \$1, RG4 lbu RG1, VL2P1(\$1) lui \$1, VH2 addu \$1, \$1, RG4 lbu \$1, VL2(\$1) sll RG1, RG1, 8 or RG1, RG1, \$1 |
|ulhu \$t1,label|Unaligned Load Halfword : Set \$t1 to the 16 bits, zero-extended, starting at effective memory byte address|lui \$1, LH2P1 lbu RG1, LL2P1(\$1) lui \$1, LH2 lbu \$1, LL2(\$1) sll RG1, RG1, 8 or RG1, RG1, \$1 |
|ulhu \$t1,label(\$t2)|Unaligned Load Halfword : Set \$t1 to the 16 bits, zero-extended, starting at effective memory byte address|lui \$1, LH2P1 addu \$1, \$1, RG4 lbu RG1, LL2P1(\$1) lui \$1, LH2 addu \$1, \$1, RG4 lbu \$1, LL2(\$1) sll RG1, RG1, 8 or RG1, RG1, \$1 |
|ulhu \$t1,label+100000|Unaligned Load Halfword : Set \$t1 to the 16 bits, zero-extended, starting at effective memory byte address|lui \$1, LHPAP1 lbu RG1, LLPP1(\$1) lui \$1, LHPA lbu \$1, LLP(\$1) sll RG1, RG1, 8 or RG1, RG1, \$1 |
|ulhu \$t1,label+100000(\$t2)|Unaligned Load Halfword : Set \$t1 to the 16 bits, zero-extended, starting at effective memory byte address|lui \$1, LHPAP1 addu \$1, \$1, RG6 lbu RG1, LLPP1(\$1) lui \$1, LHPA addu \$1, \$1, RG6 lbu \$1, LLP(\$1) sll RG1, RG1, 8 or RG1, RG1, \$1 |
|ulw \$t1,(\$t2)|Unaligned Load Word : Set \$t1 to the 32 bits starting at effective memory byte address|lwl RG1, 3(RG3) lwr RG1, 0(RG3) |
|ulw \$t1,-100(\$t2)|Unaligned Load Word : Set \$t1 to the 32 bits starting at effective memory byte address|lui \$1, VH2P3 addu \$1, \$1, RG4 lwl RG1, VL2P3(\$1) lwr RG1, VL2(RG4) |
|ulw \$t1,100000|Unaligned Load Word : Set \$t1 to the 32 bits starting at effective memory byte address|lui \$1, VH2P3 lwl RG1, VL2P3(\$1) lui \$1, VH2 lwr RG1, VL2(\$1) |
|ulw \$t1,100000(\$t2)|Unaligned Load Word : Set \$t1 to the 32 bits starting at effective memory byte address|lui \$1, VH2P3 addu \$1, \$1, RG4 lwl RG1, VL2P3(\$1) lui \$1, VH2 addu \$1, \$1, RG4 lwr RG1, VL2(\$1) |
|ulw \$t1,label|Unaligned Load Word : Set \$t1 to the 32 bits starting at effective memory byte address|lui \$1, LH2P3 lwl RG1, LL2P3(\$1) lui \$1, LH2 lwr RG1, LL2(\$1) |
|ulw \$t1,label(\$t2)|Unaligned Load Word : Set \$t1 to the 32 bits starting at effective memory byte address|lui \$1, LH2P3 addu \$1, \$1, RG4 lwl RG1, LL2P3(\$1) lui \$1, LH2 addu \$1, \$1, RG4 lwr RG1, LL2(\$1) |
|ulw \$t1,label+100000|Unaligned Load Word : Set \$t1 to the 32 bits starting at effective memory byte address|lui \$1, LHPAP3 lwl RG1, LLPP3(\$1) lui \$1, LHPA lwr RG1, LLP(\$1) |
|ulw \$t1,label+100000(\$t2)|Unaligned Load Word : Set \$t1 to the 32 bits starting at effective memory byte address|lui \$1, LHPAP3 addu \$1, \$1, RG6 lwl RG1, LLPP3(\$1) lui \$1, LHPA addu \$1, \$1, RG6 lwr RG1, LLP(\$1) |
|ush \$t1,(\$t2)|Unaligned Store Halfword: Store low-order halfword \$t1 contents into the 16 bits starting at effective memory byte address|sb RG1, 0(RG3) sll \$1, RG1, 24 srl RG1, RG1, 8 or RG1, RG1, \$1 sb RG1, 1(RG3) srl \$1, RG1, 24 sll RG1, RG1, 8 or RG1, RG1, \$1 |
|ush \$t1,-100(\$t2)|Unaligned Store Halfword: Store low-order halfword \$t1 contents into the 16 bits starting at effective memory byte address|sb RG1, VL2(RG4) sll \$1, RG1, 24 srl RG1, RG1, 8 or RG1, RG1, \$1 lui \$1, VH2P1 addu \$1, \$1, RG4 sb RG1, VL2P1(\$1) srl \$1, RG1, 24 sll RG1, RG1, 8 or RG1, RG1, \$1 |
|ush \$t1,100000|Unaligned Store Halfword: Store low-order halfword \$t1 contents into the 16 bits starting at effective memory byte address|lui \$1, VH2 sb RG1, VL2(\$1) sll \$1, RG1, 24 srl RG1, RG1, 8 or RG1, RG1, \$1 lui \$1, VH2P1 sb RG1, VL2P1(\$1) srl \$1, RG1, 24 sll RG1, RG1, 8 or RG1, RG1, \$1 |
|ush \$t1,100000(\$t2)|Unaligned Store Halfword: Store low-order halfword \$t1 contents into the 16 bits starting at effective memory byte address|lui \$1, VH2 addu \$1, \$1, RG4 sb RG1, VL2(\$1) sll \$1, RG1, 24 srl RG1, RG1, 8 or RG1, RG1, \$1 lui \$1, VH2P1 addu \$1, \$1, RG4 sb RG1, VL2P1(\$1) srl \$1, RG1, 24 sll RG1, RG1, 8 or RG1, RG1, \$1 |
|ush \$t1,label|Unaligned Store Halfword: Store low-order halfword \$t1 contents into the 16 bits starting at effective memory byte address|lui \$1, LH2 sb RG1, LL2(\$1) sll \$1, RG1, 24 srl RG1, RG1, 8 or RG1, RG1, \$1 lui \$1, LH2P1 sb RG1, LL2P1(\$1) srl \$1, RG1, 24 sll RG1, RG1, 8 or RG1, RG1, \$1 |
|ush \$t1,label(\$t2)|Unaligned Store Halfword: Store low-order halfword \$t1 contents into the 16 bits starting at effective memory byte address|lui \$1, LH2 addu \$1, \$1, RG4 sb RG1, LL2(\$1) sll \$1, RG1, 24 srl RG1, RG1, 8 or RG1, RG1, \$1 lui \$1, LH2P1 addu \$1, \$1, RG4 sb RG1, LL2P1(\$1) srl \$1, RG1, 24 sll RG1, RG1, 8 or RG1, RG1, \$1 |
|ush \$t1,label+100000|Unaligned Store Halfword: Store low-order halfword \$t1 contents into the 16 bits starting at effective memory byte address|lui \$1, LHPA sb RG1, LLP(\$1) sll \$1, RG1, 24 srl RG1, RG1, 8 or RG1, RG1, \$1 lui \$1, LHPAP1 sb RG1, LLPP1(\$1) srl \$1, RG1, 24 sll RG1, RG1, 8 or RG1, RG1, \$1 |
|ush \$t1,label+100000(\$t2)|Unaligned Store Halfword: Store low-order halfword \$t1 contents into the 16 bits starting at effective memory byte address|lui \$1, LHPA addu \$1, \$1, RG6 sb RG1, LLP(\$1) sll \$1, RG1, 24 srl RG1, RG1, 8 or RG1, RG1, \$1 lui \$1, LHPAP1 addu \$1, \$1, RG6 sb RG1, LLPP1(\$1) srl \$1, RG1, 24 sll RG1, RG1, 8 or RG1, RG1, \$1 |
|usw \$t1,(\$t2)|Unaligned Store Word : Store \$t1 contents into the 32 bits starting at effective memory byte address|swl RG1, 3(RG3) swr RG1, 0(RG3) |
|usw \$t1,-100(\$t2)|Unaligned Store Word : Store \$t1 contents into the 32 bits starting at effective memory byte address|lui \$1, VH2P3 addu \$1, \$1, RG4 swl RG1, VL2P3(\$1) swr RG1, VL2(RG4) |
|usw \$t1,100000|Unaligned Store Word : Store \$t1 contents into the 32 bits starting at effective memory byte address|lui \$1, VH2P3 swl RG1, VL2P3(\$1) lui \$1, VH2 swr RG1, VL2(\$1) |
|usw \$t1,100000(\$t2)|Unaligned Store Word : Store \$t1 contents into the 32 bits starting at effective memory byte address|lui \$1, VH2P3 addu \$1, \$1, RG4 swl RG1, VL2P3(\$1) lui \$1, VH2 addu \$1, \$1, RG4 swr RG1, VL2(\$1) |
|usw \$t1,label|Unaligned Store Word : Store \$t1 contents into the 32 bits starting at effective memory byte address|lui \$1, LH2P3 swl RG1, LL2P3(\$1) lui \$1, LH2 swr RG1, LL2(\$1) |
|usw \$t1,label(\$t2)|Unaligned Store Word : Store \$t1 contents into the 32 bits starting at effective memory byte address|lui \$1, LH2P3 addu \$1, \$1, RG4 swl RG1, LL2P3(\$1) lui \$1, LH2 addu \$1, \$1, RG4 swr RG1, LL2(\$1) |
|usw \$t1,label+100000|Unaligned Store Word : Store \$t1 contents into the 32 bits starting at effective memory byte address|lui \$1, LHPAP3 swl RG1, LLPP3(\$1) lui \$1, LHPA swr RG1, LLP(\$1) |
|usw \$t1,label+100000(\$t2)|Unaligned Store Word : Store \$t1 contents into the 32 bits starting at effective memory byte address|lui \$1, LHPAP3 addu \$1, \$1, RG6 swl RG1, LLPP3(\$1) lui \$1, LHPA addu \$1, \$1, RG6 swr RG1, LLP(\$1) |
|xor \$t1,\$t2,100|XOR : set \$t1 to (\$t2 bitwise-exclusive-OR 16-bit unsigned immediate)|xori RG1, RG2, VL3U |
|xor \$t1,100|XOR : set \$t1 to (\$t1 bitwise-exclusive-OR 16-bit unsigned immediate)|xori RG1, RG1, VL2U |
|xori \$t1,\$t2,100000|XOR Immediate : set \$t1 to (\$t2 bitwise-exclusive-OR 32-bit immediate)|lui \$1, VHL3 ori \$1, \$1, VL3U xor RG1, RG2, \$1 |
|xori \$t1,100|XOR Immediate : set \$t1 to (\$t1 bitwise-exclusive-OR 16-bit unsigned immediate)|xori RG1, RG1, VL2U |
|xori \$t1,100000|XOR Immediate : set \$t1 to (\$t1 bitwise-exclusive-OR 32-bit immediate)|lui \$1, VHL2 ori \$1, \$1, VL2U xor RG1, RG1, \$1 |
### Directives
|Directive|Explanation|
|---|---|
|.align|Align next data item on specified byte boundary (0=byte, 1=half, 2=word, 3=double)|
|.ascii|Store the string in the Data segment but do not add null terminator|
|.asciiz|Store the string in the Data segment and add null terminator|
|.byte|Store the listed value(s) as 8 bit bytes|
|.data|Subsequent items stored in Data segment at next available address|
|.double|Store the listed value(s) as double precision floating point|
|.end_macro|End macro definition.  See .macro|
|.eqv|Substitute second operand for first. First operand is symbol, second operand is expression (like #define)|
|.extern|Declare the listed label and byte length to be a global data field|
|.float|Store the listed value(s) as single precision floating point|
|.globl|Declare the listed label(s) as global to enable referencing from other files|
|.half|Store the listed value(s) as 16 bit halfwords on halfword boundary|
|.include|Insert the contents of the specified file.  Put filename in quotes.|
|.kdata|Subsequent items stored in Kernel Data segment at next available address|
|.ktext|Subsequent items (instructions) stored in Kernel Text segment at next available address|
|.macro|Begin macro definition.  See .end_macro|
|.set|Set assembler variables.  Currently ignored but included for SPIM compatability|
|.space|Reserve the next specified number of bytes in Data segment|
|.text|Subsequent items (instructions) stored in Text segment at next available address|
|.word|Store the listed value(s) as 32 bit words on word boundary|

### Syscall
<table>
  <tr>  <th>Service</th>  <th>Code in $v0</th>  <th>Arguments</th>  <th>Result</th>  </tr>
  <tr><td>print integer</td>                 <td align="center">1</td>   <td>$a0 = integer to print</td>  <td>&nbsp;</td></tr>
  <tr><td>print float</td>                   <td align="center">2</td>   <td>$f12 = float to print</td>   <td>&nbsp;</td></tr>
  <tr><td>print double</td>                  <td align="center">3</td>   <td>$f12 = double to print</td>  <td>&nbsp;</td></tr>
  <tr><td>print string</td>                  <td align="center">4</td>   <td>$a0 = address of null-terminated string to print</td>  <td>&nbsp;</td></tr>
  <tr><td>read integer</td>                  <td align="center">5</td>   <td>&nbsp;</td>  <td>$v0 contains integer read</td></tr>
  <tr><td>read float</td>                    <td align="center">6</td>   <td>&nbsp;</td>  <td>$f0 contains float read</td></tr>
  <tr><td>read double</td>                   <td align="center">7</td>   <td>&nbsp;</td>  <td>$f0 contains double read</td></tr>
  <tr><td>read string</td>                   <td align="center">8</td>   <td>$a0 = address of input buffer<br>$a1 = maximum number of characters to read</td>  <td><i>See note below table</i></td></tr>
  <tr><td>sbrk (allocate heap memory)</td>   <td align="center">9</td>   <td>$a0 = number of bytes to allocate</td>  <td>$v0 contains address of allocated memory</td></tr>
  <tr><td>exit (terminate execution)</td>   <td align="center">10</td>   <td>&nbsp;</td>  <td>&nbsp;</td></tr>
  <tr><td>print character</td>              <td align="center">11</td>   <td>$a0 = character to print</td>  <td><i>See note below table</i></td></tr>
  <tr><td>read character</td>               <td align="center">12</td>   <td>&nbsp;</td>  <td>$v0 contains character read</td></tr>
  <tr><td>open file</td>                    <td align="center">13</td>   <td>$a0 = address of null-terminated string containing filename<br>$a1 = flags<br>$a2 = mode</td>  <td>$v0 contains file descriptor (negative if error).  <i>See note below table</i></td></tr>
  <tr><td>read from file</td>               <td align="center">14</td>   <td>$a0 = file descriptor<br>$a1 = address of input buffer<br>$a2 = maximum number of characters to read</td>  <td>$v0 contains number of characters read (0 if end-of-file, negative if error).  <i>See note below table</i></td></tr>
  <tr><td>write to file</td>                <td align="center">15</td>   <td>$a0 = file descriptor<br>$a1 = address of output buffer<br>$a2 = number of characters to write</td>  <td>$v0 contains number of characters written (negative if error).  <i>See note below table</i></td></tr>
  <tr><td>close file</td>                   <td align="center">16</td>   <td>$a0 = file descriptor</td>  <td>&nbsp;</td></tr>
  <tr><td>exit2 (terminate with value)</td> <td align="center">17</td>   <td>$a0 = termination result</td>  <td><i>See note below table</i></td></tr>
  <tr><td align="center" colspan=4><em>Services 1 through 17 are compatible with the SPIM simulator, other than Open File (13) as described in the Notes below the table.
  Services 30 and higher are exclusive to MARS.</em></td></tr>
  <tr><td>time (system time)</td>           <td align="center">30</td>   <td>&nbsp;</td><td>$a0 = low order 32 bits of system time<br>$a1 = high order 32 bits of system time.  <i>See note below table</i></td></tr>
  <tr><td>MIDI out</td>                     <td align="center">31</td>   <td>$a0 = pitch (0-127)<br>$a1 = duration in milliseconds<br>$a2 = instrument (0-127)<br>$a3 = volume (0-127)</td>  <td>Generate tone and return immediately.  <i>See note below table</i></td></tr>
  <tr><td>sleep</td>                        <td align="center">32</td>   <td>$a0 = the length of time to sleep in milliseconds.</td>  <td>Causes the MARS Java thread to sleep for (at least) the specified number of milliseconds. This timing will not be precise, as the Java implementation will add some overhead.</td></tr>
  <tr><td>MIDI out synchronous              <td align="center">33</td>   <td>$a0 = pitch (0-127)<br>$a1 = duration in milliseconds<br>$a2 = instrument (0-127)<br>$a3 = volume (0-127)</td>  <td>Generate tone and return upon tone completion.  <i>See note below table</i></td></tr>
  <tr><td>print integer in hexadecimal</td> <td align="center">34</td>   <td>$a0 = integer to print</td>  <td>Displayed value is 8 hexadecimal digits, left-padding with zeroes if necessary.</td></tr>
  <tr><td>print integer in binary</td>      <td align="center">35</td>   <td>$a0 = integer to print</td>  <td>Displayed value is 32 bits, left-padding with zeroes if necessary.</td></tr>
  <tr><td>print integer as unsigned</td>    <td align="center">36</td>   <td>$a0 = integer to print</td>  <td>Displayed as unsigned decimal value.</td></tr>
  <tr><td align="center">(not used)</td>    <td align="center">37-39</td><td>&nbsp;</td>  <td>&nbsp;</td></tr>
  <tr><td>set seed</td>                     <td align="center">40</td>   <td>$a0 = i.d. of pseudorandom number generator (any int).<br>$a1 = seed for corresponding pseudorandom number generator.</td>  <td>No values are returned. Sets the seed of the corresponding underlying Java pseudorandom number generator (<tt>java.util.Random</tt>). <i>See note below table</i></td></tr>
  <tr><td>random int</td>                   <td align="center">41</td>   <td>$a0 = i.d. of pseudorandom number generator (any int).</td>  <td>$a0 contains the next pseudorandom, uniformly distributed int value from this random number generator's sequence. <i>See note below table</i></td></tr>
  <tr><td>random int range</td>             <td align="center">42</td>   <td>$a0 = i.d. of pseudorandom number generator (any int).<br>$a1 = upper bound of range of returned values.</td>  <td>$a0 contains pseudorandom, uniformly distributed int value in the range 0 <= [int] < [upper bound], drawn from this random number generator's sequence.  <i>See note below table</i></td></tr>
  <tr><td>random float</td>                 <td align="center">43</td>   <td>$a0 = i.d. of pseudorandom number generator (any int).</td>  <td>$f0 contains the next pseudorandom, uniformly distributed float value in the range 0.0 <= f < 1.0 from this random number generator's sequence.  <i>See note below table</i></td></tr>
  <tr><td>random double</td>                <td align="center">44</td>   <td>$a0 = i.d. of pseudorandom number generator (any int).</td>  <td>$f0 contains the next pseudorandom, uniformly distributed double value in the range 0.0 <= f < 1.0 from this random number generator's sequence.  <i>See note below table</i></td></tr>
  <tr><td align="center">(not used)</td>    <td align="center">45-49</td><td>&nbsp;</td>  <td>&nbsp;</td></tr>
  <tr><td>ConfirmDialog</td>                <td align="center">50</td>   <td>$a0 = address of null-terminated string that is the message to user</td>  <td>$a0 contains value of user-chosen option<br>0: Yes<br>1: No<br>2: Cancel</td></tr>
  <tr><td>InputDialogInt</td>               <td align="center">51</td>   <td>$a0 = address of null-terminated string that is the message to user</td>  <td>$a0 contains int read<br>$a1 contains status value<br>0: OK status<br>-1: input data cannot be correctly parsed<br>-2: Cancel was chosen<br>-3: OK was chosen but no data had been input into field</td></tr>
  <tr><td>InputDialogFloat</td>             <td align="center">52</td>   <td>$a0 = address of null-terminated string that is the message to user</td>  <td>$f0 contains float read<br>$a1 contains status value<br>0: OK status<br>-1: input data cannot be correctly parsed<br>-2: Cancel was chosen<br>-3: OK was chosen but no data had been input into field</td></tr>
  <tr><td>InputDialogDouble</td>            <td align="center">53</td>   <td>$a0 = address of null-terminated string that is the message to user</td>  <td>$f0 contains double read<br>$a1 contains status value<br>0: OK status<br>-1: input data cannot be correctly parsed<br>-2: Cancel was chosen<br>-3: OK was chosen but no data had been input into field</td></tr>
  <tr><td>InputDialogString</td>            <td align="center">54</td>   <td>$a0 = address of null-terminated string that is the message to user<br>$a1 = address of input buffer<br>$a2 = maximum number of characters to read</td>  <td><i>See Service 8 note below table</i><br>$a1 contains status value<br>0: OK status. Buffer contains the input string.<br>-2: Cancel was chosen. No change to buffer. <br>-3: OK was chosen but no data had been input into field. No change to buffer.<br>-4: length of the input string exceeded the specified maximum. Buffer contains the maximum allowable input string plus a terminating null.</td></tr>
  <tr><td>MessageDialog</td>                <td align="center">55</td>   <td>$a0 = address of null-terminated string that is the message to user<br>$a1 = the type of message to be displayed:<br> 
0: error message, indicated by Error icon <!-- <img src="SyscallMessageDialogError.gif"> --> <br>
1: information message, indicated by Information icon <!-- <img src="SyscallMessageDialogInformation.gif"> --> <br>
2: warning message, indicated by Warning icon <!-- <img src="SyscallMessageDialogWarning.gif"> --> <br>
3: question message, indicated by Question icon <!-- <img src="SyscallMessageDialogQuestion.gif"> --> <br>
other: plain message (no icon displayed)
</td>  <td>N/A</td></tr>
  <tr><td>MessageDialogInt</td>             <td align="center">56</td>   <td>$a0 = address of null-terminated string that is an information-type message to user<br>$a1 = int value to display in string form after the first string</td>  <td>N/A</td></tr>
  <tr><td>MessageDialogFloat</td>           <td align="center">57</td>   <td>$a0 = address of null-terminated string that is an information-type message to user<br>$f12 = float value to display in string form after the first string</td>  <td>N/A</td></tr>
  <tr><td>MessageDialogDouble</td>          <td align="center">58</td>   <td>$a0 = address of null-terminated string that is an information-type message to user<br>$f12 = double value to display in string form after the first string</td>  <td>N/A</td></tr>
  <tr><td>MessageDialogString</td>          <td align="center">59</td>   <td>$a0 = address of null-terminated string that is an information-type message to user<br>$a1 = address of null-terminated string to display after the first string</td>  <td>N/A</td></tr>
</table>
