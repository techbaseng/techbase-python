---
render_with_liquid: false
title: "NumPy Deep Dive: Data Types, Copy vs View, Shape, Reshape, Iterating, and Joining Arrays"
nav_order: 25
---

# Lesson 25 — NumPy Deep Dive: Data Types, Copy vs View, Shape, Reshape, Iterating, and Joining Arrays

---

## Lesson Introduction

Welcome to Lesson 25! By now you know how to create NumPy arrays and access elements inside them. In this lesson, we go deeper. We will learn:

- What **data types** are and how NumPy manages them
- The difference between **copying** and **viewing** an array (a concept that surprises even experienced programmers)
- How to understand and inspect the **shape** of an array
- How to **reshape** arrays from one structure into another
- How to **iterate** (loop) through arrays of any number of dimensions
- How to **join** multiple arrays together into one

Each concept builds on the last. By the end, you will be able to manipulate arrays like a data science professional.

> **Real-world relevance:** In machine learning, you constantly reshape arrays to feed them into models. In data analysis, you join datasets together. In scientific computing, you iterate through large arrays to process measurements. Everything in this lesson is used daily by professional data scientists and engineers.

---

## Prerequisites — What You Need to Know First

Before we begin, let us quickly review some ideas we depend on:

**What is a NumPy array?**
A NumPy array is an ordered list of values stored in a grid. Every element in the array must be of the same type (like all integers, or all floats). This is different from a Python list, where you can mix types.

**What is a dimension?**
A dimension (also called an axis) is a direction in which data is arranged.
- A flat list like `[1, 2, 3]` is 1-dimensional (1D).
- A table like `[[1,2],[3,4]]` is 2-dimensional (2D) — it has rows and columns.
- A cube like `[[[1,2],[3,4]],[[5,6],[7,8]]]` is 3-dimensional (3D).

**What is a data type?**
A data type defines the kind of value being stored — for example, a whole number (integer), a decimal number (float), or text (string).

---

## Part 1 — NumPy Data Types

### 1.1 What Is a Data Type, and Why Does It Matter?

Imagine you are filling out a form. Some fields only accept whole numbers (your age), some accept text (your name), and some accept decimals (your weight). A data type is exactly that — a rule about what kind of value a slot can hold.

In Python, you have basic built-in types like `int`, `float`, `str`, and `bool`. NumPy adds its own more precise types, because when you are working with millions of numbers, using the right type saves memory and makes calculations faster.

Think of it this way: storing the number 5 as a 64-bit integer uses 8 bytes of memory. If you have one billion numbers and use the wrong type, you could waste gigabytes of RAM unnecessarily.

### 1.2 Python's Built-in Data Types (Quick Review)

| Type | What it holds | Example |
|------|--------------|---------|
| `str` | Text | `"Hello"` |
| `int` | Whole numbers | `-3, 0, 42` |
| `float` | Decimal numbers | `3.14, -0.5` |
| `bool` | True or False | `True, False` |
| `complex` | Complex numbers | `1.0 + 2.0j` |

### 1.3 NumPy's Data Type System

NumPy uses short one-character codes to refer to types. Here is the full list:

| Code | Full Name | What it Means |
|------|-----------|---------------|
| `i` | integer | Whole numbers (positive and negative) |
| `b` | boolean | True or False |
| `u` | unsigned integer | Whole numbers (positive only, no negatives) |
| `f` | float | Numbers with decimals |
| `c` | complex float | Complex numbers with real and imaginary parts |
| `m` | timedelta | A difference between two times |
| `M` | datetime | A specific date and time |
| `O` | object | Any Python object |
| `S` | string (bytes) | Fixed-length byte strings |
| `U` | unicode string | Text (Unicode characters) |
| `V` | void | Fixed chunk of memory for other types |

> **Key insight:** NumPy stores data much more efficiently than Python lists because every element in a NumPy array has the exact same type. A list can hold a mix; a NumPy array cannot.

### 1.4 Checking the Data Type of an Array

Every NumPy array has a property called `.dtype` that tells you the type of its elements.

**What does `.dtype` mean?** It stands for "data type." It is like asking: "What kind of values are stored inside this array?"

**Example 1 — Integer array:**

```python
import numpy as np

arr = np.array([1, 2, 3, 4])

print(arr.dtype)
```

**Expected Output:**
```
int64
```

**Line-by-line explanation:**
- `import numpy as np` — brings in the NumPy library and gives it the short name `np`
- `arr = np.array([1, 2, 3, 4])` — creates a NumPy array from a Python list of whole numbers
- `print(arr.dtype)` — prints the data type. `int64` means a 64-bit integer (a whole number using 64 bits of memory)

**Example 2 — String array:**

```python
import numpy as np

arr = np.array(['apple', 'banana', 'cherry'])

print(arr.dtype)
```

**Expected Output:**
```
<U6
```

**Explanation of `<U6`:**
- `U` means Unicode string
- `6` means the longest string in the array has 6 characters ("banana" and "cherry" both have 6)
- `<` means little-endian byte order (a low-level storage detail you can ignore for now)

> **Thinking prompt:** What do you think would happen if you added a longer string like `"watermelon"` to this array? How would the dtype change?

### 1.5 Creating an Array With a Specific Data Type

You can tell NumPy exactly what data type to use when creating an array. You do this with the `dtype` parameter inside `np.array()`.

**What is a parameter?** A parameter is an optional instruction you give to a function to customize how it works.

**Example — Create a string array from numbers:**

```python
import numpy as np

arr = np.array([1, 2, 3, 4], dtype='S')

print(arr)
print(arr.dtype)
```

**Expected Output:**
```
[b'1' b'2' b'3' b'4']
|S1
```

