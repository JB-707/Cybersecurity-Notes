# Assembly Basics

since the CPU speaks in binary, all your code will eventually be turned into binary instructions
for your CPU to execute

binary code is vary hard for humans to understand, so people created a text representation of 
binary instructions, and the representation is called ***ASSEMBLY***

unlike most programming languages, where one command may require multiple instructions,
assembly is a one to one mapping, or equivilent, to binary. Each assembly instruction maps to
one binary instruction, and the inverse is also true.

## Assembly History

Assembly gets its name becasue asembly code needs to be assembled into binary, not compiled

It was invented by Kathleen Booth in late 1940's, for the APE(X)C  
(All-purpose Electronis(Rayon) Computer)

The second "stored-program computer" has an assembler, written by David Wheeler in 1948

## More about assembly
Assembly gives the CPU instructions to execure

assembly instructions give the CPU a specified set of things to do
an assembly isntruction needstwo things, an operation and an operand

the operation defines the "what to do" and the operand defines "what to do it to"

Assembly is arguably the easiest programming language, due to it's simplicity

Generally, the CPU look for operands to an instruction in three ways:
- Looks for any direct data given in the instructions
- Look into a register that is activly holding data that's being used
- Look through it's cache, or loads in memory from the memory card/disk for data.

The operations that are available may depend on your CPU architecture, but for x86 assembly,
some of these operaionts include:
- add (adds data together)
- sub (subtracts data)
- mul (multiplies data together)
- div (divides data together)
- mov (moves data from one place to another)
- cmp (compares two pieces of data to each other)
- test ( tests some other properties of data)

## Assembly Dialects
Since assembly is a direct trnasaltion of binary code, assembly is dependent on the CPU architecture
which means there can be multiple different dialects

some of these dialects include:
- x86 (best)
- arm (most populat)
- ppc
- mips (bad)
- risc-v
- pdp-11

Reguardless of dialect, a instruction should always be formatted in this manner:
OPERATION OPERANDS
OPERATION

### sub dialects
In the beginning of x86, Intel created
- Intel 808 CPU
- Intel 8085 CPU
- Intel 8086 CPU
- Intel 80186 CPU
- Intel 80286 CPU
- Intel 80386 CPU
the x86 architecture was made for these CPU's originally

AT&T then creted their own assembly syntax for x86, and it's terrible

tl;dr: there are two competing assembly syntaxes for the c86 architecture:
Intel syntax(the right one) and the AT&T syntax(will damage mental health)

if you can, refrain from using AT&T syntax, for the health of you and others around you

***PS: technically, AMD created the x86-64 bit architecture, which is what most 64 bit computers
use, but there is little difference between.***


