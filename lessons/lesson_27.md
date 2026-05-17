---
render_with_liquid: false
title: "NumPy Random Distributions, Permutations, Seaborn Visualisation, and Universal Functions (ufuncs)"
nav_order: 27
---

# Lesson 27 — NumPy Random Distributions, Permutations, Seaborn Visualisation, and Universal Functions (ufuncs)

---

## Lesson Introduction

Welcome to Lesson 27! In this lesson you will learn four powerful ideas that sit at the heart of modern data science and scientific computing in Python:

1. **Random Data Distributions** — how to generate random numbers that follow real-world patterns (like weighted choices and probability rules).
2. **Random Permutations** — how to shuffle arrays or create new rearrangements without changing the original data.
3. **Seaborn for Visualisation** — how to draw beautiful distribution charts using a Python library called Seaborn, so you can *see* what your data looks like.
4. **Universal Functions (ufuncs)** — NumPy's super-fast way of doing math operations on entire arrays at once without writing slow loops.

These four topics flow naturally into each other. First you will learn to *create* specially shaped random data, then to *rearrange* it, then to *visualise* it, and finally to *process* it efficiently with ufuncs. By the end of this lesson you will have everything you need for a real mini-project.

> **Prerequisites check:** This lesson assumes you have already used NumPy and know how to create arrays with `np.array()`. If you have not, quickly review: `import numpy as np` and `arr = np.array([1, 2, 3])` before continuing.

---

## Prerequisite Concepts

### What is a Python Array (NumPy ndarray)?

Before we start, a very quick reminder. In NumPy, data is stored in an **ndarray** (n-dimensional array). Think of it as a super-powered list that can hold numbers very efficiently.

```python
import numpy as np

arr = np.array([10, 20, 30, 40])
print(arr)
```

**Expected Output:**
```
[10 20 30 40]
```

### What is a Python List?

A Python list is the built-in container: `[1, 2, 3]`. NumPy arrays and Python lists look similar but NumPy arrays are far faster for maths operations. You will see both used in this lesson.

### What is a Library Import?

When you write `from numpy import random`, you are saying: "Go into the NumPy toolkit and bring out the *random* tool so I can use it directly." Instead of typing `numpy.random.choice()` every time, you just type `random.choice()`.

---

## Part 1 — Random Data Distribution

### What is a Data Distribution?

Imagine a bag of coloured marbles. You reach in and pull one out. A **data distribution** tells you the complete story of the bag: how many of each colour exist, and therefore how likely you are to pull each one.

In statistics and data science, a **data distribution** is a description of all the possible values a variable can take, and how often each value appears.

> **Real-world analogy:** Think about a school canteen that sells only four snacks: biscuits, chips, juice, and water. If you ask 100 students what they bought, maybe 10 bought biscuits, 30 bought chips, 60 bought juice, and 0 bought water. *That pattern — 10%, 30%, 60%, 0%* — is the distribution of purchases.

### What is Probability?

**Probability** is just a fancy word for "how likely is something to happen?" It is always a number between **0** and **1**:
- **0** means it will *never* happen.
- **1** means it will *always* happen.
- **0.5** means it happens roughly *half* the time.

The probabilities for all possible outcomes must always add up to exactly **1.0** (because something must happen).

### What is a Probability Density Function (PDF)?

A **Probability Density Function** is a mathematical description of a *continuous* distribution — that is, a distribution where the values can be any decimal number, not just whole numbers. It describes the probability of all values in an array or dataset.

> **Simple explanation:** Think of a PDF like a recipe that tells you the "shape" of your data. A bell-curve PDF means most values cluster in the middle. A flat PDF means all values are equally likely.

---

### The `random.choice()` Method

NumPy's `random` module gives us a method called `choice()`. This method lets you:
1. Give it a list of possible values.
2. Tell it exactly how likely each value should be (using probabilities).
3. Ask it to generate as many random picks as you want.

**Syntax breakdown:**
```python
random.choice(values_list, p=probabilities_list, size=how_many_you_want)
```

- `values_list` — the list of values to pick from, e.g. `[3, 5, 7, 9]`
- `p=` — the probability for each value; must be the same length as the values list and must sum to exactly 1.0
- `size=` — how many random values to generate; can be a single number like `(100,)` or a shape like `(3, 5)` for a 2D array

> **Important rule:** The probabilities in the `p` list **must sum to exactly 1.0**. If they don't, Python will raise an error.

---

### Simple Example 1 — Weighted Coin Flip

Let's start with the simplest possible example: a coin that is more likely to land on heads.

