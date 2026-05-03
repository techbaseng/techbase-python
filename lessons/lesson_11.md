---
render_with_liquid: false
title: "Lesson 11 – Python Lists"
nav_order: 11
---

# Lesson 11 – Python Lists

---

## Lesson Introduction

Imagine you are a teacher and you need to keep track of all your students' names. You could create a separate variable for each student:

```python
student1 = "Amara"
student2 = "Tunde"
student3 = "Ngozi"
student4 = "Emeka"
```

That works for four students — but what if you have 40? Or 400? Creating hundreds of separate variables would be exhausting and unmanageable.

This is exactly the problem that **lists** solve.

A **list** lets you store many items together inside a single variable:

```python
students = ["Amara", "Tunde", "Ngozi", "Emeka"]
```

One variable. Many items. Organised. Easy to work with.

Lists are one of the most important and most-used data structures in all of Python. You will use them constantly — for storing search results, managing user data, processing records, building menus, tracking scores, and hundreds of other everyday tasks.

By the end of this lesson, you will be able to:
- Create lists and understand their properties
- Access individual items (including backwards from the end)
- Access ranges of items using slicing
- Change, add, and remove items
- Loop through lists in several different ways
- Use list comprehension to build new lists elegantly
- Sort lists in ascending and descending order
- Copy lists correctly
- Join (concatenate) two lists together
- Use all the important built-in list methods

---

## Prerequisite Concepts

### Variables

A variable stores a value:
```python
x = 10
name = "Alice"
```

### Strings

A string is text wrapped in quotes:
```python
greeting = "Hello, world!"
```

### `print()` Function

Displays output on screen:
```python
print("Python is fun")   # Output: Python is fun
```

### `for` Loop (brief preview)

A `for` loop repeats an action for each item in a collection. We will use it heavily with lists:
```python
for item in collection:
    print(item)
```

You do not need to fully know loops yet — each example will be explained line by line.

---

## Part 1 – What Is a List?

### The Definition

A **list** is an ordered, changeable collection of items, written with square brackets `[ ]`, with items separated by commas.

```python
my_list = ["apple", "banana", "cherry"]
```

### The Four Key Properties of Lists

| Property    | Meaning                                                        |
|-------------|----------------------------------------------------------------|
| Ordered     | Items always stay in the position you placed them             |
| Changeable  | You can add, remove, or update items after creation           |
| Allows Duplicates | The same value can appear more than once               |
| Indexed     | Every item has a numbered position, starting at 0             |

### Example 1 – Creating and printing a list

```python
fruits = ["apple", "banana", "cherry"]
print(fruits)
```

**Expected Output:**
```
['apple', 'banana', 'cherry']
```

Python prints the entire list including the square brackets and quotes.

### Example 2 – Lists can hold mixed data types

Lists are flexible — they can hold strings, numbers, booleans, or any mixture:

```python
mixed = ["Alice", 25, True, 3.14]
print(mixed)
```

**Expected Output:**
```
['Alice', 25, True, 3.14]
```

### Example 3 – A list can even contain another list

```python
nested = ["fruits", ["apple", "banana"], 42]
print(nested)
```

**Expected Output:**
```
['fruits', ['apple', 'banana'], 42]
```

### The `len()` Function — How Many Items?

`len()` counts the number of items in a list:

```python
fruits = ["apple", "banana", "cherry"]
print(len(fruits))
```

**Expected Output:**
```
3
```

### Lists Allow Duplicate Values

```python
colours = ["red", "blue", "red", "green", "blue"]
print(colours)
print(len(colours))
```

**Expected Output:**
```
['red', 'blue', 'red', 'green', 'blue']
5
```

Even though "red" and "blue" appear twice, they are counted as separate items.

### The `list()` Constructor

You can also create a list using the `list()` constructor function:

```python
thislist = list(("apple", "banana", "cherry"))
print(thislist)
```

> ⚠️ Notice the **double parentheses** — the outer ones belong to `list()`, and the inner ones create a tuple that gets converted.

**Expected Output:**
```
['apple', 'banana', 'cherry']
```

---

## Part 2 – Accessing List Items

### Understanding Index Numbers

Every item in a list has a **position number** called an **index**. Python starts counting from **0**, not 1.

```
List:   ["apple", "banana", "cherry"]
Index:       0        1         2
```

Think of it like floors in a building where the ground floor is floor 0.

### Accessing by Index

Use square brackets with the index number after the list name:

```python
fruits = ["apple", "banana", "cherry"]
print(fruits[0])   # first item
print(fruits[1])   # second item
print(fruits[2])   # third item
```

**Expected Output:**
```
apple
banana
cherry
```

**Line-by-line:**
- `fruits[0]` → goes to position 0 → finds `"apple"` → prints it
- `fruits[1]` → goes to position 1 → finds `"banana"` → prints it
- `fruits[2]` → goes to position 2 → finds `"cherry"` → prints it

> 🤔 **Thinking prompt:** What happens if you try `fruits[3]`? There is no position 3 — Python will raise an `IndexError: list index out of range`.

### Negative Indexing — Counting From the End

