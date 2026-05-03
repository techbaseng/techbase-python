---
render_with_liquid: false
title: "Python Tuples – A Complete Beginner's Guide"
nav_order: 12
---

# Lesson 12: Python Tuples — Everything You Need to Know

---

## 📌 Lesson Introduction

Welcome to Lesson 12! In the last lesson, you learned about **Lists** — collections of items you can freely change. Today you will meet their close cousin: the **Tuple**.

A tuple is also a collection of items. But there's one big difference: **once you create a tuple, you cannot change it**. This might sound strange at first — why would you want data you can't change? By the end of this lesson, you will understand exactly why tuples exist, when to use them, and how to work with them confidently.

Here is what you will learn:
- What a tuple is and why it exists
- How to create tuples and access items inside them
- How to work around the "unchangeable" rule when you really need to
- How to unpack a tuple into separate variables
- How to loop through a tuple
- How to join tuples together
- Which built-in methods tuples provide
- How to use tuples in real-world mini projects

**No prior knowledge beyond what was covered in Lessons 1–11 is needed.** If you have completed the Lists lesson, you are perfectly ready. Let's go!

---

## 🔑 Prerequisite Concepts

Before we begin, let's quickly review a few ideas you already know, because we'll use them throughout this lesson.

### What is a Variable?

A variable is a name that stores a value. For example:

```python
name = "Alice"
age = 25
```

`name` stores the text `"Alice"`. `age` stores the number `25`.

### What is a List?

A list is a collection of items stored in a single variable, written with **square brackets** `[ ]`.

```python
fruits = ["apple", "banana", "cherry"]
print(fruits)
```

**Output:**
```
['apple', 'banana', 'cherry']
```

You can **change** a list after creating it — add items, remove items, swap items.

### What is an Index?

An index is the position number of an item in a collection. Python counts from **0**, not from 1.

```python
fruits = ["apple", "banana", "cherry"]
#          index 0   index 1   index 2
print(fruits[0])  # apple
print(fruits[2])  # cherry
```

**Output:**
```
apple
cherry
```

Now you are ready for tuples!

---

## 🧠 Part 1: What is a Tuple?

### The Big Idea

Imagine you are writing a program that stores the **GPS coordinates** of a city — say, latitude and longitude. These values should **never change** because Lagos is always at the same location on Earth. You don't want any part of your code accidentally modifying them.

For situations like this, Python gives you the **tuple** — a collection that is **locked** after creation.

> **Analogy:** Think of a list as a whiteboard you can erase and rewrite anytime. A tuple is a **printed certificate** — once it is printed, no one can change what it says.

### Technical Definition

A **tuple** is a collection in Python that is:
- **Ordered** — items have a fixed position (index 0, 1, 2, ...)
- **Unchangeable (Immutable)** — you cannot add, remove, or change items after creation
- **Allows duplicates** — the same value can appear more than once

Tuples are written with **round brackets (parentheses)** `( )`.

---

## 🔍 Part 2: Creating Tuples

### 2.1 Basic Tuple Syntax

```python
# Creating a simple tuple
mytuple = ("apple", "banana", "cherry")
print(mytuple)
```

**Output:**
```
('apple', 'banana', 'cherry')
```

Let's break this line down:
- `mytuple` — the name we give this tuple (just like any variable name)
- `=` — the assignment operator; it says "store this value in this variable"
- `(` — the opening round bracket; this tells Python we are creating a tuple
- `"apple", "banana", "cherry"` — three items separated by commas
- `)` — the closing round bracket

> **Why round brackets?** Square brackets `[ ]` are for lists. Round brackets `( )` are for tuples. This difference helps Python (and you!) tell them apart instantly.

---

### 2.2 Tuple Items are Ordered

When we say a tuple is **ordered**, we mean every item has a specific position that never changes.

```python
colors = ("red", "green", "blue")
#          pos 0   pos 1    pos 2
print(colors[0])  # red
print(colors[1])  # green
print(colors[2])  # blue
```

**Output:**
```
red
green
blue
```

If you create a tuple with `("red", "green", "blue")`, red will **always** be at position 0 and blue will **always** be at position 2.

---

### 2.3 Tuples Allow Duplicates

Since items are identified by position (index), the same value can appear more than once:

```python
thistuple = ("apple", "banana", "cherry", "apple", "cherry")
print(thistuple)
```

**Output:**
```
('apple', 'banana', 'cherry', 'apple', 'cherry')
```

Both `"apple"` values are perfectly valid — one is at index 0 and the other at index 3. They occupy different positions.

---

### 2.4 Tuple Length with `len()`

