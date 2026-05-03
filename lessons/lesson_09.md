---
render_with_liquid: false
title: "Lesson 09 – Python Booleans"
nav_order: 9
---

# Lesson 09 – Python Booleans

---

## Lesson Introduction

Imagine you are filling out a form and it asks: *"Are you 18 or older?"*  
Your answer can only be one of two things: **Yes** or **No**.

That is exactly what a **Boolean** is in Python.

A **Boolean** is a special type of data that holds only **one of two possible values**:

- `True`  ← means "yes", "correct", "on", or "it happened"
- `False` ← means "no", "wrong", "off", or "it did not happen"

The word "Boolean" comes from the name of a mathematician called **George Boole**, who invented a system of logic based entirely on true-or-false answers. Python (and almost every programming language) uses this idea constantly.

You will use Booleans **every single day** as a programmer, because programs constantly need to make decisions:

> *"Is the password correct? → True or False."*  
> *"Is the student's score above 50? → True or False."*  
> *"Is the shopping cart empty? → True or False."*

By the end of this lesson, you will understand:
- What Booleans are and why they exist
- How Python evaluates expressions as `True` or `False`
- How to use the `bool()` function
- Which values Python considers `True` and which it considers `False`
- How to write functions that return Boolean values
- How to use Booleans with `if` statements to make decisions

---

## Prerequisite Concepts

Before we begin, let us quickly review two things you already know that will appear in this lesson.

### Variables

A variable is a named box that stores a value.

```python
x = 10
name = "Ada"
```

### The `print()` Function

`print()` displays a value on the screen.

```python
print("Hello")   # Output: Hello
print(42)        # Output: 42
```

You already know these — great! Now let's build on them.

---

## Part 1 – What Are Boolean Values?

### The Two Boolean Values

In Python, there are exactly **two Boolean values**, and they are written with a capital first letter:

| Value   | Meaning                       |
|---------|-------------------------------|
| `True`  | Yes / Correct / It happened   |
| `False` | No / Wrong / It did not happen |

> ⚠️ **Critical beginner warning:** `True` and `False` must **always** start with a capital letter. Writing `true` or `false` (lowercase) will cause an error in Python.

```python
# ✅ Correct
x = True
y = False

# ❌ Wrong — will cause a NameError!
x = true
y = false
```

### Storing Booleans in Variables

You can store a Boolean value directly into a variable, just like you store a number or a string.

```python
is_raining = True
has_ticket = False

print(is_raining)    # Output: True
print(has_ticket)    # Output: False
```

**Line-by-line explanation:**
- `is_raining = True` — we create a variable called `is_raining` and store the Boolean `True` inside it
- `has_ticket = False` — we create a variable called `has_ticket` and store `False` inside it
- `print(is_raining)` — displays whatever is inside `is_raining`, which is `True`
- `print(has_ticket)` — displays whatever is inside `has_ticket`, which is `False`

**Expected Output:**
```
True
False
```

---

## Part 2 – Boolean Values From Comparisons

The most important way Booleans appear in Python is when you **compare two values**.

### What is a Comparison?

A comparison is a question you ask Python:  
*"Is this bigger than that?"* or *"Are these two things equal?"*

Python answers that question with `True` or `False`.

### Comparison Operators

These are the symbols Python uses for comparisons:

| Symbol | Meaning                  | Example      | Result  |
|--------|--------------------------|--------------|---------|
| `>`    | Greater than             | `10 > 9`     | `True`  |
| `<`    | Less than                | `10 < 9`     | `False` |
| `==`   | Equal to                 | `10 == 10`   | `True`  |
| `!=`   | Not equal to             | `5 != 3`     | `True`  |
| `>=`   | Greater than or equal to | `10 >= 10`   | `True`  |
| `<=`   | Less than or equal to    | `7 <= 5`     | `False` |

> 💡 **Important distinction:** A single `=` assigns a value to a variable (`x = 5`). A double `==` checks if two things are equal (`x == 5`). These are completely different!

### Example 1 – Simple comparisons printed directly

```python
print(10 > 9)
print(10 == 9)
print(10 < 9)
```

**Line-by-line explanation:**
- `print(10 > 9)` — asks "Is 10 greater than 9?" → Yes → prints `True`
- `print(10 == 9)` — asks "Is 10 equal to 9?" → No → prints `False`
- `print(10 < 9)` — asks "Is 10 less than 9?" → No → prints `False`

