---
render_with_liquid: false
title: "Lesson 14: Python Dictionaries — The Complete Beginner's Guide"
nav_order: 14
---

# Lesson 14: Python Dictionaries — The Complete Beginner's Guide

---

## Lesson Introduction

Welcome to one of the most powerful and useful lessons in your Python journey!

In this lesson, you will learn all about **Python dictionaries** — one of Python's four built-in collection types. By the end, you will be able to create, read, change, add to, remove from, loop through, copy, and nest dictionaries. You will also learn all the built-in methods dictionaries come with.

Think of a dictionary as a **real-world contact book**. When you look up a person, you don't flip through every single page — you search by their **name** (the key) and instantly find their **phone number** (the value). That's exactly how Python dictionaries work: they store data in **key-value pairs**, making lookups fast and meaningful.

Dictionaries are used everywhere in real-world software:
- **Web development**: storing user profile data (`{"username": "ada", "email": "ada@example.com"}`)
- **Data science**: storing experiment results with labels
- **APIs & JSON**: most web API responses are dictionary-like structures
- **Configuration files**: storing settings like `{"theme": "dark", "language": "en"}`

This lesson covers all 10 W3Schools dictionary pages, merged into one smooth progressive lesson.

---

## What You Need to Know First (Prerequisites)

Before diving in, make sure you are comfortable with:

- **Variables**: storing values like `x = 5`
- **Strings**: text in quotes like `"hello"`
- **Lists**: ordered collections like `[1, 2, 3]`
- **For loops**: repeating actions like `for item in my_list:`
- **The `print()` function**: displaying output

If any of these feel shaky, briefly review your earlier lessons first. This lesson will build naturally on all of them.

---

## Part 1: What Is a Dictionary?

### The Concept: Key-Value Pairs

A **dictionary** is a collection that stores data as **key-value pairs**. Every single item inside a dictionary has two parts:

- A **key** — the label or name you use to find the item (like a word in a real dictionary)
- A **value** — the actual data attached to that key (like the definition of the word)

**Analogy:** Imagine a school's attendance register:

| Student Name (Key) | Present/Absent (Value) |
|--------------------|------------------------|
| Amina              | Present                |
| Tunde              | Absent                 |
| Chidi              | Present                |

You look up a student by their **name** (key) to find their **status** (value). That's a dictionary.

### The Four Collection Types in Python

Python has four collection data types. It's important to know how they differ:

| Collection  | Ordered? | Changeable? | Duplicates? |
|-------------|----------|-------------|-------------|
| List        | Yes      | Yes         | Yes         |
| Tuple       | Yes      | No          | Yes         |
| Set         | No       | No*         | No          |
| **Dictionary** | **Yes** (Python 3.7+) | **Yes** | **No** |

> **Note:** As of Python 3.7, dictionaries are **ordered**, meaning items stay in the order you add them. In Python 3.6 and earlier, dictionaries were unordered.

---

## Part 2: Creating a Dictionary

### How to Write a Dictionary

Dictionaries are written with **curly brackets `{}`**. Inside the curly brackets, you write your key-value pairs separated by commas. Each key and its value are separated by a **colon `:`**.

**The syntax:**
```python
my_dict = {
    "key1": value1,
    "key2": value2,
    "key3": value3
}
```

### Your First Dictionary — Simple Example

