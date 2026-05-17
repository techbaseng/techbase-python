---
render_with_liquid: false
title: "Lesson 10: Python Sets — The Collection That Hates Duplicates"
nav_order: 10
---

# Lesson 10: Python Sets — The Collection That Hates Duplicates

---

## Lesson Introduction

Welcome to Lesson 10! In previous lessons, you learned about Python Lists and Tuples — two ways to store collections of things. Now you're going to learn about a third collection type: **Sets**.

Sets are special because they have three powerful rules:

1. **No duplicates allowed** — every item must be unique
2. **Unordered** — items have no position or index
3. **Items cannot be changed** once added (but you can add or remove items)

By the end of this lesson, you will be able to: create sets, access and check their values, add and remove items, loop through them, join multiple sets together, use frozensets, and apply every major set method.

**Real-world analogy:** Think of a set like a bag of unique raffle tickets. You cannot have two tickets with the same number. You can reach in and add a new ticket, or take one out, but the bag doesn't care about the order — it just guarantees every number is unique.

---

## Prerequisite Concepts

Before diving in, make sure you understand these ideas (they will appear throughout this lesson):

**Variables** — a box with a name that holds a value: `name = "Alice"`

**Lists** — an ordered collection: `fruits = ["apple", "banana", "cherry"]`

**Loops** — repeating an action: `for item in collection: print(item)`

**`in` keyword** — checking membership: `"apple" in fruits` returns `True` or `False`

**Functions** — reusable blocks of code: `len(my_set)` counts items

**Methods** — functions that belong to an object: `my_set.add("grape")` adds an item

If any of these feel unfamiliar, take a quick moment to review them before continuing.

---

## Part 1 — What is a Python Set?

### What is it?

A **set** is a built-in Python data type used to store multiple items in a single variable — but only *unique* items, and with *no guaranteed order*.

### Why does it exist?

Sometimes you need a collection where duplicates simply don't matter or shouldn't exist. For example:

- A list of unique student IDs on a system
- The set of countries a user has visited (you only care which ones, not how many times)
- Unique words in a document (for word-frequency analysis)
- Tags assigned to a product in a store

A set gives you automatic duplicate removal and powerful tools for comparing collections.

### How is it different from a List?

| Feature | List | Set |
|---|---|---|
| Ordered? | Yes (has positions 0, 1, 2…) | No (no positions) |
| Allows duplicates? | Yes | No |
| Can access by index? | Yes: `mylist[0]` | No |
| Use case | Ordered data, sequences | Unique collections |

---

### Creating a Set — The Basics

**How to write it:** Use curly brackets `{ }` and separate items with commas.

```python
myset = {"apple", "banana", "cherry"}
print(myset)
```

**Expected output (order may vary):**
```
{'banana', 'cherry', 'apple'}
```

> **Important!** Notice the output order may be different from how you typed it. That is completely normal — sets are unordered. Every time you run the program, the order might change.

---

### The Three Rules of Sets

**Rule 1: Sets are unordered**

Items do not have a fixed position. You cannot say "give me item number 2."

**Rule 2: Set items are unchangeable (but the set itself can grow or shrink)**

Once "apple" is in the set, you cannot go in and edit that specific item. However, you can *remove* "apple" and *add* "mango".

**Rule 3: No duplicates**

```python
thisset = {"apple", "banana", "cherry", "apple"}
print(thisset)
```

**Expected output:**
```
{'banana', 'cherry', 'apple'}
```

Even though "apple" was written twice, the set only keeps one copy. The duplicate is silently ignored.

---

### A Curious Edge Case: True, 1, False, and 0

Python treats `True` and `1` as the same value in sets. Similarly, `False` and `0` are considered identical.

```python
# True and 1 are the same in a set
thisset = {"apple", "banana", "cherry", True, 1, 2}
print(thisset)
```

**Expected output:**
```
{True, 2, 'banana', 'cherry', 'apple'}
```

Only one of `True` or `1` is kept (whichever appeared first).

```python
# False and 0 are the same in a set
thisset = {"apple", "banana", "cherry", False, True, 0}
print(thisset)
```

**Expected output:**
```
{False, True, 'banana', 'cherry', 'apple'}
```

> **Thinking prompt:** Why do you think Python treats `True` and `1` as the same? (Hint: internally in Python, `True` has the numeric value of `1`.)

---

### Getting the Length of a Set

Use the `len()` function to count how many items are in a set.

```python
thisset = {"apple", "banana", "cherry"}
print(len(thisset))
```

**Expected output:**
```
3
```

---

### Sets Can Hold Different Data Types

Items in a set can be strings, integers, booleans — or even a mix:

```python
set1 = {"apple", "banana", "cherry"}   # all strings
set2 = {1, 5, 7, 9, 3}                # all integers
set3 = {True, False, False}            # booleans (False appears once)
set4 = {"abc", 34, True, 40, "male"}   # mixed types
print(set4)
```

**Expected output (order may vary):**
```
{True, 34, 40, 'abc', 'male'}
```

---

### Checking the Type

Python's built-in `type()` function confirms a set is of type `set`:

```python
myset = {"apple", "banana", "cherry"}
print(type(myset))
```

**Expected output:**
```
<class 'set'>
```

---

### The `set()` Constructor

You can also create a set using the `set()` function (called a **constructor**). Notice the double round brackets — you are passing a tuple (or list) inside:

```python
# Method 1: curly braces
myset1 = {"apple", "banana", "cherry"}

# Method 2: set() constructor
myset2 = set(("apple", "banana", "cherry"))   # note the double brackets
print(myset2)
```

**Expected output:**
```
{'cherry', 'banana', 'apple'}
```

Both methods give you the same result. The constructor method is useful when you want to convert a list into a set:

```python
my_list = ["apple", "banana", "apple", "cherry", "banana"]
unique_items = set(my_list)   # removes duplicates automatically
print(unique_items)
```

**Expected output:**
```
{'cherry', 'banana', 'apple'}
```

This is one of the most practical uses of sets in real-world Python code!

---

### The Four Python Collection Types — A Quick Comparison

Python has four built-in collection types. Here is how they compare:

| Collection | Ordered? | Changeable? | Duplicates? | Example |
|---|---|---|---|---|
| **List** | Yes | Yes | Yes | `[1, 2, 2, 3]` |
| **Tuple** | Yes | No | Yes | `(1, 2, 2, 3)` |
| **Set** | No | Items no, set yes | No | `{1, 2, 3}` |
| **Dictionary** | Yes (Python 3.7+) | Yes | No (keys) | `{"a": 1}` |

---

## Part 2 — Accessing Set Items

### Why You Cannot Use an Index

In a list, you access items by their position number (called an index): `fruits[0]` gives you the first fruit.

Sets have **no positions**, so `myset[0]` will cause an error.

```python
thisset = {"apple", "banana", "cherry"}
# This will cause an error:
# print(thisset[0])   # TypeError: 'set' object is not subscriptable
```

### How DO You Access Items Then?

You have two main options:

**Option 1: Loop through the set**

```python
thisset = {"apple", "banana", "cherry"}

for x in thisset:
    print(x)
```

**Expected output (order may vary each run):**
```
banana
cherry
apple
```

Each time the loop runs, `x` holds one item from the set. Since sets are unordered, the print order is not guaranteed.

---

**Option 2: Check if an item is present using `in`**

```python
thisset = {"apple", "banana", "cherry"}
print("banana" in thisset)
```

**Expected output:**
```
True
```

```python
thisset = {"apple", "banana", "cherry"}
print("mango" in thisset)
```

**Expected output:**
```
False
```

---

**Option 3: Check if an item is NOT present using `not in`**

```python
thisset = {"apple", "banana", "cherry"}
print("banana" not in thisset)
```

**Expected output:**
```
False
```

(Because banana IS in the set, `not in` returns `False`.)

```python
thisset = {"apple", "banana", "cherry"}
print("mango" not in thisset)
```

**Expected output:**
```
True
```

---

> **Key reminder:** Once a set is created, you **cannot change** individual items directly. You cannot do `thisset[0] = "grape"`. What you CAN do is remove an item and add a new one, which we cover next.

---

## Part 3 — Adding Items to a Set

### Adding a Single Item: `add()`

The `add()` method places one new item into the set.

```python
thisset = {"apple", "banana", "cherry"}
thisset.add("orange")
print(thisset)
```

**Expected output (order may vary):**
```
{'apple', 'orange', 'banana', 'cherry'}
```

**Line-by-line explanation:**
- `thisset = {"apple", "banana", "cherry"}` — creates a set with 3 fruits
- `thisset.add("orange")` — adds "orange" to the set. The `.add()` is a method called on the set
- `print(thisset)` — shows the updated set

> **What if you add a duplicate?** Nothing bad happens — it is simply ignored:
>
> ```python
> thisset = {"apple", "banana", "cherry"}
> thisset.add("banana")   # banana already exists
> print(thisset)          # set is unchanged
> ```
> **Output:** `{'apple', 'banana', 'cherry'}`

---

### Adding Items from Another Set: `update()`

The `update()` method lets you add all items from *another set* into your set.