To count how many items are in a tuple, use the `len()` function (short for "length"):

```python
thistuple = ("apple", "banana", "cherry")
print(len(thistuple))
```

**Output:**
```
3
```

`len()` counts the items and gives you back a whole number.

---

### 2.5 The Tricky One-Item Tuple

What if you want a tuple with just one item? You might try this:

```python
# This is NOT a tuple — Python thinks the brackets are just grouping
thistuple = ("apple")
print(type(thistuple))
```

**Output:**
```
<class 'str'>
```

Python saw `("apple")` and thought: "This is just the word 'apple' in brackets, like in math — it is still a string." To make Python recognise it as a **tuple**, you must add a **trailing comma** after the single item:

```python
# THIS is a one-item tuple
thistuple = ("apple",)
print(type(thistuple))
```

**Output:**
```
<class 'tuple'>
```

> **Remember the comma rule:** A one-item tuple must have a comma after the item. `("apple",)` ✅ — `("apple")` ❌

---

### 2.6 Tuples Can Hold Mixed Data Types

A tuple is not restricted to only strings or only numbers. It can hold any mix:

```python
# Only strings
tuple1 = ("apple", "banana", "cherry")

# Only integers
tuple2 = (1, 5, 7, 9, 3)

# Only booleans
tuple3 = (True, False, False)

# Mixed types
tuple4 = ("abc", 34, True, 40, "male")

print(tuple1)
print(tuple2)
print(tuple3)
print(tuple4)
```

**Output:**
```
('apple', 'banana', 'cherry')
(1, 5, 7, 9, 3)
(False, False, False)
('abc', 34, True, 40, 'male')
```

This is useful in real programs. For example, you might store a record about a student as `("Alice", 17, True, "Senior")` — name, age, enrolled status, year group — all in one tuple.

---

### 2.7 Checking the Data Type

Python stores tuples as objects of type `tuple`. You can verify this with `type()`:

```python
mytuple = ("apple", "banana", "cherry")
print(type(mytuple))
```

**Output:**
```
<class 'tuple'>
```

---

### 2.8 Using the `tuple()` Constructor

Another way to create a tuple is to use the built-in `tuple()` function (called a **constructor**). Notice the **double round brackets** — one belongs to the function call, the other belongs to the inner collection:

```python
thistuple = tuple(("apple", "banana", "cherry"))  # note the double round-brackets
print(thistuple)
```

**Output:**
```
('apple', 'banana', 'cherry')
```

> **Thinking Prompt:** Why would you ever use `tuple()` instead of just writing `(...)` ? This comes in handy when you start with a list and want to convert it into a tuple, like `tuple(my_list)`.

---

### 2.9 Python's Four Collection Types — Side by Side

Python has four ways to store collections of data. Here's how they compare:

| Collection | Symbol | Ordered? | Changeable? | Duplicates? |
|---|---|---|---|---|
| **List** | `[ ]` | ✅ Yes | ✅ Yes | ✅ Yes |
| **Tuple** | `( )` | ✅ Yes | ❌ No | ✅ Yes |
| **Set** | `{ }` | ❌ No | ⚠️ Items can't change | ❌ No |
| **Dictionary** | `{ key: value }` | ✅ Yes (Python 3.7+) | ✅ Yes | ❌ No (keys) |

Choosing the right one matters. Use a **tuple** when your data should stay fixed, like coordinates, RGB colour values, or days of the week.

---

## 🔍 Part 3: Accessing Tuple Items

Now that you know how to create tuples, let's look at how to **read individual items** from them.

### 3.1 Accessing by Positive Index

Just like lists, you access a tuple item using square brackets with the index number.

```python
thistuple = ("apple", "banana", "cherry")
print(thistuple[1])
```

**Output:**
```
banana
```

Remember: index **0** is the first item, index **1** is the second, and so on.

```python
fruits = ("mango", "kiwi", "grape", "pear")
print(fruits[0])   # first item
print(fruits[3])   # fourth item
```

**Output:**
```
mango
pear
```

> **Thinking Prompt:** What happens if you try `fruits[4]` when there are only 4 items (indices 0–3)? Try it and read the error message carefully!

---

### 3.2 Negative Indexing — Counting from the End

Python allows **negative indexing**, which counts backwards from the end of the tuple.

- `-1` = the **last** item
- `-2` = the **second to last** item
- `-3` = the **third from the end**, etc.

```python
thistuple = ("apple", "banana", "cherry")
print(thistuple[-1])   # last item
print(thistuple[-2])   # second to last
```

**Output:**
```
cherry
banana
```

This is extremely useful when you don't know the exact length of a tuple but always need the last item.