**Expected Output:**
```
True
False
False
```

> 🤔 **Thinking prompt:** What do you think `print(10 == 10)` would print? Try changing the second number and observe how the result changes.

### Example 2 – Comparisons using variables

```python
a = 200
b = 33

print(a > b)
print(a == b)
print(b > a)
```

**Expected Output:**
```
True
False
False
```

---

## Part 3 – Using Booleans With `if` Statements

Booleans become incredibly powerful when you combine them with `if` statements. An `if` statement lets your program **make a decision** based on whether something is `True` or `False`.

### The Basic Structure of an `if` Statement

```
if  <something is True>:
    do this
else:
    do that instead
```

Think of it like a traffic light:  
- If the light is **green** (True) → you drive  
- Otherwise (False) → you stop

### Example – Check which variable is greater

```python
a = 200
b = 33

if b > a:
    print("b is greater than a")
else:
    print("b is not greater than a")
```

**Line-by-line explanation:**
- `a = 200` — stores 200 in variable `a`
- `b = 33` — stores 33 in variable `b`
- `if b > a:` — asks "Is 33 greater than 200?" → No → Python moves to the `else` block
- `print("b is greater than a")` — this line is **skipped** because the condition was False
- `else:` — this block runs when the `if` condition is False
- `print("b is not greater than a")` — this line runs

**Expected Output:**
```
b is not greater than a
```

> 🤔 **Thinking prompt:** What would happen if you changed `b = 33` to `b = 500`? Try it mentally first — then verify!

### Example – Checking a student's score

```python
score = 75

if score >= 50:
    print("Student passed!")
else:
    print("Student failed.")
```

**Expected Output:**
```
Student passed!
```

---

## Part 4 – The `bool()` Function

Python has a built-in function called `bool()` that converts **any value** into its Boolean equivalent (`True` or `False`).

### What is a Function?

A function is a named command that does a job. You **call** it by writing its name followed by parentheses `()`, and you put the value you want it to work on inside the parentheses.

```
bool( value )  →  returns True or False
```

### Example 1 – Evaluating a string and a number

```python
print(bool("Hello"))
print(bool(15))
```

**Line-by-line explanation:**
- `bool("Hello")` — asks "Does `"Hello"` have content?" → Yes → `True`
- `bool(15)` — asks "Is 15 a non-zero number?" → Yes → `True`

**Expected Output:**
```
True
True
```

### Example 2 – Using variables with `bool()`

```python
x = "Hello"
y = 15

print(bool(x))
print(bool(y))
```

**Expected Output:**
```
True
True
```

The result is the same whether you pass the value directly or pass a variable that holds the value.

---

## Part 5 – Most Values Are `True`

Here is a very important rule to memorise:

> **Almost every value in Python is `True` — as long as it is not empty, zero, or nothing.**

### Values That Are `True`

- Any **non-empty string**: `"hello"`, `"0"`, `"False"` (yes, even the string `"False"` is True!)
- Any **non-zero number**: `1`, `-5`, `3.14`, `100`
- Any **non-empty list, tuple, set, or dictionary**

### Example – True values

```python
print(bool("abc"))
print(bool(123))
print(bool(["apple", "cherry", "banana"]))
```

**Expected Output:**
```
True
True
True
```

**Explanation:**
- `"abc"` is a non-empty string → `True`
- `123` is a non-zero number → `True`
- `["apple", "cherry", "banana"]` is a non-empty list → `True`

> 🤔 **Thinking prompt:** What do you think `bool("0")` returns? Remember — `"0"` is a **string** containing the character zero, not the number zero. It has content, so it is `True`!

---

## Part 6 – Some Values Are `False`

Even though most values are `True`, there is a small group of values that are always `False`:

| Value      | Type       | Why it is False           |
|------------|------------|---------------------------|
| `False`    | Boolean    | It is `False` by definition |
| `None`     | NoneType   | Represents "nothing"      |
| `0`        | Integer    | Zero has no quantity       |
| `0.0`      | Float      | Zero as a decimal          |
| `""`       | String     | Empty string               |
| `()`       | Tuple      | Empty tuple                |
| `[]`       | List       | Empty list                 |
| `{}`       | Dictionary | Empty dictionary           |

### Example – All the False values

