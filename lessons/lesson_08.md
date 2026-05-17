---
render_with_liquid: false
title: "Lesson 08 – Python Lists Advanced: Looping, Comprehensions, Sorting, Copying, Joining & Methods"
nav_order: 8
---

# Lesson 08 – Python Lists Advanced: Looping, Comprehensions, Sorting, Copying, Joining & Methods

---

## Lesson Introduction

Welcome to **Lesson 08** — one of the most practically powerful lessons in your Python journey.

In earlier lessons you learned what a list is, how to create one, and how to read or change items inside it. Now you are going to learn **how to do things with entire lists** — how to move through every item automatically, how to build brand-new lists from scratch in one line, how to put lists in order, how to make safe copies, how to combine two lists together, and how to use Python's built-in list toolbox.

By the end of this lesson you will be able to:

- Loop through every item in a list automatically using `for` and `while`
- Build new lists in one elegant line using **list comprehensions**
- Sort a list alphabetically, numerically, in reverse, or using a custom rule
- Copy a list safely so changes to one copy do not accidentally affect the other
- Join two or more lists together
- Use all of Python's built-in list methods (`append`, `remove`, `pop`, `count`, `index`, and more)
- Build a realistic mini-project combining all of these skills

There is **no assumed prior knowledge** beyond knowing that a list is a collection of items written in square brackets. Every new term will be explained from scratch.

---

## Prerequisite Concepts (Read This First)

Before diving in, let's make sure you are comfortable with three small ideas that appear constantly in this lesson.

### What Is a List? (Quick Reminder)

A **list** in Python is a container that holds multiple values in a specific order. Each value has a numbered position called an **index**, starting from `0`.

```python
fruits = ["apple", "banana", "cherry"]
#          index 0   index 1   index 2
```

You can access one item by writing `fruits[0]` (gives `"apple"`).

### What Is a Loop?

A **loop** is a Python instruction that says: *"repeat these lines of code multiple times automatically."*

Without loops, to print three fruits you would write:

```python
print(fruits[0])
print(fruits[1])
print(fruits[2])
```

That is only 3 lines. But what if you had 1 000 fruits? Loops solve this problem.

### What Is a Function / Method?

A **function** is a saved block of code with a name. You run it by writing its name followed by `()`.

A **method** is a function that belongs to a specific thing (like a list). You call it with a dot:

```python
fruits.sort()    # .sort() is a method that belongs to the list called fruits
```

You will learn many list methods throughout this lesson.

---

## Part 1 — Looping Through a List

### 1.1 What Is Looping and Why Do We Need It?

**The problem without loops:**

Imagine you have a shopping list with 50 items and you want to print all of them. Writing 50 individual `print()` lines is slow, messy, and impractical. If you add item 51 later, you have to add another line manually.

**The solution — a loop:**

A loop says: *"Go through every item in this list, one at a time, and do something with each one."* The loop adjusts automatically no matter how many items the list contains.

**Real-world analogy:** Think of a cashier at a supermarket. They don't have separate instructions for each product on the conveyor belt. They have one rule: *"scan the item, enter the price, move to the next one."* That one rule loops over every product automatically. Python loops work the same way.

---

### 1.2 The `for` Loop — Looping Directly Through Items

The most common way to loop through a list in Python is the `for` loop. It reads almost like plain English.

**Syntax:**

```python
for variable_name in list_name:
    # do something with variable_name
```

- `variable_name` is a temporary label you make up — it holds one item from the list at a time.
- `in list_name` tells Python which list to go through.
- The indented block below runs once **for each item**.

**Example 1 — Print every fruit:**

```python
fruits = ["apple", "banana", "cherry"]

for x in fruits:
    print(x)
```

**Expected Output:**
```
apple
banana
cherry
```

**What happened, step by step?**

| Loop Turn | What `x` holds | What gets printed |
|-----------|----------------|-------------------|
| 1st       | `"apple"`      | `apple`           |
| 2nd       | `"banana"`     | `banana`          |
| 3rd       | `"cherry"`     | `cherry`          |

After the 3rd turn, the list has no more items, so the loop ends automatically.

> 💡 **Tip:** The variable name `x` is just a convention. You could write `for fruit in fruits:` or `for item in fruits:` — any name works. Pick something readable.

**Example 2 — Do something with each item:**

```python
temperatures = [22, 18, 30, 25, 17]

for temp in temperatures:
    print(temp + 273)    # Convert Celsius to Kelvin
```

**Expected Output:**
```
295
291
303
298
290
```

> 🤔 **Think about it:** What would happen if you added a 6th temperature to the list? Would you need to change the loop?

---

### 1.3 The `for` Loop with `range()` and Index Numbers

Sometimes you need to know **which position** (index) you are at, not just the value. This is useful when you want to change items inside the list or when you need to show numbered output.

**`range(len(list_name))` explained:**

- `len(fruits)` counts how many items are in the list. For `["apple","banana","cherry"]` it returns `3`.
- `range(3)` produces the numbers `0, 1, 2` — exactly the valid index positions.
- So the loop visits index 0, then 1, then 2.

**Example 3 — Print with index numbers:**

```python
fruits = ["apple", "banana", "cherry"]

for i in range(len(fruits)):
    print(i, fruits[i])
```

**Expected Output:**
```
0 apple
1 banana
2 cherry
```

**Example 4 — Number a shopping list starting from 1:**

```python
shopping = ["milk", "eggs", "bread", "butter"]

for i in range(len(shopping)):
    print(str(i + 1) + ". " + shopping[i])
```

**Expected Output:**
```
1. milk
2. eggs
3. bread
4. butter
```

> 💡 **Note:** We write `i + 1` because indexes start at 0, but humans count from 1.

---

### 1.4 The `while` Loop — Looping with a Condition

A `while` loop keeps repeating as long as a condition is `True`. It is another way to loop through a list when you want fine control over how the loop moves.

**Syntax:**

```python
i = 0
while i < len(list_name):
    # do something with list_name[i]
    i += 1    # MUST increase i each time, or the loop runs forever!
```