**Explanation:**
- `dtype='S'` — tells NumPy to store these values as byte strings
- The `b` prefix in `b'1'` means "bytes literal" — it is a string stored as raw bytes
- `|S1` means each element takes up 1 byte (since `'1'`, `'2'`, etc. are each 1 character)

**Example — Create a 4-byte integer array:**

```python
import numpy as np

arr = np.array([1, 2, 3, 4], dtype='i4')

print(arr)
print(arr.dtype)
```

**Expected Output:**
```
[1 2 3 4]
int32
```

**Explanation of `'i4'`:**
- `i` = integer
- `4` = 4 bytes (32 bits)
- So `i4` creates 32-bit integers, also known as `int32`

> For `i`, `u`, `f`, `S`, and `U`, you can specify a byte size like `i4`, `f8`, `S10`, etc.

### 1.6 What Happens When Conversion Fails?

If you try to force NumPy to convert values that cannot be converted, it raises a `ValueError`.

**What is a ValueError?** It is Python's way of saying: "The type of value you gave me makes no sense for this operation."

**Example — Trying to convert non-numeric text to integer:**

```python
import numpy as np

arr = np.array(['a', '2', '3'], dtype='i')
```

**Expected Output (Error):**
```
ValueError: invalid literal for int() with base 10: 'a'
```

**Why?** The letter `'a'` cannot be converted to a number. `'2'` and `'3'` could be, but `'a'` cannot — so the whole operation fails.

> **Beginner mistake warning:** You might think `'2'` will become `2` and `'a'` will just become `0`. It will NOT. NumPy fails completely if even one element cannot be converted.

### 1.7 Converting an Array to a Different Data Type (astype)

What if you already have an array and want to change its type? You cannot change it in-place (directly). Instead, you create a **copy** of the array with the new type using the `.astype()` method.

**What does "in-place" mean?** It means changing the actual original thing, rather than making a new version. NumPy requires you to make a new array when changing types.

**Example 1 — Convert float to integer using `'i'`:**

```python
import numpy as np

arr = np.array([1.1, 2.1, 3.1])

newarr = arr.astype('i')

print(newarr)
print(newarr.dtype)
```

**Expected Output:**
```
[1 2 3]
int32
```

**Explanation:**
- `arr = np.array([1.1, 2.1, 3.1])` — creates a float array
- `newarr = arr.astype('i')` — creates a NEW array where each value is converted to integer. The decimal part is simply cut off (truncated), not rounded
- `1.1` becomes `1`, `2.1` becomes `2`, `3.1` becomes `3`

> **Thinking prompt:** What do you think `3.9` would become? Try it! (Answer: `3` — it is truncated, not rounded)

**Example 2 — Convert float to integer using Python's built-in `int`:**

```python
import numpy as np

arr = np.array([1.1, 2.1, 3.1])

newarr = arr.astype(int)

print(newarr)
print(newarr.dtype)
```

**Expected Output:**
```
[1 2 3]
int64
```

Both `'i'` and `int` work, but they may produce slightly different integer sizes.

**Example 3 — Convert integer to boolean:**

```python
import numpy as np

arr = np.array([1, 0, 3])

newarr = arr.astype(bool)

print(newarr)
print(newarr.dtype)
```

**Expected Output:**
```
[ True False  True]
bool
```

**Explanation:** In Python (and NumPy), any non-zero number converts to `True`, and `0` converts to `False`. This is called "truthiness."

- `1` → `True`
- `0` → `False`
- `3` → `True`

> **Real-world use:** Converting to boolean is very common in data analysis. For example, you might have a column of scores and want to mark which ones are passing (non-zero = True) vs failing (zero = False).

---

## Part 2 — Copy vs View

### 2.1 The Big Idea: What Are We Really Talking About?

This is one of the most important — and most misunderstood — concepts in NumPy. Let us start with a real-world analogy.

**Analogy — The Whiteboard and the Photo:**

Imagine a whiteboard in your classroom with some numbers written on it. Now consider two different actions:

1. **Taking a photo of the whiteboard** — The photo shows the numbers, but if someone erases the whiteboard and writes new numbers, your photo still shows the old numbers. They are separate.

2. **Looking at the whiteboard through a window** — You can see the current numbers. If someone erases them and writes new ones, you immediately see the new numbers through the window.

In NumPy:
- **Copy** = the photo (completely independent)
- **View** = the window (connected to the original)

### 2.2 What Is a Copy?

A **copy** is a brand-new, completely separate array. It takes the values from the original and stores them in a new location in memory. Changes to the copy do not affect the original. Changes to the original do not affect the copy.

**Example — Make a copy, change the original:**

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5])
x = arr.copy()
arr[0] = 42

print(arr)
print(x)
```

**Expected Output:**
```
[42  2  3  4  5]
[1 2 3 4 5]
```

**Line-by-line explanation:**
- `arr = np.array([1, 2, 3, 4, 5])` — creates the original array
- `x = arr.copy()` — creates a brand-new separate array `x` with the same values
- `arr[0] = 42` — changes the first element of `arr` to 42
- `print(arr)` — shows `[42 2 3 4 5]` (the original changed)
- `print(x)` — shows `[1 2 3 4 5]` (the copy is unchanged — they are independent)

> The copy **SHOULD NOT** be affected by changes to the original.

### 2.3 What Is a View?

A **view** is like a window into the same data. It does not create a new copy of the data. Both the view and the original point to the same memory. If you change one, the other changes too.

**Example 1 — Make a view, change the original:**

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5])
x = arr.view()
arr[0] = 42

print(arr)
print(x)
```

**Expected Output:**
```
[42  2  3  4  5]
[42  2  3  4  5]
```

**Explanation:** `arr[0]` was set to 42. Both `arr` and `x` show 42 because they share the same underlying data.

> The view **SHOULD** be affected by changes to the original.

**Example 2 — Make a view, change the VIEW:**

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5])
x = arr.view()
x[0] = 31