**Real-world use:** In data processing, you might receive a tuple of sensor readings. You almost always want the most recent (last) reading — `readings[-1]` gets it without needing to know the total count.

---

### 3.3 Range of Indexes (Slicing)

You can extract a **portion** (called a "slice") of a tuple by specifying a start and end index:

```python
thistuple = ("apple", "banana", "cherry", "orange", "kiwi", "melon", "mango")
print(thistuple[2:5])
```

**Output:**
```
('cherry', 'orange', 'kiwi')
```

The slice `[2:5]` means:
- **Start at index 2** (included) — `"cherry"`
- **Stop before index 5** (not included) — so stop before `"kiwi"` at index 4

> **Important rule:** The end index is **exclusive** — the item at that index is NOT included. `[2:5]` gives you items at positions 2, 3, and 4 — NOT 5.

**Leaving out the start — slice from the beginning:**

```python
thistuple = ("apple", "banana", "cherry", "orange", "kiwi", "melon", "mango")
print(thistuple[:4])
```

**Output:**
```
('apple', 'banana', 'cherry', 'orange')
```

No start means "begin at index 0".

**Leaving out the end — slice to the end:**

```python
thistuple = ("apple", "banana", "cherry", "orange", "kiwi", "melon", "mango")
print(thistuple[2:])
```

**Output:**
```
('cherry', 'orange', 'kiwi', 'melon', 'mango')
```

No end means "go all the way to the last item".

---

### 3.4 Negative Index Slicing

You can also slice using negative indexes:

```python
thistuple = ("apple", "banana", "cherry", "orange", "kiwi", "melon", "mango")
print(thistuple[-4:-1])
```

**Output:**
```
('orange', 'kiwi', 'melon')
```

`[-4:-1]` means: from the 4th-from-last item (index -4, which is "orange"), up to but not including the last item (index -1, which is "mango").

---

### 3.5 Checking if an Item Exists — The `in` Keyword

To check if a specific value is present in a tuple, use the `in` keyword:

```python
thistuple = ("apple", "banana", "cherry")
if "apple" in thistuple:
    print("Yes, 'apple' is in the fruits tuple")
```

**Output:**
```
Yes, 'apple' is in the fruits tuple
```

This returns `True` if the item is found, `False` if not.

```python
thistuple = ("apple", "banana", "cherry")
print("mango" in thistuple)    # False
print("banana" in thistuple)   # True
```

**Output:**
```
False
True
```

---

## 🔍 Part 4: Updating Tuples (Workarounds)

### Why Can't We Change a Tuple?

You now know tuples are **immutable** (unchangeable). If you try to directly modify a tuple item, Python will throw an error:

```python
thistuple = ("apple", "banana", "cherry")
thistuple[1] = "kiwi"   # ❌ This will cause an error!
```

**Error:**
```
TypeError: 'tuple' object does not support item assignment
```

This is by design — tuples are meant to be permanent. But Python is flexible. If you truly need to change a tuple's data, there are three workarounds.

---

### 4.1 Workaround 1: Convert → Change → Convert Back

The most common approach:
1. Convert the tuple to a **list** (mutable)
2. Make your changes
3. Convert the list back to a **tuple**

```python
x = ("apple", "banana", "cherry")

# Step 1: Convert tuple to list
y = list(x)

# Step 2: Change the item
y[1] = "kiwi"

# Step 3: Convert back to tuple
x = tuple(y)

print(x)
```

**Output:**
```
('apple', 'kiwi', 'cherry')
```

Let's trace through every step:
- `y = list(x)` — creates `["apple", "banana", "cherry"]` (a list)
- `y[1] = "kiwi"` — replaces "banana" with "kiwi" in the **list**
- `x = tuple(y)` — converts the modified list back into a tuple
- Now `x` points to a brand new tuple `('apple', 'kiwi', 'cherry')`

---

### 4.2 Workaround 2: Adding Items via List Conversion

Since tuples have no `.append()` method, use the list conversion trick:

```python
thistuple = ("apple", "banana", "cherry")

# Convert to list, add item, convert back
y = list(thistuple)
y.append("orange")
thistuple = tuple(y)

print(thistuple)
```

**Output:**
```
('apple', 'banana', 'cherry', 'orange')
```

---

### 4.3 Workaround 3: Adding Items by Concatenating Tuples

You can **add two tuples together** to create a new, longer tuple:

```python
thistuple = ("apple", "banana", "cherry")
y = ("orange",)          # single-item tuple — note the trailing comma!
thistuple += y           # += is shorthand for: thistuple = thistuple + y

print(thistuple)
```

