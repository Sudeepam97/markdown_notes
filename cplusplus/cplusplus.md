# Everything C++ 
C++ is an Object Oriented programming language and it was created by Bjrane Stroustrup.





# Input and Output
* `cin` (console in) is used to get user input at runtime.
* `cout` (console out) is used to print a message on the console.
* Both `cin` and `cout` are pre-defined objects.
*  `>>` is called the `get_from` or `extraction` operator.
*  `<<` is called the `put_to` or `insertion` operator.
```cpp
// A basic program using the above concepts
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
* Data types can be pre-defined (like `int`) or user defined (like a `class` or a `struct`).
* Unlike say, JAVA, the C++ standard does not strictly define the size of its in-built data types. The sizes are compiler dependent. What C++ does define is a rule for each data type, as in "double should have a precision not less than float". The exact precision is compiler defined and not C++ defined. The mandated rules can be found here: http://www.cplusplus.com/doc/tutorial/variables/
* Given below, are the various built-in data types in C++, user defined data types will be discussed later. The sizes and range mentioned below are in accordance with GCC.

  * **char**: 1 byte. Allows us to store single characters with ASCII values b/w `[-128, 127]` (signed) or `[0, 255]` (unsigned).
    * **eg:** `char c = 'A';`
  * **short**: 2 bytes (16 bits). It allows us to store whole numbers b/w `[-2^15,  2^15 - 1]` (signed) `[0, 2^16 - 1]` (unsigned).
    * **eg:** `short num = 10;`
  * **int**: 4 bytes (32 bits). It allows us to store whole numbers b/w `[-2^31,  2^31 - 1]`(signed) `[0, 2^32 - 1]` (unsigned).
    * **eg:** `int num = 1000;`
  * **long**: C++ mandates this to be atleast as wide as `int`. Typically this is 8 bytes (64 bits), however GCC defines it to be 4 bytes/32 bits (which, mind you, is not wrong). Hence GCC `long` is the same as `int`.
    * **eg:** `long num = 1000;`
  * **long long**: 8 bytes (64 bits). In GCC, it allows us to store whole numbers b/w `[-2^63,  2^63 - 1]` in case of signed or `[0, 2^64 - 1]` (unsigned).
    * **eg:** `long long num = 1000000;`
  * **float**: Allows us to store decimal numbers, is 4 bytes in GCC with ability to store at-least 6 significant decimal digits.
    * **eg:** `float num = 5.9;`
  * **double**: Allows us to store decimal numbers, is 8 bytes in GCC with ability to store at-least 10 significant decimal digits. `long double` is the same as `double` in GCC.
    * **eg:** `double num = 6.1`
  * **boolean**: 1 byte in GCC. Allows us to store true/false values.
    * **eg:** `bool val = false;`

* `long` and `long int` mean the same, similarly `long long` and `long long int` are the same. The difference between `long` and `long long` is that, as stated above, the C++ standard mandates minimum ranges for each, and `long long` must be at least as wide as `long`. The difference, therefore, is compiler dependent.
* `short short int` does not exist.
* Data types can be declared as `signed` or `unsigned`. These are data type modifiers. Declaration is like `unsigned int a = 5`.
* Signed types can have negative numbers or their equivalents, whereas unsigned types can have non negative numbers only.





# Special Values
* `\0` is the null character.
* `NULL` is the null pointer.
* `true` is boolean truth value.
* `false` is boolean false value.





# Bit-wise Logical operations

## AND
```cpp
int a = 21;
int b = 6;
int c = a & b; // '&' Returns the bitwise AND of a and b
cout << c;     // 4
```

## OR
```cpp
int a = 21;
int b = 6;
int c = a | b; // '|' Returns the bitwise OR of a and b
cout << c;     // 23
```

## XOR
```cpp
int a = 21;
int b = 6;
int c = a & b; // '^' Returns the bitwise XOR of a and b
cout << c;     // 19
```

## NOT
```cpp
int a = 21;
int b = ~a; // '~' Returns the bitwise NOT of a and b
cout << b;  // -22
```
* Just like we write `a += b` for `a = a + b`, we can write `a |= b` for ` a = a | b`.
* bitwise operators work on integers whereas logical operators such as `&&` and `||` work on boolean.





# Shift Operators
* Shift Operators should not be used for negative numbers, as the result is undefined.
* Left Shift by `x` or right shift by `x` is equal to multiplication or division by pow(2, x) respectively.
* The digits that overflow the range of the data type (on left shift), or underflow the range of the data type (on right shift) are lost, and this results in undefined behavior.

## <u>Left Shift Operator</u>
```cpp
int a = 29;     // 0011101
int x = 2;
int b = a << x; // Shifts the bits of `a` towards left by `x` digits and stores the result in b.
cout << b;      // 116 = 1110100
```

## <u>Right Shift Operator</u>
```cpp
int a = 29;     // 0011101
int x = 2;
int b = a >> x; // Shifts the bits of `a` towards right by `x` digits and stores the result in b.
cout << b;      // 7 = 0000111
```
* **This relation is often useful**: (A XOR B) XOR B = A





# Strings

## <u>Basics</u>
`string` is an inbuilt class in C++ that allows us to work with strings (sequence of characters). C++ string objects are much more powerful than the C style strings (null terminated char arrays).
```cpp
string str; // str is an object of the string class of C++.
str = "hello friend";

// C++ Strings are 0 indexed.
str[1] = 'e';
```

## <u>Operations on string</u>
```cpp
// Both are synonomus and return the length of the string.
str.size();
str.length();

// Returns true if the length of the string `str` is 0.
str.empty();

/* Starts looking from the 2nd index and returns the first index where the
substring "abc" is encountered. Returns -1 if substring is not found. */
str.find("abc", 2);