**Example 5 — Print every fruit with a `while` loop:**

```python
fruits = ["apple", "banana", "cherry"]

i = 0
while i < len(fruits):
    print(fruits[i])
    i += 1
```

**Expected Output:**
```
apple
banana
cherry
```

**Step-by-step trace:**

| Step | `i` value | Condition `i < 3` | What prints | After `i += 1` |
|------|-----------|-------------------|-------------|----------------|
| 1    | 0         | True              | apple       | i = 1          |
| 2    | 1         | True              | banana      | i = 2          |
| 3    | 2         | True              | cherry      | i = 3          |
| 4    | 3         | **False** → STOP  | —           | —              |

> ⚠️ **Common Beginner Mistake — Forgetting `i += 1`:**
> ```python
> # WRONG — this runs forever (infinite loop)!
> i = 0
> while i < len(fruits):
>     print(fruits[i])
>     # forgot to write i += 1
> ```
> Always make sure your `while` loop has a line that eventually makes the condition `False`.

---

### 1.5 The `break` Statement — Exiting a Loop Early

`break` immediately exits the loop, even if there are more items left.

**Example 6 — Stop when you find "banana":**

```python
fruits = ["apple", "banana", "cherry"]

for x in fruits:
    if x == "banana":
        break
    print(x)
```

**Expected Output:**
```
apple
```

The loop printed `apple`, then hit `banana` and stopped. `cherry` was never reached.

---

### 1.6 The `continue` Statement — Skipping One Item

`continue` skips the rest of the current loop turn and jumps to the next item.

**Example 7 — Skip "banana", print everything else:**

```python
fruits = ["apple", "banana", "cherry"]

for x in fruits:
    if x == "banana":
        continue
    print(x)
```

**Expected Output:**
```
apple
cherry
```

> 🤔 **Think about it:** What is the difference between `break` and `continue`? `break` **ends** the loop entirely. `continue` only **skips** the current item and keeps going.

---

### 1.7 `for` Loop with `else`

Python has an unusual but useful feature: you can add an `else` block to a `for` loop. The `else` block runs **after the loop finishes normally** (i.e., it did NOT exit via `break`).

**Example 8:**

```python
fruits = ["apple", "banana", "cherry"]

for x in fruits:
    print(x)
else:
    print("Loop finished!")
```

**Expected Output:**
```
apple
banana
cherry
Loop finished!
```

---

### Part 1 — Practice Exercise

**Scenario:** You are a teacher and you have a list of student test scores. Write a program that:
1. Prints every score
2. Prints how many scores are above 50

```python
scores = [45, 72, 88, 33, 91, 50, 67]

count_pass = 0

for score in scores:
    print(score)
    if score > 50:
        count_pass += 1

print("Students who passed:", count_pass)
```

**Expected Output:**
```
45
72
88
33
91
50
67
Students who passed: 4
```

> 🔍 **Self-check:** Why is 50 not counted as a pass? Because the condition is `> 50` (strictly greater than), not `>= 50`.

---

## Part 2 — List Comprehension

### 2.1 What Is a List Comprehension?

A **list comprehension** is a special Python syntax that creates a brand-new list in a single line of code.

**Without comprehension** (the "old way"):

```python
fruits = ["apple", "banana", "cherry"]
newlist = []

for x in fruits:
    newlist.append(x)

print(newlist)
```

**Expected Output:**
```
['apple', 'banana', 'cherry']
```

**With comprehension** (the "new way"):

```python
fruits = ["apple", "banana", "cherry"]
newlist = [x for x in fruits]

print(newlist)
```

**Expected Output:**
```
['apple', 'banana', 'cherry']
```

Both produce identical results. The comprehension is shorter, faster, and once you understand it, easier to read.

---

### 2.2 The Anatomy of a List Comprehension

```
newlist = [expression   for item in iterable   if condition]
              ↑               ↑                      ↑
         What to put    Where to get items     Optional filter
         in the list    (a list, range, etc.)
```

- **expression** — What each item in the new list looks like (could be the item itself, a modified version, etc.)
- **for item in iterable** — Loop through every item from a list, range, or other collection
- **if condition** — (Optional) Only include items that pass this test

Think of it like a sentence: *"Give me [expression] for each [item] in [iterable], but only if [condition]."*

---

### 2.3 Comprehension Without a Condition (Simple Filter)

**Example 9 — Copy a list:**

```python
fruits = ["apple", "banana", "cherry", "kiwi", "mango"]
newlist = [x for x in fruits]
print(newlist)
```

**Expected Output:**
```
['apple', 'banana', 'cherry', 'kiwi', 'mango']
```

---

### 2.4 Comprehension With a Condition (`if` Filter)

**Example 10 — Only fruits whose name contains the letter "a":**

```python
fruits = ["apple", "banana", "cherry", "kiwi", "mango"]
newlist = [x for x in fruits if "a" in x]
print(newlist)
```

**Expected Output:**
```
['apple', 'banana', 'mango']
```

**Example 11 — Only numbers less than 5 from a range:**

```python
newlist = [x for x in range(10) if x < 5]
print(newlist)
```

**Expected Output:**
```
[0, 1, 2, 3, 4]
```

> 🤔 **Think about it:** `range(10)` produces 0, 1, 2, 3, 4, 5, 6, 7, 8, 9. The condition `x < 5` keeps only 0 through 4.

**Example 12 — Exclude one item:**

```python
fruits = ["apple", "banana", "cherry", "kiwi", "mango"]
newlist = [x for x in fruits if x != "apple"]
print(newlist)
```

**Expected Output:**
```
['banana', 'cherry', 'kiwi', 'mango']
```

---

### 2.5 Transforming Items (Modifying the Expression)

The **expression** part does not have to be just `x`. You can apply any transformation.

**Example 13 — Convert all fruits to UPPERCASE:**

```python
fruits = ["apple", "banana", "cherry"]
newlist = [x.upper() for x in fruits]
print(newlist)
```

**Expected Output:**
```
['APPLE', 'BANANA', 'CHERRY']
```