**Output:**
```
('apple', 'banana', 'cherry', 'orange')
```

`+=` here adds the second tuple to the end of the first, creating a new combined tuple.

> **Note:** `("orange",)` uses a trailing comma because it is a one-item tuple. `("orange")` without the comma is just a string in parentheses.

---

### 4.4 Removing Items from a Tuple

You **cannot** directly remove items from a tuple. But you can:

**Option A: Convert to list, remove, convert back:**

```python
thistuple = ("apple", "banana", "cherry")
y = list(thistuple)
y.remove("apple")
thistuple = tuple(y)
print(thistuple)
```

**Output:**
```
('banana', 'cherry')
```

**Option B: Delete the entire tuple with `del`:**

```python
thistuple = ("apple", "banana", "cherry")
del thistuple
# print(thistuple)  # This would raise an error — thistuple no longer exists
```

After `del thistuple`, the variable `thistuple` is completely removed from memory. Trying to use it afterwards will produce a `NameError`.

---

## 🔍 Part 5: Unpacking Tuples

### What Does "Packing" Mean?

When you assign values to a tuple like this:

```python
fruits = ("apple", "banana", "cherry")
```

You are **packing** three values into a single tuple variable. The values are bundled together in `fruits`.

### What Does "Unpacking" Mean?

**Unpacking** is the reverse: extracting the values back out into separate individual variables.

```python
fruits = ("apple", "banana", "cherry")

# Unpack the tuple into three variables
(green, yellow, red) = fruits

print(green)
print(yellow)
print(red)
```

**Output:**
```
apple
banana
cherry
```

Line by line:
- `(green, yellow, red) = fruits` — Python looks at the tuple `fruits` and assigns each value to the matching variable in order
- `green` gets `"apple"` (position 0)
- `yellow` gets `"banana"` (position 1)
- `red` gets `"cherry"` (position 2)

> **Rule:** The number of variables on the left **must match** the number of items in the tuple. If they don't match and you haven't used an asterisk `*`, Python will raise a `ValueError`.

**Real-world use:** When a function returns multiple values as a tuple, you can unpack them in one clean line:

```python
def get_coordinates():
    return (6.5244, 3.3792)   # Latitude and Longitude of Lagos

lat, lon = get_coordinates()
print(f"Latitude: {lat}, Longitude: {lon}")
```

**Output:**
```
Latitude: 6.5244, Longitude: 3.3792
```

---

### 5.1 Unpacking with Asterisk `*` (Collecting Remaining Values)

What if you have more tuple items than variables? Use `*` in front of one variable name to collect all extra items into a **list**:

```python
fruits = ("apple", "banana", "cherry", "strawberry", "raspberry")

(green, yellow, *red) = fruits

print(green)    # apple
print(yellow)   # banana
print(red)      # ['cherry', 'strawberry', 'raspberry']
```

**Output:**
```
apple
banana
['cherry', 'strawberry', 'raspberry']
```

The `*red` variable collects everything that was not assigned to `green` or `yellow`. It becomes a list of the remaining values.

**Putting `*` in the middle:**

```python
fruits = ("apple", "mango", "papaya", "pineapple", "cherry")

(green, *tropic, red) = fruits

print(green)     # apple
print(tropic)    # ['mango', 'papaya', 'pineapple']
print(red)       # cherry
```

**Output:**
```
apple
['mango', 'papaya', 'pineapple']
cherry
```

Python figures this out by working from both ends: `green` takes the first item, `red` takes the last item, and `*tropic` collects everything in between as a list.

---

## 🔍 Part 6: Looping Through Tuples

Loops let you go through each item in a tuple one by one and do something with it.

### 6.1 The `for` Loop (Most Common)

A `for` loop goes through every item in the tuple automatically:

```python
thistuple = ("apple", "banana", "cherry")

for x in thistuple:
    print(x)
```

**Output:**
```
apple
banana
cherry
```

Line by line:
- `for x in thistuple:` — Python starts at index 0 and works through every item
- On the first pass: `x = "apple"`, then `print(x)` prints `apple`
- On the second pass: `x = "banana"`, then `print(x)` prints `banana`
- On the third pass: `x = "cherry"`, then `print(x)` prints `cherry`
- Loop ends automatically when all items have been visited

**Real-world example:** Loop through a tuple of student names and greet each one:

```python
students = ("Alice", "Bob", "Carol", "David")

for student in students:
    print(f"Good morning, {student}!")
```

**Output:**
```
Good morning, Alice!
Good morning, Bob!
Good morning, Carol!
Good morning, David!
```

---

