---
render_with_liquid: false
title: "Python Built-in Reference: Functions, String, List, Dictionary, Tuple & Set Methods"
nav_order: 44
---

# Lesson 44 — Python Built-in Reference: Functions, Strings, Lists, Dictionaries, Tuples & Sets

---

## Lesson Introduction

Welcome to one of the most **practically powerful** lessons in the entire Python course. Up until now you have been learning *how* Python works. In this lesson you will discover the enormous **toolbox** that Python already provides for you — ready to use, no installation needed.

Think of Python's built-in functions and methods like the buttons on a professional kitchen appliance. You do not need to know *how* the motor works — you just need to know *which button does what* and *when to press it*.

This lesson covers **six major reference areas** in Python:

1. **Python Built-in Functions** — tools available everywhere in Python without importing anything
2. **String Methods** — tools for working with text
3. **List Methods** — tools for working with ordered, changeable collections
4. **Dictionary Methods** — tools for working with key-value pairs
5. **Tuple Methods** — tools for working with ordered, unchangeable sequences
6. **Set Methods** — tools for working with unique, unordered collections

By the end, you will be able to use Python's full toolkit to process text, numbers, lists, and data structures confidently.

---

## Prerequisites: What You Should Already Know

Before diving in, make sure you are comfortable with these concepts. If not, a brief recap is provided below.

**What is a function?**
A function is a named block of reusable code. You "call" it by writing its name followed by parentheses. Some functions need information sent inside the parentheses — these are called **arguments** or **parameters**.

```python
# Calling a function:
print("Hello")       # print is a function; "Hello" is the argument
result = len("Hi")   # len is a function; it gives back (returns) a value
print(result)        # Output: 2
```

**What is a method?**
A method is a function that belongs to a specific data type. You call it using a dot (`.`) after the value or variable.

```python
# Calling a method:
name = "alice"
print(name.upper())  # upper() is a method belonging to strings
# Output: ALICE
```

**What is a return value?**
When a function or method finishes its work, it can send a result back. This result is called the **return value**. You can store it in a variable.

```python
total = sum([1, 2, 3])  # sum() returns 6
print(total)            # Output: 6
```

---

## Part 1 — Python Built-in Functions

### What Are Built-in Functions?

Python ships with a set of **built-in functions** that are always available. You do not need to import any library. Just call them by name.

> **Analogy:** Built-in functions are like the tools that come pre-installed on your computer — File Explorer, Calculator, Notepad. They are there from day one, no download required.

Python has **71 built-in functions**. This lesson teaches you the most essential and commonly used ones, grouped by purpose.

---

### Group 1: Type Conversion Functions

These functions convert one data type into another.

#### `int()` — Convert to Integer

**What it is:** Converts a value into a whole number (integer). Removes any decimal part.

**Why it exists:** When you read a number from the user or a file, it arrives as a string like `"42"`. Before doing math with it, you must convert it.

```python
# Example 1 — Convert a string to integer
x = int("42")
print(x)        # Output: 42
print(type(x))  # Output: <class 'int'>

# Example 2 — Convert a float to integer (chops off decimal)
y = int(3.9)
print(y)        # Output: 3   ← NOT rounded, just truncated
```

> **Common Mistake:** `int("3.9")` will CRASH. You must first convert `"3.9"` to float, then to int.

```python
# WRONG:
# x = int("3.9")   # ValueError!

# CORRECT:
x = int(float("3.9"))
print(x)  # Output: 3
```

---

#### `float()` — Convert to Decimal Number

**What it is:** Converts a value into a decimal (floating-point) number.

```python
# Example 1
a = float("3.14")
print(a)        # Output: 3.14

# Example 2
b = float(5)
print(b)        # Output: 5.0
```

---

#### `str()` — Convert to String (Text)

**What it is:** Converts any value into its text representation.

**Why it exists:** You cannot join a number and a string using `+` without converting first.

```python
# WRONG:
# print("Your score is: " + 95)   # TypeError!

# CORRECT:
score = 95
print("Your score is: " + str(score))  # Output: Your score is: 95
```

---

#### `bool()` — Convert to True or False

**What it is:** Converts a value to `True` or `False`.

**Rule:** Most things in Python are `True`. The following are `False`: `0`, `""` (empty string), `[]` (empty list), `{}` (empty dict), `None`.

```python
print(bool(1))      # Output: True
print(bool(0))      # Output: False
print(bool("hi"))   # Output: True
print(bool(""))     # Output: False
print(bool([]))     # Output: False
```

> **Thinking Prompt:** What do you think `bool(0.0)` outputs? Why?

---

#### `list()` — Convert to List

**What it is:** Converts an iterable (anything you can loop over) into a list.

```python
# Convert a string into a list of characters
letters = list("hello")
print(letters)  # Output: ['h', 'e', 'l', 'l', 'o']

# Convert a range into a list
nums = list(range(5))
print(nums)  # Output: [0, 1, 2, 3, 4]
```

---

#### `tuple()` — Convert to Tuple

```python
t = tuple([1, 2, 3])
print(t)   # Output: (1, 2, 3)
```

---

#### `set()` — Convert to Set (removes duplicates!)

```python
s = set([1, 2, 2, 3, 3, 3])
print(s)   # Output: {1, 2, 3}  ← duplicates removed
```

---

#### `dict()` — Create a Dictionary

```python
d = dict(name="Alice", age=25)
print(d)   # Output: {'name': 'Alice', 'age': 25}
```

---

### Group 2: Math & Number Functions

#### `abs()` — Absolute Value

**What it is:** Returns the positive version of any number (removes the minus sign).

**Real-world use:** Calculating the distance between two temperatures, prices, or coordinates — distance is always positive.

```python
print(abs(-5))    # Output: 5
print(abs(3.7))   # Output: 3.7
print(abs(-100))  # Output: 100
```

---

#### `round()` — Round a Number

**What it is:** Rounds a decimal to a specified number of digits.

```python
# Basic rounding
print(round(3.7))      # Output: 4
print(round(3.2))      # Output: 3

# Round to 2 decimal places
print(round(3.14159, 2))  # Output: 3.14

# Round to nearest 10
print(round(156, -1))     # Output: 160
```

> **Banker's Rounding:** Python uses "round half to even" — `round(2.5)` gives `2`, not `3`. This surprises many beginners!

```python
print(round(2.5))   # Output: 2  (rounds to nearest even)
print(round(3.5))   # Output: 4  (rounds to nearest even)
```

---

#### `max()` — Find the Largest Value

```python
print(max(3, 7, 1, 9, 4))          # Output: 9
print(max([10, 20, 30]))            # Output: 30
print(max("apple", "banana", "cherry"))  # Output: cherry  (alphabetical)
```

---

#### `min()` — Find the Smallest Value

```python
print(min(3, 7, 1, 9, 4))   # Output: 1
print(min([10, 20, 30]))     # Output: 10
```

---

#### `sum()` — Add All Items Together

```python
grades = [85, 90, 78, 92]
total = sum(grades)
print(total)         # Output: 345

# With a starting value
print(sum([1, 2, 3], 10))  # Output: 16  (10 + 1 + 2 + 3)
```

---

#### `pow()` — Power (Exponent)

**What it is:** Raises a number to the power of another number. `pow(2, 3)` means 2³ = 8.

```python
print(pow(2, 3))    # Output: 8
print(pow(5, 2))    # Output: 25
print(pow(2, 10))   # Output: 1024

# Optional third argument: modulo
print(pow(2, 10, 100))  # Output: 24  (1024 % 100)
```

---

#### `divmod()` — Division with Remainder

**What it is:** Returns BOTH the quotient and the remainder as a tuple. Useful when dividing items into groups.

```python
quotient, remainder = divmod(17, 5)
print(quotient)    # Output: 3   (17 ÷ 5 = 3 groups)
print(remainder)   # Output: 2   (2 left over)

# Real-world: How many weeks and days in 25 days?
weeks, days = divmod(25, 7)
print(f"{weeks} weeks and {days} days")  # Output: 3 weeks and 4 days
```

---

### Group 3: Sequence & Collection Functions

#### `len()` — Count Items

