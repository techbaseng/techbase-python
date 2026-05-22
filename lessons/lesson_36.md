---
render_with_liquid: false
title: "Lesson 36: Python DSA — Lists, Searching & Bubble Sort"
nav_order: 36
---

# Lesson 36: Python DSA — Lists, Searching & Bubble Sort

---

## Lesson Introduction

Welcome to one of the most important lessons in this entire Python journey — **Data Structures and Algorithms**, commonly shortened to **DSA**.

You already know how to write Python code. Now, it is time to learn how to write **smart** Python code. Smart code is not just code that works — it is code that works **efficiently**, even when dealing with thousands or millions of pieces of data.

This lesson introduces you to the world of DSA through four essential topics: **Lists as data structures**, **building your own algorithms**, **Linear Search**, **Binary Search**, and **Bubble Sort**. These are the building blocks of efficient programming and are used every day in banking systems in Lagos, hospital databases in Abuja, and technology companies around the world.

By the end of this lesson, you will be able to:

- Explain what Data Structures and Algorithms are and why they matter
- Create and use Python lists as dynamic arrays
- Build your own simple algorithms to solve problems
- Understand and implement Linear Search with its time complexity
- Understand and implement Binary Search with its time complexity
- Understand and implement Bubble Sort with its time complexity
- Recognise the improved version of Bubble Sort and explain why it is faster
- Apply these techniques to real-world scenarios like searching records and sorting data

---

## Prerequisite Concepts

Before diving in, make sure you are comfortable with the following Python topics:

- **Lists** — creating, accessing, and looping through them (you can loop using `for i in range(len(mylist))`)
- **Functions** — defining a function with `def` and returning values with `return`
- **For loops and While loops** — both are used heavily in DSA
- **If statements** — comparing values to make decisions
- **Variables** — storing and updating values during a program

> **Quick Recap:** A Python list is an ordered collection of items stored in square brackets: `my_list = [1, 2, 3]`. You access an item using its index, starting from 0: `my_list[0]` gives `1`.

---

## Section 1: What Are Data Structures and Algorithms?

### 1.1 Understanding Data Structures

Imagine you run a small shop in Balogun Market, Lagos. Every day you receive new products. You need a way to **organise** them — maybe by type, by price, or by how many you have in stock.

In programming, a **data structure** is exactly that — a way of organising and storing data in a computer so that it can be used efficiently.

Python already comes with some built-in data structures:

- **Lists** — ordered, changeable collections (our main focus today)
- **Dictionaries** — key-value pairs
- **Sets** — unordered collections with no duplicates
- **Tuples** — ordered, unchangeable collections

Other data structures like linked lists, stacks, queues, trees, and graphs can be built using Python classes. We cover those in later lessons.

### 1.2 Understanding Algorithms

An **algorithm** is a step-by-step set of instructions for solving a problem.

Think of baking **jollof rice** in a pot. You follow steps: wash the rice, fry the tomatoes, add water, boil, stir occasionally. Those are your steps — your algorithm. Skip a step or do them in the wrong order and the result is wrong.

In programming, an algorithm tells the computer exactly what to do, in what order, to get the result you want.

### 1.3 Why DSA Matters

> "Any fool can write code that a computer can understand. Good programmers write code that humans can understand — and that runs fast."

Here is why learning DSA is so valuable:

- Python has clean readable syntax that makes learning DSA easier
- DSA allows you to **improve your problem-solving skills**
- DSA helps you **write more efficient code** — code that runs faster and uses less memory
- DSA gives you a better understanding of **memory storage**
- DSA helps you handle **complex programming challenges**
- Python with DSA is widely used in **Data Science, AI, and Machine Learning** — fields that are growing rapidly in Nigeria and across Africa

Real-world use cases you already interact with:

- **Bank apps** searching for your account number from millions of records
- **Google** sorting search results in milliseconds
- **Hospital systems** finding a patient's file quickly
- **Ride-hailing apps** like Bolt finding the nearest driver

---

## Section 2: Lists and Arrays as a Data Structure

### 2.1 What Is a List in the DSA Sense?

You have used Python lists before. In the world of DSA, a list is also called a **dynamic array** — meaning it can grow or shrink in size as needed.

A regular array (like in languages such as C or Java) has a **fixed size** — you must decide upfront how many items it will hold. Python's list is more flexible — you can add or remove items freely.

**Why is this useful?** Imagine you are building a student result management system. You don't know in advance how many students will register. A Python list lets you add students one by one as they register.

### 2.2 Creating Lists

A list is created using square brackets `[]`:

```python
# An empty list — no items yet
market_list = []

# A list with initial values
prices = [500, 1200, 350, 800, 2000]

# A list with mixed types (strings and numbers)
student = ["Adaeze", "SS3", 17, True]
```

