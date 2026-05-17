---
render_with_liquid: false
title: "Introduction to NumPy: Arrays, Indexing, and Slicing"
nav_order: 24
---

# Lesson 24 — Introduction to NumPy: Arrays, Indexing, and Slicing

---

## Lesson Introduction

Welcome to one of the most important lessons in data science and scientific computing with Python! In this lesson, you will learn about **NumPy** — a powerful Python library that makes working with numbers and collections of data fast, easy, and incredibly efficient.

By the end of this lesson you will:

- Understand what NumPy is and why it exists
- Install NumPy and import it correctly into your Python programs
- Create NumPy arrays of different shapes and dimensions
- Access individual elements in arrays using **indexing**
- Extract portions of arrays using **slicing**
- Apply all of this to realistic data scenarios

You do **not** need any prior NumPy experience. If you know basic Python (variables, lists, `print()`), you are ready to go.

---

## Prerequisite Concepts

Before we dive in, let's quickly review the concepts you should already know. If any of these feel unfamiliar, take a moment to review them.

### Python Lists

A Python list is an ordered collection of values you can create with square brackets:

```python
my_list = [10, 20, 30, 40, 50]
print(my_list[0])   # Access first element
```

**Expected Output:**
```
10
```

Lists store multiple values in one variable. NumPy arrays do something similar — but much faster and with far more powerful tools built in.

### Python `import` Keyword

When you want to use a tool (library) in Python that isn't built in, you first need to **import** it:

```python
import math          # imports the math module
print(math.sqrt(16)) # uses a function from that module
```

**Expected Output:**
```
4.0
```

You'll use `import` the same way to bring NumPy into your program.

### Python `type()` Function

The built-in `type()` function tells you what kind of object a value is:

```python
x = [1, 2, 3]
print(type(x))
```

**Expected Output:**
```
<class 'list'>
```

You'll use this with NumPy to confirm that your arrays are the correct type.

---

## Part 1 — What Is NumPy?

### The Problem NumPy Solves

Imagine you are a scientist tracking daily temperatures across 10,000 weather stations over a full year. That is 3,650,000 individual numbers you need to store, process, and analyze.

If you used a regular Python list, Python would store those numbers in scattered locations in your computer's memory — like books randomly placed across a huge library. To find one book (value), it has to search everywhere. This is **slow**.

NumPy solves this by storing all values in one continuous block of memory — like books neatly lined up on a single shelf. Your computer can find, read, and process them incredibly quickly.

> **Analogy:** A Python list is like a collection of sticky notes scattered on a wall. A NumPy array is like a printed table — organized, compact, and fast to scan.

### What Is NumPy Exactly?

**NumPy** stands for **Numerical Python**. It is a Python library created in 2005 by Travis Oliphant. It is open source, meaning anyone can use it for free.

NumPy's main features:

- Provides a powerful **array object** called `ndarray` (n-dimensional array)
- Supports up to **50× faster** processing than regular Python lists
- Includes tools for linear algebra, Fourier transforms, and matrix math
- Is the foundation for many other data science libraries like Pandas, Matplotlib, and SciPy

### Why Is NumPy Faster?

NumPy arrays are stored in **one continuous place in memory**. Computer scientists call this **locality of reference**. When values sit next to each other in memory, the processor can grab them in large batches at once — like picking up a whole tray of items instead of picking one item at a time.

Additionally, the performance-critical parts of NumPy are written in **C and C++**, which are much faster than pure Python.

> **Real-world relevance:** NumPy is used in data analysis, machine learning, image processing, financial modeling, engineering simulations, and scientific research. Learning it opens the door to all these fields.

---

## Part 2 — Getting Started with NumPy

### Step 1: Installing NumPy

If you have Python and PIP already installed, open your terminal or command prompt and type:

```
pip install numpy
```

If you are using a tool like **Anaconda**, **Jupyter Notebook**, or **Google Colab**, NumPy is usually already installed and ready to use.

To check if NumPy installed correctly, type this in Python:

```python
import numpy as np
print(np.__version__)
```

**Expected Output (version number may vary):**
```
1.26.4
```

If you see a version number — congratulations, NumPy is ready!

### Step 2: Importing NumPy

There are two ways to import NumPy.

**Option 1 — Full name:**

```python
import numpy

arr = numpy.array([1, 2, 3])
print(arr)
```

**Expected Output:**
```
[1 2 3]
```