/* Returns the last occourance of "abc" in the string. `pos` specifies the
last character in the string to be considered as the beginning of a match. */
str.rfind("abc", pos);

/* Returns a substring starting at position 3 and containing the next 5
characters (character at pos 3 included). */
str.substr(3, 5)

// Replaces characters at position 9, 10, 11, 12, & 13 with "Hello friend".
str.replace(9, 5, "Hello friend")

// Swaps the values of str1 and str2
str1.swap(str2)

/* Returns a pointer to a null-terminated character array (C style string)
containing the current value of the `str` string object*/
str.c_str()
```

## <u>Operations on characters of the string</u>
We cannot check for the case, or convert case of the entire string object directly. It has to be done character wise.

```cpp
/* Checks if the ith character of str is 
  - Uppercase.
  - Lowercase.
  - Alphanumeric.
  - Alphabet.
  - Numeric. */
isupper(str[i]);
islower(str[i]);
isalnum(str[i]);
isalpha(str[i]);
isdigit(str[i]);

/* Converts the ith character of str to
  - Uppercase
  - Lowecase */
toupper(str[i]);
tolower(str[i]);

/* returns 0 if str_1 is the same as str_2
    OR
   returns `length(str_1) - length(str_2)` if one is a substring of another.
    OR 
   if the difference is encountered at the ith position, returns (int) (str_1[i] - str_2[i]).
*/
str_1.compare(str_2);

// compare() can be used to compare substrings also, example...
str_1 = "green apple";
str_2 = "red apple";
str_1.compare(6, 5, "apple");     // == 0 (compare str_1, beginning 6 and next 5 (6 included) to apple)
str_1.compare(6, 5, str_2, 4, 5)  // == 0 (compare index 6,7,8,9,10 of str_1 to index 4,5,6,7,8 of str_2)

/* Note: `str_1 == str_2` can be used to compare strings as well. This returns a 
   ----   boolean whereas  str1.compare(str_2) returns a signed int. Also,
          compare() can be used to compare substrings of the two strings, whereas
          `==` can be used to compare whole strings only. */
 
/*
`transform()` applies an an operation uniformly to each element of a sequence.
  - The first two arguments specify the range in which operation has to be applied
  - The third argument defines the starting position from which the result would be stored.
  - The fourth argument is the operation that is to be applied.
  
This can therefore be used to add two arrays with a single line of code, or as shown below, 
to convert a string to upper or lower case in a single line of code */

transform(str.begin(), str.end(), str.begin(), ::tolower)
transform(str.begin(), str.end(), str.begin(), ::toupper)
```

## <u>Type Conversion</u>
```cpp
// Parses the string to an integer.
stoi(str);

/* Note: `atoi(str)` is a similar function, but `atoi()` is basically a C function
   ----   and it parses C style strings (null terminated char arrays) to integers.
          `stoi()` is a C++ function and it parses the C++ string objects to an
          integer. Note that the `atoi` function will silently fail if the string
          not convertible to an int, while the `stoi()` will throw an exception. */

// Parses a string to decimal.
stod(str);

// Converts an integer type to string type.
to_string(10);
```





# Working with Numbers
* The modulus operator is `%` and is defined for non negative integers only.
* C++ follows PEDMAS.
* `x++` first uses, then increments. `++x` first increments, then uses. We also have `x += 10` 
* Any arithmetic between a decimal number and an integer returns a decimal number.
* Below are some useful C++ math functions are
```cpp
pow(3, 4);  // Calculates 3^4. Returns a double
sqrt(7.5);  // Calculates the square root of 7.5. Returns a double
log(8);     // Returns the natural log of 8. log10(8) for base 8.
round(4.1); // Rounds of 4.1
max(3, 7);  // Returns the bigger number, similarly min()

