---
render_with_liquid: false
title: "NumPy Array Operations: Splitting, Searching, Sorting, Filtering & Random Numbers"
nav_order: 26
---

# Lesson 26 — NumPy Array Operations: Splitting, Searching, Sorting, Filtering & Random Numbers

---

## Lesson Introduction

Welcome to Lesson 26! In this lesson, you will master five incredibly powerful NumPy skills that data scientists, engineers, and programmers use every single day:

1. **Splitting** — breaking one array into multiple smaller arrays
2. **Searching** — finding where values live inside an array
3. **Sorting** — arranging array elements in order
4. **Filtering** — keeping only elements that meet a condition
5. **Random Numbers** — generating random integers, floats, and arrays

By the end of this lesson, you will be able to write a realistic mini-project that reads a dataset of student exam scores, cleans it, filters it, sorts it, splits it into groups, and generates random mock data for testing.

> **Real-world relevance:** Every major field — data science, machine learning, finance, science, and engineering — relies on these five operations constantly. If you master them, you can analyse real datasets with confidence.

---

## Prerequisite Concepts

Before we begin, make sure you are comfortable with these ideas. If any of them are unfamiliar, read the short explanation below before continuing.

### What is a NumPy Array?

A NumPy array is a grid of values — like a list, but much more powerful and faster. Every value in the array has a **position number called an index**, starting from `0`.

```python
import numpy as np

arr = np.array([10, 20, 30, 40, 50])
#               0    1   2   3   4   ← index numbers
```

Think of an array like a row of numbered mailboxes. Index 0 is the first mailbox, index 1 is the second, and so on.

### What is an Index?

An **index** is just the position of an element inside an array. It starts at `0`, not `1`. So the first element is at index `0`, the second at index `1`, etc.

### What is a Boolean?

A **boolean** is a value that is either `True` or `False`. Think of it like a light switch — it is either ON (`True`) or OFF (`False`).

### Quick Setup — Always Import NumPy First

Every code example in this lesson needs NumPy to be imported. Always start your program with:

```python
import numpy as np
```

---

## Section 1 — Splitting Arrays

### What is Splitting? Why Do We Need It?

Imagine you have a long list of 1,000 exam scores and you want to give each of three teachers a portion of the scores to grade. You would **split** the big list into three smaller ones. That is exactly what NumPy splitting does.

**Splitting** is the reverse of joining. Joining merges multiple arrays into one. Splitting breaks one array into multiple parts.

> **Analogy:** Think of a loaf of bread. Joining is baking multiple loaves together. Splitting is slicing one loaf into separate pieces.

---

### The `np.array_split()` Function

**What it does:** Splits one array into a given number of smaller arrays.

**Syntax:**
```python
result = np.array_split(array, number_of_splits)
```

- `array` — the array you want to split
- `number_of_splits` — how many pieces to make
- `result` — a Python **list** of smaller arrays

> **Important:** The return value is a **list** of arrays, not a single array!

---

### Example 1 — Split into 3 Equal Parts

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6])

newarr = np.array_split(arr, 3)

print(newarr)
```

**Expected Output:**
```
[array([1, 2]), array([3, 4]), array([5, 6])]
```

**Line-by-line explanation:**
- `arr = np.array([1, 2, 3, 4, 5, 6])` — creates an array with 6 elements
- `np.array_split(arr, 3)` — splits arr into 3 equal pieces: [1,2], [3,4], [5,6]
- `print(newarr)` — prints the list of 3 small arrays

> **Notice:** Each piece has exactly 2 elements because 6 ÷ 3 = 2.

---

### Example 2 — Split into 4 Parts (Unequal Division)

What happens when the array cannot be divided equally? NumPy handles this gracefully — it adjusts the sizes from the end.

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6])

newarr = np.array_split(arr, 4)

print(newarr)
```

**Expected Output:**
```
[array([1, 2]), array([3, 4]), array([5]), array([6])]
```

**Explanation:**
- 6 elements split into 4 parts: the first two parts get 2 elements, the last two parts get 1 element each.
- NumPy does NOT crash or complain — it adjusts automatically.

> **Thinking prompt:** What would happen if you tried to split 6 elements into 7 parts? Some parts would be empty! Try it and see.

> **Important note:** The regular `np.split()` function would crash here if the division is not exactly equal. Always prefer `np.array_split()` for flexibility.

---

### Accessing Individual Split Pieces

The result of `array_split()` is a list. You can access each piece using list index notation `[0]`, `[1]`, `[2]`, etc.

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6])

newarr = np.array_split(arr, 3)

