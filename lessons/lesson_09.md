---
render_with_liquid: false
title: "Lesson 09 – Python Tuples"
nav_order: 9
---

# Lesson 09 – Python Tuples

---

## Lesson Introduction

Welcome to Lesson 09! In this lesson you will learn about **tuples** — one of Python's most useful built-in data structures. You will discover what a tuple is, why it exists, how to create one, how to access and work with items inside it, how to loop through it, how to join tuples together, and which built-in methods belong to tuples.

By the end of this lesson you will be able to:

- Create tuples with any kind of data
- Access items using index numbers and slicing
- Update a tuple using Python's approved workarounds
- Unpack a tuple into individual variables
- Loop through tuples using `for` and `while` loops
- Join and multiply tuples
- Use the two tuple methods: `count()` and `index()`
- Build a real-world mini project using tuples

No prior knowledge of tuples is required. All you need is a basic understanding of Python variables and the `print()` function. If you have done the lessons on Lists, you will find tuples very familiar.

---

## Prerequisite Concepts

Before diving in, let's make sure you understand two foundational ideas.

### What is a Variable?

A variable is a name you give to a piece of data so Python can remember it.

```python
name = "Alice"
age  = 25
print(name)   # Alice
print(age)    # 25
```

### What is a List? (A quick refresher)

A list is an ordered collection of items written in **square brackets**:

```python
fruits = ["apple", "banana", "cherry"]
print(fruits)  # ['apple', 'banana', 'cherry']
```

Lists are **changeable** — you can add, remove, or update items freely. A tuple is similar but with one key difference: it is **unchangeable** (also called *immutable*). You will learn exactly what that means — and why it is useful — in the sections below.

---

## Section 1 – What Is a Tuple?

### The Concept

Imagine you are writing the GPS coordinates of your city. Latitude and longitude are fixed — they don't randomly change. Storing them in a tuple makes perfect sense, because a tuple **locks the data in place** so it cannot be accidentally modified.

> **Think of a tuple like a sealed envelope.** Once you put things inside and seal it, nobody can add, remove, or swap the contents. You can still read what is inside, but the contents are protected.

### The Technical Definition

A **tuple** is a collection which is:

- **Ordered** — the items have a fixed position (first, second, third…)
- **Unchangeable (immutable)** — once created, you cannot add, remove, or change items
- **Allows duplicate values** — the same value can appear more than once
- Written with **round brackets** `( )`

### Syntax

```python
my_tuple = ("item1", "item2", "item3")
```

### Your First Tuple

```python
mytuple = ("apple", "banana", "cherry")
print(mytuple)
```

**Expected Output:**
```
('apple', 'banana', 'cherry')
```

Notice the output shows **round brackets** `( )`. That tells you it is a tuple, not a list.

---

## Section 2 – Tuple Properties in Detail

### 2.1 Ordered

The items in a tuple are stored in a specific order, and that order never changes. "apple" will always be at position 0, "banana" at position 1, and so on.

```python
thistuple = ("apple", "banana", "cherry")
print(thistuple[0])  # Always apple
print(thistuple[1])  # Always banana
```

**Expected Output:**
```
apple
banana
```

### 2.2 Unchangeable (Immutable)

You cannot change, add, or remove items after the tuple has been created.

```python
thistuple = ("apple", "banana", "cherry")
thistuple[1] = "kiwi"   # This will cause an ERROR
```

**Expected Output (Error):**
```
TypeError: 'tuple' object does not support item assignment
```

> **Why is immutability useful?** It protects important data. For example, if your program stores the days of the week as a tuple, you never want someone accidentally changing "Monday" to "Holiday". Immutability also makes tuples slightly faster than lists in Python, which matters in performance-critical code.

### 2.3 Allows Duplicate Values

Since tuples are indexed, items can be repeated.

```python
thistuple = ("apple", "banana", "cherry", "apple", "cherry")
print(thistuple)
```

**Expected Output:**
```
('apple', 'banana', 'cherry', 'apple', 'cherry')
```

> **Think prompt:** Why would you want duplicates? Imagine recording the results of 5 coin tosses: `("heads", "tails", "heads", "heads", "tails")`. Duplicates are natural here.

---

## Section 3 – Creating Tuples

### 3.1 Standard Way — Round Brackets

```python
thistuple = ("apple", "banana", "cherry")
print(thistuple)
```

**Expected Output:**
```
('apple', 'banana', 'cherry')
```