**What it is:** Returns the number of items in a string, list, tuple, set, or dictionary.

```python
print(len("hello"))         # Output: 5   (5 characters)
print(len([1, 2, 3, 4]))    # Output: 4   (4 items)
print(len({"a": 1, "b": 2}))  # Output: 2   (2 key-value pairs)
```

---

#### `range()` — Generate a Sequence of Numbers

**What it is:** Produces a sequence of numbers. Commonly used in `for` loops.

```python
# range(stop)
for i in range(5):
    print(i, end=" ")  # Output: 0 1 2 3 4

print()  # new line

# range(start, stop)
for i in range(2, 6):
    print(i, end=" ")  # Output: 2 3 4 5

print()

# range(start, stop, step)
for i in range(0, 10, 2):
    print(i, end=" ")  # Output: 0 2 4 6 8
```

> **Key Rule:** `range()` never includes the stop number. `range(5)` gives 0, 1, 2, 3, 4 — not 5.

---

#### `sorted()` — Sort Without Changing Original

**What it is:** Returns a new sorted list without modifying the original collection.

```python
numbers = [3, 1, 4, 1, 5, 9, 2]
sorted_nums = sorted(numbers)
print(sorted_nums)   # Output: [1, 1, 2, 3, 4, 5, 9]
print(numbers)       # Output: [3, 1, 4, 1, 5, 9, 2]  ← unchanged!

# Sort in reverse
print(sorted(numbers, reverse=True))  # Output: [9, 5, 4, 3, 2, 1, 1]

# Sort strings
words = ["banana", "apple", "cherry"]
print(sorted(words))  # Output: ['apple', 'banana', 'cherry']
```

---

#### `reversed()` — Reverse an Iterable

```python
nums = [1, 2, 3, 4, 5]
for n in reversed(nums):
    print(n, end=" ")  # Output: 5 4 3 2 1

# Convert to list
print(list(reversed([10, 20, 30])))  # Output: [30, 20, 10]
```

---

#### `enumerate()` — Loop with Index

**What it is:** When looping through a list, `enumerate()` gives you both the index number and the item. This avoids needing a separate counter variable.

```python
fruits = ["apple", "banana", "cherry"]

# Without enumerate (tedious)
i = 0
for fruit in fruits:
    print(i, fruit)
    i += 1

# With enumerate (clean!)
for index, fruit in enumerate(fruits):
    print(index, fruit)
# Output:
# 0 apple
# 1 banana
# 2 cherry

# Start index at 1
for index, fruit in enumerate(fruits, start=1):
    print(index, fruit)
# Output:
# 1 apple
# 2 banana
# 3 cherry
```

---

#### `zip()` — Combine Two Lists Together

**What it is:** Pairs up items from two (or more) lists at the same position, like a zipper.

```python
names = ["Alice", "Bob", "Carol"]
scores = [85, 92, 78]

for name, score in zip(names, scores):
    print(f"{name}: {score}")
# Output:
# Alice: 85
# Bob: 92
# Carol: 78
```

---

#### `filter()` — Keep Only Matching Items

**What it is:** Applies a function to each item in a list, keeping only the items where the function returns `True`.

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

def is_even(n):
    return n % 2 == 0

evens = list(filter(is_even, numbers))
print(evens)  # Output: [2, 4, 6, 8, 10]
```

---

#### `map()` — Transform Every Item

**What it is:** Applies a function to every item and returns the transformed results.

```python
numbers = [1, 2, 3, 4, 5]

def square(n):
    return n * n

squared = list(map(square, numbers))
print(squared)  # Output: [1, 4, 9, 16, 25]
```

---

### Group 4: Input/Output Functions

#### `print()` — Display Output

**What it is:** Displays values to the screen. The most fundamental function in Python.

```python
# Basic print
print("Hello, World!")           # Output: Hello, World!

# Print multiple items
print("Name:", "Alice", "Age:", 25)  # Output: Name: Alice Age: 25

# Custom separator
print("A", "B", "C", sep="-")   # Output: A-B-C

# Custom end character (default is newline \n)
print("Hello", end=" ")
print("World")                   # Output: Hello World  (same line)

# Print nothing (blank line)
print()
```

---

#### `input()` — Get Text from the User

**What it is:** Pauses the program and waits for the user to type something. Always returns a **string**.

```python
name = input("Enter your name: ")
print("Hello, " + name + "!")

# Getting a number from user — must convert!
age = int(input("Enter your age: "))
print("You will be", age + 1, "next year")
```

---

### Group 5: Inspection & Type Functions

#### `type()` — Check the Type of a Value

```python
print(type(42))        # Output: <class 'int'>
print(type(3.14))      # Output: <class 'float'>
print(type("hello"))   # Output: <class 'str'>
print(type([1, 2]))    # Output: <class 'list'>
print(type(True))      # Output: <class 'bool'>
```

---

#### `isinstance()` — Check If a Value Is a Certain Type

**What it is:** Returns `True` if the value is an instance of the specified type.

```python
print(isinstance(42, int))     # Output: True
print(isinstance(42, float))   # Output: False
print(isinstance("hi", str))   # Output: True

# Check multiple types at once
print(isinstance(42, (int, float)))   # Output: True
```

---

#### `id()` — Get the Memory Address

**What it is:** Returns a unique identifier for an object in memory. Useful for understanding whether two variables point to the same object.

```python
a = [1, 2, 3]
b = a           # b points to the SAME list
c = [1, 2, 3]   # c is a NEW list

print(id(a) == id(b))   # Output: True  (same object)
print(id(a) == id(c))   # Output: False (different objects)
```

---

#### `dir()` — List All Methods of an Object

**What it is:** Returns a list of all attributes and methods that belong to an object. This is like opening a menu to see what tools are available.

```python
print(dir("hello"))   # Shows all string methods!
```

---

#### `help()` — Read Documentation

**What it is:** Opens interactive documentation for any function, method, or module.

```python
help(print)    # Shows documentation for print()
help(str)      # Shows all string methods and their docs
```

---

### Group 6: Logic & Checking Functions

#### `all()` — Are All Items True?

```python
print(all([True, True, True]))    # Output: True
print(all([True, False, True]))   # Output: False
print(all([1, 2, 3]))             # Output: True  (all non-zero)
print(all([1, 0, 3]))             # Output: False (0 is falsy)

# Real use: check all grades pass
grades = [75, 80, 65, 90]
print(all(g >= 50 for g in grades))  # Output: True
```

---

#### `any()` — Is At Least One Item True?

```python
print(any([False, False, True]))   # Output: True
print(any([False, False, False]))  # Output: False

# Real use: did anyone fail?
grades = [75, 80, 40, 90]
print(any(g < 50 for g in grades))  # Output: True (40 failed)
```

---

#### `hex()`, `oct()`, `bin()` — Number Base Conversions

```python
# Decimal to hexadecimal (base 16)
print(hex(255))   # Output: 0xff

# Decimal to octal (base 8)
print(oct(8))     # Output: 0o10

# Decimal to binary (base 2)
print(bin(10))    # Output: 0b1010
```

---

#### `chr()` and `ord()` — Characters and Unicode Numbers

**What they are:** `ord()` converts a character to its Unicode number; `chr()` does the reverse.

```python
print(ord("A"))    # Output: 65
print(ord("a"))    # Output: 97
print(chr(65))     # Output: A
print(chr(97))     # Output: a

# Check if two cases differ by 32
print(ord("a") - ord("A"))  # Output: 32
```

---

#### `open()` — Open a File

```python
# Writing to a file
file = open("test.txt", "w")
file.write("Hello from Python!")
file.close()