Python also supports negative indexes, which count backwards from the end of the list. `-1` means the last item, `-2` means the second-to-last, and so on.

```
List:   ["apple", "banana", "cherry"]
Neg:       -3       -2        -1
```

```python
fruits = ["apple", "banana", "cherry"]
print(fruits[-1])   # last item
print(fruits[-2])   # second to last
print(fruits[-3])   # third to last (= first)
```

**Expected Output:**
```
cherry
banana
apple
```

> 💡 **Why is this useful?** If you have a list of 1000 items and you want the last one, you don't need to count — just use `[-1]`.

### Range of Indexes — Slicing

You can extract a **slice** (a portion) of a list by specifying a start index and an end index, separated by a colon:

```python
list[start : end]
```

> ⚠️ **Critical rule:** The slice includes the start index but **excludes** the end index. `[1:4]` means positions 1, 2, and 3 — NOT position 4.

```python
fruits = ["apple", "banana", "cherry", "orange", "kiwi", "melon", "mango"]
print(fruits[2:5])
```

**Expected Output:**
```
['cherry', 'orange', 'kiwi']
```

Positions 2, 3, and 4 are included. Position 5 is not.

### Slicing From the Beginning

Leave out the start index to slice from the very beginning:

```python
print(fruits[:4])
```

**Expected Output:**
```
['apple', 'banana', 'cherry', 'orange']
```

### Slicing to the End

Leave out the end index to slice all the way to the last item:

```python
print(fruits[2:])
```

**Expected Output:**
```
['cherry', 'orange', 'kiwi', 'melon', 'mango']
```

### Negative Index Slicing

```python
print(fruits[-4:-1])
```

This means: start at the 4th item from the end, stop before the 1st item from the end.

**Expected Output:**
```
['orange', 'kiwi', 'melon']
```

### Checking if an Item Exists — `in` Keyword

Use `in` to check whether a value is present in a list:

```python
fruits = ["apple", "banana", "cherry"]
if "banana" in fruits:
    print("Yes, banana is in the list")
```

**Expected Output:**
```
Yes, banana is in the list
```

---

## Part 3 – Changing List Items

Lists are **mutable** — that means you can change their content after creation.

### Change a Single Item

Assign a new value using the index:

```python
fruits = ["apple", "banana", "cherry"]
fruits[1] = "mango"
print(fruits)
```

**Line-by-line:**
- `fruits[1] = "mango"` → goes to position 1, replaces `"banana"` with `"mango"`

**Expected Output:**
```
['apple', 'mango', 'cherry']
```

### Change a Range of Items

You can replace multiple items at once using slicing:

```python
fruits = ["apple", "banana", "cherry", "orange", "kiwi"]
fruits[1:3] = ["blackcurrant", "watermelon"]
print(fruits)
```

This replaces positions 1 and 2 with two new values.

**Expected Output:**
```
['apple', 'blackcurrant', 'watermelon', 'orange', 'kiwi']
```

### Replacing With More Items Than You Remove

If you insert more items than you remove, the list grows:

```python
fruits = ["apple", "banana", "cherry"]
fruits[1:2] = ["blackcurrant", "watermelon"]
print(fruits)
```

**Expected Output:**
```
['apple', 'blackcurrant', 'watermelon', 'cherry']
```

Only position 1 (`"banana"`) was removed, but two items were inserted.

### Replacing With Fewer Items Than You Remove

If you insert fewer items than you remove, the list shrinks:

```python
fruits = ["apple", "banana", "cherry"]
fruits[1:3] = ["watermelon"]
print(fruits)
```

**Expected Output:**
```
['apple', 'watermelon']
```

Two items (positions 1 and 2) were removed, only one was inserted.

### `insert()` — Add an Item at a Specific Position

`insert(index, value)` adds a new item **at** the given index, pushing existing items to the right:

```python
fruits = ["apple", "banana", "cherry"]
fruits.insert(2, "watermelon")
print(fruits)
```

**Expected Output:**
```
['apple', 'banana', 'watermelon', 'cherry']
```

`"watermelon"` was inserted at position 2; `"cherry"` moved to position 3.

---

## Part 4 – Adding Items to a List

### `append()` — Add to the End

`append(value)` adds a new item to the **end** of the list:

```python
fruits = ["apple", "banana", "cherry"]
fruits.append("orange")
print(fruits)
```

**Expected Output:**
```
['apple', 'banana', 'cherry', 'orange']
```

> 💡 `append()` is the most commonly used way to build up a list item by item — for example, collecting results in a loop.

### `insert()` — Add at a Specific Position (Recap)

```python
fruits = ["apple", "banana", "cherry"]
fruits.insert(1, "orange")
print(fruits)
```

**Expected Output:**
```
['apple', 'orange', 'banana', 'cherry']
```

### `extend()` — Add All Items From Another Collection

`extend(iterable)` adds every item from another list (or any iterable) to the end of the current list:

```python
fruits = ["apple", "banana", "cherry"]
tropical = ["mango", "pineapple", "papaya"]
fruits.extend(tropical)
print(fruits)
```

