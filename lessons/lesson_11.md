---
render_with_liquid: false
title: "Lesson 11: Python Dictionaries – From Zero to Real-World Mastery"
nav_order: 11
---

# Lesson 11: Python Dictionaries – From Zero to Real-World Mastery

---

## Lesson Introduction

Welcome to one of the most powerful lessons in Python! In this lesson, you will learn about **dictionaries** — one of Python's most useful and widely-used data structures.

Before you're done, you'll know how to:
- Create a dictionary and understand what it is
- Access, change, add, and remove data inside it
- Loop through a dictionary in multiple ways
- Copy a dictionary safely
- Build dictionaries inside dictionaries (nested dictionaries)
- Apply all of this in a real-world mini project

You do **not** need any prior experience with dictionaries. This lesson assumes you know only the very basics of Python (variables, print statements, and perhaps lists). Everything else will be taught step by step.

> **Real-world connection:** Dictionaries are everywhere. When a website stores your user profile, when a weather app stores city data, when a database returns a record — all of it uses something that works exactly like a Python dictionary. Once you master this, you're thinking like a real programmer.

---

## Prerequisite Concepts

Before we jump in, let's quickly make sure you understand a few ideas we'll build on.

### Variables
A variable is a named container that holds a value.

```python
name = "Alice"
age = 25
```

### Lists (Quick Review)
A list holds multiple values, one after another, accessed by position number (index).

```python
fruits = ["apple", "banana", "cherry"]
print(fruits[0])   # Output: apple
print(fruits[1])   # Output: banana
```

The **problem** with a list: you access items by their position. But what if you want to look up "the price of apples" — not "item number 0"? That's exactly where **dictionaries** shine.

---

## Part 1: What Is a Python Dictionary?

### The Core Idea

Think about a real physical dictionary (like the Oxford Dictionary). You look up a **word** (the key), and it gives you the **definition** (the value). You never say "give me definition number 47" — you say "give me the definition of *elephant*."

A Python dictionary works **exactly** the same way.

- Every piece of data has a **label (the key)**
- The label points to a **value**
- You retrieve data using the label, not a position number

> **Analogy:** Imagine a school locker system. Each student has a locker **number** (the key), and inside the locker is their **stuff** (the value). You look up locker 205, and you find what's inside — you don't count lockers one by one to find it.

### What Does a Dictionary Look Like?

```python
student = {
    "name": "Alice",
    "age": 20,
    "grade": "A"
}
```

Let's break this down symbol by symbol:

| Symbol | Meaning |
|--------|---------|
| `{` | Opens the dictionary |
| `"name"` | A **key** — the label for this piece of data |
| `:` | Separates the key from its value |
| `"Alice"` | The **value** — the actual data stored |
| `,` | Separates one key-value pair from the next |
| `}` | Closes the dictionary |

Each `key: value` pair is called a **dictionary item**.

### Your First Dictionary — Full Demo

```python
thisdict = {
    "brand": "Ford",
    "model": "Mustang",
    "year": 1964
}
print(thisdict)
```

**Expected Output:**
```
{'brand': 'Ford', 'model': 'Mustang', 'year': 1964}
```

Python prints the whole dictionary for you. Notice the curly braces `{}` in the output too.

> **Thinking prompt:** What happens if you just write `print(thisdict["brand"])`? What do you think it will show?

---

### Dictionary Items: Key Properties

Dictionaries have three important characteristics you must remember:

**1. Ordered** (Python 3.7 and later)
Items appear in the order you added them. Python 3.6 and earlier did NOT guarantee order — but modern Python does.

**2. Changeable (Mutable)**
You can add, remove, or update items after the dictionary is created.

**3. No Duplicate Keys**
Each key must be unique. If you use the same key twice, the second one **overwrites** the first.

```python
# Duplicate key example — the second "year" wins
thisdict = {
    "brand": "Ford",
    "model": "Mustang",
    "year": 1964,
    "year": 2020       # This overwrites 1964!
}
print(thisdict)
```

**Expected Output:**
```
{'brand': 'Ford', 'model': 'Mustang', 'year': 2020}
```

> **Common Beginner Mistake:** Using the same key twice and wondering why one of your values disappeared. Remember: only one value per key.

---

### Dictionary Length

To count how many items (key-value pairs) are in a dictionary, use `len()`:

```python
thisdict = {
    "brand": "Ford",
    "model": "Mustang",
    "year": 1964
}
print(len(thisdict))
```

**Expected Output:**
```
3
```

There are 3 key-value pairs, so the length is 3.

---

### Values Can Be Any Data Type

Dictionary values are not restricted to strings or numbers. They can be **any** Python data type:

```python
thisdict = {
    "brand": "Ford",          # string
    "electric": False,        # boolean
    "year": 1964,             # integer
    "colors": ["red", "white", "blue"]   # list!
}
print(thisdict)
```

**Expected Output:**
```
{'brand': 'Ford', 'electric': False, 'year': 1964, 'colors': ['red', 'white', 'blue']}
```

> **Real-world use:** When an app stores a user profile, it might store name (string), age (integer), is_premium_member (boolean), and purchased_items (list) — all in one dictionary.

---

### Checking the Data Type

Python's `type()` function confirms a dictionary is of type `dict`:

```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}
print(type(thisdict))
```

**Expected Output:**
```
<class 'dict'>
```

---

### The `dict()` Constructor — Another Way to Create a Dictionary

You can also create a dictionary using the built-in `dict()` function. Note: when using `dict()`, keys are written **without** quotes:

```python
thisdict = dict(name="John", age=36, country="Norway")
print(thisdict)
```

**Expected Output:**
```
{'name': 'John', 'age': 36, 'country': 'Norway'}
```

Both methods produce the same result. The curly-bracket method is more common in practice.

---

### Python's Four Collection Types — Where Dictionaries Fit

Python has four main collection types. Here's how they compare:

| Collection | Ordered | Changeable | Allows Duplicates |
|-----------|---------|------------|------------------|
| List `[]` | Yes | Yes | Yes |
| Tuple `()` | Yes | No | Yes |
| Set `{}` | No | No* | No |
| **Dictionary `{}`** | **Yes** | **Yes** | **No (keys only)** |

\* Set *items* are unchangeable, but you can add/remove items.

Dictionaries are the best choice when you want to label your data with meaningful names instead of position numbers.

---

## Part 2: Accessing Dictionary Items

### Method 1 — Square Bracket Notation

The most direct way to access a value is to write the dictionary name, then the key inside square brackets:

```python
thisdict = {
    "brand": "Ford",
    "model": "Mustang",
    "year": 1964
}
x = thisdict["model"]
print(x)
```

**Expected Output:**
```
Mustang
```

Think of it like this: `thisdict["model"]` means "go into `thisdict` and find the item labeled `model`."

### Method 2 — The `.get()` Method

The `.get()` method does the same thing but is **safer**:

```python
x = thisdict.get("model")
print(x)
```

**Expected Output:**
```
Mustang
```

**Why is `.get()` safer?**

If you try to access a key that doesn't exist using square brackets, Python **crashes** with a `KeyError`. But `.get()` quietly returns `None` instead of crashing:

```python
# Square bracket — crashes if key missing
print(thisdict["color"])   # KeyError: 'color'

# .get() — returns None safely
print(thisdict.get("color"))   # None
```

> **Best practice:** In production code or projects where the key might not exist, always prefer `.get()` to avoid crashes.

---

### Getting All Keys — `.keys()`

The `.keys()` method returns a view of all the keys in the dictionary:

```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}
x = thisdict.keys()
print(x)
```

**Expected Output:**
```
dict_keys(['brand', 'model', 'year'])
```

**Important — It's a "Live View":**
The keys list is linked to the dictionary. If you add a new item to the dictionary, the keys view updates automatically:

```python
car = {"brand": "Ford", "model": "Mustang", "year": 1964}
x = car.keys()
print(x)           # dict_keys(['brand', 'model', 'year'])

car["color"] = "white"    # Add a new key

print(x)           # dict_keys(['brand', 'model', 'year', 'color'])
```

**Expected Output:**
```
dict_keys(['brand', 'model', 'year'])
dict_keys(['brand', 'model', 'year', 'color'])
```

The variable `x` updated without you having to call `.keys()` again. That's what "live view" means.

---

### Getting All Values — `.values()`

The `.values()` method returns a view of all the values:

```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}
x = thisdict.values()
print(x)
```

**Expected Output:**
```
dict_values(['Ford', 'Mustang', 1964])
```

