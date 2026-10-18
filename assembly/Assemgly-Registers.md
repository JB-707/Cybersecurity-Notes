# Assembly Registers

registers are small units of memory that are the most easilly accessable to the CPU

they are used to store small pieces of data, and will eventually be used to run commands

since registers live inside the CPU, and are expensive to make, there arevey few of them

you will usually be working with "general purpouse" registers. The gernal registers for some CPUs
include:

- 8085[a, c, d, r, h, l]
- 8086[ ax, cd, dx, bx, sp, bp, si, di]
- x86 [eax, ecx, edx, ebx, esp, ebp, esi, edi]
- amd64[rax, rcx, rdx, rbx, rsp, rbp, rsi, rdi, r8, r9, r10, r11, r12, r13, r14, r15]
- arm[r0, r1, r2, r3, r4, r5, r6, r7, r8, r9, r10, r11, r12, r13, r14]

there are some registers that are special, like the instruction pointer register, which contains the address of the next instruction:
- x86 [eip]
- amd64 [rip]
- arm[r15]

There are other registers used for different things, like multimedia computation, which is very 
usefull for embedded programming, but aren't very common to use

A register is usually the wize of the word width in your CPU's architecture. 
For a 64 bit architecture, you'll registers will msot likey hold 64 bits (8 bytes | 16 nibbles)

## Partial Register Access

You also have the ability to read/write to a specific sub-portion of the register, rather then the 
full register. This easy to explain with x86. Starting from the intel 8086, we had the ax register. 
But as the architecture sizes got bigger, intel(and later amd) expanded the size of the register,
to later get eax (Extended ax), and rax (Really extended AX). Intel and amd still allowed you to 
write to the smaller sub-registers of the AX register, and this is called partial register access.

***side note: any data explicitly added to an instruction is called an immediate value***

> **WARNING**

if you modify a sub-portion of a register, modifying a bigger portion of the register, or the whole
register iself, will zero out the sub-portion. This specifically happens with 32 bit registers,
and it's done for performance reasons, to both eliminate "false" hardware dependencies, and to 
add a automatic zero-extension for 64 bit math, which most languages use.

## moving data around

To move data from one point to another, you use the mov operator. 

> **WARNING**
"mov" doesn't move the data, it simply copies the data, and  pastes it into the specified area.
it does NOT remove the data from it's original place.

You may also move data into a regisers smaller sub-portions. Just make sure the sizes line up,
otherwise you might get a SIGSEGV, or a overflow/underflow.

## Extending data
consider the following instruction
```asm
mov eax, 1
```
eax is now 0xffffffff(due to 2's compliments, this is both 4294967295 and -1)

but rax is now 0x00000000ffffffff, which is only 429...!

to fix this issue, you want to use the movsx operatior, also known as the 
move with sign-extention, to preserve the two's compliment value(it copies the top bit to the
rest of the register)

```asm
movsx rax, eax
```
### special registers
some registers "souldn't" be touched or accessed. One example is the rip(instruction pointer). 
This register points to the next instruction to be ran (can be used for cool things !D)

Another example is the stack pointer (rsp), which contains the address of a region in memory to
sore temporary data

There are many other registers like these out there, look them up if you are unsure.