### 3.2 Using the `tuple()` Constructor

You can also create a tuple using the built-in `tuple()` function. Notice the **double round brackets** — the outer pair belongs to the function call, the inner pair belongs to the tuple.

```python
thistuple = tuple(("apple", "banana", "cherry"))
print(thistuple)
```

**Expected Output:**
```
('apple', 'banana', 'cherry')
```

### 3.3 Creating a Tuple with Only One Item ⚠️

This is a famous beginner trap! If you write one item without a trailing comma, Python will NOT treat it as a tuple — it will treat it as just a string wrapped in brackets.

```python
# WRONG — this is NOT a tuple
thistuple = ("apple")
print(type(thistuple))   # <class 'str'>

# CORRECT — add a comma after the item
thistuple = ("apple",)
print(type(thistuple))   # <class 'tuple'>
```

**Expected Output:**
```
<class 'str'>
<class 'tuple'>
```

> The trailing comma is the signal to Python: "Yes, I want a tuple, not just a parenthesized expression."

### 3.4 Tuples Can Hold Any Data Type

```python
tuple1 = ("apple", "banana", "cherry")    # strings
tuple2 = (1, 5, 7, 9, 3)                 # integers
tuple3 = (True, False, False)             # booleans
mixed  = ("abc", 34, True, 40, "male")   # mixed types
```

You can store anything in a tuple — text, numbers, booleans, or a mix of all of them.

### 3.5 Checking the Data Type

```python
mytuple = ("apple", "banana", "cherry")
print(type(mytuple))
```

**Expected Output:**
```
<class 'tuple'>
```

`type()` is a built-in Python function that tells you what kind of object something is. The result `<class 'tuple'>` confirms it is a tuple.

### 3.6 Finding the Length of a Tuple

```python
thistuple = ("apple", "banana", "cherry")
print(len(thistuple))
```

**Expected Output:**
```
3
```

`len()` counts the number of items inside the tuple.

---

## Section 4 – The Four Python Collection Types (Comparison)

Python has four built-in collection types. Knowing the differences helps you pick the right one for each job.

| Collection | Ordered? | Changeable? | Allows Duplicates? | Written With |
|------------|----------|-------------|-------------------|--------------|
| **List** | ✅ Yes | ✅ Yes | ✅ Yes | `[ ]` |
| **Tuple** | ✅ Yes | ❌ No | ✅ Yes | `( )` |
| **Set** | ❌ No | ❌ Items fixed* | ❌ No | `{ }` |
| **Dictionary** | ✅ Yes (3.7+) | ✅ Yes | ❌ No (keys) | `{key: value}` |

*You can add/remove set items, but individual items cannot be changed.

**When to use a tuple instead of a list:**
- When your data should never change (e.g., days of the week, GPS coordinates, RGB color values)
- When you want a small performance boost
- When you want to signal to other programmers: "Do not modify this data"

---

## Section 5 – Accessing Tuple Items

### 5.1 Index Numbers

Every item in a tuple has a numbered position called an **index**. Counting starts at **0**, not 1.

```
Tuple:  ("apple",  "banana",  "cherry")
Index:      0          1          2
```

To access an item, write the tuple name followed by the index in square brackets `[ ]`:

```python
thistuple = ("apple", "banana", "cherry")
print(thistuple[0])   # first item
print(thistuple[1])   # second item
print(thistuple[2])   # third item
```

**Expected Output:**
```
apple
banana
cherry
```

> **Think prompt:** What happens if you try `thistuple[3]` on a tuple of 3 items? Try it! You will get an `IndexError` because there is no item at position 3.

### 5.2 Negative Indexing

Negative indexing lets you count **from the end** of the tuple. `-1` is the last item, `-2` is the second-to-last, and so on.

```
Tuple:  ("apple",  "banana",  "cherry")
Index:     -3         -2         -1
```

```python
thistuple = ("apple", "banana", "cherry")
print(thistuple[-1])   # last item
print(thistuple[-2])   # second-to-last item
```

**Expected Output:**
```
cherry
banana
```

> Negative indexing is very handy when you don't know how long a tuple is but you always need the last item.

### 5.3 Slicing — Grabbing a Range of Items

You can grab multiple items at once by specifying a **start** and **end** index separated by a colon `:`.

**Important rule:** The start index is **included**, the end index is **excluded**.

```python
thistuple = ("apple", "banana", "cherry", "orange", "kiwi", "melon", "mango")
print(thistuple[2:5])
```

