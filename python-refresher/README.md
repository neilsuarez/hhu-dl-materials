# Python Refresher

This refresher is a based on the Python
[learnxinyminutes](https://learnxinyminutes.com/docs/python3/) refresher (which
you may want to read in full anyway). It extends it with some additional topics
(e.g. type annotations, randomness).  Some examples and additional topics
originate from the [Data Science from
Scratch](https://www.oreilly.com/library/view/data-science-from/9781492041122/)
book.


## ToC

* [Comments](#comments)
* [Whitespace Formatting](#whitespace-formatting)
* [Primitive Datatypes and Operators](#primitive-datatypes-and-operators)
* [Modules](#modules)
* [Functions](#functions)
* [Exceptions and Files](#exceptions-and-files)
* [Data Structures](#data-structures)
* [Control Flow](#control-flow)
* [Comprehension](#comprehension)
* [Testing](#testing)
* [Object-Oriented Programming](#object-oriented-programming)
* [Iterables](#iterables)
* [Generators](#generators)
* [Randomness](#randomness)
* [zip and Argument Unpacking](#zip-and-argument-unpacking)
* [args and kwargs](#args-and-kwargs)
* [Type Annotations](#type-annotations)


## Comments

```python


## Comments

```python
# Single line comments start with a number symbol.

""" Multiline strings can be written
    using three "s, and are often used
    as documentation.
"""
```

Python itself ignores the comments, but they help to understand your code.


## Whitespace Formatting

Many programming languages delimit blocks of code with brackets.  Python uses
indentation for this purpose.

```python
for i in [1, 2, 3]:
    # Start of the body of the "for i" loop
    print(i)
    for j in [1, 2]:
        # Start of the body of the "for j" loop
        print(i, j)
        print("Something else")
        # End of the body of the "for j" loop
    # End of the body of the "for i" loop
```

This is pretty neat, but can lead to errors.  For instance, be careful to use
four spaces (rather than tabs) for indentation!  Your editor will normally take
care of that, though.

Whitespace is ignored inside parentheses and brackets, which allows to make the
code more readable and deal with long code lines.

```python
less_readable_list = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

potentially_more_readable_list = [[1, 2, 3],
                                  [4, 5, 6],
                                  [7, 8, 9]]
```

If you want to split a line of code outside brackets, you will have to use \\.
```python
list_in_next_line = \
    [[1, 2, 3],
     [4, 5, 6],
     [7, 8, 9]]
```


## Primitive Datatypes and Operators

### Numbers

```python
# You have numbers
3  # => 3

# Math is what you would expect
1 + 1   # => 2
8 - 1   # => 7
10 * 2  # => 20
35 / 5  # => 7.0 (the result of division is always a float)

# Integer division rounds down for both positive and negative numbers
5 // 3       # => 1
-5 // 3      # => -2
5.0 // 3.0   # => 1.0 # works on floats too
-5.0 // 3.0  # => -2.0

# To cast an int to float or a float to int
int(3.0)      # => 3
float(3)      # => 3.0
int(1.9)      # => 1

# If you want a consistent and intuitive rounding behavior, use round
# (always gives an int)
round(5 / 3)   # => 2
round(-5 / 3)  # => -2
round(1.9)     # => 2

# Modulo operation
7 % 3  # => 1

# Exponentiation (x**y, x to the yth power)
2**3  # => 8

# Enforce precedence with parentheses
(1 + 3) * 2  # => 8
```

### Booleans

```python
# Boolean values are primitives (Note: the capitalization)
True
False

# negate with not
not True   # => False
not False  # => True

# Boolean Operators
# Note "and" and "or" are case-sensitive
True and False  # => False
False or True   # => True

# True and False are actually aliases for 1 and 0
True + True # => 2
True * 8    # => 8
False - 5   # => -5
```

### None

```python
# None indicates a nonexistent value, which is similar to
# 'null's in other languages
None  # => None
```

### Equality and Comparison

```python
# Equality is ==
1 == 1  # => True
2 == 1  # => False

# Inequality is !=
1 != 1  # => False
2 != 1  # => True

# More comparisons
1 < 10  # => True
1 > 10  # => False
2 <= 2  # => True
2 >= 2  # => True

# Seeing whether a value is in a range
1 < 2 and 2 < 3  # => True
2 < 3 and 3 < 2  # => False
# Chaining makes this look nicer
1 < 2 < 3  # => True
2 < 3 < 2  # => False

# (is vs. ==) is checks if two variables refer to the same object, but == checks
# if the objects pointed to have the same values.
a = [1, 2, 3, 4]  # Point a at a new list, [1, 2, 3, 4]
b = a             # Point b at what a is pointing to
b is a            # => True, a and b refer to the same object
b == a            # => True, a's and b's objects are equal
b = [1, 2, 3, 4]  # Point b at a new list, [1, 2, 3, 4]
b is a            # => False, a and b do not refer to the same object
b == a            # => True, a's and b's objects are equal

# Don't use the equality "==" symbol to compare objects to None
# Use "is" instead. This checks for equality of object identity.
"etc" is None  # => False
None is None   # => True
```


<!---
# (is vs. ==) is checks if two variables refer to the same object, but == checks
# if the objects pointed to have the same values.
a = [1, 2, 3, 4]  # Point a at a new list, [1, 2, 3, 4]
b = a             # Point b at what a is pointing to
b is a            # => True, a and b refer to the same object
b == a            # => True, a's and b's objects are equal
b = [1, 2, 3, 4]  # Point b at a new list, [1, 2, 3, 4]
b is a            # => False, a and b do not refer to the same object
b == a            # => True, a's and b's objects are equal


# None indicates a nonexistent value, which is similar to 'null's in other languages
None  # => None

# Don't use the equality "==" symbol to compare objects to None
# Use "is" instead. This checks for equality of object identity.
"etc" is None  # => False
None is None   # => True

# Comparison operators look at the numerical value of True and False
0 == False  # => True
1 == True   # => True
2 == True   # => False
-5 != False # => True

# Using boolean logical operators on ints casts them to booleans for evaluation, but their non-cast value is returned
# Don't mix up with bool(ints) and bitwise and/or (&,|)
bool(0)     # => False
bool(4)     # => True
bool(-6)    # => True
0 and 2     # => 0
-5 or 0     # => -5

# None, 0, and empty strings/lists/dicts/tuples all evaluate to False.
# All other values are True
bool(0)   # => False
bool("")  # => False
bool([])  # => False
bool({})  # => False
bool(())  # => False

# Strings are created with " or '
"This is a string."
'This is also a string.'

# Strings can be added too! But try not to do this.
"Hello " + "world!"  # => "Hello world!"
# String literals (but not variables) can be concatenated without using '+'
"Hello " "world!"    # => "Hello world!"

# A string can be treated like a list of characters
"This is a string"[0]  # => 'T'

# You can find the length of a string
len("This is a string")  # => 16

# .format can be used to format strings, like this:
"{} can be {}".format("Strings", "interpolated")  # => "Strings can be interpolated"

# You can repeat the formatting arguments to save some typing.
"{0} be nimble, {0} be quick, {0} jump over the {1}".format("Jack", "candle stick")
# => "Jack be nimble, Jack be quick, Jack jump over the candle stick"

# You can use keywords if you don't want to count.
"{name} wants to eat {food}".format(name="Bob", food="lasagna")  # => "Bob wants to eat lasagna"

# You can also format using f-strings or formatted string literals (in Python 3.6+)
name = "Reiko"
f"She said her name is {name}." # => "She said her name is Reiko"
# You can basically put any Python statement inside the braces and it will be output in the string.
f"{name} is {len(name)} characters long." # => "Reiko is 5 characters long."
-->


### Strings

```python
# Strings are created with " or '
"This is a string."
'This is also a string.'

# Strings can be added too! But try not to do this.
"Hello " + "world!"  # => "Hello world!"
# String literals (but not variables) can be concatenated without using '+'
"Hello " "world!"    # => "Hello world!"

# A string can be treated like a list of characters
"This is a string"[0]  # => 'T'

# You can find the length of a string
len("This is a string")  # => 16

# .format can be used to format strings, like this:
"{} can be {}".format("Strings", "interpolated")  # => "Strings can be interpolated"

# You can repeat the formatting arguments to save some typing.
"{0} be nimble, {0} be quick, {0} jump over the {1}".format("Jack", "candle stick")
# => "Jack be nimble, Jack be quick, Jack jump over the candle stick"

# You can use keywords if you don't want to count.
"{name} wants to eat {food}".format(name="Bob", food="lasagna")  # => "Bob wants to eat lasagna"

# You can also format using f-strings or formatted string literals (in Python 3.6+)
name = "Reiko"
f"She said her name is {name}." # => "She said her name is Reiko"
# You can basically put any Python statement inside the braces and it will be output in the string.
f"{name} is {len(name)} characters long." # => "Reiko is 5 characters long."
```




## Modules

```python
# You can import modules
import math
print(math.sqrt(16))  # => 4.0

# You can get specific functions from a module
from math import ceil, floor
print(ceil(3.7))   # => 4.0
print(floor(3.7))  # => 3.0

# You can import all functions from a module.
# Warning: this is not recommended
from math import *

# You can shorten module names
import math as m
math.sqrt(16) == m.sqrt(16)  # => True
```

Python modules are just ordinary Python files. You can write your own, and
import them. The name of the module is the same as the name of the file.

If you have a Python script named math.py in the same folder as your current
script, the file math.py will be loaded instead of the built-in Python module.
This happens because the local folder has priority over Python's built-in
libraries.

<!---
# You can find out which functions and attributes
# are defined in a module.
import math
dir(math)
-->


## Functions

```python
# Use "def" to create new functions
def add(x, y):
    """Optional documetation string.  For example, return the sum
    of the two arguments.
    """
    print("x is {} and y is {}".format(x, y))
    return x + y  # Return values with a return statement

# Calling functions with parameters
add(5, 6)  # => prints out "x is 5 and y is 6" and returns 11

# Another way to call functions is with keyword arguments
add(y=6, x=5)  # Keyword arguments can arrive in any order.

# Functions in Python are first-class, which means that you can
# assign them to variables, provide as arguments, or return from
# functions.
def create_adder(x):
    """Create a function which adds x to whatever you want."""
    def adder(y):
        return x + y
    return adder

add_10 = create_adder(10)
add_10(3)   # => 13

# You can provide defalt argument values, which don't have
# to be specified by the caller.
def print_msg(message='whatever')
    print(message)

print_msg('hello')                    # => prints 'hello'
print_msg()                           # => prints 'whatever'

# You can use anonymous functions, but using the standard
# 'def' syntax is typically preferable.
(lambda x: x > 2)(3)                  # => True
(lambda x, y: x ** 2 + y ** 2)(2, 1)  # => 5

# There are also some higher-order functions (`map`, `filter`), 
# although Python encourages to use comprehension instead.
list(map(add_10, [1, 2, 3]))          # => [11, 12, 13]
[add_10(x) for x in [1, 2, 3]]        # The same using list comprehension
```


<!---

# Returning multiple values (with tuple assignments)
def swap(x, y):
    return y, x  # Return multiple values as a tuple without the parenthesis.
                 # (Note: parenthesis have been excluded but can be included)

x = 1
y = 2
x, y = swap(x, y)     # => x = 2, y = 1
# (x, y) = swap(x,y)  # Again parenthesis have been excluded but can be included.

# There are built-in higher order functions
list(map(add_10, [1, 2, 3]))          # => [11, 12, 13]
list(map(max, [1, 2, 3], [4, 2, 1]))  # => [4, 2, 3]

list(filter(lambda x: x > 5, [3, 4, 5, 6, 7]))  # => [6, 7]

# We can use list comprehensions for nice maps and filters
# List comprehension stores the output as a list which can itself be a nested list
[add_10(i) for i in [1, 2, 3]]         # => [11, 12, 13]
[x for x in [3, 4, 5, 6, 7] if x > 5]  # => [6, 7]

# You can construct set and dict comprehensions as well.
{x for x in 'abcddeef' if x not in 'abc'}  # => {'d', 'e', 'f'}
{x: x**2 for x in range(5)}  # => {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}

# Function Scope
x = 5

def set_x(num):
    # Local var x not the same as global variable x
    x = num    # => 43
    print(x)   # => 43

def set_global_x(num):
    global x
    print(x)   # => 5
    x = num    # global var x is now set to 6
    print(x)   # => 6

set_x(43)
set_global_x(6)
-->



## Exceptions and Files

```python
# Handle exceptions with a try/except block
try:
    # Use "raise" to raise an error
    raise IndexError("This is an index error")
except IndexError as e:
    pass                 # Pass is just a no-op. Usually you would do recovery here.
except (TypeError, NameError):
    pass                 # Multiple exceptions can be handled together, if required.
else:                    # Optional clause to the try/except block. Must follow all except blocks
    print("All good!")   # Runs only if the code in try raises no exceptions
finally:                 #  Execute under all circumstances
    print("We can clean up resources here")

# Instead of try/finally to cleanup resources you can use a with statement
with open("myfile.txt") as f:
    for line in f:
        print(line)

# Writing to a file
contents = {"aa": 12, "bb": 21}
with open("myfile1.txt", "w+") as file:
    file.write(str(contents))        # writes a string to a file

with open("myfile2.txt", "w+") as file:
    file.write(json.dumps(contents)) # writes an object to a file

# Reading from a file
with open('myfile1.txt', "r+") as file:
    contents = file.read()           # reads a string from a file
print(contents)
# print: {"aa": 12, "bb": 21}

with open('myfile2.txt', "r+") as file:
    contents = json.load(file)       # reads a json object from a file
print(contents)     
# print: {"aa": 12, "bb": 21}
```

## Data Structures

### Lists

```python
# Lists store sequences
li = []
# You can start with a prefilled list
other_li = [4, 5, 6]

# Add stuff to the end of a list with append
li.append(1)    # li is now [1]
li.append(2)    # li is now [1, 2]
li.append(4)    # li is now [1, 2, 4]
li.append(3)    # li is now [1, 2, 4, 3]
# Remove from the end with pop
li.pop()        # => 3 and li is now [1, 2, 4]
# Let's put it back
li.append(3)    # li is now [1, 2, 4, 3] again.

# Access a list like you would any array
li[0]   # => 1
# Look at the last element
li[-1]  # => 3

# Looking out of bounds is an IndexError
li[4]  # Raises an IndexError

# You can look at ranges with slice syntax.
# The start index is included, the end index is not
# (It's a closed/open range for you mathy types.)
li[1:3]   # Return list from index 1 to 3 => [2, 4]
li[2:]    # Return list starting from index 2 => [4, 3]
li[:3]    # Return list from beginning uptil index 3  => [1, 2, 4]
li[::2]   # Return list selecting every second entry => [1, 4]
li[::-1]  # Return list in reverse order => [3, 4, 2, 1]
# Use any combination of these to make advanced slices
# li[start:end:step]

# Make a one layer deep copy using slices
li2 = li[:]  # => li2 = [1, 2, 4, 3] but (li2 is li) will result in false.

# Remove arbitrary elements from a list with "del"
del li[2]  # li is now [1, 2, 3]

# Remove first occurrence of a value
li.remove(2)  # li is now [1, 3]
li.remove(2)  # Raises a ValueError as 2 is not in the list

# Insert an element at a specific index
li.insert(1, 2)  # li is now [1, 2, 3] again

# Get the index of the first item found matching the argument
li.index(2)  # => 1
li.index(4)  # Raises a ValueError as 4 is not in the list

# You can add lists
# Note: values for li and for other_li are not modified.
li + other_li  # => [1, 2, 3, 4, 5, 6]

# Concatenate lists with "extend()"
li.extend(other_li)  # Now li is [1, 2, 3, 4, 5, 6]

# Check for existence in a list with "in"
1 in li  # => True

# Examine the length with "len()"
len(li)  # => 6
```

### Tuples

```python
# Tuples are like lists but are immutable.
tup = (1, 2, 3)
tup[0]      # => 1
tup[0] = 3  # Raises a TypeError

# Note that a tuple of length one has to have a comma after the last element but
# tuples of other lengths, even zero, do not.
type((1))   # => <class 'int'>
type((1,))  # => <class 'tuple'>
type(())    # => <class 'tuple'>

# You can do most of the list operations on tuples too
len(tup)         # => 3
tup + (4, 5, 6)  # => (1, 2, 3, 4, 5, 6)
tup[:2]          # => (1, 2)
2 in tup         # => True

# You can unpack tuples (or lists) into variables
a, b, c = (1, 2, 3)  # a is now 1, b is now 2 and c is now 3
# You can also do extended unpacking
a, *b, c = (1, 2, 3, 4)  # a is now 1, b is now [2, 3] and c is now 4
# Tuples are created by default if you leave out the parentheses
d, e, f = 4, 5, 6  # tuple 4, 5, 6 is unpacked into variables d, e and f
# respectively such that d = 4, e = 5 and f = 6
# Now look how easy it is to swap two values
e, d = d, e  # d is now 5 and e is now 4
```

### Dictionaries

```python
# Dictionaries store mappings from keys to values
empty_dict = {}
# Here is a prefilled dictionary
filled_dict = {"one": 1, "two": 2, "three": 3}

# Note keys for dictionaries have to be immutable types. This is to ensure that
# the key can be converted to a constant hash value for quick look-ups.
# Immutable types include ints, floats, strings, tuples.
invalid_dict = {[1,2,3]: "123"}  # => Raises a TypeError: unhashable type: 'list'
valid_dict = {(1,2,3):[1,2,3]}   # Values can be of any type, however.

# Look up values with []
filled_dict["one"]  # => 1

# Get all keys as an iterable with "keys()". We need to wrap the call in list()
# to turn it into a list. We'll talk about those later.  Note - for Python
# versions <3.7, dictionary key ordering is not guaranteed. Your results might
# not match the example below exactly. However, as of Python 3.7, dictionary
# items maintain the order at which they are inserted into the dictionary.
list(filled_dict.keys())  # => ["three", "two", "one"] in Python <3.7
list(filled_dict.keys())  # => ["one", "two", "three"] in Python 3.7+


# Get all values as an iterable with "values()". Once again we need to wrap it
# in list() to get it out of the iterable. Note - Same as above regarding key
# ordering.
list(filled_dict.values())  # => [3, 2, 1]  in Python <3.7
list(filled_dict.values())  # => [1, 2, 3] in Python 3.7+

# You can also retrieve the list of the (key, value) pairs using "items()"
list(filled_dict.items())   # => [('one', 1), ('two', 2), ('three', 3)]

# Check for existence of keys in a dictionary with "in"
"one" in filled_dict  # => True
1 in filled_dict      # => False

# Looking up a non-existing key is a KeyError
filled_dict["four"]  # KeyError

# Use "get()" method to avoid the KeyError
filled_dict.get("one")      # => 1
filled_dict.get("four")     # => None
# The get method supports a default argument when the value is missing
filled_dict.get("one", 4)   # => 1
filled_dict.get("four", 4)  # => 4

# "setdefault()" inserts into a dictionary only if the given key isn't present
filled_dict.setdefault("five", 5)  # filled_dict["five"] is set to 5
filled_dict.setdefault("five", 6)  # filled_dict["five"] is still 5

# Adding to a dictionary
filled_dict.update({"four":4})  # => {"one": 1, "two": 2, "three": 3, "four": 4}
filled_dict["four"] = 4         # another way to add to dict

# Remove keys from a dictionary with del
del filled_dict["one"]  # Removes the key "one" from filled dict

# From Python 3.5 you can also use the additional unpacking options
{'a': 1, **{'b': 2}}  # => {'a': 1, 'b': 2}
{'a': 1, **{'a': 2}}  # => {'a': 2}
```

### Sets

```python
# Sets store ... well sets
empty_set = set()
# Initialize a set with a bunch of values. Yeah, it looks a bit like a dict. Sorry.
some_set = {1, 1, 2, 2, 3, 4}  # some_set is now {1, 2, 3, 4}

# Similar to keys of a dictionary, elements of a set have to be immutable.
invalid_set = {[1], 1}  # => Raises a TypeError: unhashable type: 'list'
valid_set = {(1,), 1}

# Add one more item to the set
filled_set = some_set
filled_set.add(5)  # filled_set is now {1, 2, 3, 4, 5}
# Sets do not have duplicate elements
filled_set.add(5)  # it remains as before {1, 2, 3, 4, 5}

# Do set intersection with &
other_set = {3, 4, 5, 6}
filled_set & other_set  # => {3, 4, 5}

# Do set union with |
filled_set | other_set  # => {1, 2, 3, 4, 5, 6}

# Do set difference with -
{1, 2, 3, 4} - {2, 3, 5}  # => {1, 4}

# Do set symmetric difference with ^
{1, 2, 3, 4} ^ {2, 3, 5}  # => {1, 4, 5}

# Check if set on the left is a superset of set on the right
{1, 2} >= {1, 2, 3} # => False

# Check if set on the left is a subset of set on the right
{1, 2} <= {1, 2, 3} # => True

# Check for existence in a set with in
2 in filled_set   # => True
10 in filled_set  # => False
```

<!--- #### Counters -->

## Control Flow

```python
# Let's just make a variable
some_var = 5

# Here is an if statement.  This prints "some_var is smaller than 10".
if some_var > 10:
    print("some_var is totally bigger than 10.")
elif some_var < 10:    # This elif clause is optional.
    print("some_var is smaller than 10.")
else:                  # This is optional too.
    print("some_var is indeed 10.")

# You can also use a ternary if-then-else as an expression.
parity = "even" if some_var % 5 == 0 else "odd"

# Python has while loops
x = 0
while x < 10:
    print("{x} is smaller than 10".format(x=10))
    x += 1

# As well as for loops
for x in range(10)    # range(10) is [1, 2, ..., 10]
    print("{x} is smaller than 10".format(x=10))

# More complex logic can be achieved using continue and break
for x in range(10):
    if x < 10:
        continue  # go immediately to the next iteration
    elif x == 5:
        break     # quit the loop
```

<!--- ## Thruthiness -->

<!--- ## Sorting -->

## Comprehension

```python
# We can use list comprehensions for nice maps and filters
# List comprehension stores the output as a list which can itself be a nested list
[i + 10 for i in [1, 2, 3]]            # => [11, 12, 13]
[x for x in [3, 4, 5, 6, 7] if x > 5]  # => [6, 7]

# You can construct set and dict comprehensions as well.
{x for x in 'abcddeef' if x not in 'abc'}  # => {'d', 'e', 'f'}
{x: x**2 for x in range(5)}  # => {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

## Testing

There are various frameworks for testing code, but during this course we will
mostly restrict ourselves to using the `assert` statements, which simply verify
that the given Boolean expression is `True` during the code execution.
```python
assert 2 + 2 == 4                         # You can use optional comment
assert 2 + 2 == 4, "2 + 2 should be 4"    # in case the assertion fails
```

You can use `assert` to test the functions and classes you write, to verify
that function arguments and/or the function's result satisfy certain
conditions, etc.


## Object-Oriented Programming

Python, as many programming languages, allows to define *classes* to
encapsulate data and the methods that can operate on them.

To give an example, let's implement a `Bag` datatype which behaves a bit like a
set, but allows to keep track of the number of occurrences of each element in
it.

```python
class Bag:
    """Just as functions, classes can/should be documented with docstrings."""

    # Constructor of the class, which takes whatever objects are required
    # to build a Bag.
    #
    # Note that the double leading and trailing underscores denote objects
    # or attributes that are used by Python but that live in user-controlled
    # namespaces. Methods(or objects or attributes) like: __init__, __str__,
    # __repr__ etc. are called special methods. You should not invent such
    # names on your own.
    #
    def __init__(self, elems=[]):
        # We keep track of the elements and their number in a dictionary.
        self.data = {}
        for elem in elems:
            self.add(elem)

    # An instance method. All methods take "self" as the first argument.
    def add(self, elem):
        """Add the given element to the bag."""
        try:
            self.data[elem] += 1
        except KeyError:
            self.data[elem] = 1

    def delete(self, elem):
        """Remove the given element from the bag."""
        try:
            k = self.data[elem]
            if k > 1:
                self.data[elem] = k - 1
            else:
                del self.data[elem]
        except KeyError:
            pass

    def number(self, elem):
        """Get the number of occurrences of the element in the bag."""
        try:
            return self.data[elem]
        except KeyError:
            return 0
```

### Inheritance

We can use inheritance to create new classes by extending or restricting the
existing ones.  For instance, let's say we know that in a particular part of
the code no elements should be removed from a given `Bag`.  We can either hope
for best and trust that the code works as expected (this may be a good idea
even if we are the authors of this piece of code), or enforce this by creating
a variant of the `Bag` which simply does not allow element removal.

```python
# Note the base class `Bag` specified inside the parentheses.
class SafeBag(Bag):
    """Bag from which elements cannot be removed"""

    # The sublass inherits all the methods (e.g., `number`) and attributes
    # (e.g., `data`) of its parent class.

    # We overwrite the `delete` method so that it raises an exception if used.
    def delete(self, elem):
        raise Exception("You cannot delete elements from the SafeBag.")
```

Note that Python will not stop the user from accessing the `data` attribute of
the `Bag` class (and, effectively, from deleting some elements manually).  You
can indicate that the attribute is *private* by using a single underscore
(i.e., `self._data`).  This works by convention, though, and the user is still
allowed to modify the attribute manually.


<!---
Classes can be pretty handy in numerical computing as well.  To give an
example, let's say that we want to perform some computations on regular numbers
in the logarithmic domain, e.g., because the numbers get either too small or
too large.
```python
math.log(2 ** 8)          # => 8
math.log(2 ** 1e10)       # raises OverflowError exception
```

One solution to this problem is to manually transform all the numbers using
`math.log`, replace `*` with `+`, `/` with `-`, etc.
-->



<!---
```python
# We use the "class" statement to create a class
class Human:

    # A class attribute. It is shared by all instances of this class
    species = "H. sapiens"

    # Basic initializer, this is called when this class is instantiated.
    # Note that the double leading and trailing underscores denote objects
    # or attributes that are used by Python but that live in user-controlled
    # namespaces. Methods(or objects or attributes) like: __init__, __str__,
    # __repr__ etc. are called special methods (or sometimes called dunder methods)
    # You should not invent such names on your own.
    def __init__(self, name):
        # Assign the argument to the instance's name attribute
        self.name = name

        # Initialize property
        self._age = 0

    # An instance method. All methods take "self" as the first argument
    def say(self, msg):
        print("{name}: {message}".format(name=self.name, message=msg))

    # Another instance method
    def sing(self):
        return 'yo... yo... microphone check... one two... one two...'

    # A class method is shared among all instances
    # They are called with the calling class as the first argument
    @classmethod
    def get_species(cls):
        return cls.species

    # A static method is called without a class or instance reference
    @staticmethod
    def grunt():
        return "*grunt*"

    # A property is just like a getter.
    # It turns the method age() into an read-only attribute of the same name.
    # There's no need to write trivial getters and setters in Python, though.
    @property
    def age(self):
        return self._age

    # This allows the property to be set
    @age.setter
    def age(self, age):
        self._age = age

    # This allows the property to be deleted
    @age.deleter
    def age(self):
        del self._age


# When a Python interpreter reads a source file it executes all its code.
# This __name__ check makes sure this code block is only executed when this
# module is the main program.
if __name__ == '__main__':
    # Instantiate a class
    i = Human(name="Ian")
    i.say("hi")                     # "Ian: hi"
    j = Human("Joel")
    j.say("hello")                  # "Joel: hello"
    # i and j are instances of type Human, or in other words: they are Human objects

    # Call our class method
    i.say(i.get_species())          # "Ian: H. sapiens"
    # Change the shared attribute
    Human.species = "H. neanderthalensis"
    i.say(i.get_species())          # => "Ian: H. neanderthalensis"
    j.say(j.get_species())          # => "Joel: H. neanderthalensis"

    # Call the static method
    print(Human.grunt())            # => "*grunt*"

    # Cannot call static method with instance of object 
    # because i.grunt() will automatically put "self" (the object i) as an argument
    print(i.grunt())                # => TypeError: grunt() takes 0 positional arguments but 1 was given

    # Update the property for this instance
    i.age = 42
    # Get the property
    i.say(i.age)                    # => "Ian: 42"
    j.say(j.age)                    # => "Joel: 0"
    # Delete the property
    del i.age
    # i.age                         # => this would raise an AttributeError
```

### Inheritance

```python
# Inheritance allows new child classes to be defined that inherit methods and
# variables from their parent class. 

# Using the Human class defined above as the base or parent class, we can
# define a child class, Superhero, which inherits the class variables like
# "species", "name", and "age", as well as methods, like "sing" and "grunt"
# from the Human class, but can also have its own unique properties.

# To take advantage of modularization by file you could place the classes above in their own files,
# say, human.py

# To import functions from other files use the following format
# from "filename-without-extension" import "function-or-class"

from human import Human


# Specify the parent class(es) as parameters to the class definition
class Superhero(Human):

    # If the child class should inherit all of the parent's definitions without
    # any modifications, you can just use the "pass" keyword (and nothing else)
    # but in this case it is commented out to allow for a unique child class:
    # pass

    # Child classes can override their parents' attributes
    species = 'Superhuman'

    # Children automatically inherit their parent class's constructor including
    # its arguments, but can also define additional arguments or definitions
    # and override its methods such as the class constructor.
    # This constructor inherits the "name" argument from the "Human" class and
    # adds the "superpower" and "movie" arguments:
    def __init__(self, name, movie=False,
                 superpowers=["super strength", "bulletproofing"]):

        # add additional class attributes:
        self.fictional = True
        self.movie = movie
        # be aware of mutable default values, since defaults are shared
        self.superpowers = superpowers

        # The "super" function lets you access the parent class's methods
        # that are overridden by the child, in this case, the __init__ method.
        # This calls the parent class constructor:
        super().__init__(name)

    # override the sing method
    def sing(self):
        return 'Dun, dun, DUN!'

    # add an additional instance method
    def boast(self):
        for power in self.superpowers:
            print("I wield the power of {pow}!".format(pow=power))


if __name__ == '__main__':
    sup = Superhero(name="Tick")

    # Instance type checks
    if isinstance(sup, Human):
        print('I am human')
    if type(sup) is Superhero:
        print('I am a superhero')

    # Get the Method Resolution search Order used by both getattr() and super()
    # This attribute is dynamic and can be updated
    print(Superhero.__mro__)    # => (<class '__main__.Superhero'>,
                                # => <class 'human.Human'>, <class 'object'>)

    # Calls parent method but uses its own class attribute
    print(sup.get_species())    # => Superhuman

    # Calls overridden method
    print(sup.sing())           # => Dun, dun, DUN!

    # Calls method from Human
    sup.say('Spoon')            # => Tick: Spoon

    # Call method that exists only in Superhero
    sup.boast()                 # => I wield the power of super strength!
                                # => I wield the power of bulletproofing!

    # Inherited class attribute
    sup.age = 31
    print(sup.age)              # => 31

    # Attribute that only exists within Superhero
    print('Am I Oscar eligible? ' + str(sup.movie))
```

### Multiple Inheritance

```python
# Another class definition
# bat.py
class Bat:

    species = 'Baty'

    def __init__(self, can_fly=True):
        self.fly = can_fly

    # This class also has a say method
    def say(self, msg):
        msg = '... ... ...'
        return msg

    # And its own method as well
    def sonar(self):
        return '))) ... ((('

if __name__ == '__main__':
    b = Bat()
    print(b.say('hello'))
    print(b.fly)


# And yet another class definition that inherits from Superhero and Bat
# superhero.py
from superhero import Superhero
from bat import Bat

# Define Batman as a child that inherits from both Superhero and Bat
class Batman(Superhero, Bat):

    def __init__(self, *args, **kwargs):
        # Typically to inherit attributes you have to call super:
        # super(Batman, self).__init__(*args, **kwargs)      
        # However we are dealing with multiple inheritance here, and super()
        # only works with the next base class in the MRO list.
        # So instead we explicitly call __init__ for all ancestors.
        # The use of *args and **kwargs allows for a clean way to pass arguments,
        # with each parent "peeling a layer of the onion".
        Superhero.__init__(self, 'anonymous', movie=True, 
                           superpowers=['Wealthy'], *args, **kwargs)
        Bat.__init__(self, *args, can_fly=False, **kwargs)
        # override the value for the name attribute
        self.name = 'Sad Affleck'

    def sing(self):
        return 'nan nan nan nan nan batman!'


if __name__ == '__main__':
    sup = Batman()

    # Get the Method Resolution search Order used by both getattr() and super().
    # This attribute is dynamic and can be updated
    print(Batman.__mro__)       # => (<class '__main__.Batman'>, 
                                # => <class 'superhero.Superhero'>, 
                                # => <class 'human.Human'>, 
                                # => <class 'bat.Bat'>, <class 'object'>)

    # Calls parent method but uses its own class attribute
    print(sup.get_species())    # => Superhuman

    # Calls overridden method
    print(sup.sing())           # => nan nan nan nan nan batman!

    # Calls method from Human, because inheritance order matters
    sup.say('I agree')          # => Sad Affleck: I agree

    # Call method that exists only in 2nd ancestor
    print(sup.sonar())          # => ))) ... (((

    # Inherited class attribute
    sup.age = 100
    print(sup.age)              # => 100

    # Inherited attribute from 2nd ancestor whose default value was overridden.
    print('Can I fly? ' + str(sup.fly)) # => Can I fly? False
```
-->

## Iterables

<!---
unique_words = set(word  for line in page  for word in line.split())
-->

```python
# Python offers a fundamental abstraction called the Iterable.
# An iterable is an object that can be treated as a sequence.
# The object returned by the range function, is an iterable.

filled_dict = {"one": 1, "two": 2, "three": 3}
our_iterable = filled_dict.keys()
print(our_iterable)  # => dict_keys(['one', 'two', 'three']). This is an object that implements our Iterable interface.

# We can loop over it.
for i in our_iterable:
    print(i)  # Prints one, two, three

# However we cannot address elements by index.
our_iterable[1]  # Raises a TypeError

# An iterable is an object that knows how to create an iterator.
our_iterator = iter(our_iterable)

# Our iterator is an object that can remember the state as we traverse through it.
# We get the next object with "next()".
next(our_iterator)  # => "one"

# It maintains state as we iterate.
next(our_iterator)  # => "two"
next(our_iterator)  # => "three"

# After the iterator has returned all of its data, it raises a StopIteration exception
next(our_iterator)  # Raises StopIteration

# You can grab all the elements of an iterator by calling list() on it.
list(filled_dict.keys())  # => Returns ["one", "two", "three"]

"""
"range(number)" returns an iterable of numbers
from zero to the given number
prints:
    0
    1
    2
    3
"""
for i in range(4):
    print(i)

"""
"range(lower, upper)" returns an iterable of numbers
from the lower number to the upper number
prints:
    4
    5
    6
    7
"""
for i in range(4, 8):
    print(i)

"""
"range(lower, upper, step)" returns an iterable of numbers
from the lower number to the upper number, while incrementing
by step. If step is not indicated, the default value is 1.
prints:
    4
    6
"""
for i in range(4, 8, 2):
    print(i)
```

## Generators

```python
# Generators help you make lazy code.
def double_numbers(iterable):
    for i in iterable:
        yield i + i

# Generators are memory-efficient because they only load the data needed to
# process the next value in the iterable. This allows them to perform
# operations on otherwise prohibitively large value ranges.
# NOTE: `range` replaces `xrange` in Python 3.
for i in double_numbers(range(1, 900000000)):  # `range` is a generator.
    print(i)
    if i >= 30:
        break

# Just as you can create a list comprehension, you can create generator
# comprehensions as well.
values = (-x for x in [1,2,3,4,5])
for x in values:
    print(x)  # prints -1 -2 -3 -4 -5 to console/terminal

# You can also cast a generator comprehension directly to a list.
values = (-x for x in [1,2,3,4,5])
gen_to_list = list(values)
print(gen_to_list)  # => [-1, -2, -3, -4, -5]
```

## Randomness

To generate random numbers, you can use the `random` module (note that PyTorch
provides a separate random numbers functionality).
```python
import random

# random.random() generates numbers uniformly in [0, 1)
[random.random() for _ in range(4)]
```

The `random` module provides in fact *pseudorandom* numbers, that is,
deterministic.  You can use `random.seed` to get the same sequence of random
numbers every time.
```python
random.seed(0)      # Set the seed to 0
random.random()     # => 0.8444218515250481
random.random()     # => 0.7579544029403025
random.seed(0)      # Reset the seed to 0
random.random()     # => 0.8444218515250481
random.random()     # => 0.7579544029403025
```

This property helps to make the experiments replicable.  Unfortunately, this is
currently hard to achieve with PyTorch (setting one seed value is definitely
not enough).

Other functions provided by `random` also may be useful:
```python
# random.shuffle allows to shuffle in place the given list
xs = list(range(5)) # xs is now [0, 1, 2, 3, 4]
random.shuffle(xs)  # xs is now [2, 0, 3, 1, 4] (for instance)

# To randomly pick one element from a list
my_best_friends = ["Bob", "Alice", "Charlie"]
random.choice(my_best_friends)                # => "Bob" for me

# To select a sample of elements *without replacement*
lottery_numbers = range(60)
random.sample(lottery_numbers, 6)             # => [51, 16, 34, 45, 59, 38]

# To select a sample *with replacement* (allowing duplicates),
# just use random.choice
[random.choice(range(4)) for _ in range(6)]  # => [2, 3, 0, 2, 3, 2]
```

## zip and Argument Unpacking

You can *zip* two lists (or iterables) together using the `zip` function.
```python
nums = (1, 2, 3)
strs = ("one", "two", "three")
pairs = list(zip(num_list, str_list))
pairs                               # => [(1, 'one'), (2, 'two'), (3, 'three')]
```

You can also *unzip* two lists using the following trick: 
```python
nums2, strs2 = zip(*pairs)
assert nums == nums2 and strs == strs2
```

The special asterisk operator (\*) performs *argument unpacking*.  In the
example above, `*pairs` unfolds `pairs` to three subsequent arguments: `(1,
'one')`, `(2, 'two')`, and `(3, 'three')`.
```python
assert list(zip(*pairs)) == list(zip((1, 'one'), (2, 'two'), (3, 'three')))
```


## args and kwargs

Argument unpacking is useful if you want to define a function with an unknown
number of arguments.
```python
# You can define functions that take a variable number of
# positional arguments
def varargs(*args):
    return args

varargs(1, 2, 3)  # => (1, 2, 3)

# You can define functions that take a variable number of
# keyword arguments, as well
def keyword_args(**kwargs):
    return kwargs

# Let's call it to see what happens
keyword_args(big="foot", loch="ness")  # => {"big": "foot", "loch": "ness"}

# You can do both at once, if you like
def all_the_args(*args, **kwargs):
    print(args)
    print(kwargs)
"""
all_the_args(1, 2, a=3, b=4) prints:
    (1, 2)
    {"a": 3, "b": 4}
"""

# When calling functions, you can do the opposite of args/kwargs!
# Use * to expand tuples and use ** to expand kwargs.
args = (1, 2, 3, 4)
kwargs = {"a": 3, "b": 4}
all_the_args(*args)            # equivalent to all_the_args(1, 2, 3, 4)
all_the_args(**kwargs)         # equivalent to all_the_args(a=3, b=4)
all_the_args(*args, **kwargs)  # equivalent to all_the_args(1, 2, 3, 4, a=3, b=4)
```

## Type Annotations

Python is a *dynamically typed language*, which means it doesn't care about
types unless we use them wrong.
```python
def add(x, y):
    return x + y

add(2, 2)       # => 4
try:
    add(2, "two")
except TypeError:
    print("Can't add int to a string")
```

However, it is possible to add type annotations in recent versions of Python.
For instance, you can specify that `x`, `y`, and the result all should be
`int`s.
```python
def add(x: int, y: int) -> int:
    return x + y
```

In contrast to statically typed languages, this still doesn't prevent the user
from executing `add(2, "two")`.  However, type annotations help to understand
the code, and they make it possible for the editor (or a code analysis tool) to
catch errors by checking if it respects the types, improve hinting, etc.
```python
# Dot product of two vectors.  Or maybe it takes lists as argumemts too?
def dot_product(x, y): ...

# Dot product of two vectors, returns an int.  Much more readable to me.
def dot_product(x: Vector, y: Vector) -> int: ...
```

PyTorch itself uses type annotations quite extensively.  You don't have to use
them to use PyTorch, but it should help you to understand what's going on.

Having to think about types forces you to design cleaner functions and interfaces.
```python
from typing import Union

# Some ugly function, but you don't know that from the def header
def secretly_ugly_function(value, operation): ...

# Just ugly function, you can immediately see that some refactoring would
# be welcome
def ugly_function(value: int,
                  operation: Union[str, int, float, bool]) -> int:
    ...
# Here the operation is allowed to be a string, int, float, or bool.
# It's likely that it's is difficult to use, but it becomes far more clear
# when the types are made explicit.
```

### How to Write Type Annotations

You can use built in types like int, float, str, list, etc.
```python
def total(xs: list) -> float
    return sum(xs)
```

You can be explicit about the types of objects a particular collection
contains.
```python
from typing import List     # Note capital L

def total(xs: List[float]) -> float:
    return sum(xs)
```

You can also type-annotate variables (in Python 3.6+).
```python
# Somewhat redundant, it's clear that x is an int.
x: int = 5

# Here it's not clear what the type of values is
values = []

# So it may be better to specify it explicitely
values: List[int] = []
```

If a variable can contain `None`, use `Optional`,
```python
from typing import Optional

def maximum(xs: List[int]) -> Optional[int]:
    """Return the maximum element in the list, or None if the list is empty."""
    ... 
```

Finally, there are also types corresponding to most/all the standard
collections available in Python.
```python
# Dictionary which maps integers to strings
int_to_str_dict: Dict[int, str] = {1: "one", 2: "two"}

# Tuples; just use as many types between the square brackets as 
# there are elements in the tuple
int_str_pair: Tuple[int, str] = (1, "one")
int_float_str_pair: Tuple[int, float, str] = (1, 1.0 "one")

# Complex types are also not too hard to define.
complex_dict: Dict[Tuple[str, int], List[int]] = {
    ("one", 1): [1],
    ("two", 2): [1, 2],
    ("thr", 3): [1, 2, 3]
}
```
