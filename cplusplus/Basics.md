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
* Given below, are the various built-in data types in C++. The sizes and range mentioned below are in accordance with GCC.
* Data types can be declared as `signed` or `unsigned`. These are data type modifiers. Declaration is like `unsigned int a = 5`.
* Signed types can have negative numbers or their equivalents, whereas unsigned types can have non negative numbers only.
* `long` and `long int` mean the same, similarly `long long` and `long long int` are the same. The difference between `long` and `long long` is that, as stated above, the C++ standard mandates minimum ranges for each, and `long long` must be at least as wide as `long`. The difference, therefore, is compiler dependent.
* `short short int` does not exist.




# Special Values
* `\0` is the null character.
* `NULL` is the null pointer.
* `true` is boolean truth value.
* `false` is boolean false value.




# Bit-wise Logical operations

Bitwise operators work on integers whereas logical operators such as `&&` and `||` work on boolean.

| Operator | Description | Example (a = 21, b = 6) |
|----------|-------------|-------------------------|
|   &      | Bitwise AND | a & b = 4               |
|   \|     | Bitwise OR  | a \| b = 23             |
|   ^      | Bitwise XOR | a ^ b = 19              |
|   ~      | Bitwise NOT |  ~a = -22               |


Just like we write `a += b` for `a = a + b`, we can write `a |= b` for ` a = a | b`.

<u>**To Remember**</u>
* `B ^ (A ^ B)` = `A`
* `A ^ 0` = `A`
* `A ^ A` = `A`

# Shift Operators
* Shift Operators should not be used for negative numbers, as the result is undefined.
* Left Shift by `x` or right shift by `x` is equal to multiplication or division by `pow(2, x)` respectively.
* The digits that overflow the range of the data type (on left shift), or underflow the range of the data type (on right shift) are lost, and this results in undefined behavior.

| Operator |     Example      |     Explaination        |
|----------|------------------|-------------------------|
|   <<     |   29 << 2 = 116  | 0011101 << 2 = 1110100  | 
|   >>     |   29 >> 2 =  7   | 0011101 >> 2 = 0000111  |
