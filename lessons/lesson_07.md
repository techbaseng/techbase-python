---
render_with_liquid: false
title: "Lesson 07 – Python Lists: Create, Access, Change, Add & Remove"
nav_order: 7
---

# Lesson 07 – Python Lists: Create, Access, Change, Add & Remove

---

## Lesson Introduction

Imagine you are keeping track of your five favourite fruits. You *could* store each one in a separate variable:

```python
fruit1 = "apple"
fruit2 = "banana"
fruit3 = "cherry"
fruit4 = "mango"
fruit5 = "grape"
```

That works — but what if you had 500 fruits? Or what if the number of fruits changes every day? Creating 500 individual variables would be a nightmare.

Python solves this with a **list** — a single container that can hold as many items as you need, all under one name. Lists are one of the most important and most-used tools in all of Python. You will use them in data analysis, web development, automation, science, games, finance, and almost every real-world Python project.

By the end of this lesson you will be able to:

- Create lists and understand exactly what they are
- Access any item in a list using its index number
- Change items that are already in a list
- Add new items to a list
- Remove items from a list
- Build a working mini-project that uses all five skills together

---

## Prerequisite Concepts

> **Before we start**, here are the small things you need to already know. If any of these feel unfamiliar, re-read your earlier lessons first.

| Concept | Quick reminder |
|---|---|
| Variables | `name = "Alice"` — a labelled box that stores a value |
| `print()` | Displays output to the screen |
| Data types | `str` (text), `int` (whole number), `float` (decimal), `bool` (`True`/`False`) |
| `len()` | Counts how many characters are in a string — we will use it to count list items today |

No other prior knowledge is needed. Everything else is taught from scratch right here.

---

## Part 1 – What Is a Python List?

### 1.1 The Real-World Analogy

Think of a **shopping list** on paper:

```
1. Milk
2. Eggs
3. Bread
4. Butter
```

Each item has a **position** (1st, 2nd, 3rd, 4th).  
You can **add** a new item at the bottom.  
You can **cross off** (remove) something you already bought.  
You can **change** "Butter" to "Olive Oil".

A Python list works in *exactly* the same way — except it lives inside your program.

---

### 1.2 The Technical Definition

A **Python list** is:

- An **ordered** collection of items (items always stay in the order you put them, unless you change that order)
- **Changeable** (you can add, remove, and edit items after creating the list)
- **Allows duplicates** (the same value can appear more than once)
- Written with **square brackets `[]`** and items separated by **commas `,`**

---

### 1.3 Creating Your First List

**Syntax:**

```python
list_name = [item1, item2, item3]
```

**Simple Example 1 – A list of fruits (strings):**

```python
fruits = ["apple", "banana", "cherry"]
print(fruits)
```

**Expected output:**
```
['apple', 'banana', 'cherry']
```

> **What happened?** Python stored three text values inside one variable called `fruits`. Notice the square brackets and the commas.

---

**Simple Example 2 – A list of numbers:**

```python
scores = [95, 87, 76, 100, 60]
print(scores)
```

**Expected output:**
```
[95, 87, 76, 100, 60]
```

---

**Simple Example 3 – A list of mixed data types:**

Python lists can hold *different types* in the same list:

```python
mixed = ["Alice", 25, True, 3.14]
print(mixed)
```

**Expected output:**
```
['Alice', 25, True, 3.14]
```

> **Thinking prompt:** Why would storing different types together be useful? Imagine a student record: name (string), age (int), passed (bool), GPA (float).

---

### 1.4 How Many Items? — `len()`

The built-in `len()` function counts the number of items in a list.

```python
fruits = ["apple", "banana", "cherry"]
print(len(fruits))
```

**Expected output:**
```
3
```

---

### 1.5 Lists Can Hold Other Lists (Nested Lists)

A list can even contain another list inside it. This is called a **nested list**.

```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
print(matrix)
```

**Expected output:**
```
[[1, 2, 3], [4, 5, 6], [7, 8, 9]]
```

We will not go deep into nested lists today, but it is important you know they exist.

---

### 1.6 The `list()` Constructor

You can also create a list using the `list()` function:

