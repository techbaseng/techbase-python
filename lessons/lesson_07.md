---
render_with_liquid: false
title: "Lesson 07 – Python Casting"
nav_order: 7
---

# Lesson 07 – Python Casting

---

## Lesson Introduction

Imagine you are at a currency exchange bureau. You walk in holding Nigerian Naira (₦), but the seller only accepts US Dollars ($). So you hand your Naira to the teller, they convert it, and hand back the equivalent amount in Dollars. The value is essentially the same — the currency (the *form*) is what changed.

That is exactly what **casting** does in Python.

Casting is the process of **converting a value from one data type into another** — changing the *form* of the data so it can be used in a different context. You might take a number and convert it into text, or take a piece of text that looks like a number and convert it into an actual number you can calculate with.

Without casting, Python programs would constantly crash when different types of data tried to work together. With casting, you become the teller — you control exactly what type each value is at any moment.

In this lesson you will learn:
- What casting is and **why** it is necessary
- The three main casting functions: `int()`, `float()`, and `str()`
- How each one works, what inputs it accepts, and what it produces
- Exactly what happens to values during each conversion (including surprising edge cases)
- How to chain conversions together
- The limits of casting — what you *cannot* cast and why
- Real-world scenarios where casting saves the day
- How to confirm your casts using `type()`

By the end of this lesson you will be confident converting data between types in any situation your programs require.

---

## Prerequisite Concepts

Before we go further, let us make sure the foundation is solid. Two ideas need to be clear.

---

### Reminder: What is a Data Type?

Every value in Python belongs to a **data type** — a category that tells Python what kind of data it is and how it should behave. The three types we focus on in this lesson are:

- `int` — whole numbers with no decimal point: `1`, `20`, `-5`, `0`
- `float` — numbers with a decimal point: `1.0`, `2.8`, `3.14`, `-0.5`
- `str` — text, anything wrapped in quotes: `"hello"`, `"3"`, `"42.5"`

Here is the key insight: `3` (an `int`), `3.0` (a `float`), and `"3"` (a `str`) all *look* like the number three — but Python treats them completely differently. They live in different categories, follow different rules, and cannot always mix without a conversion.

---

### Reminder: What is a Variable?

A **variable** is a named storage location. When you write:

```python
x = 5
```

You are storing the value `5` inside a container called `x`. You can then use `x` anywhere in your code and Python will fetch the value `5` from it.

```python
x = 5
print(x)
```

**Expected Output:**
```
5
```

Throughout this lesson, we will use variables to store values before and after casting, so you can clearly see the before and after.

---

## What is Casting?

**Casting** means explicitly telling Python to convert a value from its current type into a different type.

The word comes from metalworking — when you *cast* metal, you pour liquid metal into a mould to give it a new shape. In Python, casting pours a value into a new "mould" (a new data type), giving it a new form while preserving the underlying information (as much as possible).

### Why Does Casting Exist?

Python is **strongly typed** — it will not automatically mix incompatible types. Try adding the number `5` to the text `"3"` and Python will refuse:

```python
print(5 + "3")
```

