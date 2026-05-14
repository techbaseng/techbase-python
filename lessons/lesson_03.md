---
render_with_liquid: false
title: "Lesson 03 – Python Data Types, Numbers, Casting, and Booleans"
nav_order: 3
---

# Lesson 03 – Python Data Types, Numbers, Casting, and Booleans

---

## Lesson Introduction

Welcome to Lesson 03! In the previous lessons you learned how Python works and how variables store information. Now it is time to answer a very important question: **what kinds of information can Python store and work with?**

In this lesson you will learn:

- What a **data type** is and why it matters
- Every built-in data type Python has
- How to use `type()` to find out what type a variable is
- The three **number types**: `int`, `float`, and `complex`
- How **scientific notation** works in Python
- How to **convert (cast)** one type into another
- How to generate a **random number**
- What **Booleans** are and why they are the foundation of decision-making
- How Python decides if something is `True` or `False`
- How functions can return Boolean values
- How to use `isinstance()` to check types

By the end of this lesson you will build a mini-project: a **Student Report Card Analyser** that uses all four topics together.

> **Zero experience needed.** Every concept is explained from scratch with everyday analogies, step-by-step examples, and expected outputs.

---

## Prerequisite Concepts

Before diving in, let us review two ideas from earlier lessons that are necessary here.

### Variables

A **variable** is like a labelled box. You put a value inside the box and give the box a name so you can find it later.

```python
age = 17         # a box called "age" holding the number 17
name = "Ada"     # a box called "name" holding the word Ada
```

### The `print()` Function

`print()` shows something on screen.

```python
print(age)   # Output: 17
print(name)  # Output: Ada
```

Now you are ready.

---

## Part 1 – Python Data Types

### What Is a Data Type?

Imagine you have different types of containers in a kitchen:
- A **glass** holds liquid (water, juice).
- A **plate** holds solid food.
- A **jar** holds small items like spices.

You would not pour water on a plate — it would not work well. Similarly, in Python, different **kinds of data** are stored differently. The word **data type** (or just **type**) tells Python what kind of value is stored in a variable, and how Python is allowed to work with it.

For example:
- You can **add** two numbers together: `5 + 3` gives `8`.
- You can **join** two words together: `"hello" + " world"` gives `"hello world"`.
- But you **cannot** meaningfully add a number to a word without special steps.

Python needs to know the type so it can apply the right rules.

---

### Python's Built-In Data Types

Python comes with these data types already available — you do not need to install anything:

| Category | Type Name(s) | Plain English Meaning |
|---|---|---|
| **Text** | `str` | Words, sentences, letters |
| **Numbers** | `int`, `float`, `complex` | Whole numbers, decimal numbers, imaginary numbers |
| **Sequences** | `list`, `tuple`, `range` | Ordered collections of items |
| **Mapping** | `dict` | Key-value pairs (like a real dictionary) |
| **Sets** | `set`, `frozenset` | Unordered groups of unique items |
| **Boolean** | `bool` | Only `True` or `False` |
| **Binary** | `bytes`, `bytearray`, `memoryview` | Raw computer data (advanced) |
| **Nothing** | `NoneType` | The absence of a value |

> **Tip for beginners:** In this lesson you will focus on the most important everyday types: `str`, `int`, `float`, `complex`, and `bool`. The others will come in later lessons.

---

### How Python Assigns a Type Automatically

The beautiful thing about Python is that **you do not have to declare the type yourself**. Python is smart enough to figure it out from the value you assign.

**Analogy:** Imagine you hand someone an object. If you hand them a book, they know it is a book without you saying "here is a book." Python works the same way.

```python
x = "Hello World"    # Python sees quotes → it is a str
y = 20               # Python sees a whole number → it is an int
z = 20.5             # Python sees a decimal → it is a float
w = True             # Python sees True → it is a bool
```

**The type is set the moment you assign the value.**

---

### Checking the Type with `type()`

You can always ask Python: "What type is this variable?" using the built-in `type()` function.

**Syntax:**
```python
type(variable_name)
```

**Simple example:**

```python
x = 5
print(type(x))
```

**Expected output:**
```
<class 'int'>
```

The word `class` here just means "category." So `<class 'int'>` means "this belongs to the integer category."

**More examples:**

```python
a = "Python"
b = 3.14
c = True
d = ["apple", "mango"]

print(type(a))   # <class 'str'>
print(type(b))   # <class 'float'>
print(type(c))   # <class 'bool'>
print(type(d))   # <class 'list'>
```