```python
colours = list(("red", "green", "blue"))
print(colours)
```

**Expected output:**
```
['red', 'green', 'blue']
```

> **Note:** Notice the *double* parentheses `(( ))` — the inner `()` creates a **tuple** (another collection type), and `list()` converts it into a list.

---

### 1.7 List Data Type

To confirm something is a list, use `type()`:

```python
fruits = ["apple", "banana", "cherry"]
print(type(fruits))
```

**Expected output:**
```
<class 'list'>
```

---

## Part 2 – Accessing List Items

### 2.1 What Is an Index?

Every item in a list has a **position number** called an **index**.

> **Analogy:** Think of seats in a cinema row. Seat 0 is the first seat, seat 1 is the second, and so on.

**Python indexes start at 0, not 1.** This is called **zero-based indexing** and is used in almost all programming languages.

```
List:   ["apple", "banana", "cherry", "mango", "grape"]
Index:      0         1         2        3        4
```

---

### 2.2 Accessing a Single Item

Use the list name followed by the index number inside square brackets:

```python
fruits = ["apple", "banana", "cherry"]
print(fruits[0])   # First item
print(fruits[1])   # Second item
print(fruits[2])   # Third item
```

**Expected output:**
```
apple
banana
cherry
```

> **Common beginner mistake:** Trying `fruits[3]` when only 3 items exist (indexes 0, 1, 2). This causes an `IndexError: list index out of range`.

**Corrected version:**

```python
fruits = ["apple", "banana", "cherry"]
print(len(fruits))     # 3 items → valid indexes are 0, 1, 2
print(fruits[2])       # Correct: last item
# print(fruits[3])     # WRONG: would crash
```

---

### 2.3 Negative Indexing

Python also allows **negative indexes**. A negative index counts from the *end* of the list.

```
List:   ["apple", "banana", "cherry"]
Neg:       -3        -2        -1
```

`-1` is always the *last* item. `-2` is second from last. And so on.

```python
fruits = ["apple", "banana", "cherry"]
print(fruits[-1])   # Last item
print(fruits[-2])   # Second from last
print(fruits[-3])   # Third from last (same as index 0)
```

**Expected output:**
```
cherry
banana
apple
```

> **Thinking prompt:** When would negative indexing be more useful than positive indexing? Hint: when you always want the *last* few items, regardless of list length.

---

### 2.4 Range of Indexes (Slicing)

You can grab a **slice** (a section) of a list using a colon `:` inside the brackets.

**Syntax:**
```python
list_name[start : end]
```

- `start` = the index to begin from (included)
- `end` = the index to stop before (NOT included)

```python
fruits = ["apple", "banana", "cherry", "orange", "kiwi", "melon", "mango"]
print(fruits[2:5])
```

**Expected output:**
```
['cherry', 'orange', 'kiwi']
```

> Items at indexes 2, 3, and 4 are returned. Index 5 is the stopping point — it is NOT included.

---

**Leaving out the start index** — slice from the beginning:

```python
fruits = ["apple", "banana", "cherry", "orange", "kiwi", "melon", "mango"]
print(fruits[:4])
```

**Expected output:**
```
['apple', 'banana', 'cherry', 'orange']
```

---

**Leaving out the end index** — slice to the end:

```python
fruits = ["apple", "banana", "cherry", "orange", "kiwi", "melon", "mango"]
print(fruits[2:])
```

**Expected output:**
```
['cherry', 'orange', 'kiwi', 'melon', 'mango']
```

---

**Negative index slicing:**

```python
fruits = ["apple", "banana", "cherry", "orange", "kiwi", "melon", "mango"]
print(fruits[-4:-1])
```

**Expected output:**
```
['orange', 'kiwi', 'melon']
```

---

### 2.5 Checking If an Item Exists — `in` Keyword

Use the `in` keyword to check whether a specific value is present in the list:

```python
fruits = ["apple", "banana", "cherry"]

if "banana" in fruits:
    print("Yes, banana is in the list!")
```

**Expected output:**
```
Yes, banana is in the list!
```

```python
if "mango" in fruits:
    print("Found mango")
else:
    print("mango is NOT in the list")
```

**Expected output:**
```
mango is NOT in the list
```