**Expected Output:**
```
TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

Python is saying: *"I will not guess what you meant. You need to tell me which type these should be before I can work with them."*

Casting is your answer to that demand. You tell Python: *"Convert this `str` to an `int` first, then add them."*

```python
print(5 + int("3"))
```

**Expected Output:**
```
8
```

That is casting in action.

---

### How Python Performs Casting — The Object-Oriented Explanation

Python is an **object-oriented language**. In Python's world, every piece of data is an **object** — a self-contained bundle of data and behaviour. Every data type is actually a **class** — a blueprint for making objects of that kind.

When you call `int(...)`, `float(...)`, or `str(...)`, you are not calling a simple function — you are calling the **constructor** of the `int`, `float`, or `str` class. A constructor is a special method that builds (constructs) a new object of that class.

So `int("3")` means: *"Use the `int` class blueprint to build a brand new integer object from the value `"3"`."*

You do not need to master object-oriented programming to understand casting — just know that this is why the casting syntax looks like a function call using the type's name. Each type (class) knows how to build itself from certain kinds of input.

---

## The Three Main Casting Functions

Python provides three constructor functions for the most common type conversions:

| Function | Full Name | What it produces |
|---|---|---|
| `int()` | Integer constructor | A whole number (no decimals) |
| `float()` | Float constructor | A decimal number |
| `str()` | String constructor | A piece of text |

Each one accepts different kinds of input and produces different output. Let us explore every case.

---

## Part 1 – `int()`: Casting to Integer

### What is `int()`?

`int()` constructs an **integer** (whole number) from whatever you pass into it. An integer has no decimal point — it is a pure counting number.

The three types of values `int()` can accept are:
1. An **integer literal** — another whole number
2. A **float literal** — a decimal number (the decimal part is removed, not rounded)
3. A **string literal** — text that looks exactly like a whole number (e.g., `"3"`, `"100"`)

---

### Case 1 – `int()` from an Integer Literal

The simplest case: you pass in a whole number, and you get a whole number back.

```python
x = int(1)
print(x)
print(type(x))
```

**Expected Output:**
```
1
<class 'int'>
```

**Line by line:**
- `int(1)` → takes the integer `1` and constructs a new integer from it → result is `1`
- `print(x)` → displays `1`
- `print(type(x))` → confirms it is `<class 'int'>`

You might wonder: "Why convert an integer to an integer? That seems pointless." In isolation, it is. But in real programs, you often receive values from other sources — functions, files, user input — and you need to be *explicit* about what type you expect. Using `int()` makes your intent clear.

---

### Case 2 – `int()` from a Float Literal

When you pass a float (decimal number) into `int()`, Python **removes the decimal part entirely**. This is called **truncation**.

```python
y = int(2.8)
print(y)
print(type(y))
```

**Expected Output:**
```
2
<class 'int'>
```

> ⚠️ **Crucial concept — Truncation is NOT rounding!**
>
> `int(2.8)` gives `2`, not `3`.
> `int(9.99)` gives `9`, not `10`.
> `int(-3.7)` gives `-3`, not `-4`.
>
> Python simply **cuts off** everything after the decimal point. It never looks at the decimal digits to decide whether to round up or down. The decimal is just discarded.

Let us verify each of those:

```python
print(int(2.8))     # Truncates → 2
print(int(9.99))    # Truncates → 9
print(int(-3.7))    # Truncates → -3
print(int(0.99))    # Truncates → 0
```

**Expected Output:**
```
2
9
-3
0
```

> 💡 **Thinking Prompt:** Why does `int(-3.7)` give `-3` and not `-4`? Think about what "truncation" means — it always removes the decimal regardless of direction. `-3` is closer to zero than `-4` is. Truncation moves *toward* zero, not downward.

**If you want proper rounding**, use Python's built-in `round()` function instead:

```python
print(round(2.8))    # Rounds → 3
print(round(9.4))    # Rounds → 9
print(round(9.5))    # Rounds → 10
```

**Expected Output:**
```
3
9
10
```

---

### Case 3 – `int()` from a String Literal

You can convert a string to an integer if the string contains **exactly** a whole number — nothing else. No spaces in the middle, no decimal points, no letters mixed in.

```python
z = int("3")
print(z)
print(type(z))
```

**Expected Output:**
```
3
<class 'int'>
```

`"3"` is the text character three. After `int("3")`, it becomes the actual number `3` that you can calculate with.

**More string-to-int examples:**

```python
print(int("100"))     # → 100
print(int("-50"))     # → -50 (negative numbers work)
print(int("0"))       # → 0
```

**Expected Output:**
```
100
-50
0
```

---

### What Happens with Negative String Numbers?

```python
print(int("-50"))
```

**Expected Output:**
```
-50
```

The minus sign is understood as part of the number.

---

### The Limits of `int()` from Strings

`int()` is strict. If the string contains anything that does not look like a clean whole number, Python raises a `ValueError`:

```python
# These will ALL cause errors:
print(int("3.5"))      # ❌ Has a decimal — use float() first
print(int("hello"))    # ❌ Not a number at all
print(int("3 apples")) # ❌ Has extra characters
print(int(""))         # ❌ Empty string
```

**Error produced:**
```
ValueError: invalid literal for int() with base 10: '3.5'
```

> 💡 **Real-World Scenario:** You are reading data from a CSV file. One column is "Age" and the values come in as strings: `"17"`, `"23"`, `"31"`. You must cast them with `int()` before doing any calculations. But what if one row accidentally has `"17.5"` instead of a whole number? That will crash with a `ValueError`. This is why knowing `int()`'s limits is important — in real programs, you add error handling around conversions.

---

### Full `int()` Reference Table

| Input | Result | Notes |
|---|---|---|
| `int(1)` | `1` | Int from int — no change |
| `int(2.8)` | `2` | Float → truncated, NOT rounded |
| `int(9.99)` | `9` | Truncation again |
| `int(-3.7)` | `-3` | Truncates toward zero |
| `int("3")` | `3` | String whole number → int |
| `int("-50")` | `-50` | Negative string → int |
| `int("3.5")` | ❌ `ValueError` | String with decimal — not allowed |
| `int("hello")` | ❌ `ValueError` | Non-numeric string — not allowed |

---

## Part 2 – `float()`: Casting to Float

### What is `float()`?

`float()` constructs a **float** (decimal number) from whatever you pass into it. Floats always have a decimal point in their representation, even if the decimal part is `.0`.

The three types `float()` can accept are:
1. An **integer literal** — a whole number (`.0` is added)
2. A **float literal** — another decimal number
3. A **string literal** — text that looks like a float or an integer

---

### Case 1 – `float()` from an Integer Literal

```python
x = float(1)
print(x)
print(type(x))
```

**Expected Output:**
```
1.0
<class 'float'>
```

**Key observation:** `1` becomes `1.0`. Python adds the `.0` to signal that this is now a floating-point value. The *number* has not changed — it is still mathematically one — but the *type* has changed from `int` to `float`.

More examples:

```python
print(float(5))      # → 5.0
print(float(-8))     # → -8.0
print(float(0))      # → 0.0
print(float(100))    # → 100.0
```

**Expected Output:**
```
5.0
-8.0
0.0
100.0
```

---

### Case 2 – `float()` from a Float Literal

Pass a float in, get a float back. Mainly used to be explicit about the type.

```python
y = float(2.8)
print(y)
print(type(y))
```

**Expected Output:**
```
2.8
<class 'float'>
```

---

### Case 3 – `float()` from a String Literal

`float()` is more flexible than `int()` when it comes to strings — it accepts strings that look like either whole numbers or decimal numbers.

**String that looks like an integer:**

```python
z = float("3")
print(z)
print(type(z))
```

**Expected Output:**
```
3.0
<class 'float'>
```

**String that looks like a decimal:**

```python
w = float("4.2")
print(w)
print(type(w))
```

**Expected Output:**
```
4.2
<class 'float'>
```

More string examples:

```python
print(float("0"))       # → 0.0
print(float("-7.5"))    # → -7.5
print(float("100"))     # → 100.0
print(float("3.14159")) # → 3.14159
```

**Expected Output:**
```
0.0
-7.5
100.0
3.14159
```

---

### What Happens with Strings `float()` Cannot Handle?

Just like `int()`, `float()` will raise a `ValueError` if the string does not look like a valid number:

```python
print(float("hello"))    # ❌ ValueError
print(float("3 dogs"))   # ❌ ValueError
print(float(""))         # ❌ ValueError
```

**Error produced:**
```
ValueError: could not convert string to float: 'hello'
```

---

### Full `float()` Reference Table

| Input | Result | Notes |
|---|---|---|
| `float(1)` | `1.0` | Int → float, `.0` added |
| `float(2.8)` | `2.8` | Float from float — no change |
| `float("3")` | `3.0` | String int → float |
| `float("4.2")` | `4.2` | String decimal → float |
| `float("-7.5")` | `-7.5` | Negative string decimal → float |
| `float("hello")` | ❌ `ValueError` | Non-numeric — not allowed |

---

## Part 3 – `str()`: Casting to String

### What is `str()`?

`str()` constructs a **string** (text) from a very wide variety of inputs. Where `int()` and `float()` are strict and limited, `str()` is remarkably flexible — it can convert almost anything into its text representation.

The three types `str()` most commonly accepts are:
1. A **string literal** — text (passes through unchanged)
2. An **integer literal** — a whole number (becomes its text equivalent)
3. A **float literal** — a decimal number (becomes its text equivalent)

---

### Case 1 – `str()` from a String Literal

```python
x = str("s1")
print(x)
print(type(x))
```

**Expected Output:**
```
s1
<class 'str'>
```

Passing a string into `str()` gives you the same string back. It is equivalent to writing `x = "s1"`. Again, while this seems trivial, being explicit about expecting a string type is useful in larger programs.

---

### Case 2 – `str()` from an Integer Literal

```python
y = str(2)
print(y)
print(type(y))
```

**Expected Output:**
```
2
<class 'str'>
```

**Important:** The output *looks* like the number `2` — but it is actually the text character `"2"`. Confirm this with `type()`:

```python
y = str(2)
print(type(y))   # <class 'str'>  ← it is text, not a number
```

You can no longer do arithmetic with it directly. If you try `str(2) + 3`, Python will raise a `TypeError`.

More examples:

```python
print(str(100))     # → '100' (as text)
print(str(-5))      # → '-5' (as text)
print(str(0))       # → '0' (as text)
```

**Expected Output:**
```
100
-5
0
```

---

### Case 3 – `str()` from a Float Literal

```python
z = str(3.0)
print(z)
print(type(z))
```

**Expected Output:**
```
3.0
<class 'str'>
```

The decimal point is preserved in the text representation. More examples:

```python
print(str(3.14))     # → '3.14'
print(str(-0.5))     # → '-0.5'
print(str(100.0))    # → '100.0'
```

**Expected Output:**
```
3.14
-0.5
100.0
```

---

### Why is `str()` so Useful? — The Number-Joining Problem

Here is the most practical reason beginners need `str()`. Suppose you want to build a message that includes a calculated number:

**Wrong — Direct string + number concatenation:**

```python
age = 25
print("I am " + age + " years old.")   # ❌ TypeError
```

**Error:**
```
TypeError: can only concatenate str (not "int") to str
```

Python refuses to join a string and an integer directly. You must first convert the integer to a string:

**Right — Convert the number to a string first:**

```python
age = 25
print("I am " + str(age) + " years old.")   # ✅
```

**Expected Output:**
```
I am 25 years old.
```

> 💡 **Alternative approach:** You already know that `print("I am", age, "years old.")` works using commas. That is fine for simple output. But when you are *building* text strings to store in variables, send over a network, write to a file, or pass to another function — you need `str()` to join numbers and text into a single string value.

**Storing a message in a variable:**

```python
score = 98
message = "Your final score is: " + str(score) + " out of 100."
print(message)
```

**Expected Output:**
```
Your final score is: 98 out of 100.
```

---

### Full `str()` Reference Table

| Input | Result | Notes |
|---|---|---|
| `str("s1")` | `'s1'` | String from string — unchanged |
| `str(2)` | `'2'` | Int → string representation |
| `str(-5)` | `'-5'` | Negative int → string |
| `str(3.0)` | `'3.0'` | Float → string (keeps decimal) |
| `str(3.14)` | `'3.14'` | Float → string |
| `str(True)` | `'True'` | Bool → string |
| `str(None)` | `'None'` | NoneType → string |

Notice: `str()` can also convert booleans and `None` to their text representations!

---

## Putting It All Together — The Full Examples from the Source

Here is all the casting code from the W3Schools source, expanded with annotations:

### Casting to Integer — All Three Input Types

```python
x = int(1)    # x will be 1
y = int(2.8)  # y will be 2   (decimal truncated, NOT rounded)
z = int("3")  # z will be 3   (string "3" becomes number 3)

