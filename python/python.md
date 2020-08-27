# Some Basics
* `45.0` - An example of a floating point number.
* Python uses PEMDAS (Parentheses Exponents Multiplication Division Addition Subtraction) to evaluate expressions.
* `\` is to escape next character and so `\\` can be used to get a backslash. `eg: print ("\\")`
* Boolean values are `True` and `False`.

# Operators

| Operator     | Name           | Description                                            |
|--------------|----------------|--------------------------------------------------------|
| ``a + b``    | Addition       | Sum of ``a`` and ``b``                                 |
| ``a - b``    | Subtraction    | Difference of ``a`` and ``b``                          |
| ``a * b``    | Multiplication | Product of ``a`` and ``b``                             |
| ``a / b``    | True division  | Quotient of ``a`` and ``b``                            |
| ``a // b``   | Floor division | Quotient of ``a`` and ``b``, removing fractional parts |
| ``a % b``    | Modulus        | Integer remainder after division of ``a`` by ``b``     |
| ``a ** b``   | Exponentiation | ``a`` raised to the power of ``b``                     |
| ``-a``       | Negation       | The negative of ``a``                                  |


# Printing
```python
print () # Print statement in python3
```
**Note:** We can specify the line endings in the print function.

```python
# example 1: prints 'cheese burger'
print ("cheese", end = " ")
print ("burger")

# example 2: prints 'cheese  burger'
print ("cheese", end = "\t")
print ("burger")

# example 3: prints 'cheese
#                    burger'
print ("cheese", end = "\n")
print ("burger")
```


# Various ways of beautiful printing
```python
my_name = "Sudeepam"
statement = "My name is {}"

# Method 1
print ("My name is " + my_name)

# Method 2
print (f"My name is {my_name}")

# Method 3
print (statement.format (my_name)) # Argument of format goes within the {}
```


# Strings
```python
"""Triple quotes are used to write
multiline strings in python"""