This says: "Give me items starting at index 2 (cherry), up to but not including index 5 (kiwi)."

**Expected Output:**
```
('cherry', 'orange', 'kiwi')
```

**Leaving out the start index** → Python starts from the very beginning:

```python
print(thistuple[:4])
```

**Expected Output:**
```
('apple', 'banana', 'cherry', 'orange')
```

**Leaving out the end index** → Python goes all the way to the end:

```python
print(thistuple[2:])
```

**Expected Output:**
```
('cherry', 'orange', 'kiwi', 'melon', 'mango')
```

### 5.4 Negative Index Slicing

You can combine negative indexes with slicing:

```python
thistuple = ("apple", "banana", "cherry", "orange", "kiwi", "melon", "mango")
print(thistuple[-4:-1])
```

This grabs items from index `-4` (orange) up to but not including index `-1` (mango).

**Expected Output:**
```
('orange', 'kiwi', 'melon')
```

### 5.5 Checking if an Item Exists

Use the `in` keyword to check whether a specific value is inside a tuple:

```python
thistuple = ("apple", "banana", "cherry")
if "apple" in thistuple:
    print("Yes, 'apple' is in the fruits tuple")
```

**Expected Output:**
```
Yes, 'apple' is in the fruits tuple
```

`in` returns `True` if the item is found, and `False` if it is not.

```python
# Second example
thistuple = ("apple", "banana", "cherry")
if "mango" in thistuple:
    print("Found!")
else:
    print("Not found.")
```

**Expected Output:**
```
Not found.
```

---

## Section 6 – Updating Tuples (Workarounds)

Tuples are immutable — you cannot directly change, add, or remove items. But Python gives you approved workarounds.

### 6.1 Changing a Value

**The workaround:** Convert the tuple to a list → make your changes → convert it back to a tuple.

```python
x = ("apple", "banana", "cherry")
y = list(x)        # Step 1: convert tuple to list
y[1] = "kiwi"      # Step 2: change the item
x = tuple(y)       # Step 3: convert list back to tuple

print(x)
```

**Expected Output:**
```
('apple', 'kiwi', 'cherry')
```

**Line-by-line breakdown:**
- `y = list(x)` — creates a new list `['apple', 'banana', 'cherry']`
- `y[1] = "kiwi"` — replaces position 1 (banana) with kiwi
- `x = tuple(y)` — converts the list back into a tuple and reassigns it to `x`

### 6.2 Adding Items

**Method 1: Convert to list, append, convert back**

```python
thistuple = ("apple", "banana", "cherry")
y = list(thistuple)
y.append("orange")
thistuple = tuple(y)
print(thistuple)
```

**Expected Output:**
```
('apple', 'banana', 'cherry', 'orange')
```

**Method 2: Add two tuples together (concatenation)**

You can stick two tuples together using the `+` operator. To add just one new item, create a single-item tuple first (remember the trailing comma!):

```python
thistuple = ("apple", "banana", "cherry")
y = ("orange",)          # single-item tuple — comma is essential!
thistuple += y           # += means: thistuple = thistuple + y

print(thistuple)
```

**Expected Output:**
```
('apple', 'banana', 'cherry', 'orange')
```

### 6.3 Removing Items

**The workaround:** Convert to list → remove → convert back.

```python
thistuple = ("apple", "banana", "cherry")
y = list(thistuple)
y.remove("apple")
thistuple = tuple(y)
print(thistuple)
```

**Expected Output:**
```
('banana', 'cherry')
```

### 6.4 Deleting the Whole Tuple

If you want to destroy the tuple entirely, use the `del` keyword:

```python
thistuple = ("apple", "banana", "cherry")
del thistuple
print(thistuple)   # This will raise an error — the tuple no longer exists
```

**Expected Output (Error):**
```
NameError: name 'thistuple' is not defined
```

> After `del`, the variable no longer exists. Trying to use it will cause a `NameError`.

---

## Section 7 – Unpacking Tuples

### 7.1 What is Packing?

When you create a tuple by assigning values to it, that is called **packing**:

```python
fruits = ("apple", "banana", "cherry")
```

You are "packing" three fruits into one variable.

### 7.2 What is Unpacking?

**Unpacking** is the reverse: you extract the values back out into separate variables.

```python
fruits = ("apple", "banana", "cherry")

(green, yellow, red) = fruits

print(green)    # apple
print(yellow)   # banana
print(red)      # cherry
```

**Expected Output:**
```
apple
banana
cherry
```

