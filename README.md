# C++_cheat_sheat

* C++ was created by Bjrane Stroustrup.
* OOP Concepts
  * **Encapsulation**: Wrapping together, all the variables and functions related to an entity is encapsulation. Defining a class is a way of achieving it.
  * **Abstraction**: Means, know only the necessary parts. Creeating and using functions is a way of achieving this.
  * Polymorphism
  * Data Hiding
  * Inheritance


# Input and Output

* `cin` and `cout` (console in/out) are used for user input and printing respectively. They are predefined objects.
*  `>>` is called the `get_from` or `extraction` operator.
*  `<<` is called the `put_to` or `insertion` operator.
* Check `getline(cin, name)` for strings.

```cpp
#include <iostream>
int main() {
  int n;
  std::cout << "Enter a number: ";
  std::cin >> n;
  std::cout << "The number was: " << n;
  return 0;
}
```

# Variables and Data Types

* Variables are containers for data.
* These are the pre-defined data types of C++ ...
  * **char**: Allows us to store single characters b/w `[-128, 127]` or `[0, 255]`.
    * **eg:** `char c = 'A';`
  * **string**: Allows us to store multiple characters.
    * **eg:** `std::string s = "Sudeepam";`
  * **int**: Allows us to store whole numbers b/w `[-2^31,  2^31 - 1]`.
    * **eg:** `int num = 10;`
  * **float**: Allows us to store decimal numbers.
    * **eg:** `float num = 5.9;`
  * **double**: Allows us to store decimal numbers, but more decimals.
    * **eg:** `double num = 6.1`
  * **boolean**: Allows us to store True/False values.
    * **eg:** `bool isTrue = False;`
* Data types can be pre-defined (like `int`) or user defined (like a `class`).
* `signed`, `unsigned`, `long`, `short` are data type modifiers. 

# Working with Strings

* In C++, strings are 0 indexed.
```cpp
str = "hello";
str[1] = 'e';
```
* The following are some useful string functions.
```cpp
str.length(); // Length of a string.

str.find("abc", 2); // Starts looking from the 2nd index and returns the index where the substring "abc" is encountered.

str.substr(8, 3); // Starts at the 8th index and returns the next three chararacters.
```

# Working with Numbers

* The modulus operator is `%`
* C++ follows PEDMAS.
* `x++` first uses, then increments. `++x` first increments, then uses. We also have `x += 10` 
* Any arithmetic between a decimal number and an integer returns a decimal number.

Useful C++ math function
```cpp
#include <cmath>

pow(3, 4);  // Calculates 3^4
sqrt(7.5);  // Calculates the square root of 7.5
round(4.1); // Rounds of 4.1
fmax(3, 7); // Returns the bigger number, similarly fmin()
```

# Functions

* The program below shows a basic example
```cpp
int function_name(std::string name) {
  cout << "enter your age " << name;
  std::cin >> age;
  return age;
}
int main() {
  age = function_name("Sudeepam");
  std::cout << "Your age is: " << age;
}
```
* If the function A (main), that calls the function B (function_name), is written before B, we need to declare B first. Do this using `'int function_name(std::string);'`

# Conditional Statements

* Basics
```cpp
int main(){
  bool isMale;
  std::cin >> isMale;
  if (isMale){
    std::cout << "You are a male";
  }
  else if (!isMale){
    std::cout << "Your are not a male";
  }
  else {
    std::cout << "Invalid Choice";
  }
  return 0;
}
``` 
* `&&` is used for **AND**.
* `||` is used for **OR**.
* `==` is used for **equals**.
* `!=` is used for **not equals**.

# Switch statements

```cpp
  std::cout << "enter choice (A/B/1/2)";
  char choice
  std::cin >> choice;
  switch (choice){
    case A:
      std::cout << "Choice was 'A' ";
      break;

    case B:
      std::cout << "Choice was 'B' ";
      break;

    case 1:
      std::cout << "Choice was '1' ";
      break;

    case 2:
      std::cout << "Choice was '2' ";
      break;
    
    default:
      std::cout << "error: invalid choice. \n";
```

# While Loops

* Checks the condition and then executes the code.

```cpp
int index = 1; // No execution if index = 6 initially
while  (index <= 5){
  std::cout << index;
  index ++ ;
}
```

# Do while loops

* Executes the code and then checks the condition to see if execution must be done again.

```cpp
int index = 1; // One execution if index = 6 initially
do{
  std::cout << index;
  index ++;
} while index <= 5
```

# For loops

```cpp
for (int i = 0; i <= 5; i++){
  std::cout << i;
}
```
# Arrays

## Basics
* C++ arrays can hold multiple values of the same data type.

## 1D Arrays
* To create an integer array (say):
  * `int nums[] = {4, 8, 15, 16, 23};`
* The array above can store only the specified numbers. If we need to store, say 20 numbers, we can declare the array as ...
  * `int arr[20];`
  * OR, with initialization, `int arr[20] = {};`
  * OR, specify first few (say 3) elements, `int nums[] = {4, 8, 15};`

## 2D Arrays
* To create an integer array (say):
  * `int nums[][] = {{1, 2}, {3, 4}, {5, 6}};`
  * Similar initialization as in 1D arrays.


# Pointers and References

## Pointers
* To create a pointer variable of integer type do `int *ptr`.
* `node* get_parent(node *root)` is an example of how pointers can be passed to and returned from functions.
* `&var` gives us the address where the variable `var` is stored. 
* `*ptr` gives us the value to which the pointer variable `ptr` points.
* To acess a variable `var` of an object `obj` we can just say, `obj.var`, but if we have an object pointer say `ob_ptr` we must do
`ob_ptr->var` which essentially is equal to `(*ob_ptr).var`.

## Reference
*

## Differences b/w pointers and references
* 


# Classes and Objects

* Class is the blueprint, object is the instance of the blueprint.
```cpp
class node {
  public: // Acess specifier
    int data;
    node *next;
    
    // Constructor is a special function that is called when an object of the class is created.
    
    node (){ // Non parameterized constructor
      data = 0;
      next = NULL;
    }

    node(int ob_data, node *ob_next){ // Parameterized constructor
      data = ob_data;
      next = ob_next;
      // Constructors are mostly used to initialize member variables but can contain code for other tasks as well.
    }

  private:
    void some_function (int val){
      // Code
    }
};

node newnode;             // An Object, no constructor used
node *newnode_ptr;        // An Object Pointer
node newnode (0, NULL);   // Using constructor

// This is how we can acess the members of a class.
newnode.data = 4;
newnode.some_function(newnode.data);
```

* Check out acess specifiers and OOP using classes and objects.
* C++ structures are basically the same as C++ classes. The main differece is that, in a class all members are `private` by default, and in a structure all members are `public` by default.


# Inheritance


# To- do
* Getters and Setters
* Static Members
* Destructor
* Operator Overloading
* friend, this, new, and delete functions
* Method Overloading and Overriding
* Virtual funtion
* Abstract Classes
* File Handling
* Type Conversion
* Templates
* Initializers
* Exception Handling
* Namespace
* STL
