---
render_with_liquid: false
title: "Sorting Algorithms in Python: Selection Sort, Insertion Sort, Quicksort, Counting Sort, and Radix Sort"
nav_order: 37
---

# Lesson 37: Sorting Algorithms in Python
## Selection Sort · Insertion Sort · Quicksort · Counting Sort · Radix Sort

---

## Lesson Introduction

Every day, computers sort enormous amounts of data: products ranked by price, student grades arranged from highest to lowest, names listed alphabetically, or sensor readings organised by time. **Sorting** is one of the most fundamental tasks in computing.

In this lesson, you will learn **five important sorting algorithms** in Python, each with its own strategy, strengths, and weaknesses. By the end, you will be able to explain how each one works, write the Python code yourself, recognise when to use each one, and understand why choosing the right algorithm matters in real projects.

Think of sorting algorithms like strategies for arranging a deck of shuffled playing cards. Some strategies are slow but easy to understand. Others are blazingly fast. Some only work for certain kinds of cards. Let's explore them all.

---

## Prerequisite Concepts

Before we begin, let us quickly review a few ideas you will need to understand throughout this lesson.

### What is a List (Array) in Python?

A **list** in Python is an ordered collection of items stored in a single variable. Think of it like a row of labelled boxes — each box holds one value, and each box has a position number called an **index** (starting from 0).

```python
my_list = [7, 12, 9, 11, 3]
#           ^   ^   ^   ^  ^
# index:    0   1   2   3  4
```

- `my_list[0]` gives you `7` (the first item)
- `my_list[4]` gives you `3` (the last item)
- `len(my_list)` gives you `5` (the total number of items)

### What is a Loop?

A **loop** repeats a block of code many times. In sorting, we use loops to scan through the list over and over again.

```python
# A for loop visits each position
for i in range(5):      # i goes: 0, 1, 2, 3, 4
    print(i)
```

**Output:**
```
0
1
2
3
4
```

### What is Swapping?

**Swapping** means exchanging the positions of two values. Python makes this beautifully easy:

```python
a = 10
b = 99
a, b = b, a     # Swap! Now a=99 and b=10
print(a, b)
```

**Output:**
```
99 10
```

### What is a Function?

A **function** is a named block of code you can reuse. You define it once and call it whenever you need it.

```python
def greet(name):
    print("Hello,", name)

greet("Alice")   # calls the function
greet("Bob")
```

**Output:**
```
Hello, Alice
Hello, Bob
```

### What is Recursion?

**Recursion** is when a function calls *itself*. It is used in Quicksort. Think of it like a mirror reflecting another mirror — each reflection is a smaller version of the same image.

```python
def countdown(n):
    if n == 0:
        print("Done!")
        return
    print(n)
    countdown(n - 1)    # function calls itself with a smaller value

countdown(3)
```

**Output:**
```
3
2
1
Done!
```

Now you are ready. Let's start sorting!

---

## Part 1: Selection Sort

### What is Selection Sort?

**Selection Sort** is one of the simplest sorting strategies. The idea is this: scan the entire unsorted portion of the list, find the smallest value, and move it to the correct position at the front. Then repeat for the rest of the list.

The name comes from what it does: it **selects** the minimum value in each pass.

> **Real-World Analogy:** Imagine you have a pile of 10 coins of different sizes scattered on a table. You scan all of them, pick out the smallest coin, and place it first in a row. Then you scan the remaining coins, pick the next smallest, and place it second. You keep doing this until all coins are in order from smallest to largest.

---

### How Selection Sort Works (Step-by-Step)

Let's trace through a short array to make this concrete.

**Starting array:** `[7, 12, 9, 11, 3]`

**Pass 1:** Scan all 5 values. The smallest is **3** (at index 4). Swap 3 with the first element 7.
```
Before: [7, 12, 9, 11, 3]
After:  [3, 12, 9, 11, 7]
```

**Pass 2:** The first position is now sorted. Scan the rest: 12, 9, 11, 7. Smallest is **7** (at index 4). Swap 7 with 12.
```
Before: [3, 12, 9, 11, 7]
After:  [3,  7, 9, 11, 12]
```

**Pass 3:** Scan 9, 11, 12. Smallest is **9** — already in its correct spot. No swap needed.
```
[3, 7, 9, 11, 12]
```

**Pass 4:** Scan 11, 12. Smallest is **11** — already correct.
```
[3, 7, 9, 11, 12]  ✅ Sorted!
```

---

### Simple Example: Selection Sort Without Swapping (Basic Version)

This is the simpler but slower approach — it removes the minimum and inserts it at the front:

```python
mylist = [64, 34, 25, 5, 22, 11, 90, 12]

n = len(mylist)           # n = 8 (number of elements)

for i in range(n - 1):   # outer loop runs n-1 times
    min_index = i         # assume the current position holds the minimum

    for j in range(i + 1, n):    # inner loop scans the rest
        if mylist[j] < mylist[min_index]:
            min_index = j         # update if we find something smaller

    min_value = mylist.pop(min_index)   # remove the minimum
    mylist.insert(i, min_value)         # put it at position i

print(mylist)
```

**Expected Output:**
```
[5, 11, 12, 22, 25, 34, 64, 90]
```

Let's explain every line:

| Line | What It Does |
|------|-------------|
| `n = len(mylist)` | Gets the total count of elements (8 here) |
| `for i in range(n - 1)` | Outer loop: we need n-1 passes to sort |
| `min_index = i` | Start by assuming position `i` holds the minimum |
| `for j in range(i+1, n)` | Inner loop: scan everything after position `i` |
| `if mylist[j] < mylist[min_index]` | If we find something smaller... |
| `min_index = j` | ...update our "minimum location" |
| `mylist.pop(min_index)` | Remove the minimum from its current position |
| `mylist.insert(i, min_value)` | Insert it at the correct sorted position |

> **What happens if the input is already sorted?** Try changing the list to `[1, 2, 3, 4, 5]` and running the code. How many swaps happen?

---

### The Shifting Problem

There is a hidden cost in the basic version above. When you use `.pop()` to remove an element, Python must **slide every element after it one step down** to fill the gap. When you use `.insert()`, Python must **slide every element after it one step up** to make room.

For a list with 1,000 elements, this hidden sliding happens thousands of times — and it all costs time.

**Visual:** Removing element at index 2 from `[A, B, C, D, E]`:
```
[A, B, _, D, E]   → gap created
[A, B, D, E]      → D and E slide left to fill it
```

