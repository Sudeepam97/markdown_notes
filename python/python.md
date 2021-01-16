- comprehensions
- special _type functions
- init
- loop and functions upar
- tuple string multi line wala
- l1.sort()                 # Sorts the list in-place.
- sorted()




# Some Basics
* Everything in python is an object.
* Boolean values are `True` and `False`.
* `\` is to escape next character and so `\\` can be used to get a backslash. `eg: print ("\\")`
* Python uses PEMDAS (Parentheses Exponents Multiplication Division Addition Subtraction) to evaluate expressions.
* Python doesn't have real private methods, so one underline in the beginning of a method or attribute means you shouldn't access it, because it's not part of the API.
* The goal of two underlines in the beginning of is to avoid the attribute/method to be overridden by a subclass.
* Finally `__this__` has a special meaning to python. It is a method that python calls and not us.
* to check if some variable (say `x`) resolves to `True`, do bool(x)






# Operators
| Operator     | Name           | Description                                         |
|--------------|----------------|-----------------------------------------------------|
| `a + b`      | Addition       | Sum of `a` and `b`                                  |
| `a - b`      | Subtraction    | Difference of `a` and `b`                           |
| `a * b`      | Multiplication | Product of `a` and `b`                              |
| `a / b`      | True division  | Quotient of `a` and `b`                             |
| `a // b`     | Floor division | Quotient of `a` and `b`, removing fractional parts  |
| `a % b`      | Modulus        | Integer remainder after division of `a` by `b`      |
| `a ** b`     | Exponentiation | `a` raised to the power of `b`                      |
 `-a`         | Negation       | The negative of `a`                                  |  




# Strings
* In python, double quotes (`""` or `''`) are used for single line strings and triple quotes (`"""` or `'''`) are used for multiline strings.
```python
s = "Sudeepam Pandey."     # An object of the string class.

s.lower()                  # Convert to lower case (similarly s.upper()).
s.isupper()                # Check if everything is in upper case.
s.isdigit()                # Checks if `s` is a valid number.

s.index("e")               # First index of `e`.
s.index("Pan")             # First index where "Pan" starts.
s.replace("ud", 'du')      # Replace all occurrences of 'ud' with 'du'

s.strip('Sud')             # Strips "sud" from the start of the string
s.rstrip(',.')             # Strips the characters '.' and ',' from the end of the string

```

Strings can be concatenated with a `+` sign. Note that this requires **both** operands to be strings. Note that this method is not clean and should be avoided.
```python
age = 21
statement = "My age is " + age        # incorrect
statement = "My age is " + str(age)   # correct
```

Here's a super clean method to use if you want a single line string but the string is too large to fit in a single line of code.
```python
# Try this
output = (
  "I want to print this string "
  "in a single line "
  "but using a single line to "
  "define this in the code is super ugly. "
  "Thereforre, I will use this neat trick."
)
print(output)
```




# Printing
```python
# example 1: prints 'name'
print("name")

# example 2: comma separated
name = "sudeepam"
print("name is", name)

# example 3: We can specify the
# line endings in the print
# function like so..
print("cheese", end = " ")
print("burger")
# prints 'cheese burger'
```

### Formatted printing: 
```python
name = "Sudeepam"

# Method 1: Never Use. Not clean
print("My name is " + name)

# Method 2: Python 3.6+
print(f"My name is {name}")

# Method 3: Most resilient method
print("My name is {my_name}.format(my_name=name))
# if key value pair is not specified,
# the alphabetical order is considered.
```




# Lists
A list can accomodate multiple elements of same or different data types.

## Basics
```python
# Example 1
items = ["apple", 5, "c", "orange"]
print(items[0])      # Prints 'apple'
print(items[-1])     # Prints 'orange'

# Example 2
nums = [0, 1, 2, 3, 4, 5, 6]
print (nums[2:5])    # Prints '2, 3, 4' (2 to 4)
print (nums[4:])     # Prints '4, 5, 6' (4 to end)

# Example 3
multi_list = [
  [[1, 2], [3, 4]],
  [[5, 6], [7, 8]]
]

# A three dimensional list has been defined above. The outermost brackets 
# decide the 1st dimension, the next brackts decide the second and so on.
# The following piece of code will help you understand this... 

print(multi_list[0, 0, 0])    # = 1
print(multi_list[1, 0, 0])    # = 5
print(multi_list[1, 1, 1])    # = 8

# A nested python list cannot be accessed via multi
# dimensional slicing like MATLAB arrays or NumPy arrays.
# Example 4:
multi_list = [
  [[1, 2], [3, 4], [5, 6]],
  [[7, 8], [9, 2], [7, 3]]
]

print(multi_list[0, 1:])
# throws an error instead of printing
# [[3, 4], [5, 6]]

```

## Some methods available in lists
```python
l1 = ["hello", "darkness", "my", "old"]
l2 = [1, 2, 3, 4, 5]


l1.pop ()                 # Removes the last item of the list.
l1.reverse()              # Reverse the existing order of the list.
l1.extend(l2)             # Appends l2 at the end of l1.
l1.append("friend")       # Appends "sup" at the end of l1.
```




# Tuples
Tuples are similar to lists except the fact that **tuples are immutable.**

```python
# Example 1
t1 = (0, 1, 2, 3, 4)
print (t1[3])                     # Prints `3`

# Example 2
coordinates = [(1, 2), (3, 4)]    # List of tuples
```