print(newarr[0])   # First piece
print(newarr[1])   # Second piece
print(newarr[2])   # Third piece
```

**Expected Output:**
```
[1 2]
[3 4]
[5 6]
```

---

### Splitting 2-D Arrays (Tables)

A 2-D array is like a table with rows and columns. Splitting a 2-D array works by splitting along rows by default.

#### Example — Split a 2-D Array Into 3 Parts (Row-wise)

```python
import numpy as np

arr = np.array([[1, 2],
                [3, 4],
                [5, 6],
                [7, 8],
                [9, 10],
                [11, 12]])

newarr = np.array_split(arr, 3)

print(newarr)
```

**Expected Output:**
```
[array([[1, 2],
        [3, 4]]),
 array([[5, 6],
        [7, 8]]),
 array([[ 9, 10],
        [11, 12]])]
```

**Explanation:** The 6-row table is split into three 2-row tables.

---

#### Example — Split a 2-D Array Along Columns (axis=1)

You can split along **columns** instead of rows by using `axis=1`.

```python
import numpy as np

arr = np.array([[1, 2, 3],
                [4, 5, 6],
                [7, 8, 9],
                [10, 11, 12],
                [13, 14, 15],
                [16, 17, 18]])

newarr = np.array_split(arr, 3, axis=1)

print(newarr)
```

**Expected Output:**
```
[array([[ 1],
        [ 4],
        [ 7],
        [10],
        [13],
        [16]]),
 array([[ 2],
        [ 5],
        [ 8],
        [11],
        [14],
        [17]]),
 array([[ 3],
        [ 6],
        [ 9],
        [12],
        [15],
        [18]])]
```

**Explanation:**
- `axis=0` means split along rows (default)
- `axis=1` means split along columns
- The 3-column table is split into three 1-column tables

---

### The `hsplit()` Shortcut

`np.hsplit()` is a shorthand for splitting along columns (horizontal split). It is equivalent to `array_split(arr, n, axis=1)`.

```python
import numpy as np

arr = np.array([[1, 2, 3],
                [4, 5, 6],
                [7, 8, 9],
                [10, 11, 12],
                [13, 14, 15],
                [16, 17, 18]])

newarr = np.hsplit(arr, 3)

print(newarr)
```

**Expected Output:** Same as the `axis=1` example above.

> **Tip:** Similarly, `np.vsplit()` splits vertically (same as `axis=0`), and `np.dsplit()` splits along the depth axis for 3-D arrays.

---

## Section 2 — Searching Arrays

### What is Searching? Why Do We Need It?

Imagine you have an array of 10,000 temperature readings and you need to find all positions where the temperature exceeded 40°C. You could loop through every element yourself, but NumPy gives you a much faster, cleaner tool: `np.where()`.

**Searching** means finding the **index positions** where elements match a condition.

---

### The `np.where()` Function

**What it does:** Returns the index positions where a given condition is `True`.

**Syntax:**
```python
result = np.where(condition)
```

- `condition` — a comparison like `arr == 4` or `arr > 10`
- `result` — a **tuple** containing an array of matching index positions

> **What is a tuple?** A tuple is like a list but surrounded by `()` instead of `[]`. It cannot be changed after creation.

---

### Example 1 — Find Where a Specific Value Appears

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5, 4, 4])

x = np.where(arr == 4)

print(x)
```

**Expected Output:**
```
(array([3, 5, 6]),)
```

**Line-by-line explanation:**
- `arr == 4` — checks every element: is this equal to 4?
- `np.where(arr == 4)` — returns the positions where the answer is True
- The value `4` appears at index 3, 5, and 6

> **Thinking prompt:** What does the outer `(...)` wrapping the result mean? It means `np.where` returns a tuple. To get just the array inside, you can write `x[0]`.

---

### Example 2 — Find All Odd Numbers

The `%` symbol is the **modulo operator**. It gives the **remainder** after division.

- `7 % 2 = 1` (because 7 ÷ 2 = 3 remainder **1**)
- `8 % 2 = 0` (because 8 ÷ 2 = 4 remainder **0**)
- If `number % 2 == 1`, the number is **odd**
- If `number % 2 == 0`, the number is **even**

```python
import numpy as np

arr = np.array([10, 14, 93, 41, 8, 7])

x = np.where(arr % 2 == 1)

print(x)
```

**Expected Output:**
```
(array([2, 3, 5]),)
```

**Explanation:**
- Check each element: 10%2=0 (even), 14%2=0 (even), 93%2=1 (**odd** → index 2), 41%2=1 (**odd** → index 3), 8%2=0 (even), 7%2=1 (**odd** → index 5)
- Odd numbers are at positions 2, 3, and 5

---

### Example 3 — Find All Even Numbers

```python
import numpy as np

arr = np.array([10, 14, 93, 41, 8, 7])

x = np.where(arr % 2 == 0)

print(x)
```

