# ASCII

= American Standard Code for Information Interchange

- Maps bits to characters
- 7-bit representation
- eg. 'A' in ASCII table = 65(decimal) or 01000001

Was not good enough as only maximum of 128 unique characters (from 7 bits)

# Unicode

= universal character encoding

- eg. 'A' in unicode = U+0041 where 41 is hexadecimal value (value of 65 in decimal)

# UTF-8

= Unicode Transformation Format - 8 bits

- Most popular character encoding standard
- backwards compatible with ASCII (uses 1 byte)

- Characters are encoded using one to four bytes :
  - 1 byte for characters in the ASCII range (U+0000 to U+007F).
  - 2 bytes for characters from U+0080 to U+07FF.
  - 3 bytes for characters from U+0800 to U+FFFF.
  - 4 bytes for characters from U+10000 to U+10FFFF.