print(arr)
print(x)
```

**Expected Output:**
```
[31  2  3  4  5]
[31  2  3  4  5]
```

**Explanation:** This time we changed `x[0]` (the view). Because the view and the original share the same memory, the original `arr` also changed.

> **Common beginner mistake:** Many beginners accidentally modify data they wanted to keep. They create a view thinking it is a copy, then modify it, and are surprised when the original changes too. **Always use `.copy()` when you want an independent copy.**

### 2.4 How to Check: Does This Array Own Its Data?

NumPy gives every array a special attribute called `.base`. This attribute tells you whether the array owns its own data or is borrowing it from somewhere else.

- If `.base` returns `None` → the array **owns** its data (it is a copy or the original)
- If `.base` returns another array → the array is a **view** of that other array

**Example:**

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5])

x = arr.copy()
y = arr.view()

print(x.base)
print(y.base)
```

**Expected Output:**
```
None
[1 2 3 4 5]
```

**Explanation:**
- `x.base` is `None` — `x` is a copy; it owns its own data
- `y.base` is `[1 2 3 4 5]` — `y` is a view; it points back to `arr`

> **Quick mental test:** Before printing `.base`, ask yourself: "Is this a copy or a view?" Then check. This builds your intuition.

---

## Part 3 — Array Shape

### 3.1 What Is "Shape"?

The **shape** of an array describes how many elements it has in each dimension. It is like describing the dimensions of a box:

- A 1D array of 5 elements has shape `(5,)` — it is like a single row with 5 slots
- A 2D array with 2 rows and 4 columns has shape `(2, 4)` — like a table
- A 3D array with 2 groups, 3 rows, 4 columns has shape `(2, 3, 4)` — like a stack of tables

Think of shape as the answer to: "How is this data organized?"

### 3.2 Getting the Shape with `.shape`

Every NumPy array has a `.shape` attribute that returns a tuple describing its dimensions.

**What is a tuple?** A tuple is like a list, but it cannot be changed. It uses round brackets `()` instead of square brackets `[]`.

**Example 1 — Shape of a 2D array:**

```python
import numpy as np

arr = np.array([[1, 2, 3, 4], [5, 6, 7, 8]])

print(arr.shape)
```

**Expected Output:**
```
(2, 4)
```

**Explanation:**
- The outer list `[[...], [...]]` has 2 inner lists → 2 rows
- Each inner list has 4 elements → 4 columns
- Shape = `(2, 4)` = 2 rows, 4 columns

**How to read shape tuples:**
- First number = number of rows (or "how many groups at the outermost level")
- Second number = number of columns (or "how many elements in each group")
- Third number (if present) = elements in the next level deeper

**Example 2 — Creating an array with 5 dimensions:**

```python
import numpy as np

arr = np.array([1, 2, 3, 4], ndmin=5)

print(arr)
print('shape of array :', arr.shape)
```

**Expected Output:**
```
[[[[[1 2 3 4]]]]]
shape of array : (1, 1, 1, 1, 4)
```

**Explanation of `ndmin=5`:**
- `ndmin` = minimum number of dimensions
- We have 4 elements but we asked for 5 dimensions
- NumPy wraps them in enough brackets to reach 5 dimensions
- Shape `(1, 1, 1, 1, 4)` means: 1 group at levels 1–4, then 4 elements at the deepest level

**Understanding the shape tuple position by position:**
- Index 0 → outermost dimension has 1 element
- Index 1 → next dimension has 1 element
- Index 2 → next dimension has 1 element
- Index 3 → next dimension has 1 element
- Index 4 → innermost dimension has 4 elements

> **Thinking prompt:** If you have `arr.shape = (3, 4, 5)`, how many total elements does the array contain? (Answer: 3 × 4 × 5 = 60 elements)

---

## Part 4 — Array Reshape

### 4.1 What Does "Reshape" Mean?

Reshaping an array means **changing how the same data is organized** — rearranging the elements into a different dimensional structure — without changing the values themselves.

Think of it like rearranging 12 books:
- You can put them in one long row: 12 books in a line (1D, shape `(12,)`)
- Or 3 rows of 4 books (2D, shape `(3, 4)`)
- Or 2 shelves, each with 2 rows of 3 books (3D, shape `(2, 2, 3)`)

The books are the same — only the arrangement changes.

### 4.2 Reshape from 1D to 2D

**Example — Convert 12 elements into a 4×3 table:**

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12])

newarr = arr.reshape(4, 3)

print(newarr)
```

**Expected Output:**
```
[[ 1  2  3]
 [ 4  5  6]
 [ 7  8  9]
 [10 11 12]]
```

**Explanation:**
- Original: 12 elements in a flat line
- `reshape(4, 3)` = make 4 rows, 3 columns
- 4 × 3 = 12 ✓ (the total must match!)
- Elements fill in row by row: first row is `1, 2, 3`; second row is `4, 5, 6`; etc.

### 4.3 Reshape from 1D to 3D

**Example — Convert 12 elements into a 3D array:**

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12])

newarr = arr.reshape(2, 3, 2)

print(newarr)
```

**Expected Output:**
```
[[[ 1  2]
  [ 3  4]
  [ 5  6]]

 [[ 7  8]
  [ 9 10]
  [11 12]]]
```

**Explanation:**
- `reshape(2, 3, 2)` = 2 outer groups, each containing 3 rows, each row containing 2 elements
- 2 × 3 × 2 = 12 ✓
- Think of it as 2 small tables, each with 3 rows and 2 columns

### 4.4 The Golden Rule of Reshaping

**You can only reshape if the total number of elements stays the same.**

- 8 elements can become shape `(2, 4)`, `(4, 2)`, `(8, 1)`, `(1, 8)`, `(2, 2, 2)`
- 8 elements CANNOT become shape `(3, 3)` because 3×3=9 ≠ 8

