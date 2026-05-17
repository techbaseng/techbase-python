---
render_with_liquid: false
title: "NumPy ufuncs — Creating Functions, Arithmetic, Rounding, Logs & Summations"
nav_order: 28
---

# Lesson 28 — NumPy ufuncs: Creating Functions, Arithmetic, Rounding, Logs & Summations

---

## Lesson Introduction

Welcome to Lesson 28! In this lesson you will learn about one of NumPy's most powerful features: **ufuncs** (Universal Functions).

By the end of this lesson you will be able to:

- Understand what a ufunc is and why it exists
- Create your own custom ufunc using `frompyfunc()`
- Use built-in ufuncs for arithmetic: add, subtract, multiply, divide, power, mod
- Round decimal numbers using truncation, fix, around, floor, and ceil
- Work with logarithms at base 2, base 10, base e, and any custom base
- Use `sum()`, axis-based summation, and cumulative sum (`cumsum()`)
- Build a realistic mini-project combining all of these skills

No prior knowledge of ufuncs is needed. We will build everything from scratch.

---

## Prerequisite Concepts

Before diving in, let's make sure you understand a few building blocks.

### What is NumPy?

NumPy is a Python library used for working with numbers in large collections called **arrays**. Instead of writing a loop to process 1000 numbers one by one, NumPy lets you do it all at once in a single line — much faster and cleaner.

```python
import numpy as np

arr = np.array([10, 20, 30, 40])
print(arr * 2)
```

**Output:**
```
[20 40 60 80]
```

Every number in the array was multiplied by 2 in one step. That is the power of NumPy.

### What is a Regular Python Function?

A regular function in Python takes one or more inputs and returns an output:

```python
def double(x):
    return x * 2

print(double(5))
```

**Output:**
```
10
```

This works fine for a single number, but it cannot automatically work on an entire array. That is where ufuncs come in.

### What is an Array?

An array is like a list, but optimised for math. It can hold many numbers:

```python
import numpy as np

scores = np.array([85, 90, 78, 92, 88])
print(scores)
```

**Output:**
```
[85 90 78 92 88]
```

---

## Part 1 — What is a ufunc (Universal Function)?

### What is it?

A **ufunc** (short for Universal Function) is a special kind of function in NumPy that operates **element by element** on entire arrays automatically.

Think of it like this: imagine you have a factory assembly line. A regular function processes one item, picks it up, works on it, and puts it down. A ufunc is like an advanced machine that can process all items on the belt simultaneously — every element at the same time.

### Why does it exist?

Without ufuncs, you would need to write a loop like this to add two arrays:

```python
a = [1, 2, 3]
b = [4, 5, 6]
result = []

for i in range(len(a)):
    result.append(a[i] + b[i])

print(result)
```

**Output:**
```
[5, 7, 9]
```

This works, but it is slow and verbose. A ufunc does this in one line and runs much faster because it is written in optimised low-level code (C language) under the hood.

### NumPy already has many ufuncs built in

Functions like `np.add()`, `np.multiply()`, `np.log()`, and `np.sqrt()` are all ufuncs. You can also **create your own**.

---

## Part 2 — Creating Your Own ufunc with `frompyfunc()`

### How to create a custom ufunc

To turn your own Python function into a NumPy ufunc, you use the method `np.frompyfunc()`.

It takes three arguments:

1. The **function** you want to convert
2. The **number of input arrays** (inputs)
3. The **number of output arrays** (outputs)

### Syntax

```python
np.frompyfunc(function_name, number_of_inputs, number_of_outputs)
```

### Step-by-step simple example

Let's create a ufunc that adds two numbers together.

```python
import numpy as np

# Step 1: Define a regular Python function
def myadd(x, y):
    return x + y

# Step 2: Convert it into a ufunc
myadd = np.frompyfunc(myadd, 2, 1)
# Arguments: function, 2 inputs (x and y), 1 output

# Step 3: Use it on two arrays
result = myadd([1, 2, 3, 4], [5, 6, 7, 8])
print(result)
```

**Output:**
```
[6 8 10 12]
```

**Breaking it down line by line:**

- `def myadd(x, y):` — defines a regular function that adds two values
- `return x + y` — returns the sum
- `np.frompyfunc(myadd, 2, 1)` — wraps `myadd` into a ufunc. `2` means it takes 2 inputs; `1` means it produces 1 output
- `myadd([1,2,3,4], [5,6,7,8])` — applies the ufunc to every pair: `1+5`, `2+6`, `3+7`, `4+8`

> **Thinking Prompt:** What would happen if you changed `[5, 6, 7, 8]` to `[10, 10, 10, 10]`? Try to predict the output before running it.

---

### How to check if a function is a ufunc

You can check whether any NumPy function is a ufunc by checking its **type**. A genuine ufunc will return `<class 'numpy.ufunc'>`.

#### Example 1 — Check a known ufunc