```python
# A dictionary about a car
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

Let's break down every part:
- `thisdict` — the variable name that holds the whole dictionary
- `{` — opens the dictionary
- `"brand"` — a **key** (it's a string, so it has quotes)
- `:` — the separator between key and value
- `"Ford"` — a **value** (also a string here)
- `,` — separates one key-value pair from the next
- `}` — closes the dictionary

### Dictionaries Can Hold Many Data Types

The **values** in a dictionary can be any data type — strings, integers, booleans, lists, even other dictionaries!

```python
student = {
    "name": "Amina",        # string value
    "age": 17,              # integer value
    "is_enrolled": True,    # boolean value
    "grades": [85, 90, 78]  # list value
}
print(student)
```

**Expected Output:**
```
{'name': 'Amina', 'age': 17, 'is_enrolled': True, 'grades': [85, 90, 78]}
```

> **Think about this:** What would happen if you tried to store the same key twice? Try it mentally first, then see below.

### Duplicate Keys Are Not Allowed

Dictionaries **cannot have two items with the same key**. If you try, the second value will silently overwrite the first one — Python will not warn you!

```python
# Danger: duplicate keys
thisdict = {
    "brand": "Ford",
    "model": "Mustang",
    "year": 1964,
    "year": 2020    # "year" appears twice!
}
print(thisdict)
```

**Expected Output:**
```
{'brand': 'Ford', 'model': 'Mustang', 'year': 2020}
```

Notice `1964` is completely gone. The second `"year": 2020` **replaced** it silently. This is a very common beginner mistake — always double-check your keys!

### Checking the Length of a Dictionary

Use the built-in `len()` function to count how many items (key-value pairs) a dictionary has:

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

### Checking the Data Type

From Python's perspective, dictionaries are objects of type `dict`. You can confirm this with `type()`:

```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}
print(type(thisdict))
```

**Expected Output:**
```
<class 'dict'>
```

### Creating a Dictionary with the `dict()` Constructor

There's an alternative way to create a dictionary using the `dict()` built-in function. Instead of curly brackets and quotes for keys, you use keyword arguments:

```python
# Using dict() constructor
person = dict(name="John", age=36, country="Norway")
print(person)
```

**Expected Output:**
```
{'name': 'John', 'age': 36, 'country': 'Norway'}
```

> **Notice:** When using `dict()`, you do NOT put quotes around the key names. `name="John"` not `"name"="John"`.

**Second example — a student record:**
```python
course = dict(title="Biology", code="BIO101", credits=3)
print(course)
```

**Expected Output:**
```
{'title': 'Biology', 'code': 'BIO101', 'credits': 3}
```

---

## Part 3: Accessing Dictionary Items

Now that you can create a dictionary, let's learn how to **read** its values.

### Method 1 — Square Bracket Notation

The most direct way to get a value is to write the dictionary name followed by the **key** in square brackets:

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

**Explanation:** `thisdict["model"]` says: "go into `thisdict` and bring me the value whose key is `"model"`."

**Second example:**
```python
# Getting the year
print(thisdict["year"])
```

**Expected Output:**
```
1964
```

### Method 2 — The `.get()` Method

The `.get()` method does the same thing as square brackets, but it is **safer** for situations where you're not sure if the key exists:

```python
x = thisdict.get("model")
print(x)
```

**Expected Output:**
```
Mustang
```

**Why is `.get()` safer?** If you use square brackets with a key that doesn't exist, Python raises a `KeyError` and crashes. With `.get()`, Python simply returns `None` (or a default value you specify), and your program keeps running.

```python
# Square brackets — will CRASH if key doesn't exist
# print(thisdict["color"])   # KeyError: 'color'

# .get() — returns None safely
print(thisdict.get("color"))
```

**Expected Output:**
```
None
```

You can also provide a **default value** as the second argument to `.get()`:

```python
print(thisdict.get("color", "Not specified"))
```

**Expected Output:**
```
Not specified
```

### Getting All the Keys — `.keys()`

The `.keys()` method returns a special **view** of all the keys in the dictionary:

```python
thisdict = {
    "brand": "Ford",
    "model": "Mustang",
    "year": 1964
}

x = thisdict.keys()
print(x)
```

**Expected Output:**
```
dict_keys(['brand', 'model', 'year'])
```

**Important:** This is a **live view**, not a copy. If you add a new key to the original dictionary, the keys view updates automatically:

```python
car = {"brand": "Ford", "model": "Mustang", "year": 1964}
x = car.keys()

print(x)           # Before the change
car["color"] = "white"
print(x)           # After the change
```

**Expected Output:**
```
dict_keys(['brand', 'model', 'year'])
dict_keys(['brand', 'model', 'year', 'color'])
```

> **Think about this:** Why would this "live view" behaviour be useful? Imagine you're monitoring a system where settings change often — you always want the latest list of keys without having to re-call the method.

### Getting All the Values — `.values()`

The `.values()` method returns a live view of all the **values** in the dictionary:

```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}
x = thisdict.values()
print(x)
```

**Expected Output:**
```
dict_values(['Ford', 'Mustang', 1964])
```

Like `.keys()`, this is a live view that updates when the dictionary changes:

```python
car = {"brand": "Ford", "model": "Mustang", "year": 1964}
x = car.values()

print(x)           # Before
car["year"] = 2020
print(x)           # After — notice 2020 is now there
```

**Expected Output:**
```
dict_values(['Ford', 'Mustang', 1964])
dict_values(['Ford', 'Mustang', 2020])
```

### Getting All Key-Value Pairs — `.items()`

The `.items()` method returns each key-value pair as a **tuple** inside a list-like view:

```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}
x = thisdict.items()
print(x)
```

**Expected Output:**
```
dict_items([('brand', 'Ford'), ('model', 'Mustang'), ('year', 1964)])
```

Each item is a **tuple** — for example, `('brand', 'Ford')`. This format becomes extremely useful when you loop through dictionaries (covered in Part 8).

This is also a live view:

```python
car = {"brand": "Ford", "model": "Mustang", "year": 1964}
x = car.items()

print(x)           # Before
car["color"] = "red"
print(x)           # After — notice the new pair appears
```

**Expected Output:**
```
dict_items([('brand', 'Ford'), ('model', 'Mustang'), ('year', 1964)])
dict_items([('brand', 'Ford'), ('model', 'Mustang'), ('year', 1964), ('color', 'red')])
```

### Checking if a Key Exists — the `in` Keyword

Before accessing a key, you may want to check if it even exists. Use the `in` keyword:

```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}

if "model" in thisdict:
    print("Yes, 'model' is one of the keys in the dictionary")