```python
from numpy import random

# Our coin: 1 = heads, 0 = tails
# Probability of heads = 0.7, tails = 0.3
result = random.choice([0, 1], p=[0.3, 0.7], size=(10))

print(result)
```

**Expected Output (your output will vary because it is random):**
```
[1 1 0 1 1 1 0 1 1 1]
```

**Line-by-line explanation:**

| Line | What it does |
|------|-------------|
| `from numpy import random` | Imports the random module from NumPy |
| `random.choice([0, 1], ...)` | Tells Python to pick from the values 0 or 1 |
| `p=[0.3, 0.7]` | 0 has a 30% chance; 1 has a 70% chance |
| `size=(10)` | Generate 10 random picks |
| `print(result)` | Show the result |

> **Thinking prompt:** What would happen if you changed `p=[0.3, 0.7]` to `p=[0.0, 1.0]`? Would you ever see a 0? Try it!

---

### Simple Example 2 — Weighted Choice with Four Values

Now let's pick from four possible values with different probabilities, just like the canteen example.

```python
from numpy import random

# Values: 3, 5, 7, 9
# 3 has 10% chance, 5 has 30% chance, 7 has 60% chance, 9 has 0% chance
x = random.choice([3, 5, 7, 9], p=[0.1, 0.3, 0.6, 0.0], size=(100))

print(x)
```

**Expected Output (yours will be different but follow the same pattern):**
```
[7 7 5 7 7 3 7 5 7 7 7 5 7 7 7 7 7 5 7 7 7 5 7 7 7 7 7 5 7 7
 7 5 7 7 7 7 7 7 7 7 7 7 3 7 5 7 7 5 7 5 5 7 7 7 7 5 7 7 7 7
 5 7 7 7 5 5 7 7 7 5 7 7 5 7 7 7 7 7 7 5 7 7 3 5 7 7 5 7 7 7
 7 7 5 7 5 7 7 7 7 7]
```

**Notice:** The value 9 *never* appears because its probability is 0.0. The value 7 appears most often because it has the highest probability (0.6 = 60%).

> **Thinking prompt:** Add up the probabilities: 0.1 + 0.3 + 0.6 + 0.0 = 1.0. They add up to exactly 1. This is always required.

---

### Generating 2D Distribution Arrays

You can also generate the random values as a two-dimensional array (like a grid/table) by passing a **tuple** as the `size` parameter.

```python
from numpy import random

# Same four values, same probabilities, but now get a 3×5 table
x = random.choice([3, 5, 7, 9], p=[0.1, 0.3, 0.6, 0.0], size=(3, 5))

print(x)
```

**Expected Output:**
```
[[7 5 7 7 7]
 [5 7 7 3 7]
 [7 7 5 7 7]]
```

**Line-by-line explanation:**

| Code Part | Meaning |
|-----------|---------|
| `size=(3, 5)` | Create a 2D array with 3 rows and 5 columns |
| The result | A 3×5 table of randomly chosen values (total = 15 values) |

> **Real-world use:** In data science, you might model a weather system where rain (probability 0.4), cloud (0.35), sun (0.2), and storm (0.05) occur across a 10-day, 5-city forecast grid.

---

## Part 2 — Random Permutations

### What is a Permutation?

A **permutation** is simply a rearrangement of the same elements in a different order.

> **Everyday analogy:** Imagine you have three books on your shelf: A, B, C. One arrangement is A-B-C. A permutation could be B-C-A or C-A-B. All three books are still there — they're just in a different order.

Examples of permutations:
- `[1, 2, 3]` is a permutation of `[3, 2, 1]`
- `["apple", "banana", "cherry"]` is a permutation of `["banana", "cherry", "apple"]`

NumPy's `random` module gives us **two methods** for working with permutations:

| Method | What it does | Changes the original array? |
|--------|-------------|----------------------------|
| `shuffle()` | Rearranges the array **in-place** | **YES** — the original is changed |
| `permutation()` | Returns a new rearranged array | **NO** — the original stays the same |

This is an important difference! Let's see both in action.

---

### Method 1: `shuffle()` — Rearrange In-Place

**"In-place"** means the method *directly modifies* the original array. The array you started with gets a new order. Nothing new is created.

```python
from numpy import random
import numpy as np

arr = np.array([1, 2, 3, 4, 5])

print("Before shuffle:", arr)

random.shuffle(arr)

print("After shuffle:", arr)
```

**Expected Output (your shuffle order will vary):**
```
Before shuffle: [1 2 3 4 5]
After shuffle:  [3 1 5 2 4]
```

