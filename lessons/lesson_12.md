---
render_with_liquid: false
title: "Lesson 12: Python Dictionary Methods & If/Elif/Else Conditions"
nav_order: 12
---

# Lesson 12: Python Dictionary Methods & If / Elif / Else Conditions

---

## Lesson Introduction

Welcome to Lesson 12! In this lesson, you will master two powerful areas of Python programming:

**Part 1 — Dictionary Methods:** Python gives you a built-in toolkit of methods (special actions) that let you do powerful things with dictionaries — like safely reading values, adding new data, removing items, copying, and viewing keys/values in loops. You will learn all 11 official dictionary methods with clear examples.

**Part 2 — If / Elif / Else Conditions:** Computers make decisions just like humans do. When you wake up and check if it is raining, you decide whether to carry an umbrella. Python does the same — using `if`, `elif`, and `else` to make decisions based on conditions. This section teaches you everything about decision-making in Python, from the simplest `if` check to multi-branch `elif` chains.

By the end of this lesson you will be able to:
- Use all 11 dictionary methods confidently
- Write `if`, `elif`, and `else` statements correctly
- Combine dictionaries with conditions to build smart, real-world programs
- Complete a mini student report card project

---

## What You Need to Know First (Prerequisites)

Before continuing, make sure you are comfortable with these concepts. If any of them feel unfamiliar, here is a quick refresher:

### What is a Dictionary?

A **dictionary** is a Python data structure that stores information in **key-value pairs**. Think of it like a real-world dictionary: you look up a word (the key) and get its meaning (the value).

```python
# A simple dictionary
student = {
    "name": "Amara",
    "age": 17,
    "grade": "A"
}
```

- `"name"`, `"age"`, `"grade"` are **keys** — they are labels for your data
- `"Amara"`, `17`, `"A"` are **values** — they are the actual data

You access a value using its key:

```python
print(student["name"])   # Output: Amara
print(student["age"])    # Output: 17
```

### What is a Method?

A **method** is a built-in action that belongs to a data type. You call it using a dot (`.`) after the variable name. For example:

```python
my_dict.keys()    # The keys() method belongs to dictionaries
my_list.append()  # The append() method belongs to lists
```

Think of methods as the dictionary's own built-in tools.

### What is a Boolean?

A **Boolean** is a value that is either `True` or `False`. This is the foundation of all conditions in Python.

```python
is_raining = True
is_sunny = False
```

### What is a Comparison Operator?

Comparison operators compare two values and produce a Boolean result (`True` or `False`):

| Operator | Meaning                  | Example       | Result  |
|----------|--------------------------|---------------|---------|
| `==`     | Equal to                 | `5 == 5`      | `True`  |
| `!=`     | Not equal to             | `5 != 3`      | `True`  |
| `>`      | Greater than             | `10 > 3`      | `True`  |
| `<`      | Less than                | `2 < 8`       | `True`  |
| `>=`     | Greater than or equal to | `5 >= 5`      | `True`  |
| `<=`     | Less than or equal to    | `4 <= 6`      | `True`  |

---

# PART 1: Python Dictionary Methods

---

## Section 1 — What Are Dictionary Methods and Why Do They Exist?

Imagine you have a dictionary of student scores, and you want to:
- Safely check if a student's score exists without crashing your program
- Get a list of all student names
- Remove a student from the dictionary
- Make a copy so you don't accidentally change the original

Doing all of this manually (writing many lines of code from scratch) would be tedious and error-prone. Python's **dictionary methods** are pre-built, ready-to-use tools that do all of this for you in one line.

Python has **11 built-in dictionary methods**:

| Method          | What It Does                                                              |
|-----------------|---------------------------------------------------------------------------|
| `clear()`       | Removes all items from the dictionary (empties it)                       |
| `copy()`        | Makes a shallow copy of the dictionary                                   |
| `fromkeys()`    | Creates a new dictionary from a list of keys, with a shared value        |
| `get()`         | Safely returns the value for a key (no crash if key is missing)          |
| `items()`       | Returns all key-value pairs as a list of tuples                          |
| `keys()`        | Returns all keys in the dictionary                                        |
| `pop()`         | Removes a specific key and returns its value                             |
| `popitem()`     | Removes and returns the last inserted key-value pair                     |
| `setdefault()`  | Returns a key's value; inserts the key with a default if it doesn't exist|
| `update()`      | Adds or updates multiple key-value pairs at once                         |
| `values()`      | Returns all values in the dictionary                                      |

We will go through each one clearly with examples.

---

## Method 1: `keys()` — Get All Keys

### What Is It?

`keys()` returns a special view object that lists all the **keys** (labels) in your dictionary.

**Why use it?** When you want to see what keys exist, loop through them, or check if a key is in your dictionary.

### Simple Example

```python
person = {"name": "Chidi", "age": 25, "city": "Lagos"}

all_keys = person.keys()
print(all_keys)
```

**Expected Output:**
```
dict_keys(['name', 'age', 'city'])
```

> 💡 The output shows `dict_keys([...])` — this is a special view object, not a regular list. But you can use it in loops just like a list!

### Using `keys()` in a Loop

```python
person = {"name": "Chidi", "age": 25, "city": "Lagos"}

for key in person.keys():
    print(key)
```

