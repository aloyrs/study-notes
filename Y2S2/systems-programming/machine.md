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