mystr = "Sudeepam Pandey."             # An object of the string class.
print (mystr.lower ())                 # Convert to lower case (similarly mystr.upper()).
print (mystr.isupper ())               # Check if everything is in upper case.
print (mystr.lower().islower())        # Note that mystr.islower().lower() cannot be done.
print (mystr.index ("e"))              # First index of `e`.
print (mystr.index ("Pan")             # First index where "Pan" starts.
print (mystr.replace ("Sud", 'lol'))   # Replace the occurrence of 'Sud' with 'lol'
print (mystr.isdigit())                # Checks if `mystr` is a number. Returns False in this case.
print (mystr.rstrip(',.'))             # Strips the characters '.' and ',' from the end of the string
```

Strings can be concatenated with a `+` sign as demonstrated earlier.

```python
# Concatenation with a '+' sign
# requires both operands to be strings.
my_age = 21
print ("My age is " + my_age)        # will throw an error
print ("My age is " + str(my_age))   # works
```


# Useful Functions
```py
help(func)                # Get the documentation for indenrifier specified by `func`
len(x)                    # Generalized length function. x can be a string, list, etc.
round (x)                 # Rounds off 'x' to the closest whole number (x = 3.5 -> 4 | x = 3.4 -> 3).
abs (x)                   # Absolute value of 'x'.
pow (x, y)                # Calculates x^y (x to the power of y).
max (x, y)                # Max of x and y.
min (x, y)                # Min of x and y.
str (5)                   # Converts the number 5 to a string object.
int ('c')                 # Converts a char to an int object.
```

# Math module
```py
floor (x)                 # Greatest integer less than x.
ceil (x)                  # Least integer greater than x.
sqrt (x)                  # Square root of x.
```

# Input at run time
```python
name = input ("Enter your name: ")         # Prompts the user to input their name.
# input() accepts the input as a string.
# All other data types must be typecasted.
age = int (input ("How old are you: "))    # Prompts the user to input their age.
salary = float (input ("Your Salary? "))   # Prompts the user to input their salary.
```


# Lists
* Same list can accomodate elements of different types.
* In python, accessing a nested list cannot be done with multi dimensional slicing like [0, 1:5].
They do not work the way MATLAB or NumPy arrays work.

## Basics
```python
# Example 1
my_list = ["bro_1", 5, 'k', "bro_2"]
print (my_list[0])      # Prints bro_1
print (my_list[-1])      # Prints bro_2

# Example 2
nums = [0, 1, 2, 3, 4, 5, 6]
print (nums[2:5])       # Prints 2, 3, 4 (2 to 4)
print (nums[4:])        # Prints 4, 5, 6 (4 to end)

# Example 3
multi_list = [[[1, 2], [3, 4]],
              [[5, 6], [7, 8]]]

# A three dimensional list has been defined above. The outermost brackets 
# decide the 1st dimension, the next brackts decide the second and so on.
# The following chunk of code can help you understand this... 

print (multi_list[0, 0, 0])  # = 1
print (multi_list[0, 0, 1])  # = 2
print (multi_list[0, 1, 0])  # = 3
print (multi_list[0, 1, 1])  # = 4
print (multi_list[1, 0, 0])  # = 5
print (multi_list[1, 0, 1])  # = 6
print (multi_list[1, 1, 0])  # = 7
print (multi_list[1, 1, 1])  # = 8
```

## Common functions
```python
lis_1 = [1, 2, 3, 4, 5]
lis_2 = ["hello", "darkness", "my", "old", "friend"]

lis_1.extend (lis_2)             # Appends lis_2 at the end of lis_1.
lis_1.append ("sup")             # Appends "sup" at the end of lis_1.
lis_1.insert (2, 2.5)            # Insert 2.5 at the 2nd position of lis_1, existing elements are pushed right.
lis_1.reverse()                  # Reverse the existing order of the list.
lis_3 = lis_1.copy()             # Copy lis_1 into lis_3.
lis_2.remove ("darkness")        # Removes "darkness" from the list (pun).
lis_2.pop ()                     # Removes the last item of the list (Use the list like a Stack).
lis_2.index ("my")               # Returns the index of "my" in the list. Error if element is not in the list.
lis_2.sort()                     # Sorts the list.
lis_2.count("old")               # Count how many times the entry "old" comes in the list.
```

## List Comprehensions
```py
threshold = 5
L = [1, 7, 5, 4, 3]
elem_greater = [elem > threshold for elem in L]      # This is a list comprehension
```

# Tuples
**Note:** Tuples are immutable.

```python
# Example 1
tup_1 = (0, 1, 2, 3, 4)
print (tup_1[3])                # Prints 3

# Example 2
coordinates = [ (1, 2), (3, 4)] # List of tuples
```


# if-else
```python
a = 5
b = 4
c = 7
# The sequence explains the usual syntax.
if a > b or a > c:
  print ("a is not the least")
elif a < b and a < c :
  print ("a is the least")
elif a == b:
  print ("a is equal to b")
elif b != c:
  print ("b is not equal to c") 
else:
  print ("I'm stumped")
```


# Dictionaries
* Used to store key-value pairs.
* All keys should be unique.
```python
# Creation
my_dict = { "Jan" : "January", "Feb" : "February", "Mar" : "March", "Apr" : "April"} 
```

```python
# Accessing the value corresponding to a key
print (my_dict["Jan"])
# We can use get() function, with which, we can define
# a default if the specified key is not found.
print (my_dict.get("Jan", "Not a valid key")) 
```


# Loops

### While loop
```python
i = 0
while i < 10:
  print (i)
  i += 1
print ("finished")
```
### For loop
For loops in python can do a whole lot. They can iterate through various kind of sequences and we will demonstrate this with various examples...

```python
# Example 1 (Iterates through the characters in the String and prints them)
for letter in "Sudeepam Pandey":
  print (letter)

# Example 2 (Iterates through the items of the list and prints them)
my_list = ["item_0", "item_1", "item_2", "item_3", "item_4"]
for my_items in my_list:
  print (my_items)

# Example 3 (Iterates through the items of the list and prints them along with their index)
for index, my_items in enumerate(my_list):
  print (index)
  print (my_items)

# Example 4 (Prints all numbers in range 0 - 10, excluding 10)
for i in range(100):
  print (i)

# Example 5 (Traversing a multi dimensional list. Remember, lists don't support multi dimensional slicing)
my_list = [ [1, 2, 3],
            [4, 5, 6],
            [7, 8, 9],
            [0] ]
for row in my_list:      # row holds each row list [1, 2, 3] / [4, 5, 6] etc.
  for col in row:        # then col traverses through the list in row.
    print (col)

# Example 6 (The `in` keyword in python can actually be used to check if a value is present in a..
#            range of values). The code below checks is the character entered by user is a vowel.
ch = input("enter a character")
if ch in "AEIOUaeiou"
  print ("present")
```


# Try-except
* Imagine we are executing a long program. We would not want the entire execution to break because of minor exceptions like invalid user inputs at run time. 
* Minor runtime exceptions may occur all the time, so instead of them breaking the cycle of execution, we introduce a try-except block that can handle these exceptions at run time.
```python
# "done" will not be printed if the user does not enter a valid number. 
num = int(input("Enter a number: "))
print ("done")

# "done" will be printed even if the user does not enter a valid number. 
try:
    num = int(input("Enter a number: "))
    print (num)
except:
    print ("Invalid Input")
print ("done")
```

* Below is an example of ineffective exception handling.
* The error is a divide by zero error but we are printing invalid input, which is inconsistent
```python
try:
    val = 10 / 0
    num = int(input("Enter a number: "))
    print (num)
except:
    print ("Invalid Input")
```
We can handle this effectively with something like this...
```python
try:
    val = 10 / 0
    num = int(input("Enter a number: "))
    print (num)
# To catch the exact exception that was raised.
except Exception as e:
  print (e)
# To catch specific type of errors.
except ZeroDivisionError:
    print ("Divided by zero")
except ValueError:
    print ("Invalid Input")
```

Sometimes, it is useful to know the exact exception that was raised. It can be done as follows...
```python
try:
    val = 10 / 0
except ZeroDivisionError as err:
    print (err) # Spits out the exact message.
```


# Files I/O
Basics ...
```python
# f is the file object.
# `r`, `w`, and `a`, decide the read/write/append permissions.
# `r` is default. We can do `w+`, `r+`, and `a+`. This will
# open the file, for instance in, both read and write modes.
f = open (filename, 'r/w/a')
# Reads the contents of the file into the txt variable as a string 
txt = f.read ()
# Closes the file object
f.close ()
```

Some useful functions ...
```python
f.readline ()      # Reads one line of the file and seeks the cursor to the start of next line.
f.readlines ()     # Reads each line of the file and puts them in a list.
f.truncate ()      # Deletes the contents of the file.
f.write ("...")    # Writes contents into the file.
f.seek (k)         # Moves the cursor to the kth location in the file
```
**Note:** `'w'` overwrites the files whereas `'a'` adds to the existing contents of the files.


# Importing code
`import` keyword is used to import modules in python. Below are some examples of how modules are imported and used:
```python
# Example 1
import numpy
arr = numpy.array([1, 2, 3])

# Example 2
import numpy as np
arr = np.array([1, 2, 3])

# Example 3
from numpy import array
arr = array([1, 2, 3])
```
## Something extra
* Below is how we accept and unpack command line arguments in python.
* We can pass as many arguments as there are variables to unpack into.
* All command line arguments are strings.
```python
from sys import argv
script, first, second, third = argv
```
Now execute this script as follows in your terminal ...
```
user-PC:~$ python3 code.py hello I'm Sudeepam
```
to get ...
```python
script == "code.py"
first == "hello"
second == "I'm"
third == "Sudeepam"
```


# Functions
In python, functions are defined as follows:
```python
def function_name (arguments):
    # Code...
    # Code...
```

Examples of how arguments can be passed in python functions ...
```python
# Example 1  (Pass by value)
def pass_by_val (arg1, arg2):
    """ This is a docstring. This is basically the
    documentation of this function and this is what
    is returned by the `help` function"""
    print (f"arg1: {arg1}, arg2: {arg2}")

pass_by_val ("Sudeepam","Pandey")
```
```py
# Example 2  (Returning values)
def returning_stuff ():
    return "nothing here"

message = returning_stuff ()
print (message)
```

```py
# Example 3 (Pack arguments into a dictionary)
def pass_dictionary (*args):
    arg1, arg2 = args
    print (f"arg1: {arg1}, arg2: {arg2}")

pass_dictionary ("Sudeepam","Pandey")
```

```py
# Example 4 (Passing file pointers)
def print_file (f): 
    print (f.read())

f = open ("text_file.txt")
print_file(f)
```


# Classes and Objects
Creating a Class ...
```python
class undergrad_student:
  # Class attributes (this attribute is same for all instances of the class)
  university = "JIIT"

  # Instance attributes (these attributes can be different for each instance)
  def __init__(self, name, major, gpa, is_placed):
    self.name = name
    self.major = major
    self.gpa = gpa
    self.is_placed = is_placed

  # Instance methods
  def check_gpa_criterion (self)
    if self.gpa >= 7.0
      return True
    else
      return False
```

Creating an object (instance of a class) ...
```python
student1 = undergrad_student ("Sudeepam", "ECE", "7.0", False)
```

Accessing the members of an objects ...
```python
print (student1.name)
print (student1.major)
result = student1.check_gpa_criterion ()
if result == True
  print ("GPA criterion Satisfied")
else
  print ("GPA criterion not Satisfied")
```
In various programming languages, there is a concept of  private members of a class. If
something is declared private, it essentially means that you do not want to mess around
with it. Some languages impose this by strictly disabling the access to private members.
In a practical situation however, someone who really wants to access these private
members would be able to do so very easily.

Python therefore, does not impose any such restrictions. In reality, all class members
in python are public. Python only has a simple convention that notifies the programmer
about a private member and encourages them to not mess around with it. The convention
is to start the name of such need to be private members with a double underscore `__`.

For example:
```python
class Student:
  # hidden variable
  __hidden = "Hidden variable, don't tamper it"

  # hidden method
  def __hidden_method (self):
    #code...
    #code...

# Hidden members cannot be directly accessed from outside the class
Student1 = Student ()
print (Student1.__hidden)          # throws error

# Hidden members can be accessed with an extra line of code
print (Student1._Student__hidden)  # prints the hidden variable
```

# Inheritance
**Note:** The code snippets have been borrowed from [here](https://www.digitalocean.com/community/tutorials/understanding-class-inheritance-in-python-3).
* In inheritance a class, usually called the superclass is inherited by a subclass.
* Lets create a superclass first ...

```python
class Fish:
  def __init__ (self, first_name, last_name = "Fish", skeleton = "bone", eyelids = False):
    self.first _name = first_name
    self.last_name = last_name
    self.skeleton = skeleton
    self.eyelids = eyelids

    def swim (self):
      print ("This fish is swimming")
    
    def swim_backwards (self):
      print ("This fish can swim backwards")
```

* The subclass will be able to make use of methods and variables of the superclass
* We can also choose to just use the existing members of the superclass by using the `pass` keyword, or we can add more members and override existing members.
* Lets create a subclass ...

```python
# Example 1: using `pass`
class Trout(Fish):
    pass

terry = Trout("Terry")
print(terry.first_name + " " + terry.last_name)
print(terry.skeleton)
print(terry.eyelids)
terry.swim()
terry.swim_backwards()
```