# Reading from a file
file = open("test.txt", "r")
content = file.read()
print(content)   # Output: Hello from Python!
file.close()
```

---

### Complete Built-in Functions Quick Reference Table

| Function | Purpose | Simple Example |
|---|---|---|
| `abs(x)` | Absolute value | `abs(-5)` → `5` |
| `all(iter)` | True if all items truthy | `all([1,2,3])` → `True` |
| `any(iter)` | True if any item truthy | `any([0,1,0])` → `True` |
| `bin(x)` | Integer to binary string | `bin(10)` → `'0b1010'` |
| `bool(x)` | Convert to boolean | `bool(0)` → `False` |
| `callable(x)` | True if x can be called | `callable(print)` → `True` |
| `chr(i)` | Unicode to character | `chr(65)` → `'A'` |
| `compile(...)` | Compile source to code object | Advanced |
| `complex(r,i)` | Create complex number | `complex(2,3)` → `(2+3j)` |
| `delattr(obj,n)` | Delete attribute | OOP use |
| `dict(...)` | Create dictionary | `dict(a=1)` → `{'a':1}` |
| `dir(obj)` | List object's attributes | `dir("hi")` → list of methods |
| `divmod(a,b)` | Quotient and remainder | `divmod(7,3)` → `(2,1)` |
| `enumerate(iter)` | Index + item pairs | `enumerate(['a','b'])` |
| `eval(str)` | Evaluate expression string | `eval("2+2")` → `4` |
| `exec(code)` | Execute code string | Advanced |
| `filter(fn,iter)` | Filter by function | `filter(is_even, nums)` |
| `float(x)` | Convert to float | `float("3.5")` → `3.5` |
| `format(v,spec)` | Format a value | `format(3.14159, '.2f')` → `'3.14'` |
| `frozenset(iter)` | Immutable set | `frozenset([1,2,3])` |
| `getattr(obj,n)` | Get object attribute | OOP use |
| `globals()` | Global variable dictionary | Advanced |
| `hasattr(obj,n)` | Check if attribute exists | OOP use |
| `hash(obj)` | Hash value of object | `hash("hello")` → integer |
| `help(obj)` | Show documentation | `help(print)` |
| `hex(x)` | Integer to hex string | `hex(255)` → `'0xff'` |
| `id(obj)` | Memory address | `id(x)` → integer |
| `input(prompt)` | Get user input | `input("Name: ")` |
| `int(x)` | Convert to integer | `int("42")` → `42` |
| `isinstance(o,t)` | Check type | `isinstance(5,int)` → `True` |
| `issubclass(c,t)` | Check class hierarchy | OOP use |
| `iter(obj)` | Create iterator | `iter([1,2,3])` |
| `len(obj)` | Length/count | `len("hello")` → `5` |
| `list(iter)` | Create list | `list("abc")` → `['a','b','c']` |
| `locals()` | Local variable dictionary | Advanced |
| `map(fn,iter)` | Apply function to each item | `map(str, [1,2,3])` |
| `max(iter)` | Largest value | `max([1,5,3])` → `5` |
| `min(iter)` | Smallest value | `min([1,5,3])` → `1` |
| `next(iter)` | Next item from iterator | `next(iter([1,2,3]))` → `1` |
| `object()` | Base object | OOP use |
| `oct(x)` | Integer to octal | `oct(8)` → `'0o10'` |
| `open(file)` | Open a file | `open("data.txt","r")` |
| `ord(c)` | Character to Unicode number | `ord('A')` → `65` |
| `pow(x,y)` | x to the power y | `pow(2,3)` → `8` |
| `print(...)` | Display output | `print("hello")` |
| `range(...)` | Generate number sequence | `range(5)` → `0,1,2,3,4` |
| `repr(obj)` | Printable representation | `repr("hi")` → `"'hi'"` |
| `reversed(seq)` | Reverse iterator | `list(reversed([1,2,3]))` |
| `round(n,d)` | Round number | `round(3.14,1)` → `3.1` |
| `set(iter)` | Create set | `set([1,1,2])` → `{1,2}` |
| `setattr(o,n,v)` | Set attribute | OOP use |
| `slice(...)` | Create slice object | Advanced |
| `sorted(iter)` | Sorted list copy | `sorted([3,1,2])` → `[1,2,3]` |
| `str(x)` | Convert to string | `str(42)` → `'42'` |
| `sum(iter)` | Sum of items | `sum([1,2,3])` → `6` |
| `super()` | Call parent class | OOP use |
| `tuple(iter)` | Create tuple | `tuple([1,2])` → `(1,2)` |
| `type(obj)` | Type of object | `type(42)` → `<class 'int'>` |
| `vars(obj)` | Object's `__dict__` | OOP use |
| `zip(a,b)` | Pair items from iterables | `zip([1,2],['a','b'])` |

---

## Part 2 — Python String Methods

### What Are String Methods?

A **string** is any text enclosed in quotes. Python strings come with **47 built-in methods** that you can use to inspect, transform, clean, and format text.

> **Important Rule:** All string methods return a **new string**. They do NOT change the original string. Strings are *immutable* — they cannot be modified in place.

```python
original = "Hello World"
modified = original.lower()
print(original)   # Output: Hello World  ← unchanged!
print(modified)   # Output: hello world
```

---

### Case Methods — Changing Letter Case

#### `upper()` — Convert All to Uppercase

```python
text = "hello world"
print(text.upper())   # Output: HELLO WORLD
```

#### `lower()` — Convert All to Lowercase

```python
text = "PYTHON IS FUN"
print(text.lower())   # Output: python is fun
```

#### `capitalize()` — Capitalize First Letter Only

```python
text = "hello world"
print(text.capitalize())   # Output: Hello world
```

#### `title()` — Capitalize First Letter of Each Word

```python
text = "the quick brown fox"
print(text.title())   # Output: The Quick Brown Fox
```

#### `swapcase()` — Flip All Cases

```python
text = "Hello World"
print(text.swapcase())   # Output: hELLO wORLD
```

#### `casefold()` — Aggressive Lowercase (for comparisons)

**Why it exists:** `lower()` is not always sufficient for comparing international text. `casefold()` applies a more aggressive form of lowercasing, especially for languages like German (ß → ss).

```python
print("ß".lower())      # Output: ß
print("ß".casefold())   # Output: ss
```

---

### Search & Check Methods

#### `find()` — Find Position of a Substring

**What it returns:** The index (position) of the first match, or `-1` if not found.

```python
text = "I love Python and I love coding"
print(text.find("love"))     # Output: 2   (first occurrence)
print(text.find("Java"))     # Output: -1  (not found)
print(text.find("love", 5))  # Output: 19  (search from position 5)
```

#### `rfind()` — Find Last Occurrence

```python
text = "apple banana apple"
print(text.rfind("apple"))   # Output: 13  (last occurrence)
```

#### `index()` — Like find(), but Raises Error if Not Found

```python
text = "Hello World"
print(text.index("World"))   # Output: 6

# text.index("Python")  # Would raise: ValueError
```

#### `count()` — Count How Many Times Something Appears

```python
text = "banana"
print(text.count("a"))    # Output: 3
print(text.count("an"))   # Output: 2
print(text.count("xyz"))  # Output: 0
```

#### `startswith()` — Does the String Begin With This?

```python
url = "https://www.example.com"
print(url.startswith("https"))   # Output: True
print(url.startswith("http://")) # Output: False

# Check multiple prefixes using a tuple
filename = "report.pdf"
print(filename.startswith(("report", "summary")))  # Output: True
```

#### `endswith()` — Does the String End With This?

```python
filename = "data_report.csv"
print(filename.endswith(".csv"))   # Output: True
print(filename.endswith(".xlsx"))  # Output: False
```

---

### Cleaning Methods — Removing Whitespace

#### `strip()` — Remove Leading and Trailing Whitespace

**Real-world use:** User input often has accidental spaces. Always strip before using.

```python
user_input = "   Alice   "
print(user_input.strip())    # Output: Alice

# Strip specific characters
text = "###Hello###"
print(text.strip("#"))       # Output: Hello
```

#### `lstrip()` — Remove Left (Leading) Whitespace Only

```python
text = "   Hello"
print(text.lstrip())   # Output: Hello  (right spaces kept if any)
```

#### `rstrip()` — Remove Right (Trailing) Whitespace Only

```python
text = "Hello   "
print(text.rstrip())   # Output: Hello
```

---

### Replacing & Splitting Methods

#### `replace()` — Swap One Value for Another

```python
text = "I love cats. Cats are great."
new = text.replace("cats", "dogs")
print(new)   # Output: I love dogs. Cats are great.
# Note: replace() is case-sensitive! "Cats" was NOT replaced.