**Note**: `pow` function when typecasted to an `int` should be typecasted as (int)(pow(x) + 0.5).
```

* [These](https://www.quora.com/What-are-all-the-properties-of-modulo-which-can-be-used-in-programming-competitions)
properties of modulo are very important.





# Pointers and References

## <u>Pointers</u>
* To create a pointer variable of integer type do `int *num` or `int* num`. Both are same, the later is more sensible.
* `node* get_parent(node *root)` is an example of how pointers can be passed to and returned from functions.
* `&var` gives us the address where the variable `var` is stored. 
* `*ptr` gives us the value to which the pointer variable `ptr` points.
* To acess a variable `var` of an object `obj` we can just say, `obj.var`, but if we have an object pointer say `ob_ptr` we must do
`ob_ptr->var` which essentially is equal to `(*ob_ptr).var`.
* If `ptr` is a pointer to an `int` then `ptr + 1` will increment this address by 4 bytes. If it is a pointer to `char` then the address is incremented by 1 byte.

## <u>References</u>
* A reference is basically another name for an already existing variable.
```cpp
int i = 17;
int& r = i; // `r` is our reference variable
```

## <u>Differences b/w pointers and references</u>
* You cannot have NULL references. You must always be able to assume that a reference is connected to a legitimate piece of storage.
* Once a reference is initialized to an object, it cannot be changed to refer to another object. Pointers can be pointed to another object at any time. Remove any confusions here in the example with `i` and `r` above, we can say `r = 14` and that is
fine, the value to which a reference points can change. But we cannot change `r` to point to a different variable say `j`.
We cannot say `r = j`. Whereas this is possible with pointers.
* A reference must be initialized when it is created. Pointers can be initialized at any time.





# Functions
* C++ functions are call by value, call by pointer, or call by reference.
* The program below shows a basic example of a function.

```cpp
int function_name(std::string name = "") { // default value for name is ""
  if (name == ""){
    cout << "name not specified\n";
    return -1;
  }
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
* Note that it is not necessery to catch the value that is returned by a function.
* If there is no catch, an inbuilt data type just stays in the memory, ignored. Whereas an object of a user defined data type is destroyed when the control leaves it's scope.





# Function Overloading
* Function overloading is a method of creating multiple functions with the same name by changing the function signature.
* It is a mehtod of achieving compile-time polymorphism (an OOP concept described later in detail).
* Function Overloading is **not** the same as Function Overriding. 
```cpp
float area(int r){ // area of circle
  float pi = 3.14;
  return pi*r*r;
}
int area(int l, int b){   // area of rectangle
  return l * b
}
```





# Conditional Statements
* `&&` is used for **AND**.
* `||` is used for **OR**.
* `==` is used for **equals**.
* `!=` is used for **not equals**.
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
* We also have a short hand notation for if using the ternary operator `?`
```cpp
int greater_element = (x > y) ? x : y
//  ^returned value   ^condition  (returns x if condition is true, else returns y)
```




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
while  (index <= 5) {
  std::cout << index;
  index++;
}
```





# Do while loops
* Executes the code and then checks the condition to see if execution must be done again.
```cpp
int index = 1; // One execution if index = 6 initially
do {
  std::cout << index;
  index++;
}
while index <= 5;
```





# For loops
```cpp
for (int i = 0; i <= 5; i++){
  std::cout << i;
}
```





# Arrays

## <u>Basics</u>
* C++ arrays can hold multiple values of the same data type.

* To create an integer array (say):
  * `int nums[] = {4, 8, 15, 16, 23};`

* The array above can store only the specified numbers. If we need to store, say 20 numbers, we can declare the array as ...
  ```cpp
  int arr[20];
  ```

* The above declaration results in array being filled with garbage values. A better practice is to initialize arrray as follows,
  ```cpp
  int arr[20] = {}; // initialize with default values of data types
  ```
  * OR, specify first few (say 3) elements,
  ```cpp
  int nums[20] = {4, 8, 15};
  ```

* We can also accept the size of an array at runtime, something that was not possible (I think) in C.
```cpp
int n;
cin >> n;
int arr[n];
for (int i = 0; i < n; i++){
    cin >> arr[i];
}
```

* We can also create a 2D or rather, an N-D array like:
  ```cpp
  // Initialization is similar to 1D arrays.
  int nums[][] = { {1, 2},
                   {3, 4},
                   {5, 6} } ;
  ```

* In C and C++ we cannot have something like
  ```cpp
  n = 10; 
  int arr[n]; // Invalid
  ```
  Hence, we use vectors for dynamic arrays.

## <u>Arrays and Pointers</u>
* When I declare an array, like `int arr[20]`. The variable `arr` actually stores the address of the first element of the array and `cout << arr` will actually print this address. `cout << *arr` will print the first element of the array. `cout << *(arr + 1)` will print the second element of the array.

* So for an array we can get address of ith element with `&arr[i]` or `arr+i` and value with `arr[i]` or `*(arr + i)`.

* Also, if we have `int arr[]` then a pointer to this would be created as `int *p = arr`.

* `p++` is valid whereas `arr++` is not, even though both are pointers. `arr + 1` however, is valid. Similary, something like `p = arr` is valid but `arr = p` is not.

* When I do something like `B[2][3]` then `B[0]` and `B[1]` are 1-D arrays of 3 integers each. `B` will be a pointer **to a 1D array of 3 integers**.

* A statement like `int *p = B` will throw an error because B is not a pointer to an integer, it is a pointer to a 1-D array. int `(*p)[3] = B` is fine.

* `cout<< B+1` will return the address of `B[1][0]`

* Output of `cout << *(B+1)` is insightful. When `B+1` is a pointer to a 1D array of 3 integers, so when we de-reference it, `B+1` will give us the whole 1D array, i.e. `B[1]`, which means we are printing the name of the 1D array `B[1]` which will give us the starting address of this 1D array. Hence `cout << *(B+1)` returns the address of `B[1][0]`.

* **Practice**: `cout << *(*B + 1)` will print the value at `B[0][1]`.

## </u>Arrays and Functions</u>
* Arrays are never passed by value in a function. If I write a function definition as `void func_name(int arr[])`, The local variable `arr` is treated by the compiler, as a pointer to the original array which was passed during the call. Hence, arrays are always passed by reference.

* This makes sense because arrays can be quite big and it does not make sense to create new copies of them during function calls.

* Unlike Arrays, vectors can be passed by Values. `vectors` in detail, under the STL section.





# Exception Handling

```cpp
// Basic custom error message printing
try {
    cout << stoi(S);
}
catch(...){
    cout << "Bad String"; // if S = 'AB' say...
}
```
```cpp
// Another way
try {
  if (n < 0)
      throw runtime_error("n should be non-negative");
}
catch(exception &e){
  cout << e.what() << "\n";
}
```




# Object Oriented Programming
* Similar to how a religion would dictate, to a human who follows it, a set of rules by which they could lead a good life. A **programming paradigm** dictates to a programmer, a set of rules by which they could write good code.
* There are various programming paradigms, such as **Procedure Oriented Programming**, **Functional Programming**, **Object oriented Programming**, etc. Programming langauges are designed to allow a programmer to write code in one or more of such paradigms.
* Object Oriented programming is the most famous paradigm, and revolves around modeling the elements of code after real world entities.
* In OOP, a `class` refers to a collection of attributes of a real world entity, and an `object` of the class refers to a particular instance of those attributes. Consider the example below...
  * A `car` is a real world entity.
  * Its `model`, `reg_number`, `color` etc, are various attributes by which it can be defined.
  * Now, note that the values of these attributes are unique for each car, but each car must have these attributes no matter what.
  * To store information on various cars in a program the generic way, you would create multiple variables like `model_1`, `color_1`, `model_2`, `color_2` etc.
  * If your programming language allows you to group various variables together as a user defined data-type then that would be really nice. Something like a C `struct` would allow you to group these variables to create a user defined type, and you could then create various variables of this type for each car.
  * The problem is only half solved though. Note that although all cars may `accelerate` and `apply_breaks` the same way, a `bus` would posess similar funtionality, but for a bus the internal way of acceleratig or applying brakes (and hence the function definitions), would be different.
  * You can create multiple functions like `accelerate_bus`, `accelerate_car`, `apply_breaks_car` etc to overcome this, but then again, the process gets confusing really quickly. 
  * What if, we could wrap all of the attributes **and the functions** associated with a `car` together, and do the same for a `bus` similar to a user defined data type but with the functionality of the real world entity wrapped within it as well, and create instances of this new 'blueprint'?
* The last statement, is exactly what is achieved by a `class`. A `class` is a blueprint that wraps together the attributes and functions associated with a `car`, and each instance of this blueprint is what is called an `object`.





# Concepts of OOP
The four most important concepts of OOP are..

## <u>Encapsulation</u>
Wrapping together all the variables and functions related to an entity is encapsulation. Defining a class is a way of achieving it.

## <u>Abstraction</u>
Means, knowing only the necessary parts and hiding the details that are not required.
* Creating and using functions is a way of achievig abstractions.
* Using classes is another way, because a class can decide which data member will be visible to the outside world and which would not by using something called access specifiers (described later).
* Another way to achieve abstraction in C++ is by using header files.

## <u>Polymorphism</u>
Poymorphism refers to having many forms. Two people may have the same name but different characteristics. Ways to achieve polymorphism are:
* Function Overloading (Compile time)
* Operator Overloading (Compile time)
* Function Overriding (Run time)

## <u>Inheritance</u>
The capability of a class to derive properties and characteristics from another class is called Inheritance. Inheritance is one of the most important features of Object Oriented Programming. How C++ allows inheritance will be described in detail later.

Few more (not so core) concepts are...
* **Dynamic Binding**: In dynamic binding, the code to be executed in response to function call is decided at runtime. C++ has `virtual functions` to support this.
* **Data Hiding**: Access Specifiers allow data hiding, to basically define a scope where certain data coulb be accessed.





# Classes and Objects
* Access Specifiers
  * Acess specifiers are helpful to make sure that instance variables do not get initialized with invalid values.
  * Public members can be accessed outside the class with an object of the class.
  * Private members can be accessed within the class only.
  * Protected members can be accessed outside the class but only in a class derived (Inheritance) from this class.

* Contructor
  * Constructor is a special function that is called when an object of the class is created.
  * Constructors are mostly used to initialize member variables but can contain code for other tasks as well.
  * Constructors do not have a return type.
  * If we do not define a constructor then compiler makes one for us.
  * Howerver if we have defined even one, compiler wont make any.

```cpp
class node {
  public:
    int data;
    node *next;

    node() {                              // Non parameterized constructor
      data = 0;
      next = NULL;
    }

    node(int ob_data, node *ob_next) {    // Parameterized constructor
      data = ob_data;
      next = ob_next;
    }

  private:
    void some_function (int val){
      // Code...
      // Code...
    }

  protected:
    int some_var;
    int some_other_function () {
      // Code...
      // Code...
    }
};

node newnode;             // Creating an Object, default constructor used
node *newnode_ptr;        // Creating an Object Pointer
node newnode (0, NULL);   // Using parameterized constructor

// This is how we can acess the members of a class.
newnode.data = 4;
newnode.some_function(newnode.data);
```
* C++ structures are basically the same as C++ classes. The main differece is that, in a class all members are `private` by default, and in a structure all members are `public` by default.





# new and delete functions
* The `new` and `delete` keywords are used for dynamic memory allocation in C++.
* Dynamic memory is allocated in `heap` memory whereas rest is in `stack`. Study this in detail later.
```cpp
// Syntax for new
struct demo {
  int a;
  int b;
  demo() {
    a = 0;
    b = 0;
  }
  demo(int x, int y){
    a = x;
    b = y;
  }
}

demo ptr* = new demo();         // Now memory is allocated for an instance of `demo` and a `ptr` is a pointer to it.
demo ptr* = new demo(10, 20)    // Dynamic memory allocation with initialization.

// It makes sense to use Dynamic Memory for structures but we can
// actually have dynamic memory for default data types as well.
int ptr* = new int(25);

// Here, we dynamically allocate continous memory for an array
// of ints of and returns pointer to the first element array.
int *ptr = new int[10]
```
* If enough memory is not available in the heap to allocate, the new request indicates failure by throwing an exception of type std::bad_alloc, this can be prevented if “nothrow” is used with the new operator, in which case it returns a NULL pointer.
* Dynamically allocated memory is not freed until explicitly freed by the programmer or untill the program terminates.
* Enters the `delete` keyword. This is used to free dynamically allocated memory.
```cpp
// Syntax
delete ptr;
```





# Destructor
* Destructor is a member function which destructs or deletes an object.
* A destructor function is called automatically when the object goes out of scope.
* Destructors have same name as the class preceded by a tilde (~).
* Destructors don’t take any argument and don’t return anything.
* There can only one destructor in a class with classname preceded by (~) no parameters and no return type.
* The default destructor created by a compiler works fine unless we have dynamically allocated memory or pointer in class.
* When a class contains a pointer to memory allocated in class, we should write a destructor to release memory before the class instance is destroyed. This must be done to avoid memory leak.
```cpp
// example of destructor
class demo { 
  int i;
  public: 
    demo() { 
      i = 0; 
    } 
    ~demo() {
      // Check what to write.
    } 
};
```





# friend class and friend function
* A Friend Class can access private and protected members of other class in which it is declared as friend.
```cpp
class Node { 
  private: 
    int key; 
    Node* next;
    friend class LinkedList;  // Now class `LinkedList` can access private members of Node 
};
```
* Like a friend class, a friend function can be given special access to private and protected members. A friend function can be:
  * A method of another class.
  * A global function.
```cpp
class Node { 
private: 
    int key; 
    Node* next; 
    friend int LinkedList::search(); // Only search() of linkedList can access internal members 
}; 
```
* Friends should be used for limited purposes, too many friends lessens the value of encapsulation.
* Friendship is not mutual. If class A is a friend of B, then B doesn’t become a friend of A automatically.
* Friendship is not inherited. If a base class has a friend, then it doesn’t become a friend of the derived class(es).
* The concept of friends is not there in Java.





# static keyword
* Static keyword can be used for variables and functions...

## <u>Static Variables</u>
```cpp
// synatx to declare a static variable.
static int count = 0;
```

### <u>Static variables in a Function</u>
* When a variable is declared as static, space for it gets allocated for the lifetime of the program.
* Even if the function is called multiple times, space for the static variable is allocated only once.
* Thus, the value of variable in the previous call gets carried through the next function call.

### <u>Static variables in a class</u>
* As the variables declared as static are initialized only once the static variables in a class are shared by the objects.
* Because of this reason static variables can not be initialized using constructors.

### <u>Static objects of a class</u>
* The life of an object is within the function in which it was declared.
* When the closing braces `}` are encountered a destructor is called by C++ to destroy the object. (Do note that destructor is not called for dynamically allocated memory, i.e. for class type pointers(which I wrongly call object pointers)).
* For a non static object, the execution is like...
  * object created.
  * destructor called.
  * execution of program ends.
* For a static object, similar to a static variable, execution is like..
  * object created.
  * execution of program ends.
  * destructor called.
```cpp
#include<iostream> 
using namespace std; 
  
