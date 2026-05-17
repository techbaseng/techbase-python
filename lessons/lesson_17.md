---
render_with_liquid: false
title: "Iterators, Modules, Dates, and Math in Python"
nav_order: 17
---

# Lesson 17: Iterators, Modules, Dates, and Math in Python

---

## Lesson Introduction

Welcome to Lesson 17! In this lesson, you will learn four powerful and practical Python topics that every programmer uses regularly:

1. **Iterators** — How Python moves through data, one item at a time
2. **Modules** — How to organise and reuse code across files
3. **Dates and Times** — How to work with real-world time using Python
4. **Math** — How to do advanced calculations using Python's built-in tools

These four topics connect naturally. You use iterators to walk through data, modules to import useful tools (like `datetime` and `math`), dates to track when things happen, and math to calculate important values in science, finance, and engineering.

By the end of this lesson you will be able to write a mini program that tracks student submissions, shows the current date, and calculates statistics — all from scratch.

---

## Prerequisite Concepts

Before we begin, make sure you are comfortable with these ideas:

- **Variables** — storing values like `x = 5`
- **Lists and Tuples** — collections of items like `["apple", "banana"]`
- **For loops** — repeating actions with `for x in something:`
- **Functions** — blocks of reusable code created with `def`
- **Classes** — blueprints for objects (you will see them in the Iterator section)

If any of those feel unfamiliar, review your earlier lessons briefly before continuing.

---

## Part 1 — Python Iterators

### What is an Iterator?

Think of an iterator like a **book with a bookmark**. The bookmark remembers which page you are on. Every time you want to read, you open to the bookmark, read one page, and move the bookmark forward. You never have to remember where you are — the bookmark does that for you.

In Python, an **iterator** is an object that remembers where you are in a collection of items. Each time you ask for the "next" item, it gives you one and moves forward automatically.

**Why does this exist?**
Sometimes you have a very large amount of data and you cannot (or do not want to) load it all at once. An iterator lets you process one item at a time without needing to see the full list upfront. This saves memory and is faster for large data.

---

### Two Important Words: Iterable vs Iterator

These sound similar but mean different things.

| Word | What it means | Examples |
|------|---------------|---------|
| **Iterable** | An object you CAN loop through | `list`, `tuple`, `dict`, `set`, `string` |
| **Iterator** | An object that IS actively stepping through another object | Created by calling `iter()` on an iterable |

**Analogy:** A list is like a full bag of fruit. An iterator is the hand reaching into the bag and pulling out one fruit at a time.

---

### The `iter()` and `next()` Functions

To turn an iterable into an iterator, you use `iter()`.  
To get the next item from an iterator, you use `next()`.

**Very simple example:**

```python
mytuple = ("apple", "banana", "cherry")  # This is an iterable (a tuple)
myit = iter(mytuple)                     # This creates an iterator from it

print(next(myit))   # Step 1: get the first item
print(next(myit))   # Step 2: get the second item
print(next(myit))   # Step 3: get the third item
```

**Expected Output:**
```
apple
banana
cherry
```

**Line by line explanation:**
- `mytuple = ("apple", "banana", "cherry")` — creates a tuple with three fruits
- `myit = iter(mytuple)` — creates an iterator; it is now "pointing at" apple
- `print(next(myit))` — asks the iterator: "what's the next item?" It returns `apple` and moves the pointer to `banana`
- `print(next(myit))` — returns `banana`, pointer moves to `cherry`
- `print(next(myit))` — returns `cherry`, pointer moves past the end

> 💡 **Think about it:** What would happen if you called `next(myit)` a fourth time? There are no more items — Python would raise an error called `StopIteration`. You will learn how to handle that shortly.

---

### Strings Are Iterable Too

A string is just a sequence of characters. So strings are also iterable:

```python
mystr = "banana"
myit = iter(mystr)

print(next(myit))   # b
print(next(myit))   # a
print(next(myit))   # n
print(next(myit))   # a
print(next(myit))   # n
print(next(myit))   # a
```

**Expected Output:**
```
b
a
n
a
n
a
```

Each call to `next()` returns one character, in order.

---

### Looping Through an Iterator

You already know the `for` loop. Here is something interesting: when you use a `for` loop on a list, tuple, string, or other iterable, Python is secretly using an iterator under the hood!

```python
mytuple = ("apple", "banana", "cherry")

for x in mytuple:
    print(x)
```

**Expected Output:**
```
apple
banana
cherry
```

Python automatically calls `iter()` to create an iterator and then calls `next()` on every loop turn. The `for` loop knows when to stop because the iterator signals "done" by raising `StopIteration`.

**Same thing with a string:**

```python
mystr = "banana"

for x in mystr:
    print(x)
```

