---
render_with_liquid: false
title: "Lesson 05 – Python Data Types"
nav_order: 5
---

# Lesson 05 – Python Data Types

---

## Lesson Introduction

Imagine you are packing boxes before moving house. You would not throw your clothes, your eggs, your books, and your tools all into the same box — each category of item needs its own kind of container so it can be handled properly. Shirts fold, eggs need padding, books stack flat, and tools need to be wrapped so they do not damage anything else.

Python thinks the same way about **data**.

Every piece of data you give Python — a name, a number, a list of items, a yes/no answer — belongs to a particular **data type**. The data type tells Python exactly what kind of "box" the value lives in, what it can do, and how it behaves.

Understanding data types is one of the most important foundations in programming. Get this right, and everything else — variables, calculations, conditions, loops, functions — will make much more sense.

In this lesson you will learn:
- What a data type is and why Python uses them
- All the built-in data types Python provides, with clear explanations and examples
- What a **variable** is (a prerequisite concept — explained from scratch)
- How to use `type()` to find out what data type you are working with
- How Python sets the data type automatically when you assign a value
- How to **force** a specific data type using constructor functions
- Real-world examples of where each data type is used

---

## Prerequisite Concepts

Before we begin, let us make sure two important concepts are clear. You need to understand both of these before data types will make sense.

---

### What is a Variable?

A **variable** is a named storage location in your program. Think of it like a labelled jar on a shelf. You put something inside the jar, label it with a name, and then later you can pick it up by that name whenever you need it.

```python
age = 25
```

Here:
- `age` is the **variable name** (the label on the jar)
- `=` is the **assignment operator** — it puts a value into the variable
- `25` is the **value** being stored

From this moment on, whenever your program sees the word `age`, it fetches the value `25` from that jar.

```python
age = 25
print(age)
```

**Expected Output:**
```
25
```

You can store any kind of value in a variable — a word, a number, a list, anything. The kind of value you put in determines the **data type** of that variable.

---

### What is a Value?

A **value** is the actual piece of data — the thing you are working with. Examples of values include `"Hello"`, `42`, `3.14`, `True`, and `["apples", "bananas"]`. Every value has a data type that describes what kind of thing it is.

---

## What is a Data Type?

A **data type** is a classification — a label that tells Python what *kind* of data a value is.

Why does this matter? Because Python needs to know the type of a value before it can decide what to do with it.

Consider the `+` symbol. If you use it with numbers, Python adds them together. But if you use it with words (strings), Python *joins* them together:

```python
print(5 + 3)          # Adds two numbers
print("Hello" + " World")   # Joins two pieces of text
```

**Expected Output:**
```
8
Hello World
```

Python knows to add in the first case and join in the second because it knows the **data type** of each value. Without data types, Python would not know the difference between the number `5` and the text `"5"`.

> 💡 **Real-World Analogy:** Think of data types like the categories on a library shelf. Books, DVDs, maps, and magazines are all physical objects — but the library stores them differently, labels them differently, and handles them by different rules. Data types are Python's "shelf categories" for values.

---

## All of Python's Built-in Data Types

Python comes with many built-in data types, organised into categories. Here is the complete overview:

| Category | Data Type(s) | What it stores |
|---|---|---|
| **Text** | `str` | Words, sentences, characters |
| **Numeric** | `int`, `float`, `complex` | Whole numbers, decimal numbers, complex numbers |
| **Sequence** | `list`, `tuple`, `range` | Ordered collections of items |
| **Mapping** | `dict` | Key-value pairs (like a phone book) |
| **Set** | `set`, `frozenset` | Unordered unique collections |
| **Boolean** | `bool` | True or False only |
| **Binary** | `bytes`, `bytearray`, `memoryview` | Raw binary data |
| **None** | `NoneType` | The absence of a value |

Do not worry — we are going to explore every single one of these with clear examples. The most important ones for beginners are `str`, `int`, `float`, `bool`, `list`, `tuple`, `dict`, and `set`. The binary types are advanced and mostly used in specialised technical work.

---

## Using `type()` to Find the Data Type

Before we explore each type, learn this one essential tool: the `type()` function.

### What is `type()`?

`type()` is a built-in Python function that tells you the data type of any value or variable. You hand it something, and it tells you exactly what kind of thing it is.

```python
x = 5
print(type(x))
```

**Expected Output:**
```
<class 'int'>
```

**Breaking this down:**
- `x = 5` → stores the value `5` in a variable called `x`
- `type(x)` → asks Python: "what type of thing is `x`?"
- `print(...)` → displays the answer on screen
- The output `<class 'int'>` means: "this is an integer (whole number)"

The word `class` in the output is Python's internal way of categorising types — for now, read `<class 'int'>` as simply "this is an int".

> 💡 **`type()` is your detective tool.** Whenever you are unsure what kind of data you are working with, use `type()` to find out instantly.

---

### Quick `type()` Demos

```python
print(type("Hello"))
print(type(42))
print(type(3.14))
print(type(True))
```

**Expected Output:**
```
<class 'str'>
<class 'int'>
<class 'float'>
<class 'bool'>
```

Each one gives you a clear label for the type of value you are working with.