class demo { 
  int i; 
  public: 
    demo() { 
      i = 0; 
      cout << "Inside Constructor\n"; 
    } 
    ~demo() {
      cout << "Inside Destructor\n"; 
    } 
}; 
  
int main() {
  int x = 0; 
  if (x == 0) { 
    demo obj; 
  } 
  cout << "End of main\n"; 
}
/* Output...
Inside Constructor
Inside Destructor
End of main

...declare obj as `static GfG obj` and see the new output */
```
## <u>Static Functions</u>
* Functions within a class and outside a class both can be static, but the two are entirely different.

### <u>Static member functions of a class</u>
* Static member functions of a class, do not depend on object of class.
* We are allowed to invoke a static member function using an object of the class but it is recommended to invoke the static member functions using the scope resolution operator for redability.
* Static member functions are allowed to access only the static data members or other static member functions, they can not access the non-static data members or member functions of the class.

```cpp
#include<iostream> 
using namespace std; 
  
class demo { 
  public:
    static void print_message() { 
      cout << "This is static biatch!"; 
    }
}; 

int main() { 
    demo::print_message(); 
} 
```

### <u>Static functions outside class</u>
* Static functions, are function which are available only in the module they are defined in.
* They are not exported and cannot be put in a header file and used in another C++ file.
* This way you can write different functions sharing the same name, and also the compiler may optimize your code more thoroughly by inlining the function, knowing that no other file is dependant on it.





# this pointer
* Note that each object of a class gets its own copy of data members (class variables) and share a single copy of member functions.
* The `this` pointer is is a constant pointer that holds the memory address of the current (calling) object.
* It is passed as a hidden argument to all nonstatic member function calls and is available as a local variable within the body of the nonstatic function.
* It is not available in static member functions as static member functions can be called without any object (with class name).

Given below, are the situations where `this` pointer is useful:

## <u>When local variable’s name is same as member’s name</u>
In such a case, we can use `this` pointer to refer to the member variables of the current object.
```cpp
// A member function that sets `x` of current object to the `x` passed in the argument
void set(int x) {
  this->x = x;
}
```

## <u>To return reference to the calling object</u>
* When a reference to the calling object is returned, the returned reference can be used to chain function calls on the object.
```cpp
// A poor example of chaining
demo add(int x){
  sum += x;     // `sum` is an instance variable of class `demo`
  return *this;
}