**Expected Output:**
```
['apple', 'banana', 'cherry', 'mango', 'pineapple', 'papaya']
```

> ⚠️ `extend()` adds the individual items. It is **different** from `append()` — if you did `fruits.append(tropical)`, you would add the entire list as one nested item: `['apple', 'banana', 'cherry', ['mango', 'pineapple', 'papaya']]`.

### `extend()` Works With Any Iterable

You can extend a list with a tuple, a set, or even a string:

```python
fruits = ["apple", "banana", "cherry"]
fruits.extend(("kiwi", "orange"))   # adding from a tuple
print(fruits)
```

**Expected Output:**
```
['apple', 'banana', 'cherry', 'kiwi', 'orange']
```

---

## Part 5 – Removing Items From a List

### `remove()` — Remove by Value

`remove(value)` finds the **first occurrence** of the given value and removes it:

```python
fruits = ["apple", "banana", "cherry"]
fruits.remove("banana")
print(fruits)
```

**Expected Output:**
```
['apple', 'cherry']
```

> ⚠️ If the value appears more than once, only the **first** occurrence is removed.

```python
colours = ["red", "blue", "red", "green"]
colours.remove("red")
print(colours)
```

**Expected Output:**
```
['blue', 'red', 'green']
```

The second `"red"` remains.

### `pop()` — Remove by Index

`pop(index)` removes the item at the given index **and returns it** so you can use it:

```python
fruits = ["apple", "banana", "cherry"]
removed = fruits.pop(1)
print(fruits)
print("Removed item:", removed)
```

**Expected Output:**
```
['apple', 'cherry']
Removed item: banana
```

### `pop()` With No Index — Removes the Last Item

If you call `pop()` without an index, it removes and returns the **last** item:

```python
fruits = ["apple", "banana", "cherry"]
fruits.pop()
print(fruits)
```

**Expected Output:**
```
['apple', 'banana']
```

### `del` Statement — Remove by Index or Delete the Whole List

`del list[index]` deletes the item at that index:

```python
fruits = ["apple", "banana", "cherry"]
del fruits[0]
print(fruits)
```

**Expected Output:**
```
['banana', 'cherry']
```

`del` can also delete the **entire list variable**:

```python
fruits = ["apple", "banana", "cherry"]
del fruits
# print(fruits)   # This would cause a NameError — fruits no longer exists!
```

### `clear()` — Empty the List

`clear()` removes **all items** but keeps the list variable itself:

```python
fruits = ["apple", "banana", "cherry"]
fruits.clear()
print(fruits)
```

**Expected Output:**
```
[]
```

The list still exists — it is just empty now. This is the key difference from `del`.

---

## Part 6 – Looping Through a List

### The Basic `for` Loop

A `for` loop goes through each item in a list, one by one, and lets you do something with it:

```python
fruits = ["apple", "banana", "cherry"]

for fruit in fruits:
    print(fruit)
```

**Line-by-line:**
- `for fruit in fruits:` — on each repetition, the variable `fruit` holds the current item
- First loop: `fruit = "apple"` → prints `apple`
- Second loop: `fruit = "banana"` → prints `banana`
- Third loop: `fruit = "cherry"` → prints `cherry`

**Expected Output:**
```
apple
banana
cherry
```

### Loop Through Index Numbers Using `range()` and `len()`

Sometimes you need the index number as well as the value. Use `range(len(list))`:

```python
fruits = ["apple", "banana", "cherry"]

for i in range(len(fruits)):
    print(i, fruits[i])
```

**Line-by-line:**
- `len(fruits)` → 3
- `range(3)` → produces the numbers 0, 1, 2
- `i` takes each number; `fruits[i]` accesses the item at that position

**Expected Output:**
```
0 apple
1 banana
2 cherry
```

### While Loop Through a List

A `while` loop keeps going as long as a condition is True:

```python
fruits = ["apple", "banana", "cherry"]
i = 0

while i < len(fruits):
    print(fruits[i])
    i += 1
```

**Line-by-line:**
- `i = 0` — starts at the first index
- `while i < len(fruits):` — loops while `i` is less than 3
- `fruits[i]` — accesses the current item
- `i += 1` — moves to the next index each time (without this, the loop would run forever!)

**Expected Output:**
```
apple
banana
cherry
```

### Looping With `enumerate()` — Index AND Value Together

`enumerate()` is a cleaner way to get both the index and the value at the same time:

```python
fruits = ["apple", "banana", "cherry"]

for i, fruit in enumerate(fruits):
    print(i, fruit)
```

**Expected Output:**
```
0 apple
1 banana
2 cherry
```

---

## Part 7 – List Comprehension

### What Is List Comprehension?

List comprehension is a powerful, concise way to create a **new list** from an existing list (or any iterable) — all in a **single line of code**.

### The Problem It Solves

Without list comprehension, to create a list of fruits that contain the letter "a", you would write:

```python
fruits = ["apple", "banana", "cherry", "kiwi", "mango"]
newlist = []

for x in fruits:
    if "a" in x:
        newlist.append(x)

print(newlist)
```