> 💡 **Thinking Prompt:** What do you think `type("99")` would output? Is `"99"` a number or text? Think carefully — remember those quotes!

---

## Part 1 – Text Type: `str` (String)

### What is a String?

A **string** is any sequence of characters — letters, spaces, digits, punctuation — all wrapped together inside quotation marks.

The word comes from "a string of characters", like beads on a necklace. The necklace holds all the beads in order.

**Examples of strings:**
- `"Hello, World!"`
- `"My name is Amara"`
- `"The temperature is 28 degrees"`
- `"Python3"` ← even though it contains the number 3, it is a string because of the quotes
- `""` ← an empty string (a necklace with no beads — valid but empty)

### Setting a String Variable

```python
x = "Hello World"
print(x)
print(type(x))
```

**Expected Output:**
```
Hello World
<class 'str'>
```

### Two More String Examples

```python
name = "Chukwuemeka"
print(name)
print(type(name))
```

**Expected Output:**
```
Chukwuemeka
<class 'str'>
```

```python
city = 'Lagos'
print(city)
print(type(city))
```

**Expected Output:**
```
Lagos
<class 'str'>
```

Both double quotes `"..."` and single quotes `'...'` create strings.

### Real-World Use of Strings

Strings are used everywhere:
- Storing names, addresses, messages in a user database
- Displaying error messages in an application
- Reading text from a file or website
- Sending email subject lines
- Storing DNA sequences in bioinformatics (`"ATCGGCTA..."`)
- Representing any data that is fundamentally text-based

---

## Part 2 – Numeric Types: `int`, `float`, `complex`

Python has three types for storing numbers, depending on what kind of number you need.

---

### 2a – `int` (Integer — Whole Numbers)

An **integer** is any whole number — positive, negative, or zero. No decimal points allowed.

Think of integers as the numbers you would count on your fingers: 1, 2, 3... or backwards: -1, -2, -3... or exactly zero.

**Examples:** `0`, `1`, `-5`, `100`, `1000000`, `-999`

```python
x = 20
print(x)
print(type(x))
```

**Expected Output:**
```
20
<class 'int'>
```

```python
temperature = -7
print(temperature)
print(type(temperature))
```

**Expected Output:**
```
-7
<class 'int'>
```

**Real-World Use of int:**
- Number of students in a class: `students = 32`
- Age: `age = 17`
- Score in a game: `score = 1500`
- Number of items in stock: `stock = 247`
- Year: `year = 2024`

> 💡 **Thinking Prompt:** If you write `x = 100`, what type is `x`? What if you write `x = "100"`? Are they the same? Why not?

---

### 2b – `float` (Floating-Point — Decimal Numbers)

A **float** is any number with a decimal point. The name comes from "floating point", which refers to how computers represent decimal numbers internally (the decimal "floats" to different positions).

Think of floats as any measurement that needs precision: a temperature of 36.6°C, a price of ₦1,249.50, a height of 1.75 metres.

**Examples:** `3.14`, `0.5`, `-2.7`, `100.0`, `0.001`

```python
x = 20.5
print(x)
print(type(x))
```

**Expected Output:**
```
20.5
<class 'float'>
```

```python
pi = 3.14159
print(pi)
print(type(pi))
```

**Expected Output:**
```
3.14159
<class 'float'>
```

> ⚠️ **Important:** Even `100.0` is a float, not an int — the presence of the decimal point is what makes it a float, regardless of whether the decimal part is zero.

```python
price = 100.0
print(type(price))
```

**Expected Output:**
```
<class 'float'>
```

**Real-World Use of float:**
- Prices: `item_price = 4.99`
- Scientific measurements: `weight_kg = 72.3`
- GPS coordinates: `latitude = 6.5244`
- Percentage: `pass_rate = 87.5`
- Division results: `10 / 3` produces `3.3333...` — a float

---

### 2c – `complex` (Complex Numbers)

A **complex number** has two parts: a **real part** and an **imaginary part**. In Python, the imaginary part is written with a `j` suffix.

This is an advanced mathematical type used in fields like electrical engineering, signal processing, quantum physics, and advanced mathematics. If you are a beginner, you do not need to use this type yet — just know it exists.

**Example:** `1j`, `3+5j`, `2-4j`

```python
x = 1j
print(x)
print(type(x))
```

**Expected Output:**
```
1j
<class 'complex'>
```

```python
z = 3 + 5j
print(z)
print(type(z))
```

**Expected Output:**
```
(3+5j)
<class 'complex'>
```

**Real-World Use of complex:** Electrical engineers use complex numbers to represent AC voltage and current. Data scientists use them in Fourier transforms for audio and image processing.

---

## Part 3 – Sequence Types: `list`, `tuple`, `range`

Sequence types store **multiple items in a specific order**. Think of them as different kinds of containers that hold a collection of values.

---

### 3a – `list`

A **list** is an ordered collection of items that you **can change** (add to, remove from, or modify). Lists are written using square brackets `[...]` with items separated by commas.

Think of a list like a shopping list written on paper — you can cross things off, add new items, and rearrange the order.

```python
x = ["apple", "banana", "cherry"]
print(x)
print(type(x))
```

**Expected Output:**
```
['apple', 'banana', 'cherry']
<class 'list'>
```