**Example 14 — Double every number in a list:**

```python
numbers = [1, 2, 3, 4, 5]
doubled = [x * 2 for x in numbers]
print(doubled)
```

**Expected Output:**
```
[2, 4, 6, 8, 10]
```

**Real-world use case:** A data analyst might use this to convert a column of temperatures from Celsius to Fahrenheit in one line:

```python
celsius = [0, 10, 20, 30, 40]
fahrenheit = [(c * 9/5) + 32 for c in celsius]
print(fahrenheit)
```

**Expected Output:**
```
[32.0, 50.0, 68.0, 86.0, 104.0]
```

---

### 2.6 Conditional Expression Inside the Expression (`if...else` in the Expression)

You can also use an `if/else` directly inside the expression part (not the filter part) to choose between two values for each item.

**Syntax:**

```python
newlist = [value_if_true if condition else value_if_false  for item in iterable]
```

**Example 15 — Replace "banana" with "orange", keep everything else:**

```python
fruits = ["apple", "banana", "cherry"]
newlist = [x if x != "banana" else "orange" for x in fruits]
print(newlist)
```

**Expected Output:**
```
['apple', 'orange', 'cherry']
```

**Explained:** For each `x` in the list:
- If `x` is NOT "banana" → keep `x` as-is
- If `x` IS "banana" → replace it with `"orange"`

**Example 16 — Label numbers as "even" or "odd":**

```python
numbers = [1, 2, 3, 4, 5, 6]
labels = ["even" if n % 2 == 0 else "odd" for n in numbers]
print(labels)
```

**Expected Output:**
```
['odd', 'even', 'odd', 'even', 'odd', 'even']
```

---

### 2.7 Using `range()` as the Iterable

You can use `range()` instead of an existing list to generate values on the fly.

**Example 17 — Squares of numbers 1 through 5:**

```python
squares = [x ** 2 for x in range(1, 6)]
print(squares)
```

**Expected Output:**
```
[1, 4, 9, 16, 25]
```

---

### 2.8 Common Beginner Mistake — Confusing the Two `if` Positions

There are **two places** an `if` can go in a comprehension, and they do different things:

```python
# FILTER if — goes AFTER the for clause, NO else allowed here
[x for x in fruits if x != "banana"]        # Removes banana from results

# EXPRESSION if — goes BEFORE the for clause, MUST have else
[x if x != "banana" else "orange" for x in fruits]  # Replaces banana with orange
```

> ⚠️ **Wrong — trying to use else with a filter if:**
> ```python
> # WRONG — SyntaxError
> [x for x in fruits if x != "banana" else "orange"]
> ```
> Move the `if/else` to the expression part (before `for`) when you need an else.

---

### Part 2 — Practice Exercise

**Scenario:** You have a list of product prices. Create a new list that:
1. Includes only prices greater than 10
2. Applies a 10% discount to each qualifying price

```python
prices = [5.99, 15.00, 8.50, 22.00, 3.75, 12.99]

discounted = [round(p * 0.9, 2) for p in prices if p > 10]
print(discounted)
```

**Expected Output:**
```
[13.5, 19.8, 11.69]
```

> 🔍 **Self-check:** Why are 5.99, 8.50, and 3.75 missing from the result?

---

## Part 3 — Sorting a List

### 3.1 What Does Sorting Mean and Why Does It Matter?

**Sorting** means arranging the items in a list in a specific order — most commonly alphabetical (A to Z) or numerical (smallest to largest).

**Why sort?**

- A doctor needs patient records sorted by last name.
- A store needs products sorted by price (cheapest first).
- A teacher needs exam scores sorted highest to lowest.
- A search engine needs results sorted by relevance.

Python gives you two main tools for sorting:
- `.sort()` — **modifies the original list** (in-place sort)
- `sorted()` — **creates a new sorted list**, leaving the original unchanged

---

### 3.2 The `.sort()` Method — Sort the Original List

`.sort()` rearranges the items inside the list permanently.

**Example 18 — Sort strings alphabetically:**

```python
thislist = ["orange", "mango", "kiwi", "pineapple", "banana"]
thislist.sort()
print(thislist)
```

**Expected Output:**
```
['banana', 'kiwi', 'mango', 'orange', 'pineapple']
```

**Example 19 — Sort numbers from smallest to largest:**

```python
thislist = [100, 50, 65, 82, 23]
thislist.sort()
print(thislist)
```

**Expected Output:**
```
[23, 50, 65, 82, 100]
```

> 💡 **Remember:** `.sort()` changes the list itself. After calling it, the original order is **gone**.

---

### 3.3 Sort in Descending Order with `reverse=True`

Add `reverse=True` to sort from largest to smallest (numbers) or Z to A (strings).

**Example 20 — Sort strings Z to A:**

```python
thislist = ["orange", "mango", "kiwi", "pineapple", "banana"]
thislist.sort(reverse=True)
print(thislist)
```

**Expected Output:**
```
['pineapple', 'orange', 'mango', 'kiwi', 'banana']
```

**Example 21 — Sort numbers largest to smallest:**

```python
thislist = [100, 50, 65, 82, 23]
thislist.sort(reverse=True)
print(thislist)
```

**Expected Output:**
```
[100, 82, 65, 50, 23]
```

---

### 3.4 Case-Insensitive Sorting with `key=str.lower`

By default, Python sorts uppercase letters before lowercase letters (because uppercase letters have lower ASCII values). This can cause surprising results.

**Example 22 — Default sort (case-sensitive, uppercase first):**

```python
thislist = ["banana", "Orange", "Kiwi", "cherry"]
thislist.sort()
print(thislist)
```

**Expected Output:**
```
['Kiwi', 'Orange', 'banana', 'cherry']
```

`Kiwi` and `Orange` appear first because Python sees capital letters as "smaller."

**Example 23 — Case-insensitive sort:**

```python
thislist = ["banana", "Orange", "Kiwi", "cherry"]
thislist.sort(key=str.lower)
print(thislist)
```

**Expected Output:**
```
['banana', 'cherry', 'Kiwi', 'Orange']
```