**Expected Output:**
```
name
age
city
```

**Line-by-line explanation:**
- `for key in person.keys():` — loop through every key in the dictionary
- `print(key)` — print each key on its own line

### Checking If a Key Exists Using `in`

```python
person = {"name": "Chidi", "age": 25, "city": "Lagos"}

print("name" in person.keys())    # Output: True
print("salary" in person.keys())  # Output: False
```

> 🤔 **Thinking prompt:** What would happen if you tried `person["salary"]` directly? You would get a `KeyError`! That is why checking first (or using `.get()`) is so important.

---

## Method 2: `values()` — Get All Values

### What Is It?

`values()` returns a view of all the **values** in your dictionary.

**Why use it?** When you only care about the data, not the labels — for example, calculating the total of all scores.

### Simple Example

```python
scores = {"maths": 85, "english": 90, "science": 78}

print(scores.values())
```

**Expected Output:**
```
dict_values([85, 90, 78])
```

### Looping Through Values

```python
scores = {"maths": 85, "english": 90, "science": 78}

for score in scores.values():
    print(score)
```

**Expected Output:**
```
85
90
78
```

### Practical Use — Calculating the Total

```python
scores = {"maths": 85, "english": 90, "science": 78}

total = sum(scores.values())
print("Total score:", total)
```

**Expected Output:**
```
Total score: 253
```

**Explanation:**
- `sum(scores.values())` — Python's built-in `sum()` function adds all the values together
- The result is stored in `total` and printed

---

## Method 3: `items()` — Get All Key-Value Pairs

### What Is It?

`items()` returns a view of all key-value pairs. Each pair is wrapped in a **tuple** — a bracket `()` that holds two items: the key and the value.

**Why use it?** When you want to loop through a dictionary and need both the key AND the value at the same time.

### Simple Example

```python
student = {"name": "Fatima", "score": 92, "grade": "A"}

print(student.items())
```

**Expected Output:**
```
dict_items([('name', 'Fatima'), ('score', 92), ('grade', 'A')])
```

Each pair like `('name', 'Fatima')` is a **tuple** — the key comes first, then the value.

### Looping with `items()` — The Most Common Pattern

```python
student = {"name": "Fatima", "score": 92, "grade": "A"}

for key, value in student.items():
    print(key, "->", value)
```

**Expected Output:**
```
name -> Fatima
score -> 92
grade -> A
```

**Line-by-line explanation:**
- `for key, value in student.items():` — for each pair, Python automatically unpacks it into two variables: `key` and `value`
- `print(key, "->", value)` — print both the key and its value with an arrow between them

> 💡 This is one of the most commonly used patterns in all of Python programming! You will use it constantly.

---

## Method 4: `get()` — Safely Read a Value

### What Is It?

`get(key)` returns the value for the given key. But unlike `dict[key]`, it does **not crash** if the key doesn't exist — it returns `None` (or a default value you choose) instead.

**Why use it?** To safely read dictionary values without risking a `KeyError` crash.

### The Problem Without `get()`

```python
person = {"name": "Emeka", "age": 30}

# This CRASHES with a KeyError if 'salary' doesn't exist:
print(person["salary"])   # KeyError: 'salary'
```

### The Safe Way with `get()`

```python
person = {"name": "Emeka", "age": 30}

salary = person.get("salary")
print(salary)
```

**Expected Output:**
```
None
```

No crash! It returned `None` because `"salary"` doesn't exist in the dictionary.

### Using a Default Value with `get()`

You can provide a second argument — the value to return if the key is missing:

```python
person = {"name": "Emeka", "age": 30}

salary = person.get("salary", 0)
print(salary)
```

**Expected Output:**
```
0
```

**Explanation:**
- `person.get("salary", 0)` — look for `"salary"`; if not found, return `0` instead of `None`

### Second Example

```python
inventory = {"apples": 10, "oranges": 5}

# Key exists:
print(inventory.get("apples", 0))    # Output: 10

# Key doesn't exist:
print(inventory.get("bananas", 0))   # Output: 0
```

> 🤔 **Thinking prompt:** Why is `get()` safer than `dict[key]` in a real application? What would happen in a school database if you tried to access a student that doesn't exist?

---

## Method 5: `update()` — Add or Modify Multiple Items

### What Is It?

`update()` lets you add new key-value pairs or change existing ones — all at once — by passing in another dictionary or keyword arguments.

**Why use it?** When you need to update many things in a dictionary at once, instead of doing it one by one.

### Simple Example — Adding New Keys

```python
profile = {"name": "Ngozi", "age": 22}

profile.update({"city": "Abuja", "job": "Engineer"})

print(profile)
```

**Expected Output:**
```
{'name': 'Ngozi', 'age': 22, 'city': 'Abuja', 'job': 'Engineer'}
```

**Explanation:**
- `profile.update({...})` — pass a dictionary with new pairs to add
- Python merges the new dictionary into the existing one

### Updating Existing Keys

```python
product = {"name": "Laptop", "price": 500, "stock": 10}

product.update({"price": 450, "stock": 8})

print(product)
```

**Expected Output:**
```
{'name': 'Laptop', 'price': 450, 'stock': 8}
```

The price and stock were updated. The name stayed the same.

### Update Using Keyword Arguments

