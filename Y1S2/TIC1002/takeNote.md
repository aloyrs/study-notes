# Things to take note

By Value

- Simple data types (`int`, `float`, `char`, etc.) and structures are passed by value.
- The function **cannot change** the actual parameter.

By Pointer (Address)

- Requires the caller to pass the **address** of variables using `&`.
- Requires **dereferencing** of parameters in the function.
- Arrays are passed **by address** (automatically decaying into pointers).

By Reference (Conceptual Explanation)

- No additional syntax required (in languages like C++, not in C).
- No additional memory storage.
- Faster execution and less memory usage.

---

- When you pass an array into a function, what actually gets passed is a pointer to the first element of the array
- Composite data structure = multidimensional arrays/vectors like two dimensional array

```c
int myMatrix[3][4]

void printMatrix( int M[][4], int rows, int cols );

// In general, only the size of the first dimension of a multidimensional array can be omitted: Size of all other dimensions are compulsory
```