# Replace all occurrences
new2 = text.replace("cats", "dogs").replace("Cats", "Dogs")
print(new2)  # Output: I love dogs. Dogs are great.

# Limit replacements
text2 = "aaa"
print(text2.replace("a", "b", 2))  # Output: bba  (only first 2 replaced)
```

#### `split()` — Split into a List

**What it does:** Breaks a string into a list of smaller strings at a separator character.

```python
text = "apple,banana,cherry"
parts = text.split(",")
print(parts)   # Output: ['apple', 'banana', 'cherry']

# Split by space (default)
sentence = "The quick brown fox"
words = sentence.split()
print(words)   # Output: ['The', 'quick', 'brown', 'fox']

# Limit splits
print("a:b:c:d".split(":", 2))  # Output: ['a', 'b', 'c:d']
```

#### `rsplit()` — Split from the Right

```python
text = "a:b:c:d"
print(text.rsplit(":", 2))   # Output: ['a:b', 'c', 'd']
```

#### `splitlines()` — Split at Line Breaks

```python
poem = "Roses are red\nViolets are blue\nPython is great"
lines = poem.splitlines()
print(lines)
# Output: ['Roses are red', 'Violets are blue', 'Python is great']
```

#### `join()` — Combine a List into a String

**What it does:** The opposite of `split()`. Joins a list of strings using a separator.

```python
words = ["apple", "banana", "cherry"]
result = ", ".join(words)
print(result)   # Output: apple, banana, cherry

# Join with no separator
letters = ["H", "e", "l", "l", "o"]
print("".join(letters))   # Output: Hello

# Join path parts
path_parts = ["home", "user", "documents"]
print("/".join(path_parts))   # Output: home/user/documents
```

---

### Formatting & Alignment Methods

#### `center()` — Center the String

```python
title = "Python"
print(title.center(20))         # Output:        Python       
print(title.center(20, "*"))    # Output: *******Python*******
```

#### `ljust()` — Left Justify (Pad Right)

```python
name = "Alice"
print(name.ljust(10) + "|")    # Output: Alice     |
print(name.ljust(10, ".") + "|")  # Output: Alice.....|
```

#### `rjust()` — Right Justify (Pad Left)

```python
name = "Alice"
print(name.rjust(10) + "|")    # Output:      Alice|
```

#### `zfill()` — Pad with Zeros

**Real-world use:** Formatting order numbers, roll numbers, IDs.

```python
print("42".zfill(6))      # Output: 000042
print("1234".zfill(6))    # Output: 001234
print("-42".zfill(6))     # Output: -00042  (sign preserved)
```

#### `format()` — Insert Values into a Template

```python
template = "Hello, {}! You scored {}%."
print(template.format("Alice", 95))
# Output: Hello, Alice! You scored 95%.

# Named placeholders
template2 = "Name: {name}, Age: {age}"
print(template2.format(name="Bob", age=30))
# Output: Name: Bob, Age: 30

# Number formatting
print("{:.2f}".format(3.14159))   # Output: 3.14
print("{:>10}".format("right"))   # Output:      right
print("{:<10}".format("left"))    # Output: left      
```

---

### Checking/Validation Methods

All these return `True` or `False` and are useful for validating input.

#### `isalpha()` — Only Letters?

```python
print("Hello".isalpha())    # Output: True
print("Hello2".isalpha())   # Output: False  (has digit)
print("".isalpha())         # Output: False  (empty)
```

#### `isdigit()` — Only Digits?

```python
print("123".isdigit())      # Output: True
print("12.3".isdigit())     # Output: False  (has dot)
print("123abc".isdigit())   # Output: False
```

#### `isalnum()` — Letters or Digits Only?

```python
print("Hello123".isalnum())   # Output: True
print("Hello 123".isalnum())  # Output: False  (space is not alnum)
```

#### `isspace()` — Only Whitespace?

```python
print("   ".isspace())    # Output: True
print("   a".isspace())   # Output: False
```

#### `isupper()` / `islower()` — All Uppercase / Lowercase?

```python
print("HELLO".isupper())   # Output: True
print("hello".islower())   # Output: True
print("Hello".isupper())   # Output: False
```

#### `istitle()` — Title Case?

```python
print("The Quick Brown Fox".istitle())   # Output: True
print("The quick Brown Fox".istitle())   # Output: False
```

#### `isnumeric()` — Numeric Characters?

**More inclusive than `isdigit()`** — includes fractions, superscripts, etc.

```python
print("123".isnumeric())    # Output: True
print("½".isnumeric())      # Output: True  (fraction character)
print("12.3".isnumeric())   # Output: False
```

#### `isdecimal()` — Strict Decimal Digits Only?

```python
print("123".isdecimal())    # Output: True
print("½".isdecimal())      # Output: False
```

---

### String Methods Quick Reference Table

| Method | Purpose | Example |
|---|---|---|
| `capitalize()` | First letter upper | `"hi".capitalize()` → `'Hi'` |
| `casefold()` | Aggressive lowercase | `"ß".casefold()` → `'ss'` |
| `center(w)` | Center in width | `"hi".center(10)` → `'    hi    '` |
| `count(sub)` | Count occurrences | `"aaa".count("a")` → `3` |
| `encode()` | Encode string | `"hi".encode()` → `b'hi'` |
| `endswith(s)` | Ends with string? | `"hi.py".endswith(".py")` → `True` |
| `expandtabs(n)` | Set tab size | `"a\tb".expandtabs(4)` |
| `find(sub)` | Find index or -1 | `"hello".find("l")` → `2` |
| `format(...)` | Format string | `"{} {}".format("Hi","!")` |
| `format_map(d)` | Format from dict | `"{name}".format_map({'name':'Al'})` |
| `index(sub)` | Find index or error | `"hello".index("l")` → `2` |
| `isalnum()` | Letters/digits only? | `"abc1".isalnum()` → `True` |
| `isalpha()` | Letters only? | `"abc".isalpha()` → `True` |
| `isascii()` | ASCII only? | `"abc".isascii()` → `True` |
| `isdecimal()` | Strict decimal? | `"123".isdecimal()` → `True` |
| `isdigit()` | Digits only? | `"123".isdigit()` → `True` |
| `isidentifier()` | Valid variable name? | `"my_var".isidentifier()` → `True` |
| `islower()` | All lowercase? | `"hi".islower()` → `True` |
| `isnumeric()` | Numeric chars? | `"½".isnumeric()` → `True` |
| `isprintable()` | All printable? | `"hi".isprintable()` → `True` |
| `isspace()` | Whitespace only? | `"   ".isspace()` → `True` |
| `istitle()` | Title case? | `"Hi There".istitle()` → `True` |
| `isupper()` | All uppercase? | `"HI".isupper()` → `True` |
| `join(iter)` | Join list to string | `",".join(["a","b"])` → `'a,b'` |
| `ljust(w)` | Left justify | `"hi".ljust(5)` → `'hi   '` |
| `lower()` | All lowercase | `"HI".lower()` → `'hi'` |
| `lstrip()` | Strip left spaces | `"  hi".lstrip()` → `'hi'` |
| `maketrans()` | Translation table | Advanced |
| `partition(s)` | Split into 3 parts | `"a:b:c".partition(":")` → `('a',':','b:c')` |
| `replace(a,b)` | Replace substring | `"hi".replace("h","b")` → `'bi'` |
| `rfind(sub)` | Last index or -1 | `"abab".rfind("b")` → `3` |
| `rindex(sub)` | Last index or error | `"abab".rindex("b")` → `3` |
| `rjust(w)` | Right justify | `"hi".rjust(5)` → `'   hi'` |
| `rpartition(s)` | Partition from right | `"a:b:c".rpartition(":")` → `('a:b',':','c')` |
| `rsplit(s)` | Split from right | `"a:b:c".rsplit(":",1)` → `['a:b','c']` |
| `rstrip()` | Strip right spaces | `"hi  ".rstrip()` → `'hi'` |
| `split(s)` | Split to list | `"a,b".split(",")` → `['a','b']` |
| `splitlines()` | Split at newlines | `"a\nb".splitlines()` → `['a','b']` |
| `startswith(s)` | Starts with string? | `"hi".startswith("h")` → `True` |
| `strip()` | Strip both sides | `"  hi  ".strip()` → `'hi'` |
| `swapcase()` | Swap upper/lower | `"Hi".swapcase()` → `'hI'` |
| `title()` | Title case | `"hello world".title()` → `'Hello World'` |
| `translate(t)` | Translate chars | Advanced |
| `upper()` | All uppercase | `"hi".upper()` → `'HI'` |
| `zfill(w)` | Zero-pad | `"42".zfill(5)` → `'00042'` |

---

## Part 3 — Python List Methods

### What Are Lists?

A **list** is an ordered, changeable (mutable) collection of items. Lists can hold any data type — numbers, strings, other lists, etc.

```python
fruits = ["apple", "banana", "cherry"]
numbers = [1, 2, 3, 4, 5]
mixed = [1, "hello", True, 3.14]
```

Lists have **11 built-in methods** for adding, removing, finding, and organising items.

---

### Adding Items

#### `append()` — Add One Item to the End

```python
fruits = ["apple", "banana"]
fruits.append("cherry")
print(fruits)   # Output: ['apple', 'banana', 'cherry']
```

#### `insert()` — Add Item at a Specific Position

```python
fruits = ["apple", "cherry"]
fruits.insert(1, "banana")   # Insert at index 1
print(fruits)   # Output: ['apple', 'banana', 'cherry']
```

#### `extend()` — Add All Items from Another List

```python
fruits = ["apple", "banana"]
more_fruits = ["cherry", "date"]
fruits.extend(more_fruits)
print(fruits)   # Output: ['apple', 'banana', 'cherry', 'date']