demo obj;
obj.add(10).add(20);    // Chaining
```





# Operator overloading
* C++ has the ability to provide operators with a special meaning for a given data type, this is known as operator overloading.
* The example below demonstrates operator overloading.
```cpp
#include<iostream> 
using namespace std; 
  
class complex { 
private:
  int real, imag; 
public: 
  complex (int r = 0, int c = 0) {
    real = r;
    imag = c;
  }

  // This function is automatically called when '+'
  // is used with between two `complex` objects.
  complex operator+ (complex const &ref_b) {
        complex result;
        result.real = real + ref_b.real;
        result.imag = imag + ref_b.imag;
        return result;
  } 
  void print_complex_num() { cout << real << " + i" << imag << endl; } 
}; 
  
int main() {
    complex a(10, 5), b(2, 4); 
    complex sum = a + b;        // call to `operator+`. `a` is the calling object, `b` is the argument passed.
    sum.print_complex_num();
} 
```
* Name of an operator function is always the keyword `operator` followed by symbol of operator like `+`, `*`, etc.
* The following operators cannot be overloaded...
```cpp
   .         // dot 
   ::        // scope resolution
   ?:        // if-else
   sizeof    // duh!
```





# Inheritance
The capability of a class to derive properties and characteristics from another class is called Inheritance.
* **Sub Class**: The class that inherits properties from another class is called Sub class or Derived Class.
* **Super Class**: The class whose properties are inherited by sub class is called Base Class or Super class.

## <u>When to use inheritance</u>
* Consider a group of vehicles. Say, we need to create classes for three type of vehicles: Bus, Car, and Truck.
* The methods fuel_amount(), capacity(), apply_brakes() would be same for all the three classes.
* Hence, we would end up writing the same code thrice.
* A better method would be to create a class called `vehicles` that contains these functions, and inherit from it.
* **Note**: Vehicle(Super Class) ---> Bus(Sub Class) ---> school_bus(Possible sub class) ---> Tata_Bus/Honda_Bus(objects).
```cpp
/* Syntax
---------

class sub_class_name : access_mode base_class_name{
  // Code..
}

*/