**Example — Attempting an invalid reshape:**

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6, 7, 8])

newarr = arr.reshape(3, 3)

print(newarr)
```

**Expected Output (Error):**
```
ValueError: cannot reshape array of size 8 into shape (3,3)
```

> **Beginner mistake:** Always check that `rows × columns × depth... = total number of elements` before reshaping.

### 4.5 Does Reshape Return a Copy or a View?

**Example — Check what reshape returns:**

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6, 7, 8])

print(arr.reshape(2, 4).base)
```

**Expected Output:**
```
[1 2 3 4 5 6 7 8]
```

**Explanation:** The `.base` attribute returns the original array (not `None`), which means `reshape()` returns a **view**, not a copy. The reshaped array shares data with the original.

> **Important implication:** If you modify elements of a reshaped array, the original will also change, because they share the same memory.

### 4.6 The Unknown Dimension: Using -1

Sometimes you know one dimension but want NumPy to figure out the other. You can pass `-1` as a placeholder for one unknown dimension. NumPy will calculate the correct value automatically.

**Example — Let NumPy figure out one dimension:**

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6, 7, 8])

newarr = arr.reshape(2, 2, -1)

print(newarr)
```

**Expected Output:**
```
[[[1 2]
  [3 4]]

 [[5 6]
  [7 8]]]
```

**Explanation:**
- We told NumPy: "Make it 2 groups of 2 rows, and figure out the rest."
- Total = 8 elements. 2 × 2 × ? = 8. So ? = 2.
- NumPy calculates the `-1` dimension as 2.

> **Note:** You can only use `-1` for ONE dimension at a time. If you use it twice, NumPy cannot figure out two unknowns at once.

### 4.7 Flattening: Converting Any Array Back to 1D

Flattening means converting a multi-dimensional array into a simple 1D array. Use `reshape(-1)` to do this.

**Example — Flatten a 2D array:**

```python
import numpy as np

arr = np.array([[1, 2, 3], [4, 5, 6]])

newarr = arr.reshape(-1)

print(newarr)
```

**Expected Output:**
```
[1 2 3 4 5 6]
```

**Explanation:**
- `reshape(-1)` tells NumPy: "I want 1D, figure out the length."
- The 2D array `[[1,2,3],[4,5,6]]` becomes `[1, 2, 3, 4, 5, 6]`

> **Real-world use:** Flattening is extremely common in machine learning. Image data is often stored as 2D or 3D arrays, but many models require a flat 1D input vector.

> **Note:** Other functions like `flatten()` and `ravel()` also flatten arrays. `flatten()` always returns a copy. `ravel()` returns a view when possible. `reshape(-1)` is the most flexible approach.

---

## Part 5 — Array Iterating

### 5.1 What Does "Iterating" Mean?

Iterating means going through each element of a collection, one at a time, and doing something with each one — like checking each item in a shopping cart at checkout.

In NumPy, you can iterate through arrays using Python's `for` loop, just like with regular Python lists. The behaviour depends on how many dimensions the array has.

### 5.2 Iterating a 1D Array

With a 1D array, `for x in arr` gives you one element at a time.

**Example:**

```python
import numpy as np

arr = np.array([1, 2, 3])

for x in arr:
    print(x)
```

**Expected Output:**
```
1
2
3
```

**Explanation:**
- `for x in arr:` — loops over each element
- `x` takes the value of each element one at a time: first `1`, then `2`, then `3`
- `print(x)` — prints each value on its own line

### 5.3 Iterating a 2D Array

With a 2D array, `for x in arr` gives you **one row at a time** — not individual elements.

**Example 1 — Iterate rows:**

```python
import numpy as np

arr = np.array([[1, 2, 3], [4, 5, 6]])

for x in arr:
    print(x)
```

**Expected Output:**
```
[1 2 3]
[4 5 6]
```

**Explanation:** `x` is each row (sub-array), not each individual number.

**Example 2 — Iterate individual elements of a 2D array (nested loops):**

```python
import numpy as np

arr = np.array([[1, 2, 3], [4, 5, 6]])

for x in arr:
    for y in x:
        print(y)
```

**Expected Output:**
```
1
2
3
4
5
6
```

**Explanation:**
- The outer `for x in arr` loops over rows
- The inner `for y in x` loops over each element within each row
- Together they reach every individual number

### 5.4 Iterating a 3D Array

With a 3D array, the outermost `for` loop gives you 2D slices (layers), not rows or individual values.

**Example 1 — Iterate 2D layers:**

```python
import numpy as np

arr = np.array([[[1, 2, 3], [4, 5, 6]], [[7, 8, 9], [10, 11, 12]]])

for x in arr:
    print(x)
```

**Expected Output:**
```
[[1 2 3]
 [4 5 6]]
[[ 7  8  9]
 [10 11 12]]
```

**Example 2 — Iterate down to individual scalar values:**

```python
import numpy as np

arr = np.array([[[1, 2, 3], [4, 5, 6]], [[7, 8, 9], [10, 11, 12]]])

for x in arr:
    for y in x:
        for z in y:
            print(z)
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
```

**Explanation:** Three nested loops for a 3D array: one per dimension.

> **Pattern to remember:** For an N-dimensional array, you need N nested `for` loops to reach each individual scalar (single value). This gets impractical for very high dimensions — which is why `nditer()` exists.

### 5.5 Smart Iteration with nditer()

`nditer()` is a powerful NumPy function that lets you iterate over every scalar element of an array of ANY number of dimensions, using just a single loop. It removes the need for deeply nested `for` loops.

**Example — Iterate through a 3D array with just one loop:**

```python
import numpy as np

arr = np.array([[[1, 2], [3, 4]], [[5, 6], [7, 8]]])