```python
car = {"brand": "Toyota", "year": 2018}

car.update(year=2023, color="Red")

print(car)
```

**Expected Output:**
```
{'brand': 'Toyota', 'year': 2023, 'color': 'Red'}
```

---

## Method 6: `pop()` — Remove a Specific Key

### What Is It?

`pop(key)` removes the item with the given key from the dictionary AND returns its value so you can use it.

**Why use it?** When you need to both remove a key and use the value it had.

### Simple Example

```python
cart = {"apple": 3, "banana": 5, "mango": 2}

removed_value = cart.pop("banana")

print("Removed:", removed_value)
print("Cart after:", cart)
```

**Expected Output:**
```
Removed: 5
Cart after: {'apple': 3, 'mango': 2}
```

**Explanation:**
- `cart.pop("banana")` — removes `"banana"` from the dictionary and returns `5` (the value)
- We store that returned value in `removed_value`

### Using a Default Value to Avoid KeyError

If the key doesn't exist and you don't provide a default, `pop()` crashes:

```python
cart = {"apple": 3, "mango": 2}

# Safe pop with default:
result = cart.pop("banana", "Not in cart")
print(result)
```

**Expected Output:**
```
Not in cart
```

> 🤔 **Thinking prompt:** What happens if you call `pop()` on a key that doesn't exist, without providing a default? Try it and see!

---

## Method 7: `popitem()` — Remove the Last Item

### What Is It?

`popitem()` removes and returns the **last inserted** key-value pair as a tuple.

**Why use it?** Useful when you want to process and remove items one at a time from the end, like a stack.

### Simple Example

```python
data = {"a": 1, "b": 2, "c": 3}

last_item = data.popitem()

print("Removed:", last_item)
print("Dictionary after:", data)
```

**Expected Output:**
```
Removed: ('c', 3)
Dictionary after: {'a': 1, 'b': 2}
```

**Explanation:**
- `data.popitem()` removes `('c', 3)` because `"c"` was inserted last
- It returns the pair as a tuple

> ⚠️ **Common Mistake:** In Python versions before 3.7, `popitem()` removed a random item. In Python 3.7+, it always removes the LAST inserted item. Always check your Python version.

---

## Method 8: `clear()` — Empty the Dictionary

### What Is It?

`clear()` removes ALL items from the dictionary, leaving it completely empty.

**Why use it?** When you want to reset a dictionary and start fresh without deleting the variable itself.

### Simple Example

```python
user_data = {"name": "Kola", "score": 95, "level": 3}

print("Before:", user_data)

user_data.clear()

print("After:", user_data)
```

**Expected Output:**
```
Before: {'name': 'Kola', 'score': 95, 'level': 3}
After: {}
```

The `{}` means the dictionary is now empty.

> ⚠️ **Common Mistake:** Don't confuse `clear()` with reassigning: `user_data = {}` also empties it, but `clear()` is the "correct" method because it modifies the existing dictionary in place. If another variable points to the same dictionary, `clear()` affects both; reassignment only affects the one variable.

---

## Method 9: `copy()` — Make a Duplicate

### What Is It?

`copy()` creates a **shallow copy** of the dictionary — a new independent dictionary with the same keys and values.

**Why use it?** To work with a duplicate so you don't accidentally change the original.

### The Problem Without `copy()`

```python
original = {"name": "Ada", "score": 80}

# This does NOT create a new dict — it just creates another name for the same dict:
alias = original

alias["score"] = 99   # This also changes original!

print("Original:", original)
print("Alias:", alias)
```

**Expected Output:**
```
Original: {'name': 'Ada', 'score': 99}
Alias: {'name': 'Ada', 'score': 99}
```

Both changed! That's because `alias` and `original` point to the **same** dictionary in memory.

### The Safe Way with `copy()`

```python
original = {"name": "Ada", "score": 80}

backup = original.copy()   # A truly separate copy

backup["score"] = 99       # Only changes backup

print("Original:", original)
print("Backup:", backup)
```

**Expected Output:**
```
Original: {'name': 'Ada', 'score': 80}
Backup: {'name': 'Ada', 'score': 99}
```

Now the original is safe!

---

## Method 10: `fromkeys()` — Create a New Dictionary from Keys

### What Is It?

`fromkeys(keys, value)` creates a **brand new dictionary** using a list of keys, all set to the same value.

**Why use it?** When you want to initialize a dictionary quickly with many keys all set to the same starting value — like all scores starting at 0.

### Simple Example

```python
subjects = ["maths", "english", "science"]

scores = dict.fromkeys(subjects, 0)

print(scores)
```

**Expected Output:**
```
{'maths': 0, 'english': 0, 'science': 0}
```

**Explanation:**
- `dict.fromkeys(subjects, 0)` — creates a new dict using `subjects` as keys, all set to `0`
- Notice: we call it on `dict` (the class), not on an existing dictionary

### Without a Default Value

```python
keys = ["a", "b", "c"]

new_dict = dict.fromkeys(keys)

print(new_dict)
```

**Expected Output:**
```
{'a': None, 'b': None, 'c': None}
```

When no value is specified, all keys default to `None`.

---

## Method 11: `setdefault()` — Get Value or Insert Default

### What Is It?