**Expected Output:**
```
b
a
n
a
n
a
```

> 💡 **Real-world connection:** Every time you write `for item in my_list:`, Python is using the iterator protocol. Understanding this helps you understand how loops actually work inside Python.

---

### Creating Your Own Iterator

Python lets you build your own custom iterator by creating a class with two special methods:

- `__iter__()` — sets up the iterator (runs once when `iter()` is called)
- `__next__()` — returns the next value (runs every time `next()` is called)

**What is a class?** Think of a class as a blueprint. It defines what an object should do. `__iter__` and `__next__` are special "dunder" (double underscore) methods that Python calls automatically.

**Simple custom iterator — counts upward from 1:**

```python
class MyNumbers:
    def __iter__(self):
        self.a = 1      # Start counting from 1
        return self     # Must return the iterator object itself

    def __next__(self):
        x = self.a      # Save the current value
        self.a += 1     # Move to the next number (a += 1 means a = a + 1)
        return x        # Return the current value

myclass = MyNumbers()   # Create an instance of the class
myiter = iter(myclass)  # Call __iter__, which sets self.a = 1

print(next(myiter))     # Calls __next__, returns 1, sets self.a = 2
print(next(myiter))     # Returns 2, sets self.a = 3
print(next(myiter))     # Returns 3, sets self.a = 4
print(next(myiter))     # Returns 4
print(next(myiter))     # Returns 5
```

**Expected Output:**
```
1
2
3
4
5
```

**Line by line breakdown of `__next__`:**
- `x = self.a` — saves the current count (e.g., 1) into `x`
- `self.a += 1` — increments the count for next time (now it will be 2)
- `return x` — sends back the saved value (1)

> 💡 **What if you change `self.a = 1` to `self.a = 5`?** The sequence would start at 5, 6, 7, … Try it!

---

### StopIteration — How to Stop Your Iterator

The example above would count forever if you kept calling `next()`. In real programs, that would be a problem. Python has a solution: you raise a special signal called `StopIteration` when the sequence should end.

**Example — count from 1 to 20 only:**

```python
class MyNumbers:
    def __iter__(self):
        self.a = 1
        return self

    def __next__(self):
        if self.a <= 20:        # As long as the count is 20 or less...
            x = self.a
            self.a += 1
            return x
        else:
            raise StopIteration  # Signal: no more items!

myclass = MyNumbers()
myiter = iter(myclass)

for x in myiter:       # for loop automatically stops at StopIteration
    print(x)
```

**Expected Output:**
```
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
```

**What `raise StopIteration` does:**
- `raise` is Python's keyword for signalling an error or event
- `StopIteration` is the specific signal that tells a `for` loop "we are done"
- The `for` loop catches this signal silently and stops — you never see an error

> 💡 **Common beginner mistake:** Forgetting to include the `raise StopIteration` and having an infinite loop. Always include a stopping condition!

---

### Guided Practice — Part 1: Iterators

**Exercise 1A — Iterate manually**

**Objective:** Practice using `iter()` and `next()` on a list.

**Scenario:** A school stores student names in a list. Print the first three names manually using `next()`.

**Steps:**
1. Create a list: `students = ["Amaka", "Chidi", "Emeka", "Ngozi", "Yemi"]`
2. Create an iterator from it using `iter()`
3. Print the first three names using three separate `next()` calls

**Expected Output:**
```
Amaka
Chidi
Emeka
```

**Solution:**
```python
students = ["Amaka", "Chidi", "Emeka", "Ngozi", "Yemi"]
myit = iter(students)

print(next(myit))   # Amaka
print(next(myit))   # Chidi
print(next(myit))   # Emeka
```

**Self-check questions:**
- What would the 4th `next()` call return?
- What happens after the 5th `next()` call?

---

**Exercise 1B — Custom iterator for even numbers**

**Objective:** Build a custom iterator that generates the first N even numbers.

**Scenario:** You need even numbers for a data-processing task.

```python
class EvenNumbers:
    def __iter__(self):
        self.n = 0         # Start at 0 (first even number)
        return self

    def __next__(self):
        if self.n <= 20:   # Stop after 20
            x = self.n
            self.n += 2    # Move to next even number
            return x
        else:
            raise StopIteration

myevens = EvenNumbers()
myiter = iter(myevens)

for x in myiter:
    print(x)
```

**Expected Output:**
```
0
2
4
6
8
10
12
14
16
18
20
```

**What-if challenge:** What if you changed `self.n += 2` to `self.n += 3`? What sequence would you get?

---

## Part 2 — Python Modules

### What is a Module?