---

## Part 3 – Changing List Items

### 3.1 Why Would You Change a List Item?

Lists are **mutable** — meaning you *can* change their contents after creation. This is different from strings, which are immutable (once created, you cannot change individual characters).

> **Real-world example:** A store's inventory changes daily. Items go in and out of stock. A list lets you update that data without rebuilding everything from scratch.

---

### 3.2 Changing One Item

Assign a new value directly to a specific index:

```python
fruits = ["apple", "banana", "cherry"]
fruits[1] = "mango"
print(fruits)
```

**Expected output:**
```
['apple', 'mango', 'cherry']
```

> Position 1 (which was "banana") is now "mango". The other items are unchanged.

---

### 3.3 Changing a Range of Items

You can replace several items at once using a slice:

```python
fruits = ["apple", "banana", "cherry", "orange", "kiwi"]
fruits[1:3] = ["mango", "melon"]
print(fruits)
```

**Expected output:**
```
['apple', 'mango', 'melon', 'orange', 'kiwi']
```

> Items at indexes 1 and 2 ("banana" and "cherry") were replaced with "mango" and "melon".

---

**What if you replace a range with MORE items than the original range?**

```python
fruits = ["apple", "banana", "cherry"]
fruits[1:2] = ["mango", "melon", "grape"]
print(fruits)
```

**Expected output:**
```
['apple', 'mango', 'melon', 'grape', 'cherry']
```

> Only index 1 ("banana") was in the slice, but it was replaced by THREE items. The list grew longer!

---

**What if you replace a range with FEWER items?**

```python
fruits = ["apple", "banana", "cherry", "orange"]
fruits[1:3] = ["mango"]
print(fruits)
```

**Expected output:**
```
['apple', 'mango', 'orange']
```

> "banana" and "cherry" (2 items) were replaced by only "mango" (1 item). The list shrank.

---

### 3.4 Inserting an Item Without Replacing — `insert()`

`insert(index, value)` adds a new item at a specific position *without* removing anything:

```python
fruits = ["apple", "banana", "cherry"]
fruits.insert(2, "watermelon")
print(fruits)
```

**Expected output:**
```
['apple', 'banana', 'watermelon', 'cherry']
```

> "watermelon" was inserted at position 2. "cherry" was pushed to position 3. Nothing was deleted.

---

## Part 4 – Adding Items to a List

### 4.1 The Three Ways to Add Items

| Method | What it does |
|---|---|
| `append(value)` | Adds one item to the **end** of the list |
| `insert(index, value)` | Adds one item at a **specific position** |
| `extend(iterable)` | Adds **multiple items** from another list (or any iterable) to the end |

---

### 4.2 `append()` — Add to the End

```python
fruits = ["apple", "banana", "cherry"]
fruits.append("orange")
print(fruits)
```

**Expected output:**
```
['apple', 'banana', 'cherry', 'orange']
```

> `append()` is the most commonly used method for adding items. It always places the new item at the very end.

---

**Second example — building a list step by step:**

```python
shopping = []
shopping.append("milk")
shopping.append("eggs")
shopping.append("bread")
print(shopping)
```

**Expected output:**
```
['milk', 'eggs', 'bread']
```

> We started with an **empty list** `[]` and built it up one item at a time. This pattern is extremely common in real programs.

---

### 4.3 `insert()` — Add at a Specific Position

We already saw `insert()` in Part 3, but here it is as an *add* operation:

```python
fruits = ["apple", "banana", "cherry"]
fruits.insert(1, "kiwi")
print(fruits)
```

**Expected output:**
```
['apple', 'kiwi', 'banana', 'cherry']
```

> "kiwi" was inserted at position 1. Everything from position 1 onwards was shifted right by one.

**Insert at the beginning (position 0):**

```python
fruits = ["apple", "banana", "cherry"]
fruits.insert(0, "strawberry")
print(fruits)
```

**Expected output:**
```
['strawberry', 'apple', 'banana', 'cherry']
```

---

### 4.4 `extend()` — Add Multiple Items from Another List

```python
fruits = ["apple", "banana", "cherry"]
more_fruits = ["mango", "pineapple", "papaya"]
fruits.extend(more_fruits)
print(fruits)
```