**Key point:** After calling `shuffle(arr)`, the original `arr` is permanently changed. The values `[1, 2, 3, 4, 5]` are now in a random order.

> **Common beginner mistake:** Assigning the result to a new variable like this:
> ```python
> new_arr = random.shuffle(arr)  # WRONG! new_arr will be None
> ```
> `shuffle()` does NOT return anything. It modifies `arr` directly and returns `None`. Simply call `random.shuffle(arr)` and then use `arr`.

---

### Method 2: `permutation()` — Return a New Arrangement

`permutation()` is the safe option when you want a shuffled copy but need to keep your original data intact.

```python
from numpy import random
import numpy as np

arr = np.array([1, 2, 3, 4, 5])

print("Original arr:", arr)

new_arr = random.permutation(arr)

print("New permutation:", new_arr)
print("Original arr still:", arr)
```

**Expected Output:**
```
Original arr: [1 2 3 4 5]
New permutation: [4 1 3 5 2]
Original arr still: [1 2 3 4 5]
```

**Notice:** `arr` is completely unchanged! The shuffled version is stored in `new_arr`.

> **Real-world use case:** Imagine you have a list of 1000 student names for a quiz draw. You want to shuffle the order for fair selection, but you also want to keep the original alphabetical list intact for your records. Use `permutation()` — not `shuffle()`.

---

### Comparing shuffle() and permutation() Side by Side

```python
from numpy import random
import numpy as np

original = np.array([10, 20, 30, 40, 50])

# --- Using shuffle ---
arr_for_shuffle = original.copy()  # Make a copy first to preserve original
random.shuffle(arr_for_shuffle)
print("After shuffle():     ", arr_for_shuffle)

# --- Using permutation ---
new_version = random.permutation(original)
print("After permutation(): ", new_version)
print("Original unchanged:  ", original)
```

**Expected Output:**
```
After shuffle():      [30 10 50 20 40]
After permutation():  [20 50 10 40 30]
Original unchanged:   [10 20 30 40 50]
```

| Feature | `shuffle()` | `permutation()` |
|---------|-------------|-----------------|
| Modifies original | YES | NO |
| Returns new array | NO (returns None) | YES |
| Safe for original data | Only if you copy first | Always safe |

---

## Part 3 — Seaborn: Visualising Distributions

### Why Do We Need to Visualise?

Numbers alone can be hard to understand. When you generate 1000 random numbers, looking at them as a list tells you very little. A **chart** instantly shows you the shape: Are most values clustered together? Are they spread evenly? Are there extreme values?

This is exactly why data scientists use **visualisation libraries** — tools that turn numbers into charts.

### What is Seaborn?

**Seaborn** is a Python library specifically built for making statistical charts and visualising data distributions beautifully. It sits *on top of* another library called **Matplotlib** — think of Seaborn as the fancy user-friendly wrapper around Matplotlib's more technical engine.

> **Analogy:** Matplotlib is like a professional artist's full studio — powerful but takes time to set up. Seaborn is like a smart automated art assistant that handles all the setup for you.

### Installing Seaborn

Before using Seaborn, you need to install it. Open your terminal/command prompt and run:

```bash
pip install seaborn
```

If you are using **Jupyter Notebook**, run this inside a cell:

```python
!pip install seaborn
```

### What is Matplotlib?

**Matplotlib** is the core plotting library for Python. Seaborn uses it behind the scenes. You need to import both.

```python
import matplotlib.pyplot as plt   # For displaying charts
import seaborn as sns              # For creating distribution charts
```

- `matplotlib.pyplot` is imported as `plt` — a short name by convention
- `seaborn` is imported as `sns` — another short name by convention

---

### What is a Displot?

**Displot** stands for **distribution plot**. It is Seaborn's function for visualising how data is distributed. It takes an array (a list of numbers) and draws a curve showing how the values are spread out.

Think of it like this: if you measured the heights of 1000 people and plotted them, the displot would show a curve peaking around the average height, with fewer and fewer people as you go towards very short or very tall heights.

---

### Simple Example 1 — Basic Displot

```python
import matplotlib.pyplot as plt
import seaborn as sns

# A small list of 6 numbers
sns.displot([0, 1, 2, 3, 4, 5])

plt.show()
```

**What this produces:** A distribution chart with:
- A histogram (vertical bars showing how often each value appears)
- A smooth curve over the bars showing the overall distribution shape

**Line-by-line explanation:**