**Option 2 — Short alias `np` (this is the standard way):**

```python
import numpy as np

arr = np.array([1, 2, 3])
print(arr)
```

**Expected Output:**
```
[1 2 3]
```

The `as np` part gives NumPy a **nickname** (alias) so you can write `np.array(...)` instead of `numpy.array(...)` every time. Every NumPy programmer uses this convention — you will see `import numpy as np` in virtually every data science project in the world.

> **Think of it this way:** Instead of saying "Can you pass me the Worcestershire sauce?" every time, you just call it "the sauce." `np` is NumPy's nickname.

### Checking Your NumPy Version

The version is stored in a special attribute called `__version__` (note the double underscores on both sides):

```python
import numpy as np
print(np.__version__)
```

**Expected Output:**
```
1.26.4
```

> **Why check the version?** Some features only work in newer versions. When following tutorials online, knowing your version helps you avoid confusion.

---

## Part 3 — Creating NumPy Arrays

### What Is an `ndarray`?

The core object in NumPy is called **`ndarray`**, which stands for **n-dimensional array**. This is the container that holds your data.

Think of an `ndarray` like:
- A **1D array** = a single row of numbers (like a list)
- A **2D array** = a table with rows and columns (like a spreadsheet)
- A **3D array** = a cube of data (like multiple spreadsheets stacked on top)

You create an `ndarray` using the `np.array()` function.

### Creating Your First Array

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5])

print(arr)
print(type(arr))
```

**Line-by-line explanation:**
- `import numpy as np` — loads NumPy with alias `np`
- `np.array([1, 2, 3, 4, 5])` — passes a Python list to NumPy, which converts it into an `ndarray`
- `print(arr)` — prints the array values
- `print(type(arr))` — prints the type of the object

**Expected Output:**
```
[1 2 3 4 5]
<class 'numpy.ndarray'>
```

Notice: NumPy arrays are printed **without commas** between values — that's a quick visual sign you're looking at a NumPy array, not a Python list.

### Creating an Array from a Tuple

You can also pass a **tuple** (values in round brackets) to `np.array()`:

```python
import numpy as np

arr = np.array((10, 20, 30, 40, 50))
print(arr)
```

**Expected Output:**
```
[10 20 30 40 50]
```

NumPy accepts lists, tuples, or any sequence-like object and converts it into an `ndarray`.

> **Thinking prompt:** What do you think happens if you pass a list of strings like `["a", "b", "c"]` to `np.array()`? Try it!

---

## Part 4 — Dimensions in Arrays

### What Is a Dimension?

A **dimension** in an array is one level of depth. Think of it like nesting:
- No nesting = 0 dimensions (a single number)
- One level = 1 dimension (a flat list of numbers)
- Two levels = 2 dimensions (a table / grid)
- Three levels = 3 dimensions (a cube / stacked tables)

### 0-D Arrays (Scalars)

A **0-D array** is a single value — no list, no nesting. These are sometimes called **scalars**.

```python
import numpy as np

arr = np.array(42)
print(arr)
```

**Expected Output:**
```
42
```

You rarely create 0-D arrays directly, but you encounter them often as results of NumPy operations (like averaging a list of numbers).

### 1-D Arrays

A **1-D array** contains a flat sequence of values. This is the most common type for beginners.

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5])
print(arr)
```

**Expected Output:**
```
[1 2 3 4 5]
```

Real-world use: A 1-D array might hold a week's worth of daily temperatures: `[28, 31, 29, 33, 27, 25, 30]`.

### 2-D Arrays

A **2-D array** is like a table or spreadsheet — it has **rows** and **columns**. You create it by passing a list of lists:

```python
import numpy as np

arr = np.array([[1, 2, 3], [4, 5, 6]])
print(arr)
```

**Expected Output:**
```
[[1 2 3]
 [4 5 6]]
```

**How to read this:** The outer list `[..., ...]` contains two inner lists (the rows). Each inner list has 3 numbers (the columns).

Real-world use: A 2-D array might hold a grade book — rows = students, columns = test scores.

```
Student 1: [85, 90, 78]
Student 2: [92, 88, 95]
```

### 3-D Arrays

A **3-D array** is a list of 2-D arrays — imagine stacking multiple tables on top of each other:

```python
import numpy as np

arr = np.array([[[1, 2, 3], [4, 5, 6]], [[7, 8, 9], [10, 11, 12]]])
print(arr)
```