**How `key=str.lower` works:** Before comparing any two items, Python temporarily converts them to lowercase just for the comparison. The original capitalisation is kept in the final list — only the sorting logic uses lowercase.

---

### 3.5 Custom Sort Functions with `key=`

You can pass any function to `key=` to control how sorting decisions are made. The function receives each item and returns a value; Python sorts by those returned values.

**Example 24 — Sort strings by their length (shortest first):**

```python
def my_func(e):
    return len(e)

thislist = ["banana", "kiwi", "pineapple", "apple"]
thislist.sort(key=my_func)
print(thislist)
```

**Expected Output:**
```
['kiwi', 'apple', 'banana', 'pineapple']
```

`len("kiwi")` = 4, `len("apple")` = 5, `len("banana")` = 6, `len("pineapple")` = 9 — so sorted by those lengths.

**Example 25 — Sort a list of numbers by their distance from 50:**

```python
def distance_from_50(n):
    return abs(n - 50)

numbers = [100, 50, 65, 23, 48]
numbers.sort(key=distance_from_50)
print(numbers)
```

**Expected Output:**
```
[50, 48, 65, 23, 100]
```

> 💡 `abs()` returns the absolute value — the distance from zero, always positive. So `abs(23 - 50)` = `abs(-27)` = `27`.

---

### 3.6 The `.reverse()` Method — Flip the List Order

`.reverse()` simply flips the list backwards. It does NOT sort — it just reverses whatever order the items are currently in.

**Example 26:**

```python
fruits = ["banana", "Orange", "Kiwi", "cherry"]
fruits.reverse()
print(fruits)
```

**Expected Output:**
```
['cherry', 'Kiwi', 'Orange', 'banana']
```

---

### 3.7 The `sorted()` Built-in Function — Sort Without Changing the Original

`sorted()` returns a **new sorted list** and leaves the original list unchanged.

**Example 27:**

```python
original = [100, 50, 65, 82, 23]
new_sorted = sorted(original)

print("Original:", original)
print("Sorted:  ", new_sorted)
```

**Expected Output:**
```
Original: [100, 50, 65, 82, 23]
Sorted:   [23, 50, 65, 82, 100]
```

> 🤔 **When to use `.sort()` vs `sorted()`?**
> - Use `.sort()` when you want to permanently sort the original list.
> - Use `sorted()` when you want to keep the original list intact and work with a sorted copy.

---

### Part 3 — Practice Exercise

**Scenario:** You run a small bookshop. You have a list of book prices. Display them sorted from cheapest to most expensive, and separately from most expensive to cheapest.

```python
prices = [12.99, 7.50, 24.00, 3.99, 18.75, 9.00]

prices.sort()
print("Cheapest to most expensive:", prices)

prices.sort(reverse=True)
print("Most expensive to cheapest:", prices)
```

**Expected Output:**
```
Cheapest to most expensive: [3.99, 7.5, 9.0, 12.99, 18.75, 24.0]
Most expensive to cheapest: [24.0, 18.75, 12.99, 9.0, 7.5, 3.99]
```

---

## Part 4 — Copying a List

### 4.1 The Problem with Direct Assignment

This is one of the most important and surprising concepts for beginners. Many new Python learners make a critical mistake here.

**Example 28 — The Dangerous Mistake:**

```python
list1 = ["apple", "banana", "cherry"]
list2 = list1          # THIS IS NOT A COPY — it's a second name for the SAME list

list2.append("date")

print(list1)           # Expected ['apple','banana','cherry'] — SURPRISE!
print(list2)
```

**Expected Output:**
```
['apple', 'banana', 'cherry', 'date']
['apple', 'banana', 'cherry', 'date']
```

**Why?** When you write `list2 = list1`, Python does NOT create a new list. Instead, `list2` becomes another label pointing to the **exact same list in memory**. Any change made via `list2` is also visible via `list1`, because they are the same object.

**Analogy:** Imagine a house and two keys. If you give your friend a copy of your house key (same lock), they can enter your house. If they move the furniture, you'll find it moved too. `list2 = list1` is like giving your friend a key — not a separate identical house.

To get a **separate identical house**, you need to actually **build a copy**.

---

### 4.2 Copying with the `.copy()` Method

**Example 29 — Safe copy with `.copy()`:**

```python
list1 = ["apple", "banana", "cherry"]
list2 = list1.copy()       # Creates a REAL independent copy

list2.append("date")

print(list1)               # Original — unchanged
print(list2)               # Copy — has the new item
```

**Expected Output:**
```
['apple', 'banana', 'cherry']
['apple', 'banana', 'cherry', 'date']
```

Now `list1` and `list2` are completely independent. Changes to one do not affect the other.

---

### 4.3 Copying with the `list()` Constructor

Another clean and readable way to copy a list is to pass it to the built-in `list()` function:

**Example 30:**

```python
list1 = ["apple", "banana", "cherry"]
list2 = list(list1)        # Creates a new list with the same contents

list2[0] = "mango"

print(list1)               # Unchanged
print(list2)               # Modified copy
```

**Expected Output:**
```
['apple', 'banana', 'cherry']
['mango', 'banana', 'cherry']
```

---

### 4.4 Copying with Slice Notation `[:]`

A third common approach is the **full slice**. Slicing always returns a new list.

**Example 31:**

```python
list1 = ["apple", "banana", "cherry"]
list2 = list1[:]           # Full slice = entire list as a new copy

list2.remove("banana")

print(list1)
print(list2)
```

**Expected Output:**
```
['apple', 'banana', 'cherry']
['apple', 'cherry']
```

---

### 4.5 Summary — Three Ways to Copy a List

| Method | Code | Creates independent copy? |
|--------|------|---------------------------|
| `.copy()` | `list2 = list1.copy()` | ✅ Yes |
| `list()` | `list2 = list(list1)` | ✅ Yes |
| Slice `[:]` | `list2 = list1[:]` | ✅ Yes |
| Direct assignment | `list2 = list1` | ❌ No — same object! |