**Line-by-line breakdown:**
- `(green, yellow, red) = fruits` — Python reads the tuple from left to right and assigns each item to the matching variable
- `green` gets "apple", `yellow` gets "banana", `red` gets "cherry"

> **Important:** The number of variables on the left must match the number of items in the tuple. If they don't match, Python will raise a `ValueError` — unless you use the asterisk trick below.

### 7.3 Unpacking with an Asterisk `*` (Collect Extras)

What if you have more items than variables? Use `*` to collect the "extra" items into a list.

**Example 1 — Collect extras at the end:**

```python
fruits = ("apple", "banana", "cherry", "strawberry", "raspberry")

(green, yellow, *red) = fruits

print(green)    # apple
print(yellow)   # banana
print(red)      # ['cherry', 'strawberry', 'raspberry']
```

**Expected Output:**
```
apple
banana
['cherry', 'strawberry', 'raspberry']
```

`*red` tells Python: "Assign the first two items to `green` and `yellow`, and collect everything else into `red` as a list."

**Example 2 — Collect extras in the middle:**

```python
fruits = ("apple", "mango", "papaya", "pineapple", "cherry")

(green, *tropic, red) = fruits

print(green)    # apple
print(tropic)   # ['mango', 'papaya', 'pineapple']
print(red)      # cherry
```

**Expected Output:**
```
apple
['mango', 'papaya', 'pineapple']
cherry
```

Python assigns the first item to `green`, the last item to `red`, and collects everything in between into `tropic`.

> **Real-world use:** In data science, you might have a row of data like `(name, age, score1, score2, score3, final_score)`. You can unpack: `(name, age, *scores, final) = row` to easily separate the identifier, intermediate scores, and final score.

---

## Section 8 – Looping Through Tuples

### 8.1 The `for` Loop

The simplest way to visit every item in a tuple one by one:

```python
thistuple = ("apple", "banana", "cherry")
for x in thistuple:
    print(x)
```

**Expected Output:**
```
apple
banana
cherry
```

**Line-by-line breakdown:**
- `for x in thistuple:` — on each round of the loop, Python takes the next item from the tuple and stores it in `x`
- `print(x)` — prints the current item

### 8.2 Looping Using Index Numbers

Sometimes you need both the item AND its position. Use `range()` and `len()` together:

```python
thistuple = ("apple", "banana", "cherry")
for i in range(len(thistuple)):
    print(thistuple[i])
```

**Expected Output:**
```
apple
banana
cherry
```

**Breakdown:**
- `len(thistuple)` returns `3`
- `range(3)` produces the sequence `0, 1, 2`
- On each loop, `i` takes the value `0`, then `1`, then `2`
- `thistuple[i]` accesses the item at that index

This is useful when you need to know the position of each item, for example:

```python
thistuple = ("apple", "banana", "cherry")
for i in range(len(thistuple)):
    print(f"Item {i}: {thistuple[i]}")
```

**Expected Output:**
```
Item 0: apple
Item 1: banana
Item 2: cherry
```

### 8.3 Using a `while` Loop

A `while` loop keeps going as long as a condition is `True`. Here, we keep looping as long as `i` is less than the length of the tuple:

```python
thistuple = ("apple", "banana", "cherry")
i = 0
while i < len(thistuple):
    print(thistuple[i])
    i = i + 1
```

**Expected Output:**
```
apple
banana
cherry
```

**Breakdown:**
- `i = 0` — start at index 0
- `while i < len(thistuple):` — keep going while `i` is less than 3
- `print(thistuple[i])` — print the current item
- `i = i + 1` — move to the next index (this is essential — without it, the loop runs forever!)

> **Think prompt:** What would happen if you forgot `i = i + 1`? The loop would run forever printing "apple". Always make sure a while loop has a way to stop.

---

## Section 9 – Joining Tuples

### 9.1 Concatenating with `+`

You can combine two or more tuples into one using the `+` operator:

```python
tuple1 = ("a", "b", "c")
tuple2 = (1, 2, 3)

tuple3 = tuple1 + tuple2
print(tuple3)
```

**Expected Output:**
```
('a', 'b', 'c', 1, 2, 3)
```

The items from `tuple1` appear first, then the items from `tuple2`. The original tuples are unchanged.

**Second example:**

```python
names = ("Alice", "Bob")
scores = (95, 87)

combined = names + scores
print(combined)
```

**Expected Output:**
```
('Alice', 'Bob', 95, 87)
```