`setdefault(key, default)` is like `get()`, but with an extra superpower: if the key **doesn't exist**, it **inserts the key** with the default value into the dictionary.

**Why use it?** When you want to ensure a key exists with a starting value, but don't want to overwrite it if it already has a value.

### Simple Example

```python
data = {"name": "Bola"}

# Key doesn't exist — it gets inserted with default value:
result = data.setdefault("score", 0)

print("Result:", result)
print("Dictionary:", data)
```

**Expected Output:**
```
Result: 0
Dictionary: {'name': 'Bola', 'score': 0}
```

### Key Already Exists — No Overwrite

```python
data = {"name": "Bola", "score": 95}

# Key already exists — returns existing value without changing it:
result = data.setdefault("score", 0)

print("Result:", result)
print("Dictionary:", data)
```

**Expected Output:**
```
Result: 95
Dictionary: {'name': 'Bola', 'score': 95}
```

The score stayed `95` — `setdefault()` never overwrites an existing value.

> 💡 **Real-world use:** `setdefault()` is widely used when counting things. For example, counting how many times each word appears in a text.

```python
text = ["apple", "banana", "apple", "cherry", "banana", "apple"]
counts = {}

for word in text:
    counts.setdefault(word, 0)   # Make sure the key exists with 0
    counts[word] += 1             # Increment the count

print(counts)
```

**Expected Output:**
```
{'apple': 3, 'banana': 2, 'cherry': 1}
```

---

## Guided Practice — Dictionary Methods

### Exercise 1: Student Report System

**Objective:** Use dictionary methods to manage a student's data safely and efficiently.

**Scenario:** You are building a school database tool. You have a student's record and need to perform several operations on it.

**Setup:**

```python
student = {
    "name": "Tunde",
    "age": 16,
    "maths": 72,
    "english": 88
}
```

**Steps:**

**Step 1 — Add new subjects using `update()`:**

```python
student.update({"science": 91, "history": 65})
print(student)
```

**Expected Output:**
```
{'name': 'Tunde', 'age': 16, 'maths': 72, 'english': 88, 'science': 91, 'history': 65}
```

**Step 2 — Safely get a subject that might not exist using `get()`:**

```python
art_score = student.get("art", "Not enrolled")
print("Art:", art_score)
```

**Expected Output:**
```
Art: Not enrolled
```

**Step 3 — Print all subjects and scores using `items()`:**

```python
for subject, value in student.items():
    print(f"{subject}: {value}")
```

**Expected Output:**
```
name: Tunde
age: 16
maths: 72
english: 88
science: 91
history: 65
```

**Step 4 — Calculate average score using `values()`:**

```python
# Only average the actual scores (not name or age)
score_subjects = {"maths": 72, "english": 88, "science": 91, "history": 65}
scores_only = list(score_subjects.values())
average = sum(scores_only) / len(scores_only)
print("Average score:", average)
```

**Expected Output:**
```
Average score: 79.0
```

**Step 5 — Remove a subject using `pop()`:**

```python
removed = student.pop("history")
print("Removed history score:", removed)
print("Updated student:", student)
```

**Expected Output:**
```
Removed history score: 65
Updated student: {'name': 'Tunde', 'age': 16, 'maths': 72, 'english': 88, 'science': 91}
```

**Self-check Questions:**
1. What would `get()` return if we searched for a key that doesn't exist and gave no default?
2. What is the difference between `pop()` and `popitem()`?
3. Why is `copy()` important when sharing dictionaries?

---

# PART 2: Python If / Elif / Else Conditions

---

## Section 2 — What Are Conditions and Why Do We Need Them?

Every program needs to make **decisions**. Think about these real-world situations:

- **ATM machine:** "If the PIN is correct, allow withdrawal. Otherwise, deny access."
- **Weather app:** "If temperature > 35°C, show 'Hot'. If 20–35°C, show 'Warm'. If below 20°C, show 'Cool'."
- **Video game:** "If health = 0, display Game Over."
- **School system:** "If score >= 70, display 'Pass'. Otherwise, display 'Fail'."

In Python, we express decisions using three keywords: `if`, `elif`, and `else`.

---

## Section 3 — Python Comparison Operators (Refresher + More)

These operators evaluate to `True` or `False` and are the building blocks of all conditions:

```python
a = 10
b = 20

print(a == b)   # Equal? → False
print(a != b)   # Not equal? → True
print(a < b)    # Less than? → True
print(a > b)    # Greater than? → False
print(a <= 10)  # Less than or equal? → True
print(b >= 20)  # Greater than or equal? → True
```

**Expected Output:**
```
False
True
True
False
True
True
```

---

## Section 4 — The `if` Statement

### What Is It?

The `if` statement checks a condition. If the condition is `True`, Python runs the code block inside the `if`. If the condition is `False`, Python skips that block.

### The Structure

```
if condition:
    code to run when condition is True
```

> ⚠️ **Critical Rule — Indentation:** The code inside the `if` block MUST be indented (moved right) with spaces or a tab. Python uses indentation to know what belongs inside the `if`. Other languages use `{}` brackets, but Python uses indentation.

### Very Simple Example

```python
temperature = 38

if temperature > 35:
    print("It is very hot outside!")
```

**Expected Output:**
```
It is very hot outside!
```