**Expected output:**
```
<class 'str'>
<class 'float'>
<class 'bool'>
<class 'list'>
```

> **Thinking prompt:** What do you think the output of `print(type(42))` will be? Try guessing before reading further.

---

### Setting a Type Automatically — Full Reference Table

Here is every built-in type with the value that creates it:

```python
x = "Hello World"                        # str
x = 20                                   # int
x = 20.5                                 # float
x = 1j                                   # complex
x = ["apple", "banana", "cherry"]        # list
x = ("apple", "banana", "cherry")        # tuple
x = range(6)                             # range
x = {"name": "John", "age": 36}          # dict
x = {"apple", "banana", "cherry"}        # set
x = frozenset({"apple", "banana"})       # frozenset
x = True                                 # bool
x = b"Hello"                             # bytes
x = bytearray(5)                         # bytearray
x = memoryview(bytes(5))                 # memoryview
x = None                                 # NoneType
```

### Setting a Type Explicitly Using Constructor Functions

Sometimes you want to **force** a specific type. You do this using **constructor functions** — these are special functions named after the type:

```python
x = str("Hello World")      # explicitly a str
x = int(20)                 # explicitly an int
x = float(20.5)             # explicitly a float
x = bool(5)                 # explicitly a bool
```

You will learn more about exactly when and why to do this in the Casting section (Part 3 of this lesson).

---

## Part 2 – Python Numbers

### What Are Numbers in Python?

Numbers are one of the most important data types in any programming language. Python has **three numeric types**:

| Type | Full Name | What It Stores | Example |
|---|---|---|---|
| `int` | Integer | Whole numbers (no decimal point) | `5`, `-100`, `1000000` |
| `float` | Floating Point Number | Numbers with a decimal point | `3.14`, `-0.5`, `2.0` |
| `complex` | Complex Number | Numbers with a real and imaginary part | `3+5j`, `2j` |

> **Real-world analogy:**
> - `int` → counting people in a room (you cannot have 3.7 people).
> - `float` → measuring temperature or weight (37.5°C is perfectly fine).
> - `complex` → used in engineering, signal processing, and physics.

---

### Integer (`int`)

An **integer** is any whole number — positive, negative, or zero — with no decimal point. There is **no size limit** in Python: an integer can be as large as your computer's memory allows.

**Simple examples:**

```python
x = 1
y = 35656222554887711   # a very big number, still valid!
z = -3255522

print(type(x))
print(type(y))
print(type(z))
```

**Expected output:**
```
<class 'int'>
<class 'int'>
<class 'int'>
```

> **Common beginner mistake:** Writing a decimal like `1.0` thinking it is an integer. It is NOT — it is a `float`. Only `1` (no decimal point) is an `int`.

---

### Float (`float`)

A **float** is any number that contains a **decimal point**. The word "float" comes from "floating point" — referring to how computers store numbers with decimal places internally.

**Simple examples:**

```python
x = 1.10
y = 1.0
z = -35.59

print(type(x))
print(type(y))
print(type(z))
```

**Expected output:**
```
<class 'float'>
<class 'float'>
<class 'float'>
```

Notice that `1.0` is a float even though the decimal part is zero. The decimal point is what makes it a float.

---

### Floats with Scientific Notation

Floats can also be written using **scientific notation**. This is extremely useful in science, engineering, and data analysis when working with very large or very small numbers.

**What is scientific notation?**

Instead of writing `35000`, you write `3.5 × 10⁴`. In Python, the `e` (or `E`) represents "times 10 to the power of":

| Written form | Python form | Actual value |
|---|---|---|
| 3.5 × 10³ | `35e2` or `3.5e3` | 3500 |
| 1.2 × 10⁴ | `12E3` or `1.2e4` | 12000 |
| -8.77 × 10¹⁰⁰ | `-87.7e100` | a huge negative number |

**Example:**

```python
x = 35e3      # means 35 × 10³ = 35000.0
y = 12E4      # means 12 × 10⁴ = 120000.0
z = -87.7e100 # means -87.7 × 10¹⁰⁰

print(type(x))
print(type(y))
print(type(z))
```

**Expected output:**
```
<class 'float'>
<class 'float'>
<class 'float'>
```

> **Thinking prompt:** Why do `35e3` and `35000` give the same numeric value? What is the difference in how they are written?

---

### Complex (`complex`)

A **complex number** has two parts: a **real** part and an **imaginary** part. In Python, the imaginary part is written with a `j` at the end (in mathematics, you might see `i` instead, but Python always uses `j`).

