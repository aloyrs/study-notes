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
