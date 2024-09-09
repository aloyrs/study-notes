USING C

# Type conversion

## Implicit type conversion

- 55 + 1.75
- int money = 23.16;

## Explicit type conversion

- (int) 3.14

# Global vars

Scope is until end of program

# Preprocessor directives

- Start with # , like #include , #define
- Not recommended as is a simple text replacement mechanism

```cpp
#define M = 1 + 2;
```

# using namespace std;

```cpp
using namespace std;
```

- Tells the compiler to use the standard namespace (std) for identifiers, which simplifies the code by allowing you to omit the std:: prefix

# Function prototype

- function with no body

````cpp
int sum(int,int);
# Pass by reference

**_&_** means "address of"

```cpp
#include <iostream>

void modify(int &n) {
    n = 20;  // Directly modifies the original variable (which is like address of x)
}

int main() {
    int x = 10;
    modify(x);  // Passing x by reference
    std::cout << "x after modify: " << x << std::endl;  // Output will be 20
    return 0;
}

````

# Pointers

```cpp
#include <iostream>
using namespace std;

int main() {
    int x = 10;
    cout << "address of x = " << &x << endl;
    int *y = &x;
    cout << "address of y " << &y << endl;
    cout << "value of y = " << y << endl;
    x += 23;
    cout << "address of x after adding 23 = " << &x << endl;
    cout << "value of x after adding 23 = " << x << endl;

    return 0;
}

```

Output:

```bash
address of x = 0x98dc5ffadc
address of y 0x98dc5ffad0
value of y = 0x98dc5ffadc
address of x after adding 23 = 0x98dc5ffadc
value of x after adding 23 = 33
```