**Expected output in terminal (if you print them):**

```
[]
[500, 1200, 350, 800, 2000]
['Adaeze', 'SS3', 17, True]
```

> **Thinking prompt:** What happens if you have a list of 1,000 students? Would you write each name by hand? Of course not — your program would build the list dynamically by adding names as they are entered.

### 2.3 List Methods — Built-In Algorithms

Python lists come with several **built-in methods** (which are themselves small built-in algorithms) for performing common operations.

```python
scores = [72, 55, 88, 40, 95, 61]

# Add a new score
scores.append(78)

# Sort the list from lowest to highest
scores.sort()

print(scores)
```

**Expected output:**

```
[40, 55, 61, 72, 78, 88, 95]
```

Let's break this down line by line:

- `scores = [72, 55, 88, 40, 95, 61]` — creates a list of six exam scores
- `scores.append(78)` — adds the number 78 to the end of the list (now 7 items)
- `scores.sort()` — rearranges the list from smallest to largest
- `print(scores)` — displays the sorted list

> **Thinking prompt:** What if you called `scores.sort(reverse=True)`? What would the output be?

Here are other commonly used list methods in DSA:

| Method | What it does |
|---|---|
| `append(x)` | Adds item `x` to the end of the list |
| `sort()` | Sorts the list in ascending order |
| `sort(reverse=True)` | Sorts the list in descending order |
| `len(list)` | Returns the number of items |
| `min(list)` | Returns the smallest value |
| `max(list)` | Returns the largest value |
| `list[i]` | Accesses the item at index position `i` |

### 2.4 Building Your Own Algorithms

Sometimes the built-in methods are not enough. You need to create your **own algorithm** for a specific task.

Let's say you want to find the **cheapest price** in a list of market prices without using `min()`.

Here is a custom algorithm that does it step by step:

```python
prices = [1500, 800, 2200, 450, 1100, 700]

# Start by assuming the first price is the cheapest
cheapest = prices[0]

# Go through every price in the list
for price in prices:
    if price < cheapest:
        cheapest = price   # Update if we find something cheaper

print("Cheapest item:", cheapest)
```

**Expected output:**

```
Cheapest item: 450
```

Line-by-line explanation:

- `cheapest = prices[0]` — we assume the first item (₦1500) is the cheapest. We have to start somewhere.
- `for price in prices:` — we loop through every item in the list, one at a time
- `if price < cheapest:` — we ask: is this current price smaller than our current "cheapest"?
- `cheapest = price` — if yes, we update our record of the cheapest
- After the loop ends, `cheapest` holds the actual minimum value

This simple algorithm must **visit every item** in the list once. If the list has 6 items, it runs 6 times. If it has 6,000 items, it runs 6,000 times.

### 2.5 Understanding Time Complexity

This leads to one of the most important ideas in DSA: **time complexity**.

Time complexity tells us: **how much time does an algorithm take as the data grows bigger?**

For the "find cheapest" algorithm above:
- 6 items → 6 comparisons
- 60 items → 60 comparisons
- 600 items → 600 comparisons

The time it takes grows **proportionally** with the size of the data. We say this is **O(n)** — pronounced "Big O of n" or "linear time" — where `n` is the number of items.

Think of it like this analogy: if you are searching for a friend's name in a contacts list of 100 people by reading each name one by one, it takes 100 reads. If the list has 10,000 contacts, it takes 10,000 reads. The time grows **linearly** with the size.

We will revisit time complexity with each algorithm in this lesson.

---

## Section 3: Linear Search

### 3.1 What Is Linear Search?

Linear search (sometimes called **sequential search**) is the simplest searching algorithm in existence. It answers the question: **"Is this value in my list, and if so, where is it?"**

It works by checking each element **one by one**, from the very beginning of the list to the end, until it finds the target value — or runs out of items to check.

**Analogy:** Imagine you have a stack of 50 unmarked envelopes on a table at a post office in Ikeja. You are looking for an envelope addressed to "Chukwuemeka Obi". You pick up the first envelope, check it. Not him. Pick up the second. Not him. You keep going until you find it — or until you've checked all 50.

That is linear search.

### 3.2 How Linear Search Works — Step by Step

Given this list:

```
[3, 7, 2, 9, 5, 1, 8, 4, 6]
```

And we are searching for the value **4**:

1. Check index 0: value is 3. Not 4. Move on.
2. Check index 1: value is 7. Not 4. Move on.
3. Check index 2: value is 2. Not 4. Move on.
4. Check index 3: value is 9. Not 4. Move on.
5. Check index 4: value is 5. Not 4. Move on.
6. Check index 5: value is 1. Not 4. Move on.
7. Check index 6: value is 8. Not 4. Move on.
8. Check index 7: value is 4. **Found it!** Return index 7.

### 3.3 Implementing Linear Search in Python