**Line-by-line explanation:**
- `temperature = 38` — we store the value `38` in a variable called `temperature`
- `if temperature > 35:` — Python checks: is `38 > 35`? Yes! So it is `True`
- The colon `:` at the end of the `if` line is required — it signals that a code block follows
- `    print("It is very hot outside!")` — this line is indented (4 spaces), so it is inside the `if` block. Since the condition was `True`, this line runs

### Example Where Condition is False

```python
temperature = 20

if temperature > 35:
    print("It is very hot outside!")

print("Program continues...")
```

**Expected Output:**
```
Program continues...
```

Since `20 > 35` is `False`, the print inside the `if` block is skipped. Execution jumps to the next unindented line.

### Multiple Statements Inside an `if` Block

All statements inside the block must be at the same indentation level:

```python
age = 20

if age >= 18:
    print("You are an adult.")
    print("You can vote.")
    print("You can drive.")
```

**Expected Output:**
```
You are an adult.
You can vote.
You can drive.
```

All three `print` statements are at the same indentation level, so they are all inside the `if` block. All three run because the condition is `True`.

### Common Beginner Mistake — Missing Colon

```python
# WRONG - Missing colon after condition:
if age >= 18
    print("Adult")
# SyntaxError: invalid syntax
```

```python
# CORRECT:
if age >= 18:
    print("Adult")
```

### Common Beginner Mistake — Wrong Indentation

```python
# WRONG - print is not indented:
if age >= 18:
print("Adult")   # IndentationError
```

```python
# CORRECT - print is indented:
if age >= 18:
    print("Adult")
```

### Using Boolean Variables in `if`

You can use a variable that is already `True` or `False` directly in an `if` statement:

```python
is_logged_in = True

if is_logged_in:
    print("Welcome back!")
```

**Expected Output:**
```
Welcome back!
```

### Truthy and Falsy Values

Python treats some values as "truthy" (behaves like `True`) and others as "falsy" (behaves like `False`):

| Falsy (acts like False) | Truthy (acts like True)      |
|-------------------------|------------------------------|
| `0` (zero)              | Any non-zero number (5, -3)  |
| `""` (empty string)     | Any non-empty string         |
| `[]` (empty list)       | Any non-empty list           |
| `{}` (empty dict)       | Any non-empty dict           |
| `None`                  | Everything else              |

```python
name = ""

if name:
    print("Name exists:", name)

# Since name is an empty string (falsy), nothing is printed
print("Done")
```

**Expected Output:**
```
Done
```

```python
name = "Chidi"

if name:
    print("Name exists:", name)
```

**Expected Output:**
```
Name exists: Chidi
```

---

## Section 5 — The `else` Statement

### What Is It?

`else` is added after an `if` block. It runs when the `if` condition is `False`. Think of it as "otherwise, do this instead."

### The Structure

```
if condition:
    code runs when condition is True
else:
    code runs when condition is False
```

### Simple Example

```python
score = 55

if score >= 70:
    print("You passed!")
else:
    print("You did not pass. Try again!")
```

**Expected Output:**
```
You did not pass. Try again!
```

**Explanation:**
- `score >= 70` → `55 >= 70` → `False`
- The `if` block is skipped
- Python runs the `else` block instead

### Another Example

```python
age = 15

if age >= 18:
    print("You can vote.")
else:
    print("You are too young to vote.")
```

**Expected Output:**
```
You are too young to vote.
```

> 💡 `else` never has a condition of its own — it is simply the "everything else" case. It catches whatever the `if` didn't catch.

### Common Beginner Mistake — `else` with a condition

```python
# WRONG - else cannot have a condition:
if score >= 70:
    print("Pass")
else score < 70:     # SyntaxError!
    print("Fail")
```

```python
# CORRECT:
if score >= 70:
    print("Pass")
else:
    print("Fail")
```

---

## Section 6 — The `elif` Statement (Else If)

### What Is It?

`elif` stands for "else if." It lets you check **multiple conditions** in sequence. Python checks each condition from top to bottom and runs the first block whose condition is `True`. Once a match is found, the rest are skipped.

### The Structure

```
if condition_1:
    code for condition_1
elif condition_2:
    code for condition_2
elif condition_3:
    code for condition_3
else:
    code when nothing matched
```

### Why Do We Need `elif`?

Without `elif`, you would need multiple separate `if` statements, and ALL of them would be checked even after a match is found. `elif` stops checking once a match is found — this is both more efficient and produces correct results.

### Simple Example — Grade Calculator

```python
score = 82

if score >= 90:
    print("Grade: A")
elif score >= 80:
    print("Grade: B")
elif score >= 70:
    print("Grade: C")
elif score >= 60:
    print("Grade: D")
else:
    print("Grade: F")
```

**Expected Output:**
```
Grade: B
```

**Step-by-step trace:**
1. `score >= 90` → `82 >= 90` → `False` → skip
2. `score >= 80` → `82 >= 80` → `True` ✅ → print `"Grade: B"` → stop checking

### Another Example — Time of Day Greeting

```python
hour = 14   # 2:00 PM in 24-hour format

if hour < 12:
    print("Good morning!")
elif hour < 17:
    print("Good afternoon!")
elif hour < 21:
    print("Good evening!")
else:
    print("Good night!")
```