### 9.2 Multiplying with `*`

You can repeat the contents of a tuple by multiplying it by a number:

```python
fruits = ("apple", "banana", "cherry")
mytuple = fruits * 2

print(mytuple)
```

**Expected Output:**
```
('apple', 'banana', 'cherry', 'apple', 'banana', 'cherry')
```

The entire tuple is repeated twice. This is useful when you need to create a repeating pattern quickly.

**Another example:**

```python
signal = ("red", "green", "blue")
repeated = signal * 3
print(repeated)
```

**Expected Output:**
```
('red', 'green', 'blue', 'red', 'green', 'blue', 'red', 'green', 'blue')
```

> **Real-world use:** In image processing, RGB color values are stored as tuples like `(255, 0, 0)` for red. If you needed to create a row of 5 identical pixels, you could write `pixel = (255, 0, 0)` then `row = pixel * 5`.

---

## Section 10 – Tuple Methods

Python tuples have only **two built-in methods**. This is intentional — since you can't change a tuple, most of the list methods (append, remove, sort…) simply don't exist for tuples.

### 10.1 `count()` — How Many Times Does a Value Appear?

`count(value)` returns how many times a specific value appears in the tuple.

```python
thistuple = ("apple", "banana", "cherry", "apple", "banana", "apple")
result = thistuple.count("apple")
print(result)
```

**Expected Output:**
```
3
```

"apple" appears 3 times.

**Second example:**

```python
numbers = (1, 2, 3, 2, 4, 2, 5)
print(numbers.count(2))    # How many 2s?
print(numbers.count(9))    # How many 9s?
```

**Expected Output:**
```
3
0
```

If the value is not in the tuple, `count()` returns `0` — it does not cause an error.

> **Real-world use:** Imagine a tuple of survey responses: `responses = ("yes", "no", "yes", "yes", "no")`. You can count how many people said "yes" with `responses.count("yes")`.

### 10.2 `index()` — Where is This Value?

`index(value)` searches the tuple for a value and returns the **position (index)** of its **first** occurrence.

```python
thistuple = ("apple", "banana", "cherry")
result = thistuple.index("cherry")
print(result)
```

**Expected Output:**
```
2
```

"cherry" is at position 2.

**Second example:**

```python
thistuple = ("apple", "banana", "cherry", "apple")
print(thistuple.index("apple"))   # Returns position of FIRST "apple"
```

**Expected Output:**
```
0
```

Even though "apple" appears twice (at positions 0 and 3), `index()` only returns the position of the first one.

> **Warning:** If you search for a value that is NOT in the tuple, Python raises a `ValueError`. Always make sure the value exists first (use `in` to check).

```python
thistuple = ("apple", "banana", "cherry")
if "mango" in thistuple:
    print(thistuple.index("mango"))
else:
    print("mango is not in the tuple")
```

**Expected Output:**
```
mango is not in the tuple
```

---

## Section 11 – Guided Practice Exercises

### Exercise 1 – Warm-Up: Student Record Tuple

**Objective:** Create and access a tuple representing a student record.

**Scenario:** A school stores each student's information as a tuple: name, age, grade, and city.

**Steps:**

1. Create a tuple called `student` with these values: `("Amara", 17, "Grade 11", "Lagos")`
2. Print the full tuple
3. Print just the student's name (index 0)
4. Print the city using negative indexing
5. Print the length of the tuple

**Your code:**

```python
student = ("Amara", 17, "Grade 11", "Lagos")

print(student)
print(student[0])
print(student[-1])
print(len(student))
```

**Expected Output:**
```
('Amara', 17, 'Grade 11', 'Lagos')
Amara
Lagos
4
```

**Self-check Questions:**
- What index would give you "Grade 11"?
- What would `student[-2]` return?

---

### Exercise 2 – Slice and Check

**Objective:** Practice slicing and membership checking.

**Scenario:** A weekly weather summary is stored as a tuple.

```python
weather = ("Sunny", "Cloudy", "Rainy", "Sunny", "Windy", "Cloudy", "Sunny")
```

**Tasks:**
1. Print the first three days
2. Print the last two days using negative slicing
3. Check if "Rainy" is in the tuple and print a message

```python
weather = ("Sunny", "Cloudy", "Rainy", "Sunny", "Windy", "Cloudy", "Sunny")

print(weather[:3])
print(weather[-2:])

if "Rainy" in weather:
    print("Pack an umbrella — rain is expected this week!")
```