**Format:** `real + imaginaryj`

**Examples:**

```python
x = 3 + 5j    # real part = 3, imaginary part = 5
y = 5j         # real part = 0, imaginary part = 5
z = -5j        # real part = 0, imaginary part = -5

print(type(x))
print(type(y))
print(type(z))
```

**Expected output:**
```
<class 'complex'>
<class 'complex'>
<class 'complex'>
```

**Where are complex numbers used?**
- Electrical engineering (AC circuit analysis)
- Signal processing (audio, images)
- Physics (quantum mechanics, wave equations)
- Computer graphics (fractals like the Mandelbrot set)

> **Beginner note:** You do not need to deeply understand complex numbers yet. Just know they exist and how Python writes them.

---

### Converting Between Number Types

You can **convert** a number from one type to another using these three functions:

| Function | What it does |
|---|---|
| `int(x)` | Converts `x` to an integer (removes any decimal) |
| `float(x)` | Converts `x` to a float (adds decimal point) |
| `complex(x)` | Converts `x` to a complex number |

**Complete example:**

```python
x = 1      # int
y = 2.8    # float
z = 1j     # complex

# Convert int to float:
a = float(x)

# Convert float to int:
b = int(y)

# Convert int to complex:
c = complex(x)

print(a)          # 1.0
print(b)          # 2
print(c)          # (1+0j)

print(type(a))    # <class 'float'>
print(type(b))    # <class 'int'>
print(type(c))    # <class 'complex'>
```

**Expected output:**
```
1.0
2
(1+0j)
<class 'float'>
<class 'int'>
<class 'complex'>
```

**Important rule:** Notice that `int(2.8)` gave `2`, not `3`. Converting a float to an int in Python **always rounds DOWN** (removes the decimal, does not round to nearest). This is called **truncation**.

> **Common beginner mistake:** Expecting `int(2.8)` to give `3`. It gives `2`. Python simply cuts off the decimal — it does not round.

**Another important rule:** You **cannot** convert a `complex` number back to `int` or `float`. Python will raise an error if you try.

```python
z = 3 + 5j
# int(z)   → This will cause a TypeError!
```

---

### Random Numbers

Python does not have a standalone `random()` function built in by default. Instead, it has a built-in **module** (a collection of extra tools) called `random`.

**What is a module?** A module is like a toolbox you can borrow. You ask Python: "Please bring me the random toolbox" using the word `import`.

**Generating a random integer:**

```python
import random

print(random.randrange(1, 10))
```

**Expected output:** (any number from 1 to 9 — the end number 10 is excluded)
```
7
```

Every time you run this, the number will likely be different. This is great for:
- Dice rolling in games
- Shuffling quiz questions
- Simulating random events in science

> **Thinking prompt:** If you change `random.randrange(1, 10)` to `random.randrange(1, 7)`, what is the smallest and largest number you could get? Think about it — the answer is 1 and 6, like a dice!

---

## Part 3 – Python Casting (Type Conversion)

### What Is Casting?

**Casting** means changing a value from one data type into another. The word comes from metal-casting — you melt metal (one form) and pour it into a mould to get a different shape (another form). Same substance, different form.

**Why do we need casting?**

Sometimes your data arrives in the wrong type. For example:
- A user types their age in a text box → Python receives it as a string `"25"`, not the number `25`.
- You need to do maths with it, but you cannot do maths on strings.
- You **cast** the string to an integer so you can calculate with it.

**Another real-world example:** Imagine your school stores exam scores as text in a spreadsheet ("87", "92", "74"). Before calculating averages, you must convert them to actual numbers.

---

### Python Is Object-Oriented — Casting Uses Constructor Functions

Python is built around a concept called **object-oriented programming**. Every piece of data in Python is an **object** (a specific instance of a class/type). Casting is done using **constructor functions** — functions that "construct" (build) a new object of a given type.

The three most common casting functions are:

| Function | What it does |
|---|---|
| `int()` | Constructs an integer |
| `float()` | Constructs a float |
| `str()` | Constructs a string |

---

### Casting to Integer with `int()`

The `int()` function can create an integer from:
- An integer literal (just wraps it)
- A float (removes the decimal — truncates)
- A string that contains a whole number (like `"3"`)

**Examples:**

```python
x = int(1)    # from int  → x = 1
y = int(2.8)  # from float → y = 2  (decimal removed!)
z = int("3")  # from str  → z = 3

print(x)   # 1
print(y)   # 2
print(z)   # 3
```

**Expected output:**
```
1
2
3
```