**Expected output:**
```
['apple', 'banana', 'cherry', 'mango', 'pineapple', 'papaya']
```

> Every item from `more_fruits` was added individually to the end of `fruits`.

---

**`extend()` vs `append()` — the key difference:**

```python
fruits = ["apple", "banana"]

# append adds the whole list AS ONE item:
fruits.append(["mango", "kiwi"])
print(fruits)
```

**Expected output:**
```
['apple', 'banana', ['mango', 'kiwi']]
```

```python
fruits = ["apple", "banana"]

# extend adds each item separately:
fruits.extend(["mango", "kiwi"])
print(fruits)
```

**Expected output:**
```
['apple', 'banana', 'mango', 'kiwi']
```

> **Common beginner mistake:** Using `append()` when you meant `extend()`. The result is a nested list instead of a flat list.

---

**`extend()` also works with other iterables** like tuples:

```python
fruits = ["apple", "banana", "cherry"]
fruits.extend(("kiwi", "orange"))
print(fruits)
```

**Expected output:**
```
['apple', 'banana', 'cherry', 'kiwi', 'orange']
```

---

## Part 5 – Removing Items from a List

### 5.1 The Ways to Remove Items

| Method / Keyword | What it does |
|---|---|
| `remove(value)` | Removes the **first occurrence** of a specific value |
| `pop(index)` | Removes the item at a **specific index** (default: last item) |
| `del list[index]` | Deletes item at a specific index, or deletes the whole list |
| `clear()` | Empties the list completely (list still exists, but has no items) |

---

### 5.2 `remove()` — Remove by Value

```python
fruits = ["apple", "banana", "cherry"]
fruits.remove("banana")
print(fruits)
```

**Expected output:**
```
['apple', 'cherry']
```

> "banana" was found and removed. The list shrank by one.

---

**What if the value appears more than once?**

`remove()` only deletes the **first** occurrence:

```python
fruits = ["apple", "banana", "cherry", "banana", "mango"]
fruits.remove("banana")
print(fruits)
```

**Expected output:**
```
['apple', 'cherry', 'banana', 'mango']
```

> Only the first "banana" (at index 1) was removed. The second "banana" (originally at index 3) remains.

---

**What if the value does not exist?**

```python
fruits = ["apple", "banana", "cherry"]
fruits.remove("mango")   # "mango" is not in the list
```

**Expected output:**
```
ValueError: list.remove(x): x not in list
```

> **Common beginner mistake:** Calling `remove()` on a value that is not in the list. Always check first with `in` if you are unsure.

**Safe version:**

```python
fruits = ["apple", "banana", "cherry"]
if "mango" in fruits:
    fruits.remove("mango")
else:
    print("mango was not found in the list")
```

**Expected output:**
```
mango was not found in the list
```

---

### 5.3 `pop()` — Remove by Index

`pop()` removes and **returns** the item at a given index. If no index is given, it removes the **last** item.

```python
fruits = ["apple", "banana", "cherry"]
fruits.pop(1)
print(fruits)
```

**Expected output:**
```
['apple', 'cherry']
```

---

**`pop()` without an index — removes the last item:**

```python
fruits = ["apple", "banana", "cherry"]
fruits.pop()
print(fruits)
```

**Expected output:**
```
['apple', 'banana']
```

---

**`pop()` returns the removed item** — you can store it:

```python
fruits = ["apple", "banana", "cherry"]
removed = fruits.pop(1)
print("Removed:", removed)
print("List now:", fruits)
```

**Expected output:**
```
Removed: banana
List now: ['apple', 'cherry']
```

> This is very useful when you want to *process* the item you are removing.

---

### 5.4 `del` — Delete by Index or Slice

The `del` keyword deletes an item at a specific index:

```python
fruits = ["apple", "banana", "cherry"]
del fruits[0]
print(fruits)
```

**Expected output:**
```
['banana', 'cherry']
```

---

**Delete a slice:**

```python
fruits = ["apple", "banana", "cherry", "orange", "kiwi"]
del fruits[1:3]
print(fruits)
```

