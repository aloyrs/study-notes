# Recursion

Recursive function has :

- base case
- recursive call

## Space & Time

- Space = How much memory is taken
- Time = how long algorithm takes to run

## Recursion phases

A recursion always goes through two phases:

### 1. Wind-up Phase

- This occurs when the **base case is not satisfied**, so the function **calls itself recursively**.
- This phase continues until the **base case is reached**.

### 2. Unwind Phase

- The **recursively called functions return their values** to the previous "instances" of the function call.
- In other words:
  - The **last function call** returns to its parent (the **second-last** function call).
  - The **second-last** returns to the **third-last**, and so on.
- Eventually, the process reaches the **very first function call**, which computes the **final result**.

```cpp
int fibonacci(int n) {
    if (n <= 1) {
        return n;
    }
    return fibonacci(n-1) + fibonacci(n-2);
}
```