**Expected Output:**
```
(array([0, 1, 4]),)
```

**Explanation:** Even numbers (10, 14, 8) are at index positions 0, 1, and 4.

---

### The `np.searchsorted()` Function — Binary Search

Sometimes you have a **sorted** array and you want to know **where to insert a new value** so the array stays sorted. This is called a **binary search**.

**What is binary search?** Instead of checking every element one by one, binary search repeatedly cuts the array in half to find the right position very quickly. It is like looking up a word in a dictionary by opening to the middle first.

**Syntax:**
```python
result = np.searchsorted(sorted_array, value)
```

- `sorted_array` — must already be sorted in ascending order
- `value` — the number you want to insert
- Returns the **index** where you should insert the value to keep the array sorted

---

### Example 1 — Basic searchsorted

```python
import numpy as np

arr = np.array([6, 7, 8, 9])

x = np.searchsorted(arr, 7)

print(x)
```

**Expected Output:**
```
1
```

**Explanation:**
- The array is `[6, 7, 8, 9]`
- If we insert `7` at index **1**, the array stays sorted: `[6, 7, 7, 8, 9]`
- The method searches from the **left** by default, so it finds the first position where 7 is no longer larger than the next value

---

### Example 2 — Search From the Right Side

By default, `searchsorted()` returns the **leftmost** valid position. If you want the **rightmost** position, use `side='right'`.

```python
import numpy as np

arr = np.array([6, 7, 8, 9])

x = np.searchsorted(arr, 7, side='right')

print(x)
```

**Expected Output:**
```
2
```

**Explanation:**
- Searching from the right: the value `7` should be inserted at index **2** to keep sorted order: `[6, 7, 7, 8, 9]`
- `side='left'` → insert before existing 7 → index 1
- `side='right'` → insert after existing 7 → index 2

---

### Example 3 — Search for Multiple Values at Once

```python
import numpy as np

arr = np.array([1, 3, 5, 7])

x = np.searchsorted(arr, [2, 4, 6])

print(x)
```

**Expected Output:**
```
[1 2 3]
```

**Explanation:**
- `2` would go at index **1** (between 1 and 3)
- `4` would go at index **2** (between 3 and 5)
- `6` would go at index **3** (between 5 and 7)

> **Real-world use:** Binary search with `searchsorted` is used in stock market order books, database lookups, and anywhere you need to find where to insert a value quickly in a sorted list.

---

## Section 3 — Sorting Arrays

### What is Sorting? Why Do We Need It?

Sorting means arranging elements in a specific order — usually from smallest to largest (**ascending**) or largest to smallest (**descending**). We sort data constantly in real life: ranking student scores, ordering products by price, alphabetising names.

---

### The `np.sort()` Function

**What it does:** Returns a sorted copy of the array, leaving the original unchanged.

**Syntax:**
```python
sorted_arr = np.sort(array)
```

> **Important:** `np.sort()` does NOT change the original array. It creates a **new sorted copy**. This is safe behaviour — your original data is preserved.

---

### Example 1 — Sort Numbers

```python
import numpy as np

arr = np.array([3, 2, 0, 1])

print(np.sort(arr))
```

**Expected Output:**
```
[0 1 2 3]
```

**Explanation:** The numbers are rearranged from smallest to largest.

> **Thinking prompt:** What happens to the original `arr` after sorting? It stays unchanged! Try printing `arr` after the sort to confirm.

---

### Example 2 — Sort Strings Alphabetically

NumPy can also sort arrays of text (strings)! It sorts them alphabetically, just like a dictionary.

```python
import numpy as np

arr = np.array(['banana', 'cherry', 'apple'])

print(np.sort(arr))
```

**Expected Output:**
```
['apple' 'banana' 'cherry']
```

**Explanation:** 'apple' comes first alphabetically, then 'banana', then 'cherry'.

---

### Example 3 — Sort Booleans

```python
import numpy as np

arr = np.array([True, False, True])

print(np.sort(arr))
```

**Expected Output:**
```
[False  True  True]
```

**Explanation:** In Python/NumPy, `False` is treated as `0` and `True` as `1`. So `False` sorts before `True`.

---

### Sorting a 2-D Array

When you sort a 2-D array, NumPy sorts **each row independently**.

```python
import numpy as np

arr = np.array([[3, 2, 4],
                [5, 0, 1]])

print(np.sort(arr))
```

**Expected Output:**
```
[[2 3 4]
 [0 1 5]]
```

**Explanation:**
- Row 1: `[3, 2, 4]` → sorted to `[2, 3, 4]`
- Row 2: `[5, 0, 1]` → sorted to `[0, 1, 5]`
- Each row is sorted separately

> **Thinking prompt:** What if you wanted to sort the columns instead of the rows? You could use `np.sort(arr, axis=0)`. Try it!