Again, this is a live view. If you change a value in the dictionary, `.values()` reflects it instantly:

```python
car = {"brand": "Ford", "model": "Mustang", "year": 1964}
x = car.values()
print(x)               # dict_values(['Ford', 'Mustang', 1964])

car["year"] = 2020     # Change a value

print(x)               # dict_values(['Ford', 'Mustang', 2020])
```

**Expected Output:**
```
dict_values(['Ford', 'Mustang', 1964])
dict_values(['Ford', 'Mustang', 2020])
```

---

### Getting All Key-Value Pairs — `.items()`

The `.items()` method returns a view of all key-value pairs as a list of tuples:

```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}
x = thisdict.items()
print(x)
```

**Expected Output:**
```
dict_items([('brand', 'Ford'), ('model', 'Mustang'), ('year', 1964)])
```

Each pair is wrapped in parentheses `()` — that's a **tuple**. Think of a tuple as a locked pair: "brand" is locked with "Ford", "model" is locked with "Mustang", and so on.

This `.items()` method is especially useful in loops (more on that in Part 6).

---

### Checking if a Key Exists — the `in` Keyword

Before accessing an item, you can check whether a key exists using `in`:

```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}

if "model" in thisdict:
    print("Yes, 'model' is one of the keys in the dictionary")
```

**Expected Output:**
```
Yes, 'model' is one of the keys in the dictionary
```

This is extremely useful in programs where you're not sure if a certain key was added yet.

```python
# Another example — checking before accessing
if "color" in thisdict:
    print(thisdict["color"])
else:
    print("No color recorded yet.")
```

**Expected Output:**
```
No color recorded yet.
```

---

## Part 3: Changing Dictionary Items

### Changing a Value by Key

To update a value, refer to its key and assign a new value:

```python
thisdict = {
    "brand": "Ford",
    "model": "Mustang",
    "year": 1964
}
thisdict["year"] = 2018
print(thisdict)
```

**Expected Output:**
```
{'brand': 'Ford', 'model': 'Mustang', 'year': 2018}
```

The key `"year"` still exists — only its value changed from `1964` to `2018`.

### Using the `.update()` Method

The `.update()` method lets you update one or more values at once by passing in a small dictionary:

```python
thisdict = {
    "brand": "Ford",
    "model": "Mustang",
    "year": 1964
}
thisdict.update({"year": 2020})
print(thisdict)
```

**Expected Output:**
```
{'brand': 'Ford', 'model': 'Mustang', 'year': 2020}
```

You can update multiple items in one call:

```python
thisdict.update({"year": 2022, "model": "Explorer"})
print(thisdict)
```

**Expected Output:**
```
{'brand': 'Ford', 'model': 'Explorer', 'year': 2022}
```

> **When to use `.update()` vs. direct assignment?**
> Use direct assignment `dict["key"] = value` for changing one value quickly.
> Use `.update()` when you want to update multiple values at once, or when you're merging data from another source.

---

## Part 4: Adding Items to a Dictionary

### Adding a New Key-Value Pair

Adding a new item is exactly like changing a value — but you use a **key that doesn't exist yet**:

```python
thisdict = {
    "brand": "Ford",
    "model": "Mustang",
    "year": 1964
}
thisdict["color"] = "red"
print(thisdict)
```

**Expected Output:**
```
{'brand': 'Ford', 'model': 'Mustang', 'year': 1964, 'color': 'red'}
```

Python sees that `"color"` is not an existing key, so it **creates** a new entry.

> **Key rule to remember:** If the key exists → it **updates** the value. If the key doesn't exist → it **adds** a new item. The same syntax does both.

### Using `.update()` to Add New Items

`.update()` also works for adding, not just changing:

```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}
thisdict.update({"color": "white"})
print(thisdict)
```

**Expected Output:**
```
{'brand': 'Ford', 'model': 'Mustang', 'year': 1964, 'color': 'white'}
```

---

## Part 5: Removing Items from a Dictionary

Python gives you several ways to remove items from a dictionary. Each one is useful in different situations.

### Method 1 — `.pop(key)` — Remove by Key Name

`.pop()` removes the item with the specified key and **returns its value**:

```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}
removed = thisdict.pop("model")
print(thisdict)
print("Removed value:", removed)
```

**Expected Output:**
```
{'brand': 'Ford', 'year': 1964}
Removed value: Mustang
```