**Expected Output:**
```
Good afternoon!
```

**Trace:**
1. `hour < 12` → `14 < 12` → `False` → skip
2. `hour < 17` → `14 < 17` → `True` ✅ → print `"Good afternoon!"` → stop

### Example — Traffic Light System

```python
light = "red"

if light == "green":
    print("Go!")
elif light == "yellow":
    print("Slow down!")
elif light == "red":
    print("Stop!")
else:
    print("Unknown light color")
```

**Expected Output:**
```
Stop!
```

> 🤔 **Thinking prompt:** What if you changed `light = "red"` to `light = "purple"`? What would print?

---

## Section 7 — Combining Conditions: `and`, `or`, `not`

Sometimes a single comparison isn't enough. You can combine conditions using logical operators:

| Operator | Meaning                               | Example                   |
|----------|---------------------------------------|---------------------------|
| `and`    | Both conditions must be True          | `age >= 18 and age <= 65` |
| `or`     | At least one condition must be True   | `day == "Sat" or day == "Sun"` |
| `not`    | Reverses True to False and vice versa | `not is_banned`           |

### Using `and`

```python
age = 25
has_id = True

if age >= 18 and has_id:
    print("Entry allowed.")
else:
    print("Entry denied.")
```

**Expected Output:**
```
Entry allowed.
```

Both conditions must be `True`. `age >= 18` → `True`, `has_id` → `True` → overall `True`.

### Using `or`

```python
day = "Saturday"

if day == "Saturday" or day == "Sunday":
    print("It's the weekend!")
else:
    print("It's a weekday.")
```

**Expected Output:**
```
It's the weekend!
```

Only one condition needs to be `True`. `day == "Saturday"` → `True` → done!

### Using `not`

```python
is_banned = False

if not is_banned:
    print("User is allowed.")
else:
    print("User is banned.")
```

**Expected Output:**
```
User is allowed.
```

`not is_banned` → `not False` → `True` → run the `if` block.

---

## Section 8 — `if` Statements with Dictionaries

This is where everything comes together! You can use `if` statements with dictionaries to make smart, data-driven decisions.

### Example 1 — Check if a Key Exists

```python
student = {"name": "Amaka", "score": 88}

if "score" in student:
    print("Score found:", student["score"])
else:
    print("No score recorded.")
```

**Expected Output:**
```
Score found: 88
```

### Example 2 — Grade Based on Dictionary Score

```python
student = {"name": "Emeka", "score": 74}

score = student["score"]

if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
elif score >= 60:
    grade = "D"
else:
    grade = "F"

print(f"{student['name']} scored {score} → Grade: {grade}")
```

**Expected Output:**
```
Emeka scored 74 → Grade: C
```

### Example 3 — Check Multiple Students

```python
students = {
    "Ada": 92,
    "Bisi": 58,
    "Chike": 75,
    "Dayo": 45
}

for name, score in students.items():
    if score >= 70:
        status = "PASS"
    else:
        status = "FAIL"
    print(f"{name}: {score} → {status}")
```

**Expected Output:**
```
Ada: 92 → PASS
Bisi: 58 → FAIL
Chike: 75 → PASS
Dayo: 45 → FAIL
```

---

## Section 9 — Nested `if` Statements

An `if` statement inside another `if` statement is called a **nested if**. Use this when a second decision only matters if the first condition is already `True`.

### Example — Age and Membership Check

```python
age = 25
is_member = True

if age >= 18:
    print("Age check passed.")
    if is_member:
        print("Member discount applied!")
    else:
        print("No member discount.")
else:
    print("Must be 18 or older.")
```

**Expected Output:**
```
Age check passed.
Member discount applied!
```

**Explanation:**
- First, Python checks if `age >= 18` → `True` → enter outer `if`
- Inside the outer `if`, it checks `is_member` → `True` → print discount message

> ⚠️ **Warning:** Deeply nested `if` statements (3+ levels deep) make code hard to read. Try to keep nesting to a maximum of 2 levels when possible.

---

## Section 10 — The `pass` Statement

Sometimes you want to write an `if` block but not fill in the code yet (maybe as a placeholder). But Python doesn't allow an empty block. Use `pass` to create an empty placeholder:

```python
score = 85

if score >= 70:
    pass   # TODO: Add passing logic later

print("End of check")
```

**Expected Output:**
```
End of check
```

`pass` does nothing — it simply tells Python "this block is intentionally empty for now."

---

## Guided Practice — If / Elif / Else

### Exercise 1: Temperature Classifier

**Objective:** Use `elif` to classify a temperature reading.

**Scenario:** You are building a weather monitoring app. Write code that classifies temperature into categories.

**Steps:**

```python
temperature = 28   # Try changing this value

if temperature >= 40:
    print("Extreme heat! Stay indoors.")
elif temperature >= 30:
    print("Very hot. Stay hydrated.")
elif temperature >= 20:
    print("Warm and comfortable.")
elif temperature >= 10:
    print("Cool. Bring a jacket.")
else:
    print("Cold. Dress warmly!")
```

**Expected Output (temperature = 28):**
```
Warm and comfortable.
```

**What-if challenges:**
- Change `temperature = 28` to `42`. What prints?
- Change it to `5`. What prints?
- What is the minimum temperature that would trigger "Very hot"?