### 6.2 Looping Through Index Numbers with `range()` and `len()`

Sometimes you need the **index number** as well as the item. Use `range()` combined with `len()`:

```python
thistuple = ("apple", "banana", "cherry")

for i in range(len(thistuple)):
    print(i, thistuple[i])
```

**Output:**
```
0 apple
1 banana
2 cherry
```

- `len(thistuple)` returns `3`
- `range(3)` generates the numbers `0, 1, 2`
- In each loop pass, `i` holds the current index number
- `thistuple[i]` gets the item at that index

**Real-world use:** When you need to print a numbered list:

```python
subjects = ("Math", "English", "Science", "History")

for i in range(len(subjects)):
    print(f"{i + 1}. {subjects[i]}")
```

**Output:**
```
1. Math
2. English
3. Science
4. History
```

(We use `i + 1` so the list starts at 1, not 0.)

---

### 6.3 Using a `while` Loop

A `while` loop keeps running as long as a condition is true. You can loop through a tuple this way:

```python
thistuple = ("apple", "banana", "cherry")
i = 0

while i < len(thistuple):
    print(thistuple[i])
    i = i + 1
```

**Output:**
```
apple
banana
cherry
```

- `i = 0` — start at the first index
- `while i < len(thistuple):` — keep looping as long as `i` is less than 3
- `thistuple[i]` — access the current item by index
- `i = i + 1` — move to the next index (very important! Without this, the loop runs forever)

> **Thinking Prompt:** What would happen if you forgot to write `i = i + 1`? The loop would keep printing `"apple"` forever — an **infinite loop**! Always make sure your `while` loop has a way to end.

---

## 🔍 Part 7: Joining Tuples

Sometimes you need to combine two or more tuples into one.

### 7.1 Using the `+` Operator

```python
tuple1 = ("a", "b", "c")
tuple2 = (1, 2, 3)

tuple3 = tuple1 + tuple2
print(tuple3)
```

**Output:**
```
('a', 'b', 'c', 1, 2, 3)
```

The `+` operator **concatenates** (joins) two tuples end-to-end and creates a new tuple.

Important: the original tuples `tuple1` and `tuple2` are unchanged. The result is stored in the new variable `tuple3`.

---

### 7.2 Using the `*` Operator (Repeating)

To repeat a tuple's content multiple times, use `*` with a number:

```python
fruits = ("apple", "banana", "cherry")
mytuple = fruits * 2
print(mytuple)
```

**Output:**
```
('apple', 'banana', 'cherry', 'apple', 'banana', 'cherry')
```

`fruits * 2` creates a new tuple that is the contents of `fruits` repeated twice.

**When is this useful?** If you need a default set of values duplicated, for example default settings repeated for multiple users or tiles in a game grid.

```python
# Create a row of 4 empty slots for a game board
empty_row = ("_",) * 4
print(empty_row)
```

**Output:**
```
('_', '_', '_', '_')
```

---

## 🔍 Part 8: Tuple Methods

Unlike lists (which have many methods like `.append()`, `.remove()`, `.sort()`), tuples have only **two built-in methods**. This makes sense — since you can't change a tuple, most list methods would be useless.

### 8.1 The `count()` Method

`count()` tells you how many times a specific value appears in the tuple.

**Syntax:** `tuple.count(value)`

```python
thistuple = (1, 3, 7, 8, 7, 5, 4, 6, 8, 5)
x = thistuple.count(5)
print(x)
```

**Output:**
```
2
```

The number `5` appears twice in the tuple, so `count(5)` returns `2`.

Another example:

```python
colors = ("red", "blue", "red", "green", "red")
print(colors.count("red"))
```

**Output:**
```
3
```

`"red"` appears 3 times.

**Real-world use:** Count how many times a student chose "Math" as their favourite subject from a survey response tuple:

```python
responses = ("Math", "English", "Math", "Science", "Math", "History")
math_count = responses.count("Math")
print(f"Math was chosen {math_count} times.")
```

**Output:**
```
Math was chosen 3 times.
```

---

### 8.2 The `index()` Method

`index()` tells you the **position (index)** of the first occurrence of a specified value.

**Syntax:** `tuple.index(value)`

```python
thistuple = (1, 3, 7, 8, 7, 5, 4, 6, 8, 5)
x = thistuple.index(8)
print(x)
```

**Output:**
```
3
```

The value `8` first appears at index 3. (There is another `8` at index 8, but `index()` only returns the **first** one.)

Another example:

```python
days = ("Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun")
print(days.index("Thu"))
```

**Output:**
```
3
```

**What happens if the value doesn't exist?**