print(x)
print(y)
print(z)
print(type(x), type(y), type(z))
```

**Expected Output:**
```
1
2
3
<class 'int'> <class 'int'> <class 'int'>
```

---

### Casting to Float — All Four Input Types

```python
x = float(1)      # x will be 1.0   (int → float, .0 added)
y = float(2.8)    # y will be 2.8   (float → float, unchanged)
z = float("3")    # z will be 3.0   (string int → float)
w = float("4.2")  # w will be 4.2   (string decimal → float)

print(x)
print(y)
print(z)
print(w)
print(type(x), type(y), type(z), type(w))
```

**Expected Output:**
```
1.0
2.8
3.0
4.2
<class 'float'> <class 'float'> <class 'float'> <class 'float'>
```

---

### Casting to String — All Three Input Types

```python
x = str("s1")  # x will be 's1'   (string → string, unchanged)
y = str(2)     # y will be '2'    (int → string)
z = str(3.0)   # z will be '3.0'  (float → string, keeps decimal)

print(x)
print(y)
print(z)
print(type(x), type(y), type(z))
```

**Expected Output:**
```
s1
2
3.0
<class 'str'> <class 'str'> <class 'str'>
```

---

## Casting Between Types — The Full Conversion Map

Now that we understand all three functions, here is a clear map of all possible conversions and what happens in each case:

| From → To | Function | What changes |
|---|---|---|
| `int` → `float` | `float(5)` | `5` becomes `5.0` — decimal added |
| `int` → `str` | `str(5)` | `5` becomes `"5"` — becomes text |
| `float` → `int` | `int(5.9)` | `5.9` becomes `5` — decimal truncated |
| `float` → `str` | `str(5.9)` | `5.9` becomes `"5.9"` — becomes text |
| `str` → `int` | `int("5")` | `"5"` becomes `5` — if valid whole number |
| `str` → `float` | `float("5.9")` | `"5.9"` becomes `5.9` — if valid number |

---

## Chaining Conversions

Sometimes you need to convert through multiple steps. For example, you have a float stored as a string — you want the integer version of it. You cannot go directly from a string with a decimal to an integer (remember, `int("3.5")` raises a `ValueError`). Instead, you chain: `str → float → int`.

```python
value = "3.7"          # This is a string