---

### Exercise 2: Login System with Dictionary

**Objective:** Use a dictionary to store user credentials and `if/else` to validate login.

```python
users = {
    "admin": "password123",
    "ngozi": "securepass",
    "emeka": "mypass456"
}

# Simulated login attempt:
username = "ngozi"
password = "securepass"

if username in users:
    if users[username] == password:
        print(f"Welcome, {username}! Login successful.")
    else:
        print("Incorrect password.")
else:
    print("Username not found.")
```

**Expected Output:**
```
Welcome, ngozi! Login successful.
```

**Self-check Questions:**
1. What prints if `password = "wrongpass"`?
2. What prints if `username = "unknown"`?
3. Why do we check `username in users` first, before checking the password?

---

## Mini Project: Student Report Card Generator

### Project Overview

You will build a **Student Report Card Generator** that:
1. Stores multiple students and their subject scores in a dictionary
2. Calculates the average score for each student
3. Assigns a grade using `if/elif/else`
4. Prints a formatted report card for each student

This project combines ALL the skills from this lesson: dictionary methods, loops, and conditions.

---

### Stage 1 — Setup: Create the Student Data

```python
# Stage 1: Student database
students = {
    "Amara": {"maths": 85, "english": 78, "science": 92},
    "Bola":  {"maths": 60, "english": 55, "science": 58},
    "Chike": {"maths": 95, "english": 88, "science": 91},
    "Dayo":  {"maths": 40, "english": 45, "science": 50},
}

print("Student database loaded successfully.")
print("Number of students:", len(students))
```

**Expected Output:**
```
Student database loaded successfully.
Number of students: 4
```

---

### Stage 2 — Grade Assignment Function Logic

Before building the full project, let's write the grade logic separately:

```python
def get_grade(average):
    if average >= 90:
        return "A"
    elif average >= 80:
        return "B"
    elif average >= 70:
        return "C"
    elif average >= 60:
        return "D"
    else:
        return "F"

# Quick test:
print(get_grade(92))   # Expected: A
print(get_grade(75))   # Expected: C
print(get_grade(45))   # Expected: F
```

**Expected Output:**
```
A
C
F
```

---

### Stage 3 — Build the Full Report Card

```python
students = {
    "Amara": {"maths": 85, "english": 78, "science": 92},
    "Bola":  {"maths": 60, "english": 55, "science": 58},
    "Chike": {"maths": 95, "english": 88, "science": 91},
    "Dayo":  {"maths": 40, "english": 45, "science": 50},
}

def get_grade(average):
    if average >= 90:
        return "A"
    elif average >= 80:
        return "B"
    elif average >= 70:
        return "C"
    elif average >= 60:
        return "D"
    else:
        return "F"

# Print report card for each student
print("=" * 40)
print("       STUDENT REPORT CARDS")
print("=" * 40)

for student_name, subjects in students.items():
    # Calculate average using values()
    scores = list(subjects.values())
    average = sum(scores) / len(scores)
    grade = get_grade(average)

    # Determine pass/fail
    if grade in ["A", "B", "C"]:
        status = "PASS"
    else:
        status = "FAIL"

    # Print the report for this student
    print(f"\nStudent: {student_name}")
    print("-" * 30)

    for subject, score in subjects.items():
        print(f"  {subject.capitalize():<12}: {score}")

    print(f"  {'Average':<12}: {average:.1f}")
    print(f"  {'Grade':<12}: {grade}")
    print(f"  {'Status':<12}: {status}")

print("\n" + "=" * 40)
print("End of Report")
```

**Expected Output:**
```
========================================
       STUDENT REPORT CARDS
========================================

Student: Amara
------------------------------
  Maths       : 85
  English      : 78
  Science      : 92
  Average      : 85.0
  Grade        : B
  Status       : PASS

Student: Bola
------------------------------
  Maths       : 60
  English      : 55
  Science      : 58
  Average      : 57.7
  Grade        : F
  Status       : FAIL

Student: Chike
------------------------------
  Maths       : 95
  English      : 88
  Science      : 91
  Average      : 91.3
  Grade        : A
  Status       : PASS

Student: Dayo
------------------------------
  Maths       : 40
  English      : 45
  Science      : 50
  Average      : 45.0
  Grade        : F
  Status       : FAIL

========================================
End of Report
```

---

### Stage 4 — Enhancement: Find Top Student

```python
# Add this to the end of the Stage 3 code:

best_student = None
best_average = 0

for student_name, subjects in students.items():
    scores = list(subjects.values())
    average = sum(scores) / len(scores)

    if average > best_average:
        best_average = average
        best_student = student_name

print(f"\n🏆 Top Student: {best_student} with an average of {best_average:.1f}")
```

**Expected Output:**
```
🏆 Top Student: Chike with an average of 91.3
```

---

### Reflection Questions for the Mini Project

1. What dictionary method did you use to loop through each student's subjects and scores?
2. Why was `values()` useful when calculating the average?
3. In the grade function, why does the order of `elif` conditions matter?
4. What would happen if you put `elif average >= 60` before `elif average >= 90`?
5. How could you modify the project to also show which subject each student scored highest in?

---

## Common Beginner Mistakes — Full Summary

### Dictionary Method Mistakes