Think of a **module** like a toolbox. When you are building something, you do not carry every tool you own in your hands — you keep them in a toolbox and pick out what you need. A Python module is a file of pre-written code (functions, variables, classes) that you can "pick up" and use in your own program.

**Why do modules exist?**
- To organise code: instead of one giant messy file, split code into neat files
- To reuse code: write a function once in a module, use it in many programs
- To share code: Python has thousands of ready-made modules others have built

A module is simply a Python file saved with the `.py` extension. Any `.py` file can be a module.

---

### Creating a Module

To create a module, write your Python code in a file and save it as `something.py`.

**Create a file called `mymodule.py`:**

```python
# mymodule.py
def greeting(name):
    print("Hello, " + name)
```

That is it! You have a module. It contains one function called `greeting`.

---

### Using (Importing) a Module

To use a module in another file, you use the `import` keyword.

**In a different file (e.g., `main.py`):**

```python
import mymodule

mymodule.greeting("Jonathan")
```

**Expected Output:**
```
Hello, Jonathan
```

**Breaking it down:**
- `import mymodule` — Python finds `mymodule.py` and loads it
- `mymodule.greeting("Jonathan")` — accesses the `greeting` function inside `mymodule`
- The syntax is always: `module_name.function_name()`

> ⚠️ **Important rule:** When calling a function from a module, you must use the format `module_name.function_name()`. Forgetting the `module_name.` part is a very common beginner mistake.

---

### Variables in a Module

Modules can contain more than functions. They can hold variables of any type — strings, numbers, lists, dictionaries, and so on.

**In `mymodule.py`, add a dictionary:**

```python
# mymodule.py

def greeting(name):
    print("Hello, " + name)

person1 = {
    "name": "John",
    "age": 36,
    "country": "Norway"
}
```

**In `main.py`, access the dictionary:**

```python
import mymodule

a = mymodule.person1["age"]
print(a)
```

**Expected Output:**
```
36
```

**What happened:**
- `mymodule.person1` accesses the dictionary called `person1` inside the module
- `["age"]` gets the value associated with the `"age"` key
- The result `36` is stored in `a` and printed

---

### Renaming a Module (Aliases)

Sometimes module names are long and you want a shorter name. Use the `as` keyword to create an **alias** (a nickname).

```python
import mymodule as mx

a = mx.person1["age"]
print(a)
```

**Expected Output:**
```
36
```

Instead of typing `mymodule` every time, you type `mx`. This is especially useful with very common modules like NumPy (usually imported as `np`) or Pandas (usually imported as `pd`).

---

### Built-in Modules

Python comes with dozens of modules already installed. You do not need to create them — just import them. Examples include `platform`, `math`, `datetime`, `random`, `os`, and more.

**Example — using the `platform` module to check your operating system:**

```python
import platform

x = platform.system()
print(x)
```

**Expected Output (depends on your computer):**
```
Windows
```
or
```
Linux
```
or
```
Darwin
```
(Darwin = macOS)

---

### The `dir()` Function — What's Inside a Module?

If you ever want to see all the functions and variables inside a module, use the `dir()` function. It returns a list of everything the module contains.

```python
import platform

x = dir(platform)
print(x)
```

**Expected Output (shortened):**
```
['DEV_NULL', '_UNIXCONFDIR', '__builtins__', ..., 'architecture', 'java_ver', 'machine', 'node', 'platform', 'processor', 'python_branch', 'python_build', ...]
```

> 💡 **Real-world use:** When you discover a new module and want to explore it, `dir(module_name)` is your quick guide to what tools it provides.

---

### Importing Only Parts of a Module

Sometimes you only need one specific function or variable from a module. You can import just that one thing using the `from` keyword:

```python
from mymodule import person1

print(person1["age"])
```

**Expected Output:**
```
36
```

**Key difference:** When using `from module import something`, you do NOT use the module name prefix. You just write `person1["age"]`, not `mymodule.person1["age"]`.

**Two styles compared:**

```python
# Style 1: import the whole module
import mymodule
print(mymodule.person1["age"])   # must use prefix

# Style 2: import only what you need
from mymodule import person1
print(person1["age"])            # no prefix needed
```

Both produce the same result: `36`.

> ⚠️ **Common beginner mistake:** Using `from mymodule import person1` and then writing `mymodule.person1["age"]` — this causes a `NameError` because you did not import the full module, only the specific item.

---

### Guided Practice — Part 2: Modules

**Exercise 2A — Create and use a simple module**

**Objective:** Create a module with useful school functions.

**Step 1:** Create a file called `school.py`:

```python
# school.py

school_name = "Sunrise Academy"
total_students = 450

def welcome(student_name):
    print("Welcome to " + school_name + ", " + student_name + "!")

def average(scores):
    return sum(scores) / len(scores)
```