# Step 1: str → float
as_float = float(value)    # 3.7
print("Float:", as_float)

# Step 2: float → int (truncates)
as_int = int(as_float)     # 3
print("Int:", as_int)
```

**Expected Output:**
```
Float: 3.7
Int: 3
```

You can also write this as a single chained expression:

```python
value = "3.7"
result = int(float(value))
print(result)
```

**Expected Output:**
```
3
```

**How to read `int(float(value))`:** Python evaluates from the **inside out**.
1. First: `float(value)` → converts `"3.7"` to `3.7`
2. Then: `int(3.7)` → truncates to `3`

> 💡 **Real-World Use:** Sensor data, CSV files, and web APIs very often give you numbers as strings with decimal points. If you need integer values (e.g., pixel positions, counts, row numbers), you chain `int(float(...))` to handle both conversion steps cleanly.

---

## Verifying Casts with `type()`

Always use `type()` to confirm that your cast worked correctly. Never just assume — verify!

```python
original = "42"
converted = int(original)

print("Original value:", original)
print("Original type:", type(original))
print("Converted value:", converted)
print("Converted type:", type(converted))
```

**Expected Output:**
```
Original value: 42
Original type: <class 'str'>
Converted value: 42
Converted type: <class 'int'>
```

The value *looks* the same (`42`) but the type has completely changed from `str` to `int`. Without `type()`, you might not notice the difference — but Python certainly does.

---

## Guided Practice Exercises

Work through each exercise completely. Predict the output before running the code, then verify!

---

### Exercise 1 – Warm-Up: Name Every Result

**Objective:** Practise predicting the result and type of each cast.

Before running any code, predict: what value and what type will each line produce?

```python
a = int(7)
b = int(3.9)
c = int("55")
d = float(4)
e = float(1.5)
f = float("8")
g = float("2.71")
h = str(10)
i = str(6.0)
j = str("Python")
```

**Write your predictions, then run this verification code:**

```python
print(a, type(a))
print(b, type(b))
print(c, type(c))
print(d, type(d))
print(e, type(e))
print(f, type(f))
print(g, type(g))
print(h, type(h))
print(i, type(i))
print(j, type(j))
```

**Expected Output:**
```
7 <class 'int'>
3 <class 'int'>
55 <class 'int'>
4.0 <class 'float'>
1.5 <class 'float'>
8.0 <class 'float'>
2.71 <class 'float'>
10 <class 'str'>
6.0 <class 'str'>
Python <class 'str'>
```

**Self-check:** How many did you get right? Pay special attention to `b = int(3.9)` → did you predict `3` or `4`? And `h = str(10)` → does the output look like a number or a string? (Hint: `type()` tells you the truth.)

---

### Exercise 2 – The Sensor Data Problem

**Objective:** Practice converting string data to numeric types for calculations.

**Scenario:** A temperature monitoring system at a school records readings every hour. The readings come from a file as strings. You need to calculate the average temperature for the day.

```python
# Readings arrive as strings from the data file
reading_1 = "28.4"
reading_2 = "30.1"
reading_3 = "27.8"
reading_4 = "29.5"
reading_5 = "31.2"