**Expected Output:**
```
['apple', 'banana', 'mango']
```

That is 4 lines. With list comprehension, you can do it in 1:

```python
fruits = ["apple", "banana", "cherry", "kiwi", "mango"]
newlist = [x for x in fruits if "a" in x]
print(newlist)
```

**Expected Output:**
```
['apple', 'banana', 'mango']
```

Same result, one line. That is the power of list comprehension.

### The Syntax

```
newlist = [expression   for item in iterable   if condition]
```

| Part          | Meaning                                            |
|---------------|----------------------------------------------------|
| `expression`  | What to put in the new list (can transform items)  |
| `for item in iterable` | The loop that goes through each item      |
| `if condition` | Optional filter — only include items where True   |

### Example 1 — Filter: Only items with "a"

```python
fruits = ["apple", "banana", "cherry", "kiwi", "mango"]
newlist = [x for x in fruits if "a" in x]
print(newlist)
```

**Expected Output:**
```
['apple', 'banana', 'mango']
```

### Example 2 — Filter: Only items NOT equal to "apple"

```python
fruits = ["apple", "banana", "cherry", "kiwi", "mango"]
newlist = [x for x in fruits if x != "apple"]
print(newlist)
```

**Expected Output:**
```
['banana', 'cherry', 'kiwi', 'mango']
```

### Example 3 — No condition (include everything)

```python
fruits = ["apple", "banana", "cherry", "kiwi", "mango"]
newlist = [x for x in fruits]
print(newlist)
```

**Expected Output:**
```
['apple', 'banana', 'cherry', 'kiwi', 'mango']
```

### Example 4 — Use range() as the iterable

```python
newlist = [x for x in range(10)]
print(newlist)
```

**Expected Output:**
```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Example 5 — Filter numbers: only those less than 5

```python
newlist = [x for x in range(10) if x < 5]
print(newlist)
```

**Expected Output:**
```
[0, 1, 2, 3, 4]
```

### Example 6 — Transform items: convert all fruits to uppercase

The **expression** part can transform each item:

```python
fruits = ["apple", "banana", "cherry"]
newlist = [x.upper() for x in fruits]
print(newlist)
```

**Expected Output:**
```
['APPLE', 'BANANA', 'CHERRY']
```

### Example 7 — Expression can be any value, not just `x`

```python
fruits = ["apple", "banana", "cherry"]
newlist = ["hello" for x in fruits]
print(newlist)
```

**Expected Output:**
```
['hello', 'hello', 'hello']
```

Every item in the new list is the string `"hello"`.

### Example 8 — Conditional expression (ternary) in the expression part

You can use an `if`/`else` expression inside the expression part (before `for`):

```python
fruits = ["apple", "banana", "cherry"]
newlist = [x if x != "banana" else "orange" for x in fruits]
print(newlist)
```

**Expected Output:**
```
['apple', 'orange', 'cherry']
```

This reads: "For each fruit, keep the fruit name — BUT if it is `"banana"`, replace it with `"orange"` instead."

> 🤔 **Thinking prompt:** How would you use list comprehension to create a list of all even numbers between 0 and 20?

---

## Part 8 – Sorting Lists

### `sort()` — Sort in Ascending Order

`sort()` sorts the list **in place** (it modifies the original list):

```python
fruits = ["orange", "mango", "kiwi", "pineapple", "banana"]
fruits.sort()
print(fruits)
```

**Expected Output:**
```
['banana', 'kiwi', 'mango', 'orange', 'pineapple']
```

Strings are sorted alphabetically (A → Z).

```python
numbers = [100, 50, 65, 82, 23]
numbers.sort()
print(numbers)
```

**Expected Output:**
```
[23, 50, 65, 82, 100]
```

Numbers are sorted from smallest to largest.

### `sort(reverse=True)` — Sort in Descending Order

```python
fruits = ["orange", "mango", "kiwi", "pineapple", "banana"]
fruits.sort(reverse=True)
print(fruits)
```

**Expected Output:**
```
['pineapple', 'orange', 'mango', 'kiwi', 'banana']
```

```python
numbers = [100, 50, 65, 82, 23]
numbers.sort(reverse=True)
print(numbers)
```

**Expected Output:**
```
[100, 82, 65, 50, 23]
```

### Custom Sort Using `key` Function

You can define your own sorting logic using the `key` parameter. The `key` is a function that transforms each item before comparing.

**Example — Sort by how close each number is to 50:**

```python
def myfunc(n):
    return abs(n - 50)

