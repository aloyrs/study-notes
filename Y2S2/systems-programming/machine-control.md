# Condition Codes (Flags)

What they are: 1-bit status indicators in the EFLAGS register.

Purpose: Store results of the most recent arithmetic/logic operation to enable branching (if statements).

The Big Four:

ZF (Zero Flag): Set if result equals 0.

SF (Sign Flag): Set if result is negative.

CF (Carry Flag): Set if unsigned overflow occurred (carry out of highest bit).

OF (Overflow Flag): Set if signed overflow occurred (positive + positive = negative).

## Implicit vs Explicit flag setting

1. Implicit Setting (Side Effects)
   Most instructions update flags as a "byproduct" of their main job. You don't ask them to; they just do it.

   Happens in a rithmetic instructions: add, sub, imul, and, or, xor, shl.

2. Explicit Setting (Intentional)
   These instructions are used specifically to update flags without changing the values in your registers. They are the "logic setup" for jumps.

   Happens when using comparison instructions: cmp ,test

# Reading Condition Codes

## SetX Instructions

Set low-order byte of destination to 0 or 1 based on combinations of
condition codes

Example: setg

```c
int is_greater(long a, long b) {
    return a > b;
}
```

```bash
is_greater:
    cmpq    %rsi, %rdi    # Step 1: Explicitly compare a (%rdi) and b (%rsi)
    setg    %al           # Step 2: If a > b, set %al to 1; otherwise 0
    movzbl  %al, %eax     # Step 3: Zero-out the rest of %rax
    ret                   # Step 4: Return the 1 or 0
```

## jX Instructions

Jump to different part of code depending on condition codes

# Conditional branches

Since setX or cmov doesn't jump, the CPU must execute the instructions for both the "true" and "false" cases before picking the result. If those cases involve heavy math or slow memory access, you are wasting energy and time.

Jumps are "bad" when the condition is unpredictable (like random data), because a wrong guess forces the CPU to flush its pipeline and restart, wasting significant time.

# Loops

- **Do-While:** Execute the body, then use `cmp` and a conditional jump at the bottom to return to the start if the condition is met.

- **While:** Jump to a test at the bottom (Jump-to-Middle), then use a conditional jump to go back up to the body only if the condition is true.

- **For:** Execute the initialization, jump to the test at the bottom, and repeat a cycle of Body -> Update -> Test -> Conditional Jump.

# Example assembly code

```bash
# variable a in %rdi, p in %rsi

        testq   %rdi, %rdi
        je      .L1
        cmpq    %rdi, (%rsi)
        jge     .L1
        movq    %rdi, (%rsi)
.L1:
		movq    (%rsi), %rax
        ret
```

The Two-Step Process:

The "Check" (testq / cmpq): These instructions perform math (ANDing or Subtraction) to set bits in the EFLAGS register (like the Zero Flag or Sign Flag).

The "Action" (je / jge / jne): These instructions don't actually look at your variables; they only look at the EFLAGS register to decide whether to jump.
