# 1. Bit Width & Ranges

Everything depends on how many bits are used.

## Unsigned (n bits)

Range:
0 to (2^n − 1)

## Signed (Two’s Complement, n bits)

Range:
−2^(n−1) to (2^(n−1) − 1)

## 2's complement

Negative numbers are stored as two’s complement

To get -5 as bits, Write +5:

00000101

Flip bits:

11111010

Add 1:

11111011 = -5

## Example (8-bit)

| Type     | Min  | Max |
| -------- | ---- | --- |
| Unsigned | 0    | 255 |
| Signed   | -128 | 127 |

Signed has one extra negative number.

---

# 2. Overflow & Wraparound

Computers usually do not throw errors on integer overflow.

## Unsigned Overflow

Wraps around modulo 2^n.

Example (8-bit):
255 + 1 = 0

Example (4-bit):

- Max value = 1111 (15)
- 1111 + 0001 = 10000
- Since can only read 4 bits, result overflows = 0000 the '1' is lost

## Signed Overflow

In C/C++: undefined behavior (dangerous).
In hardware: still wraps, but language may not guarantee it.

Example (8-bit signed):
127 + 1 = -128

In a 4-bit signed system using two's complement, the leftmost bit serves as the sign indicator (0 for positive, 1 for negative).

- Range: -8 to +7
- Calculation: (4)+(5) or 0100+0101
- Binary Result: 1001
- To find the value of 1001, you invert the bits (0110) and add one (0111), which equals 7. Therefore, 1001 is -7.
- Interpretation: In signed 4-bit, represents -7. Since 4 + 5 is 9, and 9 is outside the available range, the value wraps around into the negative territory. This is identified as overflow because adding two positive numbers resulted in a negative bit pattern.

Why it "Wrapped Around"?

Think of signed numbers on a circle rather than a straight line.

The highest positive number you can have is 7 (0111). If you add 1 to it, the binary becomes 1000, which is -8.

In your calculation, 4 + 5 = 9. Since 9 is two steps past the limit of 7, it lands on -7.

Think 7 -> -8 -> -7

---

# 3. Type Casting: Signed ↔ Unsigned

Casting does NOT change bits, only interpretation.

## Signed → Unsigned

Example (8-bit):
-1 = 11111111 → unsigned = 255

```c
//when doing
int x = -1;
unsigned y = x;
//The computer does not flip bits and add one
//The computer keep bits exactly the same just read them as unsigned
// Signed view:    11111111 ... 1111  = -1
// Unsigned view:  11111111 ... 1111  = 4294967295
```

## Unsigned → Signed

If MSB = 1, number becomes negative.

Example:
200 = 11001000 → signed = -56

---

# 4. Bitwise Operations

Operate on bits directly.

| Operator | Meaning     |
| -------- | ----------- |
| &        | AND         |
| \|       | OR          |
| ^        | XOR         |
| ~        | NOT         |
| <<       | Left shift  |
| >>       | Right shift |

## Shifts

### Left Shift

x << k ≈ multiply by 2^k (if no overflow)

### Right Shift

- Unsigned → logical shift (0s added)
- Signed → arithmetic shift (sign bit copied)

Example (8-bit signed):
-4 = 11111100 >> 1 → 11111110 = -2

---

# 5. Sign Extension vs Zero Extension

When smaller types become larger:

## Unsigned → Larger Type

Pad with 0s (zero extension)

## Signed → Larger Type

Pad with sign bit (1) (sign extension)

Example:
8-bit -5 = 11111011  
16-bit = 11111111 11111011

Affects:

- Casting
- Comparisons
- Shifts

---

# 6. Signed vs Unsigned Comparisons

When comparing mixed types, signed may be converted to unsigned.

Example (C-like behavior):

int x = -1  
unsigned y = 1

Comparison:
x < y → unsigned(x) < y  
4294967295 < 1 → false

Common source of bugs.