**Expected output:**
```
['apple', 'orange', 'kiwi']
```

---

**Delete the entire list variable:**

```python
fruits = ["apple", "banana", "cherry"]
del fruits
# print(fruits)   # This would now cause a NameError — the variable no longer exists
```

> After `del fruits`, the variable `fruits` is completely gone from memory. This is different from `clear()`.

---

### 5.5 `clear()` — Empty the List

`clear()` removes all items from the list, but the list variable itself still exists:

```python
fruits = ["apple", "banana", "cherry"]
fruits.clear()
print(fruits)
```

**Expected output:**
```
[]
```

> The list is now empty `[]`, but `fruits` still exists as a variable. You can add new items to it later.

---

## Part 6 – Guided Practice Exercises

### Exercise 1 – Class Register

**Objective:** Create and display a list of student names.

**Scenario:** You are a teacher building a digital class register.

**Steps:**

1. Create a list called `students` with five student names.
2. Print the full list.
3. Print just the first student.
4. Print just the last student using negative indexing.
5. Print the number of students using `len()`.

**Starter code:**

```python
students = ["Alice", "Bob", "Charlie", "Diana", "Eve"]
# Your code below:
```

**Expected output:**

```
['Alice', 'Bob', 'Charlie', 'Diana', 'Eve']
Alice
Eve
5
```

**Self-check questions:**
- What index does "Charlie" have?
- What would `students[-2]` return?
- What would `students[1:4]` return?

---

### Exercise 2 – Shopping Cart

**Objective:** Practice adding and removing items from a list.

**Scenario:** You are building a simple shopping cart.

**Steps:**

1. Start with an empty list called `cart`.
2. Use `append()` to add: "milk", "eggs", "bread", "cheese".
3. Print the cart.
4. The customer changed their mind — remove "eggs" using `remove()`.
5. Add "yoghurt" at position 1 using `insert()`.
6. Print the final cart.
7. Print the total number of items.

**Expected output:**

```
['milk', 'eggs', 'bread', 'cheese']
['milk', 'yoghurt', 'bread', 'cheese']
4
```

**Optional what-if challenge:** What would happen if you used `pop(0)` instead of `remove("eggs")`?

---

### Exercise 3 – Temperature Log

**Objective:** Practice slicing and modifying a list.

**Scenario:** A weather station recorded temperatures for a week (in °C).

```python
temperatures = [22, 19, 25, 30, 28, 17, 21]
# Days:          Mon Tue Wed Thu  Fri  Sat Sun
```

**Tasks:**

1. Print the temperature for Wednesday (index 2).
2. Print temperatures for Tuesday to Friday (use slicing).
3. The Saturday reading was wrong — it should be 20. Fix it.
4. Print the updated list.
5. Check whether the temperature 30 is in the list and print a message.

**Expected output:**

```
25
[19, 25, 30, 28]
[22, 19, 25, 30, 28, 20, 21]
30 degrees was recorded this week.
```

---

### Exercise 4 – Combining Two Inventories

**Objective:** Practice using `extend()`.

**Scenario:** Two warehouses need to merge their stock lists.

```python
warehouse_a = ["screws", "bolts", "nails"]
warehouse_b = ["hammers", "drills", "saws"]
```

1. Use `extend()` to merge `warehouse_b` into `warehouse_a`.
2. Print the combined list.
3. Use `del` to remove "bolts" by index.
4. Print the final list.

**Expected output:**

```
['screws', 'bolts', 'nails', 'hammers', 'drills', 'saws']
['screws', 'nails', 'hammers', 'drills', 'saws']
```

---

## Part 7 – Mini-Project: Student Grade Tracker

### Project Overview

You will build a **Student Grade Tracker** — a small Python program that stores student names and their exam scores, allows grade updates, adds new students, and removes students who have withdrawn.

This project uses every skill from today's lesson.

---

### Stage 1 – Setup

Create two lists: one for student names, one for their scores. Each index position corresponds to the same student.

```python
# Stage 1 – Create the lists
names  = ["Alice", "Bob", "Charlie", "Diana", "Eve"]
scores = [88, 74, 91, 65, 83]

print("Students:", names)
print("Scores:  ", scores)
print("Total students:", len(names))
```