> **Careful:** `int("3.5")` will cause an error because `"3.5"` is not a whole number as text. Python cannot decide how to truncate from a string. You must first convert to float: `int(float("3.5"))` → `3`.

---

### Casting to Float with `float()`

The `float()` function can create a float from:
- An integer (adds `.0`)
- A float (leaves it as-is)
- A string representing a float or whole number

**Examples:**

```python
x = float(1)      # from int     → x = 1.0
y = float(2.8)    # from float   → y = 2.8
z = float("3")    # from str int → z = 3.0
w = float("4.2")  # from str flt → w = 4.2

print(x)   # 1.0
print(y)   # 2.8
print(z)   # 3.0
print(w)   # 4.2
```

**Expected output:**
```
1.0
2.8
3.0
4.2
```

---

### Casting to String with `str()`

The `str()` function converts almost anything into a text representation. This is very useful when you want to **display** a number inside a sentence.

**Examples:**

```python
x = str("s1")   # from str   → x = 's1'
y = str(2)       # from int   → y = '2'
z = str(3.0)     # from float → z = '3.0'

print(x)    # s1
print(y)    # 2
print(z)    # 3.0

print(type(x))   # <class 'str'>
print(type(y))   # <class 'str'>
print(type(z))   # <class 'str'>
```

**Expected output:**
```
s1
2
3.0
<class 'str'>
<class 'str'>
<class 'str'>
```

> **Why would you want to convert a number to a string?** Because you cannot join (concatenate) a number directly with text in Python. For example, `"Score: " + 95` will cause an error. You must write `"Score: " + str(95)` which gives `"Score: 95"`.

---

### Casting Summary Table

| From / To | `int()` | `float()` | `str()` |
|---|---|---|---|
| `int` | same | adds `.0` | text version |
| `float` | truncates decimal | same | text version |
| `str` (whole number like `"3"`) | number | number | same |
| `str` (float like `"3.5"`) | ❌ Error | number | same |
| `complex` | ❌ Error | ❌ Error | text version |

---

## Part 4 – Python Booleans

### What Is a Boolean?

A **Boolean** is the simplest data type in programming. It can only ever have **one of two values**:

- `True`
- `False`

Nothing else. Not "maybe". Not "sometimes". Just True or False.

**Analogy:** Think of a light switch. It is either ON or OFF. There is no middle ground. A Boolean in Python works exactly like a light switch.

**Where are Booleans used?**

Booleans are the foundation of **decision-making** in programs. Every time your program decides to do one thing or another — "if the student passed, print congratulations; otherwise, print try again" — it uses a Boolean to make that decision.

Real-world examples:
- Is the user logged in? `True` / `False`
- Is the temperature above 40°C? `True` / `False`
- Is the student's grade above 50? `True` / `False`
- Is the bank account balance below zero? `True` / `False`

---

### Writing Boolean Values

Booleans are written with a capital first letter:

```python
is_raining = True
is_sunny   = False

print(is_raining)    # True
print(is_sunny)      # False
print(type(is_raining))   # <class 'bool'>
```

**Expected output:**
```
True
False
<class 'bool'>
```

> **Common beginner mistake:** Writing `true` or `false` in lowercase. Python will not recognise them — they must be `True` and `False` with capital letters.

---

### Evaluating Expressions — Python Returns True or False

When you **compare** two values using a comparison operator, Python evaluates the comparison and returns a Boolean answer.

**Comparison operators:**

| Operator | Meaning |
|---|---|
| `>` | greater than |
| `<` | less than |
| `==` | equal to (note: two equals signs!) |
| `!=` | not equal to |
| `>=` | greater than or equal to |
| `<=` | less than or equal to |

**Simple example:**

```python
print(10 > 9)    # Is 10 greater than 9?
print(10 == 9)   # Is 10 equal to 9?
print(10 < 9)    # Is 10 less than 9?
```

**Expected output:**
```
True
False
False
```

Line by line:
- `10 > 9` → Yes, 10 is greater than 9 → `True`
- `10 == 9` → No, 10 is not equal to 9 → `False`
- `10 < 9` → No, 10 is not less than 9 → `False`

> **Important:** Notice the double equals `==` for comparison. A single `=` is for **assigning** a value to a variable. `==` is for **checking** if two values are equal. Confusing these is one of the most common beginner mistakes!

---

### Using Booleans in `if` Statements

The real power of Booleans shows up when you use them to make decisions with `if` statements.

**Example:**

```python
a = 200
b = 33

if b > a:
    print("b is greater than a")
else:
    print("b is not greater than a")
```