class parent {
  // Some Code..
};
class child : public parent {
  // Code...
};

```
* A derived class doesn’t inherit **access to** private data members. However, it does inherit a full parent object, which contains any private members which that class declares.
* **Public mode**: If we inherit the base class in the public mode, the public member of the base class will become public in the derived class and protected members of the base class will become protected in derived class.
* **Protected mode**: If we inherit the base class in a protected mode, both public members, and protected members of the base class will become protected in derived class.
* **Private mode**: If we derive a sub class from a Private base class. Then both public member and protected members of the base class will become Private in derived class. All members will become hidden.

## <u>Types of Inheritance in C++</u>
* Because a constructor initializes an instance of a class, they are never inherited.
* However, the subclass must call a superclass constructor as it is an extension of a superclass object.
* Creating an object of a subclass will implicitly invoke the default constructor of superclasses. User defined constructors must be called explicitly.
* In case of default constructors, on creating an object of subclass a constructor of the subclass is invoked, the constructor before its own execution, invokes the default constructors of inherited classes in the order in which they were inherited, and then executes itself.
* Parameterised constructors are called as follows:
```cpp
class superclass {
  superclass(int x, int y){
    // code...
  }
};

class subclass : public superclass {
  subclass(int x_val, y_val) : superclass(x_val, y_val){   // calling superclass constructor in definition of subclass constructor
    // code...
  }
};
```
**NOTE:** The destructors are called in reverse order of constructors.


### <u>Single Inheritance</u>
In single inheritance, a class is allowed to inherit from only one class. i.e. one sub class is inherited by one base class only.
```cpp
class Car : public Vehicle {
}; 
```

### <u>Multiple Inheritance</u>
Multiple Inheritance is a feature of C++ where a class can inherit from more than one classes.
```cpp
class child : public father, public mother {
  // Code..
};
```

### <u>Multilevel Inheritance</u>
In this type of inheritance, a derived class is created from another derived class.
```cpp
class A{
};
class B : A {
};
class C : B{
}
```

### <u>Hierarchical Inheritance</u>
In this type of inheritance, more than one sub class is inherited from a single base class.
```cpp
class vehicle{
};
class car : vehicle {
};
class bus : vehicle{
}
```

### <u>Hybrid Inheritance</u>
Hybrid Inheritance is implemented by combining more than one type of inheritance. This basically means we are using multiple types of inheritance in our code.





# Virtual functions and function overriding
* Function overriding occurs when a derived class has a different definition for one of the member functions of the base class. The base class function is said to be overridden by the definition of derived class.
* The function that is defined in the base class but overridden in the derived class is a `virtual function`.




# multiple inheritance and virtual functions





# Abstract Class
* A class is called `abstract` if it has at least one pure virtual function.
* A pure virtual function (or abstract function) in C++ is a virtual function for which we do not have an implementation in the base class. We only declare it in the base class, and the implementation is done in classes which are derived from the Abstract class.
* Note that normal virtual functions have a definition in base class and are overriden in the child class, whereas pure VFs get their first definition in the child class itself.
* Pure virtual function is useful when we know that a function should belong to a class, but we cannot actually define it in that class since definition is dependent on a special case of the class. For example, let `Shape` be a base class. We cannot provide implementation of function `draw()` in `Shape` since it is dependent on what the shape is, but we know that every derived class must have a `draw()` function.
* A pure virtual function is declared by assigning `0` in declaration. For example...

```cpp
class Shape {
  public: 
    virtual void draw() = 0; // virtual function
};
class child : public shape {
  public:
    void draw(){
      cout << "Code to draw the shape here";
    }
}

```
* If we do not override the pure virtual function in derived class, then derived class also becomes abstract class.
* We cannot have objects of virtual classes. However, we can have object pointers for virtual classes.


# Method Overriding
* It is the re-definition of base class function in its derived class with same signature i.e return type and parameters.
* Overriding can be done in the derived class only whereas overloading can be done in both, the base and derived class.
```cpp
class parent {
  public:
    virtual void display() {
      cout << "hello";
    }
};

class child : public parent {
  public:
    void display() {
      cout << "hi there!";
    }
};
```





# Copy constructor





# STL Containers

## STL iterator
* Before diving into the data structures provided by STL. Let us take a moment to understand what an `iterator` is.
* An iterator is an object (like a pointer) that points to an element inside the STL container.
* We can use iterators to move through the contents of the container.
* Depending upon the functionality of iterators they can be classified into five categories...
  * Input Iterators
  * Ouput Iterators
  * Forward Iterators
  * Bidirectional Iterators
  * Random-Access Iterators
* Different containers support different types of iterators. The most important points for us to know are...
  * Forward iterators can be compared with another iterator, two iterators will be equal only when they point to the same position. Note that equality operators are allowed but relational operators (like `<=`) are not.
  * Forward iterators can be incremented one step at a time only `itr++ / ++itr` and cannot be decremented. Note that `itr + 1` is not the same as `itr++` and is invalid.
  * Bidirectional iterators are same as forward iterators, except they can be decremented as well, so `itr-- / --itr` is also valid in case of bidirectional iterators. Again, `itr - 1` is invalid and you can only move one step at a time.
  * Random-access iterators can be used to access elements at an arbitrary offset position relative to the element they point to, making them the most complete type of iterators offering the same functionality as that of pointers.
  * Thus with random access iterators operations like `itr + 5` or `itr - 5` are valid. Also, relational operations are also allowed by random access iterators.

* `vectors`, and `dequeue` support Random-access iterators.
* `unordered_map`, `unordered_sets`, `unordered_multiset`, and `unordered_multimap` support forward iterators.
* `map`, `set`, `multiset`, and `multimap` support bi-directional iterators.


## tuple (`#include <tuple>`)
* An object of the tuple class can hold a collection of multiple elements where each can be of different type.
```cpp
// Creating a Tuple
tuple <string, char, float> student;
string name = "Sudeepam";
char gender = 'M';
float gpa = 7.0;
student = make_tuple(name, gender, gpa);

// Acessing the elements of the Tuple
string s_name = "";
char s_gender = '\0';
float s_gpa = 0.0;
tie(s_name, s_gender, s_gpa) = student;
```