**Expected Output:**
```
[[[ 1  2  3]
  [ 4  5  6]]

 [[ 7  8  9]
  [10 11 12]]]
```

Real-world use: 3-D arrays are used in image processing (height × width × colour channels), video data, medical scans, and neural networks.

### Checking the Number of Dimensions with `.ndim`

NumPy arrays have a built-in attribute called `.ndim` that tells you how many dimensions an array has:

```python
import numpy as np

a = np.array(42)
b = np.array([1, 2, 3, 4, 5])
c = np.array([[1, 2, 3], [4, 5, 6]])
d = np.array([[[1, 2, 3], [4, 5, 6]], [[1, 2, 3], [4, 5, 6]]])

print(a.ndim)
print(b.ndim)
print(c.ndim)
print(d.ndim)
```

**Expected Output:**
```
0
1
2
3
```

**What does `.ndim` mean?** The dot (`.`) accesses a property that belongs to the array object. Just like `name.upper()` is a method of a string, `.ndim` is a property of an `ndarray`.

### Creating Higher-Dimensional Arrays with `ndmin`

You can force an array to have a specific minimum number of dimensions using the `ndmin` argument:

```python
import numpy as np

arr = np.array([1, 2, 3, 4], ndmin=5)
print(arr)
print('Number of dimensions:', arr.ndim)
```

**Expected Output:**
```
[[[[[1 2 3 4]]]]]
Number of dimensions: 5
```

**What happened?** We told NumPy: "I want at least 5 dimensions." NumPy wrapped our 4 values in layer after layer of brackets until 5 dimensions were reached. The actual values `[1 2 3 4]` sit in the innermost (5th) dimension.

---

## Part 5 — Array Indexing: Accessing Individual Elements

### What Is Indexing?

**Indexing** means accessing a single specific element from an array by its **position number** (called its index).

In NumPy (and Python), indexing always starts at **0** — not 1. This trips up many beginners, so let's make it crystal clear:

```
Array:   [10, 20, 30, 40, 50]
Index:     0   1   2   3   4
```

The first element is at index `0`. The second is at index `1`. And so on.

> **Analogy:** Think of a bus with numbered seats starting at seat 0. The driver's seat is seat 0, the first passenger seat is seat 1, etc.

### Indexing a 1-D Array

You access an element by putting its index number in square brackets `[index]`:

```python
import numpy as np

arr = np.array([1, 2, 3, 4])
print(arr[0])   # First element
```

**Expected Output:**
```
1
```

```python
import numpy as np

arr = np.array([1, 2, 3, 4])
print(arr[1])   # Second element
```

**Expected Output:**
```
2
```

You can also use indexed values in calculations:

```python
import numpy as np

arr = np.array([1, 2, 3, 4])
print(arr[2] + arr[3])   # Add the 3rd and 4th elements
```

**Expected Output:**
```
7
```

**How it works:** `arr[2]` returns `3`, and `arr[3]` returns `4`. Python then adds them: `3 + 4 = 7`.

### Indexing a 2-D Array

A 2-D array is like a table with rows and columns. To access an element you need **two index numbers** separated by a comma: `arr[row, column]`.

```
arr = [[1,  2,  3,  4,  5],
       [6,  7,  8,  9, 10]]

Row 0:  1  2  3  4  5   (indices 0–4)
Row 1:  6  7  8  9  10  (indices 0–4)
```

**Example — access row 0, column 1 (value = 2):**

```python
import numpy as np

arr = np.array([[1, 2, 3, 4, 5], [6, 7, 8, 9, 10]])
print('2nd element on 1st row:', arr[0, 1])
```

**Expected Output:**
```
2nd element on 1st row: 2
```

**Example — access row 1, column 4 (value = 10):**

```python
import numpy as np

arr = np.array([[1, 2, 3, 4, 5], [6, 7, 8, 9, 10]])
print('5th element on 2nd row:', arr[1, 4])
```

**Expected Output:**
```
5th element on 2nd row: 10
```

> **Thinking prompt:** What does `arr[0, 0]` return? What about `arr[1, 0]`? Try to predict before running the code.

### Indexing a 3-D Array

For 3-D arrays, you need **three index numbers**: `arr[depth, row, column]`.

```python
import numpy as np

arr = np.array([[[1, 2, 3], [4, 5, 6]], [[7, 8, 9], [10, 11, 12]]])
print(arr[0, 1, 2])
```