# DIFFERENCE from append():
# fruits.append(more_fruits) would give: ['apple', 'banana', ['cherry', 'date']]
```

---

### Removing Items

#### `remove()` — Remove First Occurrence by Value

```python
fruits = ["apple", "banana", "apple", "cherry"]
fruits.remove("apple")        # Removes FIRST "apple" only
print(fruits)   # Output: ['banana', 'apple', 'cherry']
```

> **Common Mistake:** If the value does not exist, `remove()` raises a `ValueError`. Check first!

```python
if "mango" in fruits:
    fruits.remove("mango")
```

#### `pop()` — Remove and Return Item by Index

**What it does:** Removes the item at the given index AND returns it. If no index given, removes the last item.

```python
fruits = ["apple", "banana", "cherry"]
removed = fruits.pop()    # Remove last
print(removed)   # Output: cherry
print(fruits)    # Output: ['apple', 'banana']

removed2 = fruits.pop(0)  # Remove first
print(removed2)  # Output: apple
print(fruits)    # Output: ['banana']
```

#### `clear()` — Remove All Items

```python
fruits = ["apple", "banana", "cherry"]
fruits.clear()
print(fruits)   # Output: []
```

---

### Finding Items

#### `index()` — Find Position of First Occurrence

```python
fruits = ["apple", "banana", "cherry", "banana"]
print(fruits.index("banana"))   # Output: 1  (first occurrence)

# Search within a range
print(fruits.index("banana", 2))  # Output: 3  (search from index 2)
```

#### `count()` — Count Occurrences of a Value

```python
numbers = [1, 2, 3, 2, 4, 2]
print(numbers.count(2))   # Output: 3
print(numbers.count(5))   # Output: 0
```

---

### Ordering Items

#### `sort()` — Sort in Place (Changes Original!)

```python
numbers = [3, 1, 4, 1, 5, 9, 2]
numbers.sort()
print(numbers)   # Output: [1, 1, 2, 3, 4, 5, 9]

# Reverse sort
numbers.sort(reverse=True)
print(numbers)   # Output: [9, 5, 4, 3, 2, 1, 1]

# Sort strings
words = ["banana", "apple", "cherry"]
words.sort()
print(words)    # Output: ['apple', 'banana', 'cherry']
```

> **`sort()` vs `sorted()`:**
> - `list.sort()` — modifies the list in place, returns `None`
> - `sorted(list)` — returns a NEW list, original unchanged

```python
nums = [3, 1, 2]
result = nums.sort()
print(result)  # Output: None  ← not a list!

nums2 = [3, 1, 2]
result2 = sorted(nums2)
print(result2)  # Output: [1, 2, 3]  ← new list
```

#### `reverse()` — Reverse Order in Place

```python
fruits = ["apple", "banana", "cherry"]
fruits.reverse()
print(fruits)   # Output: ['cherry', 'banana', 'apple']
```

---

### Copying

#### `copy()` — Make a Shallow Copy

**Why this matters:** If you do `b = a`, both `a` and `b` point to the **same list**. Changing one changes the other. `copy()` creates an independent copy.

```python
original = [1, 2, 3]

# WRONG WAY (linked):
copy1 = original
copy1.append(4)
print(original)   # Output: [1, 2, 3, 4]  ← original changed!

# CORRECT WAY:
original2 = [1, 2, 3]
copy2 = original2.copy()
copy2.append(4)
print(original2)  # Output: [1, 2, 3]  ← unchanged!
print(copy2)      # Output: [1, 2, 3, 4]
```

---

### List Methods Quick Reference Table

| Method | Purpose | Example |
|---|---|---|
| `append(x)` | Add item to end | `lst.append(5)` |
| `clear()` | Remove all items | `lst.clear()` |
| `copy()` | Shallow copy | `new = lst.copy()` |
| `count(x)` | Count occurrences | `lst.count(2)` → `3` |
| `extend(iter)` | Add all items from iterable | `lst.extend([4,5])` |
| `index(x)` | Find index of first match | `lst.index("a")` → `0` |
| `insert(i,x)` | Insert at position | `lst.insert(1,"b")` |
| `pop(i)` | Remove & return item | `lst.pop()` → last item |
| `remove(x)` | Remove first match | `lst.remove("a")` |
| `reverse()` | Reverse in place | `lst.reverse()` |
| `sort()` | Sort in place | `lst.sort()` |

---

## Part 4 — Python Dictionary Methods

### What Are Dictionaries?

A **dictionary** stores data as **key-value pairs**. Think of it like a real dictionary — you look up a word (key) to find its definition (value).

```python
student = {
    "name": "Alice",
    "grade": "A",
    "score": 95
}
print(student["name"])    # Output: Alice
```

Dictionaries have **11 built-in methods**.

---

### Accessing Data

#### `get()` — Safely Get a Value

**What it does:** Returns the value for a key. If the key doesn't exist, returns `None` (or a default) instead of crashing.

```python
student = {"name": "Alice", "score": 95}

# RISKY way:
# print(student["age"])   # KeyError!

# SAFE way:
print(student.get("age"))          # Output: None
print(student.get("age", 0))       # Output: 0  (default value)
print(student.get("score", 0))     # Output: 95
```

#### `keys()` — Get All Keys

```python
student = {"name": "Alice", "score": 95, "grade": "A"}
print(student.keys())    # Output: dict_keys(['name', 'score', 'grade'])

# Loop through keys
for key in student.keys():
    print(key)
# Output: name  score  grade
```

#### `values()` — Get All Values

```python
print(student.values())   # Output: dict_values(['Alice', 95, 'A'])

for value in student.values():
    print(value)
# Output: Alice  95  A
```

#### `items()` — Get All Key-Value Pairs

```python
for key, value in student.items():
    print(f"{key}: {value}")
# Output:
# name: Alice
# score: 95
# grade: A
```

---

### Adding & Updating

#### `update()` — Add or Update Multiple Items

```python
student = {"name": "Alice", "score": 95}
student.update({"grade": "A", "score": 98})  # updates existing, adds new
print(student)
# Output: {'name': 'Alice', 'score': 98, 'grade': 'A'}
```

#### `setdefault()` — Add Key Only If It Doesn't Exist

```python
student = {"name": "Alice"}
student.setdefault("score", 0)    # Adds score=0 only if not present
print(student)   # Output: {'name': 'Alice', 'score': 0}