This is slow. We can fix it.

---

### Improved Selection Sort: Using Swapping

Instead of removing and inserting, simply **swap** the minimum value with the element at position `i`. This avoids all that sliding.

```python
mylist = [64, 34, 25, 12, 22, 11, 90, 5]

n = len(mylist)

for i in range(n):
    min_index = i             # assume position i is the minimum

    for j in range(i + 1, n):
        if mylist[j] < mylist[min_index]:
            min_index = j     # found a smaller value

    # Swap the found minimum with the element at position i
    mylist[i], mylist[min_index] = mylist[min_index], mylist[i]

print(mylist)
```

**Expected Output:**
```
[5, 11, 12, 22, 25, 34, 64, 90]
```

The result is exactly the same, but internally no elements shift around. Only two elements are swapped. This is much more efficient.

> **Why does swapping work here?** Because we don't care where the "large" element we displaced goes — we haven't sorted it yet anyway. We only need the *minimum* in the correct spot.

---

### Selection Sort Time Complexity

**Time complexity** is a way to measure how much *work* an algorithm does as the input grows.

For an array of `n` values:
- The outer loop runs approximately `n` times
- The inner loop scans on average `n/2` elements
- Total work: `n × n/2 = n²/2`

We write this as **O(n²)** (pronounced "Big-O of n squared").

What does this mean in practice?

| Array Size (n) | Approximate Operations |
|---------------|----------------------|
| 10 | ~50 |
| 100 | ~5,000 |
| 1,000 | ~500,000 |
| 10,000 | ~50,000,000 |

The work grows *very fast* as the list gets bigger. Selection Sort is practical only for small lists (a few hundred items at most).

---

## Part 2: Insertion Sort

### What is Insertion Sort?

**Insertion Sort** keeps a growing sorted region at the left of the list. It takes one value at a time from the unsorted region on the right and *inserts* it into the correct position in the sorted region.

The name says it all: you **insert** each element where it belongs.

> **Real-World Analogy:** Think of sorting a hand of playing cards. You pick up one card at a time from the table. For each new card you pick up, you look at your sorted hand from right to left, and slip the new card into the correct gap. This is exactly Insertion Sort.

---

### How Insertion Sort Works (Step-by-Step)

**Starting array:** `[7, 12, 9, 11, 3]`

**Step 1:** The first element `7` is already a "sorted section" of one.
```
Sorted: [7] | Unsorted: [12, 9, 11, 3]
```

**Step 2:** Take `12`. Is 12 > 7? Yes. So 12 stays in place.
```
Sorted: [7, 12] | Unsorted: [9, 11, 3]
```

**Step 3:** Take `9`. Is 9 > 12? No. Move 12 right. Is 9 > 7? Yes. Insert 9 before 12.
```
Sorted: [7, 9, 12] | Unsorted: [11, 3]
```

**Step 4:** Take `11`. Is 11 > 12? No. Move 12 right. Is 11 > 9? Yes. Insert 11 before 12.
```
Sorted: [7, 9, 11, 12] | Unsorted: [3]
```

**Step 5:** Take `3`. It's smaller than everything. Move 12, 11, 9, 7 all right. Insert 3 at the start.
```
Sorted: [3, 7, 9, 11, 12] ✅
```

---

### Simple Example: Basic Insertion Sort

```python
mylist = [64, 34, 25, 12, 22, 11, 90, 5]

n = len(mylist)

for i in range(1, n):          # start from index 1 (first is already "sorted")
    insert_index = i
    current_value = mylist.pop(i)    # remove the current element to insert

    for j in range(i - 1, -1, -1):  # scan the sorted part from right to left
        if mylist[j] > current_value:
            insert_index = j         # the current_value should go here or earlier

    mylist.insert(insert_index, current_value)   # put it in the right place

print(mylist)
```

**Expected Output:**
```
[5, 11, 12, 22, 25, 34, 64, 90]
```

Let's break down every piece:

| Code | Meaning |
|------|---------|
| `for i in range(1, n)` | We start from index 1; index 0 is already "sorted" (only 1 element) |
| `current_value = mylist.pop(i)` | Remove the next element from the unsorted region |
| `for j in range(i-1, -1, -1)` | Scan the sorted region from RIGHT to LEFT |
| `if mylist[j] > current_value` | If the sorted element is bigger, we need to go further left |
| `insert_index = j` | Keep updating where we'll insert |
| `mylist.insert(insert_index, current_value)` | Insert the element in the correct spot |

> **Thinking Prompt:** What if the current_value is bigger than everything in the sorted part? Walk through what happens to `insert_index`.

---

### The Hidden Shifting Problem (Again)

Just like Selection Sort, using `.pop()` and `.insert()` causes hidden shifting of elements in memory. If the array has 1,000 elements and we need to insert a small value at the beginning, all 999 other elements must slide one step to the right.

---

### Improved Insertion Sort: In-Place Shifting

Instead of removing and inserting, we copy the value we want to insert and then **shift elements one by one** to make space — stopping as soon as we find where the value belongs.

```python
mylist = [64, 34, 25, 12, 22, 11, 90, 5]

n = len(mylist)

for i in range(1, n):
    insert_index = i
    current_value = mylist[i]       # copy the value (don't remove it yet)

    for j in range(i - 1, -1, -1):
        if mylist[j] > current_value:
            mylist[j + 1] = mylist[j]   # shift this element one step to the right
            insert_index = j
        else:
            break                        # stop early — we found where it belongs

    mylist[insert_index] = current_value    # place the value in its correct spot

print(mylist)
```

**Expected Output:**
```
[5, 11, 12, 22, 25, 34, 64, 90]
```

**The key improvements:**
- `mylist[j + 1] = mylist[j]` — instead of shifting the whole array, we only shift elements one at a time, and stop (`break`) as soon as we no longer need to shift
- `mylist[insert_index] = current_value` — once we know exactly where the value belongs, place it there

> **Why does `break` help?** If we are inserting `50` into `[10, 20, 30, 40, 60, 70, 80]`, we only need to shift `60`, `70`, and `80`. As soon as we see `40 < 50`, we stop. Without `break`, we would check `40`, `30`, `20`, `10` unnecessarily.

---

### Insertion Sort Time Complexity

Like Selection Sort, Insertion Sort also has **O(n²)** average-case time complexity. On average, each of the `n` elements is compared against `n/2` other elements.

However, Insertion Sort has an important advantage:

- **Best Case (already sorted):** O(n) — it only needs to confirm each element is in place, so the inner loop almost never runs.
- **Worst Case (reverse sorted):** O(n²) — every element must travel all the way to the front.

This makes Insertion Sort much better than Bubble Sort or Selection Sort on **nearly-sorted data** — a common real-world scenario.

| Scenario | Time Complexity |
|---------|----------------|
| Best (sorted input) | O(n) |
| Average (random input) | O(n²) |
| Worst (reverse-sorted) | O(n²) |

---

## Part 3: Quicksort

### What is Quicksort?

**Quicksort** is one of the fastest sorting algorithms in practice. As the name suggests, it is genuinely quick.

The core idea:
1. Choose one element from the array called the **pivot**
2. Rearrange all other elements so that values **smaller than the pivot** are on its left, and values **larger than the pivot** are on its right
3. Now the pivot is in its **final correct position**
4. Repeat the same process **recursively** on the left sub-array and the right sub-array

The algorithm keeps dividing the problem in half until the sub-arrays are too small to sort (size 0 or 1), at which point they are already sorted.

> **Real-World Analogy:** Imagine sorting a pile of exam papers by grade. You pick one paper as your "pivot grade." You put all papers below that grade on the left pile, and all papers above it on the right pile. Then you do the same thing for each pile, and each sub-pile, until all piles are too small to need sorting. The final arrangement is in order.

---

### Understanding Recursion in Quicksort

Before seeing the code, let us make sure recursion makes sense.

A recursive function solves a big problem by solving smaller versions of the *same problem*. It needs two things:
1. A **base case**: the simplest possible input where we just return (e.g., a list of 0 or 1 elements is already sorted)
2. A **recursive case**: split the problem and call itself on the smaller pieces

```python
# Example: recursively count down
def countdown(n):
    if n <= 0:          # base case: stop here
        print("Blastoff!")
        return
    print(n)
    countdown(n - 1)    # recursive case: call itself with a smaller value

countdown(4)
```

**Output:**
```
4
3
2
1
Blastoff!
```

Quicksort works the same way — it calls itself on smaller and smaller sub-arrays until they are all sorted.

---

### How Quicksort Works (Step-by-Step)

**Starting array:** `[11, 9, 12, 7, 3]`

We choose the **last element** as the pivot: `3`

**Step 1:** All other values (11, 9, 12, 7) are greater than 3. Since 3 is the smallest, everything must go to its right. Swap 3 with the first element 11:
```
[3, 9, 12, 7, 11]
```
3 is now in its **final position**!

**Step 2:** Now sort `[9, 12, 7, 11]` to the right of 3. Choose `11` as pivot.
- 7 is less than 11 → goes left
- 9 is less than 11 → goes left
- 12 is greater than 11 → goes right
- After rearranging: `[9, 7, 11, 12]`
- 11 is in its **final position**!

**Step 3:** Sort `[9, 7]`. Choose `7` as pivot. 9 > 7, so swap:
```
[7, 9]
```
Both are in final position!

**Final sorted array:** `[3, 7, 9, 11, 12]` ✅

---

### Quicksort Code in Python

Quicksort needs two functions working together:
- `partition()` — rearranges values around a pivot
- `quicksort()` — recursively calls itself on sub-arrays

```python
def partition(array, low, high):
    pivot = array[high]     # choose the last element as pivot
    i = low - 1             # i tracks the "boundary" of smaller elements

    for j in range(low, high):        # scan from low to high-1
        if array[j] <= pivot:         # if current element is <= pivot
            i += 1                    # expand the "smaller" region
            array[i], array[j] = array[j], array[i]   # swap it in

    # Place the pivot between the two regions
    array[i + 1], array[high] = array[high], array[i + 1]
    return i + 1                      # return pivot's final index


def quicksort(array, low=0, high=None):
    if high is None:
        high = len(array) - 1         # initialise high on first call

    if low < high:                    # base case: if 0 or 1 elements, stop
        pivot_index = partition(array, low, high)   # partition and get pivot position
        quicksort(array, low, pivot_index - 1)      # sort the LEFT sub-array
        quicksort(array, pivot_index + 1, high)     # sort the RIGHT sub-array


mylist = [64, 34, 25, 5, 22, 11, 90, 12]
quicksort(mylist)
print(mylist)
```

**Expected Output:**
```
[5, 11, 12, 22, 25, 34, 64, 90]
```

### Line-by-Line Explanation of `partition()`

```python
pivot = array[high]
```
We pick the last element as the pivot. (Other choices are possible — first element, random element, etc.)

```python
i = low - 1
```
`i` is a pointer that tracks the rightmost position of the "smaller than pivot" region. It starts just *before* the region begins.

```python
for j in range(low, high):
    if array[j] <= pivot:
        i += 1
        array[i], array[j] = array[j], array[i]
```
We scan every element from `low` to `high-1`. If an element is ≤ pivot, we expand the "smaller" region (move `i` right) and swap that element into it.

```python
array[i + 1], array[high] = array[high], array[i + 1]
return i + 1
```
After scanning everything, we place the pivot itself at position `i+1` — exactly between the "smaller" and "larger" regions. This is its final sorted position.

### Line-by-Line Explanation of `quicksort()`

```python
if low < high:
```
Base case: if `low` equals or exceeds `high`, there are 0 or 1 elements — already sorted.

```python
pivot_index = partition(array, low, high)
quicksort(array, low, pivot_index - 1)
quicksort(array, pivot_index + 1, high)
```
After partitioning, the pivot is in place. We recursively sort everything to its left and everything to its right.

> **Thinking Prompt:** After `partition()` runs, can the pivot ever move again? Why or why not?

---

### Quicksort Time Complexity

| Scenario | Time Complexity | When It Happens |
|---------|----------------|----------------|
| Best Case | O(n log n) | Pivot always splits array in half |
| Average Case | O(n log n) | Random data — very common |
| Worst Case | O(n²) | Array is already sorted; pivot is always smallest or largest |

The **average case** of O(n log n) is what makes Quicksort so popular in practice. It is dramatically faster than Selection Sort or Insertion Sort for large datasets.

**Why is O(n log n) better than O(n²)?**

| n | O(n²) operations | O(n log n) operations |
|---|-----------------|----------------------|
| 1,000 | 1,000,000 | ~10,000 |
| 1,000,000 | 1,000,000,000,000 | ~20,000,000 |