```

**Expected Output:**
```
Yes, 'model' is one of the keys in the dictionary
```

**Checking for a key that does NOT exist:**
```python
if "color" in thisdict:
    print("color found")
else:
    print("color NOT found")
```

**Expected Output:**
```
color NOT found
```

> **Real-world use:** In a login system, before accessing `user["email"]`, you would first check `if "email" in user:` to prevent crashes.

---

## Part 4: Changing Dictionary Items

Dictionaries are **mutable** — that means you can change, update, add, and remove items after creation.

### Changing a Value by Key

To change a specific value, simply refer to the key and assign a new value:

```python
thisdict = {
    "brand": "Ford",
    "model": "Mustang",
    "year": 1964
}

thisdict["year"] = 2018   # Update the value for key "year"
print(thisdict)
```

**Expected Output:**
```
{'brand': 'Ford', 'model': 'Mustang', 'year': 2018}
```

**Explanation:** `thisdict["year"] = 2018` finds the key `"year"` in the dictionary and replaces its value with `2018`.

**Second example — updating a student's grade:**
```python
student = {"name": "Tunde", "subject": "Maths", "score": 65}
student["score"] = 78   # Tunde improved!
print(student)
```

**Expected Output:**
```
{'name': 'Tunde', 'subject': 'Maths', 'score': 78}
```

### Using the `.update()` Method

The `.update()` method lets you update one or more values at the same time. You pass it a dictionary with the key(s) you want to change:

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

**Updating multiple values at once:**
```python
employee = {"name": "Grace", "department": "IT", "salary": 50000}
employee.update({"department": "Engineering", "salary": 65000})
print(employee)
```

**Expected Output:**
```
{'name': 'Grace', 'department': 'Engineering', 'salary': 65000}
```

> **Why use `.update()` over direct assignment?** When you want to update several keys at once, `.update()` is cleaner. Also, if you pass it a key that doesn't yet exist, it will **add** it as a new item — making it a versatile method.

---

## Part 5: Adding Items to a Dictionary

### Adding a New Key-Value Pair

To add a completely new item to a dictionary, simply assign a value to a **new key** that doesn't exist yet:

```python
thisdict = {
    "brand": "Ford",
    "model": "Mustang",
    "year": 1964
}

thisdict["color"] = "red"   # Adding a brand new key-value pair
print(thisdict)
```

**Expected Output:**
```
{'brand': 'Ford', 'model': 'Mustang', 'year': 1964, 'color': 'red'}
```

**Explanation:** Since `"color"` didn't exist before, Python adds it as a new entry at the end of the dictionary.

**Second example — adding items to a shopping cart:**
```python
cart = {"apples": 3, "bread": 1}
cart["milk"] = 2      # Adding milk
cart["eggs"] = 12     # Adding eggs
print(cart)
```

**Expected Output:**
```
{'apples': 3, 'bread': 1, 'milk': 2, 'eggs': 12}
```

### Adding with `.update()`

You can also use the `.update()` method to add new items. If the key already exists, it updates the value; if it doesn't exist, it adds a new entry:

```python
thisdict = {
    "brand": "Ford",
    "model": "Mustang",
    "year": 1964
}

thisdict.update({"color": "white"})   # "color" is new, so it gets added
print(thisdict)
```

**Expected Output:**
```
{'brand': 'Ford', 'model': 'Mustang', 'year': 1964, 'color': 'white'}
```

> **Remember the rule:** Direct assignment (`dict["key"] = value`) and `.update({"key": value})` both work for adding new items. The difference is `.update()` lets you add or update multiple keys at once.

---

## Part 6: Removing Items from a Dictionary

There are several ways to remove items from a dictionary. Let's cover all of them.

### Method 1 — `.pop(key)` — Remove a Specific Key

The `.pop()` method removes the item with the specified key and **returns** the removed value:

```python
thisdict = {
    "brand": "Ford",
    "model": "Mustang",
    "year": 1964
}

thisdict.pop("model")
print(thisdict)
```

**Expected Output:**
```
{'brand': 'Ford', 'year': 1964}
```

You can also capture the removed value:

```python
removed = thisdict.pop("brand")
print("Removed:", removed)
print("Remaining:", thisdict)
```

**Expected Output:**
```
Removed: Ford
Remaining: {'year': 1964}
```

### Method 2 — `.popitem()` — Remove the Last Inserted Item

The `.popitem()` method removes the **last inserted** key-value pair. It returns that pair as a tuple:

```python
thisdict = {
    "brand": "Ford",
    "model": "Mustang",
    "year": 1964
}