---

### How to Sort in Descending Order (Largest First)

`np.sort()` only sorts in ascending order by default. To sort in descending order, sort first, then reverse using `[::-1]`.

```python
import numpy as np

arr = np.array([3, 1, 4, 1, 5, 9, 2, 6])

sorted_desc = np.sort(arr)[::-1]

print(sorted_desc)
```

**Expected Output:**
```
[9 6 5 4 3 2 1 1]
```

**Explanation:**
- `np.sort(arr)` gives `[1, 1, 2, 3, 4, 5, 6, 9]`
- `[::-1]` reverses it to `[9, 6, 5, 4, 3, 2, 1, 1]`

---

## Section 4 — Filtering Arrays

### What is Filtering? Why Do We Need It?

Filtering means **selecting only the elements that meet a condition** and creating a new array with just those elements.

Think of it like a coffee filter: you pour in a mixture, and only what passes through the filter gets collected. In NumPy, only elements that pass your condition get collected.

**Real-world examples:**
- Keep only exam scores above 50 (passing scores)
- Keep only temperatures below 0°C (freezing days)
- Keep only even product IDs
- Keep only positive financial transactions

---

### What is a Boolean Index List?

A **boolean index list** is a list of `True` and `False` values, one for each element in an array. When you use it to index an array:
- Elements with `True` → **included** in the result
- Elements with `False` → **excluded** from the result

---

### Example 1 — Manual Boolean Filter (Hard-coded)

```python
import numpy as np

arr = np.array([41, 42, 43, 44])

x = [True, False, True, False]

newarr = arr[x]

print(newarr)
```

**Expected Output:**
```
[41 43]
```

**Line-by-line explanation:**
- `arr = [41, 42, 43, 44]` — four elements at index 0, 1, 2, 3
- `x = [True, False, True, False]` — index 0 = True, index 1 = False, index 2 = True, index 3 = False
- `arr[x]` — keep index 0 (41 ✓), skip index 1 (42 ✗), keep index 2 (43 ✓), skip index 3 (44 ✗)
- Result: `[41, 43]`

> **Thinking prompt:** Why was 42 excluded? Because the value at its position in the filter list was `False`.

---

### Example 2 — Building a Filter with a Loop

In practice, you almost never hard-code `True` and `False`. Instead, you build the filter automatically using a loop.

**Scenario:** Keep only values higher than 42.

```python
import numpy as np

arr = np.array([41, 42, 43, 44])

# Step 1: Create an empty list to hold True/False values
filter_arr = []

# Step 2: Go through each element in arr
for element in arr:
    # Step 3: If the element is higher than 42, add True; otherwise add False
    if element > 42:
        filter_arr.append(True)
    else:
        filter_arr.append(False)

# Step 4: Apply the filter to the array
newarr = arr[filter_arr]

print(filter_arr)
print(newarr)
```

**Expected Output:**
```
[False, False, True, True]
[43 44]
```

**Line-by-line explanation:**
- We loop through `[41, 42, 43, 44]`
- `41 > 42`? No → `False`
- `42 > 42`? No → `False`
- `43 > 42`? Yes → `True`
- `44 > 42`? Yes → `True`
- `filter_arr = [False, False, True, True]`
- `arr[filter_arr]` keeps only elements at `True` positions → `[43, 44]`

---

### Example 3 — Loop Filter for Even Numbers

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6, 7])

filter_arr = []

for element in arr:
    if element % 2 == 0:    # Is the remainder zero? (even number?)
        filter_arr.append(True)
    else:
        filter_arr.append(False)

newarr = arr[filter_arr]

print(filter_arr)
print(newarr)
```

**Expected Output:**
```
[False, True, False, True, False, True, False]
[2 4 6]
```

---

### Example 4 — The NumPy Shortcut: Direct Array Conditions ⭐

The loop method works but is long. NumPy provides a much shorter and more elegant way: you can write the condition **directly on the array**, and NumPy creates the boolean array automatically!

**Filtering values > 42:**

```python
import numpy as np

arr = np.array([41, 42, 43, 44])

filter_arr = arr > 42

newarr = arr[filter_arr]

print(filter_arr)
print(newarr)
```

**Expected Output:**
```
[False False  True  True]
[43 44]
```

**What happened?** `arr > 42` does NOT give a single True/False. It checks every element and returns a **boolean array**: `[False, False, True, True]`. This is called **vectorised comparison** — NumPy processes all elements at once, which is much faster than a Python loop.

---

### Example 5 — Direct Filter for Even Numbers (Short Version)

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6, 7])

filter_arr = arr % 2 == 0

newarr = arr[filter_arr]

print(filter_arr)
print(newarr)
```