**Mistake 1 — Accessing a missing key directly:**

```python
data = {"name": "Ada"}

# WRONG - crashes with KeyError:
print(data["score"])

# CORRECT - use get():
print(data.get("score", "No score"))
```

**Mistake 2 — Forgetting `copy()` before editing:**

```python
original = {"x": 10}
copy1 = original        # NOT a copy! Both point to same dict
copy2 = original.copy() # TRUE copy

copy1["x"] = 99         # This also changes original!
copy2["x"] = 50         # This only changes copy2

print(original)   # {'x': 99}  ← original was modified!
```

**Mistake 3 — `pop()` on a missing key without a default:**

```python
data = {"a": 1}

# WRONG - crashes:
data.pop("b")

# CORRECT - use default:
data.pop("b", None)
```

**Mistake 4 — Confusing `pop()` and `popitem()`:**
- `pop("key")` — removes a specific key you name
- `popitem()` — removes the last inserted key (you don't get to choose which)

---

### If/Elif/Else Mistakes

**Mistake 1 — Missing colon:**

```python
# WRONG:
if score > 90
    print("A")

# CORRECT:
if score > 90:
    print("A")
```

**Mistake 2 — Wrong indentation:**

```python
# WRONG:
if score > 90:
print("A")    # IndentationError

# CORRECT:
if score > 90:
    print("A")
```

**Mistake 3 — Using `=` instead of `==` in a condition:**

```python
# WRONG (this assigns, not compares):
if score = 90:
    print("A")

# CORRECT (double == for comparison):
if score == 90:
    print("A")
```

**Mistake 4 — Wrong order in `elif` chains:**

```python
# WRONG - Grade A will never be reached because >= 60 catches everything first:
if score >= 60:
    grade = "D"
elif score >= 90:   # Never reached!
    grade = "A"

# CORRECT - Put the most specific (largest) condition first:
if score >= 90:
    grade = "A"
elif score >= 60:
    grade = "D"
```

**Mistake 5 — Using `else` when you need `elif`:**

```python
score = 75

# WRONG - 'else' doesn't check a condition:
if score >= 90:
    print("A")
else score >= 80:   # SyntaxError!
    print("B")

# CORRECT:
if score >= 90:
    print("A")
elif score >= 80:
    print("B")
```

---

## Lesson Reflection Questions

1. What is the difference between `get()` and accessing a key with `dict[key]`?
2. When would you use `setdefault()` instead of `get()`?
3. What does `items()` return, and why is it useful in a loop?
4. What does the colon `:` at the end of an `if` line tell Python?
5. What is the role of indentation in `if` statements?
6. Can you have an `elif` without a preceding `if`? Why or why not?
7. What is the difference between `and` and `or` in conditions?
8. What would happen if you have two `if` statements checking the same variable instead of `if/elif`? Give an example.
9. Why is the order of `elif` conditions important when checking number ranges?
10. How would you combine `items()` and `if/elif/else` to filter a dictionary and print only students who passed?

---

## Lesson Completion Checklist

Use this checklist to confirm you have mastered this lesson:

- [ ] I can name all 11 Python dictionary methods and describe what each one does
- [ ] I can use `keys()`, `values()`, and `items()` in loops
- [ ] I understand the difference between `get()` and direct key access `dict[key]`
- [ ] I can use `update()` to add and modify multiple items at once
- [ ] I can use `pop()` and `popitem()` to remove items safely
- [ ] I can use `copy()` to create an independent duplicate of a dictionary
- [ ] I can use `fromkeys()` to create a new dictionary from a list of keys
- [ ] I understand `setdefault()` and when it inserts vs. retrieves
- [ ] I can write a correct `if` statement with proper colon and indentation
- [ ] I can write `if/else` for two-path decisions
- [ ] I can write `if/elif/elif/else` for multi-path decisions
- [ ] I can combine conditions using `and`, `or`, and `not`
- [ ] I can use `if` inside dictionary loops to filter or classify data
- [ ] I completed the Student Report Card mini project
- [ ] I understand and can fix all common mistakes listed

---

## Lesson Summary

This lesson covered two major topics that work beautifully together in Python:

**Dictionary Methods** give you a complete toolkit for managing your data:
- `keys()`, `values()`, `items()` — for viewing and looping through dictionary contents
- `get()` — the safe way to read values without crashing
- `update()` — for adding or changing multiple items at once
- `pop()` / `popitem()` — for removing items
- `clear()` — for emptying a dictionary
- `copy()` — for making true duplicates
- `fromkeys()` — for creating dictionaries from key lists
- `setdefault()` — for reading with an automatic insert-if-missing feature

**If / Elif / Else Conditions** give Python the ability to make decisions:
- `if` checks a condition; if `True`, runs the block
- `else` runs when the `if` condition is `False`
- `elif` lets you check multiple conditions in sequence
- `and`, `or`, `not` combine conditions for more complex logic
- Proper **indentation** is mandatory — it defines what belongs inside each block
- Order matters in `elif` chains — put the most specific condition first

**Combined**, these two concepts let you build programs that store structured data AND respond intelligently to it — which is the foundation of virtually every real-world application: school systems, banking software, e-commerce platforms, weather apps, and much more.

---

*End of Lesson 12*