## pair (`#include <pair>`)
* This class couples together a pair of values, values may be of different types. This is a special case of tuple.
```cpp
// Creating a Pair.
pair<string, float> foo;
foo = make_pair("Sudeepam", 7.0);
// Acessing the elements of the pair
cout << "name: " << foo.first << "\n";
cout << "gpa: " << foo.second << "\n;
```


## vectors (`#include <vector>`)
* Vectors are dynamic arrays.
```cpp
// Declaring an empty vector.
vector<int> v;

// Declaring an empty vector of some size. Elements
// are initialized by default values of data types.
vector<int> v(10);

// Initializing a vector with some value (say 3).
vector<int> v(10, 3);

// WE DO NOT initialize a few elements like this.
vector<int> v(10) = {1, 2, 3};
```

* Important funtions related to vectors
```cpp
// Returns an iterator to the start of vector
v.begin();

// Returns an iterator to the end of vector
v.end();

// Returns true if the vector is empty
v.empty();

// Returns the number of elements in the vector
v.size();

// Returns the capacity of the vector
v.capacity();

// Difference between capacity and size arize because vector
// capacity is doubled when if it needs to fit more elements.
vector<int> myvector;
for (int i = 0; i < 5; i++)
  myvector.push_back(i);
cout << "size = " << myvector.size() << '\n';           // size = 5 
cout << "capacity = " << myvector.capacity() << '\n';   // capacity = 8
```

* Elements of a vector are 0 indexed and can be accessed via `[]` or `.at()` function.
* `[]` silently fails if an element is not found whereas `.at()` throws an error. 

```cpp
// examples of element access
a = v[1];
b = v.at(0);

// push an element at the rear
v.push_back(elem);

// pop an element from rear
v.pop_back();
```


## dequeue (`#include <deque>`)



## stack (`#include <stack>`)
```cpp
// declares an empty stack.
stack<int> A;

// Pushes a new element to the stack, O(1) time.
A.push(newElement);

// Pops an element off the stack, O(1) time.
// pop() removes the top element, does not return its value.
A.pop();

// top() is used to get the top element (not pop). O(1) operation.
A.top();

// Returns true if Stack is empty and false otherwise. O(1).
A.empty();

// Returns the size of the Stack. O(1)
A.size();
```


## queue (`#include <queue>`)
```cpp
// declares an empty queue.
queue<int> A;

// Pushes a new element to the queue, O(1) time.
A.push(newElement);

// Pops an element off the queue, O(1) time.
// pop() removes the front element, does not return its value.
A.pop();

// Front is used to get the top element (not pop). O(1) operation.
A.front();

// Returns true if Queue is empty and false otherwise. O(1).
A.empty();

// Returns the size of the Queue. O(1)
A.size();
```


## unordered_map and unordered_multimap (`#include <unordered_map>`)
* These are dictionary like data structures implemented via Hash tables. These can be used for O(1) search/retrievals.
* Elements are not sorted in any order.
* Keys in an `unordered_map` are unique, whereas keys of `unordered_multimap` need not be unique.
* Each element is an object of the `pair` class. Each iterator is therefore a pointer to a `pair` object.

The code snippets below use `unordered_map` but everything is same for `unordered_multimap` unless stated otherwise...
```cpp
// declares an empty map. O(1)
unordered_map<int, int> gpa;

// Traversing the unordered_map.
unordered_map<int, int>::iterator itr;    // This is an iterator(forward) to the unordered_map
/* Note: itr->first;  OR (*itr).first;    // The key.
         itr->second; OR (*itr).second;   // The value. */
for (itr = A.begin(); itr != A.end(); itr++){
  cout << itr->first << "\t" << itr->second;
}
```

Methods for inserting Key-Value Pairs ...
```cpp
/* We have an overloaded insert() function which provides various methods
to insert elements, into the unordered_map */.

/* 1: With this, we can insert multiple elements in map. This version of insert()
      returns void, and since an unordered_map can have unique keys only, with this 
      method, there is no way to know which elements were added and which are not */
gpa.insert({ {"Sudeepam", 7.0}, {"Charu", 7.2}, {"abcd", 6.9} } );

gpa["Sudeepam"] = 7.0; // Same behavior
```

```cpp
/* 2: This next version inserts a `std::pair` of key and value into the hashmap. It
      returns a `std::pair` of `iterator` and `boolean`. If the element is sucessfully
      inserted, the boolean is `true` and the iterator points to the newly inserted
      element. Else, the boolean is `false` and the iterator points to `NULL`. */
unordered_map<int, int>::iterator itr;
pair<itr, bool> result;
result = A.insert(make_pair<int, int>(key, value));

// OR
pair<int, int> my_pair(key, value);
A.insert(my_pair); // Note that it is not necessary to store the returned pair.

// OR
result = A.insert({key, value});
```