```python
days = ("Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun")
print(days.index("Holiday"))  # ❌ This will raise an error
```

**Error:**
```
ValueError: tuple.index(x): x not in tuple
```

Always make sure the item exists before calling `index()`, or use `in` to check first:

```python
days = ("Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun")
target = "Wed"

if target in days:
    print(f"{target} is at index {days.index(target)}")
else:
    print(f"{target} was not found.")
```

**Output:**
```
Wed is at index 2
```

---

## 🛠️ Guided Practice Exercises

Now let's put everything together with exercises. Work through each one step by step.

---

### Exercise 1: Creating and Exploring a Tuple

**Objective:** Create a tuple and explore its properties.

**Scenario:** You are building a simple database for a school. Store the following days of the school week as a tuple.

**Steps:**

1. Create a tuple called `school_days` with the values: `"Monday"`, `"Tuesday"`, `"Wednesday"`, `"Thursday"`, `"Friday"`
2. Print the full tuple
3. Print the total number of days using `len()`
4. Print the first day (index 0)
5. Print the last day using negative indexing
6. Check if `"Saturday"` is in the tuple and print a result

**Solution:**

```python
# Step 1: Create the tuple
school_days = ("Monday", "Tuesday", "Wednesday", "Thursday", "Friday")

# Step 2: Print the full tuple
print(school_days)

# Step 3: Print the count
print("Number of school days:", len(school_days))

# Step 4: Print the first day
print("First day:", school_days[0])

# Step 5: Print the last day using negative indexing
print("Last day:", school_days[-1])

# Step 6: Check membership
if "Saturday" in school_days:
    print("Saturday is a school day.")
else:
    print("Saturday is NOT a school day.")
```

**Expected Output:**
```
('Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday')
Number of school days: 5
First day: Monday
Last day: Friday
Saturday is NOT a school day.
```

**Self-check Questions:**
- Why did we use round brackets to create the tuple?
- What would `school_days[-2]` print?
- What is the index of `"Wednesday"`?

---

### Exercise 2: Unpacking a Student Record

**Objective:** Practice tuple unpacking.

**Scenario:** A student's record is stored as a tuple containing their name, age, and score. Unpack it and display a formatted summary.

```python
student_record = ("Chidi", 16, 87)

# Unpack the tuple
(name, age, score) = student_record

# Display the information
print(f"Student Name: {name}")
print(f"Age: {age}")
print(f"Score: {score}")

# Determine grade
if score >= 90:
    grade = "A"
elif score >= 70:
    grade = "B"
elif score >= 50:
    grade = "C"
else:
    grade = "F"

print(f"Grade: {grade}")
```

**Expected Output:**
```
Student Name: Chidi
Age: 16
Score: 87
Grade: B
```

**What-if Challenge:** Change the score to `95` and run it again. Does the grade change correctly?

---

### Exercise 3: Looping Through a Tuple

**Objective:** Use loops to process all items in a tuple.

**Scenario:** You have a tuple of exam scores for a class. Find the total, average, highest, and lowest score.

```python
scores = (72, 85, 90, 61, 78, 95, 55, 88, 74, 82)

# Initialize variables
total = 0
highest = scores[0]
lowest = scores[0]

# Loop through scores
for score in scores:
    total += score              # add each score to total
    if score > highest:
        highest = score         # update highest if current is bigger
    if score < lowest:
        lowest = score          # update lowest if current is smaller

average = total / len(scores)

print(f"Total:   {total}")
print(f"Average: {average:.1f}")
print(f"Highest: {highest}")
print(f"Lowest:  {lowest}")
```

**Expected Output:**
```
Total:   780
Average: 78.0
Highest: 95
Lowest:  55
```

**What-if Challenge:** Add two more scores to the tuple — say `100` and `45` — and re-run. Do all four statistics update correctly?

---

### Exercise 4: Working with Tuple Methods

**Objective:** Practice `count()` and `index()`.

**Scenario:** A classroom survey asked 12 students to pick their favourite subject. The results are stored in a tuple. Analyse the responses.

```python
responses = ("Math", "English", "Math", "Science", "Math", "History",
             "English", "Math", "Science", "Math", "English", "Science")

# Count how many voted for each subject
subjects = ("Math", "English", "Science", "History")

print("=== Survey Results ===")
for subject in subjects:
    count = responses.count(subject)
    print(f"{subject}: {count} vote(s)")

# Find where "History" first appears
print(f"\nFirst 'History' vote is at position: {responses.index('History')}")
```

**Expected Output:**
```
=== Survey Results ===
Math: 5 vote(s)
English: 3 vote(s)
Science: 3 vote(s)
History: 1 vote(s)

First 'History' vote is at position: 5
```

