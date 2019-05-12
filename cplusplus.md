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
* `signed`, `unsigned`, `long`, `short` are data type modifiers. Declaration is like `unsigned long int a = 5`.

Read: https://stackoverflow.com/questions/18971732/what-is-the-difference-between-long-long-long-long-int-and-long-long-i


# Bit-wise operations
* https://www.interviewbit.com/tutorial/tricks-with-bits/

## Logical Operators
### AND
```cpp
int a = 21;
int b = 6;
int c = a & b; // '&' Returns the bitwise AND of a and b
cout << c;     // 4
```

### OR
```cpp
int a = 21;
int b = 6;
int c = a | b; // '|' Returns the bitwise OR of a and b
cout << c;     // 23
```

### XOR
```cpp
int a = 21;
int b = 6;
int c = a & b; // '^' Returns the bitwise XOR of a and b
cout << c;     // 19
```

### NOT
```cpp
int a = 21;
int b = ~a; // '~' Returns the bitwise NOT of a and b
cout << b;  // -22
```
* Just like we write `a += b` for `a = a + b`, we can write `a |= b` for ` a = a | b`.
* bitwise operators work on integers whereas logical operators such as `&&` and `||` work on boolean.

## Shift Operators
* Shift Operators should not be used for negative numbers, as the result is undefined.
* Left Shift by `x` or right shift by `x` is equal to multiplication or division by pow(2, x) respectively.
* The digits that overflow the range of the data type (on left shift), or underflow the range of the data type (on right shift) are lost, and this results in undefined behavior.
### Left Shift Operator
```cpp
int a = 29;     // 0011101
int x = 2;
int b = a << x; // Shifts the bits of `a` towards left by `x` digits and stores the result in b.
cout << b;      // 116 = 1110100
```

### Right Shift Operator
```cpp
int a = 29;     // 0011101
int x = 2;
int b = a >> x; // Shifts the bits of `a` towards right by `x` digits and stores the result in b.
cout << b;      // 7 = 0000111
```

# Strings

## Basics
* `string` is an inbuilt class in C++ that allows us to work with strings. They are much more powerful than the C style strings (null terminated char arrays).
```cpp
string str; // str is now an object of the string class of C++.
str = "hello friend";

// C++ Strings are 0 indexed.
str[1] = 'e';
```
## Useful Functions
```cpp
// Returns the length of the string.
str.size(); 

// Returns true if the length of the string `str` is 0.
str.empty();

/* Starts looking from the 2nd index and returns the first index where the
substring "abc" is encountered. */
str.find("abc", 2);

// Check
str.rfing()

/* Returns a substring starting at position 3 and containing the next 5
characters (character at pos 3 included). */
str.substr(3, 5)

// Replaces characters at position 9, 10, 11, 12, & 13 with "Hello friend".
str.replace(9, 5, "Hello friend")

// Swaps the values of str1 and str2
str1.swap(str2)

/* Returns a pointer to a null-terminated character array (C style string) containing the current value of the `str` string object*/
str.c_str()
```
## Case conversion
* You cannot check for the case, or convert case of the entire string object directly. It has to be done character wise.

```cpp
/* Checks if the ith character of str is 
  - Uppercase.
  - Lowercase.
  - Alphanumeric.*/
isupper(str[i]);
islower(str[i]);
isalnum(str[i]);

/* Converts the ith character of str to
  - Uppercase
  - Lowecase */
toupper(str[i]);
tolower(str[i]);

/*returns 0 if str_1 is the same as str_2
  returns a value < 0 if str_1 is smaller than str_2
  returns a value > 0 if str_1 is larger than str_2 */
str_1.compare(str_2);

/* 
- Single line operations are done using the `transform()` function.`

- `transform()` applies an an operation uniformly to each element of a sequence.
  - The first two arguments specify the range in which operation has to be applied
  - The third argument defines the starting position from which the result would be stored.
  - The fourth argument is the operation that is to be applied.
  
This can therefore be used to add two arrays with a single line of code, or as shown below, to convert a string to upper or lower case*/

transform(str.begin(), str.end(), str.begin(), ::tolower)
transform(str.begin(), str.end(), str.begin(), ::toupper)
```

## Type Conversion
```cpp
// Parses the string to an integer.
stoi(str);

/* Note: `atoi(str)` is a similar function, but `atoi()` is basically a C function
   ----   and it parses C style strings (null terminated char arrays) to integers.
          `stoi()` is a C++ function and it parses the C++ string objects to an
          integer. Note that the `atoi` function will silently fail if the string
          not convertible to an int, while the `stoi()` will throw an exception. */

// Converts an integer type to string type.
to_string(10);
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
* In C and C++ we cannot have something like
  ```cpp
  n = 10; 
  int arr[n]; // Invalid
  ```
  Hence, we use vectors for dynamic arrays.

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
* Unlike Arrays, vectors can be passed by Values.

# Classes and Objects

* Class is the blueprint, object is the instance of the blueprint.
* Acess specifiers are helpful to make sure that instance variables do not get initialized with invalid values.
```cpp
class node {
  public: // Public members can be accessed outside the class with an object of the class
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

  private: // Private members can be accessed within the class only
    void some_function (int val){
      // Code
    }

  protected: // Can be accessed outside the class but only in a class derived (Inheritance) from this class.
    int some_var;
    int some_other_function (){
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
* Sieve of erathosthenes.
* Learn to Use terniary operators for conditions.
* Number system conversions, assuming positive numbers ...
  * Any number A<sub>3</sub>A<sub>2</sub>A<sub>1</sub>A<sub>0</sub> at base `b` conversion to decimal is done by....  
  `A0 * (b^0)` + `A1 * (b^1)` + `A2 * (b^2)` + `A3 * (b^3)` 
  * Dividing decimal number by base `b` and continously storing the remainder in down to up fashion gives us the number at base b.

## Sorting
* A stable sorting algorithm preserves the relative order of elements.
* In C++, you can sort a vector `V` with `sort(V.begin(), V.end());`


## Binary Search
* For `mid`, one way is `mid = (start + end)/2` but sometimes `start + end` can exceed the limit of int, hence a better option is:
 `mid = start + (end - start) / 2`
* Binary search can be implemented recursively also.
* The concept of Binary Search can be used for finding x so that f(x) = p, if x is a monotonic function.
* This https://www.youtube.com/watch?v=OE7wUUpJw6I variation of Binary Search is important and can be used to find the first or
  last index of an element in an array if it is present multiple times.

# Strings

* Write about C++ STL stack, queue, unordered_map, vector