for x in np.nditer(arr):
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
```

**Explanation:**
- `np.nditer(arr)` automatically handles all dimensions
- `x` is each individual scalar value, in order
- No nested loops needed!

### 5.6 Iterating with a Different Data Type Using nditer()

You can change the data type of elements during iteration using the `op_dtypes` argument. But since NumPy cannot change data in-place during iteration, it needs a temporary buffer. Enable the buffer using `flags=['buffered']`.

**What is a buffer?** Think of it as a temporary scratch pad. NumPy converts each element to the new type in this temporary space, then gives it to you.

**Example — Iterate and read values as strings:**

```python
import numpy as np

arr = np.array([1, 2, 3])

for x in np.nditer(arr, flags=['buffered'], op_dtypes=['S']):
    print(x)
```

**Expected Output:**
```
b'1'
b'2'
b'3'
```

**Explanation:**
- `op_dtypes=['S']` — convert each element to string (bytes) type
- `flags=['buffered']` — allow a buffer for temporary type conversion
- The `b` prefix shows these are byte strings

### 5.7 Iterating with a Step (Skipping Elements)

You can iterate with a step size (skip every other element) by using array slicing inside `nditer()`.

**Example — Skip every other element in a 2D array:**

```python
import numpy as np

arr = np.array([[1, 2, 3, 4], [5, 6, 7, 8]])

for x in np.nditer(arr[:, ::2]):
    print(x)
```

**Expected Output:**
```
1
3
5
7
```

**Explanation:**
- `arr[:, ::2]` — selects all rows (`:`), but only every 2nd column (`::2`)
- Columns selected: 0, 2 (indices 0 and 2 = values 1,3 in row 1 and 5,7 in row 2)
- `nditer()` then iterates over this filtered selection

### 5.8 Enumerated Iteration with ndenumerate()

Sometimes you need both the **index (position)** and the **value** of each element as you iterate. `ndenumerate()` provides both.

**What is enumeration?** It is the process of attaching a sequence number or position label to each item as you loop through them.

**Example 1 — Enumerate a 1D array:**

```python
import numpy as np

arr = np.array([1, 2, 3])

for idx, x in np.ndenumerate(arr):
    print(idx, x)
```

**Expected Output:**
```
(0,) 1
(1,) 2
(2,) 3
```

**Explanation:**
- `idx` is the index (position) as a tuple — `(0,)` means "position 0 in dimension 0"
- `x` is the value at that position

**Example 2 — Enumerate a 2D array:**

```python
import numpy as np

arr = np.array([[1, 2, 3, 4], [5, 6, 7, 8]])

for idx, x in np.ndenumerate(arr):
    print(idx, x)
```

**Expected Output:**
```
(0, 0) 1
(0, 1) 2
(0, 2) 3
(0, 3) 4
(1, 0) 5
(1, 1) 6
(1, 2) 7
(1, 3) 8
```

**Explanation:**
- `(0, 0)` means row 0, column 0 → value is 1
- `(0, 1)` means row 0, column 1 → value is 2
- `(1, 3)` means row 1, column 3 → value is 8

> **Real-world use:** `ndenumerate()` is very useful when you need to find the position of specific values in a 2D array, like finding the location of a maximum temperature in a weather grid.

---

## Part 6 — Joining Arrays

### 6.1 What Does "Joining" Mean?

Joining (also called concatenating or stacking) means combining two or more arrays into one single array. This is similar to merging spreadsheets or combining datasets.

In NumPy, you join arrays **along an axis**. Remember, an axis is just a direction:
- Axis 0 = along rows (top to bottom, stacking vertically)
- Axis 1 = along columns (left to right, combining side by side)

### 6.2 Joining with concatenate()

`np.concatenate()` is the main function for joining arrays. You pass it a tuple (or list) of arrays to combine, and optionally specify the axis.

**Important:** `np.concatenate()` requires all arrays to have the **same number of dimensions** and **matching sizes in all axes except the one being concatenated**.

**Example 1 — Join two 1D arrays:**

```python
import numpy as np

arr1 = np.array([1, 2, 3])

arr2 = np.array([4, 5, 6])

arr = np.concatenate((arr1, arr2))

print(arr)
```

**Expected Output:**
```
[1 2 3 4 5 6]
```

**Explanation:**
- `arr1` = `[1, 2, 3]` and `arr2` = `[4, 5, 6]`
- `np.concatenate((arr1, arr2))` — note the double parentheses: the outer ones are the function call, the inner ones are a tuple holding the two arrays
- Default axis is 0. For 1D arrays, this simply joins them end-to-end
- Result: `[1 2 3 4 5 6]`

**Example 2 — Join two 2D arrays along columns (axis=1):**

```python
import numpy as np

arr1 = np.array([[1, 2], [3, 4]])

arr2 = np.array([[5, 6], [7, 8]])

arr = np.concatenate((arr1, arr2), axis=1)

print(arr)
```

**Expected Output:**
```
[[1 2 5 6]
 [3 4 7 8]]
```

**Explanation:**
- `arr1` has shape `(2, 2)`: two rows, two columns
- `arr2` has shape `(2, 2)`: two rows, two columns
- `axis=1` means join along columns (side by side)
- Row 0: `[1, 2]` from arr1 + `[5, 6]` from arr2 = `[1, 2, 5, 6]`
- Row 1: `[3, 4]` from arr1 + `[7, 8]` from arr2 = `[3, 4, 7, 8]`

> **Axis 0 vs Axis 1 intuition:**
> - `axis=0` → stack one ON TOP OF the other (add more rows)
> - `axis=1` → place one BESIDE the other (add more columns)

### 6.3 Joining with stack()

`np.stack()` is similar to `concatenate()`, but with one important difference: **stacking creates a NEW axis**, while concatenating joins along an existing axis.

**Analogy:**
- `concatenate()` = laying sheets of paper end-to-end on the same table
- `stack()` = placing sheets of paper on top of each other to create a pile (a new dimension)

**Example — Stack two 1D arrays along axis=1:**

```python
import numpy as np