---

## 🚀 Mini Project: Student Grade Book

Let's combine everything we've learned into a realistic mini project.

**Project Goal:** Build a simple grade book that stores student records as tuples, analyses the data, and prints a formatted report.

---

### Stage 1: Setup — Store Student Records

Each student record is a tuple: `(name, score)`.
All records together form a **tuple of tuples**.

```python
# Each inner tuple is (student_name, score)
grade_book = (
    ("Alice",   88),
    ("Bob",     72),
    ("Carol",   95),
    ("David",   61),
    ("Eve",     79),
    ("Frank",   55),
    ("Grace",   91),
    ("Henry",   68),
)

print("Grade Book Loaded:")
print(grade_book)
```

**Milestone Output:**
```
Grade Book Loaded:
(('Alice', 88), ('Bob', 72), ('Carol', 95), ('David', 61), ('Eve', 79), ('Frank', 55), ('Grace', 91), ('Henry', 68))
```

---

### Stage 2: Core Logic — Calculate Statistics

```python
total_score = 0
highest_score = 0
lowest_score = 100
top_student = ""
lowest_student = ""

for record in grade_book:
    name, score = record    # unpack each inner tuple

    total_score += score

    if score > highest_score:
        highest_score = score
        top_student = name

    if score < lowest_score:
        lowest_score = score
        lowest_student = name

average_score = total_score / len(grade_book)
```

---

### Stage 3: Grade Assignment

```python
def assign_grade(score):
    if score >= 90:
        return "A"
    elif score >= 70:
        return "B"
    elif score >= 50:
        return "C"
    else:
        return "F"
```

---

### Stage 4: Final Output — Print the Report

```python
print("=" * 40)
print("      STUDENT GRADE REPORT")
print("=" * 40)
print(f"{'NAME':<12} {'SCORE':>6} {'GRADE':>6}")
print("-" * 40)

for record in grade_book:
    name, score = record
    grade = assign_grade(score)
    print(f"{name:<12} {score:>6} {grade:>6}")

print("-" * 40)
print(f"\nClass Average:  {average_score:.1f}")
print(f"Top Student:    {top_student} ({highest_score})")
print(f"Needs Support:  {lowest_student} ({lowest_score})")
print("=" * 40)
```

**Complete Final Output:**
```
========================================
      STUDENT GRADE REPORT
========================================
NAME          SCORE  GRADE
----------------------------------------
Alice            88      B
Bob              72      B
Carol            95      A
David            61      C
Eve              79      B
Frank            55      C
Grace            91      A
Henry            68      C
----------------------------------------

Class Average:  76.1
Top Student:    Carol (95)
Needs Support:  Frank (55)
========================================
```