Quicksort handles a million items with about 20 million operations. Selection Sort would need a **trillion** operations for the same task. The difference is enormous.

---

## Part 4: Counting Sort

### What is Counting Sort?

All the sorting algorithms we have studied so far work by **comparing** values to each other: "Is this bigger than that?" But Counting Sort takes a completely different approach — it **counts** how many times each value appears.

Instead of rearranging the original elements by comparing them, Counting Sort:
1. Creates a "count array" where position `i` stores how many times the value `i` appears in the input
2. Uses those counts to reconstruct a perfectly sorted array

> **Real-World Analogy:** Imagine you have a bag of coloured balls — some red (value 1), some blue (value 2), some green (value 3). Instead of sorting them by comparing each ball to another, you simply count: "3 red, 5 blue, 2 green." Then you put them back in order: put all 3 red ones first, then 5 blue, then 2 green. Done — and you never needed to compare red to blue!

---

### Conditions for Counting Sort

Counting Sort only works properly when:

1. **Values must be non-negative integers** — because we use each value as an *index* in the count array. A negative index would be outside the array.

2. **Values must have a limited range** — if your values can be anywhere from 0 to 1,000,000, the count array needs 1,000,001 positions, which wastes memory. Counting Sort works best when the range of values (`k`) is small compared to the number of values (`n`).

> **Good use case:** Sorting 10,000 test scores all between 0 and 100. (k=101 is tiny compared to n=10,000)

> **Bad use case:** Sorting 10 phone numbers. (k could be up to 9,999,999,999 — a huge count array for just 10 numbers)

---

### How Counting Sort Works (Step-by-Step)

**Starting array:** `[2, 3, 0, 2, 3, 2]`
Values range from 0 to 3, so our count array has 4 positions (indices 0, 1, 2, 3).

**Step 1:** Create an empty count array:
```
countArray = [0, 0, 0, 0]
#index:        0  1  2  3
```

**Step 2:** Go through each value in the original array and increment the count at that index.

- Value 2 → `countArray[2] += 1` → `[0, 0, 1, 0]`
- Value 3 → `countArray[3] += 1` → `[0, 0, 1, 1]`
- Value 0 → `countArray[0] += 1` → `[1, 0, 1, 1]`
- Value 2 → `countArray[2] += 1` → `[1, 0, 2, 1]`
- Value 3 → `countArray[3] += 1` → `[1, 0, 2, 2]`
- Value 2 → `countArray[2] += 1` → `[1, 0, 3, 2]`

**Final count array:** `[1, 0, 3, 2]`

This tells us: there is 1 zero, 0 ones, 3 twos, and 2 threes.

**Step 3:** Rebuild the sorted array from the count array:
- `countArray[0] = 1` → add one `0` → `[0]`
- `countArray[1] = 0` → add no `1`s → `[0]`
- `countArray[2] = 3` → add three `2`s → `[0, 2, 2, 2]`
- `countArray[3] = 2` → add two `3`s → `[0, 2, 2, 2, 3, 3]`

**Sorted array:** `[0, 2, 2, 2, 3, 3]` ✅

---

### Simple Example: Counting Sort in Python

```python
def countingSort(arr):
    max_val = max(arr)              # find the highest value
    count = [0] * (max_val + 1)    # create count array of size max_val+1, all zeros

    while len(arr) > 0:
        num = arr.pop(0)            # take one value from the input array
        count[num] += 1             # increment its count

    for i in range(len(count)):    # go through every possible value
        while count[i] > 0:        # as many times as it appears
            arr.append(i)          # add that value to the sorted array
            count[i] -= 1          # decrement the count

    return arr


mylist = [4, 2, 2, 6, 3, 3, 1, 6, 5, 2, 3]
mysortedlist = countingSort(mylist)
print(mysortedlist)
```

**Expected Output:**
```
[1, 2, 2, 2, 3, 3, 3, 4, 5, 6, 6]
```

### Line-by-Line Explanation

```python
max_val = max(arr)
```
Find the largest value. We need this to know how big to make the count array.

```python
count = [0] * (max_val + 1)
```
Create a count array filled with zeros. The `+1` is because we need indices from 0 up to and including `max_val`. For example, if `max_val` is 6, we need indices 0, 1, 2, 3, 4, 5, 6 — that's 7 positions.

```python
while len(arr) > 0:
    num = arr.pop(0)
    count[num] += 1
```
Remove each element from the input array and record its count. `arr.pop(0)` removes the first element and returns it.

```python
for i in range(len(count)):
    while count[i] > 0:
        arr.append(i)
        count[i] -= 1
```
Rebuild the sorted array. For each index `i`, add the value `i` exactly `count[i]` times.

> **What happens if all values are the same?** Try `[3, 3, 3, 3]`. What does the count array look like?

---

### Counting Sort Time Complexity

The time complexity of Counting Sort depends on two things:
- `n` — the number of values to sort
- `k` — the range of possible values (highest value + 1)

| Scenario | Time Complexity |
|---------|----------------|
| General | O(n + k) |
| Best case (k is tiny) | O(n) — practically linear! |
| Worst case (k >> n) | Can approach O(n²) or worse |

**Why O(n + k)?** The algorithm has two phases:
- Phase 1 (counting): visits `n` elements → O(n)
- Phase 2 (rebuilding): visits `k` positions in the count array → O(k)
- Total: O(n + k)

When `k` is small compared to `n`, this is very fast. When `k` is much larger than `n`, it becomes slow and memory-wasteful.

---

## Part 5: Radix Sort

### What is Radix Sort?

**Radix Sort** is an advanced sorting algorithm that extends the idea of Counting Sort. It sorts integers by processing them **one digit at a time**, starting from the **least significant digit** (the units column) and working towards the most significant digit (the thousands column, etc.).

The word **"radix"** means "base." In the normal decimal number system (base 10), there are 10 possible digits: 0 through 9. Radix Sort uses 10 **buckets** (one for each digit) to group numbers by their current digit, then collects them back in order.

> **Real-World Analogy:** Imagine sorting 100 library books by their 3-digit code. First, sort all books by the last digit of their code (units) into 10 piles (pile 0, pile 1, ..., pile 9). Collect the piles in order. Next, sort by the middle digit (tens) into 10 piles and collect again. Finally, sort by the first digit (hundreds). After three passes, all books are in perfect order — without ever comparing two books to each other!

---

### Why Does Starting from the Rightmost Digit Work?

