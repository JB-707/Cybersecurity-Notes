# MEMORY

## THE NEED FOR MEMORY

registers are really expensive to manufacture, so you will get a limited number of them

this created a need for a bigger area to store data, while too having fairly fast CPU access.
This place is system memory

When the CPU requests memory, it flows from your RAM card into your CPU's various caches, and from
those caches, you can add the data into your registers as needed

## MEMORY PROCESS PERSPECTIVE

your system memory( or RAM), is used for A LOT
 - registers
 - disk r&w
 - NC tx&rx
 - video card

 System memory is addressed linearly, from 0x10000 to 0x7fffffffffffff

 Each memory address refernces one byte(8 bits) in memory. This means 127 terabytes of addressable
 RAM

## A PROCESS MEMORY

you don't actually have 127 TB of RAM. Most of that RAM is virual. Your System memory gets 
partially filled in by your OS. If you want to use that memory, you'll have to ask for it.


## MEMORY ( THE STACK)

The stack refers to a region of memory that is used mostly for temporary data storage. ]

You can push values and immediates to the stack to save them for later, using the push operator

```asm
mov rax, 0xc001ca75
push rax        # NOTE: push acts like mov, it doesn't destory the original source of the data
push 0xb0bacafe # WARNING: you can only push 32 bit immediates...
push rax 

pop rbx         #sets rbx to 0xc001ca75
pop rcx         #sets rcx to 0xb0bacafe
```

The stack works like a stack because it is one. The last thing pushed is the first thing popped

***PS: pop also doesn't remove anything from the stack, it simple moves the data, then sets the 
stack pointer over a byte to move past the data. It's still there***

 
### ADDRESSING THE STACK

 At the start of a proram, the stack gets randomly defined in memory. The start of the stack is 
 placed in the stack pointer, so the CPU knows where it is. 

 The stack also grows backwards toward smaller memory addresses. So push decreases the stack, and
 pop increases the stack.


## ACCESSING MEMORY

you can move data between registers and memory with the mov operator
```asm
mov rax, 0x1333337
mov rbx, [rax]      #the brackets define a register as a pointer to a memory address
```
The code above stores into rbx whatever value is at the memory addres 0x1333337.

> [WARNING]
If you're going to use the stack, please ensure the memory address you're using actually
has data in it. Otherwise your program will crash from a SIGSEGV error.

## CONTROLLING WRITE SIZES

 You can use partials register access to store/load fewer bits

```asm
mov rax, 0x12345
mov bh, [rax]
```
The code above stores 8 bits from 0x12345 to bh

> [WARNING]
Don't forgat: changing 32-bit partials zeroes out the whole 64-bit register. But storing 32-bit
memory has no such problems


## MEMORY ENDIANESS

Data on most modern systems is tored backwards, in what's called little endian

```asm
mov eax, 0xc001ca75
mov rcx, 0x10000
mov [rcx], eax      # stores data as 75ca01c0
mov bh, [rcx]       # reads 0x75
```
### WHY LITTLE ENDIAN?

little endian was created by intel for a company called datapoint in 1972

Datapoint used little endian for easier implementation of carrying in arithmetic

Intel used little endian in 8008 for compatibility with datapoint's processes

Every step in the evolution between 8008 and modern x86 maintained some level of binary
compatibility with its predecessor

> [WARNING]

if you are dealing with multiple processors, make sure you remember the endianess of that
processor, otherwise, it could lead to errors or misrep. of data. Some processors store the
data stored in the stack normally, also known as big endian.

LITTLE ENDIAN ONLY APPLIES TO THE BITS. THE BYTE ORDER STAYS THE SAME.


## ADDRESS CALCULATION

You can do some limited calculation for memory addresses

You can use rax as an offset of some base address(in this case, the stack pointer)

```asm
mov rax, 0
mov rbx, [rsp+rax*8]        #read a qword right at the stack pointer
inc rax
mov rcx, [rsp+rax*8]        #read the qword to the right of the previous one
```

You may also get the calculated address with load effective address(lea)

```asm
mov rax, 1
pop rcx
lea rbx, [rsp+rax*8+5]      #rbx now holds the computed address for double-checking
mov rbx, [rbx]
```

Address calculation can only go so far, specifically, only up to this ammount oc calculations:

```asm
rsp+rax*(2 or 4 or 4)+rbx       #rax -> offset | rbx -> immediate
```

## RIP RELATIVE ADDRESSING

lea is one of the few instructions that can directly access the instruction pointer

```asm
lea rax, [rip]      #loads the address of the next instruction into rax
lea rax, [rip+8]    #loads the address of the next instruction, plus 8 bytes
```

You can also use mov to read directly from those locations

```asm
mov rax, [rip]      #loads 8 bytes form the instruction pointer into rax

mov [rip], rax      #you can also write to rip. This writes to the next instruction
                    #(ALL CAVEATS APPLY)
```

This is useful for working with data embedded near your code, and is what certain security features
on modern machines possible

## WRITING IMMEDIATE VALUES

You can also writes immediate values. However, you must specify their size

```asm
mov rax, 0x133337
mod DWORD PTR [rax], 0x1337
```

the syntax used to specify the size of data isn't an instruciton in assembly, but instead
is an instruction that the assember reads. This means that the syntax to specify size
might vary depending on your assember, but this works for the GNU assembler

This only applies to anything smaller then the max word size. If you nned to move any smaller data,
you must specify size

## OTHER MEMORY REGIONS

Other memory regions might be mapped in memory

One example is the HEAP.

You may also allocate memory regions in your program if need be