**Expected Output:**
```
[False  True False  True False  True False]
[2 4 6]
```

---

### One-Line Filtering

You can even combine the filter and the indexing into a single line:

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6, 7])

newarr = arr[arr % 2 == 0]

print(newarr)
```

**Expected Output:**
```
[2 4 6]
```

This is the most common style used by professional data scientists.

---

## Section 5 — Random Numbers in NumPy

### What is a Random Number?

A **random number** is a number that cannot be predicted logically before it is generated. This is different from simply "a number that changes" — true randomness means there is no pattern.

**Pseudo-random vs True Random:**
- **Pseudo-random:** Generated by a mathematical algorithm. It looks random but is technically predictable if you know the algorithm and starting point (called a "seed"). This is what NumPy uses.
- **True random:** Generated from unpredictable physical sources like keyboard timings, mouse movements, or atmospheric noise.

For most purposes — simulations, testing, data science, games — **pseudo-random numbers are perfectly fine**.

---

### Importing the Random Module

```python
from numpy import random
```

Or you can use `np.random` after importing NumPy:
```python
import numpy as np
# then use: np.random.randint(...)
```

Both approaches work. In this lesson, we use `from numpy import random` to keep examples concise.

---

### Generating a Single Random Integer

`random.randint(n)` returns a random integer from **0 up to but not including n**.

```python
from numpy import random

x = random.randint(100)

print(x)
```

**Expected Output:** A random integer between 0 and 99 (e.g., `47`)

> **Note:** Your output will be different each time you run this! That is the whole point.

**Real-world analogy:** This is like rolling a 100-sided die and reading the number.

---

### Generating a Single Random Float

`random.rand()` returns a random decimal number between **0.0 and 1.0** (never exactly 1.0).

```python
from numpy import random

x = random.rand()

print(x)
```

**Expected Output:** A random float like `0.5488135039273248`

---

### Generating a 1-D Array of Random Integers

Use `randint(high, size=(n))` to generate an array of `n` random integers from 0 to `high - 1`.

```python
from numpy import random

x = random.randint(100, size=(5))

print(x)
```

**Expected Output:** 5 random integers, e.g., `[51 92 14 71 60]`

---

### Generating a 2-D Array of Random Integers

Use `size=(rows, columns)` to make a 2-D array.

```python
from numpy import random

x = random.randint(100, size=(3, 5))

print(x)
```

**Expected Output:** A 3-row, 5-column table of random integers, e.g.:
```
[[44 38 69 21  5]
 [81 63 27 72  8]
 [96  3 44 56 78]]
```

---

### Generating a 1-D Array of Random Floats

`rand(n)` generates `n` random floats between 0.0 and 1.0.

```python
from numpy import random

x = random.rand(5)

print(x)
```

**Expected Output:** 5 random decimals, e.g., `[0.548 0.715 0.603 0.545 0.424]`

---

### Generating a 2-D Array of Random Floats

```python
from numpy import random

x = random.rand(3, 5)

print(x)
```

**Expected Output:** A 3-row, 5-column table of random floats between 0 and 1.

---

### Generating Random Values from a Custom List: `choice()`

`random.choice()` picks a random value from an array you provide.

```python
from numpy import random

x = random.choice([3, 5, 7, 9])

print(x)
```

**Expected Output:** One of: `3`, `5`, `7`, or `9` (randomly chosen)

---

### Generating a 2-D Array from a Custom List

```python
from numpy import random

x = random.choice([3, 5, 7, 9], size=(3, 5))

print(x)
```

**Expected Output:** A 3×5 grid where every value is one of 3, 5, 7, or 9, e.g.:
```
[[9 5 3 7 9]
 [5 5 7 3 9]
 [7 5 5 7 9]]
```

---

### Quick Summary of Random Functions

| Function | What it does | Example |
|---|---|---|
| `random.randint(n)` | One random integer from 0 to n-1 | `random.randint(10)` → `7` |
| `random.randint(n, size=(k))` | Array of k random integers | `random.randint(10, size=(5))` |
| `random.randint(n, size=(r, c))` | 2-D array of random integers | `random.randint(10, size=(3, 4))` |
| `random.rand()` | One random float between 0.0 and 1.0 | `random.rand()` → `0.73` |
| `random.rand(k)` | Array of k random floats | `random.rand(5)` |
| `random.rand(r, c)` | 2-D array of random floats | `random.rand(3, 5)` |
| `random.choice(arr)` | One random value from arr | `random.choice([1,2,3])` → `2` |
| `random.choice(arr, size=(r, c))` | 2-D array from arr's values | `random.choice([1,2,3], size=(2,3))` |

---

## Guided Practice Exercises

### Exercise 1 — Splitting a Sensor Dataset

**Objective:** Practice splitting arrays into equal parts.

**Scenario:** You have 9 temperature readings from 3 weather stations. Split the data so each station gets its own set of readings.

**Steps:**
1. Create the array: `[22, 25, 19, 30, 28, 24, 15, 18, 21]`
2. Split it into 3 equal parts
3. Print each part separately

**Code:**
```python
import numpy as np