**Milestone output:**

```
Students: ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve']
Scores:   [88, 74, 91, 65, 83]
Total students: 5
```

---

### Stage 2 – Access and Display

Print each student with their score using index access:

```python
# Stage 2 – Access individual records
print("\n--- Grade Report ---")
print("First student:", names[0], "→ Score:", scores[0])
print("Last student: ", names[-1], "→ Score:", scores[-1])
print("Top 3 students:", names[:3], "→ Scores:", scores[:3])
```

**Milestone output:**

```
--- Grade Report ---
First student: Alice → Score: 88
Last student:  Eve → Score: 83
Top 3 students: ['Alice', 'Bob', 'Charlie'] → Scores: [88, 74, 91]
```

---

### Stage 3 – Update a Score

Bob re-sat his exam and scored 85. Update his score:

```python
# Stage 3 – Update Bob's score (Bob is at index 1)
scores[1] = 85
print("\nUpdated scores:", scores)
print("Bob's new score:", scores[1])
```

**Milestone output:**

```
Updated scores: [88, 85, 91, 65, 83]
Bob's new score: 85
```

---

### Stage 4 – Add a New Student

A new student, Frank, joins with a score of 79:

```python
# Stage 4 – Add a new student
names.append("Frank")
scores.append(79)

print("\nAfter adding Frank:")
print("Students:", names)
print("Scores:  ", scores)
print("Total:", len(names))
```

**Milestone output:**

```
After adding Frank:
Students: ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve', 'Frank']
Scores:   [88, 85, 91, 65, 83, 79]
Total: 6
```

---

### Stage 5 – Remove a Withdrawn Student

Diana has withdrawn from the course. Remove her:

```python
# Stage 5 – Remove Diana
diana_index = names.index("Diana")   # Find her position
names.pop(diana_index)
scores.pop(diana_index)

print("\nAfter Diana withdrew:")
print("Students:", names)
print("Scores:  ", scores)
print("Total:", len(names))
```

**Milestone output:**

```
After Diana withdrew:
Students: ['Alice', 'Bob', 'Charlie', 'Eve', 'Frank']
Scores:   [88, 85, 91, 83, 79]
Total: 5
```

---

### Stage 6 – Final Report

Display the complete final class list:

```python
# Stage 6 – Final report
print("\n========== FINAL CLASS REPORT ==========")
for i in range(len(names)):
    print(f"  {names[i]:<10} Score: {scores[i]}")
print("=========================================")
print(f"Class size: {len(names)} students")
```

**Milestone output:**

```
========== FINAL CLASS REPORT ==========
  Alice      Score: 88
  Bob        Score: 85
  Charlie    Score: 91
  Eve        Score: 83
  Frank      Score: 79
=========================================
Class size: 5 students
```

---

### Reflection Questions

1. Why did we use `names.index("Diana")` before calling `pop()` instead of just using `pop()` directly?
2. What would happen if two students had the same name and you called `names.index()` on that name?
3. How would you modify this project to also track each student's letter grade (A, B, C, etc.)?
4. Could you use a single list of lists (nested lists) instead of two parallel lists? What would that look like?

---

### Optional Extensions

- Calculate and print the **average** score
- Find and print the **highest** and **lowest** score using `max()` and `min()`
- Sort students alphabetically using `.sort()`
- Add a function that searches for a student by name and returns their score

---

## Part 8 – Common Beginner Mistakes (Summary)

### Mistake 1 – IndexError: Index Out of Range

```python
# WRONG
fruits = ["apple", "banana", "cherry"]
print(fruits[3])   # Only indexes 0, 1, 2 exist!
```
```
IndexError: list index out of range
```

**Fix:** Remember that a list of `n` items has indexes `0` to `n-1`. Use `len(fruits) - 1` for the last valid index.

---

### Mistake 2 – Confusing `append()` and `extend()`

```python
# WRONG – adds nested list
fruits = ["apple", "banana"]
fruits.append(["cherry", "mango"])
print(fruits)   # ['apple', 'banana', ['cherry', 'mango']]
```

**Fix:** Use `extend()` when you want to add multiple items individually:

```python
fruits = ["apple", "banana"]
fruits.extend(["cherry", "mango"])
print(fruits)   # ['apple', 'banana', 'cherry', 'mango']
```

---

### Mistake 3 – `remove()` on a Non-Existent Value

```python
# WRONG
fruits = ["apple", "banana"]
fruits.remove("grape")   # ValueError!
```

**Fix:** Check first with `in`:

```python
if "grape" in fruits:
    fruits.remove("grape")
```

---

### Mistake 4 – Forgetting That Slicing Does NOT Include the End Index

```python
fruits = ["apple", "banana", "cherry", "orange"]
print(fruits[1:3])   # Returns items at index 1 AND 2 — NOT 3
```
```
['banana', 'cherry']
```

> The slice `[1:3]` means "from index 1 up to but NOT including index 3".

---

### Mistake 5 – `del` vs `clear()` vs Setting to `[]`

```python
fruits = ["apple", "banana"]

# del removes the variable entirely
del fruits
# print(fruits)   # NameError — 'fruits' does not exist!

# clear() empties the list, but the variable still exists
fruits = ["apple", "banana"]
fruits.clear()
print(fruits)     # []  — variable exists, just empty

# Assigning [] replaces the list with a new empty one
fruits = ["apple", "banana"]
fruits = []
print(fruits)     # []
```

---

### Mistake 6 – Modifying a List While Looping Over It

This is an advanced mistake to be aware of. Avoid removing items from a list inside a `for` loop that is iterating over the same list — it causes unexpected behaviour. Use a copy or a different approach.

---

## Reflection Questions

1. What is the difference between a **list** and a simple variable?
2. Why does Python start list indexes at 0 instead of 1?
3. When would you use `pop()` instead of `remove()`?
4. What is the difference between `append()` and `extend()`?
5. What happens to the list after you call `clear()` — does the variable disappear?
6. How would you get the last three items of a list without knowing its exact length?
7. What does `del my_list` do that is different from `my_list.clear()`?
8. If a list has 7 items, what is the index of the last item?

---

## Completion Checklist

Before moving on, confirm you can:

- [ ] Create a list using square brackets `[]`
- [ ] Create an empty list and build it up using `append()`
- [ ] Access any item by its positive index
- [ ] Access items using negative indexes
- [ ] Slice a list to get a range of items
- [ ] Check whether a value is in a list using `in`
- [ ] Change a single item by assigning to its index
- [ ] Change multiple items using slice assignment
- [ ] Add an item to the end with `append()`
- [ ] Add an item at a specific position with `insert()`
- [ ] Merge another list using `extend()`
- [ ] Remove an item by value with `remove()`
- [ ] Remove an item by index with `pop()`
- [ ] Delete an item with `del`
- [ ] Empty a list with `clear()`
- [ ] Explain the difference between `append()` and `extend()`
- [ ] Explain the difference between `del` and `clear()`
- [ ] Complete the Student Grade Tracker mini-project

---

## Lesson Summary

In this lesson you learned everything about Python lists — one of the most fundamental and powerful tools in the entire language.

**What a list is:** An ordered, changeable collection of items, written with square brackets and commas. Lists allow duplicate values and can hold any data type — including other lists.

**How to access items:** Use a zero-based index in square brackets. Negative indexes count from the end. Slicing (`[start:end]`) extracts a section of the list. The `in` keyword checks for membership.

**How to change items:** Assign a new value to an index (`list[0] = "new"`). Assign to a slice to replace multiple items at once. Use `insert(index, value)` to add without replacing.

**How to add items:** Use `append(value)` for the end, `insert(index, value)` for a specific position, and `extend(iterable)` to add all items from another list.

**How to remove items:** Use `remove(value)` to delete by value (first occurrence), `pop(index)` to delete by index (and optionally capture the removed value), `del list[index]` to delete by index or slice, and `clear()` to empty the list entirely.

**Why this matters in the real world:** Lists power virtually every Python application — from storing datasets in data science, to managing game objects, to tracking inventory in business systems, to building web application features. Mastering lists is one of the most important milestones in learning Python.

---

*End of Lesson 07 – Python Lists*