```python
thisset = {"apple", "banana", "cherry"}
tropical = {"pineapple", "mango", "papaya"}

thisset.update(tropical)
print(thisset)
```

**Expected output (order may vary):**
```
{'apple', 'mango', 'cherry', 'pineapple', 'banana', 'papaya'}
```

**Explanation:**
- `tropical` is a second set
- `thisset.update(tropical)` merges all items from `tropical` into `thisset`
- The original `thisset` is modified in place (changed directly)
- Duplicates would still be ignored

---

### Adding Items from ANY Iterable: `update()` with a List

`update()` is flexible — it doesn't require another set. You can pass a **list**, **tuple**, or **dictionary**.

```python
thisset = {"apple", "banana", "cherry"}
mylist = ["kiwi", "orange"]

thisset.update(mylist)
print(thisset)
```

**Expected output (order may vary):**
```
{'apple', 'orange', 'banana', 'cherry', 'kiwi'}
```

**Real-world scenario:** Imagine you have a set of registered usernames, and a new batch of users just signed up (stored in a list). You can merge them all into your existing set with one `update()` call.

---

### Summary: Adding Items

| Task | Method | Modifies original? |
|---|---|---|
| Add one item | `set.add("item")` | Yes |
| Add items from another set | `set.update(another_set)` | Yes |
| Add items from a list | `set.update(my_list)` | Yes |
| Add items from a tuple | `set.update(my_tuple)` | Yes |

---

## Part 4 — Removing Items from a Set

Python gives you several ways to remove items, each with slightly different behaviour.

### Method 1: `remove()` — Remove a Specific Item

```python
thisset = {"apple", "banana", "cherry"}
thisset.remove("banana")
print(thisset)
```

**Expected output:**
```
{'apple', 'cherry'}
```

> **WARNING:** If the item you try to remove does NOT exist, `remove()` will raise a `KeyError`:
>
> ```python
> thisset = {"apple", "banana", "cherry"}
> thisset.remove("mango")   # mango doesn't exist — ERROR!
> # KeyError: 'mango'
> ```

---

### Method 2: `discard()` — Remove Safely (No Error)

`discard()` works exactly like `remove()` but will NOT raise an error if the item doesn't exist. It simply does nothing.

```python
thisset = {"apple", "banana", "cherry"}
thisset.discard("banana")
print(thisset)
```

**Expected output:**
```
{'apple', 'cherry'}
```

```python
thisset = {"apple", "banana", "cherry"}
thisset.discard("mango")   # mango doesn't exist — but NO error
print(thisset)             # set unchanged
```

**Expected output:**
```
{'apple', 'banana', 'cherry'}
```

> **Tip:** Use `discard()` when you are not sure if the item exists and you don't want your program to crash. Use `remove()` when the item must exist and you want to be alerted if something goes wrong.

---

### Method 3: `pop()` — Remove a Random Item

Since sets are unordered, you cannot choose which item to remove by position. `pop()` removes and **returns** a random item.

```python
thisset = {"apple", "banana", "cherry"}
x = thisset.pop()    # removes a random item
print(x)             # prints the removed item
print(thisset)       # prints the remaining set
```