temperatures = np.array([22, 25, 19, 30, 28, 24, 15, 18, 21])

parts = np.array_split(temperatures, 3)

print("Station 1:", parts[0])
print("Station 2:", parts[1])
print("Station 3:", parts[2])
```

**Expected Output:**
```
Station 1: [22 25 19]
Station 2: [30 28 24]
Station 3: [15 18 21]
```

**Self-check:** How many elements should each station have? What happens if you split 9 elements into 4 groups?

---

### Exercise 2 — Finding Passing Scores

**Objective:** Practice using `np.where()` to find index positions.

**Scenario:** You have 7 student exam scores. Find which students passed (scored 50 or above).

**Steps:**
1. Create the scores array: `[45, 72, 38, 91, 55, 49, 83]`
2. Use `np.where()` to find positions where score >= 50
3. Print the positions
4. Print the actual passing scores

**Code:**
```python
import numpy as np

scores = np.array([45, 72, 38, 91, 55, 49, 83])

pass_positions = np.where(scores >= 50)

print("Positions of passing students:", pass_positions)
print("Passing scores:", scores[pass_positions])
```

**Expected Output:**
```
Positions of passing students: (array([1, 3, 4, 6]),)
Passing scores: [72 91 55 83]
```

**Self-check:** How many students passed? What score is at position 3?

---

### Exercise 3 — Sorting a Leaderboard

**Objective:** Practice sorting arrays.

**Scenario:** Sort student scores to build a leaderboard (highest first).

**Code:**
```python
import numpy as np

scores = np.array([45, 72, 38, 91, 55, 49, 83])

ascending = np.sort(scores)
descending = np.sort(scores)[::-1]

print("Sorted (low to high):", ascending)
print("Leaderboard (high to low):", descending)
```

**Expected Output:**
```
Sorted (low to high): [38 45 49 55 72 83 91]
Leaderboard (high to low): [91 83 72 55 49 45 38]
```

---

### Exercise 4 — Filtering Scores Above Average

**Objective:** Practice direct boolean filtering.

**Scenario:** Find and display only scores that are above the average.

**Code:**
```python
import numpy as np

scores = np.array([45, 72, 38, 91, 55, 49, 83])

average = np.mean(scores)  # np.mean() calculates the average
print("Average score:", average)

above_average = scores[scores > average]
print("Above-average scores:", above_average)
```

**Expected Output:**
```
Average score: 61.857142857142854
Above-average scores: [72 91 83]
```

---

### Exercise 5 — Generating Mock Exam Data

**Objective:** Practice using `random` to generate test data.

**Scenario:** Generate a random dataset of 20 student exam scores (between 0 and 100) for testing your code.

**Code:**
```python
from numpy import random
import numpy as np

mock_scores = random.randint(101, size=(20))

print("Mock scores:", mock_scores)
print("Highest:", np.max(mock_scores))
print("Lowest:", np.min(mock_scores))
print("Average:", np.mean(mock_scores).round(2))
```

**Expected Output (yours will differ):**
```
Mock scores: [51 92 14 71 60 20 82 86 74 74 87 99 23  2 21 52  1 87 29 37]
Highest: 99
Lowest: 1
Average: 53.15
```

---

## Mini Project — Student Score Analyser

This project combines all five skills from this lesson into a realistic data analysis tool.

### Project Overview

You are a teacher. You have a class of 12 students. You want to:
1. Generate mock scores (using random)
2. Sort the scores (from highest to lowest)
3. Filter out failing scores (below 50)
4. Find where specific score thresholds occur
5. Split the class into three performance groups

---

### Stage 1 — Setup: Generate Student Scores

```python
from numpy import random
import numpy as np

# Set a seed so we get the same "random" results each run (useful for testing)
random.seed(42)

# Generate 12 scores between 30 and 100
scores = random.randint(30, 101, size=(12))
student_ids = np.array([f"S{i+1:02d}" for i in range(12)])

print("=== RAW SCORES ===")
for sid, score in zip(student_ids, scores):
    print(f"  {sid}: {score}")
```

**Expected Output:**
```
=== RAW SCORES ===
  S01: 81
  S02: 82
  S03: 54
  S04: 93
  S05: 58
  S06: 68
  S07: 49
  S08: 46
  S09: 97
  S10: 64
  S11: 56
  S12: 76