thisdict.popitem()   # Removes ("year", 1964) — the last item
print(thisdict)
```

**Expected Output:**
```
{'brand': 'Ford', 'model': 'Mustang'}
```

> **Note:** In Python 3.7 and later, `.popitem()` always removes the **last** inserted item. In older versions, it removed a random item.

### Method 3 — `del` Keyword — Remove by Key or Delete the Whole Dictionary

The `del` keyword can remove a specific item or delete the entire dictionary:

**Removing a specific key:**
```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}
del thisdict["model"]
print(thisdict)
```

**Expected Output:**
```
{'brand': 'Ford', 'year': 1964}
```

**Deleting the entire dictionary:**
```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}
del thisdict
# print(thisdict)   # This would cause a NameError — thisdict no longer exists!
```

> **Warning:** After `del thisdict`, the variable `thisdict` no longer exists at all. Trying to use it will give a `NameError`. This is different from clearing it.

### Method 4 — `.clear()` — Empty the Dictionary

The `.clear()` method removes **all items** from the dictionary, but the dictionary variable itself still exists (it just becomes empty):

```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}
thisdict.clear()
print(thisdict)
```

**Expected Output:**
```
{}
```

**Comparison of del vs clear:**
```python
# .clear() — dictionary still exists, but is empty
my_dict = {"a": 1, "b": 2}
my_dict.clear()
print(my_dict)    # {} — empty but still exists

# del — dictionary is completely gone
my_dict2 = {"a": 1, "b": 2}
del my_dict2
# print(my_dict2) # NameError!
```

---

## Part 7: Looping Through a Dictionary

Looping (iterating) through a dictionary is one of the most commonly used operations in real programs.

### Loop 1 — Loop Through Keys (Default Behaviour)

When you use a `for` loop on a dictionary directly, Python loops through the **keys** by default:

```python
thisdict = {
    "brand": "Ford",
    "model": "Mustang",
    "year": 1964
}

for x in thisdict:
    print(x)
```

**Expected Output:**
```
brand
model
year
```

Only the **keys** are printed, not the values.

### Loop 2 — Loop Through Values

To print values, you have two options:

**Option A — Use the key inside the loop:**
```python
for x in thisdict:
    print(thisdict[x])
```

**Expected Output:**
```
Ford
Mustang
1964
```

**Option B — Use `.values()` directly:**
```python
for x in thisdict.values():
    print(x)
```

**Expected Output:**
```
Ford
Mustang
1964
```

### Loop 3 — Loop Through Keys with `.keys()`

You can be explicit and loop through keys using `.keys()`:

```python
for x in thisdict.keys():
    print(x)
```

**Expected Output:**
```
brand
model
year
```

### Loop 4 — Loop Through Both Keys and Values Together

The most useful loop uses `.items()`, which gives you both the key **and** the value together in each iteration:

```python
for key, value in thisdict.items():
    print(key, value)
```

**Expected Output:**
```
brand Ford
model Mustang
year 1964
```

**Explanation:** Each time through the loop, Python unpacks the tuple `('brand', 'Ford')` into two variables: `key` gets `'brand'` and `value` gets `'Ford'`.

**Real-world example — printing a formatted student report:**
```python
student = {
    "name": "Chidi",
    "subject": "Physics",
    "score": 88,
    "grade": "A"
}

for key, value in student.items():
    print(f"{key}: {value}")
```

**Expected Output:**
```
name: Chidi
subject: Physics
score: 88
grade: A
```

> **Thinking prompt:** What would happen if you used `for key, value in thisdict:` without `.items()`? Try to predict it, then test it — you'll get a `ValueError: too many values to unpack`.

---

## Part 8: Copying a Dictionary

### Why Can't You Just Use `=`?

You might think `copy = original` would create a separate copy, but in Python, this does NOT create a true copy. It creates a **reference** — both variables point to the exact same object in memory. Changing one will change the other!

```python
original = {"a": 1, "b": 2}
copy = original       # This is NOT a real copy — it's just another name

copy["a"] = 999
print(original)       # The original was also changed!
print(copy)
```

**Expected Output:**
```
{'a': 999, 'b': 2}
{'a': 999, 'b': 2}
```

This is a very common source of bugs for beginners!

### Method 1 — `.copy()` — Create a True Copy

The `.copy()` method creates a **new, independent** dictionary with the same items:

```python
thisdict = {
    "brand": "Ford",
    "model": "Mustang",
    "year": 1964
}

mydict = thisdict.copy()    # True independent copy

mydict["year"] = 2024       # Change the copy
print(thisdict)             # Original is unchanged
print(mydict)               # Copy has the new value
```

**Expected Output:**
```
{'brand': 'Ford', 'model': 'Mustang', 'year': 1964}
{'brand': 'Ford', 'model': 'Mustang', 'year': 2024}
```

### Method 2 — `dict()` — Create a Copy Using the Constructor

You can also pass an existing dictionary into `dict()` to create a copy:

```python
thisdict = {"brand": "Ford", "model": "Mustang", "year": 1964}

mydict = dict(thisdict)   # Creates a new, independent dictionary