student.setdefault("name", "Bob")  # Name already exists — NOT changed
print(student)   # Output: {'name': 'Alice', 'score': 0}
```

---

### Removing Items

#### `pop()` — Remove Key and Return Its Value

```python
student = {"name": "Alice", "score": 95, "grade": "A"}
removed = student.pop("grade")
print(removed)    # Output: A
print(student)    # Output: {'name': 'Alice', 'score': 95}

# With a default (prevents KeyError)
print(student.pop("age", "Not found"))   # Output: Not found
```

#### `popitem()` — Remove and Return Last Inserted Item

```python
student = {"name": "Alice", "score": 95}
item = student.popitem()
print(item)      # Output: ('score', 95)
print(student)   # Output: {'name': 'Alice'}
```

#### `clear()` — Remove All Items

```python
student.clear()
print(student)   # Output: {}
```

---

### Copying

#### `copy()` — Shallow Copy

```python
original = {"a": 1, "b": 2}
copy = original.copy()
copy["c"] = 3
print(original)   # Output: {'a': 1, 'b': 2}  ← unchanged
print(copy)       # Output: {'a': 1, 'b': 2, 'c': 3}
```

#### `fromkeys()` — Create Dictionary from Keys

**What it does:** Creates a new dictionary with specified keys, all set to the same value.

```python
keys = ["name", "score", "grade"]
empty_student = dict.fromkeys(keys, "N/A")
print(empty_student)
# Output: {'name': 'N/A', 'score': 'N/A', 'grade': 'N/A'}

# Default value is None
print(dict.fromkeys(keys))
# Output: {'name': None, 'score': None, 'grade': None}
```

---

### Dictionary Methods Quick Reference Table

| Method | Purpose | Example |
|---|---|---|
| `clear()` | Remove all pairs | `d.clear()` |
| `copy()` | Shallow copy | `new = d.copy()` |
| `fromkeys(keys, v)` | New dict from keys | `dict.fromkeys(["a","b"], 0)` |
| `get(key, default)` | Safe value access | `d.get("x", None)` |
| `items()` | All key-value pairs | `for k,v in d.items()` |
| `keys()` | All keys | `d.keys()` |
| `pop(key, default)` | Remove & return value | `d.pop("age", 0)` |
| `popitem()` | Remove last pair | `d.popitem()` |
| `setdefault(k, v)` | Add if not exists | `d.setdefault("x", 0)` |
| `update(other)` | Add/update from dict | `d.update({"a": 1})` |
| `values()` | All values | `d.values()` |

---

## Part 5 — Python Tuple Methods

### What Are Tuples?

A **tuple** is an ordered, **immutable** (unchangeable) collection. Once created, you cannot add, remove, or change its items.

```python
coordinates = (10.5, 25.3)
colors = ("red", "green", "blue")
person = ("Alice", 25, "Lagos")
```

**Why use tuples instead of lists?**
- They are faster than lists
- They protect data that should not change
- They can be used as dictionary keys (lists cannot)
- They are commonly returned by functions to group related values

Tuples have only **2 methods** because they are immutable.

---

#### `count()` — Count Occurrences of a Value

```python
nums = (1, 2, 3, 2, 4, 2)
print(nums.count(2))   # Output: 3
print(nums.count(5))   # Output: 0
```

#### `index()` — Find First Position of a Value

```python
colors = ("red", "green", "blue", "green")
print(colors.index("green"))    # Output: 1  (first occurrence)
print(colors.index("green", 2)) # Output: 3  (search from index 2)

# colors.index("purple")  # ValueError if not found
```

---

### Tuple vs List vs Dictionary — When to Use Which

| Feature | List | Tuple | Dictionary |
|---|---|---|---|
| Ordered | Yes | Yes | Yes (Python 3.7+) |
| Changeable | Yes | **No** | Yes |
| Allows Duplicates | Yes | Yes | Keys: No, Values: Yes |
| Syntax | `[1, 2, 3]` | `(1, 2, 3)` | `{"a": 1}` |
| Use When | Data may change | Data is fixed | Labelled data |

---

## Part 6 — Python Set Methods

### What Are Sets?

A **set** is an unordered collection of **unique** items. Duplicates are automatically removed. Sets do not have a fixed order and do not support indexing.

```python
fruits = {"apple", "banana", "cherry"}
print(fruits)   # Output: {'banana', 'cherry', 'apple'}  ← order not guaranteed
```

**Why use sets?**
- Remove duplicates from a list instantly
- Check membership very fast
- Perform mathematical set operations (union, intersection, difference)

Sets have **15 methods** covering both modification and mathematical operations.

---

### Adding & Removing Items

#### `add()` — Add One Item

```python
fruits = {"apple", "banana"}
fruits.add("cherry")
print(fruits)   # Output: {'apple', 'banana', 'cherry'}

# Adding a duplicate — silently ignored
fruits.add("apple")
print(fruits)   # Output: {'apple', 'banana', 'cherry'}  ← no duplicate
```

#### `update()` — Add Multiple Items

```python
fruits = {"apple"}
fruits.update(["banana", "cherry", "date"])
print(fruits)   # Output: {'apple', 'banana', 'cherry', 'date'}
```

#### `remove()` — Remove Item (Error if Not Found)

```python
fruits = {"apple", "banana", "cherry"}
fruits.remove("banana")
print(fruits)   # Output: {'apple', 'cherry'}

# fruits.remove("mango")  # KeyError!
```

#### `discard()` — Remove Item (No Error if Not Found)

```python
fruits = {"apple", "banana"}
fruits.discard("banana")   # Removed
fruits.discard("mango")    # Silently ignored (no error)
print(fruits)   # Output: {'apple'}
```

#### `pop()` — Remove and Return a Random Item

```python
fruits = {"apple", "banana", "cherry"}
removed = fruits.pop()   # Removes a random item
print(removed)           # Output: some item (order is unpredictable)
```

#### `clear()` — Remove All Items

```python
fruits = {"apple", "banana"}
fruits.clear()
print(fruits)   # Output: set()
```

---

### Mathematical Set Operations

This is where sets truly shine. These operations come directly from **mathematical set theory** used in data science, databases, and statistics.

#### `union()` — All Items from Both Sets (OR)

**What it means:** Everything in A, everything in B, no duplicates.

```python
A = {1, 2, 3, 4}
B = {3, 4, 5, 6}

print(A.union(B))   # Output: {1, 2, 3, 4, 5, 6}
print(A | B)        # Same thing using operator
```

> **Real-world use:** Combining two customer lists into one (no duplicates).

#### `intersection()` — Items in BOTH Sets (AND)

**What it means:** Only items that appear in A AND B.

```python
A = {1, 2, 3, 4}
B = {3, 4, 5, 6}

print(A.intersection(B))   # Output: {3, 4}
print(A & B)               # Same using operator
```

> **Real-world use:** Finding customers who bought BOTH Product A AND Product B.

#### `difference()` — Items in A but NOT in B

**What it means:** What A has that B doesn't have.

```python
A = {1, 2, 3, 4}
B = {3, 4, 5, 6}

print(A.difference(B))   # Output: {1, 2}   (in A but not B)
print(A - B)             # Same using operator

print(B.difference(A))   # Output: {5, 6}   (in B but not A)
```

> **Real-world use:** Finding items that were in last month's order but NOT this month's.

#### `symmetric_difference()` — Items in EITHER but NOT BOTH

**What it means:** Everything except the overlapping items.

```python
A = {1, 2, 3, 4}
B = {3, 4, 5, 6}

print(A.symmetric_difference(B))   # Output: {1, 2, 5, 6}
print(A ^ B)                       # Same using operator
```

---

### Comparison & Checking Methods

#### `issubset()` — Is A Completely Inside B?

```python
A = {1, 2}
B = {1, 2, 3, 4}

print(A.issubset(B))    # Output: True   (all of A is in B)
print(B.issubset(A))    # Output: False  (B has items not in A)
```

#### `issuperset()` — Does A Contain All of B?

```python
print(B.issuperset(A))    # Output: True   (B contains all of A)
print(A.issuperset(B))    # Output: False
```

#### `isdisjoint()` — Do A and B Share No Items?

```python
A = {1, 2, 3}
B = {4, 5, 6}
C = {3, 4, 5}