This is useful when you want to remove an item but also need to use its value one last time.

### Method 2 — `.popitem()` — Remove the Last Inserted Item

`.popitem()` removes the **most recently added** item and returns it as a tuple `(key, value)`:

```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}
thisdict.popitem()
print(thisdict)
```

**Expected Output:**
```
{'brand': 'Ford', 'model': 'Mustang'}
```

`"year": 1964` was the last item added, so it was removed.

> **Note:** In Python 3.7 and earlier, `.popitem()` removed a random item. In Python 3.8+, it always removes the last inserted item.

### Method 3 — `del` Keyword — Delete by Key or Delete Entire Dictionary

Use `del` with a specific key to remove that item:

```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}
del thisdict["model"]
print(thisdict)
```

**Expected Output:**
```
{'brand': 'Ford', 'year': 1964}
```

You can also use `del` to **delete the entire dictionary**:

```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}
del thisdict
# print(thisdict)  # This would cause a NameError — dictionary no longer exists!
```

> **Warning:** After `del thisdict`, the variable `thisdict` no longer exists in memory. Trying to use it will cause a `NameError`.

### Method 4 — `.clear()` — Empty the Dictionary

`.clear()` removes **all items** but keeps the dictionary itself (as an empty dictionary):

```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}
thisdict.clear()
print(thisdict)
```

**Expected Output:**
```
{}
```

The dictionary still exists — it's just empty now. This is different from `del` which destroys the variable entirely.

---

### Removal Methods Quick Reference

| Method | What It Removes | Returns |
|--------|----------------|---------|
| `.pop("key")` | Item with that key | The removed value |
| `.popitem()` | Last inserted item | `(key, value)` tuple |
| `del dict["key"]` | Item with that key | Nothing |
| `del dict` | The whole variable | Nothing |
| `.clear()` | All items (keeps empty dict) | Nothing |

---

## Part 6: Looping Through a Dictionary

One of the most powerful things you can do with a dictionary is loop through it — visiting every item automatically. Python gives you several ways to do this.

### Loop 1 — Loop Through Keys (Default)

When you write a basic `for` loop on a dictionary, Python loops through the **keys** by default:

```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}

for x in thisdict:
    print(x)
```

**Expected Output:**
```
brand
model
year
```

> **Thinking prompt:** What do you need to add to also print the values?

### Loop 2 — Loop Through Keys Explicitly with `.keys()`

```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}

for x in thisdict.keys():
    print(x)
```

**Expected Output:**
```
brand
model
year
```

Same result as the default loop — but writing `.keys()` makes your intention very clear to anyone reading your code.

### Loop 3 — Loop Through Values with `.values()`

```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}

for x in thisdict.values():
    print(x)
```

**Expected Output:**
```
Ford
Mustang
1964
```

### Loop 4 — Loop Through Both Keys and Values with `.items()`

This is the most common and most useful loop. It gives you the key **and** value at the same time:

```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}

for key, value in thisdict.items():
    print(key, ":", value)
```

**Expected Output:**
```
brand : Ford
model : Mustang
year : 1964
```

**Line-by-line explanation:**
- `for key, value in thisdict.items():` — each time through the loop, Python unpacks the next tuple from `.items()` into two variables: `key` and `value`
- `print(key, ":", value)` — prints the key, a colon, and the value

> **Real-world use:** Imagine building a report that shows every setting in a configuration file, or printing out every field in a user's profile — that's exactly this loop pattern.

### Loop 5 — Access Values Inside a Key Loop

You can also loop through keys and manually access each value:

```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}

for x in thisdict:
    print(thisdict[x])
```

**Expected Output:**
```
Ford
Mustang
1964
```

Here, `x` is each key. Then `thisdict[x]` retrieves the value for that key.

---

## Part 7: Copying a Dictionary

### Why Copying Matters — The Dangerous Mistake

You might think this copies a dictionary:

```python
dict1 = {"brand": "Ford", "year": 1964}
dict2 = dict1       # This is NOT a copy!
```

**This does NOT create a real copy.** Both `dict1` and `dict2` now point to the **same dictionary in memory**. If you change one, the other changes too:

```python
dict1 = {"brand": "Ford", "year": 1964}
dict2 = dict1
dict2["year"] = 2023

print(dict1)   # {"brand": "Ford", "year": 2023} — changed!
print(dict2)   # {"brand": "Ford", "year": 2023}
```

