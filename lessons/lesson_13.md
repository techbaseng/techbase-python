---
render_with_liquid: false
title: "Lesson 13: Python Sets — Everything You Need to Know"
nav_order: 13
---

# Lesson 13: Python Sets — Everything You Need to Know

---

## Lesson Introduction

Welcome to Lesson 13! In this lesson, you will learn all about **Python Sets** — one of Python's four built-in collection types.

By the end of this lesson, you will be able to:
- Create and use sets
- Understand what makes sets unique (no duplicates, no order, no index)
- Access, add, and remove items from sets
- Loop through sets
- Join sets together using several powerful methods
- Work with frozensets (the "frozen" version of a set)
- Use all built-in set methods confidently
- Complete exercises and a mini project using sets

Even if you have never heard of the word "set" in programming before, **that is completely fine**. We will start from zero and build up to real-world usage step by step.

> **Quick analogy before we start:** Think of a set like a bag of lottery balls. Each number appears only once. You cannot pull ball number 7 twice. You cannot look at ball "number 3 by position" — you just reach in and grab one. That is how Python sets work.

---

## Prerequisite Concepts

Before we dive into sets, let us quickly review a few building blocks you should be comfortable with.

### What is a Collection?

In Python, a **collection** is a single variable that holds multiple values at once. Instead of writing:

```python
fruit1 = "apple"
fruit2 = "banana"
fruit3 = "cherry"
```

You can store them together in one collection. Python has four main collection types:

| Collection | Ordered? | Changeable? | Duplicates? |
|------------|----------|-------------|-------------|
| **List**   | Yes      | Yes         | Yes         |
| **Tuple**  | Yes      | No          | Yes         |
| **Set**    | No       | Items fixed* | No         |
| **Dictionary** | Yes (Python 3.7+) | Yes | No (keys) |

> \* In a set, you cannot *change* an existing item, but you *can* add or remove items.

You do not need to master all four types to learn sets. Just know that sets have their own special rules.

### What is a `for` Loop?

A `for` loop lets you go through every item in a collection one by one.

```python
for x in ["apple", "banana"]:
    print(x)
```

**Output:**
```
apple
banana
```

We will use `for` loops to access items in sets later.

### What is the `in` Keyword?

The `in` keyword checks whether a value exists inside a collection. It returns `True` or `False`.

```python
print("apple" in ["apple", "banana"])
```

**Output:**
```
True
```

---

## Part 1: What Is a Set?

### The Big Idea

A **set** is a collection that:
1. **Has no fixed order** — you cannot predict which item comes first
2. **Does not allow duplicates** — each value can appear only once
3. **Does not use index numbers** — you cannot do `myset[0]`

### Why Do Sets Exist?

Sets are incredibly useful when you want to:
- Store a **unique list** of things (e.g., unique visitor IDs, unique words in a document)
- Quickly **check if something exists** in a large collection
- Compare two groups using **mathematical set operations** (union, intersection, difference)

Think of a guest list for an event: every name should appear only once, and you do not care what "position" each guest is in — you just want to know if someone is on the list.

---

## Part 2: Creating a Set

### Method 1 — Curly Brackets `{}`

Sets are written using **curly brackets** `{}`, with items separated by commas.

```python
fruits = {"apple", "banana", "cherry"}
print(fruits)
```

**Output (order may vary each run):**
```
{'cherry', 'apple', 'banana'}
```

> **Important:** Notice the output order is different from the input order. Sets do **not** preserve insertion order. This is normal and expected.

### Method 2 — The `set()` Constructor

You can also create a set from a list using the `set()` function. Notice the **double round brackets** — the outer ones belong to `set()`, and the inner ones wrap your list.

```python
fruits = set(("apple", "banana", "cherry"))
print(fruits)
```

**Output:**
```
{'cherry', 'banana', 'apple'}
```

> **Tip:** Use `set()` when you have data already stored in a list and you want to convert it to a set (for example, to remove duplicates instantly).

### Micro Demo: Removing Duplicates Instantly with `set()`

```python
names = ["Alice", "Bob", "Alice", "Charlie", "Bob"]
unique_names = set(names)
print(unique_names)
```

**Output:**
```
{'Charlie', 'Alice', 'Bob'}
```

The duplicates are automatically removed. This is one of the most practical uses of sets!

---

## Part 3: Set Properties in Detail

### 3.1 Unordered — No Fixed Position

Every time you print a set, the items may appear in a different order. Python does not guarantee any particular sequence.

```python
my_set = {"dog", "cat", "bird"}
print(my_set)
print(my_set)
```

