# C++

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
    * **eg:** `char c = 'A';` (Typically 1 byte)
  * **string**: Allows us to store multiple characters.
    * **eg:** `std::string s = "Sudeepam";`
  * **int**: Allows us to store whole numbers b/w `[-2^31,  2^31 - 1]`.
    * **eg:** `int num = 10;` (Typically 4 bytes)
  * **float**: Allows us to store decimal numbers.
    * **eg:** `float num = 5.9;` (Typically 4 bytes)
  * **double**: Allows us to store decimal numbers, but more decimals.
    * **eg:** `double num = 6.1` (Typically 8 bytes)
  * **boolean**: Allows us to store True/False values.
    * **eg:** `bool isTrue = False;` (Typically 2 bytes)
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
# Pointers and References

## Pointers
* To create a pointer variable of integer type do `int *num` or `int* num`. Both are same, the later is more sensible.
* `node* get_parent(node *root)` is an example of how pointers can be passed to and returned from functions.
* `&var` gives us the address where the variable `var` is stored. 
* `*ptr` gives us the value to which the pointer variable `ptr` points.
* To acess a variable `var` of an object `obj` we can just say, `obj.var`, but if we have an object pointer say `ob_ptr` we must do
`ob_ptr->var` which essentially is equal to `(*ob_ptr).var`.
* If `ptr` is a pointer to an `int` then `ptr + 1` will increment this address by 4 bytes. If it is a pointer to `char` then the address is incremented by 1 byte.

## References
* A reference is basically another name for an already existing variable,

```cpp
int i = 17;
int& r = i; // `r` is our reference variable
```

## Differences b/w pointers and references
* You cannot have NULL references. You must always be able to assume that a reference is connected to a legitimate piece of storage.

* Once a reference is initialized to an object, it cannot be changed to refer to another object. Pointers can be pointed to another object at any time.

* A reference must be initialized when it is created. Pointers can be initialized at any time.

# Functions

* C++ functions are call by value, call by pointer, or call by reference.
* The program below shows a basic example of a function.
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
* If the function A (main), that calls the function B (function_name), is written before B, we need to declare B first. Do this using `int function_name(std::string);`

# Conditional Statements

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
* To create an integer array (say):
  * `int nums[] = {4, 8, 15, 16, 23};`
* The array above can store only the specified numbers. If we need to store,  say 20 numbers, we can declare the array as ...
  * `int arr[20];`
  * OR, with initialization, `int arr[20] = {};`
  * OR, specify first few (say 3) elements, `int nums[] = {4, 8, 15};`
* We can also create a 2D or rather, an N-D array like:
  * `int nums[][] = {{1, 2}, {3, 4}, {5, 6}};`
  * Initialization is similar to 1D arrays.

## Some important points

### Arrays and Pointers.
* When I declare an array, like `int arr[20]`. The variable `arr` actually stores the address of the first element of the array and `cout << arr` will actually print this address. `cout << *arr` will print the first element of the array. `cout << *(arr + 1)` will print the second element of the array.
* So for an array we can get address of ith element with `&arr[i]` or `arr+i` and value with `arr[i]` or `*(arr + i)`.
* Also, if we have `int arr[]` then a pointer to this would be created as `int *p = arr`. `p++` is valid whereas `arr++` is not, even though both are pointers. `arr + 1` however, is valid. Similary, something like `p = arr` is valid but `arr = p` is not.
* When I do something like `B[2][3]` then `B[0]` and `B[1]` are 1-D arrays of 3 integers each. `B` will be a pointer **to a 1D array of 3 integers**.
* A statement like `int *p = B` will throw an error because B is not a pointer to an integer, it is a pointer to a 1-D array. int `(*p)[3] = B` is fine.
* `cout<< B+1` will return the address of `B[1][0]`
* Output of `cout << *(B+1)` is insightful. When `B+1` is a pointer to a 1D array of 3 integers, so when we de-reference it, `B+1` will give us the whole 1D array, i.e. `B[1]`, which means we are printing the name of the 1D array `B[1]` which will give us the starting address of this 1D array. Hence `cout << *(B+1)` returns the address of `B[1][0]`.
* **Practice**: `cout << *(*B + 1)` will print the value at `B[0][1]`.

### Arrays and Functions.
* Arrays are never passed by value in a function. If I write a function definition as `void func_name(int arr[])`, The local variable `arr` is treated by the compiler, as a pointer to the original array which was passed during the call. Hence, arrays are always passed by reference.
* This makes sense because arrays can be quite big and it does not make sense to create new copies of them during function calls.

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

# Algorithms

* Sorting algos

## Sorting
* A stable sorting algorithm preserves the relative order of elements.
* In C++, you can sort a vector `V` with `sort(V.begin(), V.end());`