This is one of the most common and confusing bugs for beginners. You must use a proper copy method.

---

### Safe Copy Method 1 — `.copy()`

```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}
mydict = thisdict.copy()
print(mydict)
```

**Expected Output:**
```
{'brand': 'Ford', 'model': 'Mustang', 'year': 1964}
```

Now `mydict` is a **completely independent** dictionary. Changes to `mydict` do **not** affect `thisdict`, and vice versa.

### Safe Copy Method 2 — `dict()` Constructor

```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}
mydict = dict(thisdict)
print(mydict)
```

**Expected Output:**
```
{'brand': 'Ford', 'model': 'Mustang', 'year': 1964}
```

Both `.copy()` and `dict()` create what's called a **shallow copy** — meaning the top-level dictionary is independent, but if your values are themselves dictionaries (nested), those inner dictionaries are still shared. For most beginner use cases, `.copy()` is perfectly safe and correct.

> **Remember the rule:** Never say `new_dict = old_dict` when you actually want a copy. Always use `.copy()` or `dict()`.

---

## Part 8: Nested Dictionaries

### What Is a Nested Dictionary?

A **nested dictionary** is a dictionary that contains other dictionaries as its values.

Think of it like a filing cabinet with drawers (outer dictionary) and folders inside each drawer (inner dictionaries).

### Creating a Nested Dictionary — All at Once

```python
myfamily = {
    "child1": {
        "name": "Emil",
        "year": 2004
    },
    "child2": {
        "name": "Tobias",
        "year": 2007
    },
    "child3": {
        "name": "Linus",
        "year": 2011
    }
}
print(myfamily)
```

**Expected Output:**
```
{'child1': {'name': 'Emil', 'year': 2004}, 'child2': {'name': 'Tobias', 'year': 2007}, 'child3': {'name': 'Linus', 'year': 2011}}
```

Here, `myfamily` has 3 keys: `"child1"`, `"child2"`, `"child3"`. Each key's value is itself a dictionary containing `"name"` and `"year"`.

### Creating a Nested Dictionary — By Combining Existing Ones

You can also create dictionaries separately and then combine them:

```python
child1 = {"name": "Emil", "year": 2004}
child2 = {"name": "Tobias", "year": 2007}
child3 = {"name": "Linus", "year": 2011}

myfamily = {
    "child1": child1,
    "child2": child2,
    "child3": child3
}
print(myfamily)
```

**Expected Output:**
```
{'child1': {'name': 'Emil', 'year': 2004}, 'child2': {'name': 'Tobias', 'year': 2007}, 'child3': {'name': 'Linus', 'year': 2011}}
```

Same result, different approach. The second approach is cleaner when the inner dictionaries are complex.

### Accessing Items Inside a Nested Dictionary

To access a value inside a nested dictionary, chain your square brackets:

```python
# Access child1's name
print(myfamily["child1"]["name"])
```

**Expected Output:**
```
Emil
```

**How to read this:** `myfamily["child1"]` gives you the inner dictionary `{"name": "Emil", "year": 2004}`. Then `["name"]` drills into that inner dictionary to get `"Emil"`.

More examples:

```python
print(myfamily["child2"]["year"])    # Output: 2007
print(myfamily["child3"]["name"])    # Output: Linus
```

### Looping Through a Nested Dictionary

```python
for child_key, child_info in myfamily.items():
    print("Key:", child_key)
    for detail_key, detail_value in child_info.items():
        print("  ", detail_key, ":", detail_value)
```

**Expected Output:**
```
Key: child1
   name : Emil
   year : 2004
Key: child2
   name : Tobias
   year : 2007
Key: child3
   name : Linus
   year : 2011
```

**Line-by-line explanation:**
- The outer loop goes through the family dictionary and assigns each child's key (`"child1"`, etc.) to `child_key`, and the inner dictionary to `child_info`
- The inner loop then goes through each inner dictionary's items
- The `"  "` (two spaces) indents the inner output to visually show the hierarchy

> **Real-world use:** This pattern is used everywhere — when an app processes JSON data from a web API, when a program reads a configuration file, when a database returns records with sub-fields. Nested dictionaries are the backbone of modern data handling.

---

## Guided Practice Exercises