**Expected output:**
```
b is not greater than a
```

Here is what happens step by step:
1. Python evaluates `b > a` → `33 > 200` → `False`
2. Because the condition is `False`, Python skips the `if` block
3. Python runs the `else` block instead and prints the message

---

### The `bool()` Function

Just like `int()` and `float()`, Python has a `bool()` function that evaluates any value and tells you whether it is `True` or `False`.

**Simple example:**

```python
print(bool("Hello"))   # True
print(bool(15))        # True
```

**Expected output:**
```
True
True
```

You can also evaluate variables:

```python
x = "Hello"
y = 15

print(bool(x))    # True
print(bool(y))    # True
```

**Expected output:**
```
True
True
```

---

### The Big Rule: Most Values Are True

Almost every value in Python evaluates to `True` — if it has any content at all.

**What is always True?**
- Any non-empty string: `"hello"`, `"a"`, `"  "` (even a space!)
- Any non-zero number: `1`, `-5`, `0.01`, `3.14`
- Any non-empty list, tuple, set, or dictionary

```python
print(bool("abc"))                     # True
print(bool(123))                       # True
print(bool(["apple", "cherry"]))       # True
```

**Expected output:**
```
True
True
True
```

---

### Some Values Are False

Only a very small set of values evaluate to `False`:

| Value | Why it is False |
|---|---|
| `False` | It is the False keyword itself |
| `None` | It represents "nothing" |
| `0` | Zero (the only false number) |
| `0.0` | Zero as a float |
| `""` | Empty string |
| `()` | Empty tuple |
| `[]` | Empty list |
| `{}` | Empty dictionary or set |

**Example:**

```python
print(bool(False))   # False
print(bool(None))    # False
print(bool(0))       # False
print(bool(""))      # False
print(bool(()))      # False
print(bool([]))      # False
print(bool({}))      # False
```

**Expected output:**
```
False
False
False
False
False
False
False
```

**Memory trick:** If a value is **empty or zero or nothing**, it is `False`. Everything else is `True`.

---

### Objects with `__len__` Returning 0

There is one more advanced case. If you create your own class (a blueprint for objects) and it has a special function called `__len__` that returns `0`, then any object of that class will evaluate to `False`.

```python
class myclass():
    def __len__(self):
        return 0

myobj = myclass()
print(bool(myobj))   # False
```

**Expected output:**
```
False
```

> **Beginner note:** You do not need to fully understand classes yet. This example just shows you that Python's True/False system is flexible and programmers can customise it.

---

### Functions Can Return Boolean Values

You can write your own functions that return `True` or `False`. This is extremely useful in real programs.

**Simple example:**

```python
def myFunction():
    return True

print(myFunction())   # True
```

**Expected output:**
```
True
```

**Using a Boolean-returning function in a decision:**

```python
def myFunction():
    return True

if myFunction():
    print("YES!")
else:
    print("NO!")
```

**Expected output:**
```
YES!
```

**Real-world example — a pass/fail check:**

```python
def passed_exam(score):
    return score >= 50

print(passed_exam(72))    # True
print(passed_exam(45))    # False

if passed_exam(72):
    print("Congratulations, you passed!")
else:
    print("Keep studying, you can do it!")
```

**Expected output:**
```
True
False
Congratulations, you passed!
```

---

### The `isinstance()` Function

Python has a powerful built-in function called `isinstance()` that checks whether a variable is of a specific data type. It returns `True` or `False`.

**Syntax:**
```python
isinstance(variable, type)
```

**Examples:**

```python
x = 200
print(isinstance(x, int))     # True  — x is an int

y = 3.14
print(isinstance(y, float))   # True  — y is a float

z = "hello"
print(isinstance(z, str))     # True  — z is a str
print(isinstance(z, int))     # False — z is NOT an int
```

**Expected output:**
```
True
True
True
False
```

**Why is `isinstance()` useful?** In real programs, you often receive data from users or files and you need to verify the type before doing calculations. For example, you would not want to do maths on a string by accident.

---

## Guided Practice Exercises

### Exercise 1 — Identifying Types

**Objective:** Use `type()` to identify the data type of various values.

**Scenario:** You are a data analyst checking a dataset before processing it.

**Steps:**

1. Assign the following values to variables:
   - `product = "Rice"`
   - `price = 850`
   - `weight = 2.5`
   - `in_stock = True`
   - `discount = None`

2. Print the type of each variable.

**Starter code:**