# Step 1: Convert all to float
temp_1 = float(reading_1)
temp_2 = float(reading_2)
temp_3 = float(reading_3)
temp_4 = float(reading_4)
temp_5 = float(reading_5)

# Step 2: Calculate total and average
total = temp_1 + temp_2 + temp_3 + temp_4 + temp_5
average = total / 5

# Step 3: Build a report message using str()
report = "Daily Average Temperature: " + str(round(average, 2)) + "°C"
print(report)
print("Max reading:", max(temp_1, temp_2, temp_3, temp_4, temp_5), "°C")
print("Min reading:", min(temp_1, temp_2, temp_3, temp_4, temp_5), "°C")
```

**Expected Output:**
```
Daily Average Temperature: 29.4°C
Max reading: 31.2 °C
Min reading: 27.8 °C
```

**What to notice:**
- `float(reading_1)` converted `"28.4"` (text) to `28.4` (a real number you can add)
- `str(round(average, 2))` converted the calculated float back to a string so it could be joined with `"Daily Average Temperature: "` using `+`
- `max()` and `min()` are built-in Python functions that find the largest and smallest values from a set of arguments

**Self-check Questions:**
- What error would you get if you tried `total = reading_1 + reading_2 + reading_3 + reading_4 + reading_5` without converting first?
- Why did we use `str(round(average, 2))` rather than just `str(average)`?

---

### Exercise 3 – Age Calculator

**Objective:** Practice `int()` conversion from string input in a realistic scenario.

**Scenario:** A school registration form collects a student's birth year as text. You need to calculate their current age.

```python
# Input arrives as a string (as if typed by a user)
birth_year_input = "2009"
current_year = 2024

# Convert the string to an integer so we can do arithmetic
birth_year = int(birth_year_input)

# Calculate age
age = current_year - birth_year