This seems counterintuitive at first. Why start from the *least* important digit?

The answer: because we sort in a **stable** way (elements with the same digit keep their relative order from previous rounds). By the time we sort on the most significant digit, all the finer distinctions (units, tens) are already correctly ordered within each group.

Think of it like sorting by last name, then first name. If you first sort alphabetically by first name in a stable way, and then sort by last name in a stable way, people with the same last name will be ordered by first name — exactly what you want.

---

### What is Stable Sorting?

A sorting algorithm is **stable** if elements with equal values maintain their original relative order after sorting.

**Example:** Consider `[3a, 1, 3b, 2]` where `3a` and `3b` both have value 3, but `3a` came first.

- **Stable sort result:** `[1, 2, 3a, 3b]` — `3a` still comes before `3b`
- **Unstable sort result:** `[1, 2, 3b, 3a]` — the order of equal elements is mixed up

Radix Sort **requires** stable sorting within each digit pass, or the result will be incorrect. When we process the tens digit, we must not disturb the work done on the units digit.

---

### How Radix Sort Works (Step-by-Step)

**Starting array:** `[33, 45, 40, 25, 17, 24]`

**Pass 1: Sort by units digit (rightmost)**

Examine the units digit of each number:
- 33 → units digit is **3**
- 45 → units digit is **5**
- 40 → units digit is **0**
- 25 → units digit is **5**
- 17 → units digit is **7**
- 24 → units digit is **4**

Place each number in the corresponding bucket (0 through 9):
```
Bucket 0: [40]
Bucket 1: []
Bucket 2: []
Bucket 3: [33]
Bucket 4: [24]
Bucket 5: [45, 25]    ← both have units digit 5; 45 came first, so stays first (stable)
Bucket 6: []
Bucket 7: [17]
Bucket 8: []
Bucket 9: []
```

Collect from buckets in order (bucket 0 first, then 1, etc.):
```
[40, 33, 24, 45, 25, 17]
```

**Pass 2: Sort by tens digit**

Examine the tens digit:
- 40 → tens digit is **4**
- 33 → tens digit is **3**
- 24 → tens digit is **2**
- 45 → tens digit is **4**
- 25 → tens digit is **2**
- 17 → tens digit is **1**

Place in buckets:
```
Bucket 1: [17]
Bucket 2: [24, 25]   ← 24 came before 25 in the list, and stays that way (stable!)
Bucket 3: [33]
Bucket 4: [40, 45]
```

Collect from buckets:
```
[17, 24, 25, 33, 40, 45]  ✅ Sorted!
```

Notice that `24` correctly comes before `25`, and `40` correctly comes before `45`, because we preserved the order from Pass 1 (stable sorting).

---

### Radix Sort Code in Python

```python
mylist = [170, 45, 75, 90, 802, 24, 2, 66]
print("Original array:", mylist)

radixArray = [[], [], [], [], [], [], [], [], [], []]   # 10 buckets for digits 0-9
maxVal = max(mylist)    # find the largest value
exp = 1                 # start with the units digit (10^0 = 1)

while maxVal // exp > 0:    # keep going as long as there are digits to process

    while len(mylist) > 0:
        val = mylist.pop()               # take a value from the back of the list
        radixIndex = (val // exp) % 10  # find the current digit
        radixArray[radixIndex].append(val)   # put it in the right bucket

    for bucket in radixArray:
        while len(bucket) > 0:
            val = bucket.pop()       # take from the END of bucket (stable!)
            mylist.append(val)       # add to the beginning of rebuilt list

    exp *= 10    # move to the next digit (tens, hundreds, ...)

print(mylist)
```

**Expected Output:**
```
Original array: [170, 45, 75, 90, 802, 24, 2, 66]
[2, 24, 45, 66, 75, 90, 170, 802]
```

### Line-by-Line Explanation

```python
radixArray = [[], [], [], [], [], [], [], [], [], []]
```
Ten empty buckets — one for each possible digit (0 through 9).

```python
maxVal = max(mylist)
exp = 1
```
We need to know how many digit positions to process. `exp` starts at 1 (units), then becomes 10 (tens), 100 (hundreds), etc.

```python
while maxVal // exp > 0:
```
This loop runs once per digit. For `maxVal = 802`:
- When `exp = 1`: `802 // 1 = 802 > 0` ✅
- When `exp = 10`: `802 // 10 = 80 > 0` ✅
- When `exp = 100`: `802 // 100 = 8 > 0` ✅
- When `exp = 1000`: `802 // 1000 = 0`, so loop stops ✅

```python
val = mylist.pop()
radixIndex = (val // exp) % 10
```
This extracts the digit at the current position. Let's trace for `val = 170` when `exp = 10`:
- `170 // 10 = 17`
- `17 % 10 = 7`
- So the tens digit of 170 is **7** → goes into bucket 7 ✅

```python
for bucket in radixArray:
    while len(bucket) > 0:
        val = bucket.pop()
        mylist.append(val)
```
We collect values from all buckets in order (bucket 0 first, then 1, then 2, ...). Using `.pop()` takes from the END of each bucket, which maintains stability.

```python
exp *= 10
```
Move to the next digit position.

---

### Radix Sort with Bubble Sort as the Underlying Sorter

Radix Sort can actually use any stable sorting algorithm to sort within each bucket. Here is a version that uses Bubble Sort:

```python
def bubbleSort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]


def radixSortWithBubbleSort(arr):
    max_val = max(arr)
    exp = 1

    while max_val // exp > 0:
        radixList = [[], [], [], [], [], [], [], [], [], []]

        for num in arr:
            radixIndex = (num // exp) % 10
            radixList[radixIndex].append(num)

        for bucket in radixList:
            bubbleSort(bucket)    # sort within each bucket

        i = 0
        for bucket in radixList:
            for num in bucket:
                arr[i] = num
                i += 1

        exp *= 10


mylist = [170, 45, 75, 90, 802, 24, 2, 66]
radixSortWithBubbleSort(mylist)
print(mylist)
```

**Expected Output:**
```
[2, 24, 45, 66, 75, 90, 170, 802]
```

---

### Radix Sort Time Complexity

| Scenario | Time Complexity | Details |
|---------|----------------|---------|
| Best Case | O(n) | Many values, few digits (k is tiny) |
| Average Case | O(n · log n) | k ≈ log n digits |
| Worst Case | O(n²) | As many digits as there are values |