# Iterable and Iterators
**DISCLAIMER**: Many questions will arise as you read through this section. Please go through the entire thing to get answers for most of them.

* In python, an `iterable` is an object that can be iterated through, and an `iterator` is an object that is used to iterate through an `iterable`.

* `iterators` and `iterables` are defined by these properties respectively:
  * All `iterators` contain a `__next()__` method.
  *  All `iterables` contain an `__iter()__` method or a `__getitem__()` method. Defining a `__iter__()` method is the preferred way to create an iterable, and defining the `__getitem__()` method is the legacy way. We'll discuss this in a bit.


* The `__iter__()` method returns an iterator for the given iterable.

* The `__next__()` method returns the next item of the iterable. If there are no further items, `__next()__` raises the `StopIteration` exception.

* The `__get_item__()` method is a bit different. It is used to **get** an item via its key or index.

  This essentially means that the `[]` syntax for getting an item by its key or index is just syntactic sugar. `__get_item__()` is what is called under the hood when you do something like `x = dummy_list[5]`.
  
  Since we're on it, let me also mention a method called `__set_item__()` which is used to **assign** by index or key, like so `dummy_list[3] = 10`. Take a look at [this](https://stackoverflow.com/questions/43627405/understanding-getitem-method/43627975#43627975) example.

* At this point, I'd like to give an example of when you would need all of this knowledge.

  Let's say that you are creating a class, and you would like the objects of this classes to be iterable via a for loop.
  
  Under the hood, a for loop just makes calls to these `__iter__()` and `__next__()` methods to perform the action of iteration, so this is where you would have to implement an `__iter__()` function for your class, and a `__next__()` function for the iterator of your class.


* Lastly, `__get_item__()` is a legacy way to create iterable classes. The idea was that anything that is indexable, would have a length, and is therefore, iterable.

  In contrast, `__iter__()` allows us to define classes that are iterable without necessarily being indexable. A perfect example for this is a linkedlist (iterable but not indexable).
  
  Finally, we should understand that in modern python, anything that is iterable and indexable should have both, an `__iter__()` and a `__get_item__()`.

Please look at [these](https://docs.python.org/3/tutorial/classes.html#iterators) docs/examples on iterators.




# Dictionaries
* Used to store key-value pairs.
* All keys should be unique.
* Internally uses a HashMap, hence complexity is O(1)
```python
# Creating a dict
months = { "Jan" : "January", "Feb" : "February", "Mar" : "March"} 

# Accessing a dict
months["Jan"]

 # Access with default value
months.get("May", "Not a valid key")

# We can update values like so
months["Jul"] = "July"

# Update existing keys, insert the ones not present
months.update({"Jan": "Birthday Month", "Jun": "June"})

# returns an iterable containing all keys of dict
months.keys()

# returns an iterable containing all values of dict
months.values()

# returns an iterable containing all key value pairs of the dict
months.items()
```




# Set
Set is...




# Comprehensions
```py
threshold = 5
L = [1, 7, 5, 4, 3]
elem_greater = [elem > threshold for elem in L]      # This is a list comprehension
```



# The `split()` function
The `split()` function allows us to split a string into a list.

`Syntax: string.split(separator, maxsplit)`

```python
# Example 1
sentence = "Welcome my friend"
words = sentence.split()
print(words)            # ["Welcome", "my", "friend"]


# Example 2
inpt = "1, 2, 3, 4, 5"
nums = inpt.split(",")  # ["1", "2", "3", "4", "5"]


# Example 3
inpt = "1, 2, 3, 4, 5"
inpt.split(",", 2)      # ["1", "2", "3"] (note that there are 2 splits here)
```




# The `map()` function
The `map()` function allows us to apply a given function to each item of an iterable and returns a map object (which is an iterator).
```python 
def square(num):
  '''Return square of num'''
  return num * num 

numbers = [5, 3, 6, 4] 
result = map(square, numbers)

# printing the result
for number in numbers:
  print("Square of {num} is {sqr}".format(
    num = number,
    sqr = next(result)
  ))
```




# Input at run-time
The Statement:
```python
name = input("Enter your name: ")
```

`input()` accepts the input as a string. All other data types must be typecasted.
```python
age = int(input("How old are you: "))
salary = float(input("Your Salary? "))
```

Taking space separated integers as input:
```python
numbers = list(map(int, input().split()))
```







# Useful Functions
```py
help(func)                # Get the documentation for indentifier specified by `func`
len(x)                    # Generalized length function. x can be a string, list, etc.
round (x)                 # Rounds off 'x' to the closest whole number (x = 3.5 -> 4 | x = 3.4 -> 3).
abs (x)                   # Absolute value of 'x'.
pow (x, y)                # Calculates x^y (x to the power of y).
max (x, y)                # Max of x and y.
min (x, y)                # Min of x and y.
```




# Math module
```py
import math

math.floor (x)                 # Greatest integer less than x.
math.ceil (x)                  # Least integer greater than x.
math.sqrt (x)                  # Square root of x.
```


# if-elif-else
```python
a = 5
b = 4
c = 7
# The sequence explains the usual syntax.
if a > b and a > c:
  print ("a is the largest")
elif a < b and a < c>:
  print ("a is the smallest")
else:
  print ("a is neither the largest, nor the smallest")
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