**Expected Output:**
```
6
```

**Step-by-step explanation of `arr[0, 1, 2]`:**

1. **First index `0`** — Selects the first 2-D array (the "first table"): `[[1, 2, 3], [4, 5, 6]]`
2. **Second index `1`** — Selects the second row from that table: `[4, 5, 6]`
3. **Third index `2`** — Selects the third element from that row: `6`

Result: `6` ✓

### Negative Indexing

Negative indexing lets you count **from the end** of the array. Index `-1` is the last element, `-2` is the second-to-last, and so on.

```
Array:  [10, 20, 30, 40, 50]
Index:   -5  -4  -3  -2  -1
```

```python
import numpy as np

arr = np.array([[1, 2, 3, 4, 5], [6, 7, 8, 9, 10]])
print('Last element from 2nd row:', arr[1, -1])
```

**Expected Output:**
```
Last element from 2nd row: 10
```

**Why use negative indexing?** When you don't know exactly how long an array is, `-1` always safely gives you the last element — no matter the length. This is very handy in real programs.

---

## Part 6 — Array Slicing: Extracting Portions of Arrays

### What Is Slicing?

**Slicing** means extracting a **range** (portion) of elements from an array — not just one element, but multiple elements in a sequence.

While indexing gives you one item (`arr[2]`), slicing gives you a **sub-array** (`arr[1:5]`).

> **Analogy:** Indexing is like pulling one book off a shelf. Slicing is like grabbing a whole section of books between shelf markers.

### The Slice Syntax

The syntax for slicing is:

```
arr[start:end]
arr[start:end:step]
```

**Rules:**
- `start` is the index where the slice **begins** (included)
- `end` is the index where the slice **stops** (NOT included — this is crucial!)
- `step` is how many positions to jump between each selected element (default is `1`)

If you leave out `start`, Python assumes `0` (beginning).
If you leave out `end`, Python assumes the end of the array.
If you leave out `step`, Python assumes `1` (every element).

### Basic Slicing Examples

**Example 1 — Slice from index 1 to index 5:**

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6, 7])
print(arr[1:5])
```

**Expected Output:**
```
[2 3 4 5]
```

**Why not `6`?** Because the end index `5` is **excluded**. The slice includes indices 1, 2, 3, and 4 — giving values `2, 3, 4, 5`.

**Example 2 — Slice from index 4 to the end:**

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6, 7])
print(arr[4:])
```

**Expected Output:**
```
[5 6 7]
```

Leaving out the `end` means "go all the way to the last element."

**Example 3 — Slice from beginning to index 4 (not included):**

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6, 7])
print(arr[:4])
```

**Expected Output:**
```
[1 2 3 4]
```

Leaving out the `start` means "begin from the very first element."

### Negative Slicing

Just like negative indexing, you can use negative numbers in a slice to count from the end:

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6, 7])
print(arr[-3:-1])
```

**Expected Output:**
```
[5 6]
```

**How to read `arr[-3:-1]`:**
- `-3` = third from the end = index 4 = value `5`
- `-1` = last element (excluded) = index 6 = value `7`
- So we get elements at positions -3 and -2: values `5` and `6`

### Using Step in Slicing

The `step` value controls the "jump" between selected elements.

**Example — every other element from index 1 to index 5:**

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6, 7])
print(arr[1:5:2])
```

**Expected Output:**
```
[2 4]
```

**How it works:** Starting at index 1 (value `2`), jump by 2 each time. Next is index 3 (value `4`). Index 5 is excluded, so we stop.

**Example — every other element from the entire array:**

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6, 7])
print(arr[::2])
```

**Expected Output:**
```
[1 3 5 7]
```

`arr[::2]` means: start from the beginning, go to the end, jump by 2 each time. So it picks indices 0, 2, 4, 6 → values 1, 3, 5, 7.

> **Thinking prompt:** What would `arr[::3]` give you? What about `arr[6:0:-1]`? Predict the outputs, then try them.

### Slicing 2-D Arrays

For 2-D arrays, you can slice both rows and columns using comma-separated slices:

```
arr[row_slice, column_slice]
```

**Example 1 — From row 1 (second row), get columns 1 to 3 (not including 4):**

```python
import numpy as np

arr = np.array([[1, 2, 3, 4, 5], [6, 7, 8, 9, 10]])
print(arr[1, 1:4])
```