The formal complexity is **O(n · k)** where:
- `n` = number of values to sort
- `k` = number of digits in the largest value

**Example scenarios:**

- 1,000,000 values, all ≤ 999 (3 digits): `O(n · 3) ≈ O(n)` — super fast!
- 1,000 values, largest is a 1,000-digit number: `O(n · 1000) ≈ O(n²)` — slow

Radix Sort is most effective when `k` is small relative to `n`.

---

## Guided Practice Exercises

### Exercise 1: Trace Selection Sort by Hand

**Objective:** Understand Selection Sort deeply by tracing it without code.

**Scenario:** You are a librarian sorting 5 books by page count. The page counts are: `[320, 150, 280, 90, 410]`

**Instructions:**
1. Draw the array at the start
2. For each pass of Selection Sort, find the minimum and mark where it goes
3. Show the array after each pass
4. Count how many swaps were needed in total

**Steps:**
- Pass 1: Minimum = ? Swap positions ? and ?
- Pass 2: Minimum = ? Swap positions ? and ?
- Pass 3: Minimum = ? Swap positions ? and ?
- Pass 4: Minimum = ? Swap positions ? and ?

**Expected Final Array:** `[90, 150, 280, 320, 410]`

**Self-check Questions:**
- How many comparisons did you make in Pass 1?
- Did any pass require zero swaps? Why?
- What would change if the array was already sorted?

---

### Exercise 2: Trace Insertion Sort by Hand

**Objective:** Build intuition for how Insertion Sort grows its sorted region.

**Scenario:** You are a nurse recording patient temperatures: `[38.5, 37.0, 39.2, 36.8, 40.1]`

**Instructions:** Sort the temperatures from lowest to highest using Insertion Sort.

Show the sorted and unsorted portions after each step:

| Step | Value Being Inserted | Sorted Region | Unsorted Region |
|------|---------------------|--------------|----------------|
| Start | — | `[38.5]` | `[37.0, 39.2, 36.8, 40.1]` |
| 1 | 37.0 | `[?, ?]` | `[39.2, 36.8, 40.1]` |
| 2 | 39.2 | `[?, ?, ?]` | `[36.8, 40.1]` |
| 3 | 36.8 | `[?, ?, ?, ?]` | `[40.1]` |
| 4 | 40.1 | `[?, ?, ?, ?, ?]` | `[]` |

**Expected Final Array:** `[36.8, 37.0, 38.5, 39.2, 40.1]`

---

### Exercise 3: Run and Modify Quicksort

**Objective:** Understand how the pivot choice affects Quicksort.

**Warm-up:** Run this code and verify the output:

```python
def partition(array, low, high):
    pivot = array[high]
    i = low - 1
    for j in range(low, high):
        if array[j] <= pivot:
            i += 1
            array[i], array[j] = array[j], array[i]
    array[i + 1], array[high] = array[high], array[i + 1]
    return i + 1

def quicksort(array, low=0, high=None):
    if high is None:
        high = len(array) - 1
    if low < high:
        pivot_index = partition(array, low, high)
        quicksort(array, low, pivot_index - 1)
        quicksort(array, pivot_index + 1, high)

scores = [88, 45, 72, 91, 33, 67, 55, 82]
quicksort(scores)
print(scores)
```

**Expected Output:**
```
[33, 45, 55, 67, 72, 82, 88, 91]
```

**What-If Challenges:**
1. What if the input is already sorted: `[1, 2, 3, 4, 5]`? How many partition calls happen? Is this the best or worst case?
2. What if all elements are the same: `[7, 7, 7, 7]`? Does the code still work?
3. What if there is only one element: `[42]`? Trace through what happens.

---

### Exercise 4: Counting Sort on Student Grades

**Objective:** Use Counting Sort on a real-world dataset.

**Scenario:** You have 15 student grades, all between 1 and 5 stars: `[3, 1, 4, 1, 5, 2, 3, 2, 4, 5, 1, 3, 2, 4, 3]`

**Step 1:** Count how many of each grade there are:

| Grade | Count |
|-------|-------|
| 1 | ? |
| 2 | ? |
| 3 | ? |
| 4 | ? |
| 5 | ? |

**Step 2:** Verify using code:

```python
def countingSort(arr):
    max_val = max(arr)
    count = [0] * (max_val + 1)

    while len(arr) > 0:
        num = arr.pop(0)
        count[num] += 1

    for i in range(len(count)):
        while count[i] > 0:
            arr.append(i)
            count[i] -= 1

    return arr

grades = [3, 1, 4, 1, 5, 2, 3, 2, 4, 5, 1, 3, 2, 4, 3]
sorted_grades = countingSort(grades)
print(sorted_grades)
```

**Expected Output:**
```
[1, 1, 1, 2, 2, 2, 3, 3, 3, 3, 4, 4, 4, 5, 5]
```

**Self-check:** Could you use Counting Sort on decimal grades like `[3.5, 4.2, 2.8]`? Why or why not?

---

### Exercise 5: Radix Sort Digit Tracing

**Objective:** Trace the digit extraction formula manually.

For each number below, calculate the units digit and the tens digit using the formula `(val // exp) % 10`:

| Number | `(val // 1) % 10` (Units) | `(val // 10) % 10` (Tens) | `(val // 100) % 10` (Hundreds) |
|--------|--------------------------|--------------------------|-------------------------------|
| 170 | ? | ? | ? |
| 45 | ? | ? | ? |
| 802 | ? | ? | ? |
| 24 | ? | ? | ? |
| 2 | ? | ? | ? |

**Verify with Python:**

```python
numbers = [170, 45, 802, 24, 2]
for val in numbers:
    units    = (val // 1)   % 10
    tens     = (val // 10)  % 10
    hundreds = (val // 100) % 10
    print(f"{val}: units={units}, tens={tens}, hundreds={hundreds}")
```

**Expected Output:**
```
170: units=0, tens=7, hundreds=1
45: units=5, tens=4, hundreds=0
802: units=2, tens=0, hundreds=8
24: units=4, tens=2, hundreds=0
2: units=2, tens=0, hundreds=0
```

---

## Mini Project: Student Score Sorter

Now let's combine everything into a realistic mini project. You will build a programme that can sort a class of students' scores using multiple algorithms and compare the results.

### Project Brief

**Scenario:** You are a data analyst for a school. You receive a list of 20 student final exam scores (whole numbers between 0 and 100). You need to sort them and provide a report showing the sorted scores and which algorithm was used.

---