**Step 2:** In your main file, use the module:

```python
import school

school.welcome("Amaka")

scores = [78, 85, 92, 70, 88]
avg = school.average(scores)
print("Class average:", avg)
print("Total students:", school.total_students)
```

**Expected Output:**
```
Welcome to Sunrise Academy, Amaka!
Class average: 82.6
Total students: 450
```

**Self-check:** What would `from school import welcome` change about how you call the function?

---

## Part 3 — Python Dates

### Why Doesn't Python Have a Built-in Date Type?

Unlike numbers or strings, a date is not one of Python's built-in data types. Instead, Python gives you a **module** called `datetime` that you can import to work with dates and times.

This connects directly to what you just learned — `datetime` is a **module**, and you must **import** it before using it.

---

### Importing and Using `datetime`

```python
import datetime

x = datetime.datetime.now()
print(x)
```

**Expected Output (will match your current date and time):**
```
2025-07-15 14:32:45.678901
```

**Breaking it down:**
- `import datetime` — loads the datetime module
- `datetime.datetime` — inside the `datetime` module, there is a class also called `datetime`
- `.now()` — calls the `now()` method, which captures the current date and time at this exact moment
- The output format is: `YYYY-MM-DD HH:MM:SS.microseconds`

The date output contains: **year, month, day, hour, minute, second, and microsecond**.

---

### Accessing Individual Date Parts

A datetime object contains many parts. You can access them individually:

```python
import datetime

x = datetime.datetime.now()

print(x.year)              # just the year number
print(x.strftime("%A"))    # full weekday name
```

**Expected Output (example):**
```
2025
Tuesday
```

- `x.year` — accesses the year attribute directly
- `x.strftime("%A")` — formats the date; `%A` means "full weekday name"

---

### Creating a Specific Date Object

You do not have to use "today's date." You can create any date you want using `datetime.datetime(year, month, day)`:

```python
import datetime

x = datetime.datetime(2020, 5, 17)

print(x)
```

**Expected Output:**
```
2020-05-17 00:00:00
```

**Parameters explained:**
- `2020` — the year
- `5` — the month (May)
- `17` — the day
- The time defaults to `00:00:00` (midnight) when not specified

You can also pass optional time parameters: `datetime.datetime(year, month, day, hour, minute, second, microsecond, timezone)`. But for most uses, just year/month/day is enough.

---

### The `strftime()` Method — Formatting Dates as Text

`strftime` stands for "string from time." It converts a date object into a human-readable string using **format codes**.

```python
import datetime

x = datetime.datetime(2018, 6, 1)

print(x.strftime("%B"))
```

**Expected Output:**
```
June
```

`%B` means "full month name."

**Complete format codes reference:**

| Code | What it gives you | Example |
|------|------------------|---------|
| `%a` | Weekday, short | Wed |
| `%A` | Weekday, full | Wednesday |
| `%w` | Weekday as number (0=Sunday) | 3 |
| `%d` | Day of month (01–31) | 31 |
| `%b` | Month name, short | Dec |
| `%B` | Month name, full | December |
| `%m` | Month as number (01–12) | 12 |
| `%y` | Year, 2-digit | 18 |
| `%Y` | Year, 4-digit | 2018 |
| `%H` | Hour (00–23) | 17 |
| `%I` | Hour (00–12) | 05 |
| `%p` | AM or PM | PM |
| `%M` | Minute (00–59) | 41 |
| `%S` | Second (00–59) | 08 |
| `%f` | Microsecond | 548513 |
| `%j` | Day number of the year (001–366) | 365 |
| `%U` | Week number of year (Sunday first) | 52 |
| `%W` | Week number of year (Monday first) | 52 |
| `%c` | Local full date and time | Mon Dec 31 17:41:00 2018 |
| `%x` | Local date | 12/31/18 |
| `%X` | Local time | 17:41:00 |

---

### Multiple Format Codes Together

You can combine many format codes to build any date string you want:

```python
import datetime

x = datetime.datetime(2024, 3, 14)

# Format: "Day, DD Month YYYY"
print(x.strftime("%A, %d %B %Y"))

# Format: "MM/DD/YYYY"
print(x.strftime("%m/%d/%Y"))

# Format: "Year: YYYY | Month: MM | Day: DD"
print(x.strftime("Year: %Y | Month: %m | Day: %d"))
```

**Expected Output:**
```
Thursday, 14 March 2024
03/14/2024
Year: 2024 | Month: 03 | Day: 14
```

> 💡 **Real-world use:** In business systems, you often need to display dates in different formats for different regions. `strftime()` is how you do that.

---

### Guided Practice — Part 3: Dates

**Exercise 3A — Birthday formatter**