# Build the output message
print("Birth Year:", birth_year, "→ Type:", type(birth_year).__name__)
print("Current Year:", current_year)
print("Calculated Age:", age, "years")
print("Message: " + "The student is " + str(age) + " years old.")
```

**Expected Output:**
```
Birth Year: 2009 → Type: int
Current Year: 2024
Calculated Age: 15 years
Message: The student is 15 years old.
```

**What to notice:**
- `int(birth_year_input)` converted `"2009"` (string) to `2009` (integer)
- Without that conversion, `current_year - birth_year_input` would crash with a `TypeError`
- `str(age)` converted the result `15` back to text so we could join it into the message string

---

### Exercise 4 – The Truncation Experiment

**Objective:** Deeply understand the difference between truncation and rounding.

**Scenario:** A marks processing system receives scores as decimal floats but must store final grades as whole numbers. Explore what happens with different values.

```python
scores = [45.2, 67.5, 89.9, 72.0, 56.499, 91.8, 50.1]

print("Score    Truncated   Rounded")
print("-" * 35)

for score in scores:
    truncated = int(score)
    rounded   = round(score)
    print(score, "  →", truncated, "       →", rounded)
```

**Expected Output:**
```
Score    Truncated   Rounded
-----------------------------------
45.2   → 45        → 45
67.5   → 67        → 68
89.9   → 89        → 90
72.0   → 72        → 72
56.499 → 56        → 56
91.8   → 91        → 92
50.1   → 50        → 50
```

> 💡 **Thinking Prompt:** Look at `67.5` — truncated gives `67`, rounded gives `68`. And `89.9` — truncated gives `89`, rounded gives `90`. Which would be fairer for student grading? Why does the choice of `int()` vs `round()` matter so much here?

**Self-check Questions:**
- Which students would be disadvantaged if the school used `int()` (truncation) instead of `round()` for grading?
- At what score does it make the biggest practical difference?

---

### Exercise 5 – Building a Report String

**Objective:** Practise using `str()` to combine computed values into readable text messages.

**Scenario:** A small business tracks weekly sales. Build a formatted weekly summary report.

```python
# Sales data (already as numbers)
week_number = 12
mon_sales = 15000
tue_sales = 22500
wed_sales = 18300
thu_sales = 27100
fri_sales = 31500

# Calculate totals and average
total = mon_sales + tue_sales + wed_sales + thu_sales + fri_sales
average_daily = total / 5
best_day_sales = max(mon_sales, tue_sales, wed_sales, thu_sales, fri_sales)

# Build report using str() to join numbers with text
print("=" * 40)
print("  WEEKLY SALES REPORT — Week " + str(week_number))
print("=" * 40)
print("Monday:    ₦" + str(mon_sales))
print("Tuesday:   ₦" + str(tue_sales))
print("Wednesday: ₦" + str(wed_sales))
print("Thursday:  ₦" + str(thu_sales))
print("Friday:    ₦" + str(fri_sales))
print("-" * 40)
print("Total:     ₦" + str(total))
print("Daily Avg: ₦" + str(round(average_daily, 2)))
print("Best Day:  ₦" + str(best_day_sales))
print("=" * 40)
```

**Expected Output:**
```
========================================
  WEEKLY SALES REPORT — Week 12
========================================
Monday:    ₦15000
Tuesday:   ₦22500
Wednesday: ₦18300
Thursday:  ₦27100
Friday:    ₦31500
----------------------------------------
Total:     ₦114400
Daily Avg: ₦22880.0
Best Day:  ₦31500
========================================
```

**What to notice:**
- Every number was converted with `str()` before being joined with `"₦"` and other text using `+`
- Without `str()`, every `"₦" + mon_sales` would crash with `TypeError: can only concatenate str (not "int") to str`
- `round(average_daily, 2)` rounds to 2 decimal places before converting to string

---

## Mini Project – Data Type Conversion Pipeline

Real-world programs constantly receive data in the wrong type — from user input, from files, from APIs — and must convert it to the right type before processing. Let us simulate this with a complete pipeline.

**The Scenario:** You are building a simple student marks processor. Raw data arrives as a list of strings (simulating data read from a text file). Your pipeline must clean, convert, calculate, and report.

---

### Stage 1 – Raw Data Arrives as Strings

```python
# Simulated raw data from a text file — everything is a string
raw_data = [
    ["Amara",    "JSS2", "78.5", "82.0", "91.3"],
    ["Chidi",    "JSS2", "65.0", "70.5", "88.0"],
    ["Fatima",   "JSS3", "92.0", "95.5", "89.0"],
    ["Emeka",    "JSS2", "55.5", "60.0", "72.5"],
    ["Ngozi",    "JSS3", "88.0", "91.0", "94.5"],
]

print("Raw data (as received from file):")
print(raw_data[0])
print("Type of first score:", type(raw_data[0][2]))   # Will be str
```

**Expected Output:**
```
Raw data (as received from file):
['Amara', 'JSS2', '78.5', '82.0', '91.3']
Type of first score: <class 'str'>
```

---

### Stage 2 – Convert and Process

```python
print("\n" + "=" * 55)
print("  STUDENT PERFORMANCE REPORT")
print("=" * 55)
print(f"{'Name':<10} {'Class':<7} {'Eng':>6} {'Math':>7} {'Sci':>6} {'Avg':>7} {'Grade':>7}")
print("-" * 55)