```python
product = "Rice"
price = 850
weight = 2.5
in_stock = True
discount = None

print(type(product))
print(type(price))
print(type(weight))
print(type(in_stock))
print(type(discount))
```

**Expected output:**
```
<class 'str'>
<class 'int'>
<class 'float'>
<class 'bool'>
<class 'NoneType'>
```

**Self-check questions:**
- Why is `850` an `int` but `2.5` is a `float`?
- What would happen to the type of `price` if you changed it to `850.0`?
- What does `NoneType` mean in everyday terms?

---

### Exercise 2 — Working with Numbers

**Objective:** Create and work with all three number types.

**Scenario:** A science student needs to record measurements from three different experiments.

**Steps:**

1. Create an integer for the number of samples: `samples = 150`
2. Create a float for the temperature reading: `temp = 36.6`
3. Create a complex number for an electrical value: `impedance = 4 + 3j`
4. Create a float using scientific notation for a very small quantity: `mass = 9.11e-31` (mass of an electron in kg)
5. Print each variable and its type.

```python
samples   = 150
temp      = 36.6
impedance = 4 + 3j
mass      = 9.11e-31

print(samples, type(samples))
print(temp, type(temp))
print(impedance, type(impedance))
print(mass, type(mass))
```

**Expected output:**
```
150 <class 'int'>
36.6 <class 'float'>
(4+3j) <class 'complex'>
9.11e-31 <class 'float'>
```

**What-if challenge:** What happens if you change `samples = 150` to `samples = 150.0`? Run it and observe.

---

### Exercise 3 — Type Casting Practice

**Objective:** Convert between types using `int()`, `float()`, and `str()`.

**Scenario:** A school system stores scores as strings (from a CSV file) and you must convert them for calculations.

```python
# Scores stored as strings (from a CSV file)
score1 = "85"
score2 = "92"
score3 = "78"

# Step 1: Convert to integers
score1_num = int(score1)
score2_num = int(score2)
score3_num = int(score3)

# Step 2: Calculate average
average = (score1_num + score2_num + score3_num) / 3

# Step 3: Display result as a sentence (cast float to str)
print("Average score: " + str(average))
print("Data type of average: " + str(type(average)))
```

**Expected output:**
```
Average score: 85.0
Data type of average: <class 'float'>
```

**Self-check questions:**
- Why is the average `85.0` and not `85`? (Hint: what does division always return in Python 3?)
- What would happen if you tried `int(score1) + score2` directly?

---

### Exercise 4 — Boolean Evaluation

**Objective:** Evaluate different values using `bool()` and understand True/False rules.

**Scenario:** A shop inventory checker decides if items are in stock.

```python
# Test different values
stock_count = 0
item_name = ""
price = 25.99
available_sizes = ["S", "M", "L"]

print("Stock count:", bool(stock_count))       # False — zero
print("Item name:", bool(item_name))            # False — empty string
print("Price:", bool(price))                    # True — non-zero
print("Sizes:", bool(available_sizes))          # True — non-empty list

# Decision
if bool(available_sizes):
    print("This item is available in multiple sizes.")
else:
    print("No sizes available.")
```

**Expected output:**
```
Stock count: False
Item name: False
Price: True
Sizes: True
This item is available in multiple sizes.
```

---

## Mini-Project — Student Report Card Analyser

Now you will bring everything together in one realistic project.

### Project Description

You will write a Python program that:
1. Stores student information using appropriate data types
2. Converts scores from strings to numbers (casting)
3. Calculates averages
4. Evaluates pass/fail using Booleans
5. Generates a random bonus question score
6. Displays a formatted report

---

### Stage 1 – Setup: Store Student Data

```python
import random

# Student information — different data types
student_name   = "Amara Johnson"      # str
student_id     = 2024001              # int
is_enrolled    = True                 # bool

# Scores stored as strings (simulating data from a file)
math_score     = "78"
english_score  = "85"
science_score  = "91"

print("=== STUDENT REPORT CARD ===")
print("Name:", student_name)
print("ID:", student_id)
print("Enrolled:", is_enrolled)
```

**Milestone output:**
```
=== STUDENT REPORT CARD ===
Name: Amara Johnson
ID: 2024001
Enrolled: True
```

---

### Stage 2 – Core Logic: Cast and Calculate

```python
# Cast string scores to integers
math    = int(math_score)
english = int(english_score)
science = int(science_score)

# Generate a random bonus score (0 to 5)
bonus = random.randrange(0, 6)

# Calculate total and average
total   = math + english + science + bonus
average = float(total) / 4   # divide by 4 subjects including bonus

print("\nSubject Scores:")
print("  Mathematics:", math)
print("  English:", english)
print("  Science:", science)
print("  Bonus Question:", bonus)
print("  Total:", total)
print("  Average:", average)
```