> 💡 **When does copying matter in real life?** In data science, you often need to process a dataset without destroying the original. A researcher might copy their raw data before cleaning it, so the original stays intact for verification.

---

### Part 4 — Practice Exercise

**Scenario:** You have a roster of students. You want to create a "backup" roster before making changes.

```python
original_roster = ["Alice", "Bob", "Charlie", "Diana"]
backup_roster = original_roster.copy()

# Enroll a new student in the working copy
original_roster.append("Eve")

print("Current roster:", original_roster)
print("Backup roster: ", backup_roster)
```

**Expected Output:**
```
Current roster: ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve']
Backup roster:  ['Alice', 'Bob', 'Charlie', 'Diana']
```

---

## Part 5 — Joining / Concatenating Lists

### 5.1 What Is Joining?

**Joining** (also called **concatenating**) two or more lists means combining them into one single list. All items from both lists appear together.

**Real-world example:** You manage two warehouses. Warehouse A has one inventory list, Warehouse B has another. To get the combined inventory, you join the two lists.

---

### 5.2 Method 1 — The `+` Operator

The simplest way to join two lists is to add them with `+`:

**Example 32:**

```python
list1 = ["a", "b", "c"]
list2 = [1, 2, 3]

list3 = list1 + list2
print(list3)
```

**Expected Output:**
```
['a', 'b', 'c', 1, 2, 3]
```

> 💡 This creates a **new combined list**. `list1` and `list2` are unchanged.

**Example 33 — Joining three lists:**

```python
fruits = ["apple", "banana"]
veggies = ["carrot", "spinach"]
grains = ["rice", "oats"]

all_foods = fruits + veggies + grains
print(all_foods)
```

**Expected Output:**
```
['apple', 'banana', 'carrot', 'spinach', 'rice', 'oats']
```

---

### 5.3 Method 2 — The `.extend()` Method

`.extend()` adds all items from one list **directly into another list** (modifies the first list in place):

**Example 34:**

```python
list1 = ["a", "b", "c"]
list2 = [1, 2, 3]

list1.extend(list2)
print(list1)
```

**Expected Output:**
```
['a', 'b', 'c', 1, 2, 3]
```

> 🤔 **What is the difference between `+` and `.extend()`?**
> - `+` creates a **brand new list**, leaving both originals unchanged.
> - `.extend()` **modifies** `list1` by adding items from `list2` into it.

**Example 35 — Adding a tuple to a list with `.extend()`:**

`.extend()` accepts any iterable (list, tuple, set, range, etc.), not just lists:

```python
list1 = ["apple", "banana", "cherry"]
tuple1 = ("kiwi", "orange")

list1.extend(tuple1)
print(list1)
```

**Expected Output:**
```
['apple', 'banana', 'cherry', 'kiwi', 'orange']
```

---

### 5.4 Method 3 — A Loop with `.append()`

You can also join lists manually using a loop:

**Example 36:**

```python
list1 = ["a", "b", "c"]
list2 = [1, 2, 3]

for x in list2:
    list1.append(x)

print(list1)
```

**Expected Output:**
```
['a', 'b', 'c', 1, 2, 3]
```

> 💡 This works but `.extend()` is more concise and faster. Use the loop approach when you need to filter or transform items during the join.

---

### 5.5 Joining Summary

| Method | Code | Modifies original? | Use when |
|--------|------|--------------------|----------|
| `+` operator | `c = a + b` | ❌ No | You want a new list |
| `.extend()` | `a.extend(b)` | ✅ Yes (adds to `a`) | You want to grow one list |
| Loop + `.append()` | `for x in b: a.append(x)` | ✅ Yes | You need to filter/transform during join |

---

### Part 5 — Practice Exercise

**Scenario:** You manage two event guest lists. Combine them into one master list.

```python
vip_guests = ["Alice", "Bob", "Charlie"]
general_guests = ["Diana", "Eve", "Frank"]

# Method 1: using +
master_list = vip_guests + general_guests
print("Master list:", master_list)

# Method 2: using .extend()
vip_guests.extend(general_guests)
print("VIP list extended:", vip_guests)
```

**Expected Output:**
```
Master list: ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve', 'Frank']
VIP list extended: ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve', 'Frank']
```

---

## Part 6 — All Python List Methods

Python lists come with a powerful built-in toolbox of methods. Here is a complete reference guide for every method, with explanations and examples.

### Overview Table

| Method | What It Does |
|--------|-------------|
| `append()` | Adds one item to the end |
| `clear()` | Removes all items |
| `copy()` | Returns a copy of the list |
| `count()` | Counts how many times a value appears |
| `extend()` | Adds all items from another iterable to the end |
| `index()` | Returns the index of the first occurrence of a value |
| `insert()` | Inserts an item at a specified position |
| `pop()` | Removes and returns the item at a specified index |
| `remove()` | Removes the first occurrence of a specified value |
| `reverse()` | Reverses the order of the list |
| `sort()` | Sorts the list |

---

### 6.1 `append()` — Add One Item to the End

**What it does:** Adds a single item to the very end of the list.

**Syntax:** `list.append(item)`

**Example 37:**

```python
thislist = ["apple", "banana", "cherry"]
thislist.append("orange")
print(thislist)
```

**Expected Output:**
```
['apple', 'banana', 'cherry', 'orange']
```

> ⚠️ **Common mistake:** Appending a list inside a list:
> ```python
> thislist.append(["orange", "grape"])
> # This adds ONE item that is itself a list: ['apple', 'banana', 'cherry', ['orange', 'grape']]
> # Use .extend() if you want to add multiple items separately
> ```

---

### 6.2 `clear()` — Remove All Items

**What it does:** Empties the list completely. The list object still exists, it just has no items.

**Syntax:** `list.clear()`

**Example 38:**

```python
thislist = ["apple", "banana", "cherry"]
thislist.clear()
print(thislist)
```

**Expected Output:**
```
[]
```

---

### 6.3 `copy()` — Return a Copy

Already covered in Part 4. Quick reminder:

**Example 39:**