arr1 = np.array([1, 2, 3])

arr2 = np.array([4, 5, 6])

arr = np.stack((arr1, arr2), axis=1)

print(arr)
```

**Expected Output:**
```
[[1 4]
 [2 5]
 [3 6]]
```

**Explanation:**
- Both arrays have 3 elements
- `axis=1` creates a new second dimension (columns)
- Element `arr1[0]=1` and `arr2[0]=4` become the first row `[1, 4]`
- Element `arr1[1]=2` and `arr2[1]=5` become the second row `[2, 5]`
- Element `arr1[2]=3` and `arr2[2]=6` become the third row `[3, 6]`
- Result shape: `(3, 2)` — 3 rows, 2 columns

### 6.4 Convenience Stacking Functions

NumPy also provides three helper functions for common stacking directions:

#### hstack() — Stack Horizontally (Along Rows)

"h" stands for horizontal. `hstack()` joins arrays side by side — adding columns.

```python
import numpy as np

arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])

arr = np.hstack((arr1, arr2))

print(arr)
```

**Expected Output:**
```
[1 2 3 4 5 6]
```

**Explanation:** Elements placed next to each other horizontally (in the same row). For 1D arrays, this is the same as `concatenate()`.

#### vstack() — Stack Vertically (Along Columns)

"v" stands for vertical. `vstack()` stacks arrays on top of each other — adding rows.

```python
import numpy as np

arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])

arr = np.vstack((arr1, arr2))

print(arr)
```

**Expected Output:**
```
[[1 2 3]
 [4 5 6]]
```

**Explanation:** `arr2` is placed as a new row beneath `arr1`. The result has 2 rows and 3 columns.

#### dstack() — Stack Along Depth (Height)

"d" stands for depth. `dstack()` stacks arrays along a third axis — going deep, like layers.

```python
import numpy as np

arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])

arr = np.dstack((arr1, arr2))

print(arr)
```

**Expected Output:**
```
[[[1 4]
  [2 5]
  [3 6]]]
```

**Explanation:**
- This creates a 3D array with shape `(1, 3, 2)`
- Each pair of matching-index elements is combined into the depth dimension
- Position 0: `[1, 4]` (1 from arr1, 4 from arr2)
- Position 1: `[2, 5]`
- Position 2: `[3, 6]`

> **Quick summary table:**
>
> | Function | Direction | Adds New Axis? |
> |----------|-----------|----------------|
> | `hstack()` | Horizontal (side by side) | No |
> | `vstack()` | Vertical (top and bottom) | No |
> | `dstack()` | Depth (3rd dimension) | Yes |
> | `stack()` | Any axis | Yes |
> | `concatenate()` | Any existing axis | No |

---

## Guided Practice Exercises

### Exercise 1 — Data Types

**Objective:** Practise checking and converting data types.

**Scenario:** You have a list of temperature readings stored as floats. You want to check the type, convert them to integers (for approximate comparison), and verify.

**Steps:**

1. Create an array: `temperatures = np.array([36.6, 37.1, 38.2, 36.9, 37.5])`
2. Print the dtype
3. Convert to integers using `.astype(int)`
4. Print the new array and its dtype
5. Check: what happened to the decimal parts?

**Expected output after step 4:**
```
[36 37 38 36 37]
int64
```

**Self-check questions:**
- Was 37.1 rounded to 37 or truncated to 37? (Both give 37 here, but what about 37.9?)
- What would `astype(bool)` give for these temperature values?

---

### Exercise 2 — Copy vs View

**Objective:** Understand when data is shared and when it is independent.

**Scenario:** You have a student grade array. You make a copy for a "backup" and a view for "display". You then update a grade.

**Steps:**

1. Create: `grades = np.array([85, 90, 78, 92, 88])`
2. Make a copy: `backup = grades.copy()`
3. Make a view: `display = grades.view()`
4. Update: `grades[2] = 100`
5. Print `grades`, `backup`, and `display`
6. Check `.base` for both `backup` and `display`

**Expected output:**
```
[85 90 100 92 88]   # grades (original, changed)
[85 90  78 92 88]   # backup (copy, unchanged)
[85 90 100 92 88]   # display (view, changed with original)
```

**Self-check questions:**
- What does `backup.base` return?
- What does `display.base` return?
- Why is it important to use `.copy()` when you need an independent backup?

---

### Exercise 3 — Shape and Reshape

**Objective:** Practise understanding and changing array structures.

**Scenario:** A data scientist has 24 daily measurements and needs to organise them into a weekly table.

**Steps:**

1. Create: `data = np.arange(1, 25)` (creates an array from 1 to 24)
2. Print the shape
3. Reshape into 4 weeks × 6 days: `data.reshape(4, 6)`
4. Print the reshaped array
5. Reshape into 3D: 2 groups × 3 rows × 4 columns
6. Flatten back to 1D using `reshape(-1)`

**Hints:**
- `np.arange(1, 25)` creates `[1, 2, 3, ..., 24]`
- 4 × 6 = 24 ✓
- 2 × 3 × 4 = 24 ✓

**Expected output for step 3:**
```
[[ 1  2  3  4  5  6]
 [ 7  8  9 10 11 12]
 [13 14 15 16 17 18]
 [19 20 21 22 23 24]]