**Reflection Questions:**
- Why did we store the records as tuples instead of lists? (Hint: student names and scores shouldn't be accidentally modified)
- What would happen if we added a third value to each record, like `("Alice", 88, "Present")`? How would you change the unpacking code?
- Can you extend this project to also count how many students got each grade using `count()`?

**Optional Extension:** Add an attendance column to each tuple record and count how many students were "Present" using `count()`.

---

## ⚠️ Common Beginner Mistakes

### Mistake 1: Forgetting the Comma in a One-Item Tuple

```python
# ❌ WRONG — this is just a string
single = ("hello")
print(type(single))     # <class 'str'>

# ✅ CORRECT — add the trailing comma
single = ("hello",)
print(type(single))     # <class 'tuple'>
```

**Why it happens:** Brackets in math and in Python function calls are used for grouping, not for creating tuples. The comma is what tells Python "this is a tuple".

---

### Mistake 2: Trying to Directly Modify a Tuple

```python
# ❌ WRONG
my_tuple = ("apple", "banana", "cherry")
my_tuple[1] = "kiwi"   # TypeError!

# ✅ CORRECT — use the convert-change-convert workaround
my_list = list(my_tuple)
my_list[1] = "kiwi"
my_tuple = tuple(my_list)
print(my_tuple)     # ('apple', 'kiwi', 'cherry')
```

---

### Mistake 3: Forgetting That Indexing Starts at 0

```python
fruits = ("apple", "banana", "cherry")

# ❌ WRONG — trying to get the "first" item with index 1
print(fruits[1])   # banana  ← this is actually the SECOND item!

# ✅ CORRECT — first item is at index 0
print(fruits[0])   # apple
```

---

### Mistake 4: Going Out of Range

```python
fruits = ("apple", "banana", "cherry")

# ❌ WRONG — there are only 3 items (indices 0, 1, 2)
print(fruits[3])   # IndexError: tuple index out of range

# ✅ CORRECT — use len() to check before accessing
print(len(fruits))   # 3
print(fruits[2])     # cherry (last valid index)
```

---

### Mistake 5: Mismatched Unpacking Variables

```python
fruits = ("apple", "banana", "cherry")

# ❌ WRONG — 2 variables for 3 items (without *)
(a, b) = fruits    # ValueError: too many values to unpack

# ✅ CORRECT — match the count
(a, b, c) = fruits
print(a, b, c)     # apple banana cherry

# ✅ OR use * to collect extras
(a, *rest) = fruits
print(a)      # apple
print(rest)   # ['banana', 'cherry']
```

---

### Mistake 6: Concatenating a Tuple with a Non-Tuple

```python
t1 = ("apple", "banana")

# ❌ WRONG — can't add a tuple and a list
result = t1 + ["cherry"]   # TypeError!

# ✅ CORRECT — both must be tuples
result = t1 + ("cherry",)
print(result)   # ('apple', 'banana', 'cherry')
```

---

## 💭 Reflection Questions

Take a moment to test your understanding:

1. What is the key difference between a **tuple** and a **list** in Python?
2. Why would a programmer intentionally use a tuple instead of a list?
3. If `t = (10, 20, 30, 40, 50)`, what does `t[1:4]` return?
4. How would you unpack `(latitude, longitude) = (6.5244, 3.3792)` — what values do the variables get?
5. Given `scores = (85, 90, 85, 70, 85)`, what does `scores.count(85)` return?
6. What does `scores.index(70)` return for the same tuple above?
7. If you join `("a", "b")` and `("c", "d")` using `+`, what is the result?
8. What happens when you multiply a tuple: `("go",) * 3`?
9. In the statement `(first, *rest) = (1, 2, 3, 4, 5)`, what is the value of `rest`?
10. Name one real-world situation where you would use a tuple instead of a list.

---

## ✅ Completion Checklist

Before you move on to the next lesson, make sure you can:

- [ ] Create a tuple with multiple items using round brackets
- [ ] Create a single-item tuple correctly (with the trailing comma)
- [ ] Access a specific tuple item using its positive index
- [ ] Access items using negative indexing (from the end)
- [ ] Slice a range of items from a tuple
- [ ] Check if an item exists using `in`
- [ ] Modify tuple values using the convert-change-convert workaround
- [ ] Add items to a tuple by concatenation or list conversion
- [ ] Remove items from a tuple using list conversion
- [ ] Unpack a tuple into multiple variables
- [ ] Use `*` to collect remaining values when unpacking
- [ ] Loop through a tuple using a `for` loop
- [ ] Loop with index using `range()` and `len()`
- [ ] Loop using a `while` loop
- [ ] Join two tuples with `+`
- [ ] Repeat a tuple with `*`
- [ ] Use `count()` to count occurrences of a value
- [ ] Use `index()` to find the first position of a value
- [ ] Complete the mini grade book project

---

## 📋 Lesson Summary

Here is everything you learned in Lesson 12, condensed for quick review:

**What is a tuple?**
A tuple is an ordered, immutable (unchangeable) collection of items written with round brackets `( )`. It allows duplicate values and can hold any data type.

**Creating tuples:**
- Multi-item: `t = ("a", "b", "c")`
- One-item: `t = ("a",)` ← comma is required!
- Using constructor: `t = tuple(["a", "b", "c"])`

**Accessing items:**
- Positive index: `t[0]` → first item
- Negative index: `t[-1]` → last item
- Slice: `t[1:3]` → items at index 1 and 2
- Membership: `"a" in t` → True or False

**Updating (workaround):**
```python
t = list(t)   # convert to list
# ... make changes ...
t = tuple(t)  # convert back
```

**Unpacking:**
```python
(a, b, c) = ("x", "y", "z")     # basic
(first, *rest) = (1, 2, 3, 4)   # with asterisk
```

**Looping:**
```python
for item in t:            # direct loop
for i in range(len(t)):   # loop with index
```

**Joining:**
```python
t3 = t1 + t2     # concatenate
t3 = t1 * 3      # repeat
```

**Methods:**
- `t.count(value)` — how many times does `value` appear?
- `t.index(value)` — what is the first index of `value`?

**When to use tuples (real-world):**
- Storing fixed data: GPS coordinates, RGB colour codes, database records
- Returning multiple values from a function
- Protecting data from accidental modification
- As dictionary keys (lists can't be dict keys; tuples can)

---

*You are now ready for Lesson 13: Python Sets!*