numbers = [100, 50, 65, 82, 23]
numbers.sort(key=myfunc)
print(numbers)
```

**Expected Output:**
```
[50, 65, 23, 82, 100]
```

`abs(n - 50)` gives the distance from 50. The closest numbers come first.

### Case-Insensitive Sort

By default, Python sorts strings case-sensitively. Uppercase letters come before lowercase in ASCII ordering:

```python
fruits = ["banana", "Orange", "Kiwi", "cherry"]
fruits.sort()
print(fruits)
```

**Expected Output:**
```
['Kiwi', 'Orange', 'banana', 'cherry']
```

Capital letters come first! To sort without caring about case, use `key=str.lower`:

```python
fruits = ["banana", "Orange", "Kiwi", "cherry"]
fruits.sort(key=str.lower)
print(fruits)
```

**Expected Output:**
```
['banana', 'cherry', 'Kiwi', 'Orange']
```

### `reverse()` — Reverse the Order of a List

`reverse()` simply flips the list — it does **not** sort, it just reverses whatever order the items are currently in:

```python
fruits = ["banana", "Orange", "Kiwi", "cherry"]
fruits.reverse()
print(fruits)
```

**Expected Output:**
```
['cherry', 'Kiwi', 'Orange', 'banana']
```

### `sorted()` — Return a Sorted Copy Without Changing Original

Unlike `sort()`, the built-in function `sorted()` creates a **new** sorted list and leaves the original untouched:

```python
fruits = ["orange", "mango", "kiwi"]
sorted_fruits = sorted(fruits)
print(sorted_fruits)   # sorted copy
print(fruits)          # original unchanged
```

**Expected Output:**
```
['kiwi', 'mango', 'orange']
['orange', 'mango', 'kiwi']
```

---

## Part 9 – Copying a List

### Why You Cannot Just Use `=`

This is one of the most important and most misunderstood topics for beginners. Look at this:

```python
list1 = ["apple", "banana", "cherry"]
list2 = list1
list2.append("orange")
print(list1)
print(list2)
```

**Expected Output:**
```
['apple', 'banana', 'cherry', 'orange']
['apple', 'banana', 'cherry', 'orange']
```

Both lists changed! Why?

Because `list2 = list1` does **not** copy the list — it makes `list2` point to the **same list in memory**. There is still only one list, and both `list1` and `list2` are two names for the same thing.

> 💡 **Analogy:** It is like two remote controls pointing at the same TV. Pressing a button on either remote changes the same TV.

To create a truly independent copy, use one of these methods:

### Method 1 — `copy()` Method

```python
list1 = ["apple", "banana", "cherry"]
list2 = list1.copy()
list2.append("orange")
print(list1)   # unchanged
print(list2)   # has orange
```

**Expected Output:**
```
['apple', 'banana', 'cherry']
['apple', 'banana', 'cherry', 'orange']
```

Now they are independent.

### Method 2 — `list()` Constructor

```python
list1 = ["apple", "banana", "cherry"]
list2 = list(list1)
print(list2)
```

**Expected Output:**
```
['apple', 'banana', 'cherry']
```

### Method 3 — Slice `[:]`

This creates a full slice of the entire list, which is effectively a copy:

```python
list1 = ["apple", "banana", "cherry"]
list2 = list1[:]
print(list2)
```

**Expected Output:**
```
['apple', 'banana', 'cherry']
```

All three methods produce a shallow copy — an independent list with the same top-level items.

---

## Part 10 – Joining Two Lists

### Method 1 — The `+` Operator

The `+` operator concatenates (joins) two lists into one new list:

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

The original lists are not modified.

### Method 2 — `extend()` Method

`extend()` adds all items from one list to the end of another, modifying the first list:

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

`list1` is modified in place. `list2` is unchanged.

### Method 3 — A `for` Loop

Manually appending each item:

```python
list1 = ["a", "b", "c"]
list2 = [1, 2, 3]

for item in list2:
    list1.append(item)