**Objective:** Create a date for a birthday and print it in three different formats.

**Scenario:** You are building a school records system. Format a student's birthday in three ways.

```python
import datetime

birthday = datetime.datetime(2005, 8, 22)

# Format 1: Full written date
print(birthday.strftime("%A, %d %B %Y"))

# Format 2: Short numeric
print(birthday.strftime("%m/%d/%Y"))

# Format 3: Just the year and month
print(birthday.strftime("%B %Y"))
```

**Expected Output:**
```
Monday, 22 August 2005
08/22/2005
August 2005
```

---

**Exercise 3B — Today's date display**

```python
import datetime

today = datetime.datetime.now()

print("Today is:", today.strftime("%A, %d %B %Y"))
print("Current time:", today.strftime("%H:%M:%S"))
print("Day of year:", today.strftime("%j"))
```

**Expected Output (example — will match your current date):**
```
Today is: Tuesday, 15 July 2025
Current time: 09:45:22
Day of year: 196
```

**Self-check questions:**
- What format code gives just the day name?
- How would you display only the hour and minute (like `09:45`)?

---

## Part 4 — Python Math

### Two Ways to Do Math in Python

Python gives you two levels of math tools:

1. **Built-in functions** — always available, no import needed (`min()`, `max()`, `abs()`, `pow()`)
2. **The `math` module** — powerful functions you must import first (`math.sqrt()`, `math.ceil()`, `math.floor()`, `math.pi`)

---

### Built-in Math Functions

These functions are part of Python itself — no `import` needed.

**`min()` and `max()` — find the lowest or highest value:**

```python
x = min(5, 10, 25)
y = max(5, 10, 25)

print(x)
print(y)
```

**Expected Output:**
```
5
25
```

- `min(5, 10, 25)` — compares the three values and returns the smallest: 5
- `max(5, 10, 25)` — returns the largest: 25

**They also work on lists:**

```python
scores = [72, 88, 65, 94, 51]
print(min(scores))   # 51
print(max(scores))   # 94
```

---

**`abs()` — absolute value (always positive):**

The absolute value of a number is its distance from zero — always positive.

```python
x = abs(-7.25)
print(x)
```

**Expected Output:**
```
7.25
```

`-7.25` becomes `7.25`. Think of it as "remove the minus sign."

**Real-world use:** In finance, you might have a balance of -500 (debt). `abs(-500)` gives you `500` — the amount owed without the sign.

```python
debt = -15000
print("Amount owed:", abs(debt))
```
**Output:**
```
Amount owed: 15000
```

---

**`pow(x, y)` — raise x to the power of y:**

```python
x = pow(4, 3)    # same as 4 × 4 × 4
print(x)
```

**Expected Output:**
```
64
```

- `pow(4, 3)` means 4³ = 4 × 4 × 4 = 64

**More examples:**

```python
print(pow(2, 10))   # 2^10 = 1024
print(pow(5, 2))    # 5^2 = 25
print(pow(9, 0.5))  # 9^0.5 = square root of 9 = 3.0
```

**Expected Output:**
```
1024
25
3.0
```

> 💡 **Real-world use:** `pow()` is used in compound interest formulas, physics (energy calculations), and computer science (hash functions, encryption).

---

### The `math` Module

For more advanced mathematical operations, Python includes a dedicated `math` module.

```python
import math
```

Once imported, you have access to dozens of functions and constants.

---

**`math.sqrt()` — square root:**

The square root of a number is what you multiply by itself to get that number. For example, the square root of 64 is 8 (because 8 × 8 = 64).

```python
import math

x = math.sqrt(64)
print(x)
```

**Expected Output:**
```
8.0
```

Note: `sqrt()` always returns a float (a decimal number).

**More examples:**

```python
import math

print(math.sqrt(25))    # 5.0
print(math.sqrt(100))   # 10.0
print(math.sqrt(2))     # 1.4142135623730951
```

> 💡 **Real-world use:** In physics, calculating the length of a diagonal (Pythagoras theorem): `c = math.sqrt(a**2 + b**2)`. In statistics, the standard deviation formula involves square roots.

---

**`math.ceil()` — round UP to the nearest whole number:**

`ceil` stands for "ceiling." Just like a ceiling is always above you, `ceil()` always goes upward.

```python
import math

x = math.ceil(1.4)    # 1.4 rounds UP to 2
y = math.ceil(7.001)  # 7.001 rounds UP to 8
z = math.ceil(-1.4)   # -1.4 rounds UP to -1

print(x)   # 2
print(y)   # 8
print(z)   # -1
```

**Expected Output:**
```
2
8
-1
```

