---
render_with_liquid: false
title: "Lesson 06 — Python Numbers"
nav_order: 6
---

# Lesson 06 — Python Numbers

---

## Lesson Introduction

Numbers are at the heart of almost every program ever written. Whether you are calculating a student's grade, tracking account balances, measuring sensor readings, or running a machine learning model — numbers are involved. Python has a rich and precise system for working with numbers, and this lesson covers every part of it.

By the end of this lesson you will:

- Know the **three built-in number types** in Python: `int`, `float`, and `complex`.
- Understand what each type is, when to use it, and how it behaves.
- Use the `type()` function to inspect what kind of number you have.
- Understand how Python handles numbers of **unlimited size**.
- Know the difference between integer division and regular division.
- Generate **random numbers** using Python's `random` module.
- Use the built-in **`math` module** for advanced mathematical operations.
- Apply all of this in **realistic STEM and data scenarios**.

This lesson assumes you have completed Lessons 01–05 and are comfortable with variables, `print()`, and basic data types.

---

## Prerequisite Concepts

Before continuing, make sure you understand:

- **Variables** — how to create them and assign values (`x = 10`).
- **`print()`** — how to display values on the screen.
- **Data types** — the idea that values in Python have a type (from Lesson 05).
- **f-strings** — `f"The answer is {x}"` for formatted output.

If any of these feel unfamiliar, review Lesson 04 and Lesson 05 first.

---

## Part 1 — The Three Number Types in Python

Python has exactly **three built-in numeric types**:

| Type | Full Name | What it stores | Example |
|------|-----------|----------------|---------|
| `int` | Integer | Whole numbers, positive or negative, no decimal point | `42`, `-7`, `0` |
| `float` | Floating-Point Number | Numbers with a decimal point | `3.14`, `-0.5`, `2.0` |
| `complex` | Complex Number | Numbers with a real and imaginary part | `3+5j`, `2j` |

Let us explore each one deeply.

---

## Part 2 — Integers (`int`)

### What is an Integer?

An **integer** is a whole number — a number with no fractional or decimal part. Integers can be positive, negative, or zero.

**Real-world examples of integers:**
- Number of students in a class: `45`
- Temperature in whole degrees: `-3` (it is 3 degrees below zero)
- Year: `2026`
- Bank account balance (in whole Naira): `150000`
- Number of items in a shopping cart: `0` (empty cart)

**Mathematical definition:** Integers are members of the set `{..., -3, -2, -1, 0, 1, 2, 3, ...}`

### Creating Integers in Python

Simply assign a whole number to a variable — no decimal point, no quotes.

```python
x = 1
y = 35656222554887711
z = -3255522
```

**Displaying integers:**

```python
x = 1
y = 35656222554887711
z = -3255522

print(x)
print(y)
print(z)
```

**Expected Output:**
```
1
35656222554887711
-3255522
```

### Python Integers Have No Size Limit

This is one of Python's most impressive features. In many other programming languages (like C or Java), integers have a fixed maximum size — for example, a standard `int` in Java can hold values up to about 2.1 billion. If you exceed that, the program breaks in subtle ways.

**Python has no such limit.** A Python `int` can be as large as your computer's memory allows.

```python
# This is a perfectly valid Python integer!
huge_number = 99999999999999999999999999999999999999999999999999
print(huge_number)
```

**Expected Output:**
```
99999999999999999999999999999999999999999999999999
```

**Real-world relevance:** This matters in cryptography, astronomy (distances in metres), genomics (DNA base pair counts), and financial systems where extreme precision is required.

### Negative Integers

Use a minus sign (`-`) before the number:

```python
temperature = -15
debt = -75000
below_sea_level = -420

print(temperature)
print(debt)
print(below_sea_level)
```

**Expected Output:**
```
-15
-75000
-420
```

### Verifying the Type with `type()`

Python provides a built-in function called `type()` that tells you the **data type** of any value or variable.

```python
x = 42
print(type(x))
```

**Expected Output:**
```
<class 'int'>
```

This output means: "x belongs to the class (type) called `int`."

**Try it with different values:**

```python
print(type(100))
print(type(-7))
print(type(0))
```

**Expected Output:**
```
<class 'int'>
<class 'int'>
<class 'int'>
```

> **Thinking prompt:** What do you think `type("Hello")` would output? What about `type(True)`?

### Integer Arithmetic

You can perform all standard arithmetic operations on integers:

```python
a = 20
b = 6

print(a + b)    # Addition
print(a - b)    # Subtraction
print(a * b)    # Multiplication
print(a ** b)   # Exponentiation (power): 20 to the power of 6
print(a // b)   # Integer (floor) division — result is always a whole number
print(a % b)    # Modulus — the remainder after division
```

**Expected Output:**
```
26
14
120
64000000
3
2
```

**Line-by-line breakdown of the less obvious operations:**

- `a ** b` → `20 ** 6` → 20 × 20 × 20 × 20 × 20 × 20 → `64000000`
- `a // b` → `20 // 6` → How many times does 6 go into 20 completely? **3 times** (3 × 6 = 18, with 2 left over). Result: `3`
- `a % b` → `20 % 6` → What is the remainder when 20 is divided by 6? 20 - (3 × 6) = 20 - 18 = **2**. Result: `2`

> **Key insight — `//` vs `/`:** Notice that `20 // 6` gives `3` (an integer), but `20 / 6` would give `3.3333...` (a float). The `//` operator is called **floor division** because it rounds down to the nearest whole number.

```python
print(20 / 6)    # Regular division → float
print(20 // 6)   # Integer (floor) division → int
```

**Expected Output:**
```
3.3333333333333335
3
```

**Real-world use of `%` (modulus):**

The modulus operator is used in many practical scenarios:
- Checking if a number is even or odd: if `n % 2 == 0` then it is even.
- Clock arithmetic: what hour will it be 100 hours from now? `(current_hour + 100) % 24`
- Distributing items equally into groups.

