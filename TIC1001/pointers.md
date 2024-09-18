# Pass by value

```cpp
int a;
int b;
void addOne(int temp, int a ,int b){
    a += temp;
    b += temp;
}
addOne(10,a,b);
```

- Copies of the values of a and b are made and used inside the function (passed by value)

# Pass by reference

```cpp
#include <iostream>
using namespace std;

void modify(int &n) {
    n = 20;  // Directly modifies the original variable (which is like address of x)
}

int main() {
    int x = 10;
    modify(x);  // Passing x by reference
    cout << "x after modify: " << x << endl;  // Output will be 20
    return 0;
}

```

# Pointers

& = address-of operator

\* = dereference operator

```cpp
#include <iostream>
using namespace std;

int main() {
    int x = 10;
    cout << "address of x = " << &x << endl;
    // Create pointer y pointing to address of x
    int *y = &x;
    cout << "address of y = " << &y << endl;
    cout << "value of y = " << y << endl;
    x += 23;
    cout << "address of x after adding 23 = " << &x << endl;
    cout << "value of x after adding 23 = " << x << endl;
    // deference by using the * operator
    cout << "dereferenced value of y = " << *y << endl;

    return 0;
}

```

Output:

```bash
address of x = 0x98dc5ffadc
address of y = 0x98dc5ffad0
value of y = 0x98dc5ffadc
address of x after adding 23 = 0x98dc5ffadc
value of x after adding 23 = 33
dereferenced value of y = 33
```

## Pointer in functions

```cpp
void swap(int *a, int *b) {
    int temp;
    temp = *a;  // Store the value at address a in temp
    *a = *b;    // Put the value at address b into the address a
    *b = temp;  // Put the value stored in temp into the address b
}

int main() {
    int x = 10;
    int y = 20;

    printf("Before swapping: x = %d, y = %d\n", x, y);

    // Call the swap function with addresses of x and y
    swap(&x, &y);

    printf("After swapping: x = %d, y = %d\n", x, y);

    return 0;
}
```

```bash
Before swapping: x = 10, y = 20
After swapping: x = 20, y = 10
```