**Quick method — just checking if a value exists:**

The fastest way in Python to check if a value is in a list is the `in` operator:

```python
students = ["Amara", "Biodun", "Chioma", "Danladi", "Emeka"]

if "Chioma" in students:
    print("Student found!")
else:
    print("Student not found.")
```

**Expected output:**

```
Student found!
```

But what if you need to know the **position** (index) of the value? The `in` operator does not tell you that. For that, you need a proper linear search function.

**Full linear search with index returned:**

```python
def linearSearch(arr, targetVal):
    # Loop through every index in the list
    for i in range(len(arr)):
        # Check if the current value matches what we are looking for
        if arr[i] == targetVal:
            return i    # Return the index where it was found
    return -1           # Return -1 if value was never found

# Our list of test scores
scores = [72, 55, 88, 40, 95, 61, 78]

# We want to find where the score 95 is
target = 95
result = linearSearch(scores, target)

if result != -1:
    print(f"Score {target} found at index {result}")
else:
    print(f"Score {target} not found in the list")
```

**Expected output:**

```
Score 95 found at index 4
```

Line-by-line breakdown of the function:

- `def linearSearch(arr, targetVal):` — defines our function. It takes `arr` (the list) and `targetVal` (what we're looking for)
- `for i in range(len(arr)):` — `len(arr)` gives the total number of items. `range(len(arr))` generates indices 0, 1, 2, 3, ... up to the last index. `i` takes each index value one turn at a time.
- `if arr[i] == targetVal:` — we access the item at position `i` using `arr[i]`, then compare it to our target
- `return i` — if we found a match, we immediately return the index and **exit the function**
- `return -1` — if the loop finishes without finding anything, we return -1. By convention, -1 means "not found" because -1 is never a valid list index

> **Thinking prompt:** What happens if the same value appears **twice** in the list? Which index will be returned?

**Second example — searching a list of Nigerian city names:**

```python
def linearSearch(arr, targetVal):
    for i in range(len(arr)):
        if arr[i] == targetVal:
            return i
    return -1

cities = ["Lagos", "Abuja", "Kano", "Port Harcourt", "Ibadan", "Enugu"]
city_to_find = "Port Harcourt"

result = linearSearch(cities, city_to_find)

if result != -1:
    print(f"{city_to_find} is at index {result}")
else:
    print(f"{city_to_find} is not in the list")
```

**Expected output:**

```
Port Harcourt is at index 3
```

### 3.4 Linear Search Time Complexity

In the **best case** — the item we're looking for is the very first one — only **1 comparison** is needed.

In the **worst case** — the item is at the very end, or not in the list at all — **n comparisons** are needed (where `n` is the size of the list).

We always measure time complexity by the worst case:

**Time complexity of Linear Search: O(n)**

This means: if the list doubles in size, the search takes approximately twice as long.

- 100 items → up to 100 comparisons
- 1,000 items → up to 1,000 comparisons
- 1,000,000 items → up to 1,000,000 comparisons

This is fine for small lists. But for very large datasets, we need something faster. That brings us to Binary Search.

---

## Section 4: Binary Search

### 4.1 What Is Binary Search?

Binary Search is a **much faster** search algorithm — but with one important requirement: **the list must already be sorted**.

If the list is sorted, Binary Search can find a value in a fraction of the time that Linear Search would take. Instead of checking every item one by one, Binary Search repeatedly **cuts the search area in half**.

**Analogy:** Think of searching for a name in a physical dictionary. You don't start from page 1 and read every word. You open the book roughly in the middle. If the name you want comes before the current page alphabetically, you look in the left half. If it comes after, you look in the right half. You keep halving the remaining pages until you find it.

That is Binary Search.

### 4.2 How Binary Search Works — Step by Step

Let's say we have this **sorted** list:

```
[2, 3, 7, 7, 11, 15, 25]
```

We want to find the value **11**.

**Step 1:** Check the middle value. The middle index of a 7-item list is index 3 (calculated as `(0 + 6) // 2 = 3`). Value at index 3 is **7**.

Is 7 equal to 11? No.
Is 11 greater than 7? Yes → search the **right half**: [11, 15, 25]

**Step 2:** Our new search area is indices 4 to 6. The new middle is index 5 (calculated as `(4 + 6) // 2 = 5`). Value at index 5 is **15**.

Is 15 equal to 11? No.
Is 11 less than 15? Yes → search the **left half**: [11]

**Step 3:** Our new search area is only index 4. Value at index 4 is **11**.

Is 11 equal to 11? **Yes! Found it!** Return index 4.

**Binary Search found the value in just 3 comparisons**, instead of 5 comparisons that Linear Search would have needed.

### 4.3 Implementing Binary Search in Python

```python
def binarySearch(arr, targetVal):
    left = 0               # Start of the search area
    right = len(arr) - 1   # End of the search area

    while left <= right:
        # Find the middle index
        mid = (left + right) // 2

        # Did we find the target?
        if arr[mid] == targetVal:
            return mid

        # Target is in the right half — move left boundary up
        if arr[mid] < targetVal:
            left = mid + 1
        # Target is in the left half — move right boundary down
        else:
            right = mid - 1

    # If we exit the loop, the value was not found
    return -1

# IMPORTANT: The list must be sorted!
exam_scores = [40, 55, 61, 72, 78, 88, 95]
target = 72

result = binarySearch(exam_scores, target)

if result != -1:
    print(f"Score {target} found at index {result}")
else:
    print(f"Score {target} not found")
```

**Expected output:**

```
Score 72 found at index 3
```

Detailed line-by-line breakdown:

- `left = 0` — we begin searching from the very first index (0)
- `right = len(arr) - 1` — we end searching at the very last index. A list of 7 items has indices 0–6, so `right = 6`
- `while left <= right:` — we keep searching as long as there is still a valid range to search. When `left` goes past `right`, the search area is empty and we stop.
- `mid = (left + right) // 2` — calculate the middle index. `//` is integer division (no decimal). For left=0, right=6: `(0+6)//2 = 3`
- `if arr[mid] == targetVal: return mid` — we found it! Return the index immediately.
- `if arr[mid] < targetVal: left = mid + 1` — our target is **larger** than the middle value, so we look to the right. We move our left boundary to just after the middle.
- `else: right = mid - 1` — our target is **smaller** than the middle value, so we look to the left. We move our right boundary to just before the middle.
- `return -1` — if the loop ends without finding anything, the value is not in the list.

**Second example — searching for a product price:**

```python
def binarySearch(arr, targetVal):
    left = 0
    right = len(arr) - 1

    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == targetVal:
            return mid
        if arr[mid] < targetVal:
            left = mid + 1
        else:
            right = mid - 1
    return -1

# Market prices (must be sorted!)
prices = [150, 300, 500, 750, 1000, 1500, 2000, 3500, 5000]
search_price = 1000

result = binarySearch(prices, search_price)

if result != -1:
    print(f"Price ₦{search_price} found at index {result}")
else:
    print(f"Price ₦{search_price} not in list")
```

**Expected output:**

```
Price ₦1000 found at index 4
```

### 4.4 Binary Search Time Complexity

Each time Binary Search compares a value, it **eliminates half of the remaining items** from consideration.

- Start: 1,000 items to check
- After 1st comparison: 500 items left
- After 2nd comparison: 250 items left
- After 3rd comparison: 125 items left
- After 10th comparison: about 1 item left

In the worst case, Binary Search needs at most **log₂(n)** comparisons.

**Time complexity of Binary Search: O(log₂n)**

Compare these numbers:

| Number of items (n) | Linear Search (worst case) | Binary Search (worst case) |
|---|---|---|
| 10 | 10 comparisons | 4 comparisons |
| 100 | 100 comparisons | 7 comparisons |
| 1,000 | 1,000 comparisons | 10 comparisons |
| 1,000,000 | 1,000,000 comparisons | 20 comparisons |

This is a **massive** difference. Binary Search on a list of one million items needs at most 20 comparisons. Linear Search could need a million.

> **Important reminder:** Binary Search only works on **sorted** lists. If your list is not sorted, sort it first — then search.

---

## Section 5: Bubble Sort

### 5.1 What Is Sorting? Why Does It Matter?

Before we can use Binary Search, we need our data to be **sorted**. Sorting is also important in many other situations:

- Displaying students' results from highest to lowest grade
- Arranging products in a store from cheapest to most expensive
- Organising customer transactions by date
- Ranking football teams in the NPFL standings

Bubble Sort is one of the simplest sorting algorithms to understand and implement.

### 5.2 What Is Bubble Sort?

Bubble Sort is an algorithm that sorts a list of values from **lowest to highest** (ascending order).

The name "Bubble Sort" comes from how the algorithm works: the largest values **"bubble up"** toward the end of the list, one pass at a time — just like bubbles in suya oil rising to the surface.

**How it works:**

1. Go through the list, one value at a time
2. For each value, compare it with the **next** value
3. If the current value is **greater** than the next, **swap** them
4. Repeat this process as many times as there are values in the list

### 5.3 Manual Walk-Through: Seeing Bubble Sort in Action

Let's trace through a small list by hand:

```
[7, 12, 9, 11, 3]
```

**Pass 1 (first complete run through the list):**

- Compare 7 and 12: 7 < 12, no swap → `[7, 12, 9, 11, 3]`
- Compare 12 and 9: 12 > 9, **swap** → `[7, 9, 12, 11, 3]`
- Compare 12 and 11: 12 > 11, **swap** → `[7, 9, 11, 12, 3]`
- Compare 12 and 3: 12 > 3, **swap** → `[7, 9, 11, 3, 12]`

After Pass 1: `[7, 9, 11, 3, 12]` → The largest value **12 has bubbled to the end** ✓

**Pass 2:**

- Compare 7 and 9: no swap → `[7, 9, 11, 3, 12]`
- Compare 9 and 11: no swap → `[7, 9, 11, 3, 12]`
- Compare 11 and 3: **swap** → `[7, 9, 3, 11, 12]`
- (12 is already in place — we skip it)

After Pass 2: `[7, 9, 3, 11, 12]` → 11 and 12 in place ✓

**Pass 3:**

- Compare 7 and 9: no swap
- Compare 9 and 3: **swap** → `[7, 3, 9, 11, 12]`

After Pass 3: `[7, 3, 9, 11, 12]`

**Pass 4:**

- Compare 7 and 3: **swap** → `[3, 7, 9, 11, 12]`

**Final sorted list: `[3, 7, 9, 11, 12]`** ✓

### 5.4 Implementing Bubble Sort in Python

```python
mylist = [64, 34, 25, 12, 22, 11, 90, 5]

n = len(mylist)   # n = 8 (number of items)

# Outer loop: runs n-1 times (one pass per item, minus 1)
for i in range(n - 1):
    # Inner loop: compares adjacent pairs
    # Each pass, one fewer comparison is needed (the last i items are already sorted)
    for j in range(n - i - 1):
        # If the current item is greater than the next item, swap them
        if mylist[j] > mylist[j + 1]:
            mylist[j], mylist[j + 1] = mylist[j + 1], mylist[j]

print(mylist)
```

**Expected output:**

```
[5, 11, 12, 22, 25, 34, 64, 90]
```

Detailed line-by-line breakdown:

- `n = len(mylist)` — we store the list length in `n` for reuse. Here n = 8.
- `for i in range(n - 1):` — the outer loop runs 7 times (n-1). Why n-1 and not n? Because after n-1 passes, the list is guaranteed to be sorted.
- `for j in range(n - i - 1):` — the inner loop compares adjacent pairs. The `- i` part is important: after each outer loop pass, the last `i` elements are already sorted and don't need to be checked again. This makes the algorithm slightly faster each round.
- `if mylist[j] > mylist[j + 1]:` — are these two neighbours in the wrong order?
- `mylist[j], mylist[j + 1] = mylist[j + 1], mylist[j]` — this is Python's elegant **simultaneous swap**. Both values swap positions in one line, without needing a temporary variable.

> **Thinking prompt:** What would happen if you ran this on a list that's already sorted, like `[1, 2, 3, 4, 5]`? It would still run all the loops but never swap anything. Can we make it stop early?

### 5.5 Improved Bubble Sort — Stopping Early

Consider this nearly-sorted list:

```python
mylist = [3, 7, 9, 11, 12]
```

After the very first pass through this list, no swaps happen — because it's already sorted! But the basic Bubble Sort keeps running through more passes anyway, wasting time.

The **improved Bubble Sort** adds a flag that detects when no swaps happen during a pass. If no swaps happened, the list is already sorted and we can **stop early**:

```python
mylist = [7, 3, 9, 12, 11]

n = len(mylist)

for i in range(n - 1):
    swapped = False   # Assume no swaps happened this pass

    for j in range(n - i - 1):
        if mylist[j] > mylist[j + 1]:
            mylist[j], mylist[j + 1] = mylist[j + 1], mylist[j]
            swapped = True   # A swap happened — list not yet fully sorted

    if not swapped:
        break   # No swaps this pass → list is sorted → stop immediately

print(mylist)
```

**Expected output:**

```
[3, 7, 9, 11, 12]
```

New lines explained:

- `swapped = False` — at the start of every outer loop pass, we assume nothing will need to be swapped
- `swapped = True` — if we do swap something, we record that fact
- `if not swapped: break` — if we finished the entire inner loop without swapping anything, the list is sorted. `break` exits the outer loop immediately, saving unnecessary passes.

**When does this improvement matter most?** When sorting a list that is already nearly sorted. In the best case (fully sorted list), the improved version runs through only **one pass** — a dramatic saving.

### 5.6 Bubble Sort Time Complexity

In the basic Bubble Sort:
- The outer loop runs **n-1** times
- For each outer pass, the inner loop runs up to **n** times (decreasing slightly each pass)
- Total comparisons: roughly **n × n = n²**

**Time complexity of Bubble Sort: O(n²)**

Compare what this means in practice:

| Number of items (n) | Bubble Sort (approximate operations) |
|---|---|
| 10 | 100 |
| 100 | 10,000 |
| 1,000 | 1,000,000 |
| 10,000 | 100,000,000 |

As you can see, Bubble Sort gets very slow for large datasets. This is why faster sorting algorithms like **Quicksort** (covered in a later lesson) are preferred in real-world applications.

However, Bubble Sort is an excellent algorithm for:
- Teaching the fundamentals of sorting
- Sorting very small lists where performance is not a concern
- Situations where the list is nearly sorted (with the improved version)

---

## Section 6: Guided Practice Exercises

### Exercise 1: Find the Maximum Value (Warm-Up)

**Objective:** Write an algorithm to find the highest mark in a class test result without using Python's built-in `max()` function.

**Scenario:** Teacher Ngozi has recorded the following test scores for her JSS3 class in Abuja:

```
[45, 72, 60, 88, 51, 95, 67, 73]
```

**Steps:**

1. Create a variable `highest` and assign it the first score in the list
2. Loop through each score
3. If the current score is greater than `highest`, update `highest`
4. After the loop, print the result

**Solution:**

```python
scores = [45, 72, 60, 88, 51, 95, 67, 73]

highest = scores[0]   # Assume the first score is the highest

for score in scores:
    if score > highest:
        highest = score

print("Highest score:", highest)
```

**Expected output:**

```
Highest score: 95
```

**Self-check questions:**

- What would happen if all scores were the same, say all 70?
- What if the list had only one item?

---

### Exercise 2: Linear Search on Student Records

**Objective:** Write a linear search function to find a student in a school register.

**Scenario:** The school secretary at Citadel Academy, Lagos needs to check if "Fatima" is registered this term. The student list is:

```python
students = ["Tunde", "Amaka", "Yusuf", "Fatima", "Chidinma", "Babatunde", "Ngozi"]
```

**Steps:**

1. Define a `linearSearch(arr, target)` function
2. Loop through the list using `range(len(arr))`
3. Return the index if the name is found
4. Return -1 if not found
5. Call the function and print an appropriate message

**Solution:**

```python
def linearSearch(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1

students = ["Tunde", "Amaka", "Yusuf", "Fatima", "Chidinma", "Babatunde", "Ngozi"]
name = "Fatima"

result = linearSearch(students, name)

if result != -1:
    print(f"{name} is registered. Found at position {result + 1} on the register.")
else:
    print(f"{name} is not registered this term.")
```

**Expected output:**

```
Fatima is registered. Found at position 4 on the register.
```

**Note:** We print `result + 1` because the list uses 0-based indexing (starts at 0), but people count from 1.

**What-if challenge:** What if you searched for "Chika"? Try it — what output do you get?

---

### Exercise 3: Sort and Then Search

**Objective:** Combine sorting and Binary Search to efficiently find a product price.

**Scenario:** A supermarket in Port Harcourt has recorded these product prices (unsorted):

```python
prices = [1500, 300, 4500, 750, 2000, 200, 850, 3200]
```

Sort the list, then use Binary Search to check if a price of ₦850 exists.

**Solution:**

```python
def binarySearch(arr, target):
    left = 0
    right = len(arr) - 1

    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1

prices = [1500, 300, 4500, 750, 2000, 200, 850, 3200]

# Step 1: Sort the list (REQUIRED before Binary Search)
prices.sort()
print("Sorted prices:", prices)

# Step 2: Search for the price
target_price = 850
result = binarySearch(prices, target_price)

if result != -1:
    print(f"Price ₦{target_price} found at index {result} in sorted list.")
else:
    print(f"Price ₦{target_price} not found.")
```

**Expected output:**

```
Sorted prices: [200, 300, 750, 850, 1500, 2000, 3200, 4500]
Price ₦850 found at index 3 in sorted list.
```

**What-if challenge:** What would happen if you searched for ₦1000 (which is not in the list)?

---

## Section 7: Mini Project — Student Grade Manager

Let's bring everything together in a realistic mini project.

**Project Goal:** Build a simple Student Grade Manager that stores exam scores, sorts them, finds the highest and lowest scores, and allows you to search for a specific score.

### Stage 1: Set Up the Data

```python
# Student names and their scores
students = ["Amara", "Biodun", "Chioma", "Danladi", "Emeka", "Funmi", "Gbenga"]
scores   = [72,      88,       55,       91,        67,      78,      84]

print("=== CLASS RESULTS ===")
for i in range(len(students)):
    print(f"{students[i]}: {scores[i]}")
```

**Expected output:**

```
=== CLASS RESULTS ===
Amara: 72
Biodun: 88
Chioma: 55
Danladi: 91
Emeka: 67
Funmi: 78
Gbenga: 84
```

### Stage 2: Find Highest and Lowest (Custom Algorithm)

```python
# Find highest score manually
highest = scores[0]
highest_student = students[0]

for i in range(len(scores)):
    if scores[i] > highest:
        highest = scores[i]
        highest_student = students[i]

# Find lowest score manually
lowest = scores[0]
lowest_student = students[0]

for i in range(len(scores)):
    if scores[i] < lowest:
        lowest = scores[i]
        lowest_student = students[i]

print(f"\nTop student: {highest_student} with {highest}/100")
print(f"Lowest score: {lowest_student} with {lowest}/100")
```

**Expected output:**

```
Top student: Danladi with 91/100
Lowest score: Chioma with 55/100
```

### Stage 3: Search for a Score Using Linear Search

```python
def linearSearch(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1

search_score = 78
result = linearSearch(scores, search_score)

if result != -1:
    print(f"\nScore {search_score} belongs to {students[result]}")
else:
    print(f"\nNo student scored exactly {search_score}")
```

**Expected output:**

```
Score 78 belongs to Funmi
```

### Stage 4: Sort the Scores and Use Binary Search

```python
def binarySearch(arr, target):
    left = 0
    right = len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1

# Sort a COPY of the scores (we don't want to scramble the original pairing)
sorted_scores = sorted(scores)

print("\nSorted scores:", sorted_scores)

# Binary search in sorted list
search_target = 88
bs_result = binarySearch(sorted_scores, search_target)

if bs_result != -1:
    print(f"Score {search_target} found at index {bs_result} in sorted list")
else:
    print(f"Score {search_target} not found")
```

**Expected output:**

```
Sorted scores: [55, 67, 72, 78, 84, 88, 91]
Score 88 found at index 5 in sorted list
```

### Stage 5: Sort with Bubble Sort

```python
def bubbleSort(arr):
    n = len(arr)
    for i in range(n - 1):
        swapped = False
        for j in range(n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        if not swapped:
            break
    return arr

scores_copy = scores.copy()
bubbleSort(scores_copy)

print("\nScores after Bubble Sort:", scores_copy)
```

**Expected output:**

```
Scores after Bubble Sort: [55, 67, 72, 78, 84, 88, 91]
```

> **Reflection:** The output of Bubble Sort matches `sorted()`. Both produce the same sorted list — but `sorted()` uses a more advanced algorithm internally. Bubble Sort is slower but easier to understand.

**Optional extension:** Can you modify the project to accept a student name as input and display their score?

---

## Section 8: Common Beginner Mistakes

### Mistake 1: Using Binary Search on an Unsorted List

```python
# WRONG — list is not sorted!
prices = [1500, 300, 4500, 750, 2000]
result = binarySearch(prices, 750)   # Will likely give wrong result or -1
```

**Why it fails:** Binary Search makes decisions based on the assumption that smaller values are on the left and larger values are on the right. If the list is unsorted, those assumptions are wrong and the algorithm may look in the wrong half — missing the value entirely.

**Correction:**
```python
prices = [1500, 300, 4500, 750, 2000]
prices.sort()   # Sort FIRST
result = binarySearch(prices, 750)   # Now it works correctly
```

---

### Mistake 2: Forgetting to Return -1 in Linear Search

```python
# WRONG — no return -1
def linearSearch(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    # Nothing returned if not found — function returns None

result = linearSearch([1, 2, 3], 99)
if result != -1:   # This comparison fails because result is None, not -1
    print("Found")
```

**Correction:**
```python
def linearSearch(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1   # Always return -1 if not found
```

---

### Mistake 3: Off-By-One Errors in Binary Search

```python
# WRONG — right is set to len(arr) instead of len(arr) - 1
def binarySearch(arr, target):
    left = 0
    right = len(arr)   # BUG: should be len(arr) - 1

    while left <= right:
        mid = (left + right) // 2
        # ...
```

**Why it fails:** If a list has 5 items (indices 0–4), the last valid index is 4 (`len(arr) - 1`). Setting `right = len(arr)` means `right = 5`, which is beyond the list. Accessing `arr[5]` on a 5-item list causes an `IndexError`.

**Correction:**
```python
right = len(arr) - 1   # Correct
```

---

### Mistake 4: Confusing the Outer and Inner Loops in Bubble Sort

```python
# WRONG — using the same loop variable for both loops
for i in range(n - 1):
    for i in range(n - i - 1):   # BUG: reusing 'i' overwrites the outer counter!
        ...
```

**Correction:**
```python
for i in range(n - 1):
    for j in range(n - i - 1):   # Use a different variable 'j' for the inner loop
        ...
```

---

### Mistake 5: Not Using a Copy Before Sorting

```python
students = ["Tunde", "Amaka", "Fatima"]
scores   = [75, 92, 61]

scores.sort()   # This modifies the original list in place!
# Now scores = [61, 75, 92], but students still = ["Tunde", "Amaka", "Fatima"]
# The pairing is now WRONG — Fatima who had 61 is now matched with 75
```

**Correction:**
```python
sorted_scores = sorted(scores)   # Creates a new sorted list, original is unchanged
# OR
sorted_scores = scores.copy()
sorted_scores.sort()
```

---

## Section 9: Reflection Questions

Think carefully about these questions. Try to answer them before looking back at the lesson:

1. What is the difference between a **data structure** and an **algorithm**?
2. Why does Linear Search have a time complexity of **O(n)**?
3. Why must Binary Search only be used on **sorted** lists?
4. If you had a sorted list of 1,024 items, what is the **maximum** number of comparisons Binary Search would need? *(Hint: 2¹⁰ = 1,024)*
5. Walk through Bubble Sort manually on `[5, 3, 8, 1]`. How many swaps happen in the first pass?
6. Why is the **improved Bubble Sort** better than the basic version for nearly-sorted lists?
7. You are building a contact list for a mobile app with 10 million users. You need to search for a user by name. Would you choose Linear Search or Binary Search? Why?
8. In the Bubble Sort algorithm, why does the inner loop use `range(n - i - 1)` instead of `range(n)`?

---

## Completion Checklist

Before moving on, confirm you can do each of the following:

- [ ] Explain what DSA stands for and why it matters in software development
- [ ] Create a Python list and use built-in list methods like `append()` and `sort()`
- [ ] Write a custom algorithm to find the minimum or maximum value in a list
- [ ] Explain what time complexity means and what O(n) represents
- [ ] Write a `linearSearch()` function that returns the index of a target value or -1
- [ ] Explain why Linear Search has time complexity O(n)
- [ ] Write a `binarySearch()` function using a while loop with left/right pointers
- [ ] Explain why Binary Search has time complexity O(log₂n)
- [ ] Explain the requirement that Binary Search needs a sorted list
- [ ] Trace through Bubble Sort manually on a small array
- [ ] Write a `bubbleSort()` function using nested loops
- [ ] Write the improved Bubble Sort with the `swapped` flag and `break`
- [ ] Explain why Bubble Sort has time complexity O(n²)
- [ ] Avoid the common mistakes covered in Section 8

---

## Lesson Summary

You have just completed a foundational lesson in **Data Structures and Algorithms** — one of the most important topics in all of computer science.

Here is what you learned today:

**Data Structures** are organised ways to store data. Python's built-in **list** is a dynamic array that is the foundation for many DSA operations.

**Algorithms** are step-by-step instructions for solving problems. You can build your own or use Python's built-in ones.

**Time Complexity** measures how an algorithm's running time grows as the input size grows. We use **Big O notation** to express this:
- O(n) — linear time (doubles if data doubles)
- O(log₂n) — logarithmic time (only increases by 1 step when data doubles)
- O(n²) — quadratic time (quadruples when data doubles — slow!)

**Linear Search** — O(n) — checks every element one by one. Simple, works on any list (sorted or not), but slow for large datasets.

**Binary Search** — O(log₂n) — works on **sorted** lists only, but is dramatically faster. Cuts the search area in half with every comparison.

**Bubble Sort** — O(n²) — compares adjacent pairs and swaps them until the list is sorted. Easy to understand but slow for large lists. The improved version stops early if the list becomes sorted before all passes are complete.

---

## Quick Reference Card

| Algorithm | Works on | Time Complexity | Key Requirement |
|---|---|---|---|
| Linear Search | Any list | O(n) | None |
| Binary Search | Sorted list only | O(log₂n) | List MUST be sorted |
| Bubble Sort | Any list | O(n²) | None |

**Key function signatures to remember:**

```python
# Linear Search
def linearSearch(arr, targetVal):
    for i in range(len(arr)):
        if arr[i] == targetVal:
            return i
    return -1

# Binary Search (list must be sorted!)
def binarySearch(arr, targetVal):
    left = 0
    right = len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == targetVal:
            return mid
        elif arr[mid] < targetVal:
            left = mid + 1
        else:
            right = mid - 1
    return -1

# Improved Bubble Sort
def bubbleSort(arr):
    n = len(arr)
    for i in range(n - 1):
        swapped = False
        for j in range(n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        if not swapped:
            break
    return arr
```

**Key vocabulary:**

- **DSA** — Data Structures and Algorithms
- **Data structure** — a way of organising data (e.g. list, dictionary, stack)
- **Algorithm** — a step-by-step solution to a problem
- **Time complexity** — how an algorithm's speed scales with data size
- **Big O notation** — mathematical way to express time complexity
- **Linear Search** — check every element one by one
- **Binary Search** — halve the search area with each comparison (requires sorted list)
- **Bubble Sort** — compare adjacent pairs and swap; repeat until sorted
- **Swap** — exchange the positions of two values
- **O(n)** — linear time
- **O(log₂n)** — logarithmic time
- **O(n²)** — quadratic time