print(list1)
```

**Expected Output:**
```
['a', 'b', 'c', 1, 2, 3]
```

This is the most verbose approach but is useful when you want to filter or transform items during the join.

---

## Part 11 – List Methods Reference

Python provides many built-in methods for lists. Here is a complete reference with explanations and examples.

### `append(value)` — Add item to end

```python
fruits = ["apple", "banana"]
fruits.append("cherry")
print(fruits)   # ['apple', 'banana', 'cherry']
```

### `insert(index, value)` — Add item at position

```python
fruits = ["apple", "cherry"]
fruits.insert(1, "banana")
print(fruits)   # ['apple', 'banana', 'cherry']
```

### `extend(iterable)` — Add all items from another iterable

```python
fruits = ["apple"]
fruits.extend(["banana", "cherry"])
print(fruits)   # ['apple', 'banana', 'cherry']
```

### `remove(value)` — Remove first occurrence of value

```python
fruits = ["apple", "banana", "cherry"]
fruits.remove("banana")
print(fruits)   # ['apple', 'cherry']
```

### `pop(index)` — Remove item at index (default: last item)

```python
fruits = ["apple", "banana", "cherry"]
item = fruits.pop(1)
print(fruits)   # ['apple', 'cherry']
print(item)     # banana
```

### `del list[index]` — Delete item at index

```python
fruits = ["apple", "banana", "cherry"]
del fruits[0]
print(fruits)   # ['banana', 'cherry']
```

### `clear()` — Remove all items

```python
fruits = ["apple", "banana", "cherry"]
fruits.clear()
print(fruits)   # []
```

### `index(value)` — Return index of first occurrence

```python
fruits = ["apple", "banana", "cherry"]
print(fruits.index("cherry"))   # 2
```

### `count(value)` — Count how many times a value appears

```python
fruits = ["apple", "banana", "apple", "cherry", "apple"]
print(fruits.count("apple"))   # 3
```

### `sort()` — Sort the list in ascending order

```python
numbers = [3, 1, 4, 1, 5]
numbers.sort()
print(numbers)   # [1, 1, 3, 4, 5]
```

### `sort(reverse=True)` — Sort in descending order

```python
numbers = [3, 1, 4, 1, 5]
numbers.sort(reverse=True)
print(numbers)   # [5, 4, 3, 1, 1]
```

### `reverse()` — Reverse the order of items

```python
fruits = ["apple", "banana", "cherry"]
fruits.reverse()
print(fruits)   # ['cherry', 'banana', 'apple']
```

### `copy()` — Return a shallow copy

```python
fruits = ["apple", "banana", "cherry"]
copy = fruits.copy()
print(copy)   # ['apple', 'banana', 'cherry']
```

### Quick Reference Table

| Method          | What It Does                              | Returns      |
|-----------------|-------------------------------------------|--------------|
| `append(x)`     | Adds `x` to the end                       | `None`       |
| `insert(i, x)`  | Inserts `x` at index `i`                  | `None`       |
| `extend(iter)`  | Adds all items from `iter`                | `None`       |
| `remove(x)`     | Removes first occurrence of `x`           | `None`       |
| `pop(i)`        | Removes and returns item at `i`           | The item     |
| `clear()`       | Empties the list                          | `None`       |
| `index(x)`      | Returns index of first `x`                | Index number |
| `count(x)`      | Counts how many times `x` appears         | Count number |
| `sort()`        | Sorts in place (ascending by default)     | `None`       |
| `reverse()`     | Reverses in place                         | `None`       |
| `copy()`        | Returns a shallow copy                    | New list     |

---

## Guided Practice Exercises

### Exercise 1 – Build a Shopping List

**Objective:** Practice creating, appending, and printing a list.

**Scenario:** You are building a grocery shopping list.

**Steps:**
1. Create an empty list called `shopping`
2. Use `append()` to add 5 grocery items one by one
3. Print the full list
4. Print how many items are in the list

```python
shopping = []
shopping.append("rice")
shopping.append("tomatoes")
shopping.append("onions")
shopping.append("eggs")
shopping.append("milk")

print("Shopping list:", shopping)
print("Total items:", len(shopping))
```

**Expected Output:**
```
Shopping list: ['rice', 'tomatoes', 'onions', 'eggs', 'milk']
Total items: 5
```

**What-if challenge:** Add `"bread"` at position 2 using `insert()`. Then print the updated list.

---

### Exercise 2 – Student Score Analyser

**Objective:** Practice accessing, modifying, and using list methods.

**Scenario:** A class has five students with these test scores. The teacher needs to fix a data entry error and analyse the results.

```python
scores = [78, 45, 92, 61, 88]

# Step 1: Print the original list
print("Original scores:", scores)

# Step 2: The score of 45 was a data entry error — it should be 75
scores[1] = 75
print("Corrected scores:", scores)

# Step 3: Sort the scores from lowest to highest
scores.sort()
print("Sorted scores:", scores)

# Step 4: Print the highest score (last after sorting)
print("Highest score:", scores[-1])

# Step 5: Print the lowest score (first after sorting)
print("Lowest score:", scores[0])
```

**Expected Output:**
```
Original scores: [78, 45, 92, 61, 88]
Corrected scores: [78, 75, 92, 61, 88]
Sorted scores: [61, 75, 78, 88, 92]
Highest score: 92
Lowest score: 61
```

---

### Exercise 3 – List Comprehension: Even Numbers

**Objective:** Practice list comprehension with a numeric range.

```python
# Create a list of all even numbers from 0 to 20 (inclusive)
evens = [x for x in range(21) if x % 2 == 0]
print(evens)
```

**Expected Output:**
```
[0, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20]
```

**What-if challenge:** Modify it to get all numbers divisible by 3 between 0 and 30.

---

### Exercise 4 – Loop and Label

**Objective:** Practice looping with `enumerate()`.

```python
subjects = ["Maths", "English", "Science", "History", "Art"]

for i, subject in enumerate(subjects):
    print(f"Subject {i+1}: {subject}")
```

**Expected Output:**
```
Subject 1: Maths
Subject 2: English
Subject 3: Science
Subject 4: History
Subject 5: Art
```

> 💡 `f"..."` is an f-string — a way to embed variable values directly inside a string using `{}`.

---

### Exercise 5 – Removing Items Safely

**Objective:** Practice `remove()`, `pop()`, and `clear()`.

```python
inventory = ["laptop", "mouse", "keyboard", "monitor", "headphones"]
print("Original:", inventory)

# Remove "mouse" by name
inventory.remove("mouse")
print("After remove:", inventory)

# Pop the last item and display what was removed
removed = inventory.pop()
print("Popped:", removed)
print("After pop:", inventory)