**Output (may vary between runs):**
```
{'bird', 'cat', 'dog'}
{'cat', 'dog', 'bird'}
```

> **Thinking prompt:** If sets have no order, how do we work with the items? We use loops and membership checks — which we will cover in Part 5.

### 3.2 No Duplicates Allowed

If you add the same value twice, the set keeps only one copy.

```python
colours = {"red", "blue", "red", "green", "blue"}
print(colours)
```

**Output:**
```
{'green', 'blue', 'red'}
```

`"red"` and `"blue"` were each added twice but appear only once.

### 3.3 Special Rule: `True` and `1` Are the Same; `False` and `0` Are the Same

In Python, `True` equals `1` and `False` equals `0` numerically. Sets treat them as duplicates:

```python
s = {"apple", "banana", True, 1, 2}
print(s)
```

**Output:**
```
{True, 2, 'banana', 'apple'}
```

> `True` and `1` are the same value, so the set keeps only one. `True` was listed first, so it is kept.

```python
s2 = {"apple", False, 0, "cherry"}
print(s2)
```

**Output:**
```
{False, 'cherry', 'apple'}
```

> `False` and `0` are treated as one value.

### 3.4 Unchangeable Items

Once you create a set, you **cannot change an existing item**. You cannot say "change 'apple' to 'mango'" directly. However, you *can* remove an item and add a new one.

### 3.5 Mixed Data Types Are Allowed

A set can hold strings, integers, booleans, and even floats — all in the same set.

```python
mixed = {"hello", 42, True, 3.14}
print(mixed)
```

**Output:**
```
{True, 3.14, 42, 'hello'}
```

> **Note:** A set **cannot** contain mutable (changeable) objects like lists or other sets as items. That would cause an error.

---

## Part 4: Set Length and Data Type

### Getting the Number of Items — `len()`

```python
fruits = {"apple", "banana", "cherry"}
print(len(fruits))
```

**Output:**
```
3
```

`len()` counts how many items are in the set.

### Checking the Data Type — `type()`

```python
my_set = {"apple", "banana"}
print(type(my_set))
```

**Output:**
```
<class 'set'>
```

This confirms Python sees it as a set object.

---

## Part 5: Accessing Set Items

### The Key Rule: No Index Access

Because sets are unordered, there is **no position 0, 1, or 2**. This means you **cannot** do:

```python
# This will cause an ERROR!
fruits = {"apple", "banana", "cherry"}
print(fruits[0])   # ❌ TypeError: 'set' object is not subscriptable
```

So how do we work with the items? Two ways:

### Method 1 — Loop Through with `for`

```python
fruits = {"apple", "banana", "cherry"}

for item in fruits:
    print(item)
```

**Output (order may vary):**
```
cherry
banana
apple
```

Each item gets assigned to the variable `item` one at a time, and we print it.

### Method 2 — Check Membership with `in`

To ask "is this value in the set?", use `in`. This returns `True` or `False`.

```python
fruits = {"apple", "banana", "cherry"}

print("banana" in fruits)
print("mango" in fruits)
```

**Output:**
```
True
False
```

### Checking with `not in`

```python
fruits = {"apple", "banana", "cherry"}

print("mango" not in fruits)
```

**Output:**
```
True
```

> **Real-world use:** Imagine a set of banned usernames. When a new user registers, you check: `if new_username in banned_usernames:`. This runs extremely fast even with millions of entries — sets use a technique called **hashing** that makes lookups almost instant.

---

## Part 6: Adding Items to a Set

### 6.1 Adding One Item — `.add()`

The `.add()` method adds **one item** to the set.

```python
fruits = {"apple", "banana", "cherry"}
fruits.add("mango")
print(fruits)
```

**Output:**
```
{'mango', 'banana', 'cherry', 'apple'}
```

> **What if you add a duplicate?** Nothing happens. The set stays the same.

```python
fruits = {"apple", "banana", "cherry"}
fruits.add("apple")  # already exists
print(fruits)
```

**Output:**
```
{'cherry', 'banana', 'apple'}
```

No error, no change — the duplicate is simply ignored.

### 6.2 Adding Multiple Items — `.update()`

The `.update()` method adds **multiple items** from any iterable (a list, tuple, or even another set).

**From a list:**
```python
fruits = {"apple", "banana"}
fruits.update(["mango", "grape", "cherry"])
print(fruits)
```

**Output:**
```
{'mango', 'apple', 'banana', 'grape', 'cherry'}
```

**From another set:**
```python
set_a = {"apple", "banana"}
set_b = {"cherry", "mango"}
set_a.update(set_b)
print(set_a)
```