print(A.isdisjoint(B))   # Output: True   (no shared items)
print(A.isdisjoint(C))   # Output: False  (3 is shared)
```

---

### In-Place Operation Methods (Modify the Set Directly)

These do the same operations as above but **change the original set** instead of returning a new one.

```python
A = {1, 2, 3}
B = {3, 4, 5}

# intersection_update — keep only shared items
A.intersection_update(B)
print(A)   # Output: {3}

A = {1, 2, 3}
# difference_update — remove items found in B
A.difference_update(B)
print(A)   # Output: {1, 2}

A = {1, 2, 3}
# symmetric_difference_update — keep only non-shared items
A.symmetric_difference_update(B)
print(A)   # Output: {1, 2, 4, 5}
```

---

### Set Methods Quick Reference Table

| Method | Purpose | Example |
|---|---|---|
| `add(x)` | Add item | `s.add(5)` |
| `clear()` | Remove all | `s.clear()` |
| `copy()` | Shallow copy | `s2 = s.copy()` |
| `difference(t)` | Items in s not in t | `s.difference(t)` |
| `difference_update(t)` | Remove items in t from s | `s.difference_update(t)` |
| `discard(x)` | Remove if exists (no error) | `s.discard(5)` |
| `intersection(t)` | Items in both | `s.intersection(t)` |
| `intersection_update(t)` | Keep only items in both | `s.intersection_update(t)` |
| `isdisjoint(t)` | No shared items? | `s.isdisjoint(t)` → `bool` |
| `issubset(t)` | s inside t? | `s.issubset(t)` → `bool` |
| `issuperset(t)` | s contains t? | `s.issuperset(t)` → `bool` |
| `pop()` | Remove random item | `s.pop()` |
| `remove(x)` | Remove (error if missing) | `s.remove(5)` |
| `symmetric_difference(t)` | Items in s or t, not both | `s.symmetric_difference(t)` |
| `symmetric_difference_update(t)` | Update with symmetric diff | `s.symmetric_difference_update(t)` |
| `union(t)` | All items from both | `s.union(t)` |
| `update(t)` | Add all items from t | `s.update([4,5,6])` |

---

## Guided Practice Exercises

### Exercise 1 — Student Report Card Processor

**Objective:** Use built-in functions and string methods to process student data.

**Scenario:** You are building a report card system for a school. Given a list of student names and scores, your program must generate formatted output.

**Steps:**

```python
# Step 1: Define the data
students = {
    " alice johnson ": 85,
    "BOB SMITH": 72,
    "  CAROL LEE  ": 91,
    "david brown": 68,
    "EVE WILSON": 55
}

# Step 2: Process each student
print("=" * 40)
print("STUDENT REPORT CARD".center(40))
print("=" * 40)

for raw_name, score in students.items():
    # Clean and format the name
    name = raw_name.strip().title()
    
    # Determine grade
    if score >= 90:
        grade = "A"
    elif score >= 80:
        grade = "B"
    elif score >= 70:
        grade = "C"
    elif score >= 60:
        grade = "D"
    else:
        grade = "F"
    
    # Format and print
    print(f"{name.ljust(20)} Score: {str(score).rjust(3)}  Grade: {grade}")

print("=" * 40)
# Statistics
scores = list(students.values())
print(f"Class Average: {sum(scores) / len(scores):.1f}")
print(f"Highest Score: {max(scores)}")
print(f"Lowest Score:  {min(scores)}")
passing = len([s for s in scores if s >= 60])
print(f"Passing Students: {passing}/{len(scores)}")
```

**Expected Output:**
```
========================================
           STUDENT REPORT CARD           
========================================
Alice Johnson        Score:  85  Grade: B
Bob Smith            Score:  72  Grade: C
Carol Lee            Score:  91  Grade: A
David Brown          Score:  68  Grade: D
Eve Wilson           Score:  55  Grade: F
========================================
Class Average: 74.2
Highest Score: 91
Lowest Score:  55
Passing Students: 4/5
```

**Self-check Questions:**
1. What happens to `"  CAROL LEE  "` after `.strip().title()`?
2. Why did we use `str(score).rjust(3)`?
3. What does `{sum(scores) / len(scores):.1f}` mean?

---

### Exercise 2 — Inventory Manager

**Objective:** Use list and dictionary methods to manage a shop inventory.

```python
# Starting inventory
inventory = {
    "apples": 50,
    "bananas": 30,
    "cherries": 80,
    "dates": 15,
    "elderberries": 5
}

# Simulate purchases and restocking
purchases = {"apples": 20, "bananas": 30, "dates": 10, "mangoes": 5}
restock = {"bananas": 50, "elderberries": 40, "figs": 25}

# Process purchases
for item, qty in purchases.items():
    if item in inventory:
        inventory[item] -= qty
    else:
        print(f"WARNING: {item} not in inventory — purchase rejected")

# Process restocking
inventory.update({k: inventory.get(k, 0) + v for k, v in restock.items()})

# Show inventory report
print("\nINVENTORY REPORT")
print("-" * 30)
for item, qty in sorted(inventory.items()):
    status = "LOW STOCK" if qty <= 10 else ""
    print(f"{item.capitalize():<15} {str(qty).rjust(5)}  {status}")

# Low stock alerts
low = [item for item, qty in inventory.items() if qty <= 10]
if low:
    print(f"\nLow Stock Alert: {', '.join(low)}")
```

---

### Exercise 3 — Text Analyser

**Objective:** Use string methods to analyse a text.

```python
text = """
Python is a versatile programming language. Python is used in web development,
data science, artificial intelligence, and automation. Python is easy to learn.
"""

# Clean the text
text = text.strip().lower()

# Word frequency analysis
words = text.split()
unique_words = set(words)

print(f"Total words: {len(words)}")
print(f"Unique words: {len(unique_words)}")
print(f"Character count (no spaces): {len(text.replace(' ', '').replace(chr(10), ''))}")

# Find most mentioned word (simple)
word_counts = {}
for word in words:
    # Remove punctuation
    clean_word = word.strip(".,!?;:")
    word_counts[clean_word] = word_counts.get(clean_word, 0) + 1

# Sort by frequency
sorted_words = sorted(word_counts.items(), key=lambda x: x[1], reverse=True)
print("\nTop 5 most frequent words:")
for word, count in sorted_words[:5]:
    print(f"  '{word}': {count} times")

# Check if certain words are present
keywords = ["python", "java", "science", "web"]
for kw in keywords:
    print(f"'{kw}' appears: {word_counts.get(kw, 0)} time(s)")
```

---

## Mini Project — Student Data Dashboard

### Project Overview

Build a complete student data processing system that uses all the data structures and methods learned in this lesson.

### Stage 1 — Setup Data

```python
# Student records
students = [
    {"name": "Alice Johnson", "scores": [85, 92, 78, 90], "subjects": {"Math", "Science", "English"}},
    {"name": "Bob Smith",     "scores": [72, 68, 75, 80], "subjects": {"Math", "Art", "History"}},
    {"name": "Carol Lee",     "scores": [95, 88, 92, 97], "subjects": {"Science", "Math", "Computing"}},
    {"name": "David Brown",   "scores": [55, 60, 52, 65], "subjects": {"English", "Art", "PE"}},
    {"name": "Eve Wilson",    "scores": [80, 85, 88, 82], "subjects": {"Science", "English", "Computing"}},
]
```

### Stage 2 — Calculate Statistics Per Student

```python
def get_grade(avg):
    if avg >= 90: return "A"
    elif avg >= 80: return "B"
    elif avg >= 70: return "C"
    elif avg >= 60: return "D"
    else: return "F"

print("STUDENT DASHBOARD".center(60, "="))
for student in students:
    name = student["name"]
    scores = student["scores"]
    avg = sum(scores) / len(scores)
    grade = get_grade(avg)
    highest = max(scores)
    lowest = min(scores)
    
    print(f"\n{name}")
    print(f"  Scores:  {scores}")
    print(f"  Average: {avg:.1f}  |  Grade: {grade}")
    print(f"  Highest: {highest}  |  Lowest: {lowest}")
    print(f"  Subjects: {', '.join(sorted(student['subjects']))}")
```

### Stage 3 — Class-Wide Analysis

```python
# Collect all averages
all_averages = [sum(s["scores"]) / len(s["scores"]) for s in students]

