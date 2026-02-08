Processors:
- IA32, the traditional x86
- x86-64, the standard

Code Forms:
- Machine Code: The byte-level programs that a processor executes
- Assembly Code: A text representation of machine code

Turning C to machine code = Source Code → Preprocessor (.i) → Compiler (.s) → Assembler (.o) → Linker (.exe)

# Assembly code commands

## movq

Syntax: movq source, destination

Instruction, Action, Equivalent C Code

"movq (%rdi), %rax", Read memory to register, t1 = *xp

"movq (%rsi), %rdx", Read memory to register, t2 = *yp

"movq %rax, (%rsi)", Write register to memory, *yp = t1

"movq %rdx, (%rdi)", Write register to memory, *xp = t2

# Simple Memory Addressing
1. Normal (R)
This is the most basic form of memory access. The register contains the actual memory address.

Math: Memory[Register]

C Equivalent: val = *ptr;

Example: movq (%rcx), %rax (Go to the address stored in %rcx, get the data, and put it in %rax).

2. Displacement D(R)
This adds a fixed number (offset) to the address in the register. This is how the CPU accesses specific fields in a Struct or a local variable on the Stack.

Math: Memory[Register + Constant]

Example: movq 8(%rbp), %rdx (Go to the address in %rbp, add 8 bytes, and read the data there).

# General form of memroy addressing mode 

The General Formula
D(Rb, Ri, S) translates to: Address = BaseRegister + (IndexRegister * Scale) + Displacement

Breakdown of Components
D (Displacement): A constant offset (usually for starting at a specific field).

Rb (Base Register): The starting address (the start of the array).

Ri (Index Register): The element index (the "i" in array[i]).

S (Scale): Must be 1, 2, 4, or 8.

address = Reg[Rb] + (S * Reg[Ri]) + D

Why these numbers? These correspond to the standard sizes of primitive data types: char (1), short (2), int (4), and long/pointer (8).