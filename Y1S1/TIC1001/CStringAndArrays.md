TIC1001 lecture 6

For C progamming language

- arrays cannot be assigned , but values can be copied to another array
- each character represents an integer value mapped in ASCII table

  eg.'A' = 65

  'A' + 1 = 'B'

  'd' - 32 = 'D'

  'A' < 'Z'

- Strings are just arrays of character

```c
char c = 'd'
printf("%c",c)
char vowel[5] = {'a','e','i','o','u'};

char name[9] = "aloysius";
// C-String ends with a null character like : aloysius\0
// Ensure size of c-string is n+1 for null terminator
printf("%s",name);
```

# String functions in C

```c
#include <string.h>

// strlen
// strcmp
// strcpy
// strcat
```

# Arrays

```c
void test(int arr[]) {
    printf("%lu", sizeof(arr));
}

int main(void) {
    int x[10] = {0};
    printf("%lu ", sizeof(x));
    test(x);
}

// 40 8
```

The reason why the second output is 8 is because arrays are passed by reference. So arr is a pointer which is either 64 bits (8 bytes) or 32 bits (4 bytes) depending on your system memory size.