**Expected Output:**
```
('Sunny', 'Cloudy', 'Rainy')
('Cloudy', 'Sunny')
Pack an umbrella — rain is expected this week!
```

**What-if challenge:** What would `weather[1:6:2]` return? (Hint: the third number in slicing is the "step".)

---

### Exercise 3 – Unpacking in Action

**Objective:** Unpack a tuple representing a product listing.

**Scenario:** An e-commerce database stores product info as a tuple.

```python
product = ("Wireless Headphones", "Electronics", 49.99, "In Stock")
```

**Tasks:**
1. Unpack all four values into separate variables: `name`, `category`, `price`, `status`
2. Print a formatted summary

```python
product = ("Wireless Headphones", "Electronics", 49.99, "In Stock")

(name, category, price, status) = product

print(f"Product: {name}")
print(f"Category: {category}")
print(f"Price: ${price}")
print(f"Status: {status}")
```

**Expected Output:**
```
Product: Wireless Headphones
Category: Electronics
Price: $49.99
Status: In Stock
```

---

### Exercise 4 – Loop and Summarise

**Objective:** Loop through a tuple to calculate a total.

**Scenario:** A student's exam scores for the semester are stored in a tuple.

```python
scores = (72, 85, 91, 68, 79, 88)
```

**Tasks:**
1. Loop through the tuple and print each score
2. Calculate and print the total
3. Calculate and print the average

```python
scores = (72, 85, 91, 68, 79, 88)

total = 0

for score in scores:
    print(f"Score: {score}")
    total += score

average = total / len(scores)
print(f"\nTotal: {total}")
print(f"Average: {average:.1f}")
```

**Expected Output:**
```
Score: 72
Score: 85
Score: 91
Score: 68
Score: 79
Score: 88

Total: 483
Average: 80.5
```

---

### Exercise 5 – Using `count()` and `index()`

**Objective:** Use both tuple methods on a real dataset.

**Scenario:** Survey responses from 10 people who were asked their favourite season.

```python
responses = ("Summer", "Winter", "Summer", "Spring", "Summer",
             "Autumn", "Winter", "Summer", "Spring", "Winter")
```

**Tasks:**
1. Count how many people chose "Summer"
2. Find the position of the first "Winter"
3. Count how many chose "Autumn"

```python
responses = ("Summer", "Winter", "Summer", "Spring", "Summer",
             "Autumn", "Winter", "Summer", "Spring", "Winter")

summer_votes = responses.count("Summer")
first_winter  = responses.index("Winter")
autumn_votes  = responses.count("Autumn")

print(f"Summer votes: {summer_votes}")
print(f"First Winter at index: {first_winter}")
print(f"Autumn votes: {autumn_votes}")
```

**Expected Output:**
```
Summer votes: 4
First Winter at index: 1
Autumn votes: 1
```

---

## Section 12 – Mini Project: Student Grade Report

This mini project combines everything you have learned into a realistic program.

### Project Scenario

You are building a simple student grade report system for a school. Each student's record is stored as a tuple. The program should display a formatted report, calculate the average, find the highest and lowest scores, and determine the student's grade.

### Stage 1 – Setup the Data

```python
# Student record tuple: (name, student_id, subject_scores)
# Subject scores are stored as a nested tuple
student_name = "Chidi Okafor"
student_id   = "STU-2024-007"
scores       = (78, 85, 92, 67, 88, 74, 91)
subjects     = ("Mathematics", "English", "Physics", "Chemistry",
                "Biology", "History", "Computer Science")
```

**Milestone check:** Print the student name and the number of subjects:

```python
print(f"Student: {student_name}")
print(f"Number of subjects: {len(scores)}")
```

**Expected Output:**
```
Student: Chidi Okafor
Number of subjects: 7
```

### Stage 2 – Build the Core Report

```python
student_name = "Chidi Okafor"
student_id   = "STU-2024-007"
scores       = (78, 85, 92, 67, 88, 74, 91)
subjects     = ("Mathematics", "English", "Physics", "Chemistry",
                "Biology", "History", "Computer Science")

print("=" * 45)
print(f"  STUDENT GRADE REPORT")
print(f"  Name: {student_name}")
print(f"  ID:   {student_id}")
print("=" * 45)

total = 0
for i in range(len(subjects)):
    print(f"  {subjects[i]:<22}: {scores[i]}")
    total += scores[i]
```