# Clear the list
inventory.clear()
print("After clear:", inventory)
```

**Expected Output:**
```
Original: ['laptop', 'mouse', 'keyboard', 'monitor', 'headphones']
After remove: ['laptop', 'keyboard', 'monitor', 'headphones']
Popped: headphones
After pop: ['laptop', 'keyboard', 'monitor']
After clear: []
```

---

### Exercise 6 – The Copy Trap

**Objective:** Understand why `list2 = list1` is dangerous.

```python
# Dangerous — both names point to the same list
original = [1, 2, 3]
wrong_copy = original
wrong_copy.append(99)
print("original:", original)       # Also changed!
print("wrong_copy:", wrong_copy)

# Correct — use .copy()
original = [1, 2, 3]
real_copy = original.copy()
real_copy.append(99)
print("original:", original)       # Unchanged
print("real_copy:", real_copy)
```

**Expected Output:**
```
original: [1, 2, 3, 99]
wrong_copy: [1, 2, 3, 99]
original: [1, 2, 3]
real_copy: [1, 2, 3, 99]
```

---

## Mini Project – Student Grade Manager

### Project Goal

Build a complete student grade management program that:
1. Stores student names and scores
2. Finds top and bottom performers
3. Filters passing students using list comprehension
4. Sorts and displays a ranked leaderboard

### Stage 1 – Set Up the Data

```python
students = ["Amara", "Tunde", "Ngozi", "Emeka", "Chisom", "Femi", "Aisha"]
scores   = [82, 67, 91, 55, 78, 43, 88]
```

**Milestone:** Two parallel lists — student names and their corresponding scores.

### Stage 2 – Basic Information

```python
print("=== CLASS OVERVIEW ===")
print(f"Total students: {len(students)}")
print(f"Scores recorded: {len(scores)}")
```

**Expected Output:**
```
=== CLASS OVERVIEW ===
Total students: 7
Scores recorded: 7
```

### Stage 3 – Display All Results

```python
print("\n=== ALL RESULTS ===")
for i in range(len(students)):
    print(f"{students[i]}: {scores[i]}")
```

**Expected Output:**
```
=== ALL RESULTS ===
Amara: 82
Tunde: 67
Ngozi: 91
Emeka: 55
Chisom: 78
Femi: 43
Aisha: 88
```

### Stage 4 – Find Top and Bottom Scorers

```python
highest = max(scores)
lowest  = min(scores)

top_index    = scores.index(highest)
bottom_index = scores.index(lowest)

print(f"\nTop scorer:    {students[top_index]} with {highest}")
print(f"Bottom scorer: {students[bottom_index]} with {lowest}")
```

**Expected Output:**
```
Top scorer:    Ngozi with 91
Bottom scorer: Femi with 43
```

### Stage 5 – Filter Passing Students (score ≥ 50)

```python
passing = [students[i] for i in range(len(students)) if scores[i] >= 50]
failing = [students[i] for i in range(len(students)) if scores[i] < 50]

print(f"\nPassing students ({len(passing)}): {passing}")
print(f"Failing students ({len(failing)}): {failing}")
```

**Expected Output:**
```
Passing students (6): ['Amara', 'Tunde', 'Ngozi', 'Emeka', 'Chisom', 'Aisha']
Failing students (1): ['Femi']
```

### Stage 6 – Sort and Display Leaderboard

```python
# Pair students with scores and sort by score descending
paired = list(zip(students, scores))
paired.sort(key=lambda x: x[1], reverse=True)

print("\n=== LEADERBOARD ===")
for rank, (name, score) in enumerate(paired, 1):
    print(f"{rank}. {name}: {score}")
```

**Expected Output:**
```
=== LEADERBOARD ===
1. Ngozi: 91
2. Aisha: 88
3. Amara: 82
4. Chisom: 78
5. Tunde: 67
6. Emeka: 55
7. Femi: 43
```

### Reflection Questions

1. What would happen if two students had the same score? How would the leaderboard look?
2. How could you add a new student and score mid-program?
3. How would you calculate the class average score?
4. What does `zip()` do in Stage 6? Why is it useful?

### Optional Extension

Calculate and print the class average:

```python
average = sum(scores) / len(scores)
print(f"\nClass average: {average:.1f}")
```

**Expected Output:**
```
Class average: 72.0
```

---

## Common Beginner Mistakes

### Mistake 1 – Using index 1 for the first item

```python
fruits = ["apple", "banana", "cherry"]

# ❌ Wrong — index 1 is the SECOND item
print(fruits[1])   # banana

# ✅ Correct — index 0 is the FIRST item
print(fruits[0])   # apple
```

**Why:** Python lists start counting at 0, not 1.

---

### Mistake 2 – Index out of range

```python
fruits = ["apple", "banana", "cherry"]

# ❌ Wrong — there is no index 3 in a 3-item list (0, 1, 2)
print(fruits[3])   # IndexError: list index out of range

# ✅ Correct — last valid index is len(fruits) - 1 = 2
print(fruits[2])   # cherry
# Or use negative index:
print(fruits[-1])  # cherry
```

---

### Mistake 3 – `append()` vs `extend()` confusion

```python
fruits = ["apple", "banana"]
more   = ["cherry", "kiwi"]