mydict["brand"] = "Toyota"
print(thisdict)            # Original unchanged
print(mydict)              # Copy has new value
```

**Expected Output:**
```
{'brand': 'Ford', 'model': 'Mustang', 'year': 1964}
{'brand': 'Toyota', 'model': 'Mustang', 'year': 1964}
```

> **Rule to remember:** If you need an independent copy of a dictionary, always use `.copy()` or `dict()`. Never use plain `=` for copying.

---

## Part 9: Nested Dictionaries

### What Is a Nested Dictionary?

A **nested dictionary** is a dictionary that contains other dictionaries as values. Think of it like a filing cabinet where each drawer (outer dictionary) contains folders (inner dictionaries) full of documents (data).

**Real-world analogy:** A school database might have a dictionary of students, where each student's record is itself a dictionary.

### Creating a Nested Dictionary — Method 1: Direct

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

### Creating a Nested Dictionary — Method 2: From Existing Dictionaries

You can also create separate dictionaries first, then combine them:

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

### Accessing Items in a Nested Dictionary

To access a value deep inside a nested dictionary, you **chain** the key lookups:

```python
# Get "Emil" — the name of child1
print(myfamily["child1"]["name"])
```

**Expected Output:**
```
Emil
```

**Step-by-step breakdown:**
1. `myfamily["child1"]` → gives you `{"name": "Emil", "year": 2004}`
2. `["name"]` → gives you `"Emil"`

**More examples:**
```python
print(myfamily["child2"]["year"])   # Get the year of child2
print(myfamily["child3"]["name"])   # Get the name of child3
```

**Expected Output:**
```
2007
Linus
```

### Looping Through a Nested Dictionary

```python
for child_key, child_info in myfamily.items():
    print(f"\n{child_key}:")
    for detail_key, detail_value in child_info.items():
        print(f"  {detail_key}: {detail_value}")
```

**Expected Output:**
```
child1:
  name: Emil
  year: 2004

child2:
  name: Tobias
  year: 2007

child3:
  name: Linus
  year: 2011
```

**Explanation of the double loop:**
- The **outer loop** goes through each child (`child1`, `child2`, `child3`)
- The **inner loop** goes through each detail inside each child's dictionary (`name`, `year`)

> **Real-world use:** Nested dictionaries are the backbone of JSON data from APIs. When you call a weather API or a stock price API, the response is almost always a nested dictionary structure.

---

## Part 10: Dictionary Methods — The Complete Reference

Python dictionaries come with many built-in methods. Here is every one of them explained clearly.

### 1. `.clear()` — Remove All Items

Empties the dictionary completely. The variable remains, but becomes `{}`.

```python
car = {"brand": "Ford", "model": "Mustang"}
car.clear()
print(car)
```
**Output:** `{}`

### 2. `.copy()` — Return a Shallow Copy

Creates an independent copy of the dictionary.

```python
original = {"a": 1, "b": 2}
backup = original.copy()
backup["c"] = 3
print(original)   # {"a": 1, "b": 2} — untouched
print(backup)     # {"a": 1, "b": 2, "c": 3}
```

### 3. `dict.fromkeys(keys, value)` — Create a Dictionary from Keys

Creates a new dictionary from a list of keys. All keys get the same value. If no value is given, `None` is used.

```python
# Create a dict with all keys set to the same value
keys = ("name", "age", "city")
new_dict = dict.fromkeys(keys, "unknown")
print(new_dict)
```

**Expected Output:**
```
{'name': 'unknown', 'age': 'unknown', 'city': 'unknown'}
```

**Without a value — defaults to None:**
```python
result = dict.fromkeys(["a", "b", "c"])
print(result)
```

**Expected Output:**
```
{'a': None, 'b': None, 'c': None}
```

**Real-world use:** Quickly initialise a dictionary with default values, like setting all test scores to 0.

```python
subjects = ["Maths", "English", "Science", "History"]
scores = dict.fromkeys(subjects, 0)
print(scores)
```

**Expected Output:**
```
{'Maths': 0, 'English': 0, 'Science': 0, 'History': 0}
```

### 4. `.get(key, default)` — Get Value Safely

Returns the value for a key. Returns `None` (or your specified default) if the key doesn't exist. Prevents crashes.

```python
car = {"brand": "Ford", "year": 1964}
print(car.get("brand"))             # Ford
print(car.get("color"))             # None
print(car.get("color", "Unknown"))  # Unknown
```

### 5. `.items()` — Get All Key-Value Pairs

Returns a view of all key-value pairs as tuples. This is the primary tool for looping through a dictionary's contents.

```python
car = {"brand": "Ford", "model": "Mustang", "year": 1964}
print(car.items())
```

**Expected Output:**
```
dict_items([('brand', 'Ford'), ('model', 'Mustang'), ('year', 1964)])
```

### 6. `.keys()` — Get All Keys

Returns a live view of all keys.

```python
car = {"brand": "Ford", "model": "Mustang", "year": 1964}
print(car.keys())
```

**Expected Output:**
```
dict_keys(['brand', 'model', 'year'])
```

### 7. `.pop(key, default)` — Remove and Return a Value

Removes the specified key and returns its value. If the key is not found and no default is given, it raises a `KeyError`.

```python
car = {"brand": "Ford", "model": "Mustang", "year": 1964}
removed = car.pop("model")
print(removed)   # Mustang
print(car)       # {'brand': 'Ford', 'year': 1964}
```

**With a default (prevents crash if key missing):**
```python
result = car.pop("color", "Not found")
print(result)    # Not found
```

### 8. `.popitem()` — Remove and Return the Last Item

Removes and returns the **last inserted** key-value pair as a tuple.

```python
car = {"brand": "Ford", "model": "Mustang", "year": 1964}
item = car.popitem()
print(item)    # ('year', 1964)
print(car)     # {'brand': 'Ford', 'model': 'Mustang'}
```

### 9. `.setdefault(key, default)` — Get a Value or Set a Default

Returns the value of a key. If the key does not exist, it **inserts** the key with the given default value and returns that default.

```python
car = {"brand": "Ford", "model": "Mustang"}