**Expected Output:**
```
=============================================
  STUDENT GRADE REPORT
  Name: Chidi Okafor
  ID:   STU-2024-007
=============================================
  Mathematics           : 78
  English               : 85
  Physics               : 92
  Chemistry             : 67
  Biology               : 88
  History               : 74
  Computer Science      : 91
```

### Stage 3 – Enhancements (Statistics)

```python
# After the loop, add:
average   = total / len(scores)

# Sorting by converting to a list temporarily
scores_list = list(scores)
scores_list.sort()
lowest  = scores_list[0]
highest = scores_list[-1]

print("-" * 45)
print(f"  Total Score : {total}")
print(f"  Average     : {average:.1f}")
print(f"  Highest     : {highest}")
print(f"  Lowest      : {lowest}")
```

**Expected Output:**
```
---------------------------------------------
  Total Score : 575
  Average     : 82.1
  Highest     : 92
  Lowest      : 67
```

### Stage 4 – Final Grade Assignment

```python
if average >= 90:
    grade = "A"
elif average >= 80:
    grade = "B"
elif average >= 70:
    grade = "C"
elif average >= 60:
    grade = "D"
else:
    grade = "F"

print(f"  Final Grade : {grade}")
print("=" * 45)
```

**Expected Output:**
```
  Final Grade : B
=============================================
```

### Full Project Code (All Stages Combined)

```python
student_name = "Chidi Okafor"
student_id   = "STU-2024-007"
scores       = (78, 85, 92, 67, 88, 74, 91)
subjects     = ("Mathematics", "English", "Physics", "Chemistry",
                "Biology", "History", "Computer Science")

print("=" * 45)
print("  STUDENT GRADE REPORT")
print(f"  Name: {student_name}")
print(f"  ID:   {student_id}")
print("=" * 45)

total = 0
for i in range(len(subjects)):
    print(f"  {subjects[i]:<22}: {scores[i]}")
    total += scores[i]

average   = total / len(scores)
scores_list = list(scores)
scores_list.sort()
lowest  = scores_list[0]
highest = scores_list[-1]

print("-" * 45)
print(f"  Total Score : {total}")
print(f"  Average     : {average:.1f}")
print(f"  Highest     : {highest}")
print(f"  Lowest      : {lowest}")

if average >= 90:
    grade = "A"
elif average >= 80:
    grade = "B"
elif average >= 70:
    grade = "C"
elif average >= 60:
    grade = "D"
else:
    grade = "F"

print(f"  Final Grade : {grade}")
print("=" * 45)
```

**Full Expected Output:**
```
=============================================
  STUDENT GRADE REPORT
  Name: Chidi Okafor
  ID:   STU-2024-007
=============================================
  Mathematics           : 78
  English               : 85
  Physics               : 92
  Chemistry             : 67
  Biology               : 88
  History               : 74
  Computer Science      : 91
---------------------------------------------
  Total Score : 575
  Average     : 82.1
  Highest     : 92
  Lowest      : 67
  Final Grade : B
=============================================
```

**Reflection Questions:**
- Why was a tuple a good choice for `scores` and `subjects` in this project?
- How would you modify the project to handle a second student?
- What would happen if you stored the scores in a list instead?

**Optional Extension:** Add a feature that prints the subject where the student scored the highest, and the subject where they scored the lowest.

---

## Section 13 – Common Beginner Mistakes

### Mistake 1 – Forgetting the Trailing Comma in a One-Item Tuple

```python
# WRONG
t = ("hello")
print(type(t))   # <class 'str'>  ← Not a tuple!

# CORRECT
t = ("hello",)
print(type(t))   # <class 'tuple'>  ← Correct!
```

**Fix:** Always add a comma after the single item when creating a one-item tuple.

---

### Mistake 2 – Trying to Change a Tuple Directly

```python
# WRONG
t = ("apple", "banana", "cherry")
t[0] = "mango"   # TypeError!
```

**Fix:** Convert to a list first, make changes, then convert back:

```python
t = list(t)
t[0] = "mango"
t = tuple(t)
print(t)   # ('mango', 'banana', 'cherry')
```

---

### Mistake 3 – Forgetting That Index Counting Starts at 0

```python
t = ("a", "b", "c")
print(t[1])   # Many beginners expect "a", but the answer is "b"
```

**Fix:** Remember — the **first** item is always at index `0`, not `1`.

---

### Mistake 4 – Mismatched Unpacking Variables