```python
import numpy as np

print(type(np.add))
```

**Output:**
```
<class 'numpy.ufunc'>
```

`np.add` is a ufunc — confirmed.

#### Example 2 — Check a non-ufunc function

```python
import numpy as np

print(type(np.concatenate))
```

**Output:**
```
<class 'builtin_function_or_method'>
```

`np.concatenate` is a built-in NumPy function but **not** a ufunc — notice the different type.

#### Example 3 — Check something that doesn't exist (produces an error)

```python
import numpy as np

print(type(np.blahblah))
```

**Output:**
```
AttributeError: module 'numpy' has no attribute 'blahblah'
```

NumPy raises an error if the function doesn't exist at all.

#### Example 4 — Use an if statement to check

You can write a proper check using an `if` statement:

```python
import numpy as np

if type(np.add) == np.ufunc:
    print('add is ufunc')
else:
    print('add is not ufunc')
```

**Output:**
```
add is ufunc
```

**Why is this useful?** In real projects, you might receive a function from someone else or load it dynamically. This check lets you verify it behaves like a ufunc before using it on large arrays.

---

### Second custom ufunc example — squaring a number

```python
import numpy as np

def mysquare(x):
    return x * x

mysquare = np.frompyfunc(mysquare, 1, 1)
# 1 input, 1 output

result = mysquare([2, 3, 4, 5])
print(result)
```

**Output:**
```
[4 9 16 25]
```

Every number in the array was squared automatically.

> **Real-world use:** In physics, squaring values is common — for example, calculating kinetic energy (`½mv²`) for every object in a simulation simultaneously.

---

## Part 3 — Simple Arithmetic ufuncs

NumPy provides ready-made ufuncs for all common arithmetic operations. The big advantage over using Python's `+`, `-`, `*`, `/` operators directly is that these functions can accept lists, tuples, or any array-like object, and they support an optional `where` parameter that lets you apply the operation **only where a condition is true**.

> **Key concept — Arithmetic Conditionally:** You can tell NumPy to only perform the calculation on elements that meet a condition. We will focus on the core functions first, then explore conditional usage.

---

### 3.1 Addition — `np.add()`

The `add()` function adds corresponding elements from two arrays and returns a new array.

```python
import numpy as np

arr1 = np.array([10, 11, 12, 13, 14, 15])
arr2 = np.array([20, 21, 22, 23, 24, 25])

newarr = np.add(arr1, arr2)

print(newarr)
```

**Output:**
```
[30 32 34 36 38 40]
```

**How it works:** Each pair is added position by position — `10+20=30`, `11+21=32`, `12+22=34`, and so on.

> **Thinking Prompt:** What would happen if arr1 had 6 elements and arr2 had only 3?

---

### 3.2 Subtraction — `np.subtract()`

The `subtract()` function subtracts corresponding elements of the second array from the first.

```python
import numpy as np

arr1 = np.array([10, 20, 30, 40, 50, 60])
arr2 = np.array([20, 21, 22, 23, 24, 25])

newarr = np.subtract(arr1, arr2)

print(newarr)
```

**Output:**
```
[-10  -1   8  17  26  35]
```

**How it works:** `10-20=-10`, `20-21=-1`, `30-22=8`, `40-23=17`, `50-24=26`, `60-25=35`.

Notice that negative results are perfectly fine — NumPy handles them automatically.

---

### 3.3 Multiplication — `np.multiply()`

The `multiply()` function multiplies corresponding elements.

```python
import numpy as np

arr1 = np.array([10, 20, 30, 40, 50, 60])
arr2 = np.array([20, 21, 22, 23, 24, 25])

newarr = np.multiply(arr1, arr2)

print(newarr)
```

**Output:**
```
[ 200  420  660  920 1200 1500]
```

**How it works:** `10×20=200`, `20×21=420`, `30×22=660`, and so on.

> **Real-world use:** In finance, you might multiply an array of quantities by an array of unit prices to get the total cost for each item in an order.

---

### 3.4 Division — `np.divide()`

The `divide()` function divides elements of the first array by corresponding elements of the second.

```python
import numpy as np

arr1 = np.array([10, 20, 30, 40, 50, 60])
arr2 = np.array([ 3,  5, 10,  8,  2, 33])

newarr = np.divide(arr1, arr2)

print(newarr)
```

**Output:**
```
[ 3.33333333  4.          3.          5.         25.          1.81818182]
```

**How it works:** `10÷3≈3.333`, `20÷5=4.0`, `30÷10=3.0`, `40÷8=5.0`, `50÷2=25.0`, `60÷33≈1.818`.

NumPy always returns decimal (float) results for division.

---

### 3.5 Power — `np.power()`

The `power()` function raises each element of the first array to the power of the corresponding element in the second array.

```python
import numpy as np

arr1 = np.array([10, 20, 30, 40, 50, 60])
arr2 = np.array([ 3,  5,  6,  8,  2, 33])

newarr = np.power(arr1, arr2)

print(newarr)
```