# Key "model" already exists — returns its value
x = car.setdefault("model", "Bronco")
print(x)      # Mustang (original value kept)
print(car)    # {'brand': 'Ford', 'model': 'Mustang'}

# Key "color" does NOT exist — inserts it with the default
y = car.setdefault("color", "white")
print(y)      # white
print(car)    # {'brand': 'Ford', 'model': 'Mustang', 'color': 'white'}
```

### 10. `.update(iterable)` — Add or Update Items

Updates the dictionary with items from another dictionary or iterable of key-value pairs. Existing keys are updated; new keys are added.

```python
car = {"brand": "Ford", "model": "Mustang", "year": 1964}
car.update({"year": 2020, "color": "blue"})
print(car)
```

**Expected Output:**
```
{'brand': 'Ford', 'model': 'Mustang', 'year': 2020, 'color': 'blue'}
```

### 11. `.values()` — Get All Values

Returns a live view of all values.

```python
car = {"brand": "Ford", "model": "Mustang", "year": 1964}
print(car.values())
```

**Expected Output:**
```
dict_values(['Ford', 'Mustang', 1964])
```

---

## Part 11: Guided Practice Exercises

Work through these carefully. Try each one yourself before looking at the solution.

---

### Exercise 1: Build a Student Profile

**Objective:** Create and print a dictionary.

**Scenario:** You are building a school database system. Store the following information about a student:
- Name: Fatima
- Age: 16
- Class: JSS3
- Subject favourite: Biology
- Score: 92

**Steps:**
1. Create a dictionary called `student` with all five details.
2. Print the entire dictionary.
3. Print only the student's name.
4. Print only the score.

**Solution:**
```python
student = {
    "name": "Fatima",
    "age": 16,
    "class": "JSS3",
    "favourite_subject": "Biology",
    "score": 92
}

print(student)
print(student["name"])
print(student["score"])
```

**Expected Output:**
```
{'name': 'Fatima', 'age': 16, 'class': 'JSS3', 'favourite_subject': 'Biology', 'score': 92}
Fatima
92
```

**Self-check questions:**
- What happens if you print `student["grade"]`?
- How would you use `.get()` to print `student["grade"]` safely?

---

### Exercise 2: Update and Add to a Dictionary

**Objective:** Modify an existing dictionary.

**Scenario:** Fatima's score has been updated to 95 after a remark. Also, the teacher wants to add her house (school house): "Blue House".

```python
student = {
    "name": "Fatima",
    "age": 16,
    "score": 92
}

# Step 1: Update the score
student["score"] = 95

# Step 2: Add the house
student["house"] = "Blue House"

print(student)
```

**Expected Output:**
```
{'name': 'Fatima', 'age': 16, 'score': 95, 'house': 'Blue House'}
```

**What-if challenge:** Try the same using `.update()` instead of direct assignment.

---

### Exercise 3: Loop Through a Dictionary

**Objective:** Print a formatted report from a dictionary.

```python
product = {
    "name": "Laptop",
    "brand": "TechCo",
    "price": 450000,
    "in_stock": True
}

print("=== Product Report ===")
for key, value in product.items():
    print(f"{key.capitalize()}: {value}")
```

**Expected Output:**
```
=== Product Report ===
Name: Laptop
Brand: TechCo
Price: 450000
In_stock: True
```

**Hint on `key.capitalize()`:** This turns `"name"` into `"Name"` for nicer display.

---

### Exercise 4: Remove Items Safely

**Scenario:** A hospital patient record needs cleanup. Remove the "temp_note" field safely and also remove the last added item.

```python
patient = {
    "id": "P-001",
    "name": "Emeka",
    "condition": "Stable",
    "temp_note": "To be updated"
}

# Remove temp_note using .pop()
removed = patient.pop("temp_note")
print(f"Removed note: {removed}")
print(patient)