A list can hold items of different types:

```python
mixed_list = ["Amara", 17, 3.14, True]
print(mixed_list)
print(type(mixed_list))
```

**Expected Output:**
```
['Amara', 17, 3.14, True]
<class 'list'>
```

**Real-World Use of list:**
- A list of student names in a class
- A list of product names in a shop
- Daily temperatures recorded over a week: `[28, 31, 27, 29, 30, 33, 26]`
- A to-do list in an app
- Search results returned from a database

---

### 3b – `tuple`

A **tuple** is like a list, but it is **fixed** — once created, you cannot change its contents. Tuples are written with round brackets `(...)`.

Think of a tuple like a printed, laminated card. The information is set, sealed, and permanent. You can read it, but you cannot cross things out or write new things on it.

```python
x = ("apple", "banana", "cherry")
print(x)
print(type(x))
```

**Expected Output:**
```
('apple', 'banana', 'cherry')
<class 'tuple'>
```

**Why use a tuple instead of a list?**
Because permanence is sometimes a feature, not a bug. If you have a set of values that should never change — like the days of the week, or a set of GPS coordinates for a fixed location — a tuple protects that data from accidental modification.

**Real-World Use of tuple:**
- Days of the week: `("Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun")`
- RGB colour values: `(255, 128, 0)` — red, green, blue values that define a colour
- A fixed pair of coordinates: `(latitude, longitude)`
- Return values from a function that gives multiple results

---

### 3c – `range`

A **range** represents a sequence of numbers, generated on demand. Instead of storing all the numbers, it just remembers the start, stop, and step, and produces each number when needed.

`range(6)` means: "give me the numbers 0, 1, 2, 3, 4, 5" — starting from 0, up to but not including 6.

```python
x = range(6)
print(x)
print(type(x))
```

**Expected Output:**
```
range(0, 6)
<class 'range'>
```

To see all the values, convert it to a list:

```python
print(list(range(6)))
```

**Expected Output:**
```
[0, 1, 2, 3, 4, 5]
```

**Real-World Use of range:**
- Looping a certain number of times: "repeat this action 10 times"
- Generating a series of numbers for a data table
- Creating row numbers for a spreadsheet report

---

## Part 4 – Mapping Type: `dict` (Dictionary)

### What is a Dictionary?

A **dict** (short for **dictionary**) stores data as **key-value pairs**. Think of it like a real dictionary: you look up a word (the **key**), and you find its definition (the **value**).

Or think of a phone book: you look up a person's name (key), and you find their phone number (value).

Dicts are written using curly braces `{...}` with `key: value` pairs separated by commas.

```python
x = {"name": "John", "age": 36}
print(x)
print(type(x))
```

**Expected Output:**
```
{'name': 'John', 'age': 36}
<class 'dict'>
```

Here, `"name"` is a key and `"John"` is its value. `"age"` is a key and `36` is its value.

```python
student = {"name": "Fatima", "score": 91, "grade": "A"}
print(student)
print(type(student))
```

**Expected Output:**
```
{'name': 'Fatima', 'score': 91, 'grade': 'A'}
<class 'dict'>
```

**Real-World Use of dict:**
- A student's profile: name, age, score, class
- Product information: name, price, stock count, category
- Settings in an application: font size, theme colour, language
- JSON data from a web API (nearly all web data is structured like a dict)
- A contact in a phonebook app

---

## Part 5 – Set Types: `set` and `frozenset`

### What is a Set?

A **set** is an unordered collection of **unique** items. Unlike lists, sets automatically remove duplicates. Sets are written with curly braces `{...}`.

Think of a set like a bag of unique coloured marbles — you cannot have two identical marbles, and the bag does not keep them in any particular order.

```python
x = {"apple", "banana", "cherry"}
print(x)
print(type(x))
```

**Expected Output:**
```
{'cherry', 'banana', 'apple'}
<class 'set'>
```

> ⚠️ **Notice:** The output order may differ from what you typed — sets are **unordered**. Python does not guarantee any particular display order for sets.

**Automatic duplicate removal:**

```python
fruits = {"apple", "banana", "apple", "cherry", "banana"}
print(fruits)
```

**Expected Output:**
```
{'cherry', 'banana', 'apple'}
```

Python silently removed the duplicates. Only unique items remain.

**Real-World Use of set:**
- Getting a list of unique visitors to a website
- Checking which items appear in both of two lists (intersection)
- Removing duplicates from a data column in data analysis
- Finding unique words in a document (text analysis)

---

### `frozenset`

A **frozenset** is exactly like a `set`, but **frozen** (immutable — cannot be changed after creation). Just as a tuple is the immutable version of a list, a frozenset is the immutable version of a set.

```python
x = frozenset({"apple", "banana", "cherry"})
print(x)
print(type(x))
```

**Expected Output:**
```
frozenset({'cherry', 'banana', 'apple'})
<class 'frozenset'>
```

**Real-World Use of frozenset:** Useful when you need a set that serves as a dictionary key (regular sets cannot be dict keys because they are mutable, but frozensets can).

---

## Part 6 – Boolean Type: `bool`

### What is a Boolean?

A **boolean** (`bool`) is the simplest possible data type — it can only ever hold one of two values: `True` or `False`.