```python
print(bool(False))
print(bool(None))
print(bool(0))
print(bool(""))
print(bool(()))
print(bool([]))
print(bool({}))
```

**Expected Output:**
```
False
False
False
False
False
False
False
```

### Side-by-side comparison: True vs False

```python
# Non-empty string → True
print(bool("hello"))    # True

# Empty string → False
print(bool(""))         # False

# Non-zero number → True
print(bool(42))         # True

# Zero → False
print(bool(0))          # False

# Non-empty list → True
print(bool([1, 2, 3]))  # True

# Empty list → False
print(bool([]))         # False
```

**Expected Output:**
```
True
False
True
False
True
False
```

> 💡 **Real-world analogy:** Think of a cup of water. If the cup has any water in it at all, it is "True" (it has content). If the cup is completely empty, it is "False" (nothing inside).

### Advanced: Objects With `__len__` Returning 0 Are Also `False`

This is a more advanced concept, but worth knowing. If you create a custom object (class) that has a special method called `__len__` which returns `0`, Python will treat that object as `False`.

```python
class myclass():
    def __len__(self):
        return 0

myobj = myclass()
print(bool(myobj))
```

**Expected Output:**
```
False
```

**Explanation:**
- `class myclass():` — creates a new type of object called `myclass`
- `def __len__(self):` — defines a special method that tells Python "what is the length of this object?"
- `return 0` — says the length is 0
- `myobj = myclass()` — creates an instance (a copy) of that class
- `bool(myobj)` — Python asks `__len__` for the size → gets 0 → returns `False`

You don't need to fully understand classes yet — just know that this behaviour exists.

---

## Part 7 – Functions That Return Boolean Values

You can write your own functions that give back a `True` or `False` answer. This is extremely useful for creating reusable "yes or no" checks in your programs.

### Example 1 – A function that returns True

```python
def myFunction():
    return True

print(myFunction())
```

**Line-by-line explanation:**
- `def myFunction():` — defines a function called `myFunction`
- `return True` — when the function is called, it sends back the value `True`
- `print(myFunction())` — calls the function and prints whatever it returns

**Expected Output:**
```
True
```

### Example 2 – Using a Boolean-returning function in an `if` statement

```python
def myFunction():
    return True

if myFunction():
    print("YES!")
else:
    print("NO!")
```

**Line-by-line explanation:**
- `if myFunction():` — calls the function; if it returns `True`, the `if` block runs
- Since `myFunction()` returns `True`, Python executes `print("YES!")`

**Expected Output:**
```
YES!
```

> 💡 **Real-world use case:** In a login system, you might have a function called `is_password_correct()` that returns `True` or `False`. Your program then does: `if is_password_correct(): allow_entry()`.

### Example 3 – A more realistic Boolean function

```python
def is_adult(age):
    if age >= 18:
        return True
    else:
        return False

print(is_adult(20))   # True
print(is_adult(15))   # False
```

**Expected Output:**
```
True
False
```

---

## Part 8 – Built-in Functions That Return Booleans

Python comes with many built-in functions that automatically return `True` or `False`. One very useful one is `isinstance()`.

### The `isinstance()` Function

`isinstance(object, type)` checks whether a given value is of a specific data type. It returns `True` if it is, and `False` if it is not.

```python
isinstance( value, data_type )  →  True or False
```

### Example – Check if a variable is an integer

```python
x = 200
print(isinstance(x, int))
```

**Line-by-line explanation:**
- `x = 200` — stores the number 200 in `x`
- `isinstance(x, int)` — asks "Is `x` an integer (`int`)?" → Yes → returns `True`
- `print(...)` — displays the result

**Expected Output:**
```
True
```

### Example – Testing different types

```python
name = "Alice"
score = 95
price = 4.99

print(isinstance(name, str))    # True  — name is a string
print(isinstance(score, int))   # True  — score is an integer
print(isinstance(price, float)) # True  — price is a float
print(isinstance(name, int))    # False — name is NOT an integer
```

**Expected Output:**
```
True
True
True
False
```

---

## Guided Practice Exercises

### Exercise 1 – Warm-Up: Print Boolean Results

**Objective:** Practice reading comparison expressions and predicting their Boolean output.

**Before running the code**, predict whether each line will print `True` or `False`:

```python
print(5 > 3)
print(10 == 10)
print(7 < 2)
print(4 != 4)
print(100 >= 100)
print(3 <= 2)
```