### Stage 1: Setup — Generate the Data

```python
import random

# Generate 20 random scores between 0 and 100
random.seed(42)    # seed makes results reproducible
scores = [random.randint(0, 100) for _ in range(20)]
print("Original scores:", scores)
```

**Expected Output (with seed 42):**
```
Original scores: [2, 79, 26, 75, 8, 69, 21, 11, 75, 63, 52, 76, 29, 24, 34, 53, 27, 64, 12, 6]
```

---

### Stage 2: Core Logic — Implement All Four Algorithms

```python
# --- Selection Sort ---
def selection_sort(arr):
    arr = arr[:]          # create a copy so we don't modify the original
    n = len(arr)
    for i in range(n):
        min_index = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_index]:
                min_index = j
        arr[i], arr[min_index] = arr[min_index], arr[i]
    return arr


# --- Insertion Sort ---
def insertion_sort(arr):
    arr = arr[:]
    n = len(arr)
    for i in range(1, n):
        insert_index = i
        current_value = arr[i]
        for j in range(i - 1, -1, -1):
            if arr[j] > current_value:
                arr[j + 1] = arr[j]
                insert_index = j
            else:
                break
        arr[insert_index] = current_value
    return arr


# --- Quicksort ---
def _partition(arr, low, high):
    pivot = arr[high]
    i = low - 1
    for j in range(low, high):
        if arr[j] <= pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1

def quicksort(arr, low=0, high=None):
    arr = arr[:] if high is None else arr    # copy only on first call
    if high is None:
        high = len(arr) - 1
        result = arr[:]
        _quicksort_inplace(result, 0, high)
        return result
    return arr

def _quicksort_inplace(arr, low, high):
    if low < high:
        pivot_index = _partition(arr, low, high)
        _quicksort_inplace(arr, low, pivot_index - 1)
        _quicksort_inplace(arr, pivot_index + 1, high)


# --- Counting Sort ---
def counting_sort(arr):
    arr = arr[:]
    max_val = max(arr)
    count = [0] * (max_val + 1)
    for num in arr:
        count[num] += 1
    result = []
    for i in range(len(count)):
        result.extend([i] * count[i])
    return result
```

---

### Stage 3: Enhancements — Run and Compare

```python
import random
random.seed(42)
scores = [random.randint(0, 100) for _ in range(20)]

print("=" * 50)
print("STUDENT SCORE SORTING REPORT")
print("=" * 50)
print(f"\nOriginal scores ({len(scores)} students):")
print(scores)
print()

# Run all sorting algorithms
sel_sorted = selection_sort(scores)
ins_sorted = insertion_sort(scores)
count_sorted = counting_sort(scores)

# Quicksort (in-place version)
quick_arr = scores[:]
_quicksort_inplace(quick_arr, 0, len(quick_arr) - 1)

print("Selection Sort result:  ", sel_sorted)
print("Insertion Sort result:  ", ins_sorted)
print("Quicksort result:       ", quick_arr)
print("Counting Sort result:   ", count_sorted)

# Milestone output: statistics on sorted data
print("\n--- ANALYSIS ---")
print(f"Lowest score:   {sel_sorted[0]}")
print(f"Highest score:  {sel_sorted[-1]}")
print(f"Median score:   {sel_sorted[len(sel_sorted)//2]}")
print(f"Students >= 50: {sum(1 for s in sel_sorted if s >= 50)}")
print(f"Students < 50:  {sum(1 for s in sel_sorted if s < 50)}")
```

**Expected Output (example):**
```
==================================================
STUDENT SCORE SORTING REPORT
==================================================

Original scores (20 students):
[2, 79, 26, 75, 8, 69, 21, 11, 75, 63, 52, 76, 29, 24, 34, 53, 27, 64, 12, 6]

Selection Sort result:   [2, 6, 8, 11, 12, 21, 24, 26, 27, 29, 34, 52, 53, 63, 64, 69, 75, 75, 76, 79]
Insertion Sort result:   [2, 6, 8, 11, 12, 21, 24, 26, 27, 29, 34, 52, 53, 63, 64, 69, 75, 75, 76, 79]
Quicksort result:        [2, 6, 8, 11, 12, 21, 24, 26, 27, 29, 34, 52, 53, 63, 64, 69, 75, 75, 76, 79]
Counting Sort result:    [2, 6, 8, 11, 12, 21, 24, 26, 27, 29, 34, 52, 53, 63, 64, 69, 75, 75, 76, 79]

--- ANALYSIS ---
Lowest score:   2
Highest score:  79
Median score:   34
Students >= 50: 9
Students < 50:  11
```

**Reflection Questions:**
- All four algorithms produced the same sorted list. Why?
- Which algorithm would you trust most for 10 million scores? Why?
- Could you use Counting Sort if scores could be 0 to 999? What about 0 to 9,999,999?

---

### Stage 4: Advanced Extension — Add Radix Sort

Try adding Radix Sort to the report:

```python
def radix_sort(arr):
    arr = arr[:]
    radix_array = [[] for _ in range(10)]
    max_val = max(arr)
    exp = 1

    while max_val // exp > 0:
        while len(arr) > 0:
            val = arr.pop()
            radix_index = (val // exp) % 10
            radix_array[radix_index].append(val)

        for bucket in radix_array:
            while len(bucket) > 0:
                val = bucket.pop()
                arr.append(val)

        exp *= 10

    return arr

# Test it:
test = [170, 45, 75, 90, 802, 24, 2, 66]
print("Radix Sort:", radix_sort(test))
```

**Expected Output:**
```
Radix Sort: [2, 24, 45, 66, 75, 90, 170, 802]
```

---

## Common Beginner Mistakes

### Mistake 1: Off-By-One Error in Selection Sort

❌ **Wrong:**
```python
for i in range(n):       # outer loop
    for j in range(i, n):   # inner loop starts at i, not i+1
```

When `j` starts at `i`, the algorithm compares an element with itself, which wastes a comparison and can cause issues.

✅ **Correct:**
```python
for i in range(n):
    min_index = i
    for j in range(i + 1, n):   # start one position AFTER i
```

---

### Mistake 2: Forgetting the `break` in Improved Insertion Sort

❌ **Wrong:**
```python
for j in range(i - 1, -1, -1):
    if arr[j] > current_value:
        arr[j + 1] = arr[j]
        insert_index = j
    # No break! The loop continues even after finding the right spot
```