**Output:**
```
[      1000    3200000  729000000 6553600000000000        2500            0]
```

*(Note: 60^33 overflows a standard integer and wraps to 0 in some NumPy versions)*

**How it works:** `10³=1000`, `20⁵=3,200,000`, `30⁶=729,000,000`, etc.

> **Real-world use:** Used in exponential growth models — population growth, compound interest, signal processing, and scientific simulations.

---

### 3.6 Remainder / Modulo — `np.mod()` and `np.remainder()`

The **remainder** (also called **modulo**) is what is left over after integer division. For example, `10 ÷ 3 = 3 remainder 1` — so `10 % 3 = 1`.

Both `np.mod()` and `np.remainder()` do the same thing.

```python
import numpy as np

arr1 = np.array([10, 20, 30, 40, 50, 60])
arr2 = np.array([ 3,  7,  9,  8,  2, 33])

newarr = np.mod(arr1, arr2)

print(newarr)
```

**Output:**
```
[ 1  6  3  0  0 27]
```

**How it works:**
- `10 % 3 = 1` (10 = 3×3 + 1)
- `20 % 7 = 6` (20 = 7×2 + 6)
- `30 % 9 = 3` (30 = 9×3 + 3)
- `40 % 8 = 0` (40 = 8×5 + 0, divides evenly)
- `50 % 2 = 0` (50 is even)
- `60 % 33 = 27` (60 = 33×1 + 27)

Using `np.remainder()` gives exactly the same result:

```python
newarr = np.remainder(arr1, arr2)
print(newarr)
```

**Output:**
```
[ 1  6  3  0  0 27]
```

> **Real-world use:** Modulo is used in cryptography, scheduling (what day of the week will it be in 100 days?), and game programming (wrapping a position around a boundary).

---

### 3.7 Quotient and Mod Together — `np.divmod()`

The `divmod()` function returns **both** the integer quotient **and** the remainder in one call. It returns two arrays at once.

```python
import numpy as np

arr1 = np.array([10, 20, 30, 40, 50, 60])
arr2 = np.array([ 3,  7,  9,  8,  2, 33])

newarr = np.divmod(arr1, arr2)

print(newarr)
```

**Output:**
```
(array([ 3,  2,  3,  5, 25,  1]), array([ 1,  6,  3,  0,  0, 27]))
```

**Breaking it down:**
- The **first array** `[3, 2, 3, 5, 25, 1]` contains the **quotients** (how many times the divisor fits in whole)
- The **second array** `[1, 6, 3, 0, 0, 27]` contains the **remainders** (what is left over)

For `10 ÷ 3`: quotient is `3`, remainder is `1`.

---

### 3.8 Absolute Values — `np.absolute()`

The **absolute value** of a number is its distance from zero — it removes the negative sign.

- `absolute(-5) = 5`
- `absolute(5) = 5`

```python
import numpy as np

arr = np.array([-1, -2, 1, 2, 3, -4])

newarr = np.absolute(arr)

print(newarr)
```

**Output:**
```
[1 2 1 2 3 4]
```

> **Important note:** NumPy also has `np.abs()` which does the same thing. However, it is recommended to use `np.absolute()` to avoid confusion with Python's built-in `math.abs()`. Using the wrong one in certain contexts can cause unexpected results.

> **Real-world use:** In engineering and data science, absolute values are used to measure error — the difference between a predicted value and the actual value, regardless of direction.

---

## Part 4 — Rounding Decimals

When working with real-world data (prices, measurements, scientific readings), you often get messy decimal numbers like `3.1666667` or `-2.9999`. NumPy provides five different ways to clean up decimals.

### The five rounding methods at a glance

| Method | Function | What it does |
|--------|----------|--------------|
| Truncation | `np.trunc()` | Chops off the decimal, keeps integer part |
| Fix | `np.fix()` | Same as trunc — towards zero |
| Rounding | `np.around()` | Standard rounding (≥5 rounds up) |
| Floor | `np.floor()` | Always rounds **down** to nearest integer |
| Ceil | `np.ceil()` | Always rounds **up** to nearest integer |

---

### 4.1 Truncation — `np.trunc()` and `np.fix()`

**Truncation** simply removes the decimal part and returns the integer part — it always moves towards zero regardless of the decimal value.

```python
import numpy as np

arr = np.trunc([-3.1666, 3.6667])

print(arr)
```

**Output:**
```
[-3.  3.]
```

