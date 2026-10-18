# COMPUTER ARCHITECTURE

All code eventually leads to the CPU, whether it's interpreted or compiled

## digging deeper
Your CPU is made up of a bunch of small circuts, organized into logic gates to compute values and
give you everything you see on your computer

There are 4 main logic gates:
- AND gate (if 1 AND 2 are true, the output is TRUE)
- OR gate(if 1 OR 2 are true, then the output is TRUE)
- NOT gate(if 1 is FALSE, then the output is TRUE)
- XOR gate(if and ONLY IF 1 or 2 is true, the output is true)

By combining these main logic gates in clever ways, we can start creating computing components

One example of these is an ADDER, which is a unit that takes two numbers and a carry flag, and 
computes the sum of the two numbers

Another example is a MULTIPLEXER, which gives you the ability to chose which output you want to use
from the unit.

## computer architecture (very high level)

After some time, you eventually get to a computer, which usually holds these main components

- a CPU
- "Some sort of bridge"(we'll find out what this is later)
- Disk
- NC, BT, etc.

A cpu isn't just some monolythic unit, it also carries components with it. Some of these incluse:

- CU(Control Unit; Decides what processes to execute, decodes instructions, dispatches data)
- Registers(small bits of memory that are the msot accessable to the CPU, used for quick comp.)
- ALU(arithmatic logical unit; various computations are donehere)
- Cache(bigger, but less accessable sotrage unit for the CPU)

The CPU only has memory access to its registers and the cache. Every othermemory component gets
loaded in or out through "Some sort of bridge" to your CPU

your CPU may also have multiple cores, or sections, each with their own CU, ALU, registers, and 
caches. Usually, each core will have one small cahce, and also share one larger cache

## CPU history

everything concerning the CPU and it's architecture was invented by three smart indiviuals
John Mauchly(Physicist), John Presper Eckert(Electrical Engineer), and John Von Neumann(math.)

***PS: john mauchly and john presper wrote the original draft, which 
john von neuman took credit for***