# Remove the last item using .popitem()
last = patient.popitem()
print(f"Last item removed: {last}")
print(patient)
```

**Expected Output:**
```
Removed note: To be updated
{'id': 'P-001', 'name': 'Emeka', 'condition': 'Stable'}
Last item removed: ('condition', 'Stable')
{'id': 'P-001', 'name': 'Emeka'}
```

---

### Exercise 5: Working with Nested Dictionaries

**Scenario:** A university stores records of multiple students.

```python
university = {
    "student1": {"name": "Aisha", "dept": "Engineering", "gpa": 3.8},
    "student2": {"name": "Kola", "dept": "Medicine", "gpa": 3.5},
    "student3": {"name": "Ngozi", "dept": "Law", "gpa": 3.9}
}

# Print Kola's department
print(university["student2"]["dept"])

# Print all students and their GPAs
for student_id, info in university.items():
    print(f"{info['name']} — GPA: {info['gpa']}")
```

**Expected Output:**
```
Medicine
Aisha — GPA: 3.8
Kola — GPA: 3.5
Ngozi — GPA: 3.9
```

---

## Part 12: Mini Project — Student Grade Book System

This project brings together everything you have learned. You will build a simple grade book using dictionaries.

### Project Overview

You are building a grade book for a secondary school teacher. The system will:
1. Store 3 students with their names, subjects, and scores
2. Display all students and their scores
3. Find the highest scoring student
4. Add a new student
5. Remove a student who has withdrawn

---

### Stage 1: Setup — Create the Grade Book

```python
# The grade book — a dictionary of dictionaries
gradebook = {
    "student_1": {"name": "Amina", "subject": "Chemistry", "score": 88},
    "student_2": {"name": "Babatunde", "subject": "Physics", "score": 75},
    "student_3": {"name": "Chioma", "subject": "Biology", "score": 92}
}

print("=== Grade Book Created ===")
print(gradebook)
```

**Milestone Output:**
```
=== Grade Book Created ===
{'student_1': {'name': 'Amina', 'subject': 'Chemistry', 'score': 88}, ...}
```

---

### Stage 2: Display All Students

```python
print("\n=== All Students ===")
for student_id, details in gradebook.items():
    print(f"{details['name']} | {details['subject']} | Score: {details['score']}")
```

**Milestone Output:**
```
=== All Students ===
Amina | Chemistry | Score: 88
Babatunde | Physics | Score: 75
Chioma | Biology | Score: 92
```

---

### Stage 3: Find the Highest Scorer

```python
print("\n=== Finding Top Student ===")

top_student = None
top_score = 0

for student_id, details in gradebook.items():
    if details["score"] > top_score:
        top_score = details["score"]
        top_student = details["name"]

print(f"Top student: {top_student} with a score of {top_score}")
```

**Milestone Output:**
```
=== Finding Top Student ===
Top student: Chioma with a score of 92
```

---

### Stage 4: Add a New Student

```python
# Adding a new student
gradebook["student_4"] = {"name": "Dele", "subject": "Maths", "score": 80}

print("\n=== After Adding Dele ===")
for student_id, details in gradebook.items():
    print(f"{details['name']} | Score: {details['score']}")
```

**Milestone Output:**
```
=== After Adding Dele ===
Amina | Score: 88
Babatunde | Score: 75
Chioma | Score: 92
Dele | Score: 80
```

---

### Stage 5: Remove a Student Who Withdrew

```python
# Babatunde has withdrawn from school
removed = gradebook.pop("student_2")
print(f"\n{removed['name']} has been removed from the grade book.")

print("\n=== Final Grade Book ===")
for student_id, details in gradebook.items():
    print(f"{details['name']} | {details['subject']} | Score: {details['score']}")
```

**Final Output:**
```
Babatunde has been removed from the grade book.

=== Final Grade Book ===
Amina | Chemistry | Score: 88
Chioma | Biology | Score: 92
Dele | Maths | Score: 80
```

**Optional enhancement ideas:**
- Add a function to calculate the average score of all students
- Allow the user to input student names with `input()`
- Add a letter grade (A, B, C) based on the score

---

## Part 13: Common Beginner Mistakes

### Mistake 1 — Using `=` Instead of `.copy()`

```python
# WRONG — both variables point to the same dictionary
original = {"a": 1}
copy = original
copy["b"] = 2
print(original)   # {'a': 1, 'b': 2} — original was changed too!

# CORRECT — use .copy()
original = {"a": 1}
copy = original.copy()
copy["b"] = 2
print(original)   # {'a': 1} — original is safe
```

### Mistake 2 — Duplicate Keys Silently Overwrite

```python
# WRONG — duplicate keys
d = {"x": 10, "x": 20}
print(d)   # {'x': 20} — first value was silently lost!

# CORRECT — use unique keys
d = {"x1": 10, "x2": 20}
```

### Mistake 3 — Accessing a Non-Existent Key with Square Brackets

```python
car = {"brand": "Toyota"}

# WRONG — will crash with KeyError
# print(car["color"])

# CORRECT — use .get() for safety
print(car.get("color"))            # None
print(car.get("color", "Unknown")) # Unknown
```

### Mistake 4 — Confusing `.keys()` Return Type

```python
car = {"brand": "Ford", "year": 1964}
keys = car.keys()