**Explanation:**
- `-3.1666` → remove `.1666` → result is `-3.0` (moved towards zero, not towards `-4`)
- `3.6667` → remove `.6667` → result is `3.0` (even though it's close to 4, truncation ignores that)

Using `np.fix()` gives the same result:

```python
import numpy as np

arr = np.fix([-3.1666, 3.6667])

print(arr)
```

**Output:**
```
[-3.  3.]
```

> **Common Beginner Mistake:** Beginners often confuse truncation with floor. They behave differently for **negative numbers**. Truncation of `-3.7` gives `-3` (towards zero), but floor of `-3.7` gives `-4` (always down). We will see this clearly in 4.4.

---

### 4.2 Standard Rounding — `np.around()`

The `around()` function applies the standard mathematical rounding rule: if the digit after the rounding position is **5 or more**, round up; if it is **less than 5**, round down.

```python
import numpy as np

arr = np.around(3.1666, 2)

print(arr)
```

**Output:**
```
3.17
```

**Explanation:** We are rounding to 2 decimal places. The third decimal is `6`, which is ≥5, so the second decimal rounds up from `6` to `7`. Final result: `3.17`.

More examples:

```python
import numpy as np

print(np.around(3.1444, 2))   # third decimal is 4, so round down
print(np.around(3.1500, 2))   # third decimal is 5, so round up
print(np.around(7.55, 1))     # second decimal is 5, so round up
print(np.around(100.456, 0))  # round to whole number
```

**Output:**
```
3.14
3.15
7.6
100.0
```

The second argument to `np.around()` is the **number of decimal places** to keep.

> **Real-world use:** Used any time you display prices, grades, or measurements that need a fixed number of decimal places.

---

### 4.3 Floor — `np.floor()`

The **floor** of a number is the **largest integer that is less than or equal to it**. In simple terms: always round down to the next lower whole number.

```python
import numpy as np

arr = np.floor([-3.1666, 3.6667])

print(arr)
```

**Output:**
```
[-4.  3.]
```

**Explanation:**
- `floor(-3.1666)` = `-4` — the next integer going **downward** from `-3.1666` is `-4`
- `floor(3.6667)` = `3` — the next integer going **downward** from `3.6667` is `3`

Think of a number line:
```
... -4  -3.1666  -3  ...  3  3.6667  4 ...
floor(-3.1666) = -4            floor(3.6667) = 3
```

> **Analogy:** Floor is like an elevator that always takes you to the floor **below** where you are, not the floor above.

---

### 4.4 Ceil — `np.ceil()`

The **ceil** (ceiling) of a number is the **smallest integer that is greater than or equal to it**. In simple terms: always round up to the next higher whole number.

```python
import numpy as np

arr = np.ceil([-3.1666, 3.6667])

print(arr)
```

**Output:**
```
[-3.  4.]
```

**Explanation:**
- `ceil(-3.1666)` = `-3` — the next integer going **upward** from `-3.1666` is `-3`
- `ceil(3.6667)` = `4` — the next integer going **upward** from `3.6667` is `4`

> **Analogy:** Ceil is like an elevator that always takes you to the floor **above** where you are.

### Quick comparison of all four rounding behaviours

```python
import numpy as np

value = 3.4
print("trunc:", np.trunc(value))    # → 3.0
print("around:", np.around(value))  # → 3.0
print("floor:", np.floor(value))    # → 3.0
print("ceil:", np.ceil(value))      # → 4.0

value = 3.6
print("trunc:", np.trunc(value))    # → 3.0
print("around:", np.around(value))  # → 4.0
print("floor:", np.floor(value))    # → 3.0
print("ceil:", np.ceil(value))      # → 4.0

value = -3.4
print("trunc:", np.trunc(value))    # → -3.0  (towards zero)
print("floor:", np.floor(value))    # → -4.0  (always down)
print("ceil:", np.ceil(value))      # → -3.0  (always up)
```

**Output:**
```
trunc: 3.0
around: 3.0
floor: 3.0
ceil: 4.0
trunc: 3.0
around: 4.0
floor: 3.0
ceil: 4.0
trunc: -3.0
floor: -4.0
ceil: -3.0
```

---

## Part 5 — Logarithms with NumPy ufuncs

### What is a logarithm?

A **logarithm** answers this question: "How many times do I multiply this base number by itself to get the result?"

For example:
- `log₂(8) = 3` because `2 × 2 × 2 = 8`
- `log₁₀(1000) = 3` because `10 × 10 × 10 = 1000`
- `logₑ(e) = 1` because `e¹ = e`

Logarithms are the **inverse of exponentiation**. If `2³ = 8`, then `log₂(8) = 3`.

> **Real-world use:** Logarithms appear everywhere — measuring earthquake magnitude (Richter scale), sound intensity (decibels), pH in chemistry, information theory, machine learning (log loss), and financial models (log returns).

NumPy provides functions to compute logs at base 2, base 10, and base e. It also lets you compute logs at **any** custom base using `frompyfunc()`.

> **Important note:** If NumPy cannot compute a log (e.g., log of zero or a negative number), it places `-inf` or `inf` in that position instead of crashing.

---

### 5.1 Log base 2 — `np.log2()`

```python
import numpy as np

arr = np.arange(1, 10)
# arange(1, 10) creates [1, 2, 3, 4, 5, 6, 7, 8, 9]

print(np.log2(arr))
```

**Output:**
```
[0.         1.         1.58496250 2.         2.32192809 2.58496250
 2.80735492 3.         3.16992500]
```

**Explanation:**
- `log₂(1) = 0` because `2⁰ = 1`
- `log₂(2) = 1` because `2¹ = 2`
- `log₂(4) = 2` because `2² = 4`
- `log₂(8) = 3` because `2³ = 8`
- Non-powers-of-2 like `3` give decimals: `log₂(3) ≈ 1.585`

> **About `np.arange(1, 10)`:** This creates a NumPy array of integers from 1 to 9 (the end value 10 is excluded). It is like Python's `range()` but returns a NumPy array.

> **Real-world use:** Log base 2 is used heavily in computer science — measuring bits of information, binary tree depth, and algorithm complexity analysis.

---

### 5.2 Log base 10 — `np.log10()`

```python
import numpy as np

arr = np.arange(1, 10)

print(np.log10(arr))
```

**Output:**
```
[0.         0.30103000 0.47712125 0.60205999 0.69897000 0.77815125
 0.84509804 0.90308999 0.95424251]
```

**Explanation:**
- `log₁₀(1) = 0` because `10⁰ = 1`
- `log₁₀(10) = 1` because `10¹ = 10` (not in this range but the pattern holds)
- `log₁₀(100) = 2` because `10² = 100`

> **Real-world use:** The Richter scale for earthquakes uses log base 10. An earthquake of magnitude 6 is 10× stronger than magnitude 5.

---

### 5.3 Natural log (base e) — `np.log()`

The **natural logarithm** uses base **e**, where `e ≈ 2.71828`. It is written as `ln` in mathematics but as `np.log()` in NumPy.

```python
import numpy as np

arr = np.arange(1, 10)

print(np.log(arr))
```

**Output:**
```
[0.         0.69314718 1.09861229 1.38629436 1.60943791 1.79175947
 1.94591015 2.07944154 2.19722458]
```

**Explanation:**
- `ln(1) = 0` because `e⁰ = 1`
- `ln(e) = 1` (approximately `ln(2.718) ≈ 1`)
- `ln(2) ≈ 0.693`
- `ln(8) ≈ 2.079`

> **Real-world use:** Natural logs are fundamental in calculus, continuous compound interest formulas, population growth models, and neural network training.

---

### 5.4 Log at any custom base

NumPy does not have a built-in function for arbitrary bases, but you can create one using `frompyfunc()` with Python's built-in `math.log()`.

`math.log(value, base)` calculates the log of `value` at the given `base`.

```python
from math import log
import numpy as np

# Create a custom ufunc for log at any base
nplog = np.frompyfunc(log, 2, 1)
# 2 inputs: the value and the base
# 1 output: the log result

result = nplog(100, 15)
print(result)
```

**Output:**
```
1.6728419785793796
```

**Explanation:** `log₁₅(100) ≈ 1.673` means `15^1.673 ≈ 100`. We are asking: "To what power must 15 be raised to get 100?"

You can now apply this to an entire array:

```python
from math import log
import numpy as np

nplog = np.frompyfunc(log, 2, 1)

values = np.array([10, 100, 1000])
result = nplog(values, 10)  # log base 10 of each value
print(result)
```

**Output:**
```
[1.0 2.0 3.0]
```

This confirms: `log₁₀(10)=1`, `log₁₀(100)=2`, `log₁₀(1000)=3`.

---

## Part 6 — Summations

### Addition vs Summation — what is the difference?

These two concepts sound similar but are different in NumPy:

- **Addition** (`np.add`) operates between **two arrays**, element by element — pairing up positions and adding each pair
- **Summation** (`np.sum`) adds up elements **across** one or more arrays — collapsing them into a single number (or fewer numbers)

### 6.1 Addition (review)

```python
import numpy as np

arr1 = np.array([1, 2, 3])
arr2 = np.array([1, 2, 3])

newarr = np.add(arr1, arr2)
print(newarr)
```

**Output:**
```
[2 4 6]
```

Result is still an array of the same length: `1+1=2`, `2+2=4`, `3+3=6`.

---

### 6.2 Summation — `np.sum()`

`np.sum()` adds up all elements across all arrays passed to it, returning a **single number**.

```python
import numpy as np

arr1 = np.array([1, 2, 3])
arr2 = np.array([1, 2, 3])

newarr = np.sum([arr1, arr2])
print(newarr)
```

**Output:**
```
12
```

**Explanation:** All elements combined: `1 + 2 + 3 + 1 + 2 + 3 = 12`. Everything is added up into one total.

---

### 6.3 Summation over an axis — `axis=1`

Sometimes you don't want the total of everything — you want the total **per array**. You can control this with the `axis` parameter.

- `axis=0` — sum **across** arrays (add corresponding positions)
- `axis=1` — sum **within** each array (total of each individual array)

```python
import numpy as np

arr1 = np.array([1, 2, 3])
arr2 = np.array([1, 2, 3])

newarr = np.sum([arr1, arr2], axis=1)
print(newarr)
```

**Output:**
```
[6 6]
```

**Explanation:**
- Sum of `arr1` alone: `1 + 2 + 3 = 6`
- Sum of `arr2` alone: `1 + 2 + 3 = 6`
- Result: `[6, 6]` — one total per array

> **Analogy:** Imagine two students each took a 3-question test. `axis=1` gives the total score per student. `axis=0` without axis gives the grand total of all marks.

Let's try a more illustrative example:

```python
import numpy as np

store_a_sales = np.array([100, 200, 150])   # sales on 3 days
store_b_sales = np.array([80, 170, 210])    # sales on 3 days

# Total sales per store
per_store = np.sum([store_a_sales, store_b_sales], axis=1)
print("Per store totals:", per_store)

# Grand total of all sales
grand_total = np.sum([store_a_sales, store_b_sales])
print("Grand total:", grand_total)
```

**Output:**
```
Per store totals: [450 460]
Grand total: 910
```

---

### 6.4 Cumulative Sum — `np.cumsum()`

A **cumulative sum** (also called a **running total** or **partial sum**) means you keep a rolling total as you go through the array — each position shows the sum of all elements up to and including that position.

**Example:** For the array `[1, 2, 3, 4]`, the cumulative sum is:
- Position 0: `1` (just the first element)
- Position 1: `1 + 2 = 3`
- Position 2: `1 + 2 + 3 = 6`
- Position 3: `1 + 2 + 3 + 4 = 10`

Result: `[1, 3, 6, 10]`

```python
import numpy as np

arr = np.array([1, 2, 3])

newarr = np.cumsum(arr)
print(newarr)
```

**Output:**
```
[1 3 6]
```

**Explanation:**
- `[1]` → `1`
- `[1, 2]` → `1+2=3`
- `[1, 2, 3]` → `1+2+3=6`

> **Real-world use:** Cumulative sums are used in sales tracking (running total of revenue over a month), sports statistics (cumulative points scored), finance (running portfolio value), and science (accumulated rainfall).

---

## Guided Practice Exercises

### Exercise 1 — Custom ufunc for Doubling

**Objective:** Create a custom ufunc that doubles any number.

**Scenario:** You have a list of item prices and need to find double each price for a "buy 2 get 1 free" display.

**Steps:**
1. Define a regular Python function `double(x)` that returns `x * 2`
2. Convert it to a ufunc using `np.frompyfunc()`
3. Apply it to a prices array

**Starting code:**
```python
import numpy as np

prices = np.array([5.99, 12.50, 3.25, 8.75])

# Your code here
```

**Hints:** The function takes 1 input and returns 1 output.

**Expected output:**
```
[11.98 25.0  6.5  17.5 ]
```

**Self-check questions:**
- How many inputs and outputs did you specify in `frompyfunc()`?
- What type does `type(double)` show after conversion?

---

### Exercise 2 — Arithmetic on Student Data

**Objective:** Practice `np.add`, `np.subtract`, and `np.absolute` with realistic data.

**Scenario:** You have the exam scores of 5 students in two subjects. You want to find the total, the difference, and the absolute difference (regardless of which is higher).

```python
import numpy as np

maths   = np.array([78, 85, 92, 60, 74])
english = np.array([82, 79, 88, 71, 80])

# Task 1: Find total score per student (maths + english)
total = np.add(maths, english)
print("Total scores:", total)

# Task 2: Find the difference (maths - english)
diff = np.subtract(maths, english)
print("Differences:", diff)

# Task 3: Find absolute difference (remove negative signs)
abs_diff = np.absolute(diff)
print("Absolute differences:", abs_diff)
```

**Expected output:**
```
Total scores: [160 164 180 131 154]
Differences: [ -4   6   4 -11  -6]
Absolute differences: [ 4  6  4 11  6]
```

**What-if challenge:** What if you used `np.multiply(maths, english)`? What does that represent?

---

### Exercise 3 — Rounding a Financial Dataset

**Objective:** Practice all five rounding methods on real-looking currency values.

**Scenario:** A store calculates prices after tax and gets messy decimals. You need to round them different ways for different reports.

```python
import numpy as np

prices_after_tax = np.array([12.3499, 7.5001, 99.9999, 5.5000, 3.1111])

print("Original:   ", prices_after_tax)
print("Truncated:  ", np.trunc(prices_after_tax))
print("Around 2dp: ", np.around(prices_after_tax, 2))
print("Floor:      ", np.floor(prices_after_tax))
print("Ceil:       ", np.ceil(prices_after_tax))
```

**Expected output:**
```
Original:    [12.3499  7.5001 99.9999  5.5      3.1111]
Truncated:   [12.  7. 99.  5.  3.]
Around 2dp:  [12.35  7.5  100.    5.5    3.11]
Floor:       [12.  7. 99.  5.  3.]
Ceil:        [13.  8. 100.   6.  4.]
```

**Self-check:** Why does `floor(99.9999)` give `99.0` but `around(99.9999, 2)` gives `100.0`?

---

### Exercise 4 — Summation of Daily Sales

**Objective:** Use `np.sum()`, axis-based summation, and `np.cumsum()`.

**Scenario:** Three shops recorded their daily sales over 4 days. Find totals and running totals.

```python
import numpy as np

shop1 = np.array([200, 350, 180, 420])
shop2 = np.array([310, 290, 400, 250])
shop3 = np.array([150, 460, 220, 380])

# Task 1: Total sales per shop (axis=1)
per_shop = np.sum([shop1, shop2, shop3], axis=1)
print("Total per shop:", per_shop)

# Task 2: Grand total across all shops and days
grand = np.sum([shop1, shop2, shop3])
print("Grand total:", grand)

# Task 3: Running total for shop1
running = np.cumsum(shop1)
print("Shop1 running total:", running)
```

**Expected output:**
```
Total per shop: [1150 1250 1210]
Grand total: 3610
Shop1 running total: [ 200  550  730 1150]
```

---

## Mini Project — Student Performance Analyser

In this project, you will build a complete student grade analysis tool using all the concepts covered in this lesson.

### Scenario

You are a school data analyst. You have the scores of 5 students across 3 subjects: Maths, Science, and English. Your job is to:
1. Calculate total scores using arithmetic ufuncs
2. Round averages cleanly
3. Compute log-scaled scores for a special grade report
4. Show cumulative totals to track how marks accumulate across subjects

---

### Stage 1 — Setup

```python
import numpy as np
from math import log

# Student scores (5 students × 3 subjects)
maths   = np.array([78, 85, 92, 60, 74])
science = np.array([82, 79, 88, 71, 80])
english = np.array([70, 90, 85, 65, 77])
```

---

### Stage 2 — Total Scores Using Arithmetic ufuncs

```python
# Add maths and science
ms_total = np.add(maths, science)
print("Maths + Science:", ms_total)

# Add english to get grand total per student
grand_total = np.add(ms_total, english)
print("Grand totals:   ", grand_total)
```

**Milestone Output:**
```
Maths + Science: [160 164 180 131 154]
Grand totals:    [230 254 265 196 231]
```

---

### Stage 3 — Averages and Rounding

```python
# Divide grand total by 3 to get average
averages = np.divide(grand_total, 3)
print("Raw averages:   ", averages)

# Round to 1 decimal place using around()
rounded_avg = np.around(averages, 1)
print("Rounded averages:", rounded_avg)

# Floor and ceil for grade boundaries
floor_avg = np.floor(averages)
ceil_avg  = np.ceil(averages)
print("Floor averages: ", floor_avg)
print("Ceil averages:  ", ceil_avg)
```

**Milestone Output:**
```
Raw averages:    [76.66666667 84.66666667 88.33333333 65.33333333 77.        ]
Rounded averages: [76.7 84.7 88.3 65.3 77. ]
Floor averages:  [76. 84. 88. 65. 77.]
Ceil averages:   [77. 85. 89. 66. 77.]
```

---

### Stage 4 — Log-scaled Score Report

In some academic analytics tools, scores are log-transformed to better understand the spread between high and low performers.

```python
# Natural log of rounded averages
print("Natural log of averages:", np.log(rounded_avg))

# Log base 10
print("Log10 of averages:      ", np.around(np.log10(rounded_avg), 4))

# Custom ufunc: log base 5 of averages
nplog = np.frompyfunc(log, 2, 1)
log5 = nplog(rounded_avg, 5)
print("Log base 5 of averages: ", log5)
```

**Milestone Output:**
```
Natural log of averages: [4.33972... 4.43956... 4.48084... 4.17869... 4.34381...]
Log10 of averages:       [1.8848 1.928  1.946  1.8149 1.8865]
Log base 5 of averages:  [2.689... 2.754... 2.778... 2.592... 2.692...]
```

---

### Stage 5 — Cumulative Totals

```python
# Cumulative sum shows how totals build up subject by subject
# Arrange subjects as rows, then check cumsum per student

all_scores = np.array([maths, science, english])

# Sum per subject (all students combined per subject)
per_subject = np.sum(all_scores, axis=1)
print("Total per subject:", per_subject)

# Running total across subjects
running_subject_total = np.cumsum(per_subject)
print("Running subject total:", running_subject_total)
```

**Milestone Output:**
```
Total per subject: [389 400 387]
Running subject total: [ 389  789 1176]
```

---

### Stage 6 — Final Reflection

- Which student had the highest total score?
- How did the cumulative subject totals help you understand which subject contributed the most overall marks?
- What does the log-transformed score tell you that the raw average doesn't?

**Optional enhancement:** Add a `np.power()` step to compute a "bonus multiplier" for students who scored above 85 average.

---

## Common Beginner Mistakes

**Mistake 1 — Wrong number of inputs in `frompyfunc()`**

```python
# WRONG: function takes 2 args but frompyfunc says 1 input
def myadd(x, y):
    return x + y

myadd = np.frompyfunc(myadd, 1, 1)  # ← Error! Should be 2, not 1
```

**Fix:** Count the arguments in your function and match that number.

```python
myadd = np.frompyfunc(myadd, 2, 1)  # ← Correct
```

---

**Mistake 2 — Confusing `floor` and `trunc` for negative numbers**

```python
import numpy as np

print(np.floor(-2.3))   # -3.0  ← goes DOWN (further from zero)
print(np.trunc(-2.3))   # -2.0  ← goes TOWARDS ZERO
```

Remember: floor always goes down the number line; trunc always moves towards zero.

---

**Mistake 3 — Expecting `np.sum` to behave like `np.add`**

```python
import numpy as np

a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

print(np.add(a, b))       # [5 7 9]  — element-wise addition
print(np.sum([a, b]))     # 21       — total of everything
```

Use `np.add()` when you want a result array; use `np.sum()` when you want a total.

---

**Mistake 4 — Calling log on zero**

```python
import numpy as np

print(np.log(0))   # -inf   (not an error, but -infinity)
print(np.log(-1))  # nan    (not a number — can't take log of negative)
```

Always filter out zeros and negatives from your data before applying log functions.

---

**Mistake 5 — Using `np.abs()` instead of `np.absolute()`**

Both work in most cases, but `np.absolute()` is the preferred NumPy way to avoid potential naming conflicts with Python's `abs()` in complex code.

---

## Reflection Questions

1. What is the key difference between a regular Python function and a NumPy ufunc?
2. How does `frompyfunc()` transform an ordinary function into a ufunc?
3. When would you use `np.mod()` instead of `np.divide()`?
4. What is the difference between `floor`, `ceil`, and `trunc` for the number `-4.5`?
5. If you had a list of earthquake magnitudes and wanted to understand relative strength, which log function would you use and why?
6. What is the difference between `np.add(arr1, arr2)` and `np.sum([arr1, arr2])`?
7. In what real-world scenario would a cumulative sum be the right tool to use?
8. Why does NumPy place `-inf` instead of raising an error when computing `log(0)`?

---

## Completion Checklist

- [ ] I understand what a ufunc is and why it is useful
- [ ] I can create a custom ufunc using `np.frompyfunc()`
- [ ] I can check whether a function is a ufunc using `type()`
- [ ] I can use `np.add`, `np.subtract`, `np.multiply`, `np.divide`
- [ ] I can use `np.power`, `np.mod`, `np.remainder`, `np.divmod`
- [ ] I can use `np.absolute` to remove negative signs
- [ ] I understand the five rounding methods: trunc, fix, around, floor, ceil
- [ ] I can use `np.log2`, `np.log10`, and `np.log` (natural log)
- [ ] I can create a custom log ufunc for any base
- [ ] I understand the difference between `np.add` and `np.sum`
- [ ] I can use `axis=1` to sum within individual arrays
- [ ] I can compute cumulative sums with `np.cumsum`
- [ ] I completed the mini-project

---

## Lesson Summary

In this lesson you explored the full world of NumPy **ufuncs** — from creating your own to using powerful built-in mathematical functions.

**Creating ufuncs:** Use `np.frompyfunc(function, num_inputs, num_outputs)` to convert any regular Python function into a ufunc that can operate on entire arrays at once. Verify with `type(func) == np.ufunc`.

**Arithmetic ufuncs:** NumPy provides `np.add`, `np.subtract`, `np.multiply`, `np.divide`, `np.power`, `np.mod` / `np.remainder`, `np.divmod`, and `np.absolute` — all of which work element-by-element across arrays and support conditional operation via the `where` parameter.

**Rounding decimals:** Five methods give you precise control — `np.trunc()` / `np.fix()` chop towards zero, `np.around()` applies standard rounding rules, `np.floor()` always goes down, and `np.ceil()` always goes up.

**Logarithms:** Use `np.log2()`, `np.log10()`, and `np.log()` (base e) for the most common cases. For any custom base, combine `frompyfunc()` with Python's `math.log()` to build your own log ufunc.

**Summations:** Understand the critical difference — `np.add()` pairs elements from two arrays; `np.sum()` collapses everything into a total. Use `axis=1` to get per-array totals. Use `np.cumsum()` for running totals that grow element by element.

These tools are the foundation for data analysis, scientific computing, financial modelling, machine learning preprocessing, and engineering simulations. Mastering them gives you the ability to work with large datasets quickly, accurately, and expressively.