**Real-world use:** If you need 7.5 buses to transport students, you must order 8 buses — you cannot have half a bus. `math.ceil(7.5)` gives you 8.

---

**`math.floor()` — round DOWN to the nearest whole number:**

`floor` is the opposite. Just like a floor is always below you, `floor()` always goes downward.

```python
import math

x = math.floor(1.4)    # 1.4 rounds DOWN to 1
y = math.floor(7.999)  # 7.999 rounds DOWN to 7
z = math.floor(-1.4)   # -1.4 rounds DOWN to -2

print(x)   # 1
print(y)   # 7
print(z)   # -2
```

**Expected Output:**
```
1
7
-2
```

**Comparison of rounding functions:**

| Value | `round()` | `math.ceil()` | `math.floor()` |
|-------|-----------|--------------|----------------|
| 1.4 | 1 | 2 | 1 |
| 1.5 | 2 | 2 | 1 |
| 1.9 | 2 | 2 | 1 |
| -1.4 | -1 | -1 | -2 |

---

**`math.pi` — the constant π (Pi):**

Pi is the ratio of a circle's circumference to its diameter. It is approximately 3.14159... and goes on forever.

```python
import math

x = math.pi
print(x)
```

**Expected Output:**
```
3.141592653589793
```

**Real-world use — calculate the area of a circle:**

```python
import math

radius = 7
area = math.pi * radius ** 2   # Area = π × r²
print("Area of circle:", area)
```

**Expected Output:**
```
Area of circle: 153.93804002589985
```

---

### Second Example Set — Reinforcing Math Concepts

**Example: Physics — distance calculation with `sqrt`:**

```python
import math

# How far is a point (x=3, y=4) from the origin (0,0)?
# Pythagoras: distance = sqrt(x^2 + y^2)
x = 3
y = 4
distance = math.sqrt(x**2 + y**2)
print("Distance:", distance)
```

**Expected Output:**
```
Distance: 5.0
```

**Example: Budgeting — `ceil` for packaging:**

```python
import math

items = 55
items_per_box = 12

boxes_needed = math.ceil(items / items_per_box)
print("Boxes needed:", boxes_needed)
```

**Expected Output:**
```
Boxes needed: 5
```

(55 ÷ 12 = 4.58… → round up → 5 boxes)

---

### Guided Practice — Part 4: Math

**Exercise 4A — Score analysis**

**Objective:** Use built-in and math functions together on student scores.

**Scenario:** A teacher has a list of test scores and wants to analyze them.

```python
import math

scores = [72, 85, 91, 63, 78, 88, 55, 94, 70, 82]

print("Highest score:", max(scores))
print("Lowest score:", min(scores))
print("Average:", sum(scores) / len(scores))

# How many boxes of certificates (5 per box) are needed?
boxes = math.ceil(len(scores) / 5)
print("Certificate boxes needed:", boxes)

# Variance-like: sqrt of average squared difference from 80
diffs_sq = [(s - 80)**2 for s in scores]
spread = math.sqrt(sum(diffs_sq) / len(diffs_sq))
print("Spread from 80:", round(spread, 2))
```

**Expected Output:**
```
Highest score: 94
Lowest score: 55
Average: 77.8
Certificate boxes needed: 2
Spread from 80: 12.47
```

---

## Mini Project — Student Submission Tracker

Now you will combine all four topics: iterators, modules, dates, and math.

**Project Goal:** Build a simple student submission tracker that:
1. Stores student names and scores
2. Iterates through them with a custom iterator
3. Shows the current date of the report
4. Calculates math statistics

---

### Stage 1 — Setup: Create the data module

**Create a file called `student_data.py`:**

```python
# student_data.py

students = ["Amaka", "Chidi", "Emeka", "Ngozi", "Yemi", "Bola", "Tunde"]

scores = {
    "Amaka": 85,
    "Chidi": 72,
    "Emeka": 90,
    "Ngozi": 68,
    "Yemi": 88,
    "Bola": 75,
    "Tunde": 94
}

passing_score = 70
```

**Milestone output:** ✅ Module created with student data.

---

### Stage 2 — Custom Iterator for Students

**Create `main.py`:**

```python
# main.py
import student_data
import datetime
import math

# --- Custom Iterator ---
class StudentIterator:
    def __iter__(self):
        self.index = 0
        return self

    def __next__(self):
        if self.index < len(student_data.students):
            name = student_data.students[self.index]
            self.index += 1
            return name
        else:
            raise StopIteration

print("=== STUDENT LIST ===")
si = StudentIterator()
for name in iter(si):
    print("-", name)
```

**Milestone Output:**
```
=== STUDENT LIST ===
- Amaka
- Chidi
- Emeka
- Ngozi
- Yemi
- Bola
- Tunde
```