### Exercise 1 — Build a Student Profile

**Objective:** Create and access a dictionary representing a student's record.

**Scenario:** You're building a simple student management system. Each student has a name, age, subject, and grade.

**Steps:**
1. Create a dictionary called `student` with keys: `"name"`, `"age"`, `"subject"`, `"grade"`
2. Fill in values of your choice
3. Print the full dictionary
4. Print only the student's name
5. Print only the grade

**Starter Code:**
```python
student = {
    "name": "Amara",
    "age": 18,
    "subject": "Mathematics",
    "grade": "A"
}

# Step 3
print(student)

# Step 4
print(student["name"])

# Step 5
print(student["grade"])
```

**Expected Output:**
```
{'name': 'Amara', 'age': 18, 'subject': 'Mathematics', 'grade': 'A'}
Amara
A
```

**Self-check:** Can you also print the student's subject using `.get()` instead of square brackets?

---

### Exercise 2 — Update and Expand a Dictionary

**Objective:** Practice changing and adding values.

**Scenario:** A student just changed their subject and also got their exam score recorded.

**Steps:**
1. Start with the student dictionary from Exercise 1
2. Update `"subject"` to `"Physics"`
3. Add a new key `"score"` with value `95`
4. Print the updated dictionary

```python
student = {
    "name": "Amara",
    "age": 18,
    "subject": "Mathematics",
    "grade": "A"
}

student["subject"] = "Physics"    # Change existing value
student["score"] = 95             # Add new key

print(student)
```

**Expected Output:**
```
{'name': 'Amara', 'age': 18, 'subject': 'Physics', 'grade': 'A', 'score': 95}
```

**What-if challenge:** What happens if you try `student.update({"grade": "B", "score": 88})`? Try it!

---

### Exercise 3 — Remove Items Safely

**Objective:** Practice the different removal methods.

**Scenario:** The school's system needs to remove certain fields from a student record.

```python
student = {
    "name": "Amara",
    "age": 18,
    "subject": "Physics",
    "grade": "A",
    "score": 95
}

# Remove "score" using pop and capture the removed value
removed_score = student.pop("score")
print("Removed score:", removed_score)
print("After pop:", student)

# Remove the last added item
student.popitem()
print("After popitem:", student)

# Remove "age" using del
del student["age"]
print("After del:", student)
```

**Expected Output:**
```
Removed score: 95
After pop: {'name': 'Amara', 'age': 18, 'subject': 'Physics', 'grade': 'A'}
After popitem: {'name': 'Amara', 'age': 18, 'subject': 'Physics'}
After del: {'name': 'Amara', 'subject': 'Physics'}
```

---

### Exercise 4 — Loop and Report

**Objective:** Use a loop to generate a readable report from a dictionary.

**Scenario:** Print a formatted summary of a product.

```python
product = {
    "name": "Laptop",
    "brand": "TechPro",
    "price": 750,
    "in_stock": True,
    "weight_kg": 1.8
}

print("=== Product Report ===")
for field, info in product.items():
    print(f"{field}: {info}")
```

**Expected Output:**
```
=== Product Report ===
name: Laptop
brand: TechPro
price: 750
in_stock: True
weight_kg: 1.8
```

**Note on `f"{field}: {info}"`:** This is an f-string — a convenient way to embed variable values inside a string. The variables go inside the curly braces.

---

### Exercise 5 — Safe vs. Unsafe Copy

**Objective:** Observe the difference between reference assignment and a real copy.

```python
original = {"city": "Lagos", "country": "Nigeria", "population": 15000000}

# Unsafe — both variables point to the same object
unsafe_copy = original
unsafe_copy["population"] = 999

print("Original after unsafe copy change:", original)
# "population" is 999 — the original was modified!

# Now reset and do a safe copy
original = {"city": "Lagos", "country": "Nigeria", "population": 15000000}
safe_copy = original.copy()
safe_copy["population"] = 999

print("Original after safe copy change:", original)
# "population" is still 15000000 — original is untouched!
print("Safe copy:", safe_copy)
```

**Expected Output:**
```
Original after unsafe copy change: {'city': 'Lagos', 'country': 'Nigeria', 'population': 999}
Original after safe copy change: {'city': 'Lagos', 'country': 'Nigeria', 'population': 15000000}
Safe copy: {'city': 'Lagos', 'country': 'Nigeria', 'population': 999}
```