```

---

### Exercise 4 — Iterating

**Objective:** Practise looping through multi-dimensional arrays.

**Scenario:** You have a 3×3 multiplication table and need to print every value.

**Steps:**

1. Create: `table = np.array([[1,2,3],[2,4,6],[3,6,9]])`
2. Use nested `for` loops to print every element
3. Repeat using `np.nditer()`
4. Use `np.ndenumerate()` to print each element with its position

**Expected output for step 4:**
```
(0, 0) 1
(0, 1) 2
(0, 2) 3
(1, 0) 2
(1, 1) 4
(1, 2) 6
(2, 0) 3
(2, 1) 6
(2, 2) 9
```

---

### Exercise 5 — Joining Arrays

**Objective:** Practise combining arrays in different directions.

**Scenario:** You have two student score tables from two classes and want to combine them.

**Steps:**

1. Create: `class1 = np.array([[80, 85], [90, 88]])`
2. Create: `class2 = np.array([[75, 79], [95, 91]])`
3. Use `concatenate(axis=0)` to stack classes vertically (add more students)
4. Use `concatenate(axis=1)` to add more subjects (side by side)
5. Use `vstack()` for step 3 and `hstack()` for step 4

**Expected output for step 3:**
```
[[80 85]
 [90 88]
 [75 79]
 [95 91]]
```

**Expected output for step 4:**
```
[[80 85 75 79]
 [90 88 95 91]]
```

---

## Mini Project — Student Performance Analyser

**Goal:** Build a small data pipeline that uses all six topics from this lesson.

**Scenario:** You are a data analyst at a school. You have raw exam score data as a flat list of 12 scores (from 4 students across 3 subjects). You need to organise, inspect, and extend this data.

### Stage 1 — Setup and Data Inspection

```python
import numpy as np

# 12 raw scores: 4 students, 3 subjects each
raw_scores = np.array([72, 85, 90, 68, 79, 88, 95, 77, 82, 55, 91, 63])

# Step 1: Check the dtype
print("Data type:", raw_scores.dtype)

# Step 2: Check the shape
print("Shape:", raw_scores.shape)
```

**Expected output:**
```
Data type: int64
Shape: (12,)
```

### Stage 2 — Reshape into Student × Subject Table

```python
# Reshape into 4 students × 3 subjects
score_table = raw_scores.reshape(4, 3)

print("Score Table:")
print(score_table)
print("New shape:", score_table.shape)
```

**Expected output:**
```
Score Table:
[[72 85 90]
 [68 79 88]
 [95 77 82]
 [55 91 63]]
New shape: (4, 3)
```

### Stage 3 — Create a Backup (Copy) and a View

```python
# Safe backup (independent copy)
backup = score_table.copy()

# Display view (linked to original)
display = score_table.view()

# Modify a score (student 3 had a data entry error)
score_table[3, 2] = 73

print("Updated table:")
print(score_table)
print("\nBackup (unchanged):")
print(backup)
print("\nDisplay view (reflects update):")
print(display)
```

**Expected output:**
```
Updated table:
[[72 85 90]
 [68 79 88]
 [95 77 82]
 [55 91 73]]

Backup (unchanged):
[[72 85 90]
 [68 79 88]
 [95 77 82]
 [55 91 63]]

Display view (reflects update):
[[72 85 90]
 [68 79 88]
 [95 77 82]
 [55 91 73]]
```

### Stage 4 — Iterate and Find Each Student's Data

```python
# Print each student's scores with their row index
print("Student scores by index:")
for idx, score in np.ndenumerate(score_table):
    print(f"  Student {idx[0]+1}, Subject {idx[1]+1}: {score}")
```

**Expected output (first few lines):**
```
Student scores by index:
  Student 1, Subject 1: 72
  Student 1, Subject 2: 85
  Student 1, Subject 3: 90
  Student 2, Subject 1: 68
  ...
```

### Stage 5 — Add New Class Data and Join

```python
# New class data — 4 more students
new_class = np.array([[88, 74, 69], [91, 85, 78], [60, 55, 72], [77, 83, 88]])

# Combine both classes (axis=0 = add more rows)
all_students = np.concatenate((score_table, new_class), axis=0)

print("All students combined:")
print(all_students)
print("Combined shape:", all_students.shape)
```

**Expected output:**
```
All students combined:
[[72 85 90]
 [68 79 88]
 [95 77 82]
 [55 91 73]
 [88 74 69]
 [91 85 78]
 [60 55 72]
 [77 83 88]]
Combined shape: (8, 3)
```

### Stage 6 — Convert and Flatten

```python
# Convert scores to boolean (True = passed with any score, False = 0)
bool_scores = all_students.astype(bool)
print("\nAll non-zero? (True = has a score):")
print(bool_scores)