---

### Stage 3 — Date Stamped Report

```python
# Add to main.py

print("\n=== SUBMISSION REPORT ===")
today = datetime.datetime.now()
print("Report Date:", today.strftime("%A, %d %B %Y"))
print("Time Generated:", today.strftime("%H:%M:%S"))
```

**Milestone Output:**
```
=== SUBMISSION REPORT ===
Report Date: Tuesday, 15 July 2025
Time Generated: 10:23:45
```

---

### Stage 4 — Score Analysis with Math

```python
# Add to main.py

all_scores = list(student_data.scores.values())

print("\n=== SCORE STATISTICS ===")
print("Highest Score:", max(all_scores))
print("Lowest Score:", min(all_scores))
print("Average Score:", round(sum(all_scores) / len(all_scores), 2))
print("Square root of highest score:", round(math.sqrt(max(all_scores)), 2))
print("Boxes of certificates (10 per box):", math.ceil(len(all_scores) / 10))

passed = [s for s in all_scores if s >= student_data.passing_score]
print("Students passed:", len(passed), "out of", len(all_scores))
```

**Milestone Output:**
```
=== SCORE STATISTICS ===
Highest Score: 94
Lowest Score: 68
Average Score: 81.71
Square root of highest score: 9.7
Boxes of certificates (10 per box): 1
Students passed: 6 out of 7
```

---

### Stage 5 — Final Complete Program

**Full `main.py`:**

```python
import student_data
import datetime
import math

# Custom Iterator
class StudentIterator:
    def __iter__(self):
        self.index = 0
        return self

    def __next__(self):
        if self.index < len(student_data.students):
            name = student_data.students[self.index]
            self.index += 1
            return name
        else:
            raise StopIteration

# Print student list
print("=== STUDENT LIST ===")
si = StudentIterator()
for name in iter(si):
    score = student_data.scores[name]
    status = "PASS" if score >= student_data.passing_score else "FAIL"
    print(f"  {name}: {score} — {status}")

# Date report
print("\n=== SUBMISSION REPORT ===")
today = datetime.datetime.now()
print("Report Date:", today.strftime("%A, %d %B %Y"))
print("Time Generated:", today.strftime("%H:%M:%S"))

# Score analysis
all_scores = list(student_data.scores.values())
print("\n=== SCORE STATISTICS ===")
print("Highest Score:", max(all_scores))
print("Lowest Score:", min(all_scores))
print("Average Score:", round(sum(all_scores) / len(all_scores), 2))
print("Sqrt of highest:", round(math.sqrt(max(all_scores)), 2))
print("Boxes needed (10/box):", math.ceil(len(all_scores) / 10))
passed = [s for s in all_scores if s >= student_data.passing_score]
print("Students passed:", len(passed), "out of", len(all_scores))
```

**Complete Final Output:**
```
=== STUDENT LIST ===
  Amaka: 85 — PASS
  Chidi: 72 — PASS
  Emeka: 90 — PASS
  Ngozi: 68 — FAIL
  Yemi: 88 — PASS
  Bola: 75 — PASS
  Tunde: 94 — PASS

=== SUBMISSION REPORT ===
Report Date: Tuesday, 15 July 2025
Time Generated: 10:23:45

=== SCORE STATISTICS ===
Highest Score: 94
Lowest Score: 68
Average Score: 81.71
Sqrt of highest: 9.7
Boxes needed (10/box): 1
Students passed: 6 out of 7
```

**Reflection questions:**
- What would you change to lower the passing score to 65?
- How would you add a "class rank" feature using sorted scores?
- Could you use `strftime` to show the report in a Nigerian date format (e.g., `15/07/2025`)?

**Optional extension:** Add a function to `student_data.py` that takes a list of scores and returns a letter grade (A, B, C, D, F), then use your iterator to print each student's grade.

---

## Common Beginner Mistakes

### Mistake 1 — Calling `next()` too many times

```python
# Wrong — no StopIteration guard
mytuple = ("a", "b")
myit = iter(mytuple)
print(next(myit))   # a
print(next(myit))   # b
print(next(myit))   # ERROR: StopIteration
```

**Fix:** Use a `for` loop (it stops automatically) or wrap in a `try/except`:

```python
mytuple = ("a", "b")
myit = iter(mytuple)
try:
    while True:
        print(next(myit))
except StopIteration:
    print("Done!")
```

---

### Mistake 2 — Forgetting `raise StopIteration` in a custom iterator

```python
# Wrong — infinite loop!
class Counter:
    def __iter__(self):
        self.n = 1
        return self
    def __next__(self):
        x = self.n
        self.n += 1
        return x   # ← no stopping condition!
```