---

## Mini Project: Student Grade Book

In this project, you'll build a small grade book program that stores student data in nested dictionaries and generates a report.

### Project Overview

You will create a grade book where:
- Each student has a name, subject scores, and a calculated average
- The system can display a full report
- You can look up a specific student's info

### Stage 1 — Setup: Create the Grade Book

```python
gradebook = {
    "Alice": {
        "math": 88,
        "science": 92,
        "english": 75
    },
    "Bob": {
        "math": 70,
        "science": 65,
        "english": 80
    },
    "Chisom": {
        "math": 95,
        "science": 91,
        "english": 98
    }
}
```

**Milestone check:** Print the entire gradebook to confirm it was set up correctly.

```python
print(gradebook)
```

---

### Stage 2 — Core Logic: Calculate and Display Averages

```python
print("======= GRADE BOOK REPORT =======\n")

for student_name, scores in gradebook.items():
    print(f"Student: {student_name}")
    
    total = 0
    for subject, score in scores.items():
        print(f"  {subject.capitalize()}: {score}")
        total += score
    
    average = total / len(scores)
    print(f"  Average Score: {average:.1f}")
    print()   # blank line between students
```

**Expected Output:**
```
======= GRADE BOOK REPORT =======

Student: Alice
  Math: 88
  Science: 92
  English: 75
  Average Score: 85.0

Student: Bob
  Math: 70
  Science: 65
  English: 80
  Average Score: 71.7

Student: Chisom
  Math: 95
  Science: 91
  English: 98
  Average Score: 94.7
```

**Line-by-line explanation of key parts:**
- `total = 0` — we start a counter at zero for each student
- `total += score` — adds each subject score to the running total
- `average = total / len(scores)` — divides the total by the number of subjects to get the average
- `f"  Average Score: {average:.1f}"` — `:.1f` formats the number to 1 decimal place
- `.capitalize()` — makes the first letter uppercase (e.g., "math" → "Math")

---

### Stage 3 — Enhancement: Look Up a Single Student

```python
def lookup_student(gradebook, name):
    if name in gradebook:
        print(f"\n--- {name}'s Scores ---")
        for subject, score in gradebook[name].items():
            print(f"  {subject.capitalize()}: {score}")
    else:
        print(f"Student '{name}' not found in the grade book.")

lookup_student(gradebook, "Bob")
lookup_student(gradebook, "David")
```

**Expected Output:**
```
--- Bob's Scores ---
  Math: 70
  Science: 65
  English: 80

Student 'David' not found in the grade book.
```

---

### Stage 4 — Enhancement: Add a New Student

```python
def add_student(gradebook, name, scores):
    gradebook[name] = scores
    print(f"Student '{name}' added successfully.")

add_student(gradebook, "Diana", {"math": 82, "science": 79, "english": 88})
lookup_student(gradebook, "Diana")
```

**Expected Output:**
```
Student 'Diana' added successfully.

--- Diana's Scores ---
  Math: 82
  Science: 79
  English: 88
```

### Reflection Questions

1. What would happen if two students had the same name? How would the dictionary behave?
2. How would you modify the code to assign a letter grade (A, B, C) based on the average?
3. Can you add a function to find the **top-performing student**?

**Optional Extension:** Try adding a `remove_student(gradebook, name)` function that uses `.pop()` to remove a student.

---

## Common Beginner Mistakes

### Mistake 1 — Using a List Index Style on a Dictionary

```python
# WRONG
mydict = {"name": "Alice", "age": 25}
print(mydict[0])    # KeyError! Dictionaries don't use numbers as positions
```

**Fix:**
```python
print(mydict["name"])    # Correct — use the key name
```

### Mistake 2 — Forgetting Quotes Around String Keys

```python
# WRONG
mydict = {name: "Alice"}    # NameError — Python looks for a variable called name

# CORRECT
mydict = {"name": "Alice"}  # Key is a string — must have quotes
```

### Mistake 3 — Using Duplicate Keys

```python
# WRONG — duplicate key
config = {
    "timeout": 30,
    "timeout": 60    # This silently overwrites 30!
}
print(config["timeout"])   # Output: 60 — you lost 30!
```

**Fix:** Use distinct, meaningful key names.