Other functions ...
```cpp
// Return the number of entries having key as `k`
A.count(k);
/* This function can also be used to check if a certain key does
not exsits (count > 0) or does not exsit (count = 0) in the map */

// Returns the number of elements in the container. O(1).
A.size()

// True if the container size is 0, false otherwise. O(1).
A.empty();













//------- YAHAN SE EDIT ------------


/* Can be used to acess the value corosponding to key `k`. If the 
key `k` does not exist, an out of bounds exception is thrown */
A.at(k);

/* Returns an iterator to the element, if the specified key-value is found,
   or unordered_map::end if the specified key is not found in the container.
   O(1) average case. Rare worst case O(n). */
unordered_map<int, int>::iterator itr = A.find(K);
if (itr) == A.end())  //means that K does not exist in A.
  return null;
else
  cout << itr->first << "\t" << itr->second; 
```

* Erasing elements from a map ...
```cpp
unordered_map<string, string>::iterator itr;
/* 1: Return an iterator pointing to the position immediately following the last of the elements erased.*/
itr = mymap.erase(mymap.begin());  // erasing by iterator
/* 2: Returns an iterator pointing to the position immediately following the last of the elements erased.*/
itr = mymap.erase(mymap.find("China"), mymap.end()); // erasing by range
/* 3: Returns the number of elements erased. Since an unordered_map has unique keys, if an element did exist
      and is now erased, the returned value is 1, and if the element did not exist, the value is 0.*/
int num = mymap.erase("France"); // erasing by key
```



## unordered_set and unordered_multiset (`#include <unordered_set>`)
* Almost same, a certain type of insertion does not work..



* Do not forget to write about internal implementation of set, map, multimap, , unorderd_maps etc.
## map and multimap
## Using maps when unhashable stuff has to be hashed
## Set and multiset




## priority_queue (`#include <queue>`)
* Priority queues are **essentially the same as queues** except that the ordering of the queue formed is done, based on some priority of elements and not on the order in which they were inserted into the queue.
* Note the fact that **they are essentially the same as queues**. Thus, you can access and remove the top element of the queue only. The only difference is the push operation.
* Note that unlike `sets` and `multisets`, that we would discuss next, there is no concept of `iterating over` a priority queue. Note again, they are the same as `queues`, and the only difference is the way in which queue elements are ordered.

* Priority Queues are implemented via heaps. (imagine them as specifically ordered queues though).
* A max heap is constructed by default, but a min heap can also be created.
* Duplicates can exist within a priority queue.

```cpp
// Declare a priority queue. O(1).
priority_queue<int> pq;

// Returns true if priority queue is empty, else false. O(1).
pq.empty();

// Returns the size of the priority queue. O(1).
pq.size();

// Returns the value of the highest priority element of a priority queue. O(1).
pq.top();

// Inserts an element into priority queue. O(log n).
pq.push(5);
// O(log n) push suggests that the time complexity of building
// a priority queue from an unsorted array is O(nlog n)
// However, this time complexity is O(n). See below...
// https://www.geeksforgeeks.org/time-complexity-of-building-a-heap/


// pops the highest priority element from the queue. O(log n).
pq.pop();

// priority queue of pair of elements. Elements are ordered by first value of pair.
priority_queue<pair<int, int> > pq;

// Syntax to create a min heap priority queue is as follows:
priority_queue<Type, vector<Type>, ComparisonType > min_heap_pq;

// example: Min heap priority queue of integers
priority_queue <int, vector<int>, greater<int> > pq;

// example: Min heap priority queue of pairs
typedef pair<int, int> pair_type;
priority_queue <pair_type, vector<pair_type>, greater<pair_type> > pq;
```

* Priority queue of a user defined type can also be made but we must define a priority ourselves using operator overloading.
* Simply writing `priority_queue<class_name> pq;` would through an error since default priorities are not defined for class type.
```cpp
#include <iostream>
#include <queue>
using namespace std;

// priority queue for class type  
class Person {
  public:
    int age;
    float height;
    Person (int x, float y){
      age = x;
      height = y;
    }
}; 


// In std::sort custom comparision, if `true` is returned, the first argument
// is gets placed *before* the second argument, because a std::sort is
// ascending by default.

// A std::priority_queue is a max heap or descending by default. Therefore, a
// `true` value returned by a custom comparator would place the first argument
// *after* the second argument.

// With this in mind, lets tak a look at the custom priority function below.

// This returns true when height(p1) > height(p2). Thus the element with greater
// height is placed after the one with smaller height. This results is a height
// ordered `min heap`, i.e. smallest height would be on top of priority queue.
struct comp{
  bool operator()(const Person &p1, const Person &p2){
    return p1.height > p2.height;
  }
};

int main(){
  priority_queue<Person, vector<Person>, comp> pq;
  
  Person p1(30, 5.7);
  Person p2(25, 6.0);
  Person p3(20, 5.6);
  pq.push(p1);
  pq.push(p2);
  pq.push(p3);
  cout << pq.top().height << "\n";  // 5.6
  pq.pop();
  cout << pq.top().height << "\n";  // 5.7
  pq.pop();
  cout << pq.top().height << "\n";  // 6.0
  pq.pop();
  if (pq.empty())
    cout << "empty now\n";

  return 0;
}
```


## Difference between priority queue and set
(https://stackoverflow.com/questions/10141841/difference-between-stdset-and-stdpriority-queue)








# To-do
* File Handling
* Exception Handling
* Namespace



## <u>useful functions</u> (check complexity and usage)
* __gcd()
* upper_bound()
* lower_bound()
* distance()
* sort(A.begin(), A.end());
* *max_element(A.begin(), A.end()); (similarly min_element())
* binary_search();





# To do
* Virtual functions
* multiple inheritance and virtual functions
* Abstract Class
* Copy constructor
--------