Think of a boolean like a light switch — it is either on (`True`) or off (`False`). Nothing in between.

The name comes from mathematician George Boole, who developed the algebra of logic (Boolean algebra) in the 1800s.

```python
x = True
print(x)
print(type(x))
```

**Expected Output:**
```
True
<class 'bool'>
```

```python
is_raining = False
print(is_raining)
print(type(is_raining))
```

**Expected Output:**
```
False
<class 'bool'>
```

> ⚠️ **Critical:** In Python, `True` and `False` must begin with a **capital letter**. Writing `true` or `false` (lowercase) will cause an error — Python will not recognise them.

**Wrong:**
```python
x = true    # ❌ NameError: name 'true' is not defined
```

**Right:**
```python
x = True    # ✅ Correct
```

**Real-World Use of bool:**
- Is a user logged in? `is_logged_in = True`
- Has a payment been confirmed? `payment_confirmed = False`
- Is a student passing? `is_passing = True`
- Did the file upload successfully? `upload_success = True`
- Controlling `if` statements and conditions — booleans are the backbone of all decision-making in programming

---

## Part 7 – Binary Types: `bytes`, `bytearray`, `memoryview`

These types deal with **raw binary data** — the 0s and 1s that computers use at the lowest level. They are advanced types used in specific technical work.

### `bytes`

A `bytes` object stores a sequence of integers (0–255), representing raw binary data. Once created, it cannot be changed.

```python
x = b"Hello"
print(x)
print(type(x))
```

**Expected Output:**
```
b'Hello'
<class 'bytes'>
```

The `b` prefix before the quotes tells Python this is bytes, not a regular string.

**Real-World Use:** Reading binary files (images, audio), network communication, cryptography, encoding data for transmission.

---

### `bytearray`

A `bytearray` is like `bytes` but **mutable** — you can change individual bytes after creation.

```python
x = bytearray(5)
print(x)
print(type(x))
```

**Expected Output:**
```
bytearray(b'\x00\x00\x00\x00\x00')
<class 'bytearray'>
```

`bytearray(5)` creates a bytearray of 5 zero bytes (`\x00` is hexadecimal for zero).

**Real-World Use:** Modifying binary file contents, building network packets, image processing at the pixel level.

---

### `memoryview`

A `memoryview` provides a way to access the memory of another binary object (like `bytes` or `bytearray`) without copying it. This is used for efficiency when working with very large binary data.

```python
x = memoryview(bytes(5))
print(x)
print(type(x))
```

**Expected Output:**
```
<memory at 0x...>
<class 'memoryview'>
```

**Real-World Use:** High-performance data processing, scientific computing, working with large binary arrays without expensive memory copies.

> 💡 **Beginner note:** You will rarely use binary types as a beginner. They become relevant in systems programming, data engineering, and low-level work. For now, just know they exist.

---

## Part 8 – None Type: `NoneType`

### What is `None`?

`None` is Python's way of representing **nothing** — the intentional absence of a value. It is not zero, not an empty string, not `False`. It is specifically the concept of "no value here".

Think of `None` like an empty box with a label that says "intentionally empty". It is different from a box that contains a `0` (which is *something*) or a box containing an empty string `""` (still *something*, just empty text).

```python
x = None
print(x)
print(type(x))
```

**Expected Output:**
```
None
<class 'NoneType'>
```

> ⚠️ **Critical:** `None` must always start with a capital `N`. Writing `none` (lowercase) will cause an error.

**Real-World Use of None:**
- A function that does not return anything — its return value is `None`
- A database field that has no data entered yet
- A variable declared but not yet assigned a meaningful value
- Representing "no answer" in a quiz app when a user skips a question

---

## How Python Sets the Data Type Automatically

One of Python's most beginner-friendly features is **automatic type detection**. When you assign a value to a variable, Python looks at the value and automatically figures out what type it should be. You do not have to announce the type — Python reads the clue from the value itself.

Here are the rules Python uses:

| What you write | What Python reads | Data type assigned |
|---|---|---|
| `x = "Hello World"` | Sees quotes → text | `str` |
| `x = 20` | Sees a whole number | `int` |
| `x = 20.5` | Sees a decimal point | `float` |
| `x = 1j` | Sees `j` suffix | `complex` |
| `x = ["apple", "banana"]` | Sees `[...]` → square brackets | `list` |
| `x = ("apple", "banana")` | Sees `(...)` → round brackets | `tuple` |
| `x = range(6)` | Sees `range(...)` call | `range` |
| `x = {"name": "John"}` | Sees `{key: value}` pairs | `dict` |
| `x = {"apple", "banana"}` | Sees `{...}` no colons | `set` |
| `x = frozenset({"apple"})` | Sees `frozenset(...)` call | `frozenset` |
| `x = True` | Sees `True` or `False` keyword | `bool` |
| `x = b"Hello"` | Sees `b"..."` prefix | `bytes` |
| `x = bytearray(5)` | Sees `bytearray(...)` call | `bytearray` |
| `x = memoryview(bytes(5))` | Sees `memoryview(...)` call | `memoryview` |
| `x = None` | Sees `None` keyword | `NoneType` |

Let us verify a few of these with code:

