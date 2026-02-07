# Types of float numbers representation

1. Normalized Numbers (The standard)
Most numbers you use in code (like 1.5, 100.0, or 15213.0 from your image) are represented as normalized.

2. Denormalized Numbers (The safety net)
Numbers are represented as denormalized only when they are incredibly small—so close to zero that they can no longer be normalized.
Less than the smallest normalized value.

3. Special Values
- exp = 111...1 represents infinity, eg. 1.0/0.0
- exp = 000...0 represents NaN, eg. sqrt(-1)

# Normalisation

Encode into a 32-bit IEEE 754 floating-point representation

## 1. Value Conversion

The process begins by converting the decimal number into binary and normalizing it:

* Decimal value: 15213.0
* Binary representation: 11101101101101
* Normalized binary: 1.1101101101101 x 2^13

## 2. Significand (M)

The significand represents the precision bits of the number:

* The normalized form is 1.fractional_part.
* M = 1.1101101101101
* The frac field stores only the bits after the binary point.
* Padding with zeros is used to fill the 23-bit field: 11011011011010000000000.

## 3. Exponent (E)

The exponent field uses a biased representation to handle both large and small numbers:

* The mathematical exponent (E) is 13.
* The bias for a 32-bit float is 127.
* The stored exponent (Exp) is calculated as E + Bias.
* Calculation: 13 + 127 = 140.
* Binary representation of 140: 10001100.

## 4. Final Result

The encoded 32-bit string is composed of three sections:

* Sign (s): 0 (indicates a positive number)
* Exponent (exp): 10001100
* Fraction (frac): 11011011011010000000000

The mathematical formula used for this encoding is v = (-1)^s * M * 2^E, where E = Exp - Bias.

Final:
01000110011011011011010000000000

---