```python
thislist = ["apple", "banana", "cherry"]
mylist = thislist.copy()
print(mylist)
```

**Expected Output:**
```
['apple', 'banana', 'cherry']
```

---

### 6.4 `count()` — Count Occurrences of a Value

**What it does:** Returns how many times a specific value appears in the list.

**Syntax:** `list.count(value)`

**Example 40:**

```python
thislist = [1, 4, 2, 9, 7, 8, 9, 3, 1]
print(thislist.count(9))
```

**Expected Output:**
```
2
```

**Real-world use:** A weather analyst might count how many days in a month the temperature exceeded 30°C.

```python
temps = [28, 31, 33, 29, 35, 30, 33, 32, 31, 33]
print("Days above 30:", temps.count(31) + temps.count(32) + temps.count(33) + temps.count(35))
```

> 💡 For more complex counting conditions, use a loop or comprehension instead.

---

### 6.5 `extend()` — Add Items from Another Iterable

Already covered in Part 5. Quick reminder:

**Example 41:**

```python
thislist = ["apple", "banana", "cherry"]
thislist.extend(["kiwi", "orange"])
print(thislist)
```

**Expected Output:**
```
['apple', 'banana', 'cherry', 'kiwi', 'orange']
```

---

### 6.6 `index()` — Find the Position of a Value

**What it does:** Returns the **index** (position) of the first occurrence of a specified value.

**Syntax:** `list.index(value)`

**Example 42:**

```python
thislist = ["apple", "banana", "cherry"]
print(thislist.index("cherry"))
```

**Expected Output:**
```
2
```

**Example 43 — Search within a range:**

You can optionally pass a start and end position: `list.index(value, start, end)`

```python
fruits = ["apple", "banana", "cherry", "banana", "kiwi"]
print(fruits.index("banana"))       # First banana is at index 1
print(fruits.index("banana", 2))    # Search from index 2 onwards — finds banana at index 3
```

**Expected Output:**
```
1
3
```

> ⚠️ **Common mistake:** If the value does not exist, `.index()` raises a `ValueError`. Use this carefully or check first with `if value in list`.

---

### 6.7 `insert()` — Add an Item at a Specific Position

**What it does:** Inserts an item at the index you specify. All existing items at and after that index shift one position to the right.

**Syntax:** `list.insert(index, item)`

**Example 44:**

```python
thislist = ["apple", "banana", "cherry"]
thislist.insert(1, "orange")
print(thislist)
```

**Expected Output:**
```
['apple', 'orange', 'banana', 'cherry']
```

`"orange"` was inserted at index 1. `"banana"` moved from index 1 to index 2. `"cherry"` moved from index 2 to index 3.

**Example 45 — Insert at the beginning:**

```python
thislist = ["banana", "cherry"]
thislist.insert(0, "apple")
print(thislist)
```

**Expected Output:**
```
['apple', 'banana', 'cherry']
```

---

### 6.8 `pop()` — Remove and Return an Item by Index

**What it does:** Removes the item at the specified index and **returns** it (so you can use the removed item). If no index is given, it removes and returns the **last** item.

**Syntax:** `list.pop(index)` or `list.pop()`

**Example 46 — Pop the last item:**

```python
thislist = ["apple", "banana", "cherry"]
removed = thislist.pop()
print("Removed:", removed)
print("List now:", thislist)
```

**Expected Output:**
```
Removed: cherry
List now: ['apple', 'banana']
```

**Example 47 — Pop a specific index:**

```python
thislist = ["apple", "banana", "cherry"]
removed = thislist.pop(1)
print("Removed:", removed)
print("List now:", thislist)
```

**Expected Output:**
```
Removed: banana
List now: ['apple', 'cherry']
```

> 💡 **Real-world use:** `pop()` is commonly used in "stack" data structures — like a pile of plates where you always take from the top. Each `pop()` removes the most recently added item.

---

### 6.9 `remove()` — Remove an Item by Value

**What it does:** Finds the **first occurrence** of the specified value and removes it. Unlike `pop()`, you give it a **value**, not an index.

**Syntax:** `list.remove(value)`

**Example 48:**

```python
thislist = ["apple", "banana", "cherry"]
thislist.remove("banana")
print(thislist)
```

**Expected Output:**
```
['apple', 'cherry']
```

**Example 49 — Removes only the FIRST occurrence:**

```python
thislist = ["apple", "banana", "cherry", "banana"]
thislist.remove("banana")
print(thislist)
```

**Expected Output:**
```
['apple', 'cherry', 'banana']
```

Only the first `"banana"` was removed. The second one remains.

> ⚠️ **Common mistake:** If the value does not exist in the list, `remove()` raises a `ValueError`. Check first with `if value in list` if you are not sure.

---

### 6.10 `reverse()` — Reverse the List In-Place

Already covered in Part 3. Quick reminder:

**Example 50:**

```python
fruits = ["apple", "banana", "cherry"]
fruits.reverse()
print(fruits)
```

**Expected Output:**
```
['cherry', 'banana', 'apple']
```

---

### 6.11 `sort()` — Sort the List In-Place

Already covered in Part 3. Quick reminder:

**Example 51:**

```python
cars = ["Ford", "BMW", "Volvo"]
cars.sort()
print(cars)
```

**Expected Output:**
```
['BMW', 'Ford', 'Volvo']
```

---

### 6.12 Method Chaining — Can You Chain List Methods?

Most list methods return `None` (they modify in place), so you **cannot** chain them like string methods. This is a common beginner mistake:

```python
# WRONG — .sort() returns None, so you'd be printing None
result = thislist.sort()
print(result)      # Prints: None
```

```python
# CORRECT — sort first, then print the list itself
thislist.sort()
print(thislist)
```

---

## Part 7 — List Exercises (Practice Section)

The following exercises are inspired by the W3Schools Python Lists exercises. Work through each one, attempt it yourself, then check the solution.

---

### Exercise 1 — Print the Second Item

**Task:** Print the second item in the list `fruits = ["apple", "banana", "cherry"]`.