```python
x = "Hello World"
print(type(x))

x = 20
print(type(x))

x = 20.5
print(type(x))

x = ["apple", "banana", "cherry"]
print(type(x))

x = ("apple", "banana", "cherry")
print(type(x))

x = {"name": "John", "age": 36}
print(type(x))

x = {"apple", "banana", "cherry"}
print(type(x))

x = True
print(type(x))

x = None
print(type(x))
```

**Expected Output:**
```
<class 'str'>
<class 'int'>
<class 'float'>
<class 'list'>
<class 'tuple'>
<class 'dict'>
<class 'set'>
<class 'bool'>
<class 'NoneType'>
```

> 💡 **Thinking Prompt:** In the code above, notice we re-used the variable name `x` for many different types. Each time we assigned a new value, the type of `x` changed! Python allows this — it is called **dynamic typing**. Some other languages require you to lock a variable to one type forever. Python is more flexible.

---

## How to Set a Specific Data Type (Constructor Functions)

Sometimes you want to be **explicit** — you want to tell Python exactly what type to use, rather than letting it guess. You do this using **constructor functions**.

A **constructor function** is a special function whose name is the same as the data type. You call it and pass your value inside it, and it creates a value of that specific type.

Here is the complete set of constructor functions:

| Constructor call | Data type produced |
|---|---|
| `str("Hello World")` | `str` |
| `int(20)` | `int` |
| `float(20.5)` | `float` |
| `complex(1j)` | `complex` |
| `list(("apple", "banana", "cherry"))` | `list` |
| `tuple(("apple", "banana", "cherry"))` | `tuple` |
| `range(6)` | `range` |
| `dict(name="John", age=36)` | `dict` |
| `set(("apple", "banana", "cherry"))` | `set` |
| `frozenset(("apple", "banana", "cherry"))` | `frozenset` |
| `bool(5)` | `bool` |
| `bytes(5)` | `bytes` |
| `bytearray(5)` | `bytearray` |
| `memoryview(bytes(5))` | `memoryview` |

Let us look at the most useful ones in detail:

---

### Using `str()` — Explicitly Create a String

```python
x = str("Hello World")
print(x)
print(type(x))
```

**Expected Output:**
```
Hello World
<class 'str'>
```

You can also convert a number to a string using `str()`:

```python
score = str(95)
print(score)
print(type(score))
```

**Expected Output:**
```
95
<class 'str'>
```

Now `score` holds the text `"95"`, not the number `95`. This is useful when you need to join a number with text using concatenation (covered in later lessons).

---

### Using `int()` — Explicitly Create an Integer

```python
x = int(20)
print(x)
print(type(x))
```

**Expected Output:**
```
20
<class 'int'>
```

You can convert a float to an int (this removes the decimal part — it does **not** round):

```python
x = int(9.9)
print(x)
```

**Expected Output:**
```
9
```

> ⚠️ `int(9.9)` gives `9`, not `10`. It always cuts off the decimal without rounding. This is called **truncation**.

---

### Using `float()` — Explicitly Create a Float

```python
x = float(20.5)
print(x)
print(type(x))
```

**Expected Output:**
```
20.5
<class 'float'>
```

You can convert an integer to a float:

```python
x = float(7)
print(x)
```

**Expected Output:**
```
7.0
```

The `.0` is added to show it is now a float.

---

### Using `bool()` — Explicitly Create a Boolean

```python
x = bool(5)
print(x)
print(type(x))
```

**Expected Output:**
```
True
<class 'bool'>
```

> 💡 **Interesting rule:** In Python, almost every non-zero, non-empty value converts to `True`. Zero, empty strings `""`, empty lists `[]`, and `None` all convert to `False`.

```python
print(bool(0))      # False — zero is "falsy"
print(bool(""))     # False — empty string is "falsy"
print(bool([]))     # False — empty list is "falsy"
print(bool(None))   # False — None is "falsy"
print(bool(1))      # True
print(bool("Hi"))   # True
print(bool([1, 2])) # True
```

**Expected Output:**
```
False
False
False
False
True
True
True
```

---

### Using `list()` — Convert to a List

```python
x = list(("apple", "banana", "cherry"))
print(x)
print(type(x))
```

**Expected Output:**
```
['apple', 'banana', 'cherry']
<class 'list'>
```

Notice: we passed a **tuple** `("apple", "banana", "cherry")` into `list()`, and Python converted it to a list. This is how you convert between sequence types.

---

### Using `dict()` — Create a Dictionary with Constructor

```python
x = dict(name="John", age=36)
print(x)
print(type(x))
```

**Expected Output:**
```
{'name': 'John', 'age': 36}
<class 'dict'>
```

Notice the syntax difference: inside `dict()`, you write `key=value` without quotes around the key name.

---

## Guided Practice Exercises

Work through each exercise carefully. Predict the output before running the code!

---

### Exercise 1 – Identify the Type

**Objective:** Build the habit of recognising data types from how they look.

Look at each value below. Without running any code, guess what type each one is. Then write the code to verify your guess using `type()`.

```python
a = "Ibadan"
b = 42
c = 3.14
d = True
e = ["Maths", "English", "Science"]
f = ("red", "green", "blue")
g = {"country": "Nigeria", "capital": "Abuja"}
h = None
```