# Flatten the entire score table to 1D
flat_scores = all_students.reshape(-1)
print("\nFlat list of all scores:")
print(flat_scores)
```

**Reflection questions:**
- Which axis would you use to add a 4th subject column to all students?
- Why is it important to keep the backup before making changes?
- What shape would you get if you stacked the two classes with `np.stack()` instead of `np.concatenate()`?

**Optional extension:** Try computing the average score for each student using `np.mean(all_students, axis=1)`.

---

## Common Beginner Mistakes

### Mistake 1 — Assuming astype() Rounds (It Does Not)

```python
# WRONG assumption:
arr = np.array([2.9, 3.7])
result = arr.astype(int)
# Beginner expects: [3, 4]
# Reality: [2, 3]  <- truncated, not rounded!
```

**Fix:** Use `np.round()` first if you need rounding, then convert.

```python
arr = np.array([2.9, 3.7])
result = np.round(arr).astype(int)
print(result)  # Output: [3 4]
```

---

### Mistake 2 — Treating a View Like a Copy

```python
arr = np.array([1, 2, 3, 4, 5])
x = arr.view()        # NOT a copy!
x[0] = 999            # This changes arr too!
print(arr)            # [999  2  3  4  5] — surprise!
```

**Fix:** Use `.copy()` when you need independence.

```python
x = arr.copy()        # Now truly independent
x[0] = 999
print(arr)            # [1 2 3 4 5] — original is safe
```

---

### Mistake 3 — Invalid Reshape (Forgetting to Check Total Elements)

```python
arr = np.array([1, 2, 3, 4, 5, 6])
# WRONG: 6 elements cannot form a 2x4 grid (2x4=8, not 6)
result = arr.reshape(2, 4)  # ValueError!
```

**Fix:** Always verify that `new_shape[0] × new_shape[1] × ... = original_total_elements`.

```python
# Correct options for 6 elements:
arr.reshape(2, 3)   # 2x3=6 ✓
arr.reshape(3, 2)   # 3x2=6 ✓
arr.reshape(6, 1)   # 6x1=6 ✓
arr.reshape(1, 6)   # 1x6=6 ✓
arr.reshape(2, 3, 1) # 2x3x1=6 ✓
```

---

### Mistake 4 — Using -1 in More Than One Dimension

```python
arr = np.array([1, 2, 3, 4, 5, 6])
# WRONG: can only use -1 once
result = arr.reshape(-1, -1)  # ValueError!
```

**Fix:** Only one dimension can be -1. Specify all other dimensions explicitly.

```python
result = arr.reshape(2, -1)  # NumPy calculates: 6/2=3, so shape (2,3) ✓
```

---

### Mistake 5 — Concatenating Arrays with Mismatched Shapes

```python
arr1 = np.array([[1, 2, 3]])      # shape (1, 3)
arr2 = np.array([[4, 5], [6, 7]]) # shape (2, 2)
result = np.concatenate((arr1, arr2), axis=0)  # Error! Different column counts
```

**Fix:** All arrays being concatenated must match in ALL dimensions except the one being combined.

```python
arr1 = np.array([[1, 2], [3, 4]])  # shape (2, 2)
arr2 = np.array([[5, 6], [7, 8]])  # shape (2, 2)
result = np.concatenate((arr1, arr2), axis=0)  # shape (4, 2) ✓
```

---

## Reflection Questions

1. What is the difference between a NumPy data type like `int32` and Python's regular `int`? Why would you choose one over the other?

2. You have two students' project files as arrays. Student A's file has 50 values and Student B's file has 50 values. What is the difference between using `concatenate()` and `stack()` to combine them? Which gives you a 2D array and which gives you a 1D array?

3. If you have an array of shape `(6, 4)` and you want to convert it to shape `(8, 3)`, is this possible? How would you check?

4. You iterate through a 2D array using just one `for` loop. What does each iteration give you — rows, columns, or individual elements?

5. You made a view of an array and gave it to a colleague. They changed a value in their "copy". Your original also changed. Whose fault is this, and how could it have been prevented?

6. In what real-world situation would `dstack()` be more useful than `hstack()` or `vstack()`? (Hint: think about image data with colour channels.)

7. You need to process every element of a 5-dimensional array. Would you use nested `for` loops or `np.nditer()`? Why?

---

## Completion Checklist

Before moving on, verify you can do each of the following:

- [ ] Explain what `.dtype` is and how to check it on a NumPy array
- [ ] Name at least 5 NumPy data type codes (e.g., `i`, `f`, `S`, `b`, `U`)
- [ ] Create an array with a specified dtype using the `dtype=` parameter
- [ ] Convert an array to a different type using `.astype()`
- [ ] Explain the difference between a copy and a view
- [ ] Use `.copy()` to create an independent array
- [ ] Use `.view()` to create a linked view
- [ ] Use `.base` to check if an array owns its data
- [ ] Read a `.shape` tuple and understand what each number means
- [ ] Reshape an array from 1D to 2D and 3D
- [ ] Use `-1` as a wildcard dimension in `reshape()`
- [ ] Flatten a multi-dimensional array using `reshape(-1)`
- [ ] Iterate through 1D, 2D, and 3D arrays using `for` loops
- [ ] Use `np.nditer()` to iterate over all elements in any-dimensional array
- [ ] Use `np.ndenumerate()` to get element positions and values together
- [ ] Join two arrays using `np.concatenate()` with axis=0 and axis=1
- [ ] Explain the difference between `hstack()`, `vstack()`, and `dstack()`
- [ ] Use `np.stack()` to create a new axis during combination

---

## Lesson Summary

In this lesson, you explored six essential NumPy tools used by every data scientist:

**Data Types:** NumPy arrays store values with precise types (`int32`, `float64`, `bool`, `U`, etc.). Use `.dtype` to check the type and `.astype()` to convert to a different type. Conversion truncates floats (does not round) when converting to integers.

**Copy vs View:** A `.copy()` creates an independent new array — changes to one do not affect the other. A `.view()` creates a window into the same data — changes to one affect both. Use `.base` to check: `None` = copy/original, otherwise = view.

**Shape:** The `.shape` attribute returns a tuple showing how many elements exist in each dimension. For a table with 3 rows and 4 columns, shape is `(3, 4)`.

**Reshape:** `reshape()` rearranges data into a new structure without changing the values. The total number of elements must stay the same. Use `-1` for one unknown dimension. Use `reshape(-1)` to flatten any array to 1D. Reshape returns a view, not a copy.

**Iterating:** A single `for` loop on an N-D array gives you slices of dimension N-1. To reach individual values, use N nested loops. `np.nditer()` handles any number of dimensions with just one loop. `np.ndenumerate()` gives both the index and value at each step.

**Joining:** `np.concatenate()` merges arrays along an existing axis. `np.stack()` creates a new axis. `hstack()`, `vstack()`, and `dstack()` are shortcuts for horizontal, vertical, and depth stacking.

> **Coming up next:** In Lesson 26, you will learn how to split arrays apart, search for elements, sort data, and apply filters — completing your toolkit for professional-grade NumPy array manipulation.
