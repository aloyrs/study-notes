# Structs vs Classes

Structs members are public by default, used for simple data structures that don’t need encapsulation or complex behavior.

Classes when you need more control over data (e.g., private members), encapsulation, or object-oriented features like inheritance and polymorphism.

# Struct

```cpp
#include <iostream>
using namespace std;

// Define a struct for Point
struct Point {
    int x;   // Public member
    int y;   // Public member

    // Constructor for convenience
    Point(int xVal, int yVal) : x(xVal), y(yVal) {}

    // Method to display the point
    void display() {
        cout << "Point(" << x << ", " << y << ")" << endl;
    }
};

```

# Class

```cpp
using namespace std;
#include <vector>
#include <string>

class Person
{
private:
  string name;
  int age;
  Person *mother;

public:
  // if not constructor is created , cpp will provide a default constructor
  Person(string name, int age)
  {
    this->name = name;
    this->age = age;
  }
  // can have more than one constructor
  Person(string name, int age, Person &mother)
  {
    this->name = name;
    this->age = age;
    this->mother = &mother; //pass into pointer the address of reference 'mother'
  }

  string get_name()
  {
    return name;
  }
  int get_age()
  {
    return age;
  }
  // return type of pointer, as class returns a pointer of mother
  Person *get_mother()
  {
    return mother;
  }
};

int main()
{
  Person mary("MARY", 40);
  Person ben("BEN", 10, mary);

  cout << ben.get_mother()->get_name();
  // ben.get_mother() returns a pointer
  // To get mary's name, we need to use ->get_name() , the pointer -> to access the pointers attribute
  return 0;
}

// MARY

```

## Destructor

If your class allocates memory (for example, using new), you should have a destructor that frees the allocated memory (using delete).

In C++, when you use new and delete, the memory is managed on the heap.

We make sure to free memory to prevent 'memory leak'

```cpp
#include <iostream>
using namespace std;

class MyClass
{
private:
  int *data; // Pointer to dynamically allocated memory

public:
  // Constructor
  MyClass(int value)
  {
    data = new int; // Dynamically allocate memory
    *data = value;
    cout << "Constructor called: data = " << *data << endl;
  }

  // Destructor
  ~MyClass()
  {
    delete data; // Free the dynamically allocated memory
    cout << "Destructor called: memory freed" << endl;
  }

  // Function to display the data
  void display()
  {
    cout << "Data: " << *data << endl;
  }
};

int main()
{
  MyClass obj(42); // Constructor is called, memory is allocated
  obj.display();   // Display the value of data
  // Destructor is automatically called when obj goes out of scope, freeing memory
  return 0;
}

/*
Constructor called: data = 42
Data: 42
Destructor called: memory freed
*/

```