**Your Verification Code:**
```python
a = "Ibadan"
b = 42
c = 3.14
d = True
e = ["Maths", "English", "Science"]
f = ("red", "green", "blue")
g = {"country": "Nigeria", "capital": "Abuja"}
h = None

print(type(a))
print(type(b))
print(type(c))
print(type(d))
print(type(e))
print(type(f))
print(type(g))
print(type(h))
```

**Expected Output:**
```
<class 'str'>
<class 'int'>
<class 'float'>
<class 'bool'>
<class 'list'>
<class 'tuple'>
<class 'dict'>
<class 'NoneType'>
```

**Self-check:** Did you guess all 8 correctly? Which ones surprised you?

---

### Exercise 2 – The Quote Trap

**Objective:** Understand the difference between a number and a number-as-text.

**Scenario:** A student is building a simple calculator. They write the following code. Predict what will happen — will it add, or will it join?

```python
a = "10"
b = "20"
print(a + b)
print(type(a))
```

**Expected Output:**
```
1020
<class 'str'>
```

**Why?** Because `"10"` and `"20"` are strings (text), not integers. When you `+` two strings, Python joins them (concatenates). So `"10" + "20"` gives `"1020"`, not `30`.

**The Fix — Convert to int first:**

```python
a = int("10")
b = int("20")
print(a + b)
print(type(a))
```

**Expected Output:**
```
30
<class 'int'>
```

**Self-check Questions:**
- Why did `"10" + "20"` give `"1020"` and not `30`?
- How did wrapping with `int()` change the behaviour?
- What other constructor function could you use instead of `int()` if you wanted the answer as `30.0`?

---

### Exercise 3 – Build a Student Profile Dictionary

**Objective:** Practice creating and displaying a `dict`.

**Scenario:** You are building a school management system. Create a dictionary that stores a student's profile with the following information:
- Name: Adaeze
- Age: 15
- Class: JSS3
- Subject Score: 88.5
- Is Active Student: True

**Your Code:**
```python
student = {
    "name": "Adaeze",
    "age": 15,
    "class": "JSS3",
    "score": 88.5,
    "is_active": True
}

print(student)
print(type(student))
print(type(student["name"]))
print(type(student["age"]))
print(type(student["score"]))
print(type(student["is_active"]))
```

**Expected Output:**
```
{'name': 'Adaeze', 'age': 15, 'class': 'JSS3', 'score': 88.5, 'is_active': True}
<class 'dict'>
<class 'str'>
<class 'int'>
<class 'float'>
<class 'bool'>
```

**Notice:** The dictionary itself is a `dict`, but each **value inside it** has its own type! The data types are nested inside each other. This is very common in real programs.

---

### Exercise 4 – The Deduplication Challenge

**Objective:** See how `set` automatically removes duplicates.

**Scenario:** A school attendance system collected student IDs for an event, but some students scanned in multiple times. Use a set to get a clean, unique list.

```python
raw_scan_ids = [101, 102, 103, 101, 104, 102, 105, 103, 101]
print("Raw list:", raw_scan_ids)
print("Total scan events:", len(raw_scan_ids))

unique_ids = set(raw_scan_ids)
print("Unique students:", unique_ids)
print("Number of unique students:", len(unique_ids))
print(type(unique_ids))
```

**Expected Output:**
```
Raw list: [101, 102, 103, 101, 104, 102, 105, 103, 101]
Total scan events: 9
Unique students: {101, 102, 103, 104, 105}
Number of unique students: 5
<class 'set'>
```

> 💡 **What is `len()`?** `len()` is a built-in function that counts the number of items in a collection. We used it here to count list items and set items.

**Self-check Questions:**
- Why did 9 scan events result in only 5 unique students?
- What real-world systems use this kind of deduplication?

---

### Exercise 5 – Type Conversion Round-Trip

**Objective:** Practice converting between types using constructor functions.

**Scenario:** A temperature sensor returns values as strings (because it reads them from a text file). You need to convert them to floats to do calculations.

```python
# Step 1: Values arrive as strings
temp_1 = "36.6"
temp_2 = "37.1"
temp_3 = "35.9"

print("Types before conversion:")
print(type(temp_1), type(temp_2), type(temp_3))

# Step 2: Convert to float
temp_1 = float(temp_1)
temp_2 = float(temp_2)
temp_3 = float(temp_3)

print("\nTypes after conversion:")
print(type(temp_1), type(temp_2), type(temp_3))

# Step 3: Calculate average
average = (temp_1 + temp_2 + temp_3) / 3
print("\nAverage Temperature:", average)
```

**Expected Output:**
```
Types before conversion:
<class 'str'> <class 'str'> <class 'str'>

Types after conversion:
<class 'float'> <class 'float'> <class 'float'>

Average Temperature: 36.53333333333333
```