**Expected Output:**
```
[7 8 9]
```

**Breakdown:**
- `arr[1, ...]` selects the second row: `[6, 7, 8, 9, 10]`
- `..., 1:4]` slices columns 1, 2, 3 (not 4): `7, 8, 9`

**Example 2 — From both rows, get only column index 2:**

```python
import numpy as np

arr = np.array([[1, 2, 3, 4, 5], [6, 7, 8, 9, 10]])
print(arr[0:2, 2])
```

**Expected Output:**
```
[3 8]
```

**Breakdown:**
- `0:2` selects both rows (indices 0 and 1)
- `2` selects only column 2
- Row 0, col 2 = `3`; Row 1, col 2 = `8` → result: `[3, 8]`

**Example 3 — Slice both rows AND columns to get a 2-D sub-array:**

```python
import numpy as np

arr = np.array([[1, 2, 3, 4, 5], [6, 7, 8, 9, 10]])
print(arr[0:2, 1:4])
```

**Expected Output:**
```
[[2 3 4]
 [7 8 9]]
```

**Breakdown:**
- `0:2` → both rows
- `1:4` → columns 1, 2, 3 (not 4)
- Row 0: columns 1,2,3 → `2, 3, 4`
- Row 1: columns 1,2,3 → `7, 8, 9`
- Result is a 2-D array: `[[2 3 4], [7 8 9]]`

---

## Guided Practice Exercises

### Exercise 1 — Warm-Up: Building Your First Arrays

**Objective:** Create arrays of different dimensions and inspect them.

**Scenario:** You are a data analyst tracking exam scores at a school.

**Steps:**

1. Create a 1-D array called `scores` containing: `72, 85, 90, 68, 77, 95, 88`
2. Print the array
3. Print its type using `type()`
4. Print how many dimensions it has using `.ndim`

```python
import numpy as np

scores = np.array([72, 85, 90, 68, 77, 95, 88])
print(scores)
print(type(scores))
print(scores.ndim)
```

**Expected Output:**
```
[72 85 90 68 77 95 88]
<class 'numpy.ndarray'>
1
```

**Self-check Questions:**
- Why is the type `numpy.ndarray` and not `list`?
- What would change if you added another list inside to make it 2-D?

---

### Exercise 2 — Indexing Practice

**Objective:** Access specific elements from a 1-D and 2-D array.

**Scenario:** You have a temperature dataset for 7 days and a 2-row table of grades for two students.

```python
import numpy as np

# Daily temperatures
temps = np.array([28, 31, 29, 33, 27, 25, 30])

# Student grades: student 1 and student 2 across 3 subjects
grades = np.array([[85, 90, 78], [92, 88, 95]])

# Task 1: Print the temperature on day 3 (Wednesday)
print("Wednesday temperature:", temps[2])

# Task 2: Print the last temperature using negative indexing
print("Sunday temperature:", temps[-1])

# Task 3: Print student 2's score in subject 3 (last subject)
print("Student 2, Subject 3:", grades[1, 2])

# Task 4: Print student 1's score in subject 1
print("Student 1, Subject 1:", grades[0, 0])
```

**Expected Output:**
```
Wednesday temperature: 29
Sunday temperature: 30
Student 2, Subject 3: 95
Student 1, Subject 1: 85
```

**Optional what-if challenge:** Change `grades[1, 2]` to `grades[1, -1]`. Do you get the same result? Why?

---

### Exercise 3 — Slicing Practice

**Objective:** Extract meaningful portions of arrays using slicing.

**Scenario:** You have daily sales data for 2 weeks (14 days) and need to extract different time periods.

```python
import numpy as np

sales = np.array([150, 200, 175, 220, 190, 160, 210,
                  180, 230, 165, 195, 215, 185, 240])

# Task 1: Get sales for the first week (days 0–6)
print("Week 1 sales:", sales[:7])

# Task 2: Get sales for the second week (days 7–13)
print("Week 2 sales:", sales[7:])

# Task 3: Get sales from day 3 to day 7 (not including day 7)
print("Days 3-6 sales:", sales[3:7])

# Task 4: Get every other day's sales from the full 2 weeks
print("Every other day:", sales[::2])

# Task 5: Get the last 3 days using negative slicing
print("Last 3 days:", sales[-3:])
```