# ❌ append adds the LIST as one item
fruits.append(more)
print(fruits)   # ['apple', 'banana', ['cherry', 'kiwi']]

# ✅ extend adds each item individually
fruits = ["apple", "banana"]
fruits.extend(more)
print(fruits)   # ['apple', 'banana', 'cherry', 'kiwi']
```

---

### Mistake 4 – Copying with `=` instead of `.copy()`

```python
# ❌ This does NOT create a copy — both names point to the same list
list2 = list1

# ✅ This creates a real independent copy
list2 = list1.copy()
```

---

### Mistake 5 – Slicing end index is exclusive

```python
fruits = ["apple", "banana", "cherry", "orange"]

# ❌ Thinking fruits[1:3] includes index 3
print(fruits[1:3])   # ['banana', 'cherry'] — NOT 'orange'

# The rule: start is INCLUSIVE, end is EXCLUSIVE
```

---

### Mistake 6 – `sort()` modifies original; `sorted()` returns a new list

```python
numbers = [3, 1, 2]

# sort() changes the list in place, returns None
result = numbers.sort()
print(result)    # None  ← common mistake!
print(numbers)   # [1, 2, 3]

# sorted() returns a new sorted list, original unchanged
numbers = [3, 1, 2]
result = sorted(numbers)
print(result)    # [1, 2, 3]
print(numbers)   # [3, 1, 2]
```

---

### Mistake 7 – Modifying a list while looping through it

```python
numbers = [1, 2, 3, 4, 5]

# ❌ Dangerous — removing items while looping causes skipped items
for n in numbers:
    if n % 2 == 0:
        numbers.remove(n)

print(numbers)   # [1, 3, 5] — might seem fine but can skip items!

# ✅ Safer — loop over a copy
for n in numbers[:]:
    if n % 2 == 0:
        numbers.remove(n)
```

---

## Reflection Questions

1. What is the index of the **last item** in a list of 10 items?
2. What is the difference between `remove()` and `pop()`?
3. What does `list2 = list1.copy()` do that `list2 = list1` does not?
4. You have a list: `nums = [5, 3, 8, 1]`. After calling `nums.sort()`, what does `nums` look like?
5. What does the `in` keyword do when used with a list?
6. What is the difference between `append()` and `extend()`?
7. Write a list comprehension that creates a list of squares of numbers 1 through 10.
8. What does `sort(reverse=True)` do differently from `reverse()`?
9. What is the difference between `sort()` and `sorted()`?
10. What does `clear()` do? How is it different from `del mylist`?

---

## Completion Checklist

Before moving to the next lesson, confirm you can:

- [ ] Create a list with different data types
- [ ] Access items using positive and negative indexes
- [ ] Use slicing to extract a range of items
- [ ] Change individual items and ranges of items
- [ ] Add items with `append()`, `insert()`, and `extend()`
- [ ] Remove items with `remove()`, `pop()`, `del`, and `clear()`
- [ ] Loop through a list with `for`, `while`, and `enumerate()`
- [ ] Write a list comprehension with and without a condition
- [ ] Sort a list ascending and descending with `sort()` and `sorted()`
- [ ] Reverse a list with `reverse()`
- [ ] Copy a list correctly using `.copy()` or `list()`
- [ ] Join two lists using `+` and `extend()`
- [ ] Recall what each list method does from the reference table
- [ ] Avoid all common beginner mistakes listed above

---

## Lesson Summary

You have now mastered Python Lists — one of the most powerful tools in the entire language. Here is a compact summary:

**Creating a list:**
```python
fruits = ["apple", "banana", "cherry"]
```

**Accessing items:**
```python
fruits[0]    # apple  (first)
fruits[-1]   # cherry (last)
fruits[1:3]  # ['banana', 'cherry'] (slice)
```

**Changing items:**
```python
fruits[1] = "mango"
```

**Adding items:**
```python
fruits.append("orange")       # add to end
fruits.insert(1, "kiwi")      # add at position
fruits.extend(["grape", "plum"]) # add many
```

**Removing items:**
```python
fruits.remove("mango")    # by value
fruits.pop(0)             # by index (returns item)
del fruits[0]             # by index (no return)
fruits.clear()            # remove all
```

**Looping:**
```python
for fruit in fruits:
    print(fruit)

for i, fruit in enumerate(fruits):
    print(i, fruit)
```

**List comprehension:**
```python
newlist = [x.upper() for x in fruits if "a" in x]
```

**Sorting:**
```python
fruits.sort()               # ascending, in place
fruits.sort(reverse=True)   # descending, in place
sorted_copy = sorted(fruits) # new sorted list
```

**Copying:**
```python
copy = fruits.copy()   # or: list(fruits) or fruits[:]
```

**Joining:**
```python
combined = list1 + list2
list1.extend(list2)
```

Lists are the foundation of data processing in Python. Everything you learn from here — loops, functions, file handling, data analysis — will use lists constantly. You are now well-equipped to move forward!