| Line | Meaning |
|------|---------|
| `import matplotlib.pyplot as plt` | Load the Matplotlib display engine, call it `plt` |
| `import seaborn as sns` | Load Seaborn charting library, call it `sns` |
| `sns.displot([0, 1, 2, 3, 4, 5])` | Create a distribution chart from the list of 6 numbers |
| `plt.show()` | Actually display the chart on screen |

> **Why `plt.show()`?** Seaborn creates the chart in memory, but `plt.show()` is the command that pushes it to your screen. Without it, nothing appears.

---

### Simple Example 2 — Displot Without the Histogram (KDE Only)

Sometimes you want to see only the smooth curve (called a **KDE — Kernel Density Estimate**) without the histogram bars underneath. This is useful when you have a lot of data and just want to see the shape.

```python
import matplotlib.pyplot as plt
import seaborn as sns

# Pass kind="kde" to show only the smooth curve
sns.displot([0, 1, 2, 3, 4, 5], kind="kde")

plt.show()
```

**What this produces:** Only the smooth density curve — no bars.

**What is KDE (Kernel Density Estimate)?**
A KDE is a smooth curve that estimates the probability distribution of your data. Instead of counting exact values in bins (like a histogram), it draws a flowing curve that approximates the shape of the data.

> **Key note:** For the rest of the NumPy tutorial (particularly when visualising random distributions like Normal, Binomial, Poisson, etc.), the standard approach is to use `sns.displot(arr, kind="kde")`.

---

### Practical Example — Visualising a Random Distribution

Now let's combine what we learned in Part 1 with Seaborn to actually *see* a distribution:

```python
from numpy import random
import matplotlib.pyplot as plt
import seaborn as sns

# Generate 1000 random values from our weighted choice
x = random.choice([3, 5, 7, 9], p=[0.1, 0.3, 0.6, 0.0], size=(1000))

# Visualise the distribution
sns.displot(x, kind="kde")
plt.title("Distribution of Weighted Random Choices")
plt.show()
```

**What you will see:** A curve with a large peak around 7 (since it has 60% probability), a smaller bump around 5 (30%), and a tiny presence near 3 (10%). The value 9 will not appear at all.

> **Thinking prompt:** What would the chart look like if all four values had equal probability of 0.25? Try changing the `p` values and observe the shape.

---

## Part 4 — NumPy Universal Functions (ufuncs)

### What Are ufuncs?

**ufuncs** stands for **Universal Functions**. These are special NumPy functions that are designed to work on entire arrays at once — on every element simultaneously — instead of going through them one by one.

> **Analogy:** Imagine you need to paint 100 fence posts. The slow way: you paint them one at a time with a small brush. The fast way: you use a spray painter that covers all 100 at once. ufuncs are NumPy's spray painter.

### Why Use ufuncs?

The main reasons to use ufuncs are:

1. **Speed (Vectorization):** They are dramatically faster than Python loops for large datasets.
2. **Simplicity:** One line of code replaces a multi-line loop.
3. **Extra power:** They support special options like `where`, `dtype`, and `out` for advanced control.

### What is Vectorization?

**Vectorization** means converting an operation that would normally loop over elements one-by-one into a single operation that processes the entire array at once.

Modern CPUs (the chips inside your computer) are specifically designed to perform these "do-it-to-everything-at-once" operations extremely fast. This is called **SIMD (Single Instruction, Multiple Data)** at the hardware level — but you don't need to worry about that. Just know that vectorization uses the computer's hardware more efficiently.

---

### The Problem: Slow Python Loops

Let's first see the *old slow way* of adding two lists together:

```python
# The slow Python way — using a loop
x = [1, 2, 3, 4]
y = [4, 5, 6, 7]
z = []   # Empty list to store results

for i, j in zip(x, y):      # zip() pairs up elements: (1,4), (2,5), (3,6), (4,7)
    z.append(i + j)          # Add each pair and store the result

print(z)
```

**Expected Output:**
```
[5, 7, 9, 11]
```

**Line-by-line explanation:**

| Line | Meaning |
|------|---------|
| `x = [1, 2, 3, 4]` | First list of numbers |
| `y = [4, 5, 6, 7]` | Second list of numbers |
| `z = []` | Start with an empty list to collect results |
| `for i, j in zip(x, y):` | Loop through both lists together, pairing elements |
| `z.append(i + j)` | Add the paired numbers and add them to the results list |

This works! But imagine doing this with 1 million numbers — it would be slow.

---

### The Fast Way: NumPy's `np.add()` ufunc

NumPy has a built-in ufunc called `add()` that does exactly the same thing in one line, but much faster:

```python
import numpy as np

x = [1, 2, 3, 4]
y = [4, 5, 6, 7]

z = np.add(x, y)   # Add all elements at once — no loop needed!

print(z)
```

**Expected Output:**
```
[ 5  7  9 11]
```

**Notice:** The result is exactly the same as the loop version! But `np.add()` did it in a single operation instead of iterating step by step.

> **Thinking prompt:** The output looks like `[ 5  7  9 11]` (with spaces, no commas) instead of `[5, 7, 9, 11]`. Why? Because NumPy arrays print differently from Python lists — no commas, and numbers are aligned.

---

### What Happens Inside np.add()?

```
Input x:  [1,  2,  3,  4]
Input y:  [4,  5,  6,  7]
            ↓   ↓   ↓   ↓
Result z: [5,  7,  9, 11]
```

NumPy processes each matching pair (position 0 with position 0, position 1 with position 1, and so on) all at the same time — this is **element-wise** operation.

---

### Additional ufunc Arguments

ufuncs support special optional arguments that give you more control:

| Argument | What it does | Example |
|----------|-------------|---------|
| `where` | A boolean condition — only apply the operation where True | `np.add(x, y, where=[True, False, True, True])` |
| `dtype` | Specify the data type of the output | `np.add(x, y, dtype=float)` |
| `out` | Specify an output array to write results into | `np.add(x, y, out=result_array)` |

You do not need to memorise all of these right now. The key idea is: ufuncs are flexible tools that go beyond basic loops.

---

### The Performance Difference: Why It Matters

To understand why vectorisation matters, consider this: if you have a dataset with **1 million data points** (common in real data science work), a Python loop might take several seconds. The equivalent NumPy ufunc operation runs in milliseconds.

For example, adding two arrays of 1,000,000 numbers:
- Python loop: ~0.5 seconds
- NumPy ufunc: ~0.005 seconds (100x faster)

This is why data scientists, machine learning engineers, and scientists use NumPy — it makes working with large datasets practical.

---

### Simple ufunc Examples to Consolidate

**Example A — Adding arrays:**
```python
import numpy as np

a = np.array([10, 20, 30])
b = np.array([1, 2, 3])

result = np.add(a, b)
print(result)
```
**Output:** `[11 22 33]`

**Example B — Multiplying arrays:**
```python
import numpy as np

a = np.array([2, 4, 6])
b = np.array([3, 3, 3])

result = np.multiply(a, b)
print(result)
```
**Output:** `[ 6 12 18]`

**Example C — Squaring all elements (using np.power):**
```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5])

squared = np.power(arr, 2)   # Raise each element to the power of 2
print(squared)
```
**Output:** `[ 1  4  9 16 25]`

> **Thinking prompt:** What would `np.power(arr, 3)` produce? Try to calculate the answer before running it.

---

## Guided Practice Exercises

### Exercise 1 — Weighted Lottery Simulation

**Objective:** Simulate a simple lottery where different prizes have different probabilities.

**Scenario:** A raffle has 4 possible prizes:
- Prize A (₦5,000): 5% chance
- Prize B (₦1,000): 15% chance
- Prize C (₦200): 30% chance
- No prize (₦0): 50% chance

**Your Task:**

1. Use `random.choice()` to simulate 500 raffle draws.
2. Print the result.
3. Count how many times each prize was won using `np.unique()` (optional bonus).

**Steps:**

```python
from numpy import random
import numpy as np

# Step 1: Define prizes and their probabilities
prizes = [5000, 1000, 200, 0]
probabilities = [0.05, 0.15, 0.30, 0.50]

# Step 2: Simulate 500 draws
draws = random.choice(prizes, p=probabilities, size=(500))

# Step 3: Print results
print("First 20 draws:", draws[:20])

# Bonus Step: Count how many times each prize appeared
values, counts = np.unique(draws, return_counts=True)
for val, cnt in zip(values, counts):
    print(f"Prize ₦{val}: appeared {cnt} times ({cnt/500*100:.1f}%)")
```

**Expected Output (approximate — exact numbers vary):**
```
First 20 draws: [   0    0  200    0    0    0  200    0 1000    0    0  200    0    0    0    0    0    0    0    0]
Prize ₦0:    appeared 251 times (50.2%)
Prize ₦200:  appeared 149 times (29.8%)
Prize ₦1000: appeared 76 times (15.2%)
Prize ₦5000: appeared 24 times (4.8%)
```