**Output:**
```
{'banana', 'cherry', 'apple', 'mango'}
```

**From a tuple:**
```python
colours = {"red", "blue"}
colours.update(("green", "yellow"))
print(colours)
```

**Output:**
```
{'red', 'green', 'blue', 'yellow'}
```

> **Summary:** Use `.add()` for one item, `.update()` for many items.

---

## Part 7: Removing Items from a Set

There are several ways to remove items from a set. Let us learn each one.

### 7.1 `.remove(value)` — Remove a Specific Item

```python
fruits = {"apple", "banana", "cherry"}
fruits.remove("banana")
print(fruits)
```

**Output:**
```
{'cherry', 'apple'}
```

> ⚠️ **Warning:** If the value does **not** exist, `.remove()` will raise a `KeyError`. Always be sure the item exists before using `.remove()`.

```python
fruits = {"apple", "cherry"}
fruits.remove("banana")  # ❌ KeyError: 'banana'
```

### 7.2 `.discard(value)` — Safe Removal (No Error)

`.discard()` works exactly like `.remove()`, but if the item is not found, **it does nothing** instead of raising an error.

```python
fruits = {"apple", "banana", "cherry"}
fruits.discard("banana")  # works fine
fruits.discard("mango")   # item doesn't exist — no error!
print(fruits)
```

**Output:**
```
{'cherry', 'apple'}
```

> **When to use `.discard()` vs `.remove()`:**
> - Use `.remove()` when you are *sure* the item exists and want an error if it doesn't (to catch bugs).
> - Use `.discard()` when it's OK if the item isn't there.

### 7.3 `.pop()` — Remove a Random Item

Since sets have no order, `.pop()` removes and returns **a random item**.

```python
fruits = {"apple", "banana", "cherry"}
removed = fruits.pop()
print("Removed:", removed)
print("Remaining:", fruits)
```

**Output (varies — any item could be removed):**
```
Removed: cherry
Remaining: {'apple', 'banana'}
```