**Milestone output (bonus varies):**
```
Subject Scores:
  Mathematics: 78
  English: 85
  Science: 91
  Bonus Question: 3
  Total: 257
  Average: 64.25
```

---

### Stage 3 – Enhancements: Boolean Pass/Fail

```python
# Determine pass or fail (pass mark is 50)
passed = average >= 50

print("\nResult:")
print("  Passed:", passed)

if passed:
    print("  Status: CONGRATULATIONS! You have passed.")
else:
    print("  Status: You did not pass. Keep working hard!")

# Check if any score is below 50 (danger zone)
any_failed_subject = (math < 50) or (english < 50) or (science < 50)

if any_failed_subject:
    print("  Warning: One or more subjects need improvement.")
else:
    print("  All individual subjects passed.")
```

**Milestone output:**
```
Result:
  Passed: True
  Status: CONGRATULATIONS! You have passed.
  All individual subjects passed.
```

---

### Stage 4 – Final Output: Full Report with `isinstance()` Check

```python
# Verify types using isinstance
print("\n--- Type Verification ---")
print("Name is str:", isinstance(student_name, str))
print("ID is int:", isinstance(student_id, int))
print("Average is float:", isinstance(average, float))
print("Passed is bool:", isinstance(passed, bool))

# Final grade letter
if average >= 70:
    grade = "A"
elif average >= 60:
    grade = "B"
elif average >= 50:
    grade = "C"
else:
    grade = "F"

print("\nFinal Grade:", grade)
print("=== END OF REPORT ===")
```

**Final expected output (example with bonus = 3):**
```
--- Type Verification ---
Name is str: True
ID is int: True
Average is float: True
Passed is bool: True

Final Grade: B
=== END OF REPORT ===
```

---

### Complete Project Code

```python
import random

# Stage 1: Setup
student_name   = "Amara Johnson"
student_id     = 2024001
is_enrolled    = True
math_score     = "78"
english_score  = "85"
science_score  = "91"

print("=== STUDENT REPORT CARD ===")
print("Name:", student_name)
print("ID:", student_id)
print("Enrolled:", is_enrolled)

# Stage 2: Cast and Calculate
math    = int(math_score)
english = int(english_score)
science = int(science_score)
bonus   = random.randrange(0, 6)
total   = math + english + science + bonus
average = float(total) / 4

print("\nSubject Scores:")
print("  Mathematics:", math)
print("  English:", english)
print("  Science:", science)
print("  Bonus Question:", bonus)
print("  Total:", total)
print("  Average:", average)

# Stage 3: Boolean Pass/Fail
passed = average >= 50
print("\nResult:")
print("  Passed:", passed)

if passed:
    print("  Status: CONGRATULATIONS! You have passed.")
else:
    print("  Status: You did not pass. Keep working hard!")

any_failed_subject = (math < 50) or (english < 50) or (science < 50)
if any_failed_subject:
    print("  Warning: One or more subjects need improvement.")
else:
    print("  All individual subjects passed.")

# Stage 4: Type verification and final grade
print("\n--- Type Verification ---")
print("Name is str:", isinstance(student_name, str))
print("ID is int:", isinstance(student_id, int))
print("Average is float:", isinstance(average, float))
print("Passed is bool:", isinstance(passed, bool))

if average >= 70:
    grade = "A"
elif average >= 60:
    grade = "B"
elif average >= 50:
    grade = "C"
else:
    grade = "F"

print("\nFinal Grade:", grade)
print("=== END OF REPORT ===")
```

**Reflection questions:**
- What would happen if you removed the `int()` casting and tried to add the score strings together?
- Why is `average` a float and not an integer?
- What happens to the output if `bonus` is `0`?
- How would you modify this program to handle four subjects plus the bonus?

**Optional extension:** Add a second student and compare their averages. Print who scored higher.

---

## Common Beginner Mistakes

### Mistake 1 — Lowercase `true` and `false`

```python
# WRONG:
result = true     # NameError: name 'true' is not defined

# CORRECT:
result = True
```

### Mistake 2 — Confusing `=` and `==`

```python
# WRONG — this assigns 10 to x, it does not compare:
if x = 10:        # SyntaxError

# CORRECT — this checks if x equals 10:
if x == 10:
    print("x is 10")
```