```python
fruits = ["apple", "banana", "cherry"]
print(fruits[1])
```

**Expected Output:**
```
banana
```

---

### Exercise 2 — Change the Third Item

**Task:** Change the third item in the list `fruits` from `"cherry"` to `"watermelon"`.

```python
fruits = ["apple", "banana", "cherry"]
fruits[2] = "watermelon"
print(fruits)
```

**Expected Output:**
```
['apple', 'banana', 'watermelon']
```

---

### Exercise 3 — Find the Length

**Task:** Print the number of items in the list `fruits`.

```python
fruits = ["apple", "banana", "cherry"]
print(len(fruits))
```

**Expected Output:**
```
3
```

---

### Exercise 4 — Add an Item

**Task:** Use the correct method to add `"orange"` to the list `fruits`.

```python
fruits = ["apple", "banana", "cherry"]
fruits.append("orange")
print(fruits)
```

**Expected Output:**
```
['apple', 'banana', 'cherry', 'orange']
```

---

### Exercise 5 — Remove an Item

**Task:** Use the correct method to remove `"banana"` from the list.

```python
fruits = ["apple", "banana", "cherry"]
fruits.remove("banana")
print(fruits)
```

**Expected Output:**
```
['apple', 'cherry']
```

---

### Exercise 6 — Loop and Print

**Task:** Use a `for` loop to print every item in the list.

```python
fruits = ["apple", "banana", "cherry"]
for x in fruits:
    print(x)
```

**Expected Output:**
```
apple
banana
cherry
```

---

### Exercise 7 — Sort Alphabetically

**Task:** Use the correct method to sort the list `cars` alphabetically.

```python
cars = ["Porsche", "BMW", "Volvo", "Audi"]
cars.sort()
print(cars)
```

**Expected Output:**
```
['Audi', 'BMW', 'Porsche', 'Volvo']
```

---

### Exercise 8 — Copy a List

**Task:** Use the correct method to copy the list `fruits` into a variable called `mylist`.

```python
fruits = ["apple", "banana", "cherry"]
mylist = fruits.copy()
print(mylist)
```

**Expected Output:**
```
['apple', 'banana', 'cherry']
```

---

## Part 8 — Mini Project: Student Grade Manager

### Project Overview

You will build a **Student Grade Manager** that stores student names and their exam scores, then uses all the skills from this lesson to analyse and display results.

**Skills used:** loops, list comprehension, sorting, copying, joining, and list methods.

---

### Stage 1 — Setup: Create Your Data

```python
# Student names and their scores
students = ["Alice", "Bob", "Charlie", "Diana", "Eve", "Frank"]
scores   = [72, 45, 88, 91, 33, 67]
```

---

### Stage 2 — Loop Through and Display Results

```python
print("=== Grade Report ===")
for i in range(len(students)):
    print(students[i] + ": " + str(scores[i]))
```

**Expected Output:**
```
=== Grade Report ===
Alice: 72
Bob: 45
Charlie: 88
Diana: 91
Eve: 33
Frank: 67
```

---

### Stage 3 — Use List Comprehension to Identify Passing Students

A passing score is 50 or above.

```python
passing = [students[i] for i in range(len(students)) if scores[i] >= 50]
failing = [students[i] for i in range(len(students)) if scores[i] < 50]

print("\nPassing students:", passing)
print("Failing students:", failing)
```

**Expected Output:**
```
Passing students: ['Alice', 'Charlie', 'Diana', 'Eve...']
Failing students: ['Bob', 'Eve']
```

Wait — let's check: Eve scored 33, so she fails. Bob scored 45, so he fails. Let's verify:

```
Alice 72 ✅  Bob 45 ❌  Charlie 88 ✅  Diana 91 ✅  Eve 33 ❌  Frank 67 ✅
```

```
Passing students: ['Alice', 'Charlie', 'Diana', 'Frank']
Failing students: ['Bob', 'Eve']
```

---

### Stage 4 — Sort the Scores (Keep a Copy of Original)

```python
scores_copy = scores.copy()
scores_copy.sort()

print("\nScores lowest to highest:", scores_copy)
print("Original scores unchanged:", scores)
```

**Expected Output:**
```
Scores lowest to highest: [33, 45, 67, 72, 88, 91]
Original scores unchanged: [72, 45, 88, 91, 33, 67]
```

---

### Stage 5 — Add a New Class and Join Lists

A new class of students just joined. Join the two groups.

```python
new_students = ["Grace", "Hank"]
new_scores   = [80, 55]

all_students = students + new_students
all_scores   = scores + new_scores

print("\nAll students:", all_students)
print("All scores:  ", all_scores)
```

**Expected Output:**
```
All students: ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve', 'Frank', 'Grace', 'Hank']
All scores:   [72, 45, 88, 91, 33, 67, 80, 55]
```

---

### Stage 6 — Final Summary Using Methods

```python
print("\n=== Summary ===")
print("Total students:", len(all_students))
print("Highest score: ", max(all_scores))
print("Lowest score:  ", min(all_scores))
print("Top scorer:    ", all_students[all_scores.index(max(all_scores))])
print("Needs support: ", all_students[all_scores.index(min(all_scores))])
```

**Expected Output:**
```
=== Summary ===
Total students: 8
Highest score:  91
Lowest score:   33
Top scorer:     Diana
Needs support:  Eve
```

---

### Stage 7 — Complete Project Code

```python
# ===== Student Grade Manager =====

students = ["Alice", "Bob", "Charlie", "Diana", "Eve", "Frank"]
scores   = [72, 45, 88, 91, 33, 67]

# --- Grade Report ---
print("=== Grade Report ===")
for i in range(len(students)):
    print(students[i] + ": " + str(scores[i]))

# --- Pass/Fail ---
passing = [students[i] for i in range(len(students)) if scores[i] >= 50]
failing = [students[i] for i in range(len(students)) if scores[i] < 50]

print("\nPassing students:", passing)
print("Failing students:", failing)

# --- Sorted Copy ---
scores_copy = scores.copy()
scores_copy.sort()
print("\nScores (sorted):", scores_copy)

# --- Join New Class ---
new_students = ["Grace", "Hank"]
new_scores   = [80, 55]

all_students = students + new_students
all_scores   = scores + new_scores

# --- Summary ---
print("\n=== Summary ===")
print("Total students:", len(all_students))
print("Highest score: ", max(all_scores))
print("Lowest score:  ", min(all_scores))
print("Top scorer:    ", all_students[all_scores.index(max(all_scores))])
print("Needs support: ", all_students[all_scores.index(min(all_scores))])
```