> **Use case:** `.pop()` is useful when you want to process and remove items from a set one at a time (like a queue where order doesn't matter).

### 7.4 `.clear()` — Remove All Items

Empties the set completely but keeps the set object.

```python
fruits = {"apple", "banana", "cherry"}
fruits.clear()
print(fruits)
```

**Output:**
```
set()
```

> `set()` means an empty set. (Note: `{}` alone creates an empty *dictionary*, not a set — be careful!)

### 7.5 `del` — Delete the Set Entirely

The `del` keyword deletes the variable itself from memory.

```python
fruits = {"apple", "banana", "cherry"}
del fruits
print(fruits)   # ❌ NameError: name 'fruits' is not defined
```

After `del fruits`, the variable no longer exists at all.

### Removal Method Comparison Table

| Method         | What it does                         | Error if not found? |
|----------------|--------------------------------------|---------------------|
| `.remove(x)`   | Removes item x                       | Yes — `KeyError`    |
| `.discard(x)`  | Removes item x if it exists          | No                  |
| `.pop()`       | Removes and returns a random item    | Error if set empty  |
| `.clear()`     | Removes all items                    | No                  |
| `del setname`  | Deletes the set variable entirely    | No                  |

---

## Part 8: Looping Through a Set

You can use a `for` loop to visit every item in a set.

### Basic Loop

```python
countries = {"Nigeria", "Ghana", "Kenya"}

for country in countries:
    print(country)
```

**Output (order may vary):**
```
Kenya
Ghana
Nigeria
```

### Loop with Condition

```python
numbers = {10, 25, 7, 42, 3, 18}

for num in numbers:
    if num > 10:
        print(num, "is greater than 10")
```

**Output (order may vary):**
```
25 is greater than 10
42 is greater than 10
18 is greater than 10
```

### Loop to Build a New List from a Set

```python
words = {"hello", "world", "python"}
upper_words = []

for word in words:
    upper_words.append(word.upper())

print(upper_words)
```

**Output:**
```
['WORLD', 'HELLO', 'PYTHON']
```

> **Real-world use:** Loop through a set of unique product IDs, check each one in a database, and collect results.

---

## Part 9: Joining Sets

This is one of the most powerful features of sets. You can combine two or more sets using several methods, each doing something slightly different.

### 9.1 `.union()` — All Items from Both Sets (No Duplicates)

`union()` returns a **new set** containing every item from both sets, with duplicates removed.

```python
set1 = {"apple", "banana", "cherry"}
set2 = {"cherry", "mango", "grape"}

result = set1.union(set2)
print(result)
```

**Output:**
```
{'grape', 'cherry', 'apple', 'mango', 'banana'}
```

Notice `"cherry"` appears only once even though it is in both sets.

You can also use the `|` operator (pipe symbol) as a shortcut:

```python
result = set1 | set2
print(result)
```

**Output:**
```
{'grape', 'cherry', 'apple', 'mango', 'banana'}
```

### 9.2 `.update()` — Join Into the Original Set

Unlike `.union()`, `.update()` **modifies the original set in place** rather than returning a new one.

```python
set1 = {"apple", "banana"}
set2 = {"cherry", "mango"}

set1.update(set2)
print(set1)
```

**Output:**
```
{'banana', 'cherry', 'apple', 'mango'}
```

> **Difference:** `union()` → creates a new set. `update()` → changes the existing set.

### 9.3 `.intersection()` — Only Items in Both Sets

`intersection()` returns only the items that appear in **all** sets being compared.

```python
set1 = {"apple", "banana", "cherry"}
set2 = {"banana", "cherry", "mango"}

result = set1.intersection(set2)
print(result)
```

**Output:**
```
{'banana', 'cherry'}
```

Only `"banana"` and `"cherry"` exist in both sets.

Shortcut using `&`:
```python
result = set1 & set2
```

### 9.4 `.intersection_update()` — Intersection In Place

Like `.update()` vs `.union()`, this modifies the original set instead of returning a new one.

```python
set1 = {"apple", "banana", "cherry"}
set2 = {"banana", "cherry", "mango"}

set1.intersection_update(set2)
print(set1)
```

**Output:**
```
{'banana', 'cherry'}
```

### 9.5 `.difference()` — Items in First Set but NOT in Second

```python
set1 = {"apple", "banana", "cherry"}
set2 = {"banana", "cherry", "mango"}

result = set1.difference(set2)
print(result)
```

**Output:**
```
{'apple'}
```

Only `"apple"` is in `set1` but not in `set2`.

Shortcut using `-`:
```python
result = set1 - set2
```

### 9.6 `.difference_update()` — Difference In Place

```python
set1 = {"apple", "banana", "cherry"}
set2 = {"banana", "cherry"}

set1.difference_update(set2)
print(set1)
```

**Output:**
```
{'apple'}
```

### 9.7 `.symmetric_difference()` — Items in Either But NOT Both

This gives you all items that are **unique to each set** — items that appear in only one of the two sets.

```python
set1 = {"apple", "banana", "cherry"}
set2 = {"banana", "cherry", "mango"}

result = set1.symmetric_difference(set2)
print(result)
```

**Output:**
```
{'apple', 'mango'}
```

`"apple"` is only in `set1`. `"mango"` is only in `set2`. `"banana"` and `"cherry"` are in both, so they are excluded.

Shortcut using `^`:
```python
result = set1 ^ set2
```

### 9.8 `.symmetric_difference_update()` — Symmetric Difference In Place

```python
set1 = {"apple", "banana", "cherry"}
set2 = {"banana", "cherry", "mango"}

set1.symmetric_difference_update(set2)
print(set1)
```

**Output:**
```
{'apple', 'mango'}
```

### Visual Summary of Join Methods

```
set1 = {A, B, C}
set2 = {B, C, D}

union()                  → {A, B, C, D}   — everything
intersection()           → {B, C}          — only shared items
difference(set2)         → {A}             — in set1, not set2
difference(set1)         → {D}             — in set2, not set1
symmetric_difference()   → {A, D}          — unique to each
```

---

## Part 10: Set Methods for Comparison

Beyond joining, sets have powerful comparison methods.

### `.issubset()` — Is One Set Contained in Another?

```python
set1 = {"banana", "cherry"}
set2 = {"apple", "banana", "cherry", "mango"}

print(set1.issubset(set2))
```

**Output:**
```
True
```

Every item in `set1` is also in `set2`, so `set1` is a subset of `set2`.

### `.issuperset()` — Does One Set Contain All Items of Another?

```python
print(set2.issuperset(set1))
```

**Output:**
```
True
```

### `.isdisjoint()` — Do the Sets Share No Items?

```python
set1 = {"apple", "banana"}
set2 = {"cherry", "mango"}

print(set1.isdisjoint(set2))
```

**Output:**
```
True
```

They share nothing in common, so they are "disjoint."

```python
set3 = {"apple", "grape"}
print(set1.isdisjoint(set3))
```

**Output:**
```
False
```

`"apple"` is shared, so they are not disjoint.

### `.copy()` — Make a Copy of a Set

```python
original = {"apple", "banana", "cherry"}
copy_set = original.copy()
copy_set.add("mango")

print("Original:", original)
print("Copy:", copy_set)
```

**Output:**
```
Original: {'cherry', 'apple', 'banana'}
Copy: {'cherry', 'apple', 'banana', 'mango'}
```

The original is unchanged. This is important — if you just did `copy_set = original`, both variables would point to the **same** set object.

---

## Part 11: Complete Set Methods Reference

Here is a full reference table of all Python set methods:

| Method                         | Description                                                        |
|--------------------------------|--------------------------------------------------------------------|
| `add(x)`                       | Adds one element to the set                                        |
| `clear()`                      | Removes all elements                                               |
| `copy()`                       | Returns a shallow copy of the set                                  |
| `difference(set2)`             | Returns items in set but not in set2                               |
| `difference_update(set2)`      | Removes items in set that also appear in set2                      |
| `discard(x)`                   | Removes x if present (no error if not found)                       |
| `intersection(set2)`           | Returns items present in both sets                                 |
| `intersection_update(set2)`    | Keeps only items present in both sets                              |
| `isdisjoint(set2)`             | Returns True if sets have no common items                          |
| `issubset(set2)`               | Returns True if all items in this set are also in set2             |
| `issuperset(set2)`             | Returns True if this set contains all items of set2                |
| `pop()`                        | Removes and returns a random item                                  |
| `remove(x)`                    | Removes x; raises KeyError if not found                            |
| `symmetric_difference(set2)`   | Returns items in either set but not both                           |
| `symmetric_difference_update(set2)` | Keeps only items that are unique to each set                  |
| `union(set2)`                  | Returns all items from both sets                                   |
| `update(iterable)`             | Adds all items from an iterable into this set                      |

---

## Part 12: Frozenset — The Immutable Set

### What Is a Frozenset?

A **frozenset** is a set that **cannot be changed at all** after creation. You cannot add items, remove items, or modify it in any way.

Think of it like a sealed envelope — once you seal it, nothing goes in or out.

### Why Use Frozenset?

- When you want the **protection of a set** (unique items, membership testing) but need **immutability**
- Frozensets can be used as **dictionary keys** or as **items inside another set** (regular sets cannot do this!)
- Useful when sharing data between functions and you want to ensure no one can accidentally change it

### Creating a Frozenset

```python
fruits = frozenset({"apple", "banana", "cherry"})
print(fruits)
```

**Output:**
```
frozenset({'cherry', 'banana', 'apple'})
```

You can also create from a list:

```python
numbers = frozenset([1, 2, 3, 4, 5])
print(numbers)
```

**Output:**
```
frozenset({1, 2, 3, 4, 5})
```

### Frozenset Is Immutable — You Cannot Change It

```python
fruits = frozenset({"apple", "banana"})
fruits.add("mango")   # ❌ AttributeError: 'frozenset' object has no attribute 'add'
```

Any attempt to add, remove, or update a frozenset raises an error.

### Frozenset Can Still Be Iterated and Tested

Even though you cannot change it, you can still loop through it and check membership:

```python
fruits = frozenset({"apple", "banana", "cherry"})

for item in fruits:
    print(item)

print("apple" in fruits)
```

**Output:**
```
apple
banana
cherry
True
```

### Frozenset Supports Set Operations

```python
fs1 = frozenset({"apple", "banana", "cherry"})
fs2 = frozenset({"banana", "mango"})

print(fs1.union(fs2))
print(fs1.intersection(fs2))
print(fs1.difference(fs2))
```

**Output:**
```
frozenset({'cherry', 'banana', 'mango', 'apple'})
frozenset({'banana'})
frozenset({'cherry', 'apple'})
```

### Frozenset as a Dictionary Key

This is something a regular set cannot do:

```python
# Using frozenset as a dictionary key
regions = {
    frozenset({"Lagos", "Abuja"}): "Nigeria",
    frozenset({"Accra", "Kumasi"}): "Ghana"
}
print(regions)
```

**Output:**
```
{frozenset({'Abuja', 'Lagos'}): 'Nigeria', frozenset({'Kumasi', 'Accra'}): 'Ghana'}
```

### Set vs Frozenset — Quick Comparison

| Feature           | `set`   | `frozenset` |
|-------------------|---------|-------------|
| Mutable           | Yes     | No          |
| Allows duplicates | No      | No          |
| Ordered           | No      | No          |
| Hashable (usable as dict key) | No | Yes   |
| Can use `.add()`  | Yes     | No          |
| Supports `in`     | Yes     | Yes         |
| Supports loops    | Yes     | Yes         |

---

## Part 13: Guided Practice Exercises

### Exercise 1: Creating and Inspecting a Set

**Objective:** Create a set and explore its basic properties.

**Scenario:** You are building a student attendance system. Store the names of students who attended class today.

**Steps:**
1. Create a set called `attended` with these names: `"Alice"`, `"Bob"`, `"Charlie"`, `"Alice"`, `"Diana"`, `"Bob"`
2. Print the set
3. Print the number of students who attended (using `len()`)
4. Check if `"Charlie"` is in the set
5. Check if `"Eve"` is in the set

**Expected Output:**
```
{'Diana', 'Bob', 'Charlie', 'Alice'}
4
True
False
```

**Solution:**
```python
attended = {"Alice", "Bob", "Charlie", "Alice", "Diana", "Bob"}
print(attended)
print(len(attended))
print("Charlie" in attended)
print("Eve" in attended)
```

**Self-check:** Did the output have 4 names even though 6 were provided? Good — sets removed the duplicates automatically!

---

### Exercise 2: Adding and Removing Items

**Objective:** Modify a set dynamically.

**Scenario:** The school tuck-shop sells snacks. Update the menu set as items run out or get added.

**Steps:**
1. Start with: `menu = {"pies", "juice", "biscuits", "chips"}`
2. Add `"water"` to the menu
3. Add `"cake"` and `"yoghurt"` using one method call
4. Remove `"chips"` safely (use `discard`)
5. Try to remove `"soda"` (which doesn't exist) safely
6. Print the final menu

**Expected Output:**
```
{'pies', 'juice', 'water', 'biscuits', 'yoghurt', 'cake'}
```

**Solution:**
```python
menu = {"pies", "juice", "biscuits", "chips"}
menu.add("water")
menu.update(["cake", "yoghurt"])
menu.discard("chips")
menu.discard("soda")  # no error
print(menu)
```

**What-if challenge:** What would happen if you used `.remove("soda")` instead of `.discard("soda")`?

---

### Exercise 3: Looping Through a Set

**Objective:** Use a `for` loop to process set items.

**Scenario:** You have a set of exam scores for different subjects. Print each score and classify it.

```python
scores = {72, 45, 88, 55, 91, 63}

for score in scores:
    if score >= 70:
        print(f"{score} — PASS")
    else:
        print(f"{score} — FAIL")
```

**Expected Output (order may vary):**
```
72 — PASS
45 — FAIL
88 — PASS
55 — FAIL
91 — PASS
63 — FAIL
```

**Self-check questions:**
- Why might the output order differ when you run the code again?
- How would you modify this to count the number of passes?

---

### Exercise 4: Set Operations (Union, Intersection, Difference)

**Objective:** Use set operations to compare two groups.

**Scenario:** Two classes took an elective subject. Find out:
- Who is in either class (union)
- Who is in both classes (intersection)
- Who is in Class A but not Class B (difference)

```python
class_a = {"Alice", "Bob", "Charlie", "Diana"}
class_b = {"Charlie", "Diana", "Eve", "Frank"}

# All students in either class
all_students = class_a.union(class_b)
print("All students:", all_students)

# Students in both classes
in_both = class_a.intersection(class_b)
print("In both:", in_both)

# Only in Class A
only_a = class_a.difference(class_b)
print("Only in Class A:", only_a)

# Only in Class B
only_b = class_b.difference(class_a)
print("Only in Class B:", only_b)

# Students unique to each class
unique_each = class_a.symmetric_difference(class_b)
print("Unique to each:", unique_each)
```

**Expected Output:**
```
All students: {'Charlie', 'Frank', 'Eve', 'Alice', 'Bob', 'Diana'}
In both: {'Charlie', 'Diana'}
Only in Class A: {'Alice', 'Bob'}
Only in Class B: {'Frank', 'Eve'}
Unique to each: {'Frank', 'Eve', 'Alice', 'Bob'}
```

---

### Exercise 5: Frozenset Practice

**Objective:** Create and use a frozenset.

**Scenario:** A geography quiz app stores the capitals of African countries. Once set, the data should not change.

```python
ng_capitals = frozenset({"Abuja", "Lagos"})  # Abuja is capital; Lagos is largest city
gh_capitals = frozenset({"Accra"})

# Check
print("Abuja" in ng_capitals)
print(type(ng_capitals))

# Attempt to modify — this will fail
try:
    ng_capitals.add("Kano")
except AttributeError as e:
    print(f"Error: {e}")
```

**Expected Output:**
```
True
<class 'frozenset'>
Error: 'frozenset' object has no attribute 'add'
```

---

## Part 14: Mini Project — Unique Word Analyser

### Project Brief

You will build a tool that analyses text and gives statistics about unique words.

**Scenario:** You work at a newspaper. Your editor wants a quick tool that takes a paragraph of text and tells her:
- How many unique words it contains
- Words unique to Paragraph A (not in Paragraph B)
- Words shared between two paragraphs
- All words across both paragraphs

---

### Stage 1: Setup — Split Text into Words

First, let us turn a string into a set of unique lowercase words.

```python
paragraph_a = "the cat sat on the mat and the cat was happy"

# Step 1: Split the string into individual words
words_a = paragraph_a.split()
print("Word list:", words_a)

# Step 2: Convert to a set to get unique words
unique_a = set(words_a)
print("Unique words:", unique_a)
print("Count:", len(unique_a))
```

**Output:**
```
Word list: ['the', 'cat', 'sat', 'on', 'the', 'mat', 'and', 'the', 'cat', 'was', 'happy']
Unique words: {'and', 'on', 'sat', 'mat', 'cat', 'happy', 'was', 'the'}
Count: 8
```

> `.split()` is a string method that splits a sentence into a list of words at each space.

---

### Stage 2: Core Logic — Compare Two Paragraphs

```python
paragraph_a = "the cat sat on the mat and the cat was happy"
paragraph_b = "the dog ran on the grass and the dog was tired"

set_a = set(paragraph_a.split())
set_b = set(paragraph_b.split())

# All unique words across both
all_words = set_a.union(set_b)

# Words in both paragraphs
shared = set_a.intersection(set_b)

# Words only in paragraph A
only_in_a = set_a.difference(set_b)

# Words only in paragraph B
only_in_b = set_b.difference(set_a)
```

---

### Stage 3: Display Results

```python
print("=" * 40)
print("UNIQUE WORD ANALYSIS REPORT")
print("=" * 40)
print(f"\nParagraph A has {len(set_a)} unique words.")
print(f"Paragraph B has {len(set_b)} unique words.")
print(f"\nTotal unique words across both: {len(all_words)}")
print(f"Words shared by both: {shared}")
print(f"Words only in Paragraph A: {only_in_a}")
print(f"Words only in Paragraph B: {only_in_b}")
```

**Expected Output:**
```
========================================
UNIQUE WORD ANALYSIS REPORT
========================================

Paragraph A has 8 unique words.
Paragraph B has 8 unique words.

Total unique words across both: 13
Words shared by both: {'the', 'and', 'was', 'on'}
Words only in Paragraph A: {'sat', 'mat', 'cat', 'happy'}
Words only in Paragraph B: {'dog', 'ran', 'grass', 'tired'}
```

---

### Stage 4: Enhancement — Wrap in a Function

```python
def analyse_texts(text_a, text_b):
    set_a = set(text_a.lower().split())
    set_b = set(text_b.lower().split())

    print("=" * 45)
    print("      UNIQUE WORD ANALYSIS REPORT")
    print("=" * 45)
    print(f"\nText A unique word count : {len(set_a)}")
    print(f"Text B unique word count : {len(set_b)}")
    print(f"\nShared words             : {set_a & set_b}")
    print(f"Only in Text A           : {set_a - set_b}")
    print(f"Only in Text B           : {set_b - set_a}")
    print(f"All unique words combined: {len(set_a | set_b)}")
    print("=" * 45)

# Test it
t1 = "Python is fast and Python is fun"
t2 = "Java is fast and Java is verbose"

analyse_texts(t1, t2)
```

**Expected Output:**
```
=============================================
      UNIQUE WORD ANALYSIS REPORT
=============================================

Text A unique word count : 5
Text B unique word count : 5

Shared words             : {'fast', 'and', 'is'}
Only in Text A           : {'python', 'fun'}
Only in Text B           : {'java', 'verbose'}
All unique words combined: 7
=============================================
```

### Reflection Questions
- What would happen if you passed the same text for both arguments?
- How would you extend this to work with three paragraphs?
- Can you make it case-sensitive? When would you want that?

### Optional Extensions
- Strip punctuation from words before adding to the set
- Count how many sentences each paragraph has
- Save the report to a `.txt` file

---

## Part 15: Common Beginner Mistakes

### Mistake 1: Using `{}` for an Empty Set

```python
# ❌ WRONG — this creates an empty DICTIONARY, not a set!
empty = {}
print(type(empty))   # <class 'dict'>

# ✅ CORRECT — use set() for an empty set
empty = set()
print(type(empty))   # <class 'set'>
```

### Mistake 2: Trying to Access Items by Index

```python
# ❌ WRONG
fruits = {"apple", "banana", "cherry"}
print(fruits[0])   # TypeError!

# ✅ CORRECT — loop through or check membership
for item in fruits:
    print(item)
```

### Mistake 3: Using `.remove()` When Not Sure Item Exists

```python
# ❌ RISKY — raises KeyError if "mango" isn't there
fruits = {"apple", "banana"}
fruits.remove("mango")

# ✅ SAFE — use discard
fruits.discard("mango")   # no error
```

### Mistake 4: Expecting a Fixed Order

```python
# ❌ ASSUMPTION — sets do not guarantee order
items = {"z", "a", "m"}
print(items)   # might print {'m', 'a', 'z'} — order unpredictable

# ✅ If you need order, convert to a sorted list first:
print(sorted(items))   # ['a', 'm', 'z']
```

### Mistake 5: Putting a List Inside a Set

```python
# ❌ WRONG — lists are mutable and cannot be set items
bad_set = {[1, 2], [3, 4]}   # TypeError: unhashable type: 'list'

# ✅ CORRECT — use tuples (immutable) instead
good_set = {(1, 2), (3, 4)}
print(good_set)   # {(1, 2), (3, 4)}
```

### Mistake 6: Confusing `.union()` and `.update()`

```python
set1 = {"a", "b"}
set2 = {"c", "d"}

# union() returns a NEW set — set1 is unchanged
new_set = set1.union(set2)
print(set1)    # {'a', 'b'}  — original unchanged
print(new_set) # {'a', 'b', 'c', 'd'}

# update() MODIFIES set1 in place — no new set is returned
set1.update(set2)
print(set1)    # {'a', 'b', 'c', 'd'}  — original changed!
```

---

## Part 16: Reflection Questions

Take a moment to think through these questions. Try to answer before looking back at the lesson.

1. What are the three key properties of a Python set?
2. You have a list with 10,000 items and many duplicates. How would you instantly remove all duplicates?
3. What is the difference between `.remove()` and `.discard()`?
4. A friend says `{}` creates an empty set. Are they correct? Explain.
5. When would you use a `frozenset` instead of a regular set?
6. You have two sets of customer emails from two different marketing campaigns. How would you find emails that appear in both campaigns?
7. What does `set1.symmetric_difference(set2)` return? Give an example.
8. Can you put a list inside a set? What about a tuple?

---

## Part 17: Completion Checklist

Before moving to the next lesson, tick off each item:

- [ ] I understand what a Python set is and how it differs from a list
- [ ] I can create a set using `{}` and `set()`
- [ ] I know that sets have no duplicates, no fixed order, and no index
- [ ] I can get the length of a set using `len()`
- [ ] I can check if an item is in a set using `in` and `not in`
- [ ] I can loop through a set using a `for` loop
- [ ] I can add one item using `.add()` and multiple items using `.update()`
- [ ] I know the difference between `.remove()` and `.discard()`
- [ ] I can remove all items with `.clear()` and delete a set with `del`
- [ ] I understand `union()`, `intersection()`, `difference()`, and `symmetric_difference()`
- [ ] I know the difference between methods that return a new set and those that modify in place
- [ ] I understand what a frozenset is and when to use it
- [ ] I have completed at least two guided exercises
- [ ] I have completed the mini project

---

## Lesson Summary

Excellent work completing Lesson 13! Here is everything you learned:

**What is a Set?**
A Python set is an unordered collection with no duplicate values and no index. Items cannot be changed directly, but the set can grow or shrink.

**Creating Sets:**
Use `{item1, item2}` or `set(iterable)`. An empty set must be created with `set()` — not `{}`.

**Accessing Items:**
You cannot use `set[0]`. Instead, loop with `for`, or check membership with `in` / `not in`.

**Adding Items:**
`.add(x)` for one item. `.update(iterable)` for many items from any collection.

**Removing Items:**
`.remove(x)` raises an error if not found. `.discard(x)` is silent. `.pop()` removes a random item. `.clear()` empties the set. `del setname` deletes it entirely.

**Joining Sets:**
`.union()` → all items. `.intersection()` → shared items. `.difference()` → items in one but not other. `.symmetric_difference()` → items unique to each set.

**Frozenset:**
An immutable version of a set. Created with `frozenset()`. Cannot be modified. Can be used as a dictionary key or as an item in another set.

**Real-World Uses:**
Removing duplicates, membership testing, finding common or unique elements between datasets, building keyword filters, and tracking unique visitors or events.

---

> **Up next: Lesson 14 — Python Dictionaries.** You will learn how to store key-value pairs, the most powerful Python collection for representing real-world data like records, settings, and lookups.