```

> **New concept:** `random.seed(42)` fixes the random number generator so it always produces the same numbers. This is useful when you want reproducible results during testing. Change `42` to any number to get a different but reproducible set.

---

### Stage 2 — Sort the Scores (Leaderboard)

```python
sorted_scores = np.sort(scores)[::-1]   # Descending order

print("\n=== LEADERBOARD (Highest First) ===")
for rank, score in enumerate(sorted_scores, 1):
    print(f"  Rank {rank}: {score}")
```

**Expected Output:**
```
=== LEADERBOARD (Highest First) ===
  Rank 1: 97
  Rank 2: 93
  Rank 3: 82
  ...
```

---

### Stage 3 — Filter Passing and Failing Students

```python
passing_mask = scores >= 50
failing_mask = scores < 50

passing_scores = scores[passing_mask]
failing_scores = scores[failing_mask]

print(f"\n=== PASS/FAIL SUMMARY ===")
print(f"  Passing scores (>=50): {passing_scores}")
print(f"  Failing scores (<50):  {failing_scores}")
print(f"  Pass rate: {len(passing_scores)}/{len(scores)} students")
```

**Expected Output:**
```
=== PASS/FAIL SUMMARY ===
  Passing scores (>=50): [81 82 54 93 58 68 97 64 56 76]
  Failing scores (<50):  [49 46]
  Pass rate: 10/12 students
```

---

### Stage 4 — Search for Grade Boundaries

```python
# Find where grades cross the 70 threshold (B grade boundary)
b_grade_positions = np.where(scores >= 70)
print(f"\n=== B GRADE OR HIGHER (>=70) ===")
print(f"  Student positions: {b_grade_positions[0]}")
print(f"  Scores: {scores[b_grade_positions]}")

# Use searchsorted to find where 75 would rank in the sorted list
rank_of_75 = np.searchsorted(np.sort(scores), 75)
print(f"\n  A score of 75 would rank at position: {rank_of_75} in the sorted list")
```

---

### Stage 5 — Split into Performance Groups

```python
# Sort scores first, then split into 3 groups: bottom, middle, top
sorted_for_groups = np.sort(scores)
groups = np.array_split(sorted_for_groups, 3)

print("\n=== PERFORMANCE GROUPS ===")
print(f"  Bottom group:  {groups[0]}")
print(f"  Middle group:  {groups[1]}")
print(f"  Top group:     {groups[2]}")
```

**Expected Output:**
```
=== PERFORMANCE GROUPS ===
  Bottom group:  [46 49 54 56]
  Middle group:  [58 64 68 76]
  Top group:     [81 82 93 97]
```

---

### Stage 6 — Final Summary Dashboard

```python
print("\n=== FINAL CLASS SUMMARY ===")
print(f"  Total students:  {len(scores)}")
print(f"  Average score:   {np.mean(scores):.1f}")
print(f"  Highest score:   {np.max(scores)}")
print(f"  Lowest score:    {np.min(scores)}")
print(f"  Students passing: {np.sum(scores >= 50)}")
print(f"  Students failing: {np.sum(scores < 50)}")
```

---

### Optional Extension Challenges

- Add a **grade letter** (A, B, C, D, F) to each score using `np.where()` conditions
- Generate a second class of 12 students and compare the two class averages
- Find students who scored within 5 points of the class average (use `np.where(np.abs(scores - mean) <= 5)`)

---

## Common Beginner Mistakes

### Mistake 1 — Using `np.split()` Instead of `np.array_split()`

```python
# WRONG - this will crash if division is unequal
arr = np.array([1, 2, 3, 4, 5])
# np.split(arr, 3)  # ValueError! 5 cannot be split into 3 equal parts

# RIGHT - this adjusts automatically
result = np.array_split(arr, 3)   # Works fine: [1,2], [3,4], [5]
```

---

### Mistake 2 — Forgetting That `where()` Returns a Tuple

```python
import numpy as np
arr = np.array([1, 2, 3, 4])

result = np.where(arr > 2)
print(result)        # (array([2, 3]),)  ← it's a tuple!
print(result[0])     # array([2, 3])     ← to get just the array, use [0]
```

---

### Mistake 3 — Assuming `np.sort()` Modifies the Original Array

```python
import numpy as np
arr = np.array([3, 1, 2])

np.sort(arr)       # This does NOT change arr!
print(arr)         # Still [3 1 2] ← ORIGINAL UNCHANGED

sorted_arr = np.sort(arr)   # You must capture the result in a variable
print(sorted_arr)  # [1 2 3]
```

---

### Mistake 4 — Building Filter Lists Manually When You Can Use Direct Conditions

```python
import numpy as np
arr = np.array([10, 20, 30, 40, 50])