**Expected Output:**
```
Week 1 sales: [150 200 175 220 190 160 210]
Week 2 sales: [180 230 165 195 215 185 240]
Days 3-6 sales: [220 190 160 210]
Every other day: [150 175 190 210 230 195 185]
Last 3 days: [215 185 240]
```

---

## Mini Project — Student Performance Tracker

### Project Goal

Build a small NumPy-based student performance tracker that stores and analyses exam results using arrays, indexing, and slicing.

### Setup — Create the Data

We have 3 students, each with scores in 4 subjects (Maths, English, Science, History):

```python
import numpy as np

# 2-D array: rows = students, columns = subjects
# Subjects: Maths, English, Science, History
performance = np.array([
    [78, 85, 90, 72],   # Student 1
    [92, 88, 76, 95],   # Student 2
    [65, 70, 88, 80]    # Student 3
])

print("Full performance table:")
print(performance)
print("Dimensions:", performance.ndim)
```

**Expected Output:**
```
Full performance table:
[[78 85 90 72]
 [92 88 76 95]
 [65 70 88 80]]
Dimensions: 2
```

### Stage 1 — Access Individual Scores

```python
# Student 2's Science score (row 1, column 2)
print("Student 2's Science score:", performance[1, 2])

# Student 3's History score (last student, last subject)
print("Student 3's History score:", performance[-1, -1])
```

**Expected Output:**
```
Student 2's Science score: 76
Student 3's History score: 80
```

### Stage 2 — Extract Specific Data with Slicing

```python
# All scores for Student 1 (first row, all columns)
print("Student 1's all scores:", performance[0, :])

# All students' Maths scores (all rows, first column)
print("All Maths scores:", performance[:, 0])

# Scores for students 1 and 2 in first two subjects
print("Top 2 students, first 2 subjects:")
print(performance[0:2, 0:2])
```

**Expected Output:**
```
Student 1's all scores: [78 85 90 72]
All Maths scores: [78 92 65]
Top 2 students, first 2 subjects:
[[78 85]
 [92 88]]
```

### Stage 3 — Milestone Reflection