print("\n" + "CLASS STATISTICS".center(60, "="))
print(f"Class Average: {sum(all_averages) / len(all_averages):.1f}")
print(f"Top Score: {max(all_averages):.1f} ({students[all_averages.index(max(all_averages))]['name']})")
print(f"Lowest Score: {min(all_averages):.1f} ({students[all_averages.index(min(all_averages))]['name']})")

# Subject analysis
all_subjects = set()
for s in students:
    all_subjects.update(s["subjects"])

print(f"\nAll subjects offered: {', '.join(sorted(all_subjects))}")

# Who takes Math?
math_students = [s["name"] for s in students if "Math" in s["subjects"]]
print(f"Students taking Math: {', '.join(math_students)}")

# Subjects shared between Alice and Carol
alice_subjects = students[0]["subjects"]
carol_subjects = students[2]["subjects"]
shared = alice_subjects.intersection(carol_subjects)
print(f"Alice & Carol's shared subjects: {', '.join(shared)}")
```

**Milestone Output Sample:**
```
========================STUDENT DASHBOARD========================

Alice Johnson
  Scores:  [85, 92, 78, 90]
  Average: 86.2  |  Grade: B
  Highest: 92  |  Lowest: 78
  Subjects: English, Math, Science

...

======================CLASS STATISTICS========================
Class Average: 77.3
Top Score: 93.0 (Carol Lee)
Lowest Score: 58.0 (David Brown)
```

### Stage 4 — Reflection Questions

1. Why did we use a **set** for subjects instead of a list?
2. What would happen if two students had the same average — who would show as "Top Score"?
3. How would you modify this to allow adding a new student?
4. How could you use `zip()` to pair student names with their averages?

---

## Common Beginner Mistakes

### Mistake 1: Expecting `sort()` to Return a List

```python
# WRONG:
numbers = [3, 1, 2]
sorted_numbers = numbers.sort()
print(sorted_numbers)  # Output: None  ← wrong!

# CORRECT:
sorted_numbers = sorted(numbers)   # Use sorted() instead
# OR
numbers.sort()
print(numbers)          # Use the original list, now sorted
```

---

### Mistake 2: Modifying a String "In Place"

```python
# WRONG assumption:
name = "alice"
name.upper()          # This does NOT change name!
print(name)           # Output: alice

# CORRECT:
name = name.upper()   # Assign the result back
print(name)           # Output: ALICE
```

---

### Mistake 3: Using `append()` Instead of `extend()`

```python
list1 = [1, 2, 3]
list2 = [4, 5, 6]

# WRONG (if you want to add individual items):
list1.append(list2)
print(list1)   # Output: [1, 2, 3, [4, 5, 6]]  ← nested list!

# CORRECT:
list1 = [1, 2, 3]
list1.extend(list2)
print(list1)   # Output: [1, 2, 3, 4, 5, 6]
```

---

### Mistake 4: Forgetting `get()` for Dictionary Access

```python
student = {"name": "Alice"}

# WRONG:
# print(student["age"])   # KeyError!

# CORRECT:
print(student.get("age", 0))   # Output: 0
```

---

### Mistake 5: Assuming Sets Are Ordered

```python
my_set = {3, 1, 4, 1, 5, 9}
# You CANNOT do: my_set[0]  — sets don't support indexing!
# Order is not guaranteed.

# If you need to iterate:
for item in sorted(my_set):  # Sort first for predictable order
    print(item)
```

---

### Mistake 6: Confusing `remove()` and `discard()` for Sets

```python
fruits = {"apple", "banana"}

# remove() raises error if not found:
# fruits.remove("mango")   # KeyError!

# discard() is safe:
fruits.discard("mango")    # No error, no change
```

---

### Mistake 7: Not Converting `input()` to a Number

```python
# WRONG:
age = input("Your age: ")
next_year = age + 1   # TypeError! Can't add int to str

# CORRECT:
age = int(input("Your age: "))
next_year = age + 1
print("Next year you'll be:", next_year)
```

---

### Mistake 8: Confusing `int("3.9")` with `int(float("3.9"))`

```python
# WRONG:
# x = int("3.9")   # ValueError!

# CORRECT:
x = int(float("3.9"))
print(x)   # Output: 3
```

---

## Reflection Questions

1. What is the difference between `sort()` and `sorted()`? When would you use each?
2. Why do strings have so many more methods than tuples?
3. What is the difference between `remove()` and `discard()` for sets? When is `discard()` safer?
4. When would you use `all()` vs `any()`? Give a real-world example for each.
5. You have two lists of students: one from Monday's class and one from Tuesday's. How would you find students who attended BOTH days? Which data structure would you use?
6. What is the difference between `list.copy()` and assigning a list to a new variable (`b = a`)?
7. How would `enumerate()` make looping through a list of items and printing numbered lines easier?
8. Why is `get()` safer than `dict[key]` when accessing dictionary values?

---

## Completion Checklist

Mark each item as you complete it:

- [ ] I can use `int()`, `float()`, `str()`, and `bool()` to convert between types
- [ ] I understand what `len()`, `range()`, `sorted()`, and `reversed()` do
- [ ] I can use `enumerate()` to loop with an index
- [ ] I can use `zip()` to pair items from two lists
- [ ] I can use `map()` and `filter()` to transform and filter collections
- [ ] I know the difference between `all()` and `any()`
- [ ] I can use `print()` with `sep=` and `end=` parameters
- [ ] I can safely get user input with `input()` and convert it
- [ ] I can use `upper()`, `lower()`, `title()`, `strip()` on strings
- [ ] I can use `split()` and `join()` to convert between strings and lists
- [ ] I can use `replace()`, `find()`, `count()`, `startswith()`, `endswith()`
- [ ] I can use `format()` and f-strings for formatting output
- [ ] I can add, remove, sort, and copy list items using list methods
- [ ] I can access dictionary data with `get()`, `keys()`, `values()`, `items()`
- [ ] I can update and remove dictionary entries safely
- [ ] I understand what a tuple is and know its 2 methods
- [ ] I can use `add()`, `remove()`, `discard()`, `update()` on sets
- [ ] I can perform `union()`, `intersection()`, `difference()` on sets
- [ ] I can use `issubset()`, `issuperset()`, and `isdisjoint()`
- [ ] I completed the Student Dashboard mini-project

---

## Lesson Summary

In this lesson you explored Python's entire built-in reference — the complete toolkit that Python gives you for free.

**Built-in Functions** are tools available everywhere. The most important ones to master are: `print()`, `input()`, `len()`, `range()`, `sorted()`, `enumerate()`, `zip()`, `map()`, `filter()`, `type()`, `isinstance()`, `int()`, `float()`, `str()`, `bool()`, `abs()`, `round()`, `max()`, `min()`, `sum()`, and `all()`/`any()`.

**String Methods** are called on text values using a dot. All string methods return NEW strings — strings are immutable. The most practical string methods are: `strip()`, `split()`, `join()`, `replace()`, `upper()`, `lower()`, `title()`, `find()`, `startswith()`, `endswith()`, `format()`, and `isdigit()`.

**List Methods** modify the list in place (except `copy()` and `count()`/`index()`). Master: `append()`, `extend()`, `insert()`, `remove()`, `pop()`, `sort()`, `reverse()`, `copy()`, `count()`, and `index()`.

**Dictionary Methods** give you safe access, update, and iteration. Master: `get()`, `keys()`, `values()`, `items()`, `update()`, `pop()`, `setdefault()`, `copy()`, and `fromkeys()`.

**Tuple Methods** — just `count()` and `index()` since tuples are immutable. Use tuples when data should not change.

**Set Methods** provide mathematical set operations — union, intersection, difference, symmetric difference — essential in data science and analysis. `discard()` is safer than `remove()`. `issubset()`, `issuperset()`, and `isdisjoint()` let you compare sets.

> **Real-world connection:** Every Python program you will ever write — whether it's a web application, a data analysis script, a machine learning model, or an automation tool — relies on these built-in functions and methods daily. Mastering this reference is the difference between writing slow, repetitive code and writing clean, professional Python.