**Fix:** Always add a stopping condition:

```python
def __next__(self):
    if self.n <= 10:
        x = self.n
        self.n += 1
        return x
    else:
        raise StopIteration
```

---

### Mistake 3 — Using the module name after `from ... import`

```python
# Wrong
from mymodule import greeting
mymodule.greeting("Amaka")   # NameError: mymodule is not defined

# Correct
from mymodule import greeting
greeting("Amaka")            # No prefix needed
```

---

### Mistake 4 — Forgetting to import `datetime` or `math`

```python
# Wrong
x = datetime.datetime.now()   # NameError: datetime is not defined

# Correct
import datetime
x = datetime.datetime.now()
```

---

### Mistake 5 — Using `datetime()` directly instead of `datetime.datetime()`

```python
# Wrong
import datetime
x = datetime(2020, 5, 17)      # TypeError

# Correct
import datetime
x = datetime.datetime(2020, 5, 17)   # datetime module → datetime class → constructor
```

**Or use a shortcut:**

```python
from datetime import datetime
x = datetime(2020, 5, 17)   # Now you can use it directly
```

---

### Mistake 6 — Confusing `math.ceil` and `math.floor`

A quick reminder:
- `ceil` = **ceiling** = always goes **UP**
- `floor` = **floor** = always goes **DOWN**

```python
import math
print(math.ceil(4.1))    # 5  (goes UP)
print(math.floor(4.9))   # 4  (goes DOWN)
```

---

### Mistake 7 — Forgetting `import math` before using `math.sqrt`

```python
# Wrong
x = math.sqrt(16)   # NameError

# Correct
import math
x = math.sqrt(16)   # 4.0
```

---

## Reflection Questions

1. What is the difference between an **iterable** and an **iterator**? Can you give one example of each?

2. When would you prefer to use `from mymodule import function_name` instead of `import mymodule`?

3. If you use `datetime.datetime.now()` at midnight on New Year's Day, what would `strftime("%Y")` return? What about `strftime("%j")`?

4. You have a list of 23 students and 5 students fit per group. How would you use `math.ceil()` to find the number of groups needed?

5. Why does a custom iterator need both `__iter__()` and `__next__()`? What would happen if you only had one?

6. A temperature reading is `-12.7` degrees. What does `abs(-12.7)` return and why is that useful in a weather application?

7. You are building a library system. How would you use a module to organise the code for books, members, and borrowing separately?

---

## Completion Checklist

Before moving to the next lesson, make sure you can answer YES to all of these:

- [ ] I understand what an iterator is and how it is different from an iterable
- [ ] I can use `iter()` and `next()` to manually step through a tuple or list
- [ ] I can use a `for` loop on any iterable and understand it uses an iterator internally
- [ ] I can build a custom iterator class using `__iter__()` and `__next__()`
- [ ] I know how to add `StopIteration` to stop a custom iterator
- [ ] I understand what a module is and why it is useful
- [ ] I can create a simple module file and import it with `import`
- [ ] I know the difference between `import module` and `from module import name`
- [ ] I can use an alias with the `as` keyword when importing
- [ ] I can import the `datetime` module and get the current date and time
- [ ] I can create a specific date using `datetime.datetime(year, month, day)`
- [ ] I can format a date as a string using `strftime()` and at least 5 format codes
- [ ] I can use `min()`, `max()`, `abs()`, and `pow()` without any import
- [ ] I can import the `math` module and use `sqrt()`, `ceil()`, `floor()`, and `pi`
- [ ] I completed the Student Submission Tracker mini-project

---

## Lesson Summary

In this lesson you covered four important Python topics that work together in almost every real-world program:

**Iterators** let you move through any sequence one item at a time. Every `for` loop secretly uses an iterator. You can build your own by creating a class with `__iter__()` and `__next__()` methods, and control when to stop using `raise StopIteration`.

**Modules** are Python files that store reusable code. You import them with `import module_name` and access their contents with `module_name.something`. You can rename them with `as` for convenience, import just specific parts with `from module import name`, and explore their contents with `dir()`.

**Dates** are handled through Python's built-in `datetime` module. You can get today's date with `datetime.datetime.now()`, create any specific date with `datetime.datetime(year, month, day)`, and format dates into readable text using `strftime()` with format codes like `%A`, `%d`, `%B`, `%Y`.

**Math** comes in two layers: built-in functions like `min()`, `max()`, `abs()`, and `pow()` that are always available, and the `math` module which adds `sqrt()`, `ceil()`, `floor()`, `pi`, and much more. These tools are essential for STEM work, data analysis, and financial calculations.

Together, these tools form the backbone of writing clean, organised, and practical Python programs.

---

*End of Lesson 17*