# SLOW and unnecessary
filter_arr = []
for element in arr:
    if element > 25:
        filter_arr.append(True)
    else:
        filter_arr.append(False)
result = arr[filter_arr]

# FAST and Pythonic - do this instead!
result = arr[arr > 25]     # One line, faster, cleaner
print(result)              # [30 40 50]
```

---

### Mistake 5 — Using `searchsorted()` on an Unsorted Array

```python
import numpy as np

# WRONG - array is not sorted!
arr = np.array([5, 2, 8, 1, 9])
# np.searchsorted(arr, 6)  # The result would be meaningless!

# RIGHT - sort first
arr_sorted = np.sort(arr)       # [1 2 5 8 9]
position = np.searchsorted(arr_sorted, 6)
print(position)                  # 3 (insert 6 between 5 and 8)
```

---

### Mistake 6 — Confusing `randint()` and `rand()`

```python
from numpy import random

# randint → random INTEGERS
x = random.randint(10)         # One integer from 0 to 9
y = random.randint(10, size=5) # Five integers from 0 to 9

# rand → random FLOATS between 0.0 and 1.0
a = random.rand()              # One float
b = random.rand(5)             # Five floats
```

---

## Reflection Questions

Think about these questions after completing the lesson. Writing down your answers will help lock in your understanding.

1. What is the difference between `np.split()` and `np.array_split()`? When would you choose one over the other?

2. `np.where()` returns a **tuple**. Why do you think NumPy wraps the result in a tuple? (Hint: think about 2-D arrays — you might need both row and column indices.)

3. Does `np.sort()` change the original array? How is this different from Python's built-in `list.sort()` method?

4. You have an array of 1,000 prices. Write (in plain English, no code needed) the steps you would take to find all prices above the average price.

5. When would you want to use `random.seed()` before generating random numbers? When would you NOT want to use it?

6. Imagine you have a sorted array of employees' ages. You want to find where a new employee aged 34 should be placed. Which NumPy function would you use?

---

## Completion Checklist

Check off each item as you complete it:

- [ ] I can split a 1-D array into equal parts using `np.array_split()`
- [ ] I understand what happens when the array cannot be divided equally
- [ ] I can access individual pieces from a split result using list indexing
- [ ] I can split a 2-D array along rows (default) and along columns (`axis=1`)
- [ ] I can use `np.where()` to find index positions of matching elements
- [ ] I understand that `np.where()` returns a tuple
- [ ] I can use the modulo operator `%` to test even/odd conditions
- [ ] I understand what `searchsorted()` does and why the array must be sorted first
- [ ] I can sort a 1-D array in ascending and descending order
- [ ] I know that `np.sort()` returns a copy without changing the original
- [ ] I can sort strings and booleans
- [ ] I can create a boolean filter array manually and with a direct condition
- [ ] I can use direct array conditions for one-line filtering
- [ ] I can generate random integers with `random.randint()`
- [ ] I can generate random floats with `random.rand()`
- [ ] I can generate 1-D and 2-D random arrays
- [ ] I can pick random values from a custom array with `random.choice()`
- [ ] I completed all 5 practice exercises
- [ ] I completed the mini project
- [ ] I understand at least 5 of the common beginner mistakes

---

## Lesson Summary

In this lesson, you mastered five core NumPy array operations:

**Splitting** — `np.array_split(arr, n)` breaks one array into `n` smaller arrays. It handles unequal splits gracefully, unlike the stricter `np.split()`. For 2-D arrays, `axis=1` splits along columns; `np.hsplit()` is the horizontal splitting shortcut.

**Searching** — `np.where(condition)` returns the index positions where elements satisfy a condition. It returns a tuple, so use `result[0]` to get the raw index array. `np.searchsorted(sorted_arr, value)` efficiently finds where to insert a value to maintain sort order — very fast due to binary search. Use `side='right'` to get the rightmost valid position.

**Sorting** — `np.sort(arr)` returns a **new sorted copy** without modifying the original. It sorts numbers, strings, and booleans. For descending order, append `[::-1]`. For 2-D arrays, each row is sorted independently by default.

**Filtering** — You can filter arrays using a boolean index list. Building this list manually with a loop works, but the NumPy shortcut — writing the condition directly on the array (e.g., `arr[arr > 50]`) — is far more concise and efficient. This vectorised approach is central to professional data science.

**Random Numbers** — `np.random` provides `randint(n)` for random integers, `rand()` for random floats between 0 and 1, and `choice(arr)` for random picks from a custom list. All functions accept `size=(rows, cols)` to generate multi-dimensional arrays. Use `random.seed(n)` for reproducible results during testing.

Together, these five tools allow you to manipulate, interrogate, and generate data efficiently — skills that form the backbone of data science, machine learning, scientific computing, and software engineering.