### Mistake 3 — Expecting `int(2.8)` to Round Up

```python
# WRONG assumption:
x = int(2.8)
print(x)   # Many beginners expect 3

# ACTUAL output:
# 2   (Python truncates — it cuts, it does not round)
```

To round properly, use the `round()` function:
```python
x = round(2.8)
print(x)    # 3
```

### Mistake 4 — Trying to Concatenate a Number and a String Directly

```python
score = 85

# WRONG:
print("Your score is: " + score)   # TypeError!

# CORRECT — cast the number to string first:
print("Your score is: " + str(score))   # Your score is: 85
```

### Mistake 5 — Trying to Cast a Non-Numeric String to int

```python
# WRONG:
x = int("hello")   # ValueError — "hello" is not a number!

# CORRECT — only cast strings that actually contain numbers:
x = int("42")    # Fine → 42
```

### Mistake 6 — Trying to Convert Complex to int or float

```python
z = 3 + 5j

# WRONG:
x = int(z)    # TypeError — cannot convert complex to int

# Complex numbers can only be converted to str:
x = str(z)    # Fine → "(3+5j)"
```

### Mistake 7 — Assuming Empty String is True

```python
name = ""

# Many beginners expect this to print something:
if name:
    print("Name is set")
else:
    print("Name is empty")   # This prints — empty string is False!
```

---

## Reflection Questions

Think carefully about these questions. Try to answer them before looking back at the lesson.

1. Why does Python need different data types? Could everything just be a string?
2. What is the difference between `int(2.9)` and `round(2.9)`?
3. If you have `x = "50"` and `y = 50`, are they the same? How would you check?
4. Why does `bool(0)` return `False` but `bool(0.01)` return `True`?
5. Can a function return both `True` and `False` depending on the input? Write a simple example in your head.
6. What would happen if you accidentally stored someone's age as `"25"` (a string) and tried to add `1` to it?
7. Why does Python use `j` for imaginary numbers instead of `i` as in mathematics?
8. If `bool([])` is `False` and `bool(["item"])` is `True`, what does this tell you about how Python treats collections?

---

## Completion Checklist

Go through this checklist. Tick each item only when you can do it confidently:

- [ ] I can explain what a data type is in my own words
- [ ] I know all of Python's built-in data type categories
- [ ] I can use `type()` to check the type of any variable
- [ ] I know the difference between `int`, `float`, and `complex`
- [ ] I can write a float using scientific notation (e.g. `1.5e3`)
- [ ] I can use `int()`, `float()`, and `str()` to cast between types
- [ ] I understand that `int(2.8)` gives `2`, not `3`
- [ ] I know that complex numbers cannot be converted to int or float
- [ ] I can import the `random` module and generate a random number
- [ ] I know that `True` and `False` must start with capital letters
- [ ] I can use `bool()` to evaluate whether a value is True or False
- [ ] I know which values are always `False` (empty, zero, None)
- [ ] I can write a function that returns a Boolean value
- [ ] I can use `isinstance()` to check a variable's type
- [ ] I completed the Student Report Card mini-project

---

## Lesson Summary

In this lesson, you covered four closely connected topics that form the foundation of every Python program.

**Data Types** tell Python what kind of value a variable holds. Python automatically assigns the type when you assign a value, but you can check it with `type()` and explicitly set it with constructor functions. Python has types for text (`str`), numbers (`int`, `float`, `complex`), collections (`list`, `tuple`, `dict`, `set`), logic (`bool`), and more.

**Numbers** come in three forms. Integers (`int`) are whole numbers of unlimited size. Floats (`float`) have decimal points and can be written in scientific notation (e.g. `3.5e4`). Complex numbers (`complex`) have real and imaginary parts written with `j`. You can convert between int, float, and complex — but not from complex back to int or float.

**Casting** is the process of changing a value from one type to another. This is essential when data arrives in the wrong format, such as numbers stored as strings. `int()` truncates decimals (does not round). `float()` adds decimal precision. `str()` converts anything to text for display purposes.

**Booleans** are the simplest type — only `True` or `False`. They are the engine of every decision in a program. Python evaluates expressions and returns a Boolean. Nearly everything is `True` in Python; only empty values, zero, `None`, and `False` itself are `False`. The `bool()` function, comparison operators, `isinstance()`, and user-defined functions all produce Boolean results.

Together, these four concepts let you store the right kind of data, convert it when needed, and make decisions based on its value — the core of all programming logic.

---

*Sources: W3Schools Python Tutorial — Data Types, Numbers, Casting, and Booleans*