for row in raw_data:
    name   = str(row[0])         # Already a string, but explicit
    cls    = str(row[1])         # Already a string
    eng    = float(row[2])       # Convert string → float
    math   = float(row[3])       # Convert string → float
    sci    = float(row[4])       # Convert string → float

    average = (eng + math + sci) / 3

    # Determine grade using simple thresholds
    if average >= 90:
        grade = "A"
    elif average >= 75:
        grade = "B"
    elif average >= 60:
        grade = "C"
    else:
        grade = "F"

    # Print row — convert floats back to strings for formatting
    print(name.ljust(10), cls.ljust(7),
          str(eng).rjust(6), str(math).rjust(7),
          str(sci).rjust(6), str(round(average, 1)).rjust(7),
          grade.rjust(7))

print("=" * 55)
```

**Expected Output:**
```
=======================================================
  STUDENT PERFORMANCE REPORT
=======================================================
Name       Class     Eng    Math    Sci    Avg   Grade
-------------------------------------------------------
Amara      JSS2     78.5    82.0   91.3   83.9       B
Chidi      JSS2     65.0    70.5   88.0   74.5       C
Fatima     JSS3     92.0    95.5   89.0   92.2       A
Emeka      JSS2     55.5    60.0   72.5   62.7       C
Ngozi      JSS3     88.0    91.0   94.5   91.2       A
=======================================================
```

---

### Stage 3 – Summary Statistics

```python
# Collect all averages (as floats, not strings)
averages = []
for row in raw_data:
    eng  = float(row[2])
    math = float(row[3])
    sci  = float(row[4])
    averages.append((eng + math + sci) / 3)

overall_avg = sum(averages) / len(averages)
highest     = max(averages)
lowest      = min(averages)