**Self-check questions:**
- Do the counts roughly match the probabilities you set?
- What happens if you increase the draws to 10,000? Do the percentages get closer to the exact probabilities?
- What happens if all probabilities are equal (0.25 each)?

---

### Exercise 2 — Shuffling a Student List

**Objective:** Practice the difference between `shuffle()` and `permutation()`.

**Scenario:** You are a teacher with 8 students. You want to randomly assign them to two groups of 4.

```python
from numpy import random
import numpy as np

students = np.array(["Alice", "Bob", "Carol", "David",
                     "Emma", "Frank", "Grace", "Henry"])

# --- Method 1: Using permutation (safe — keeps original intact) ---
shuffled = random.permutation(students)

print("Original list:", students)
print("Shuffled list:", shuffled)

# Split into two groups
group1 = shuffled[:4]
group2 = shuffled[4:]

print("\nGroup 1:", group1)
print("Group 2:", group2)
```

**Expected Output (your shuffle will differ):**
```
Original list: ['Alice' 'Bob' 'Carol' 'David' 'Emma' 'Frank' 'Grace' 'Henry']
Shuffled list: ['Grace' 'Bob' 'Emma' 'Alice' 'Henry' 'Frank' 'Carol' 'David']

Group 1: ['Grace' 'Bob' 'Emma' 'Alice']
Group 2: ['Henry' 'Frank' 'Carol' 'David']
```

**Self-check questions:**
- Did the original `students` array change?
- Could you use `shuffle()` here instead? What would you need to do differently?
- What if you ran the code again — would you get the same groups?

---

### Exercise 3 — Fast Array Arithmetic with ufuncs

**Objective:** Compare the loop approach vs ufunc approach.

**Scenario:** You have sales data for 5 shops. You need to apply a 10% bonus to each shop's monthly revenue.

```python
import numpy as np

# Monthly revenue (in thousands of Naira)
revenue = np.array([120, 85, 200, 145, 310])

# --- The slow way (loop) ---
bonuses_loop = []
for r in revenue:
    bonuses_loop.append(r * 0.10)
print("Bonuses (loop method):", bonuses_loop)

# --- The fast way (ufunc / vectorized) ---
bonuses_ufunc = np.multiply(revenue, 0.10)
print("Bonuses (ufunc method):", bonuses_ufunc)

# --- New totals ---
new_revenue = np.add(revenue, bonuses_ufunc)
print("Revenue after bonus:", new_revenue)
```

**Expected Output:**
```
Bonuses (loop method): [12.0, 8.5, 20.0, 14.5, 31.0]
Bonuses (ufunc method): [12.  8.5 20.  14.5 31. ]
Revenue after bonus: [132.   93.5 220.  159.5 341. ]
```

**Self-check questions:**
- Are both methods producing the same result?
- Which method would you prefer for a dataset with 1 million entries?
- Can you modify the code to apply a 15% bonus only to shops earning more than 150?

---

### Exercise 4 — Visualising a Weighted Distribution

**Objective:** Use Seaborn to visualise a weighted distribution and observe its shape.

```python
from numpy import random
import matplotlib.pyplot as plt
import seaborn as sns

# Simulate exam grade categories (A, B, C, D, F)
# Most students get B or C, few get A or F
grades_numeric = random.choice([90, 75, 60, 45, 30],
                                p=[0.10, 0.35, 0.40, 0.10, 0.05],
                                size=(500))

# Visualise
sns.displot(grades_numeric, kind="kde")
plt.title("Simulated Exam Grade Distribution")
plt.xlabel("Score")
plt.ylabel("Density")
plt.show()
```

**What to observe:** The curve should peak around 60-75 (since C and B have the highest probabilities), with smaller peaks toward 90 and declining toward 30.

---

## Mini Project — Student Performance Analysis System

### Project Description

You work as a data analyst for a school. You need to:
1. Simulate exam scores for 200 students with a realistic distribution.
2. Randomly shuffle students to create fair seating groups.
3. Apply performance bonuses (ufunc operations).
4. Visualise the final distribution.

### Stage 1 — Setup

```python
from numpy import random
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

print("=== Student Performance Analysis System ===\n")
```

**Expected Output:**
```
=== Student Performance Analysis System ===
```

### Stage 2 — Simulate Exam Scores

We simulate scores on a scale of 0–100 using weighted categories:

```python
# Score bands: Excellent(85-100), Good(70-84), Average(50-69), Below(30-49), Poor(0-29)
score_bands = [92, 77, 60, 40, 15]
score_probs = [0.10, 0.25, 0.40, 0.20, 0.05]

scores = random.choice(score_bands, p=score_probs, size=(200))

print("First 10 student scores:", scores[:10])
print("Total students:", len(scores))
```