### Mistake 4 — Confusing `=` (assign) with Updating

```python
# You can't do this for a new key
mydict["new_key"]    # KeyError — you must assign a value

# Correct
mydict["new_key"] = "some value"
```

### Mistake 5 — Shallow Copy Trap with Nested Dictionaries

```python
original = {"info": {"city": "Abuja"}}
copy = original.copy()
copy["info"]["city"] = "Lagos"

print(original["info"]["city"])   # Output: Lagos — original was changed!
```

**Why?** `.copy()` only copies the outer dictionary. The inner dictionary is still shared. For fully independent copies of nested dictionaries, you need `copy.deepcopy()` from Python's `copy` module:

```python
import copy
original = {"info": {"city": "Abuja"}}
safe_copy = copy.deepcopy(original)
safe_copy["info"]["city"] = "Lagos"
print(original["info"]["city"])   # Output: Abuja — original safe!
```

### Mistake 6 — Accessing a Non-Existent Key with Square Brackets

```python
mydict = {"name": "Alice"}
print(mydict["age"])    # KeyError: 'age'
```

**Fix — use `.get()` with a default value:**

```python
print(mydict.get("age", "Not specified"))   # Output: Not specified
```

The second argument to `.get()` is the default value returned when the key doesn't exist.

---

## Reflection Questions

Test your understanding by thinking through these questions:

1. What is the difference between a list and a dictionary in Python? When would you choose one over the other?
2. Why does Python not allow duplicate keys in a dictionary?
3. What is the difference between `.pop("key")` and `.popitem()`?
4. Why is `dict2 = dict1` dangerous, and what should you use instead?
5. What does `.items()` return, and why is it useful in a loop?
6. If you nest a dictionary inside another dictionary, how do you access a value in the inner dictionary?
7. What is the difference between using `.get("key")` and `dict["key"]`?
8. In what real-world situation would you use a nested dictionary?

---

## Completion Checklist

Before moving to the next lesson, confirm that you can:

- [ ] Create a dictionary using curly brackets `{}` and the `dict()` constructor
- [ ] Access dictionary values using square bracket notation and `.get()`
- [ ] Use `.keys()`, `.values()`, and `.items()` to view dictionary contents
- [ ] Check whether a key exists using `in`
- [ ] Change existing values using direct assignment and `.update()`
- [ ] Add new key-value pairs to a dictionary
- [ ] Remove items using `.pop()`, `.popitem()`, `del`, and `.clear()`
- [ ] Loop through a dictionary using all four loop patterns
- [ ] Create a safe copy using `.copy()` or `dict()`
- [ ] Create a nested dictionary and access values inside it
- [ ] Loop through a nested dictionary with a double loop
- [ ] Explain at least 3 common beginner mistakes and how to avoid them
- [ ] Complete the mini project (Grade Book)

---

## Lesson Summary

Congratulations — you've completed one of the most important lessons in Python!

Here's what you now know:

**Dictionaries** are ordered (Python 3.7+), changeable, and do not allow duplicate keys. They store data as `key: value` pairs inside curly braces `{}`.

**Creating:** Use `{key: value}` syntax or the `dict()` constructor.

**Accessing:** Use `dict["key"]` or the safer `dict.get("key")`. View all keys with `.keys()`, all values with `.values()`, and all pairs with `.items()`.

**Changing:** Assign directly with `dict["key"] = new_value` or use `.update({})` for multiple changes at once.

**Adding:** Same syntax as changing — if the key doesn't exist, it gets created.

**Removing:** Use `.pop("key")` to remove by name and get the value back, `.popitem()` to remove the last item, `del dict["key"]` to delete by key, and `.clear()` to empty the whole dictionary.

**Looping:** Loop over keys (default), `.keys()`, `.values()`, or `.items()` for key-value pairs together.

**Copying:** Never use `dict2 = dict1`. Always use `dict2 = dict1.copy()` or `dict2 = dict(dict1)`.

**Nesting:** Dictionaries can contain other dictionaries. Access nested values by chaining square brackets: `outer["key1"]["key2"]`.

> **What's next?** In the next lesson, you'll encounter `if/else` statements — which pair beautifully with dictionaries to build programs that make decisions based on stored data.

---

*Sources: W3Schools Python Dictionary Tutorials (python_dictionaries.asp through python_dictionaries_nested.asp)*