# WRONG — this doesn't work directly on the view object
# first_key = keys[0]   # TypeError: 'dict_keys' object is not subscriptable

# CORRECT — convert to list first if you need indexing
keys_list = list(car.keys())
print(keys_list[0])   # brand
```

### Mistake 5 — Forgetting Colons in Nested Dictionaries

```python
# WRONG — missing colon after outer key
# myfamily = {
#     "child1" {         # SyntaxError!
#         "name": "Emil"
#     }
# }

# CORRECT — colon after every key, including outer keys
myfamily = {
    "child1": {          # Colon here!
        "name": "Emil"
    }
}
```

### Mistake 6 — Modifying a Dictionary While Looping Through It

```python
scores = {"Amina": 90, "Tunde": 55, "Ngozi": 80}

# WRONG — never add or remove items while looping!
# for key in scores:
#     if scores[key] < 60:
#         del scores[key]   # RuntimeError: dictionary changed size during iteration

# CORRECT — loop over a copy of the keys
for key in list(scores.keys()):
    if scores[key] < 60:
        del scores[key]

print(scores)  # {'Amina': 90, 'Ngozi': 80}
```

---

## Part 14: Reflection Questions

Think carefully about each of these. Try to answer before checking:

1. What is the difference between a dictionary and a list in Python?
2. Why are duplicate keys not allowed in a dictionary?
3. What is the difference between `.pop()` and `.popitem()`?
4. When would you use `.get()` instead of square bracket notation?
5. What is the difference between `del my_dict` and `my_dict.clear()`?
6. What does "a live view" mean in the context of `.keys()`, `.values()`, and `.items()`?
7. If you loop through a dictionary with `for x in my_dict:`, what does `x` contain?
8. Why does `copy = original` not create a true independent copy of a dictionary?
9. How would you access the value `"Linus"` from this dictionary: `{"child3": {"name": "Linus", "year": 2011}}`?
10. In what real-world programming scenario would a nested dictionary be useful?

---

## Part 15: Lesson Completion Checklist

Review this checklist before moving to the next lesson. Check off each item you are confident about:

- [ ] I can create a dictionary using curly brackets `{}`
- [ ] I can create a dictionary using the `dict()` constructor
- [ ] I understand what key-value pairs are
- [ ] I know that dictionaries do not allow duplicate keys
- [ ] I can access a value using square bracket notation: `my_dict["key"]`
- [ ] I can access a value safely using `.get()`
- [ ] I can retrieve all keys using `.keys()`
- [ ] I can retrieve all values using `.values()`
- [ ] I can retrieve all key-value pairs using `.items()`
- [ ] I can check if a key exists using the `in` keyword
- [ ] I can change a value using direct assignment: `my_dict["key"] = new_value`
- [ ] I can update values using `.update()`
- [ ] I can add new items to a dictionary
- [ ] I can remove items using `.pop()`, `.popitem()`, `del`, and `.clear()`
- [ ] I understand the difference between `del` and `.clear()`
- [ ] I can loop through keys, values, and key-value pairs
- [ ] I can create a proper copy using `.copy()` or `dict()`
- [ ] I understand why `copy = original` is not a true copy
- [ ] I can create nested dictionaries
- [ ] I can access nested dictionary values using chained keys
- [ ] I know all 11 dictionary methods and what they do
- [ ] I can use `dict.fromkeys()` to initialise a dictionary with default values
- [ ] I have completed the mini project

---

## Lesson Summary

Congratulations on completing Lesson 14!

Here is a quick summary of everything you have learned:

**Dictionaries** store data as **key-value pairs** inside curly brackets `{}`. They are **ordered** (Python 3.7+), **mutable** (changeable), and do **not allow duplicate keys**.

| Task | How to do it |
|------|-------------|
| Create | `d = {"key": "value"}` or `dict(key="value")` |
| Access | `d["key"]` or `d.get("key")` |
| Get all keys | `d.keys()` |
| Get all values | `d.values()` |
| Get all pairs | `d.items()` |
| Check key exists | `"key" in d` |
| Change value | `d["key"] = new_value` |
| Update | `d.update({"key": new_value})` |
| Add new item | `d["new_key"] = value` |
| Remove by key | `d.pop("key")` |
| Remove last item | `d.popitem()` |
| Delete key | `del d["key"]` |
| Clear all | `d.clear()` |
| Copy safely | `d.copy()` or `dict(d)` |
| Loop keys | `for k in d:` |
| Loop values | `for v in d.values():` |
| Loop both | `for k, v in d.items():` |
| Nested access | `d["outer"]["inner"]` |
| Init with defaults | `dict.fromkeys(keys, default)` |

Dictionaries are one of the most important and most-used data structures in Python. Mastering them opens the door to working with APIs, JSON data, databases, web development, data science, and much more.

In the next lesson, you will continue building on these skills as you learn about Python conditional statements and control flow!

---

*Sources: W3Schools Python Dictionaries Tutorial (all 10 pages)*