**Expected output (yours may differ since it's random):**
```
apple
{'banana', 'cherry'}
```

> **Note:** Because `pop()` removes a random item, you can never predict which item gets removed. This is rarely used when you need predictable behaviour.

---

### Method 4: `clear()` — Empty the Entire Set

`clear()` removes ALL items from the set, leaving an empty set behind.

```python
thisset = {"apple", "banana", "cherry"}
thisset.clear()
print(thisset)
```

**Expected output:**
```
set()
```

> **What is `set()`?** An empty set is displayed as `set()` — not `{}` because `{}` in Python means an empty *dictionary*, not an empty set.

---

### Method 5: `del` — Delete the Set Entirely

`del` removes the entire set variable from memory.

```python
thisset = {"apple", "banana", "cherry"}
del thisset
print(thisset)   # This line will cause an error!
```

**Expected output:**
```
NameError: name 'thisset' is not defined
```

The set no longer exists. Trying to print it results in an error.

---

### Summary: Removing Items

| Method | Behaviour | Raises error if item missing? |
|---|---|---|
| `remove("item")` | Removes specified item | Yes — KeyError |
| `discard("item")` | Removes specified item | No — silent |
| `pop()` | Removes a random item | No (but fails if set empty) |
| `clear()` | Removes all items, keeps set | N/A |
| `del setname` | Deletes the set variable | N/A |

---

## Part 5 — Looping Through a Set

### The `for` Loop with Sets

You can go through every item in a set using a `for` loop, exactly like with lists:

```python
thisset = {"apple", "banana", "cherry"}

for x in thisset:
    print(x)
```

**Expected output (order may vary):**
```
cherry
banana
apple
```

**Line-by-line explanation:**
- `for x in thisset:` — starts a loop. Each time through, `x` takes on the value of one item from the set
- `print(x)` — prints the current item
- The loop runs once for every unique item in the set

### Practical Example: Looping and Checking

```python
fruits = {"apple", "banana", "cherry", "mango"}

for fruit in fruits:
    if "a" in fruit:
        print(fruit, "contains the letter 'a'")
```

**Expected output (order may vary):**
```
banana contains the letter 'a'
apple contains the letter 'a'
mango contains the letter 'a'
```

---

> **Thinking prompt:** If you run the loop example above twice, would the output be in the same order? Why or why not?

---

## Part 6 — Joining Sets

This is where sets become incredibly powerful. Python offers many ways to combine sets, and each method does something different.

### Method 1: `union()` — Combine Everything

`union()` returns a **new set** containing all items from both sets. Duplicates across sets are automatically removed.

```python
set1 = {"a", "b", "c"}
set2 = {1, 2, 3}

set3 = set1.union(set2)
print(set3)
```

**Expected output (order may vary):**
```
{'a', 1, 2, 'b', 3, 'c'}
```

You can also use the `|` operator as a shortcut:

```python
set3 = set1 | set2
print(set3)
```

**Same output.**

#### Joining More Than Two Sets

```python
set1 = {"a", "b", "c"}
set2 = {1, 2, 3}
set3 = {"John", "Elena"}
set4 = {"apple", "bananas", "cherry"}

myset = set1.union(set2, set3, set4)
print(myset)
```

Or with `|`:
```python
myset = set1 | set2 | set3 | set4
```

#### Joining a Set and a Tuple

`union()` can combine sets with other data types (lists, tuples):

```python
x = {"a", "b", "c"}
y = (1, 2, 3)

z = x.union(y)
print(z)
```

**Expected output:**
```
{1, 2, 3, 'a', 'b', 'c'}
```

> **Note:** The `|` operator only works set-to-set. `union()` is more flexible.

---

### Method 2: `update()` — Merge In Place

`update()` inserts all items from one set into another, **changing the original set**.

```python
set1 = {"a", "b", "c"}
set2 = {1, 2, 3}

set1.update(set2)
print(set1)
```

**Expected output:**
```
{'a', 1, 2, 'b', 3, 'c'}
```

Unlike `union()` which creates a **new** set, `update()` modifies `set1` directly.

---

### Method 3: `intersection()` — Keep Only Shared Items

`intersection()` returns a new set containing **only** items that exist in **both** sets.

Think of it as: *"What do these two sets have in common?"*

```python
set1 = {"apple", "banana", "cherry"}
set2 = {"google", "microsoft", "apple"}

set3 = set1.intersection(set2)
print(set3)
```

**Expected output:**
```
{'apple'}
```

Only "apple" is in both sets, so that's the only item returned.

Shortcut using `&`:
```python
set3 = set1 & set2
print(set3)
```

**Same output.**

#### `intersection_update()` — Modify in Place

```python
set1 = {"apple", "banana", "cherry"}
set2 = {"google", "microsoft", "apple"}

set1.intersection_update(set2)
print(set1)
```

**Expected output:**
```
{'apple'}
```

#### True/False Edge Case in Intersection

```python
set1 = {"apple", 1, "banana", 0, "cherry"}
set2 = {False, "google", 1, "apple", 2, True}

set3 = set1.intersection(set2)
print(set3)
```

**Expected output:**
```
{False, 1, 'apple'}
```

`1` and `True` are treated as the same value; `0` and `False` are treated the same.

---

### Method 4: `difference()` — Items in First, NOT in Second

`difference()` returns items from the **first set** that are **not** in the second set.

```python
set1 = {"apple", "banana", "cherry"}
set2 = {"google", "microsoft", "apple"}

set3 = set1.difference(set2)
print(set3)
```

**Expected output:**
```
{'banana', 'cherry'}
```

"apple" exists in both sets, so it is excluded. "banana" and "cherry" are only in `set1`, so they survive.

Shortcut using `-`:
```python
set3 = set1 - set2
```

#### `difference_update()` — Modify in Place

```python
set1 = {"apple", "banana", "cherry"}
set2 = {"google", "microsoft", "apple"}

set1.difference_update(set2)
print(set1)
```

**Expected output:**
```
{'banana', 'cherry'}
```

---

### Method 5: `symmetric_difference()` — Everything EXCEPT Shared Items

`symmetric_difference()` keeps all items from both sets **except** the ones they share.

Think of it as: *"Give me everything unique to each set, but nothing in common."*

```python
set1 = {"apple", "banana", "cherry"}
set2 = {"google", "microsoft", "apple"}

set3 = set1.symmetric_difference(set2)
print(set3)
```

**Expected output:**
```
{'banana', 'cherry', 'google', 'microsoft'}
```

"apple" is in both, so it is excluded. Everything else is kept.

Shortcut using `^`:
```python
set3 = set1 ^ set2
```

#### `symmetric_difference_update()` — Modify in Place

```python
set1 = {"apple", "banana", "cherry"}
set2 = {"google", "microsoft", "apple"}

set1.symmetric_difference_update(set2)
print(set1)
```

**Expected output:**
```
{'banana', 'cherry', 'google', 'microsoft'}
```

---

### Joining Methods — Big Picture Summary

| Method | What it keeps | New set? | Shortcut |
|---|---|---|---|
| `union()` | All items from both | Yes | `\|` |
| `update()` | All items from both | No (modifies original) | — |
| `intersection()` | Only shared items | Yes | `&` |
| `intersection_update()` | Only shared items | No | — |
| `difference()` | Items in set1 NOT in set2 | Yes | `-` |
| `difference_update()` | Items in set1 NOT in set2 | No | — |
| `symmetric_difference()` | Everything EXCEPT shared | Yes | `^` |
| `symmetric_difference_update()` | Everything EXCEPT shared | No | — |

---

## Part 7 — Frozenset: The Immutable Set

### What is a Frozenset?

A **frozenset** is like a set, but completely frozen — you cannot add or remove any items at all after it is created. It is permanently sealed.

Regular set vs frozenset:
- Regular set: unique, unordered. You can add/remove items.
- Frozenset: unique, unordered. You CANNOT add/remove items.

### Why Would You Use a Frozenset?

- When you need a set that should never be modified (protecting data integrity)
- When you need to use a set as a **dictionary key** (normal sets cannot be dictionary keys because they are mutable, but frozensets can)
- When working in multi-threaded programs where data should be safely read-only

### Creating a Frozenset

Use the `frozenset()` constructor:

```python
x = frozenset({"apple", "banana", "cherry"})
print(x)
print(type(x))
```

**Expected output:**
```
frozenset({'cherry', 'banana', 'apple'})
<class 'frozenset'>
```

### Frozenset vs Regular Set

```python
# Regular set — can add items
myset = {"apple", "banana"}
myset.add("cherry")    # Works fine
print(myset)

# Frozenset — cannot add items
myfs = frozenset({"apple", "banana"})
# myfs.add("cherry")   # Would raise: AttributeError: 'frozenset' object has no attribute 'add'
```

### What Can You Do with a Frozenset?

Even though you cannot modify it, you can still use all **non-modifying** set methods:

| Method | Shortcut | What it does |
|---|---|---|
| `copy()` | — | Returns a copy of the frozenset |
| `difference()` | `-` | Returns items in this frozenset not in another |
| `intersection()` | `&` | Returns items present in both |
| `isdisjoint()` | — | Returns True if the two sets share nothing |
| `issubset()` | `<=` or `<` | Returns True if this is a subset of another |
| `issuperset()` | `>=` or `>` | Returns True if this is a superset of another |
| `symmetric_difference()` | `^` | Returns all items not shared by both |
| `union()` | `\|` | Returns all items from both |

```python
fs1 = frozenset({"apple", "banana", "cherry"})
fs2 = frozenset({"banana", "mango"})

# Intersection of two frozensets
result = fs1.intersection(fs2)
print(result)
```

**Expected output:**
```
frozenset({'banana'})
```

---

## Part 8 — All Set Methods Reference

Python sets come with a rich set of built-in methods. Here is the complete list, with plain-English descriptions:

| Method | Description |
|---|---|
| `add()` | Adds one element to the set |
| `clear()` | Removes all elements from the set |
| `copy()` | Returns a copy of the set |
| `difference()` | Returns elements in this set but not in another |
| `difference_update()` | Removes elements found in another set from this set |
| `discard()` | Removes the specified element (no error if missing) |
| `intersection()` | Returns elements present in all specified sets |
| `intersection_update()` | Keeps only elements found in all specified sets |
| `isdisjoint()` | Returns True if the two sets share no elements |
| `issubset()` | Returns True if every element of this set is in another |
| `issuperset()` | Returns True if this set contains every element of another |
| `pop()` | Removes and returns a random element |
| `remove()` | Removes a specified element (raises error if missing) |
| `symmetric_difference()` | Returns elements in either set, but not in both |
| `symmetric_difference_update()` | Updates the set with symmetric difference |
| `union()` | Returns a set containing all elements from all sets |
| `update()` | Adds all elements of another set (or iterable) |

---

### Quick Examples for Key Methods

**`issubset()` — Is this set entirely inside another?**

```python
set1 = {"a", "b"}
set2 = {"a", "b", "c", "d"}

print(set1.issubset(set2))   # True — all of set1 is inside set2
print(set2.issubset(set1))   # False — set2 has more than set1
```

**Expected output:**
```
True
False
```

**`issuperset()` — Does this set contain all of another?**

```python
print(set2.issuperset(set1))   # True — set2 contains everything in set1
print(set1.issuperset(set2))   # False
```

**Expected output:**
```
True
False
```

**`isdisjoint()` — Do the sets share nothing?**

```python
setA = {"apple", "banana"}
setB = {"cherry", "mango"}
setC = {"banana", "kiwi"}

print(setA.isdisjoint(setB))   # True — nothing shared
print(setA.isdisjoint(setC))   # False — "banana" is shared
```

**Expected output:**
```
True
False
```

---

## Part 9 — Guided Practice Exercises

### Exercise 1: Build a Unique Visitors Set

**Objective:** Practice creating sets and removing duplicates.

**Scenario:** A website tracking visitors recorded these names (some repeated): `["Alice", "Bob", "Charlie", "Alice", "Dave", "Bob", "Eve"]`

**Task:** Convert this list to a set to get only unique visitors, then print the count.

**Steps:**
1. Store the list in a variable called `visitor_log`
2. Convert it to a set called `unique_visitors`
3. Print `unique_visitors`
4. Print the number of unique visitors using `len()`

**Hints:**
- `set(a_list)` converts a list to a set
- `len(a_set)` counts items

**Solution:**

```python
visitor_log = ["Alice", "Bob", "Charlie", "Alice", "Dave", "Bob", "Eve"]
unique_visitors = set(visitor_log)
print(unique_visitors)
print("Total unique visitors:", len(unique_visitors))
```

**Expected output (order may vary):**
```
{'Charlie', 'Alice', 'Bob', 'Dave', 'Eve'}
Total unique visitors: 5
```

**Self-check:** Did you get 5 unique visitors? Correct! The duplicates ("Alice" and "Bob") were removed.

---

### Exercise 2: Membership Checking in a Set

**Objective:** Practice using `in` and `not in`.

**Scenario:** A school has a set of students who passed an exam.

**Task:**
1. Create a set called `passed` with these names: "Alice", "Bob", "Diana", "Frank"
2. Check if "Bob" passed (print True/False)
3. Check if "Charlie" passed (print True/False)
4. Print a message: "Diana passed!" only if Diana is in the set

```python
passed = {"Alice", "Bob", "Diana", "Frank"}

print("Bob passed:", "Bob" in passed)
print("Charlie passed:", "Charlie" in passed)

if "Diana" in passed:
    print("Diana passed!")
```

**Expected output:**
```
Bob passed: True
Charlie passed: False
Diana passed!
```

---

### Exercise 3: Track Product Tags

**Objective:** Practice `add()`, `discard()`, and looping.

**Scenario:** An e-commerce store has a set of product tags for a shirt.

**Task:**
1. Start with `tags = {"cotton", "casual", "summer"}`
2. Add the tag "blue"
3. Remove the tag "summer" using `discard()`
4. Loop through all tags and print each one

```python
tags = {"cotton", "casual", "summer"}
tags.add("blue")
tags.discard("summer")

print("Current tags:")
for tag in tags:
    print("-", tag)
```

**Expected output (order may vary):**
```
Current tags:
- blue
- cotton
- casual
```

---

### Exercise 4: Finding Common Courses

**Objective:** Practice `intersection()`.

**Scenario:** Two students each enrolled in different courses. Find out which courses they both take.

```python
alice_courses = {"Math", "Physics", "Chemistry", "English"}
bob_courses = {"Biology", "Math", "English", "Art"}

common = alice_courses.intersection(bob_courses)
print("Courses both Alice and Bob take:", common)
```

**Expected output:**
```
Courses both Alice and Bob take: {'Math', 'English'}
```

**What-if challenge:** What if you also want to know which courses ONLY Alice takes (not Bob)? Use `difference()`.

```python
only_alice = alice_courses.difference(bob_courses)
print("Courses only Alice takes:", only_alice)
```

**Expected output:**
```
Courses only Alice takes: {'Chemistry', 'Physics'}
```

---

### Exercise 5: Merging Teams

**Objective:** Practice `union()` and `update()`.

**Scenario:** Two departments need to merge their employee sets.

```python
dept_a = {"Alice", "Bob", "Charlie"}
dept_b = {"Diana", "Eve", "Bob"}

# Option 1: Create a new combined set
combined = dept_a.union(dept_b)
print("Combined team:", combined)

# Option 2: Merge dept_b into dept_a directly
dept_a.update(dept_b)
print("Updated dept_a:", dept_a)
```

**Expected output (order may vary):**
```
Combined team: {'Charlie', 'Alice', 'Bob', 'Diana', 'Eve'}
Updated dept_a: {'Charlie', 'Alice', 'Bob', 'Diana', 'Eve'}
```

---

## Part 10 — Mini Project: Student Eligibility Checker

### Project Description

You are building a simple eligibility checker for a school event. The school has sets of students in different categories, and you need to answer several questions using set operations.

### Setup

```python
# All enrolled students
enrolled = {"Alice", "Bob", "Charlie", "Diana", "Eve", "Frank", "Grace"}

# Students who paid their event fee
paid = {"Alice", "Charlie", "Eve", "Grace", "Henry"}   # Note: Henry not enrolled!

# Students with discipline issues (excluded from event)
excluded = {"Bob", "Frank"}
```

---

### Stage 1: Find Eligible Students

Eligible = enrolled AND paid AND NOT excluded.

```python
# Step 1: Find students who are both enrolled and paid
enrolled_and_paid = enrolled.intersection(paid)
print("Enrolled and paid:", enrolled_and_paid)

# Step 2: Remove excluded students
eligible = enrolled_and_paid.difference(excluded)
print("Eligible for event:", eligible)
```

**Expected output:**
```
Enrolled and paid: {'Charlie', 'Alice', 'Grace', 'Eve'}
Eligible for event: {'Charlie', 'Alice', 'Grace', 'Eve'}
```

(None of the excluded students were in `enrolled_and_paid`, so the result is the same.)

---

### Stage 2: Find Problem Cases

```python
# Who paid but is not enrolled? (Data entry error!)
paid_not_enrolled = paid.difference(enrolled)
print("Paid but not enrolled (error!):", paid_not_enrolled)

# Who is enrolled but hasn't paid?
enrolled_not_paid = enrolled.difference(paid)
print("Enrolled but not paid:", enrolled_not_paid)
```

**Expected output:**
```
Paid but not enrolled (error!): {'Henry'}
Enrolled but not paid: {'Bob', 'Diana', 'Frank'}
```

---

### Stage 3: Generate Final Report

```python
print("\n--- EVENT ELIGIBILITY REPORT ---")
print(f"Total enrolled students: {len(enrolled)}")
print(f"Total who paid: {len(paid)}")
print(f"Eligible to attend: {len(eligible)} students")
print(f"Students eligible: {eligible}")
print(f"Cannot attend (excluded): {excluded.intersection(enrolled)}")
print(f"Need to pay: {enrolled_not_paid}")
print(f"Data error (paid but not enrolled): {paid_not_enrolled}")
```

**Expected output:**
```
--- EVENT ELIGIBILITY REPORT ---
Total enrolled students: 7
Total who paid: 5
Eligible to attend: 4 students
Students eligible: {'Charlie', 'Alice', 'Grace', 'Eve'}
Cannot attend (excluded): {'Bob', 'Frank'}
Need to pay: {'Bob', 'Diana', 'Frank'}
Data error (paid but not enrolled): {'Henry'}
```

---

### Reflection Questions

1. Why is a set a better choice than a list for this project?
2. What happens if you try to add "Alice" to the `enrolled` set again?
3. How would you use `symmetric_difference()` to find students in exactly one of the two sets (enrolled or paid, but not both)?
4. What would a `frozenset` be useful for in this project?

**Optional extension:** Add a fourth set — `awarded_scholarship = {"Alice", "Diana"}` — and find all students eligible AND on scholarship.

---

## Part 11 — Common Beginner Mistakes

### Mistake 1: Trying to Access a Set Item by Index

```python
# WRONG
myset = {"apple", "banana", "cherry"}
print(myset[0])   # TypeError: 'set' object is not subscriptable

# CORRECT — Loop through it
for item in myset:
    print(item)
```

### Mistake 2: Expecting a Specific Order from a Set

```python
# DANGEROUS assumption
myset = {"apple", "banana", "cherry"}
for item in myset:
    print(item)
# Do NOT assume the output will always be apple → banana → cherry
# It could be any order, and could change between runs
```

If you need ordered output from a set, convert it to a sorted list first:

```python
myset = {"apple", "banana", "cherry"}
for item in sorted(myset):
    print(item)
# Now alphabetically sorted: apple, banana, cherry
```

### Mistake 3: Using `remove()` When the Item Might Not Exist

```python
# WRONG — will crash if "mango" isn't there
myset.remove("mango")

# CORRECT — use discard() to be safe
myset.discard("mango")   # No error, even if "mango" isn't there
```

### Mistake 4: Confusing an Empty Set with an Empty Dictionary

```python
# This is an empty DICTIONARY, not a set!
empty_dict = {}
print(type(empty_dict))   # <class 'dict'>

# This is an empty SET (use the constructor)
empty_set = set()
print(type(empty_set))   # <class 'set'>
```

### Mistake 5: Expecting `update()` to Return a New Set

```python
set1 = {"a", "b"}
set2 = {"c", "d"}

# WRONG — update() returns None, not a new set
result = set1.update(set2)
print(result)   # None!

# CORRECT — use union() for a new set, OR just use update() and access set1
set1.update(set2)
print(set1)   # {'a', 'b', 'c', 'd'}

# OR for a new set:
result = set1.union(set2)
print(result)   # new combined set
```

### Mistake 6: Storing a Mutable Item in a Set

Sets can only contain items that are **immutable** (unchangeable). So you cannot store a list inside a set:

```python
# WRONG — lists cannot go into sets
bad_set = {[1, 2, 3], "hello"}   # TypeError: unhashable type: 'list'

# CORRECT — use tuples (which are immutable) instead of lists
good_set = {(1, 2, 3), "hello"}  # Works fine!
```

---

## Part 12 — Reflection Questions

Think about these questions to reinforce what you learned:

1. What are the three defining properties of a Python set?
2. You have a list with 1000 items, many repeated. How would you get a count of unique items only?
3. When would you choose `discard()` over `remove()`?
4. What is the difference between `union()` and `update()`?
5. What is the difference between `intersection()` and `difference()`?
6. You need a set that you can use as a dictionary key. What type should you use instead of a regular set?
7. If you have sets `A = {1, 2, 3}` and `B = {3, 4, 5}`, what does `A ^ B` give you?
8. Why does `{}` not create an empty set in Python?

---

## Completion Checklist

Go through this list. If you can confidently answer "yes" to each item, you have mastered Lesson 10!

- [ ] I can create a set using `{}` and using `set()`
- [ ] I understand that sets are unordered, have no duplicates, and items cannot be changed directly
- [ ] I know that `True`/`1` and `False`/`0` are treated as duplicates in sets
- [ ] I can use `in` and `not in` to check membership
- [ ] I can loop through a set with a `for` loop
- [ ] I can add items using `add()` and `update()`
- [ ] I know the difference between `remove()` (raises error) and `discard()` (no error)
- [ ] I can use `pop()`, `clear()`, and `del` to remove items
- [ ] I can join sets using `union()`, `update()`, `intersection()`, `difference()`, and `symmetric_difference()`
- [ ] I can use the shortcut operators: `|`, `&`, `-`, `^`
- [ ] I understand what a `frozenset` is and when to use it
- [ ] I know all major set methods and what they do
- [ ] I completed the mini-project successfully

---

## Lesson Summary

Here is everything you learned in this lesson at a glance:

**What a Set Is:** An unordered, duplicate-free collection of unique items. Written with `{}` or created with `set()`.

**Three Core Properties:**
- Unordered: no indexes, no guaranteed order
- No duplicates: same value appears only once
- Items unchangeable: you can add/remove, but not edit existing items

**Accessing Items:** Use `in`/`not in` to check membership, or `for` loops to visit each item.

**Adding Items:**
- `add("item")` — adds one item
- `update(other)` — adds items from another set or iterable

**Removing Items:**
- `remove("item")` — raises error if missing
- `discard("item")` — safe, no error
- `pop()` — removes random item
- `clear()` — empties the set
- `del setname` — deletes the variable

**Joining Sets:**
- `union()` / `|` — everything from both
- `update()` — merge into original
- `intersection()` / `&` — only shared items
- `difference()` / `-` — items in first, not second
- `symmetric_difference()` / `^` — everything except shared

**Frozenset:** An immutable set — cannot add or remove items. Created with `frozenset()`. Useful as dictionary keys or for read-only data.

**Real-World Uses:** Removing duplicates from data, checking membership, finding common or unique elements between datasets, set theory operations in data analysis and machine learning.

---

*Lesson 10 complete. You are now ready for Lesson 11: Python Dictionaries.*