**Expected Output:**
```
First 10 student scores: [60 77 60 40 60 60 77 60 15 60]
Total students: 200
```

### Stage 3 — Create Student IDs and Shuffle for Seating

```python
# Create student IDs
student_ids = np.arange(1, 201)  # IDs from 1 to 200

# Shuffle to create random seating order
seating_order = random.permutation(student_ids)

print("Original IDs (first 10):", student_ids[:10])
print("Seating order (first 10):", seating_order[:10])
print("Original IDs unchanged (first 10):", student_ids[:10])
```

**Expected Output:**
```
Original IDs (first 10): [ 1  2  3  4  5  6  7  8  9 10]
Seating order (first 10): [143  78  22  91 166  34   5 188  61 120]
Original IDs unchanged (first 10): [ 1  2  3  4  5  6  7  8  9 10]
```

### Stage 4 — Apply Bonus Points with ufuncs

Students who scored below 50 receive a 5-point bonus. We apply this using ufuncs:

```python
# Create a bonus array: 5 points for scores below 50, 0 otherwise
bonus = np.where(scores < 50, 5, 0)   # np.where is also a ufunc-style operation

# Apply the bonus using np.add
final_scores = np.add(scores, bonus)

# Cap at 100 using np.minimum
final_scores = np.minimum(final_scores, 100)

print("Sample before bonus:", scores[:5])
print("Bonus applied:       ", bonus[:5])
print("Final scores:        ", final_scores[:5])
```

**Expected Output (will vary):**
```
Sample before bonus: [60 77 60 40 60]
Bonus applied:       [ 0  0  0  5  0]
Final scores:        [60 77 60 45 60]
```

### Stage 5 — Visualise the Final Distribution

```python
# Plot before and after
fig, axes = plt.subplots(1, 2, figsize=(12, 5))

sns.histplot(scores, ax=axes[0], color="steelblue")
axes[0].set_title("Before Bonus")
axes[0].set_xlabel("Score")

sns.histplot(final_scores, ax=axes[1], color="green")
axes[1].set_title("After Bonus")
axes[1].set_xlabel("Score")

plt.suptitle("Student Score Distribution")
plt.tight_layout()
plt.show()

print("\nAverage score before bonus:", np.mean(scores).round(2))
print("Average score after bonus: ", np.mean(final_scores).round(2))
```

**Expected Output:**
```
Average score before bonus: 62.15
Average score after bonus:  63.40
```

**Milestone checkpoint:** At this point you have:
- Generated 200 scores using weighted random choice
- Shuffled student IDs safely using `permutation()`
- Applied conditional bonuses using ufunc-style operations
- Visualised before and after distributions

### Optional Extensions

- Add a `grade_letter` column (A, B, C, D, F) based on final score ranges.
- Randomly assign students to 10 exam halls using `random.choice()`.
- Plot a KDE curve comparing score distributions of different grade bands.

---

## Common Beginner Mistakes

### Mistake 1 — Probabilities That Don't Sum to 1.0

```python
# WRONG — probabilities sum to 0.9, not 1.0
x = random.choice([1, 2, 3], p=[0.2, 0.3, 0.4])  # Missing 0.1!
```

**Error you will see:**
```
ValueError: probabilities do not sum to 1
```

**Correct version:**
```python
x = random.choice([1, 2, 3], p=[0.2, 0.3, 0.5])  # 0.2+0.3+0.5 = 1.0 ✓
```

---

### Mistake 2 — Assigning the Return Value of shuffle()

```python
# WRONG — shuffle() returns None, not the shuffled array
arr = np.array([1, 2, 3, 4])
shuffled = random.shuffle(arr)   # shuffled = None!
print(shuffled)  # Prints: None
```

**Correct version:**
```python
arr = np.array([1, 2, 3, 4])
random.shuffle(arr)   # Modifies arr directly
print(arr)            # Prints the shuffled array
```

---

### Mistake 3 — Wrong Number of Probabilities

```python
# WRONG — 4 values but only 3 probabilities
x = random.choice([3, 5, 7, 9], p=[0.1, 0.3, 0.6])
```

**Error:**
```
ValueError: 'a' and 'p' must have same size
```

**Correct version:**
```python
x = random.choice([3, 5, 7, 9], p=[0.1, 0.3, 0.6, 0.0])  # One probability per value
```

---

### Mistake 4 — Forgetting plt.show() with Seaborn