```python
# Is 17 odd or even?
print(17 % 2)   # Output: 1 (remainder is 1, so 17 is odd)
print(16 % 2)   # Output: 0 (no remainder, so 16 is even)
```

---

## Part 3 — Floats (`float`)

### What is a Float?

A **float** (short for "floating-point number") is any number that contains a **decimal point**. The term "floating-point" refers to the way computers represent these numbers internally — the decimal point can "float" to different positions.

**Real-world examples of floats:**
- Temperature: `36.6` degrees Celsius (body temperature)
- Price: `1499.99` Naira
- Scientific measurement: `9.81` (acceleration due to gravity, m/s²)
- Percentage: `87.5` (a student's percentage score)
- GPS coordinate: `7.3776` (latitude of Ibadan, Nigeria)

### Creating Floats in Python

Simply include a decimal point in the number:

```python
x = 1.10
y = 1.0
z = -35.59
```

**Displaying floats:**

```python
x = 1.10
y = 1.0
z = -35.59

print(x)
print(y)
print(z)
```

**Expected Output:**
```
1.1
1.0
-35.59
```

Notice that `1.10` printed as `1.1` — Python automatically removes unnecessary trailing zeros (but keeps the decimal point to show it is still a float).

### Verifying Float Type

```python
x = 3.14
print(type(x))
```

**Expected Output:**
```
<class 'float'>
```

### Floats Can Use Scientific Notation (`e` notation)

For very large or very small numbers, Python supports scientific notation using the letter `e` (which means "times 10 to the power of").

**The format:** `mantissa e exponent`
- `1.5e3` means 1.5 × 10³ = 1.5 × 1000 = **1500.0**
- `1.5e-3` means 1.5 × 10⁻³ = 1.5 ÷ 1000 = **0.0015**

```python
x = 35e3      # 35 × 10³ = 35,000
y = 12E4      # 12 × 10⁴ = 120,000   (E and e are both valid)
z = -87.7e100 # -87.7 × 10¹⁰⁰ (an astronomically large number)

print(x)
print(y)
print(z)
```

**Expected Output:**
```
35000.0
120000.0
-8.77e+101
```

**Real-world use of scientific notation:**
- Physics: speed of light = `3e8` metres per second (3 × 10⁸)
- Chemistry: Avogadro's number ≈ `6.022e23`
- Finance: national debt figures
- Astronomy: distance from Earth to the Sun ≈ `1.496e11` metres

```python
# Speed of light in metres per second
speed_of_light = 3e8
print(f"Speed of light: {speed_of_light} m/s")

# Avogadro's number
avogadro = 6.022e23
print(f"Avogadro's number: {avogadro}")
```

**Expected Output:**
```
Speed of light: 300000000.0 m/s
Avogadro's number: 6.022e+23
```

### Float Arithmetic

All arithmetic operations work with floats just as with integers:

```python
a = 10.5
b = 3.2

print(a + b)
print(a - b)
print(a * b)
print(a / b)
print(a ** 2)
```

**Expected Output:**
```
13.7
7.300000000000001
33.6
3.28125
110.25
```

> **Notice something strange?** `10.5 - 3.2` printed as `7.300000000000001` instead of `7.3`. This is not a bug in Python — it is a known quirk of how computers store decimal numbers in binary (base-2). Most decimal fractions cannot be represented exactly in binary, so tiny rounding errors appear.

**This is called floating-point imprecision.** It affects every programming language that uses IEEE 754 floating-point standard (which is almost all of them).

**When does it matter?**
- For most everyday programs: not at all. The error is microscopic.
- For financial calculations: use Python's `decimal` module instead of `float`.
- For scientific computing: be aware of it when comparing floats.

**How to display a cleaner result:**

```python
result = 10.5 - 3.2
print(f"{result:.1f}")   # Format to 1 decimal place
```

**Expected Output:**
```
7.3
```

### Integer ÷ Integer = Float

An important Python rule: when you divide two integers using `/`, the result is **always a float**, even if the division is exact.

```python
print(10 / 2)   # Exactly 5, but Python gives a float
print(7 / 2)    # Not exact — definitely a float
```

**Expected Output:**
```
5.0
3.5
```

`10 / 2` gives `5.0` (a float), not `5` (an int). If you need a plain integer result, use `//` (floor division) instead.

---

## Part 4 — Complex Numbers (`complex`)

### What is a Complex Number?

A **complex number** has two parts:
- A **real part** — a regular number
- An **imaginary part** — a multiple of `j` (the imaginary unit, defined as √(-1))

**The format in Python:** `real + imaginaryj`

**Examples:**
- `3 + 5j` — real part is 3, imaginary part is 5
- `2j` — real part is 0, imaginary part is 2
- `1 - 4j` — real part is 1, imaginary part is -4

> **Mathematical background:** In mathematics, the imaginary unit is written as `i` (where `i² = -1`). In Python and engineering, it is written as `j` instead. Both mean the same thing.

### Why Do Complex Numbers Exist?

You might be wondering: "When would I ever use a square root of a negative number?" The answer surprises most people — complex numbers are used *constantly* in the real world:

- **Electrical engineering:** Analysing alternating current (AC) circuits — every electrical engineer uses complex numbers daily.
- **Signal processing:** Audio processing, radio waves, Wi-Fi signals.
- **Quantum physics:** The Schrödinger equation (the foundation of quantum mechanics) uses complex numbers.
- **Computer graphics:** Fractals (like the famous Mandelbrot set) are generated using complex arithmetic.
- **Control systems:** Designing autopilots, robotics, and stability systems.

### Creating Complex Numbers in Python

```python
x = 3 + 5j
y = 5j
z = -5j
```

**Displaying complex numbers:**

```python
x = 3 + 5j
y = 5j
z = -5j

print(x)
print(y)
print(z)
```

**Expected Output:**
```
(3+5j)
5j
(-0-5j)
```

### Verifying Complex Type

```python
x = 3 + 5j
print(type(x))
```

**Expected Output:**
```
<class 'complex'>
```

### Accessing the Real and Imaginary Parts

Every complex number object has `.real` and `.imag` attributes:

```python
z = 3 + 5j
print(z.real)    # The real part
print(z.imag)    # The imaginary part
```

**Expected Output:**
```
3.0
5.0
```

Notice that `.real` and `.imag` always return **floats**, even if the parts look like whole numbers.

### Basic Arithmetic with Complex Numbers

```python
a = 2 + 3j
b = 1 - 2j

print(a + b)   # Add real parts, add imaginary parts
print(a - b)   # Subtract real parts, subtract imaginary parts
print(a * b)   # Uses the rule (a+bj)(c+dj) = (ac-bd) + (ad+bc)j
```

**Expected Output:**
```
(3+1j)
(1+5j)
(8-1j)
```

**Verification of `a * b`:**

(2 + 3j) × (1 - 2j)
= (2×1) + (2×-2j) + (3j×1) + (3j×-2j)
= 2 - 4j + 3j - 6j²
= 2 - j - 6(-1)    ← because j² = -1
= 2 - j + 6
= 8 - j
= **(8-1j)** ✓

> **Beginner note:** You do not need to memorise complex number arithmetic right now. The important thing is knowing that this type exists in Python and where it is used professionally.

---

## Part 5 — The `type()` Function in Depth

You have seen `type()` used several times already. Let us look at it more carefully.

### What `type()` Does

`type()` is a built-in Python function that takes **one argument** and returns the **data type** (class) of that argument.

**Syntax:**
```python
type(value_or_variable)
```

### Using `type()` on All Three Number Types

```python
x = 1       # int
y = 2.8     # float
z = 1j      # complex

print(type(x))
print(type(y))
print(type(z))
```

**Expected Output:**
```
<class 'int'>
<class 'float'>
<class 'complex'>
```

### Using `type()` as a Condition Check

You can use `type()` to check whether a value is the type you expect:

```python
x = 42

if type(x) == int:
    print("x is an integer")
else:
    print("x is not an integer")
```

**Expected Output:**
```
x is an integer
```

> **Professional note:** In real Python code, developers often use `isinstance()` instead of `type() ==` for type checking, because `isinstance()` also handles inheritance. But for learning purposes, `type()` is perfect.

### `type()` Works on Any Python Object

`type()` is not limited to numbers — it works on any value:

```python
print(type("Hello"))      # <class 'str'>
print(type(True))         # <class 'bool'>
print(type([1, 2, 3]))    # <class 'list'>
print(type(None))         # <class 'NoneType'>
```

---

## Part 6 — Type Conversion Between Number Types

Python makes it easy to convert between number types using three built-in functions:

| Function | Converts to | Example |
|----------|-------------|---------|
| `int(x)` | Integer | `int(3.9)` → `3` |
| `float(x)` | Float | `float(5)` → `5.0` |
| `complex(x)` | Complex | `complex(3)` → `(3+0j)` |

### Converting to Integer with `int()`

```python
x = int(1)      # int from int (no change)
y = int(2.8)    # int from float — truncates (cuts off) the decimal part
z = int("3")    # int from string — only works if the string is a whole number

print(x)
print(y)
print(z)
print(type(x))
```

**Expected Output:**
```
1
2
3
<class 'int'>
```

> **Important:** `int(2.8)` does NOT round to 3. It **truncates** — it cuts off everything after the decimal point and keeps only the whole number part. So `int(2.9)` → `2`, and `int(-2.9)` → `-2` (not `-3`).

```python
print(int(2.1))    # 2
print(int(2.9))    # 2 (NOT 3!)
print(int(-2.9))   # -2 (NOT -3!)
```

**Expected Output:**
```
2
2
-2
```

**If you want proper rounding**, use Python's built-in `round()` function:

```python
print(round(2.9))    # 3 (rounds to nearest whole number)
print(round(2.5))    # 2 (Python uses "banker's rounding" — rounds to nearest even)
print(round(3.5))    # 4
```

### Converting to Float with `float()`

```python
x = float(1)      # float from int
y = float(2.8)    # float from float (no change)
z = float("3")    # float from string
w = float("4.2")  # float from string with decimal

print(x)
print(y)
print(z)
print(w)
```

**Expected Output:**
```
1.0
2.8
3.0
4.2
```

### Converting to Complex with `complex()`

```python
x = complex(1)       # complex from int → real part = 1, imaginary = 0
y = complex(2.8)     # complex from float → real part = 2.8, imaginary = 0
z = complex(1j)      # complex from imaginary
w = complex(1, 2)    # complex(real, imaginary) → 1 + 2j

print(x)
print(y)
print(z)
print(w)
```

**Expected Output:**
```
(1+0j)
(2.8+0j)
1j
(1+2j)
```

### What You CANNOT Convert

```python
# You CANNOT convert a complex number to int or float
c = 3 + 5j
print(int(c))    # ❌ Error!
```

**Error:**
```
TypeError: can't convert complex to int
```

This makes mathematical sense — a complex number has two components. You cannot collapse two numbers into one without losing information.

### Type Conversion Summary Table

| From → To | `int()` | `float()` | `complex()` |
|-----------|---------|-----------|-------------|
| `int` | ✅ (no change) | ✅ adds `.0` | ✅ adds `+0j` |
| `float` | ✅ truncates decimal | ✅ (no change) | ✅ adds `+0j` |
| `complex` | ❌ Error | ❌ Error | ✅ (no change) |
| `str` (numeric) | ✅ if whole number | ✅ if numeric | ❌ Error |

---

## Part 7 — Random Numbers

### Why Do We Need Random Numbers?

**Random numbers** are used in:
- **Games** — shuffling cards, rolling dice, spawning enemies at random locations
- **Security** — generating passwords, encryption keys, one-time codes (OTPs)
- **Scientific simulations** — Monte Carlo simulations, modelling random physical processes
- **Machine learning** — randomly splitting datasets, initialising neural network weights
- **Testing** — generating random test data
- **Lotteries and draws** — fair selection of winners

### Python Does Not Have a Built-in Random Number Function

Unlike `print()` or `type()`, random number generation is not a built-in function. You must **import** the `random` module first. A **module** is a collection of extra functions that Python does not load by default — you bring it in with the `import` keyword when you need it.

```python
import random
```

This one line gives you access to all the random number tools.

### Generating a Random Float Between 0 and 1

The most basic random function is `random.random()`, which returns a random float between 0.0 (inclusive) and 1.0 (exclusive):

```python
import random

print(random.random())
```

**Example Output (yours will differ — it is random!):**
```
0.7231857392814065
```

Every time you run this, you get a different number. That is the whole point.

### Generating a Random Integer in a Range

`random.randint(a, b)` returns a random integer between `a` and `b`, **inclusive on both ends** (unlike Python's `range()` which excludes the upper bound).

```python
import random

# Random integer between 1 and 10 (including 1 and 10)
print(random.randint(1, 10))
```

**Example Output:**
```
7
```

Run it again — you might get `3`, or `10`, or `1`. It is genuinely random.

**Simulating a dice roll:**

```python
import random

dice = random.randint(1, 6)
print(f"You rolled: {dice}")
```

**Example Output:**
```
You rolled: 4
```

**Generating multiple random integers:**

```python
import random

print(random.randint(1, 100))
print(random.randint(1, 100))
print(random.randint(1, 100))
```

**Example Output:**
```
73
12
91
```

### Other Useful `random` Module Functions

```python
import random

# random.uniform(a, b) — random float between a and b
temperature = random.uniform(20.0, 35.0)
print(f"Random temperature: {temperature:.2f}°C")

# random.choice(sequence) — pick a random item from a list
fruits = ["apple", "banana", "mango", "guava", "orange"]
chosen = random.choice(fruits)
print(f"Random fruit: {chosen}")

# random.shuffle(list) — shuffle a list in place
numbers = [1, 2, 3, 4, 5]
random.shuffle(numbers)
print(f"Shuffled: {numbers}")
```

**Example Output (yours will differ):**
```
Random temperature: 27.84°C
Random fruit: mango
Shuffled: [3, 1, 5, 2, 4]
```

### Setting a Random Seed (for Reproducibility)

In testing and scientific work, you sometimes want your "random" numbers to be **reproducible** — the same sequence every time. You can achieve this by setting a **seed**:

```python
import random

random.seed(42)   # Any integer can be the seed
print(random.randint(1, 100))
print(random.randint(1, 100))
print(random.randint(1, 100))
```

**Output (always the same when seed is 42):**
```
52
3
94
```

Run this code ten times — you will always get `52, 3, 94`. The seed makes the "random" sequence predictable, which is essential for debugging and reproducible research.

---

## Part 8 — The `math` Module

### What is the `math` Module?

The `math` module gives you access to **advanced mathematical functions** that go beyond basic arithmetic. It is part of Python's standard library — you do not need to install anything, just import it.

```python
import math
```

### Constants in the `math` Module

```python
import math

print(math.pi)     # π (pi) ≈ 3.14159...
print(math.e)      # Euler's number ≈ 2.71828...
print(math.tau)    # τ = 2π ≈ 6.28318...
print(math.inf)    # Positive infinity
print(math.nan)    # "Not a Number" (represents undefined/invalid results)
```

**Expected Output:**
```
3.141592653589793
2.718281828459045
6.283185307179586
inf
nan
```

### Square Root — `math.sqrt()`

```python
import math

print(math.sqrt(25))    # √25 = 5
print(math.sqrt(2))     # √2 ≈ 1.414...
print(math.sqrt(144))   # √144 = 12
```

**Expected Output:**
```
5.0
1.4142135623730951
12.0
```

> **Note:** `math.sqrt()` always returns a **float**, even if the result is a whole number (`5.0` not `5`).

**Real-world use:** Calculating the hypotenuse of a right-angled triangle (Pythagoras' theorem: c = √(a² + b²)):

```python
import math

a = 3
b = 4
c = math.sqrt(a**2 + b**2)
print(f"Hypotenuse: {c}")
```

**Expected Output:**
```
Hypotenuse: 5.0
```

### Ceiling and Floor — `math.ceil()` and `math.floor()`

These two functions round numbers, but in a specific direction:
- `math.ceil(x)` — **ceiling**: rounds **up** to the nearest integer
- `math.floor(x)` — **floor**: rounds **down** to the nearest integer

```python
import math

x = 1.4
y = 1.9
z = -1.4
w = -1.9

print("ceil:")
print(math.ceil(x))    # 2
print(math.ceil(y))    # 2
print(math.ceil(z))    # -1  (rounds up toward zero for negatives)
print(math.ceil(w))    # -1

print("floor:")
print(math.floor(x))   # 1
print(math.floor(y))   # 1
print(math.floor(z))   # -2  (rounds down away from zero for negatives)
print(math.floor(w))   # -2
```

**Expected Output:**
```
ceil:
2
2
-1
-1
floor:
1
1
-2
-2
```

**Analogy for ceil/floor:**

Imagine a building where each floor is numbered. If you are at level 1.4 (between floor 1 and floor 2):
- `ceil(1.4)` = 2 → "go up to the next complete floor"
- `floor(1.4)` = 1 → "go down to the current complete floor"

**Real-world use of `ceil`:** Calculating how many buses you need to transport a group of people:

```python
import math

passengers = 47
seats_per_bus = 15

buses_needed = math.ceil(passengers / seats_per_bus)
print(f"Buses needed: {buses_needed}")
```

**Expected Output:**
```
Buses needed: 4
```

Why `ceil`? Because `47 / 15 = 3.133...` — you cannot have a third of a bus. You need 4 complete buses.

### Absolute Value — `math.fabs()` and `abs()`

`abs(x)` returns the **absolute value** (distance from zero) of a number — always positive.
`math.fabs(x)` does the same but always returns a float.

```python
import math

print(abs(-7))         # 7   (int)
print(abs(-3.5))       # 3.5 (float)
print(math.fabs(-7))   # 7.0 (always float)
```

**Expected Output:**
```
7
3.5
7.0
```

**Real-world use:** Calculating the difference between two measurements regardless of direction:

```python
measured = 98.6
actual = 100.0
error = abs(measured - actual)
print(f"Measurement error: {error:.1f}")
```

**Expected Output:**
```
Measurement error: 1.4
```

### Power — `math.pow()`

`math.pow(x, y)` raises `x` to the power of `y`. Unlike the `**` operator, it always returns a float.

```python
import math

print(math.pow(2, 10))    # 2¹⁰ = 1024
print(math.pow(3, 3))     # 3³ = 27
print(2 ** 10)             # Also works, returns int
```

**Expected Output:**
```
1024.0
27.0
1024
```

### Logarithms — `math.log()`

`math.log(x)` returns the **natural logarithm** (base *e*) of x.
`math.log(x, base)` returns the logarithm of x with a specified base.
`math.log10(x)` returns the base-10 logarithm.
`math.log2(x)` returns the base-2 logarithm.

```python
import math

print(math.log(math.e))    # Natural log of e = 1.0
print(math.log(100, 10))   # log₁₀(100) = 2.0
print(math.log10(1000))    # log₁₀(1000) = 3.0
print(math.log2(8))        # log₂(8) = 3.0
```

**Expected Output:**
```
1.0
2.0
2.9999999999999996
3.0
```

> `math.log(100, 10)` shows a tiny floating-point imprecision (`2.9999...` instead of `3.0`). Use `math.log10()` for base-10 calculations — it is more accurate.

**Real-world use:** Calculating compound interest time periods, decibel levels, earthquake magnitude (Richter scale), pH calculations in chemistry.

### Trigonometric Functions

`math` includes the full set of trigonometric functions used in physics, engineering, and navigation. Angles are in **radians** by default.

```python
import math

# Convert 90 degrees to radians first
angle_degrees = 90
angle_radians = math.radians(angle_degrees)

print(math.sin(angle_radians))    # sin(90°) = 1.0
print(math.cos(angle_radians))    # cos(90°) ≈ 0.0 (tiny float imprecision)
print(math.tan(math.radians(45))) # tan(45°) = 1.0
```

**Expected Output:**
```
1.0
6.123233995736766e-17
0.9999999999999999
```

> The very small values instead of exact 0.0 and 1.0 are due to floating-point imprecision — mathematically they should be exactly 0 and 1.

### Converting Degrees and Radians

```python
import math

# Degrees → Radians
print(math.radians(180))    # π
print(math.radians(90))     # π/2

# Radians → Degrees
print(math.degrees(math.pi))         # 180.0
print(math.degrees(math.pi / 2))     # 90.0
```

**Expected Output:**
```
3.141592653589793
1.5707963267948966
180.0
90.0
```

### Other Useful `math` Functions

```python
import math

# Factorial: n! = n × (n-1) × ... × 2 × 1
print(math.factorial(5))    # 5! = 120
print(math.factorial(10))   # 10! = 3628800

# GCD: Greatest Common Divisor
print(math.gcd(24, 36))     # 12

# isfinite, isinf, isnan
print(math.isfinite(100))       # True
print(math.isinf(math.inf))     # True
print(math.isnan(math.nan))     # True
```

**Expected Output:**
```
120
3628800
12
True
True
True
```

### Quick Reference — `math` Module

| Function | Description | Example | Output |
|----------|-------------|---------|--------|
| `math.sqrt(x)` | Square root | `math.sqrt(16)` | `4.0` |
| `math.ceil(x)` | Round up | `math.ceil(2.1)` | `3` |
| `math.floor(x)` | Round down | `math.floor(2.9)` | `2` |
| `math.fabs(x)` | Absolute value (float) | `math.fabs(-5)` | `5.0` |
| `math.pow(x, y)` | Power (float result) | `math.pow(2, 8)` | `256.0` |
| `math.log(x)` | Natural log (base e) | `math.log(math.e)` | `1.0` |
| `math.log10(x)` | Log base 10 | `math.log10(100)` | `2.0` |
| `math.log2(x)` | Log base 2 | `math.log2(8)` | `3.0` |
| `math.sin(x)` | Sine (radians) | `math.sin(0)` | `0.0` |
| `math.cos(x)` | Cosine (radians) | `math.cos(0)` | `1.0` |
| `math.tan(x)` | Tangent (radians) | `math.tan(0)` | `0.0` |
| `math.radians(x)` | Degrees → Radians | `math.radians(180)` | `3.14159...` |
| `math.degrees(x)` | Radians → Degrees | `math.degrees(math.pi)` | `180.0` |
| `math.factorial(n)` | n! | `math.factorial(5)` | `120` |
| `math.gcd(a, b)` | Greatest common divisor | `math.gcd(12, 8)` | `4` |
| `math.pi` | π constant | `math.pi` | `3.14159...` |
| `math.e` | Euler's number | `math.e` | `2.71828...` |
| `math.inf` | Positive infinity | `math.inf` | `inf` |

---

## Guided Practice Exercises

### Exercise 1 — Identify the Number Type

**Objective:** Practice using `type()` to inspect values.

For each of the following, predict the type before running the code, then verify with `type()`:

```python
a = 100
b = -3.5
c = 2 + 4j
d = 3e5
e = 1.0
f = 0
g = -0.0001

print(type(a))
print(type(b))
print(type(c))
print(type(d))
print(type(e))
print(type(f))
print(type(g))
```

**Expected Output:**
```
<class 'int'>
<class 'float'>
<class 'complex'>
<class 'float'>
<class 'float'>
<class 'int'>
<class 'float'>
```

**Self-check:** Were your predictions correct? Which ones surprised you?
- `d = 3e5` → float (scientific notation is always a float)
- `e = 1.0` → float (the `.0` makes it a float, not an int)
- `f = 0` → int (zero without a decimal point is an integer)

---

### Exercise 2 — Temperature Converter (int/float arithmetic)

**Objective:** Use float arithmetic in a real-world calculation.

**Scenario:** Build a simple temperature converter that converts Celsius to Fahrenheit and Kelvin.

**Formula:**
- Fahrenheit = (Celsius × 9/5) + 32
- Kelvin = Celsius + 273.15

```python
# Temperature in Celsius
celsius = 100.0   # Boiling point of water

# Convert to Fahrenheit
fahrenheit = (celsius * 9 / 5) + 32

# Convert to Kelvin
kelvin = celsius + 273.15

# Display results
print(f"Temperature Conversions")
print(f"-----------------------")
print(f"Celsius    : {celsius}°C")
print(f"Fahrenheit : {fahrenheit}°F")
print(f"Kelvin     : {kelvin} K")
```

**Expected Output:**
```
Temperature Conversions
-----------------------
Celsius    : 100.0°C
Fahrenheit : 212.0°F
Kelvin     : 373.15 K
```

**Challenge:** Change `celsius` to `37.0` (normal body temperature) and rerun. What do you get?

---

### Exercise 3 — Random Number Games

**Objective:** Use the `random` module in three different scenarios.

```python
import random

# Scenario 1: Simulate a coin flip
coin = random.randint(0, 1)
result = "Heads" if coin == 0 else "Tails"
print(f"Coin flip: {result}")

# Scenario 2: Pick a random student from a list
students = ["Chidi", "Amaka", "Tunde", "Ngozi", "Emeka", "Blessing"]
winner = random.choice(students)
print(f"Selected student: {winner}")

# Scenario 3: Generate a random exam score (between 50 and 100)
score = random.randint(50, 100)
print(f"Random exam score: {score}/100")
```

**Example Output (yours will differ):**
```
Coin flip: Heads
Selected student: Ngozi
Random exam score: 78
```

---

### Exercise 4 — Circle Calculations (math module)

**Objective:** Use `math.pi`, `math.sqrt()`, and `math.pow()` together.

**Scenario:** A civil engineer needs to calculate properties of a circular water tank.

```python
import math

# Radius of the tank in metres
radius = 4.5

# Area of the circle: A = π × r²
area = math.pi * math.pow(radius, 2)

# Circumference: C = 2 × π × r
circumference = 2 * math.pi * radius

# Diameter
diameter = 2 * radius

# Volume of a cylindrical tank with height 3m: V = π × r² × h
height = 3.0
volume = math.pi * math.pow(radius, 2) * height

print(f"=== Circular Tank Calculations ===")
print(f"Radius        : {radius} m")
print(f"Diameter      : {diameter} m")
print(f"Area          : {area:.2f} m²")
print(f"Circumference : {circumference:.2f} m")
print(f"Volume (h=3m) : {volume:.2f} m³")
```

**Expected Output:**
```
=== Circular Tank Calculations ===
Radius        : 4.5 m
Diameter      : 9.0 m
Area          : 63.62 m²
Circumference : 28.27 m
Volume (h=3m) : 190.85 m³
```

---

### Exercise 5 — Floor Division and Modulus (Practical)

**Objective:** Use `//` and `%` to solve a real-world grouping problem.

**Scenario:** A school has 157 students to be divided into groups of 12 for a field trip.

```python
total_students = 157
group_size = 12

# How many complete groups?
complete_groups = total_students // group_size

# How many students are left over?
remaining = total_students % group_size

print(f"Total students : {total_students}")
print(f"Group size     : {group_size}")
print(f"Complete groups: {complete_groups}")
print(f"Remaining      : {remaining} student(s)")
print(f"Extra group?   : {'Yes' if remaining > 0 else 'No'}")
```

**Expected Output:**
```
Total students : 157
Group size     : 12
Complete groups: 13
Remaining      : 1 student(s)
Extra group?   : Yes
```

**Verification:** 13 × 12 = 156, with 1 student left over. ✓

---

## Mini Project — Scientific Calculator

Let us build a complete, well-commented scientific calculator that uses everything from this lesson.

### Project: The Python Scientist's Calculator

**Goal:** A program that accepts a number and performs a full set of calculations on it — arithmetic, type checking, random generation, and mathematical functions.

```python
import math
import random

# ============================================================
# PYTHON SCIENTIST'S CALCULATOR
# Demonstrates: int, float, type(), math module, random module
# ============================================================

print("=" * 55)
print("         PYTHON SCIENTIST'S CALCULATOR")
print("=" * 55)

# --- Section 1: Number Types ---
print("\n[ NUMBER TYPES ]")
a = 42
b = 3.14159
c = 2 + 3j

print(f"  a = {a}  →  type: {type(a).__name__}")
print(f"  b = {b}  →  type: {type(b).__name__}")
print(f"  c = {c}  →  type: {type(c).__name__}")

# --- Section 2: Integer Arithmetic ---
print("\n[ INTEGER ARITHMETIC  (x = 17, y = 5) ]")
x, y = 17, 5
print(f"  {x} + {y}  = {x + y}")
print(f"  {x} - {y}  = {x - y}")
print(f"  {x} * {y}  = {x * y}")
print(f"  {x} / {y}  = {x / y:.4f}  (float division)")
print(f"  {x} // {y} = {x // y}     (floor division)")
print(f"  {x} % {y}  = {x % y}      (remainder/modulus)")
print(f"  {x} ** {y} = {x ** y}  (exponentiation)")

# --- Section 3: Type Conversion ---
print("\n[ TYPE CONVERSION ]")
num = 7.85
print(f"  Original  : {num}  ({type(num).__name__})")
print(f"  int({num}) : {int(num)}    ({type(int(num)).__name__})  ← truncated!")
print(f"  round({num}): {round(num)}    ({type(round(num)).__name__}) ← rounded")
print(f"  float(7)  : {float(7)}  ({type(float(7)).__name__})")

# --- Section 4: Math Functions ---
print("\n[ MATH MODULE FUNCTIONS  (n = 81) ]")
n = 81
print(f"  math.sqrt({n})      = {math.sqrt(n)}")
print(f"  math.floor(3.7)    = {math.floor(3.7)}")
print(f"  math.ceil(3.2)     = {math.ceil(3.2)}")
print(f"  math.factorial(6)  = {math.factorial(6)}")
print(f"  math.log10(1000)   = {math.log10(1000)}")
print(f"  math.pi            = {math.pi:.6f}")
print(f"  math.e             = {math.e:.6f}")

# --- Section 5: Random Numbers ---
print("\n[ RANDOM MODULE ]")
print(f"  random.randint(1, 100)    = {random.randint(1, 100)}")
print(f"  random.uniform(0.0, 1.0) = {random.uniform(0.0, 1.0):.4f}")
print(f"  random.choice(['A','B','C','D']) = {random.choice(['A','B','C','D'])}")

# --- Section 6: Scientific Application ---
print("\n[ SCIENTIFIC APPLICATION: Projectile Motion ]")
print("  (Ball thrown at 45° with initial speed 20 m/s)")
v0 = 20.0               # initial speed (m/s)
angle_deg = 45.0        # launch angle (degrees)
g = 9.81                # gravity (m/s²)
angle_rad = math.radians(angle_deg)

max_height = (v0 * math.sin(angle_rad))**2 / (2 * g)
range_dist = (v0**2 * math.sin(2 * angle_rad)) / g
time_flight = (2 * v0 * math.sin(angle_rad)) / g

print(f"  Max Height   : {max_height:.2f} m")
print(f"  Range        : {range_dist:.2f} m")
print(f"  Flight Time  : {time_flight:.2f} s")

print("\n" + "=" * 55)
print("  Calculations complete!")
print("=" * 55)
```

**Expected Output:**
```
=======================================================
         PYTHON SCIENTIST'S CALCULATOR
=======================================================

[ NUMBER TYPES ]
  a = 42  →  type: int
  b = 3.14159  →  type: float
  c = (2+3j)  →  type: complex

[ INTEGER ARITHMETIC  (x = 17, y = 5) ]
  17 + 5  = 22
  17 - 5  = 12
  17 * 5  = 85
  17 / 5  = 3.4000  (float division)
  17 // 5 = 3     (floor division)
  17 % 5  = 2      (remainder/modulus)
  17 ** 5 = 1419857  (exponentiation)

[ TYPE CONVERSION ]
  Original  : 7.85  (float)
  int(7.85) : 7    (int)  ← truncated!
  round(7.85): 8    (int) ← rounded
  float(7)  : 7.0  (float)

[ MATH MODULE FUNCTIONS  (n = 81) ]
  math.sqrt(81)      = 9.0
  math.floor(3.7)    = 3
  math.ceil(3.2)     = 4
  math.factorial(6)  = 720
  math.log10(1000)   = 2.9999999999999996
  math.pi            = 3.141593
  math.e             = 2.718282

[ RANDOM MODULE ]
  random.randint(1, 100)    = 63
  random.uniform(0.0, 1.0) = 0.4821
  random.choice(['A','B','C','D']) = C

[ SCIENTIFIC APPLICATION: Projectile Motion ]
  (Ball thrown at 45° with initial speed 20 m/s)
  Max Height   : 10.19 m
  Range        : 40.77 m
  Flight Time  : 2.88 s

=======================================================
  Calculations complete!
=======================================================
```

**Reflection Questions:**
- Why is `int(7.85)` = 7 and not 8? What function gives 8?
- In the random section, your output will differ from the example. Why?
- In the projectile motion section, what does `math.sin()` and `math.radians()` do?
- What would happen if you changed the launch angle to 90°? What would the range be?
- Which number type — `int`, `float`, or `complex` — is most commonly used in everyday programming?

**Optional Advanced Extensions:**
1. Add a section that generates 5 random exam scores, calculates their average, and displays a summary.
2. Add a Pythagorean theorem calculator that takes two sides `a` and `b` and computes the hypotenuse.
3. Create a compound interest calculator using `math.pow()`: `A = P × (1 + r/n)^(nt)`.

---

## Common Beginner Mistakes

### Mistake 1 — Confusing `/` and `//`

**Wrong understanding:**
```python
result = 7 / 2
print(result)    # Expecting 3
```

**Actual Output:**
```
3.5
```

**Fix — use `//` for whole-number (floor) division:**
```python
result = 7 // 2
print(result)    # 3
```

---

### Mistake 2 — Assuming `int()` Rounds

**Wrong understanding:**
```python
print(int(9.9))   # Expecting 10 (rounded)
```

**Actual Output:**
```
9
```

`int()` **truncates** (chops off the decimal), it does not round. Use `round()` for rounding.

**Fix:**
```python
print(round(9.9))   # 10 — properly rounded
```

---

### Mistake 3 — Forgetting to `import random` or `import math`

**Wrong:**
```python
print(random.randint(1, 10))   # No import!
```

**Error:**
```
NameError: name 'random' is not defined
```

**Fix — always import at the top of your file:**
```python
import random
print(random.randint(1, 10))
```

---

### Mistake 4 — Using `math.sqrt()` on a Negative Number

**Wrong:**
```python
import math
print(math.sqrt(-4))
```

**Error:**
```
ValueError: math domain error
```

**Why:** The square root of a negative number is an imaginary number, which `math.sqrt()` cannot handle. Use `cmath.sqrt()` (the complex math module) instead:

```python
import cmath
print(cmath.sqrt(-4))   # Output: 2j
```

---

### Mistake 5 — Expecting `random.randint()` to Exclude the Upper Bound

**Common confusion** (mixing up with Python's `range()` which excludes the upper bound):

```python
import random
# This CAN produce 10 — both endpoints are inclusive!
print(random.randint(1, 10))
```

`random.randint(a, b)` includes **both** `a` and `b`.
`range(a, b)` includes `a` but excludes `b`.

---

### Mistake 6 — Floating-Point Comparison

**Wrong:**
```python
result = 0.1 + 0.2
if result == 0.3:
    print("Equal!")
else:
    print("Not equal!")
```

**Output:**
```
Not equal!
```

**Why:** `0.1 + 0.2` in floating-point binary is `0.30000000000000004`, not exactly `0.3`.

**Fix — use rounding or a tolerance threshold:**
```python
result = 0.1 + 0.2
if round(result, 10) == round(0.3, 10):
    print("Equal!")
```

**Output:**
```
Equal!
```

---

### Mistake 7 — Trying to Convert Complex to int/float

**Wrong:**
```python
z = 3 + 4j
print(int(z))    # Trying to convert complex to int
```

**Error:**
```
TypeError: can't convert complex to int
```

**Fix — extract the real part first if that is what you need:**
```python
z = 3 + 4j
print(int(z.real))    # 3
```

---

## Reflection Questions

1. What are the three numeric types in Python? Give one real-world example of when you would use each.
2. Can a Python integer be larger than 1 billion? What about 1 trillion? What is the limit?
3. What is the difference between `/` and `//`? Give an example that shows why the distinction matters.
4. What is floating-point imprecision? Give an example. Why does it happen?
5. What does scientific notation `1.5e4` mean? What is the value?
6. What does `type(3.14)` return? What does it tell you?
7. Why can you NOT convert a complex number directly to a float?
8. What does `int(7.99)` return? Is it 8? Why or why not?
9. What module do you need to import to generate random numbers?
10. What is the difference between `random.randint(1, 10)` and `range(1, 10)` in terms of whether the upper bound is included?
11. What is `math.ceil()` and `math.floor()`? Give a real-world scenario where `math.ceil()` is the right choice.
12. What does `math.pi` return? Where would you use it in a real program?
13. What is the difference between `math.pow(2, 8)` and `2 ** 8`?
14. What is a random seed, and why would a scientist or developer want to set one?
15. In which professional fields are complex numbers regularly used?

---

## Completion Checklist

Tick each item when you can do it without looking at your notes.

- [ ] I can name the three Python number types: `int`, `float`, `complex`.
- [ ] I can give a real-world example of when to use each type.
- [ ] I can create variables of all three types and verify with `type()`.
- [ ] I understand that Python `int` has no maximum size limit.
- [ ] I understand the difference between `/` (float division) and `//` (floor division).
- [ ] I understand the `%` (modulus) operator and can give a practical example.
- [ ] I can write numbers using scientific notation (`e` notation).
- [ ] I understand what floating-point imprecision is and why it happens.
- [ ] I can convert between `int`, `float`, and `complex` using `int()`, `float()`, `complex()`.
- [ ] I know that `int()` truncates (does NOT round) and can use `round()` correctly.
- [ ] I can import and use the `random` module.
- [ ] I can use `random.randint()`, `random.random()`, `random.choice()`, and `random.shuffle()`.
- [ ] I know that `random.randint(a, b)` includes both endpoints.
- [ ] I understand what a random seed does and how to set one.
- [ ] I can import and use the `math` module.
- [ ] I can use `math.sqrt()`, `math.ceil()`, `math.floor()`, `math.pow()`, `math.fabs()`.
- [ ] I know the values of `math.pi` and `math.e`.
- [ ] I can use `math.log()`, `math.log10()`, `math.log2()`.
- [ ] I can use `math.sin()`, `math.cos()`, `math.radians()`, `math.degrees()`.
- [ ] I have identified and can fix all 7 common beginner mistakes.
- [ ] I have completed all 5 guided practice exercises.
- [ ] I have built and run the Scientific Calculator mini project.

---

## Lesson Summary

### The Three Number Types

| Type | Example | Created when | `type()` output |
|------|---------|--------------|-----------------|
| `int` | `42`, `-7`, `0` | No decimal point | `<class 'int'>` |
| `float` | `3.14`, `-0.5`, `1.0`, `2e3` | Has decimal point or uses `e` notation | `<class 'float'>` |
| `complex` | `3+5j`, `2j` | Uses `j` for imaginary part | `<class 'complex'>` |

### Key Rules
- `int` has **no size limit** in Python.
- `/` always returns a **float**; `//` (floor division) returns an **int**.
- `%` (modulus) returns the **remainder** after floor division.
- `int()` **truncates** (does not round); use `round()` for rounding.
- You **cannot** convert `complex` directly to `int` or `float`.
- Floating-point numbers can have **tiny imprecision** due to binary representation.

### Type Conversion
```python
int(3.9)       # → 3  (truncated, not rounded)
float(5)       # → 5.0
complex(2)     # → (2+0j)
complex(1, 3)  # → (1+3j)
round(3.9)     # → 4  (properly rounded)
```

### Random Numbers
```python
import random
random.random()           # float in [0.0, 1.0)
random.randint(1, 10)     # int from 1 to 10 inclusive
random.uniform(0.0, 5.0)  # float in [0.0, 5.0]
random.choice(my_list)    # random element from list
random.shuffle(my_list)   # shuffle list in place
random.seed(42)           # make results reproducible
```

### Math Module
```python
import math
math.sqrt(x)         # square root
math.ceil(x)         # round up
math.floor(x)        # round down
math.fabs(x)         # absolute value (float)
math.pow(x, y)       # x to the power y (float)
math.log10(x)        # base-10 logarithm
math.sin/cos/tan(x)  # trig functions (x in radians)
math.radians(deg)    # degrees → radians
math.degrees(rad)    # radians → degrees
math.factorial(n)    # n!
math.pi              # 3.14159...
math.e               # 2.71828...
```

---

> **What comes next?** In Lesson 07 we will explore **Python Casting** — a deeper look at type conversion, including how to convert between number types and string types, and the special rules that apply. Casting is an essential skill whenever you take user input or read data from files, since all input starts as text.

---

*Source: W3Schools Python Tutorial — [python_numbers.asp](https://www.w3schools.com/python/python_numbers.asp)*