At this point, you have:
- Stored multi-student data in a 2-D array
- Retrieved individual scores using `[row, col]` indexing
- Extracted entire rows (single student's data)
- Extracted entire columns (all students' score in one subject)
- Sliced sub-sections of the table

**Reflection questions:**
- How would you add a 4th student? (Hint: you'd need a new row)
- How would you get only Science and History scores for all students? (Hint: `performance[:, 2:4]`)

### Stage 4 — Extended Exploration

```python
# All students' last two subjects (History and Science)
print("Science and History for all students:")
print(performance[:, 2:4])

# Every other student's English score
print("Every other student's English:", performance[::2, 1])
```

**Expected Output:**
```
Science and History for all students:
[[90 72]
 [76 95]
 [88 80]]
Every other student's English: [85 70]
```

---

## Common Beginner Mistakes

### Mistake 1 — Forgetting That Indexing Starts at 0

**Wrong thinking:** "The first element is at index 1."

```python
import numpy as np
arr = np.array([10, 20, 30])
print(arr[1])   # Beginner thinks this gives 10
```

**Actual Output:**
```
20
```

**Corrected thinking:** Index 0 = first element, index 1 = second element.

```python
print(arr[0])   # Correct: this gives 10
```

---

### Mistake 2 — Forgetting the Slice End is Excluded

**Wrong:** "I want elements at positions 2, 3, and 4, so I write `arr[2:4]`."

```python
import numpy as np
arr = np.array([10, 20, 30, 40, 50])
print(arr[2:4])
```

**Actual Output:**
```
[30 40]
```

Only positions 2 and 3 are included — **not** 4. To include position 4, write `arr[2:5]`.

---

### Mistake 3 — Using List Syntax for 2-D Indexing

**Wrong:**
```python
arr[0][1]   # Python-list style — works, but not preferred
```

**Preferred NumPy style:**
```python
arr[0, 1]   # Cleaner and faster
```

Both technically work, but `arr[0, 1]` is the proper NumPy way and is more efficient.

---

### Mistake 4 — Confusing Dimensions

**Wrong:** Creating a 1-D array when you meant a 2-D array:

```python
import numpy as np
arr = np.array([1, 2, 3, 4, 5, 6])   # This is 1-D with 6 elements
print(arr.ndim)
```

**Output:**
```
1
```

**Correct for a 2×3 table:**
```python
arr = np.array([[1, 2, 3], [4, 5, 6]])   # This is 2-D: 2 rows, 3 columns
print(arr.ndim)
```

**Output:**
```
2
```

---

### Mistake 5 — Forgetting Commas Between Inner Lists in 2-D Arrays

**Wrong:**
```python
arr = np.array([[1, 2, 3] [4, 5, 6]])   # Missing comma between the two lists!
```

This will cause a `TypeError`. Always separate inner lists with commas:

**Correct:**
```python
arr = np.array([[1, 2, 3], [4, 5, 6]])
```

---

## Reflection Questions

Take a few minutes to think about these questions. Try to answer them in your own words before checking back in the lesson:

1. Why is NumPy significantly faster than a regular Python list for numerical operations?
2. If an array has the values `[100, 200, 300, 400, 500]`, what is the index of `300`? What about its negative index?
3. What does `arr[2:6]` return for an array of 10 elements? Which elements are included?
4. A 2-D array has 4 rows and 6 columns. How would you access the element in the 3rd row and 5th column?
5. What is the difference between `arr[3]` and `arr[3:4]`? Why would each be useful?
6. If you use `arr[-1]` on a 1-D array, what do you get? What about `arr[-3:]`?
7. You are building a data analysis tool for a hospital tracking 10 patients' heart rates over 7 days. What shape of NumPy array would you use to store all this data?

---

## Completion Checklist

Before moving to the next lesson, make sure you can confidently say yes to each item:

- [ ] I understand what NumPy is and why it is faster than Python lists
- [ ] I can install NumPy using `pip install numpy`
- [ ] I can import NumPy with the standard alias `import numpy as np`
- [ ] I know how to check the NumPy version with `np.__version__`
- [ ] I can create a NumPy array using `np.array()`
- [ ] I can create arrays from both lists and tuples
- [ ] I understand what 0-D, 1-D, 2-D, and 3-D arrays are
- [ ] I can use `.ndim` to check the number of dimensions
- [ ] I can create higher-dimensional arrays using the `ndmin` argument
- [ ] I can access a 1-D array element using `arr[index]`
- [ ] I can access a 2-D array element using `arr[row, col]`
- [ ] I can access a 3-D array element using `arr[depth, row, col]`
- [ ] I understand that indexing starts at `0`, not `1`
- [ ] I can use negative indices to count from the end
- [ ] I can slice a 1-D array with `arr[start:end]`
- [ ] I understand that the end index in a slice is **excluded**
- [ ] I can use the step parameter in slicing: `arr[start:end:step]`
- [ ] I can use negative slicing
- [ ] I can slice a 2-D array to get rows, columns, or sub-tables
- [ ] I have identified and understood all 5 common beginner mistakes

---

## Lesson Summary

Congratulations on completing Lesson 24! Here is what you have learned:

**NumPy Fundamentals:**
NumPy (Numerical Python) is an open-source Python library designed for fast numerical computing. Its core object, the `ndarray`, stores data in a single continuous block of memory, making it up to 50× faster than regular Python lists. The performance-critical code is written in C/C++.

**Installing and Importing:**
NumPy is installed with `pip install numpy` and imported using the universal convention `import numpy as np`. You can verify the installation by printing `np.__version__`.

**Creating Arrays:**
Arrays are created with `np.array()`, which accepts lists, tuples, or any sequence. Arrays can have 0, 1, 2, 3, or any number of dimensions. The `.ndim` attribute reveals the number of dimensions, and the `ndmin` argument forces a minimum number.

**Indexing:**
Individual elements are accessed with square brackets using their index position, starting from `0`. 2-D arrays use `arr[row, col]` notation. Negative indices count from the end (`-1` = last element).

**Slicing:**
Slicing extracts ranges of elements using `arr[start:end]` or `arr[start:end:step]`. The start index is included, but the end index is excluded. Step controls the jump between elements. 2-D arrays can be sliced in both dimensions simultaneously.

**Real-World Relevance:**
NumPy is the foundation of the entire Python data science ecosystem. It is used in machine learning (TensorFlow, scikit-learn), data analysis (Pandas), visualisation (Matplotlib), scientific computing (SciPy), and image processing. Mastering NumPy arrays, indexing, and slicing is your first step toward all of these powerful tools.

> **Next Steps:** In the following lessons, you will explore NumPy data types, the difference between array copies and views, array reshaping, and mathematical operations — building on everything you have learned here.