```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.displot([1, 2, 3, 4, 5])
# Nothing appears! You forgot plt.show()
```

**Correct version:**
```python
sns.displot([1, 2, 3, 4, 5])
plt.show()  # This actually displays the chart
```

---

### Mistake 5 — Using a Python Loop Instead of a ufunc

```python
# INEFFICIENT for large datasets
result = []
for val in big_array:
    result.append(val * 2)
```

**Better version:**
```python
import numpy as np
result = np.multiply(big_array, 2)  # Faster and cleaner
```

---

### Mistake 6 — Expecting shuffle() Not to Change the Original

```python
arr = np.array([1, 2, 3, 4, 5])
random.shuffle(arr)
# arr is NOW changed — you cannot get the original back!
```

**Safe version if you need the original:**
```python
arr = np.array([1, 2, 3, 4, 5])
arr_copy = arr.copy()    # Save a copy FIRST
random.shuffle(arr)       # Now it's safe — original is in arr_copy
```

---

## Reflection Questions

Take a moment to think through these questions. They will help you lock in your understanding.

1. **Distributions:** If you set all probabilities equal (e.g., `p=[0.25, 0.25, 0.25, 0.25]`), what shape would you expect the distribution chart to show? Flat or peaked?

2. **Probabilities:** A weather forecaster says there is a 30% chance of rain, 50% chance of clouds, and 20% chance of sun tomorrow. How would you model this as a `random.choice()` call?

3. **Permutations:** You are building an app that shows quiz questions in a random order to each user, but must always display all questions (no repeats, no skips). Which method — `shuffle()` or `permutation()` — is safer to use and why?

4. **Seaborn:** Why would a data scientist prefer `kind="kde"` over the default histogram view when working with continuous data like temperatures or weights?

5. **Vectorization:** If you have a dataset of 5 million sensor readings and need to multiply each by 2.5, why would using `np.multiply()` be significantly better than a Python `for` loop?

6. **ufuncs vs loops:** In your own words, explain what "element-wise" means in the context of ufuncs. Use the `np.add([1,2,3], [4,5,6])` example to explain.

---

## Completion Checklist

Go through this list before moving to the next lesson. Check each item you can confidently do:

- [ ] I can explain what a data distribution is using a real-world example
- [ ] I know that probabilities in `random.choice()` must sum to exactly 1.0
- [ ] I can use `random.choice()` with custom probabilities to generate 1D and 2D arrays
- [ ] I understand the difference between `shuffle()` (modifies original) and `permutation()` (returns new array)
- [ ] I can explain why you should use `arr.copy()` before using `shuffle()` if you need the original
- [ ] I know what Seaborn is and how it relates to Matplotlib
- [ ] I can install Seaborn and draw a basic displot
- [ ] I understand what `kind="kde"` does in `sns.displot()`
- [ ] I can explain what a ufunc is and why it is faster than a loop
- [ ] I understand what "vectorization" means
- [ ] I can use `np.add()` and `np.multiply()` on arrays
- [ ] I have completed at least two of the guided exercises
- [ ] I have attempted the mini-project

---

## Lesson Summary

In this lesson you covered four tightly connected topics in NumPy data science:

**Part 1 — Random Data Distribution:** You learned that a data distribution describes how likely each value is to occur. Using `random.choice()`, you can generate arrays where values appear with custom probabilities. The probabilities must always sum to 1.0. You can generate both 1D and 2D arrays by adjusting the `size` parameter.

**Part 2 — Random Permutations:** You learned two methods for rearranging data. `shuffle()` rearranges the array in-place (the original changes; returns `None`). `permutation()` returns a new rearranged array and leaves the original untouched. Use `permutation()` when you need to keep your original data safe.

**Part 3 — Seaborn Visualisation:** You learned that Seaborn is a Python library that sits on top of Matplotlib and makes it easy to visualise distributions. A `displot` is a distribution plot. Using `kind="kde"` draws a smooth density curve. Always call `plt.show()` to display the chart.

**Part 4 — Universal Functions (ufuncs):** You learned that ufuncs are NumPy's fast, vectorized functions that operate on entire arrays at once without loops. Vectorization converts slow element-by-element iteration into a single fast operation that uses the computer's hardware efficiently. Common ufuncs include `np.add()`, `np.multiply()`, and `np.power()`. ufuncs also accept advanced arguments like `where`, `dtype`, and `out`.

Together, these four skills form the foundation for serious data science work: generating realistic test data, rearranging it safely, visualising it clearly, and processing it efficiently at scale.

---

*End of Lesson 27 — Well done for completing this lesson!*
