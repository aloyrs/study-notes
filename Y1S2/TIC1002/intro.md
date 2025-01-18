Intro to TIC1002

```cpp
// Create a struct
struct Fraction {
    int num;
    int den;
}

//Use struct
Fraction fractionOne;
Fraction fractionTwo = {1,4}

```

# Pass by value

```cpp
void inverse(Fraction frac) {
    frac = {frac.den, frac.num};
}
int main()
{
    Fraction one_third = {1, 3};
    inverse(one_third);
    printf("%d/%d\n", one_third.num, one_third.den);
}
```

# Pass by reference

```cpp
void inverse(Fraction & frac) {
    frac = {frac.den, frac.num};
}
int main()
{
    Fraction one_third = {1, 3};
    inverse(one_third);
    printf("%d/%d\n", one_third.num, one_third.den);
}
// Not very obvious from main when comparing to pass by value
```

# Pass by pointer

- more used than 'pass by reference'

```cpp
void inverse(Fraction *frac) {
    *frac = {frac->den, frac->num};
}
int main()
{
    Fraction one_third = {1, 3};
    inverse(&one_third);
    printf("%d/%d\n", one_third.num, one_third.den);
}
// More used as is easier to see in main , but more complicated

```

# ->

The -> operator provides a shortcut for accessing members (fields or methods) of a structure or class through a pointer

```cpp
frac->num
//is equivalent to
(*frac).num
```

## Why Use -> Instead of (\*ptr).member?

**(\*frac).num** , parentheses are necessary

**.** has higher precedence than **\***

Without parentheses, **\*frac.num** would be interpreted incorrectly.

So we use **frac->num** instead, where frac is a pointer