This means even after finding where `current_value` belongs, the algorithm keeps checking smaller indices unnecessarily. It still gives the right answer, but wastes time.

✅ **Correct:**
```python
for j in range(i - 1, -1, -1):
    if arr[j] > current_value:
        arr[j + 1] = arr[j]
        insert_index = j
    else:
        break    # stop as soon as we've gone past where it belongs
```

---

### Mistake 3: Using Counting Sort with Negative or Float Values

❌ **Wrong:**
```python
arr = [-5, 3, 1, -2, 4]
max_val = max(arr)          # max_val = 4
count = [0] * (max_val + 1) # creates [0, 0, 0, 0, 0]

for num in arr:
    count[num] += 1     # ERROR! count[-5] is index -5, which is index 0 in Python
                        # This causes incorrect behaviour (not a crash, but wrong results)
```

✅ **Correct:** Only use Counting Sort on non-negative integers. If you have negative values, you need to shift them first or use a different algorithm.

---

### Mistake 4: Modifying the Original List in Sorting Functions

❌ **Wrong:**
```python
def selection_sort(arr):
    n = len(arr)
    for i in range(n):
        ...    # This modifies arr directly

original = [3, 1, 2]
sorted_list = selection_sort(original)
print(original)    # [1, 2, 3] — the original was changed too!
```

✅ **Correct:** Make a copy first:
```python
def selection_sort(arr):
    arr = arr[:]    # create a copy
    n = len(arr)
    ...
```

---

### Mistake 5: Quicksort Stack Overflow on Very Large Sorted Input

Quicksort is recursive. If the input is already sorted and you always pick the last element as the pivot, the algorithm degrades to O(n²) and makes `n` recursive calls. For very large inputs, Python may run out of "call stack" space and crash.

✅ **Solutions:**
- Randomly shuffle the input before sorting
- Choose a random pivot instead of always the last element
- Use Python's built-in `sorted()` for large datasets, which uses Timsort — a hybrid algorithm that handles these cases gracefully

---

### Mistake 6: Forgetting That Radix Sort Requires Stable Sorting

If you implement the inner sorting step of Radix Sort in an unstable way (e.g., picking elements from the wrong end of buckets), the final result may be incorrectly ordered even though each pass appears to work.

✅ **Always test:** After Radix Sort, verify that the output is identical to what `sorted()` would produce for the same input.

---

## Reflection Questions

1. **Selection Sort** always makes the same number of comparisons regardless of whether the input is sorted or random. Why is this? Is this a strength or a weakness?

2. **Insertion Sort** performs very well on nearly-sorted data. Can you think of a real-world scenario where data is almost always nearly sorted? (Hint: think about stock prices each day, or a to-do list where you add new tasks to the end.)

3. **Quicksort** is on average much faster than Selection and Insertion Sort, yet those simpler sorts still appear in many textbooks and real applications. When might you prefer Selection Sort over Quicksort?

4. **Counting Sort** does not compare elements at all. How is it possible to sort correctly without ever comparing values? What does this tell us about the difference between "comparison-based" and "non-comparison-based" sorting algorithms?

5. **Radix Sort** requires stable sorting at each digit pass. Try to explain *why* in your own words, using a specific example of what would go wrong if the sorting were unstable.

6. If you needed to sort one billion phone numbers (10 digits each), which algorithm from this lesson would you choose and why?

7. The O(n log n) vs O(n²) difference seems abstract. If one algorithm takes 1 second for 1,000 elements, how long would it take for 1,000,000 elements under O(n²)? Under O(n log n)?

---

## Completion Checklist

Go through each item and tick it off when you are confident:

- [ ] I can explain Selection Sort using a real-world analogy
- [ ] I can explain why swapping is better than remove-and-insert in Selection Sort
- [ ] I can explain Insertion Sort using a real-world analogy
- [ ] I understand why `break` in improved Insertion Sort is an optimisation
- [ ] I can explain what a "pivot" is in Quicksort
- [ ] I understand why Quicksort uses recursion
- [ ] I can trace through the `partition()` function on a small array
- [ ] I can explain why Counting Sort only works on non-negative integers with a limited range
- [ ] I understand what the count array represents and how it is used to rebuild the sorted array
- [ ] I can explain what the radix (base) is and how Radix Sort uses buckets
- [ ] I understand what "stable sorting" means and why Radix Sort requires it
- [ ] I can extract any digit from a number using `(val // exp) % 10`
- [ ] I can write all five algorithms from scratch (or close to it)
- [ ] I understand when to use each algorithm (strengths and limitations)
- [ ] I completed at least 3 of the 5 exercises
- [ ] I completed at least Stage 1–3 of the mini project

---

## Lesson Summary

In this lesson, you learned five important sorting algorithms, each with a different strategy:

**Selection Sort (O(n²)):** Repeatedly finds the minimum value in the unsorted portion and moves it to the front using a swap. Simple to understand, but slow for large datasets. The swapping version avoids expensive memory shifting operations.

**Insertion Sort (O(n²) average, O(n) best):** Builds a sorted region from left to right by inserting each new element into its correct position. The optimised version shifts elements rather than removing and reinserting, and uses `break` to stop early. Excellent on nearly-sorted data.

**Quicksort (O(n log n) average):** A divide-and-conquer algorithm that selects a pivot, partitions the array around it, and recursively sorts both sides. Much faster than the previous two on large, random datasets. Can degrade to O(n²) on already-sorted data if the pivot choice is poor.

**Counting Sort (O(n + k)):** A non-comparison algorithm that counts occurrences of each value and rebuilds the sorted array from those counts. Extremely fast when the range of values is small, but only works on non-negative integers and becomes inefficient when the value range is large.

**Radix Sort (O(n · k)):** Sorts integers digit by digit, starting from the least significant digit. Requires stable sorting at each digit pass to preserve the order established by previous passes. Very efficient for large sets of integers with few digits.

**Quick Reference: Which Algorithm to Choose**

| Situation | Best Algorithm |
|-----------|---------------|
| Small list (< 100 items) | Insertion Sort |
| Nearly-sorted data | Insertion Sort |
| Large random data, general use | Quicksort |
| Integer data, small value range | Counting Sort |
| Large integer dataset, limited digit count | Radix Sort |
| Need guaranteed performance, not to code yourself | Python's built-in `sorted()` (Timsort) |

---

*Lesson 37 complete. You now have a thorough understanding of five foundational sorting algorithms, their Python implementations, and the reasoning behind when to use each one.*