print("\nCLASS SUMMARY:")
print("Overall Average: " + str(round(overall_avg, 2)))
print("Highest Score:   " + str(round(highest, 2)))
print("Lowest Score:    " + str(round(lowest, 2)))
print("Students: "        + str(len(raw_data)))
```

**Expected Output:**
```
CLASS SUMMARY:
Overall Average: 80.9
Highest Score:   92.17
Lowest Score:    62.67
Students: 5
```

---

### Milestone Reflection

Look at what this project required:
- String data → float (`float(row[2])`) for calculations
- Float results → string (`str(round(...))`) for display and text joining
- String data → string (`str(row[0])`) to be explicit about type

Every single piece of work involved casting. This is what real data pipelines look like. Every app you use — banking, social media, school management — has code that looks exactly like this under the surface.

---

### Optional Extension Challenges

1. Add a column for the **highest individual subject score** per student (not average — just the single highest subject)
2. Count how many students passed (average ≥ 60) and how many failed, and print the counts using `str()` in a message
3. Find which subject (Eng, Math, Sci) had the highest class-wide average and report it

---

## Common Beginner Mistakes

---

### Mistake 1 – Using `int()` on a String with a Decimal

**Wrong:**
```python
x = int("3.5")   # ❌ ValueError
```

**Error:**
```
ValueError: invalid literal for int() with base 10: '3.5'
```

**Right — Chain through float first:**
```python
x = int(float("3.5"))   # ✅ → 3
```

**Why:** `int()` does not understand decimal strings. `float()` does. So convert to float first, then truncate to int.

---

### Mistake 2 – Thinking `int()` Rounds

**Wrong assumption:**
```python
x = int(9.9)   # You might expect 10
```

**Actual output:**
```
9
```

**Right — Use `round()` if you need proper rounding:**
```python
x = round(9.9)   # → 10
```

---

### Mistake 3 – Joining a Number to a String Without `str()`

**Wrong:**
```python
age = 25
message = "I am " + age + " years old."   # ❌ TypeError
```

**Right:**
```python
age = 25
message = "I am " + str(age) + " years old."   # ✅
```

---

### Mistake 4 – Thinking `str(42)` Still Behaves Like a Number

**Wrong assumption:**
```python
x = str(42)
print(x + 8)    # ❌ TypeError — x is now text, not a number
```

**Right:**
```python
x = str(42)
print(x + "8")    # ✅ → "428" (string joining, not addition!)
# OR
x = int(str(42))
print(x + 8)      # ✅ → 50 (convert back to int, then add)
```

---

### Mistake 5 – Passing Non-Numeric Text to `int()` or `float()`

**Wrong:**
```python
x = int("twenty")     # ❌ ValueError
y = float("hello")    # ❌ ValueError
```

**Right — Only pass strings that look like valid numbers:**
```python
x = int("20")         # ✅ → 20
y = float("3.14")     # ✅ → 3.14
```

---

### Mistake 6 – Forgetting That `float(1)` Gives `1.0`, Not `1`

**Wrong assumption:**
```python
x = float(1)
print(x == 1)    # You might doubt this...
```

**Actual output:**
```
True
```

Mathematically, `1.0 == 1` is `True` in Python — the values are equivalent. But their *types* differ. If you check `type(float(1)) == type(1)`, that is `False`. The value is the same; the category is different.

---

### Mistake 7 – Casting `None` or `True`/`False` with `int()` — Surprising Results

```python
print(int(True))     # → 1  (True is treated as 1)
print(int(False))    # → 0  (False is treated as 0)
```

**Expected Output:**
```
1
0
```

This is valid Python behaviour — booleans are actually a subtype of integer in Python. `True` is `1` and `False` is `0`. This can be very useful (for counting how many True values are in a list), but can also cause confusion if you accidentally pass a boolean where you expected a number.

---

## Reflection Questions

1. What is casting, in your own words? Use an analogy that is different from the currency exchange example in the introduction.
2. What is the difference between truncation and rounding? Give a specific example showing a case where they produce different results.
3. Why does `int("3.5")` fail, but `int(float("3.5"))` succeed? Walk through the steps.
4. You receive the value `"99"` from a text file. If you try to add `1` to it without casting, what error do you get? Write the fix.
5. When would you use `str()` to convert a number? Give two different real-world scenarios.
6. What does `float("3")` produce? Is the result mathematically the same as `int("3")`? Are they the same type?
7. A classmate says: "Casting changes the value of the data." Is this always true? Give an example where the value is preserved and one where information is lost.
8. What is a `ValueError` and in which casting scenarios might you encounter it?

---

## Completion Checklist

Before moving on, confirm you can say yes to all of the following:

- [ ] I can explain what casting is and why it is necessary
- [ ] I understand that Python uses constructor functions (classes) for casting
- [ ] I can use `int()` to cast from int, float, and valid string inputs
- [ ] I know that `int()` truncates (does NOT round) when converting from float
- [ ] I know that `int()` raises a `ValueError` for strings with decimals or non-numeric content
- [ ] I can use `float()` to cast from int, float, and valid string inputs (whole or decimal)
- [ ] I can use `str()` to convert integers, floats, and other values to text
- [ ] I know why `str()` is needed when joining numbers with text using `+`
- [ ] I can chain conversions: `int(float("3.7"))` to go from a decimal string to an integer
- [ ] I can use `type()` to verify that a cast worked correctly
- [ ] I can identify and fix the most common casting mistakes

---

## Lesson Summary

**Casting** is the act of explicitly converting a value from one data type to another. Python is strongly typed — different types cannot automatically mix, so casting is how you bridge them.

Python performs casting through **constructor functions**, which are named after the type they create. This works because Python is an object-oriented language where every data type is actually a class.

---

**`int()` — Constructs an Integer**

Accepts: integers, floats (truncates — never rounds), strings of whole numbers only.

```python
int(1)      → 1       # int from int
int(2.8)    → 2       # float → int (TRUNCATED, not rounded)
int("3")    → 3       # string whole number → int
int("3.5")  → ❌ ValueError    # string with decimal — not allowed
int("hi")   → ❌ ValueError    # non-numeric — not allowed
```

---

**`float()` — Constructs a Float**

Accepts: integers (adds `.0`), floats, strings of whole or decimal numbers.

```python
float(1)      → 1.0    # int → float (.0 added)
float(2.8)    → 2.8    # float from float
float("3")    → 3.0    # string int → float
float("4.2")  → 4.2    # string decimal → float
float("hi")   → ❌ ValueError   # non-numeric — not allowed
```

---

**`str()` — Constructs a String**

Accepts: almost anything — strings, integers, floats, booleans, None.

```python
str("s1")   → 's1'     # string from string
str(2)      → '2'      # int → string
str(3.0)    → '3.0'    # float → string (keeps decimal)
str(True)   → 'True'   # bool → string
str(None)   → 'None'   # None → string
```

---

**Key chaining pattern:**
```python
int(float("3.7"))   → 3   # str → float → int (the two-step route)
```

**Always verify with `type()`:**
```python
x = int("42")
print(type(x))    # <class 'int'>  ← confirmed!
```

---

> 🎉 **Congratulations!** You have completed Lesson 07. You now have a complete, practical understanding of Python casting — one of the most important everyday skills in programming. Data arrives in the wrong type constantly, and you now know exactly how to transform it. In the next lesson, you will explore **Python Strings** — learning how to slice, modify, format, and work with text data in powerful ways!