**Expected Output:**
```
True
True
False
False
True
False
```

**Self-check:** Did your predictions match? If any surprised you, re-read the comparison operators table in Part 2.

---

### Exercise 2 – Student Pass/Fail Checker

**Objective:** Use a Boolean comparison inside an `if` statement to make a decision.

**Scenario:** A student scored 62 out of 100. The passing mark is 50.

**Steps:**
1. Store the student's score in a variable
2. Use an `if` statement to check if the score is 50 or above
3. Print "Pass" if True, "Fail" if False

```python
student_score = 62
passing_mark = 50

if student_score >= passing_mark:
    print("Result: Pass")
else:
    print("Result: Fail")
```

**Expected Output:**
```
Result: Pass
```

**What-if challenge:** Change `student_score` to `45`. What happens now?

---

### Exercise 3 – The `bool()` Explorer

**Objective:** Use `bool()` to test which values are truthy and which are falsy.

```python
# Test these values one by one
print(bool(1))        # Non-zero number
print(bool(0))        # Zero
print(bool("Python")) # Non-empty string
print(bool(""))       # Empty string
print(bool([1, 2]))   # Non-empty list
print(bool([]))       # Empty list
print(bool(None))     # None
```

**Expected Output:**
```
True
False
True
False
True
False
False
```

**Self-check question:** Can you explain in your own words why `bool("")` returns `False` but `bool(" ")` (a space) returns `True`?

---

### Exercise 4 – Is It a String?

**Objective:** Use `isinstance()` to check data types.

```python
def check_type(value):
    if isinstance(value, str):
        print(str(value) + " is a string → True")
    else:
        print(str(value) + " is NOT a string → False")

check_type("hello")
check_type(42)
check_type(3.14)
check_type("100")
```

**Expected Output:**
```
hello is a string → True
42 is NOT a string → False
3.14 is NOT a string → False
100 is a string → True
```

> 💡 Notice that `"100"` is a **string** (it has quotes), even though it looks like a number. `isinstance("100", str)` returns `True`.

---

## Mini Project – Smart Access Control System

### Project Goal

Build a simple program that checks whether a person is allowed to enter a restricted area based on two conditions:
1. They must be **18 or older**
2. They must **have a valid pass**

### Stage 1 – Setup the Data

```python
# Person's details
person_name = "Amara"
person_age = 22
has_valid_pass = True
```

**Milestone output:** Nothing printed yet — just data stored.

### Stage 2 – Core Logic: Write the Check Functions

```python
def is_old_enough(age):
    return age >= 18

def has_access(age, valid_pass):
    if is_old_enough(age) and valid_pass:
        return True
    else:
        return False
```

**Line-by-line explanation:**
- `is_old_enough(age)` — returns `True` if age is 18 or above, otherwise `False`
- `has_access(age, valid_pass)` — returns `True` only if **both** conditions are met: age ≥ 18 AND valid_pass is True
- `and` — a logical operator that means "both must be True"

### Stage 3 – Display the Result

```python
person_name = "Amara"
person_age = 22
has_valid_pass = True

def is_old_enough(age):
    return age >= 18

def has_access(age, valid_pass):
    if is_old_enough(age) and valid_pass:
        return True
    else:
        return False

# Check and display
if has_access(person_age, has_valid_pass):
    print(person_name + " is ALLOWED entry.")
else:
    print(person_name + " is DENIED entry.")
```

**Expected Output:**
```
Amara is ALLOWED entry.
```

### Stage 4 – Test Different Scenarios

```python
# Test 1: Too young, has pass
print(bool(has_access(16, True)))    # False

# Test 2: Old enough, no pass
print(bool(has_access(25, False)))   # False

# Test 3: Old enough, has pass
print(bool(has_access(30, True)))    # True

# Test 4: Exactly 18, has pass
print(bool(has_access(18, True)))    # True
```

**Expected Output:**
```
False
False
True
True
```

### Reflection Questions

1. What would you need to change to allow entry from age 21 instead of 18?
2. What would `has_access(18, False)` return and why?
3. Can you add a third condition — for example, the person must also have a `membership_card`?

### Optional Extension

Modify the program to check a list of multiple people:

```python
visitors = [
    {"name": "Tunde", "age": 17, "pass": True},
    {"name": "Ngozi", "age": 25, "pass": True},
    {"name": "Emeka", "age": 19, "pass": False},
]

for visitor in visitors:
    result = has_access(visitor["age"], visitor["pass"])
    if result:
        print(visitor["name"] + ": ALLOWED")
    else:
        print(visitor["name"] + ": DENIED")
```

**Expected Output:**
```
Tunde: DENIED
Ngozi: ALLOWED
Emeka: DENIED
```

---

## Common Beginner Mistakes

### Mistake 1 – Using lowercase `true` or `false`

```python
# ❌ Wrong
x = true   # NameError: name 'true' is not defined

# ✅ Correct
x = True
```

**Why:** Python treats `True` and `False` as special keywords, and they must be written with an uppercase first letter. `true` is not a keyword — Python would look for a variable called `true` and fail.

---

### Mistake 2 – Confusing `=` with `==`

```python
# ❌ Wrong — this assigns 5 to x, not a comparison
if x = 5:
    print("equal")   # SyntaxError

# ✅ Correct — this compares x to 5
if x == 5:
    print("equal")
```

**Why:** `=` sets a value. `==` checks if two values are equal.

---

### Mistake 3 – Thinking `"False"` (as a string) is False

```python
x = "False"
print(bool(x))   # True!
```

**Why:** `"False"` is a **non-empty string**. Any non-empty string is `True`, even if the string happens to spell the word "False".

---

### Mistake 4 – Forgetting the colon after `if` and `else`

```python
# ❌ Wrong
if x > 5
    print("big")

# ✅ Correct
if x > 5:
    print("big")
```

---

### Mistake 5 – Using `bool()` when you just need a comparison

```python
# ❌ Unnecessary
if bool(x > 5) == True:
    print("big")

# ✅ Simpler and cleaner
if x > 5:
    print("big")
```

**Why:** `if` already evaluates the condition as a Boolean. You don't need to wrap it in `bool()` or compare it to `True`.

---

## Reflection Questions

1. In your own words, what is a Boolean? What are the only two values it can have?
2. What is the difference between `=` and `==` in Python?
3. Name three values that Python evaluates as `False`.
4. What does `bool("0")` return? Why?
5. What does `isinstance(3.14, int)` return? Why?
6. Why is it useful for a function to return a Boolean value?
7. What does the word "truthy" mean when talking about Python values?
8. If you have `x = []`, what does `bool(x)` return, and why?

---

## Completion Checklist

Before moving to the next lesson, confirm that you can:

- [ ] Explain what a Boolean is and name its two possible values
- [ ] Write `True` and `False` correctly (with capital letters)
- [ ] Use comparison operators (`>`, `<`, `==`, `!=`, `>=`, `<=`) to produce Boolean results
- [ ] Use an `if`/`else` statement with a Boolean condition
- [ ] Use the `bool()` function to convert a value to `True` or `False`
- [ ] List at least five values that Python considers `False`
- [ ] Write a simple function that returns `True` or `False`
- [ ] Use `isinstance()` to check a variable's data type
- [ ] Avoid the common beginner mistakes listed above

---

## Lesson Summary

In this lesson, you learned about **Booleans** — one of the most fundamental concepts in all of programming.

Here is a compact summary of everything covered:

**The two Boolean values:**
```python
True   # yes, correct, something is there
False  # no, wrong, nothing is there
```

**Comparisons return Booleans:**
```python
print(10 > 9)    # True
print(10 == 9)   # False
```

**`if` statements use Booleans to make decisions:**
```python
if score >= 50:
    print("Pass")
else:
    print("Fail")
```

**`bool()` converts any value to True or False:**
```python
bool("hello")  # True
bool("")       # False
bool(42)       # True
bool(0)        # False
```

**Most values are True. Falsy values include:**
`False`, `None`, `0`, `""`, `()`, `[]`, `{}`

**Functions can return Booleans:**
```python
def is_adult(age):
    return age >= 18

print(is_adult(20))   # True
print(is_adult(15))   # False
```

**`isinstance()` checks data types:**
```python
x = 200
print(isinstance(x, int))    # True
print(isinstance(x, str))    # False
```

Booleans are the foundation of **decision-making** in Python. Every `if` statement, every loop condition, and every logical check you ever write will rely on Boolean values. You are now ready to move forward to Python Operators, where you will learn even more powerful ways to combine and evaluate conditions.