**Self-check Questions:**
- What would happen if you tried to calculate the average BEFORE converting to float?
- How would you round the average to 2 decimal places? (Hint: look up Python's `round()` function!)

---

## Mini Project – Python Data Type Inspector

Let us build a small, useful program that demonstrates all the key data types in a realistic scenario. You will create a **product record** for an online store, using all the major data types.

---

### Stage 1 – Define the Product Data

```python
# Product basic information
product_name = "Wireless Earbuds"       # str
product_id = 10042                       # int
price = 12499.99                         # float
is_available = True                      # bool
stock_count = None                       # NoneType — stock not yet confirmed
```

---

### Stage 2 – Define Collections

```python
# List of features (can be updated as features change)
features = ["Bluetooth 5.0", "20hr battery", "Water resistant", "Touch controls"]

# Tuple of supported colours (fixed — no new colours being added)
colours = ("Black", "White", "Navy Blue")

# Dictionary of full product record
product = {
    "name": product_name,
    "id": product_id,
    "price": price,
    "available": is_available,
    "features": features,
    "colours": colours,
    "stock": stock_count
}

# Set of category tags (unique only)
tags = {"electronics", "audio", "wireless", "bluetooth", "audio", "earbuds", "wireless"}
```

---

### Stage 3 – Display and Inspect

```python
print("=" * 45)
print("      PRODUCT DATA TYPE INSPECTOR")
print("=" * 45)

print("\nProduct Name:", product_name, "→ Type:", type(product_name).__name__)
print("Product ID:  ", product_id,   "→ Type:", type(product_id).__name__)
print("Price:       ", price,         "→ Type:", type(price).__name__)
print("Available:   ", is_available,  "→ Type:", type(is_available).__name__)
print("Stock:       ", stock_count,   "→ Type:", type(stock_count).__name__)

print("\nFeatures (list):  ", features)
print("Type:", type(features).__name__)

print("\nColours (tuple):  ", colours)
print("Type:", type(colours).__name__)

print("\nTags (set):", tags)
print("Type:", type(tags).__name__)
print("(Duplicates 'wireless' and 'audio' were removed automatically)")

print("\nFull Product Dict:", product)
print("Type:", type(product).__name__)
print("=" * 45)
```

**Expected Output:**
```
=============================================
      PRODUCT DATA TYPE INSPECTOR
=============================================

Product Name: Wireless Earbuds → Type: str
Product ID:   10042            → Type: int
Price:        12499.99         → Type: float
Available:    True             → Type: bool
Stock:        None             → Type: NoneType

Features (list):   ['Bluetooth 5.0', '20hr battery', 'Water resistant', 'Touch controls']
Type: list

Colours (tuple):   ('Black', 'White', 'Navy Blue')
Type: tuple

Tags (set): {'bluetooth', 'earbuds', 'wireless', 'electronics', 'audio'}
Type: set
(Duplicates 'wireless' and 'audio' were removed automatically)

Full Product Dict: {'name': 'Wireless Earbuds', 'id': 10042, 'price': 12499.99, 'available': True, 'features': [...], 'colours': (...), 'stock': None}
Type: dict
=============================================
```

> 💡 **Notice:** `type(product_name).__name__` gives you just the name (`'str'`) without the `<class '...'>` wrapper. The `.__name__` part extracts just the clean name from the type object. This makes the output much more readable.

---

### Stage 4 – Reflection Questions

1. Why did we use a `list` for features but a `tuple` for colours?
2. Why is `stock_count = None` more meaningful than `stock_count = 0`?
3. What happened to the duplicate tags in the `set`?
4. How many different data types appear inside the `product` dictionary?
5. Could you add a new colour to `colours` after creating the tuple? Why or why not?

---

### Optional Extension Challenges

1. Add a `ratings` list to the product with 5 customer ratings (floats between 1.0 and 5.0), then calculate and print the average rating
2. Convert the `features` list to a `tuple` using `tuple()` and print both — notice the brackets change from `[...]` to `(...)`
3. Add a `discount_percent` field as an `int` and calculate the discounted price using `price * (1 - discount_percent / 100)`

---

## Common Beginner Mistakes

---

### Mistake 1 – Confusing a Number with a Number-as-String

**Wrong — thinking `"5"` and `5` are the same:**
```python
x = "5"
print(x + 3)   # ❌ TypeError: can only concatenate str (not "int") to str
```

**Right:**
```python
x = 5           # No quotes → integer
print(x + 3)   # ✅ Works — output: 8
```

Or convert explicitly:
```python
x = "5"
print(int(x) + 3)   # ✅ Convert first — output: 8
```

---

### Mistake 2 – Using Lowercase `true` and `false`

**Wrong:**
```python
x = true     # ❌ NameError: name 'true' is not defined
y = false    # ❌ NameError: name 'false' is not defined
```

**Right:**
```python
x = True     # ✅ Capital T
y = False    # ✅ Capital F
```

---

### Mistake 3 – Using Lowercase `none`

**Wrong:**
```python
x = none     # ❌ NameError: name 'none' is not defined
```

**Right:**
```python
x = None     # ✅ Capital N
```

---

### Mistake 4 – Confusing `list` and `tuple` Brackets

**Wrong (mixing brackets):**
```python
my_list  = ("apple", "banana")    # This is actually a TUPLE, not a list!
my_tuple = ["apple", "banana"]    # This is actually a LIST, not a tuple!
```

**Right:**
```python
my_list  = ["apple", "banana"]    # ✅ Square brackets → list
my_tuple = ("apple", "banana")    # ✅ Round brackets → tuple
```

---

### Mistake 5 – Confusing `dict` and `set` Curly Braces

Both use `{...}` but they are very different:

```python
my_set  = {"apple", "banana"}              # ← No colons → this is a SET
my_dict = {"fruit": "apple", "veg": "yam"} # ← Colons between key:value → DICT
```

**How to tell them apart:** If there are colons `:` separating pairs, it is a `dict`. If it is just comma-separated values with no colons, it is a `set`.

---

### Mistake 6 – Assuming `int()` Rounds

**Wrong assumption:**
```python
print(int(9.9))   # You might expect 10 (rounded)
```

**Actual output:**
```
9
```

`int()` **truncates** (cuts off) the decimal — it never rounds. To round, use `round()` instead:

```python
print(round(9.9))   # Output: 10
```

---

### Mistake 7 – Expecting a Set to Keep Order

**Wrong expectation:**
```python
my_set = {"banana", "apple", "cherry"}
print(my_set)   # You might expect: {'banana', 'apple', 'cherry'}
```

**Actual output (order varies — may be different each time):**
```
{'cherry', 'apple', 'banana'}
```

Sets are **unordered**. Never rely on a set maintaining the order you put items in. If order matters, use a `list` or `tuple`.

---

## Reflection Questions

1. In Python, how does it know the difference between `5` (an integer) and `"5"` (a string)? What is the visual clue?
2. What is the difference between a `list` and a `tuple`? When would you choose one over the other?
3. What is the difference between a `dict` and a `set`? How can you tell them apart by looking at the code?
4. Why would `None` be more useful than `0` for representing "no data"?
5. A friend tells you: `x = True` and `y = 1` must be different types. Do you agree? Test it with `type()` and explain the result.
6. You have a list of 1,000 email addresses, and some are duplicates. What single data type conversion would instantly remove all the duplicates?
7. What does `type()` return, and how do you use it?
8. Can one dictionary hold values of different data types? Show an example to support your answer.

---

## Completion Checklist

Before moving to the next lesson, make sure you can confidently say yes to all of the following:

- [ ] I understand what a data type is and why Python uses them
- [ ] I know what a `str` is and how to create one
- [ ] I know the difference between `int` and `float` and when to use each
- [ ] I know what `bool` is and that it can only be `True` or `False` (capital letters)
- [ ] I know what `None` is and that it represents the absence of a value
- [ ] I understand that `list` uses `[...]` and is mutable (changeable)
- [ ] I understand that `tuple` uses `(...)` and is immutable (fixed)
- [ ] I understand that `dict` uses `{key: value}` pairs with colons
- [ ] I understand that `set` stores only unique items and is unordered
- [ ] I can use `type()` to check the data type of any value
- [ ] I understand that Python sets the type automatically when a value is assigned
- [ ] I know how to use constructor functions like `int()`, `float()`, `str()`, `list()` to set types explicitly
- [ ] I can identify and fix the most common type-related mistakes

---

## Lesson Summary

**Data types** are Python's system for categorising values. Every value has a type that tells Python what kind of data it is and what rules apply to it.

Python's built-in types fall into these groups:

**Text:** `str` — any sequence of characters in quotes: `"Hello"`, `'Nigeria'`

**Numeric:** `int` (whole numbers like `42`), `float` (decimals like `3.14`), `complex` (numbers with imaginary parts like `3+5j`)

**Sequence:** `list` (ordered, changeable, `[...]`), `tuple` (ordered, fixed, `(...)`), `range` (a sequence of numbers)

**Mapping:** `dict` (key-value pairs, `{"name": "Ada", "age": 15}`)

**Set:** `set` (unique items, unordered, `{...}`), `frozenset` (like set but fixed)

**Boolean:** `bool` — only `True` or `False`

**Binary:** `bytes`, `bytearray`, `memoryview` — for raw binary data (advanced)

**None:** `NoneType` — represents the absence of a value (`None`)

**Key tools:**
- `type(x)` → tells you the data type of `x`
- Constructor functions (`int()`, `float()`, `str()`, `list()`, etc.) → explicitly set or convert types

**Python sets types automatically** based on the value you assign. You only need constructor functions when you want to be explicit or when you are converting from one type to another.

```python
# Quick Reference Examples

x = "Hello"                    # str
x = 42                         # int
x = 3.14                       # float
x = True                       # bool
x = None                       # NoneType
x = [1, 2, 3]                  # list
x = (1, 2, 3)                  # tuple
x = {"a": 1, "b": 2}          # dict
x = {1, 2, 3}                  # set

# Check type
print(type(x))                 # <class 'set'>

# Convert type
x = int("42")                  # str → int: 42
x = float(7)                   # int → float: 7.0
x = str(100)                   # int → str: "100"
x = list((1, 2, 3))            # tuple → list: [1, 2, 3]
x = set([1, 1, 2, 3, 3])      # list → set (removes duplicates): {1, 2, 3}
```

---

> 🎉 **Congratulations!** You have completed Lesson 05. You now understand every major data type Python uses and how they relate to real-world data. This knowledge is the foundation for everything that comes next — variables, calculations, conditions, loops, and functions all depend on understanding what kind of data you are working with. In the next lesson, you will explore **Python Numbers** in much greater depth!