```python
# WRONG — 3 items, only 2 variables
t = ("apple", "banana", "cherry")
(a, b) = t   # ValueError!
```

**Fix:** Make sure the number of variables matches the number of tuple items, or use `*` to capture extras:

```python
(a, *b) = t
print(a)   # apple
print(b)   # ['banana', 'cherry']
```

---

### Mistake 5 – Using `index()` on a Non-Existent Value

```python
t = ("apple", "banana", "cherry")
print(t.index("mango"))   # ValueError! "mango" is not in the tuple
```

**Fix:** Always check with `in` before using `index()`:

```python
if "mango" in t:
    print(t.index("mango"))
else:
    print("mango is not in the tuple")
```

---

### Mistake 6 – Using Double Brackets Incorrectly with `tuple()`

```python
# WRONG
t = tuple("apple", "banana")   # TypeError

# CORRECT
t = tuple(("apple", "banana"))  # Pass the items inside an inner set of brackets
print(t)   # ('apple', 'banana')
```

---

## Section 14 – Reflection Questions

Take a moment to test your understanding before moving on.

1. What are the three key characteristics of a tuple?
2. How is a tuple different from a list?
3. What output do you expect from `("a", "b", "c")[1]`?
4. If a tuple has 5 items, what index refers to the last item using negative indexing?
5. Why must you add a trailing comma when creating a single-item tuple?
6. What is "unpacking" a tuple?
7. In what situation would you use `*` when unpacking a tuple?
8. Name the two tuple methods and describe what each does.
9. You have a tuple `t = (10, 20, 30, 40, 50)`. What does `t[1:4]` return?
10. Why might you choose a tuple over a list when storing days of the week?

---

## Section 15 – Completion Checklist

Check off each item as you complete it:

- [ ] I can create a tuple using round brackets `( )`
- [ ] I can create a tuple using the `tuple()` constructor
- [ ] I know how to create a single-item tuple (with the trailing comma)
- [ ] I can access items using positive and negative index numbers
- [ ] I can slice a range of items from a tuple
- [ ] I can check if a value exists in a tuple using `in`
- [ ] I understand why tuples are immutable and how to work around it
- [ ] I can unpack a tuple into separate variables
- [ ] I can use `*` to capture extra items during unpacking
- [ ] I can loop through a tuple using `for`, index-based `for`, and `while`
- [ ] I can join two tuples using `+`
- [ ] I can multiply a tuple using `*`
- [ ] I can use `count()` to count how often a value appears
- [ ] I can use `index()` to find the position of a value
- [ ] I completed the mini project and understand each part
- [ ] I can explain all six common beginner mistakes and how to fix them

---

## Lesson Summary

Here is a compact reference of everything covered in this lesson:

**Creating Tuples**

```python
t = ("a", "b", "c")           # standard
t = tuple(("a", "b", "c"))    # using constructor
t = ("a",)                    # single-item (comma required!)
```

**Accessing Items**

```python
t[0]        # first item
t[-1]       # last item
t[1:3]      # slice (index 1 included, 3 excluded)
t[:2]       # from start to index 2
t[2:]       # from index 2 to end
"x" in t    # True if "x" is in the tuple
```

**Updating (Workaround)**

```python
lst = list(t)     # convert to list
lst[0] = "new"    # make changes
t = tuple(lst)    # convert back
```

**Unpacking**

```python
(a, b, c) = t              # standard unpacking
(a, *rest) = t             # star collects extras as a list
(a, *middle, z) = t        # star in the middle
```

**Looping**

```python
for item in t:             # direct loop
for i in range(len(t)):    # index-based loop

i = 0
while i < len(t):          # while loop
    print(t[i])
    i += 1
```

**Joining**

```python
t3 = t1 + t2      # concatenate
t2 = t1 * 3       # repeat 3 times
```

**Tuple Methods**

```python
t.count("value")   # count occurrences
t.index("value")   # find first position
```

**The Four Python Collections**

| | List | Tuple | Set | Dictionary |
|---|---|---|---|---|
| Ordered | ✅ | ✅ | ❌ | ✅ |
| Changeable | ✅ | ❌ | ❌* | ✅ |
| Duplicates | ✅ | ✅ | ❌ | ❌ |
| Syntax | `[]` | `()` | `{}` | `{k:v}` |

---

*Great work completing Lesson 09! You now understand Python tuples from the ground up — what they are, why they exist, and how to use every feature they offer. In the next lesson, you will explore **Python Sets**, another collection type with its own unique rules.*