> 🚀 **Optional Extension Challenges:**
> - Calculate and display the **class average**.
> - Add a **letter grade** (A, B, C, D, F) next to each score using a comprehension.
> - Sort students by score from highest to lowest and display a ranked leaderboard.

---

## Part 9 — Common Beginner Mistakes (Full Reference)

| Mistake | Wrong Code | Why It's Wrong | Correct Code |
|---------|-----------|----------------|-------------|
| Modifying list while looping | `for x in lst: lst.remove(x)` | Skips items because list shrinks | Loop over a copy: `for x in lst.copy()` |
| Forgetting `i += 1` in while | `while i < len(lst): print(lst[i])` | Infinite loop | Add `i += 1` inside the loop |
| `=` instead of `.copy()` | `b = a` | Both point to same list | `b = a.copy()` |
| Appending a list instead of extending | `a.append([1,2])` | Adds `[1,2]` as one nested item | `a.extend([1,2])` |
| Sorting returns `None` | `result = lst.sort(); print(result)` | `.sort()` returns `None` | `lst.sort(); print(lst)` |
| `.index()` on missing value | `lst.index("x")` when x not in lst | Raises `ValueError` | Check first: `if "x" in lst:` |
| `if/else` in wrong comprehension position | `[x for x in lst if x != "a" else "b"]` | `SyntaxError` | `[x if x != "a" else "b" for x in lst]` |
| Forgetting `range()` vs `len()` | `for i in len(lst):` | `len()` returns an int, not iterable | `for i in range(len(lst)):` |

---

## Part 10 — Reflection Questions

Think through each of these questions. Try to answer them without looking at your notes first.

1. What is the difference between a `for` loop and a `while` loop? When would you prefer one over the other?

2. In a list comprehension, where does the `if` filter go? Where does the `if/else` expression go? Why can't they be in the same place?

3. Why does `list2 = list1` not create a true copy? What actually happens in memory?

4. What is the difference between `.sort()` and `sorted()`? When would you use each one?

5. What is the difference between `.append()` and `.extend()`? What happens if you append a list instead of extending?

6. You call `.pop()` on a list with no argument. What happens? What does it return?

7. If you call `.sort()` on a list and then try to print the return value, what do you see? Why?

8. Can you think of a real-world scenario where you would need to: (a) loop through a list, (b) copy a list, (c) join two lists?

---

## Completion Checklist

Before moving to the next lesson, make sure you can confidently tick off each item:

- [ ] I can loop through a list using a `for` loop
- [ ] I can loop through a list using a `while` loop with an index
- [ ] I understand what `break` and `continue` do inside a loop
- [ ] I can write a basic list comprehension without a condition
- [ ] I can write a list comprehension with an `if` filter
- [ ] I can write a list comprehension with an `if/else` in the expression
- [ ] I can sort a list alphabetically and numerically with `.sort()`
- [ ] I can sort in reverse order with `reverse=True`
- [ ] I can perform a case-insensitive sort with `key=str.lower`
- [ ] I understand the difference between `.sort()` and `sorted()`
- [ ] I know why `list2 = list1` is NOT a copy
- [ ] I can make a safe copy using `.copy()`, `list()`, or `[:]`
- [ ] I can join two lists using `+` and `.extend()`
- [ ] I know what every list method does: `append`, `clear`, `copy`, `count`, `extend`, `index`, `insert`, `pop`, `remove`, `reverse`, `sort`
- [ ] I completed the Student Grade Manager mini-project

---

## Lesson Summary

Here is a quick-reference summary of everything covered in Lesson 08:

### Looping

```python
# for loop — direct
for x in mylist:
    print(x)

# for loop — by index
for i in range(len(mylist)):
    print(mylist[i])

# while loop
i = 0
while i < len(mylist):
    print(mylist[i])
    i += 1
```

### List Comprehension

```python
# Basic
newlist = [x for x in mylist]

# With filter
newlist = [x for x in mylist if x != "apple"]

# With transformation
newlist = [x.upper() for x in mylist]

# With if/else in expression
newlist = [x if x != "banana" else "orange" for x in mylist]
```

### Sorting

```python
mylist.sort()                    # A to Z, smallest to largest
mylist.sort(reverse=True)        # Z to A, largest to smallest
mylist.sort(key=str.lower)       # Case-insensitive sort
sorted_copy = sorted(mylist)     # Returns new list, original unchanged
mylist.reverse()                 # Reverses current order
```

### Copying

```python
copy1 = mylist.copy()    # Method 1
copy2 = list(mylist)     # Method 2
copy3 = mylist[:]        # Method 3
# NEVER: copy4 = mylist  ← this is NOT a copy!
```

### Joining

```python
combined = list1 + list2         # New list
list1.extend(list2)              # Adds list2 into list1
```

### All List Methods

```python
mylist.append(item)              # Add to end
mylist.clear()                   # Empty the list
mylist.copy()                    # Return a copy
mylist.count(value)              # Count occurrences
mylist.extend(iterable)          # Add all from iterable
mylist.index(value)              # Find position of value
mylist.insert(index, item)       # Insert at position
mylist.pop(index)                # Remove and return by index
mylist.remove(value)             # Remove first occurrence by value
mylist.reverse()                 # Reverse in place
mylist.sort()                    # Sort in place
```

---

> 🎉 **Congratulations!** You have completed Lesson 08. You now have a complete toolkit for working with Python lists at a professional level. In the next lesson, you will explore **Python Tuples** — a close cousin of the list with some important differences.
