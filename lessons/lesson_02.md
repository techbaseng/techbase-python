---
render_with_liquid: false
title: "Lesson 02 – Python Comments and Variables"
nav_order: 2
---

# Lesson 02 – Python Comments and Variables

---

## Lesson Introduction

Welcome to Lesson 02! In Lesson 01 you learned how Python works and how to print things on the screen. Now we are going to learn two of the most important building blocks of every Python program:

1. **Comments** – notes you write inside your code that Python completely ignores. They are for *you* (the programmer), not for the computer.
2. **Variables** – labelled boxes that store information so your program can remember and reuse it later.

By the end of this lesson you will be able to:

- Write single-line and multi-line comments in Python.
- Create variables and store different kinds of data in them.
- Name variables correctly following Python's rules.
- Assign one value to many variables at the same time.
- Print variables to the screen in different ways.
- Understand the difference between local and global variables.

Take your time, try every example, and read every explanation. There are no silly questions here — we start from zero.

---

## Prerequisite Concepts

Before we dive in, make sure you are comfortable with one thing from Lesson 01:

**The `print()` function** — this is how we display output on the screen.

```python
print("Hello, World!")
```

**Expected output:**
```
Hello, World!
```

`print(...)` simply shows whatever is inside the parentheses on your screen. We will use it constantly in this lesson to check our work.

---

## PART 1 — Python Comments

---

### What Is a Comment?

Think of a comment like a sticky note on your code. Imagine you are writing a recipe. Sometimes you jot little notes to yourself: *"Use ripe tomatoes here!"* Those notes are for you — not part of the cooking instructions. Comments in Python work exactly the same way.

A **comment** is a line (or part of a line) in your Python file that Python completely skips when running your program. It does **not** execute, it does **not** produce output, and it does **not** affect anything. It is purely a human-readable note.

### Why Do Comments Exist?

Comments solve several real problems:

- **Explaining what code does** — When you or a teammate reads the code three months later, comments remind everyone *why* a decision was made.
- **Making code readable** — Long programs become confusing. Comments break them into understandable sections.
- **Temporarily disabling code** — During testing, you can "turn off" a line of code by making it a comment instead of deleting it.

Professional programmers in software companies, data science labs, research institutions, and engineering firms all use comments daily. Well-commented code is considered a sign of a good programmer.

---

### How to Create a Single-Line Comment

In Python, a comment starts with the **hash symbol** `#`. Everything on the line after `#` is ignored by Python.

**Syntax:**
```python
# This is a comment
```

**Example 1 — Comment on its own line:**

```python
# This line is a comment. Python ignores it completely.
print("Hello, World!")
```

**Expected output:**
```
Hello, World!
```

Notice that only the `print` line produced output. The comment did nothing — Python skipped it entirely.

**Breaking it down line by line:**
- `# This line is a comment.` → Python sees the `#` and skips the whole line.
- `print("Hello, World!")` → Python runs this and displays `Hello, World!`

---

**Example 2 — Comment at the end of a line (inline comment):**

You can also place a comment at the end of a working line of code. Python will run the code part and ignore everything after the `#`.

```python
print("Hello, World!")  # This is an inline comment
```

**Expected output:**
```
Hello, World!
```

The comment here is just a label explaining what this line does. Python ran `print("Hello, World!")` and completely ignored `# This is an inline comment`.

> **Tip:** Leave two spaces before an inline comment. It keeps your code tidy and readable.

---

**Example 3 — Using a comment to disable code:**

This is very useful when you are testing. Instead of deleting a line, you turn it into a comment:

```python
# print("Hello, World!")
print("Cheers, Mate!")
```

**Expected output:**
```
Cheers, Mate!
```

The first `print` is commented out — Python ignores it. Only the second `print` runs.

> **Why is this useful?** Imagine you wrote a line of code that is causing an error. Instead of deleting it (and losing your work), you comment it out temporarily. Then you uncomment it later when you are ready.

---

### How to Create a Multi-Line Comment

Python does **not** have a built-in multi-line comment symbol (unlike some other languages). But there are two easy ways to write comments that span multiple lines.

**Method 1 — Use `#` on every line:**

```python
# This is a comment
# written across
# more than one line
print("Hello, World!")
```

**Expected output:**
```
Hello, World!
```

Each line starts with `#`, so Python skips each one individually.

---

**Method 2 — Use a triple-quoted string (not assigned to any variable):**

Python lets you write text inside triple quotes `"""..."""`. If you never assign this text to a variable, Python reads it and immediately throws it away. Programmers take advantage of this trick to write multi-line comments.

```python
"""
This is a comment
written in
more than just one line
"""
print("Hello, World!")
```

**Expected output:**
```
Hello, World!
```

The triple-quoted block is technically a **string**, but since it is not stored anywhere or used for anything, Python discards it. The `print` still runs normally.

> **Important Note:** This method is *widely used* but is technically a string that gets ignored — not a true comment. The `#` method is the "official" way to write comments in Python.

---

### A Quick Comparison

| Situation | What to use |
|---|---|
| Short explanation on one line | `# Your note here` |
| Note at the end of a code line | `code  # Your note` |
| Long explanation across many lines | `#` on each line OR `"""..."""` |
| Temporarily disabling a line | `# print("disabled line")` |

---

### Thinking Prompt

> What happens if you put a `#` in the middle of a word, like `pri#nt("Hello")`? Try it! What do you notice?

---

## PART 2 — Python Variables

---

### What Is a Variable?

Imagine you are working at a supermarket. You need to remember the price of tomatoes: ₦500. You write it on a small sticky label and stick it on a jar. Now whenever you look at the jar, you know the price.

A **variable** in Python is exactly like that sticky label and jar. The *label* is the variable name. The *jar* holds the value. Whenever your program needs that value, it looks up the label.

**In simple terms:** A variable is a named location in your computer's memory where you can store a piece of data.

### Why Do Variables Exist?

Without variables, every program would have to hardcode every number and every piece of text — and you could never reuse or change data. Variables allow programs to:

- **Remember information** (a user's name, a test score, a temperature reading)
- **Reuse data** without repeating it
- **Update data** as the program runs (e.g., a score increasing in a game)
- **Make calculations** flexible (calculate tax for any salary, not just one fixed amount)

In data science, a variable might store a dataset. In a game, it stores the player's health. In an app, it stores a user's login name. Variables are everywhere.

---

### Creating a Variable

Python makes creating variables extremely simple. You do **not** need to declare what type of data goes in it first. You just write the name, an equals sign `=`, and the value.

**Syntax:**
```
variable_name = value
```

The `=` sign here is called the **assignment operator**. It means: *"store the value on the right into the name on the left."*

**Example 1 — Your first variable:**

```python
x = 5
print(x)
```

**Expected output:**
```
5
```

- `x = 5` → Create a variable named `x` and store the number `5` in it.
- `print(x)` → Show the value stored in `x`. Python looks up `x`, finds `5`, and prints it.

---

**Example 2 — A text variable:**

```python
name = "John"
print(name)
```

**Expected output:**
```
John
```

- `name = "John"` → Create a variable called `name` and store the text (called a **string**) `"John"` in it.
- `print(name)` → Python looks up `name`, finds `"John"`, and prints it.

---

**Example 3 — Multiple variables:**

```python
x = 5
y = "John"
print(x)
print(y)
```

**Expected output:**
```
5
John
```

You can create as many variables as you need. Each one stores its own value independently.

---

### Variables Can Change Type

In many programming languages, once you say a variable holds a number, it can *only* hold numbers. Python is more flexible — a variable can hold different types of data at different times. This is called **dynamic typing**.

```python
x = 4        # x is an integer (a whole number)
x = "Sally"  # Now x is a string (text)
print(x)
```

**Expected output:**
```
Sally
```

The variable `x` first held the number `4`. Then we reassigned it to hold the text `"Sally"`. Python updated it without complaint. The old value `4` is gone.

> **Thinking prompt:** What would happen if you added a third line: `x = 3.14`? What would `print(x)` show then?

---

### Casting — Forcing a Specific Data Type

Sometimes you want to make absolutely sure a variable stores a specific type of data. You do this with **casting** — using built-in functions to convert values.

| Function | What it does | Example |
|---|---|---|
| `str(...)` | Converts to text (string) | `str(3)` → `'3'` |
| `int(...)` | Converts to a whole number (integer) | `int(3)` → `3` |
| `float(...)` | Converts to a decimal number | `float(3)` → `3.0` |

**Example:**

```python
x = str(3)    # x will be '3' (text)
y = int(3)    # y will be 3 (whole number)
z = float(3)  # z will be 3.0 (decimal number)

print(x)
print(y)
print(z)
```

**Expected output:**
```
3
3
3.0
```

Notice how `x` printed `3` (looks the same) but it is actually stored as text, not a number. And `z` printed `3.0` — the `.0` shows it is stored as a decimal (float).

---

### Checking the Type of a Variable

Curious what type of data a variable holds? Use the built-in `type()` function. It tells you exactly what kind of value is stored.

```python
x = 5
y = "John"
print(type(x))
print(type(y))
```

**Expected output:**
```
<class 'int'>
<class 'str'>
```

- `int` means **integer** — a whole number (no decimal point).
- `str` means **string** — text.

You will learn much more about data types in the next lesson. For now, just know that `type()` is a useful tool to check your work.

---

### Single Quotes or Double Quotes?

When storing text in a variable, you can use either single quotes `'...'` or double quotes `"..."`. They work exactly the same way.

```python
x = "John"
# is the same as
x = 'John'
print(x)
```

**Expected output:**
```
John
```

Use whichever style you prefer — but try to stay consistent throughout your code.

---

### Case-Sensitivity: Capital Letters Matter!

Python is **case-sensitive**. This means `age`, `Age`, and `AGE` are three completely different variables. A capital letter makes it a different name.

```python
a = 4
A = "Sally"
print(a)
print(A)
```

**Expected output:**
```
4
Sally
```

`a` and `A` are two separate variables. `A = "Sally"` does **not** overwrite `a = 4`. They live independently.

> **Common mistake:** Writing `Print(x)` instead of `print(x)`. Python is case-sensitive about built-in functions too! `Print` with a capital P will cause an error.

---

## PART 3 — Variable Names

---

### Rules for Naming Variables

Variable names are not completely free — Python has rules. If you break these rules, Python will give you an error and your program will not run.

**The rules are:**

1. A variable name must start with a **letter** (a–z, A–Z) or an **underscore** `_`.
2. A variable name **cannot** start with a number.
3. A variable name can only contain **letters, numbers, and underscores** — no spaces, no hyphens, no symbols.
4. Variable names are **case-sensitive** (`age` ≠ `Age` ≠ `AGE`).
5. Variable names **cannot** be Python **reserved keywords** (special words Python already uses, like `print`, `if`, `for`, `while`, etc.).

**Legal (valid) variable names:**

```python
myvar = "John"
my_var = "John"
_my_var = "John"
myVar = "John"
MYVAR = "John"
myvar2 = "John"
```

All of the above are perfectly fine variable names.

**Illegal (invalid) variable names — these cause errors:**

```python
2myvar = "John"    # ERROR: cannot start with a number
my-var = "John"    # ERROR: hyphens are not allowed
my var = "John"    # ERROR: spaces are not allowed
```

If you try running any of these, Python will give you a `SyntaxError`.

---

### Naming Conventions — How Professionals Name Variables

Beyond the strict rules, professional programmers follow certain *styles* to make their code readable. For Python, the three most common styles for multi-word variable names are:

**1. Camel Case** — Start each word (except the first) with a capital letter:
```python
myVariableName = "John"
```

**2. Pascal Case** — Start every word with a capital letter:
```python
MyVariableName = "John"
```

**3. Snake Case** — Use underscores between words (this is the *recommended Python style*):
```python
my_variable_name = "John"
```

> **Best practice for Python:** The official Python style guide (called PEP 8) recommends **snake_case** for variable names. This is what you will see in professional Python code and most tutorials. Examples: `student_name`, `total_score`, `average_temperature`.

---

### Descriptive Names Are Better Than Short Names

A variable named `x` tells you nothing. A variable named `student_age` tells you exactly what it stores. Use descriptive names.

```python
# Hard to understand:
x = 18
y = "Amara"

# Easy to understand:
student_age = 18
student_name = "Amara"
```

Both versions work the same way in Python. But the second version is much easier to read and maintain.

---

## PART 4 — Assigning Multiple Values

---

### Assigning Different Values to Multiple Variables at Once

Python has a shortcut: you can assign values to multiple variables in a single line, separating everything with commas.

**Syntax:**
```python
variable1, variable2, variable3 = value1, value2, value3
```

**Example:**

```python
x, y, z = "Orange", "Banana", "Cherry"
print(x)
print(y)
print(z)
```

**Expected output:**
```
Orange
Banana
Cherry
```

Python matched them up in order: `x` gets `"Orange"`, `y` gets `"Banana"`, `z` gets `"Cherry"`.

> **Important:** The number of variable names on the left must match the number of values on the right. If they don't match, Python will give you a `ValueError`.

**Example of the error to avoid:**
```python
# This causes an error:
x, y = "Orange", "Banana", "Cherry"  # 2 names, 3 values — mismatch!
```

---

### Assigning the Same Value to Multiple Variables at Once

If you want several variables to hold the same value, you can chain assignments together.

```python
x = y = z = "Orange"
print(x)
print(y)
print(z)
```

**Expected output:**
```
Orange
Orange
Orange
```

All three variables (`x`, `y`, `z`) now store the string `"Orange"`. This is very useful when setting up default values.

---

### Unpacking a Collection

If you have a list (a collection of values), you can "unpack" it — assign each item in the list to its own variable, all in one line.

```python
fruits = ["apple", "banana", "cherry"]
x, y, z = fruits
print(x)
print(y)
print(z)
```

**Expected output:**
```
apple
banana
cherry
```

- `fruits` is a list containing three items.
- `x, y, z = fruits` unpacks those three items into three separate variables.
- `x` gets `"apple"`, `y` gets `"banana"`, `z` gets `"cherry"`.

This technique is used constantly in real Python programs — for example, when reading rows from a spreadsheet or receiving data from a web API.

---

## PART 5 — Output Variables

---

### Printing a Single Variable

The simplest way to display a variable's value is to pass it to `print()`:

```python
x = "Python is awesome"
print(x)
```

**Expected output:**
```
Python is awesome
```

---

### Printing Multiple Variables in One `print()` Statement

You can print several variables together by separating them with commas inside `print()`. Python automatically adds a space between them.

```python
x = "Python"
y = "is"
z = "awesome"
print(x, y, z)
```

**Expected output:**
```
Python is awesome
```

Python put a space between each variable for you — that is the default behaviour of `print()` with commas.

---

### Combining Variables with the `+` Operator

You can also join (concatenate) variables using the `+` operator. This works for text (strings):

```python
x = "Python "
y = "is "
z = "awesome"
print(x + y + z)
```

**Expected output:**
```
Python is awesome
```

Notice there is a space inside `"Python "` and `"is "` — because `+` does not add spaces automatically (unlike commas).

> **Watch out:** You can only use `+` to join variables of the same type. Adding a number to a text string causes an error.

**This causes an error:**
```python
x = 5
y = "John"
print(x + y)  # TypeError: cannot mix int and str
```

**The fix:** Convert the number to a string first using `str()`:
```python
x = 5
y = "John"
print(str(x) + " " + y)
```

**Expected output:**
```
5 John
```

---

### The Best Way to Print Variables: f-strings

The cleanest, most professional way to print variables mixed with text is using **f-strings** (formatted strings). An f-string starts with the letter `f` before the quote, and you put variable names inside curly braces `{}`.

```python
name = "Amara"
age = 18
print(f"My name is {name} and I am {age} years old.")
```

**Expected output:**
```
My name is Amara and I am 18 years old.
```

This approach works with all data types (text, numbers, decimals) without any conversion needed. You will use f-strings constantly in real Python programming.

---

## PART 6 — Global Variables

---

### What Is Scope?

Before understanding global variables, you need to understand **scope** — the idea of *where* a variable can be seen and used in your program.

Think of it like this: imagine you write a note and put it inside a locked box. Only people who have the key to that box can read the note. In Python, **functions** (blocks of reusable code you will learn later) work like locked boxes. Variables created inside a function are only visible *inside* that function.

- A **local variable** is created inside a function. It only exists inside that function.
- A **global variable** is created outside all functions. It can be seen and used anywhere in the program.

---

### Global Variables

A variable created at the top level of your script (outside any function) is called a **global variable**. It is accessible from everywhere in the program.

```python
x = "awesome"

def myfunc():
    print("Python is " + x)

myfunc()
```

**Expected output:**
```
Python is awesome
```

- `x = "awesome"` is created *outside* `myfunc()` — it is a global variable.
- Inside `myfunc()`, Python can still see `x` because global variables are visible everywhere.
- `myfunc()` calls the function to run it.

---

### Local Variables

If you create a variable *inside* a function, it is local — it only exists inside that function.

```python
def myfunc():
    x = "fantastic"
    print("Python is " + x)

myfunc()
```

**Expected output:**
```
Python is fantastic
```

Here, `x = "fantastic"` is created *inside* `myfunc()`. It is a local variable. It exists only while the function is running and disappears after.

---

### When a Local Variable Has the Same Name as a Global Variable

This is where beginners often get confused. When a function creates a local variable with the same name as a global variable, the local one takes over *inside* the function — but the global one stays unchanged *outside*.

```python
x = "awesome"

def myfunc():
    x = "fantastic"
    print("Python is " + x)

myfunc()
print("Python is " + x)
```

**Expected output:**
```
Python is fantastic
Python is awesome
```

- Inside `myfunc()`, the local `x = "fantastic"` takes priority.
- Outside `myfunc()`, the global `x = "awesome"` is untouched.

---

### The `global` Keyword — Modifying a Global Variable from Inside a Function

Normally, when you create a variable inside a function, Python treats it as local. But what if you want to create or modify a **global** variable from inside a function? You use the `global` keyword to tell Python to use the global version.

**Example 1 — Creating a global variable inside a function:**

```python
def myfunc():
    global x
    x = "fantastic"

myfunc()
print("Python is " + x)
```

**Expected output:**
```
Python is fantastic
```

- `global x` tells Python: "The `x` I am about to create/modify is the global `x`, not a local one."
- After `myfunc()` runs, the global `x` now holds `"fantastic"`.
- `print("Python is " + x)` runs outside the function and uses the global `x`.

**Example 2 — Modifying an existing global variable inside a function:**

```python
x = "awesome"

def myfunc():
    global x
    x = "fantastic"

myfunc()
print("Python is " + x)
```

**Expected output:**
```
Python is fantastic
```

Without the `global x` keyword, this function would create a local copy instead of modifying the real global variable. The `global` keyword ensures we modify the actual global one.

> **Real-world use case:** In a game program, you might have a global variable called `score = 0`. Every function that gives the player points needs to use `global score` to actually update the shared score — otherwise each function would just create its own local copy.

---

## PART 7 — Guided Practice Exercises

---

### Exercise 1 — Writing Useful Comments

**Objective:** Practice adding meaningful comments to code.

**Scenario:** You are writing a program that calculates a student's final grade.

**Task:** Copy this code and add a comment above each line explaining what it does:

```python
student_name = "Chidera"
score = 85
passing_score = 50
print(student_name)
print(score)
print(score >= passing_score)
```

**One possible solution:**

```python
# Store the student's full name
student_name = "Chidera"

# Store the student's exam score out of 100
score = 85

# Define the minimum score needed to pass
passing_score = 50

# Print the student's name
print(student_name)

# Print the student's score
print(score)

# Print True if the student passed, False if they failed
print(score >= passing_score)
```

**Expected output:**
```
Chidera
85
True
```

**Self-check questions:**
- Did your comments explain the *purpose* of each line, not just what Python does mechanically?
- Are your comments concise and easy to read?

---

### Exercise 2 — Creating and Printing Variables

**Objective:** Create variables to store information about a person and print them.

**Scenario:** You are building a simple student record system.

**Steps:**
1. Create a variable `student_name` and store your own name in it.
2. Create a variable `student_age` and store your age in it.
3. Create a variable `student_class` and store your class name (e.g., `"SS2"`) in it.
4. Print all three variables using an f-string in one `print()` statement.

**Expected code:**

```python
student_name = "Amara"
student_age = 17
student_class = "SS2"

print(f"Name: {student_name}, Age: {student_age}, Class: {student_class}")
```

**Expected output:**
```
Name: Amara, Age: 17, Class: SS2
```

**What-if challenge:** What happens if you change `student_age` to a string like `"seventeen"` instead of the number `17`? Try it and observe.

---

### Exercise 3 — Multiple Assignment

**Objective:** Use both forms of multiple assignment.

**Scenario:** Track the three top scores in a class quiz.

**Task:** Assign `95`, `87`, and `76` to variables `first_place`, `second_place`, and `third_place` in a single line, then print all three.

**Solution:**

```python
first_place, second_place, third_place = 95, 87, 76

print(f"1st Place: {first_place}")
print(f"2nd Place: {second_place}")
print(f"3rd Place: {third_place}")
```

**Expected output:**
```
1st Place: 95
2nd Place: 87
3rd Place: 76
```

**Bonus:** Now assign the same default score `0` to three variables `player1`, `player2`, `player3` in one line.

```python
player1 = player2 = player3 = 0
print(player1, player2, player3)
```

**Expected output:**
```
0 0 0
```

---

### Exercise 4 — Global vs Local Variables

**Objective:** Understand the difference between global and local scope.

**Scenario:** A simple game program needs a shared score.

```python
# Global score starts at zero
score = 0

def award_bonus():
    global score
    score = score + 50   # Add 50 bonus points

def award_points():
    global score
    score = score + 10   # Add 10 regular points

award_points()
award_points()
award_bonus()

print(f"Final score: {score}")
```

**Expected output:**
```
Final score: 70
```

**Trace through the logic:**
- `score` starts at `0`.
- `award_points()` adds 10 → `score = 10`
- `award_points()` adds 10 again → `score = 20`
- `award_bonus()` adds 50 → `score = 70`
- `print` shows `70`

**Self-check:** What would happen if you removed both `global score` lines? Try it and read the error message.

---

## PART 8 — Mini Project: Student Profile Card

---

### Project Overview

You will build a simple Python program that creates a complete profile card for a student and prints it in a formatted, readable way. This project combines comments, variables, multiple assignment, output formatting, and global variables.

---

### Stage 1 — Setup the Student Data

```python
# =============================================
# STUDENT PROFILE CARD — Mini Project
# =============================================

# Student personal information
student_name = "Fatima Bello"
student_age = 16
student_gender = "Female"
student_class = "JSS3"
student_school = "Unity Secondary School"
```

**What we did:**
- Used comments to label the section clearly (the `===` border is a common style trick for section headers in comments).
- Created five variables to store different kinds of information about the student.

---

### Stage 2 — Add Academic Information

```python
# Subject scores
english_score = 78
mathematics_score = 91
science_score = 85

# Calculate the average score (sum of all scores divided by number of subjects)
average_score = (english_score + mathematics_score + science_score) / 3

# Define the passing mark
passing_mark = 50
```

**What we did:**
- Created three score variables for different subjects.
- Calculated the average by adding all three scores and dividing by 3. Python handles the arithmetic automatically.
- Stored the minimum passing mark in a variable so it can be changed in one place if needed.

---

### Stage 3 — Global Status Variable

```python
# Global variable: overall pass/fail status
status = "Not determined"

def evaluate_student():
    global status
    if average_score >= passing_mark:
        status = "PASSED"
    else:
        status = "FAILED"

evaluate_student()
```

**What we did:**
- Created a global `status` variable that starts with a placeholder text.
- Defined a function `evaluate_student()` that uses `global status` to update the real global variable.
- Called the function to evaluate the student.

---

### Stage 4 — Print the Final Profile Card

```python
# =============================================
# PRINTING THE PROFILE CARD
# =============================================

print("=" * 40)
print("        STUDENT PROFILE CARD")
print("=" * 40)
print(f"Name        : {student_name}")
print(f"Age         : {student_age}")
print(f"Gender      : {student_gender}")
print(f"Class       : {student_class}")
print(f"School      : {student_school}")
print("-" * 40)
print(f"English     : {english_score}")
print(f"Mathematics : {mathematics_score}")
print(f"Science     : {science_score}")
print(f"Average     : {average_score:.1f}")
print("-" * 40)
print(f"Result      : {status}")
print("=" * 40)
```

**Expected output:**
```
========================================
        STUDENT PROFILE CARD
========================================
Name        : Fatima Bello
Age         : 16
Gender      : Female
Class       : JSS3
School      : Unity Secondary School
----------------------------------------
English     : 78
Mathematics : 91
Science     : 85
Average     : 84.7
----------------------------------------
Result      : PASSED
========================================
```

**Line-by-line explanation:**
- `"=" * 40` → This repeats the `=` character 40 times, creating a divider line. This is a string multiplication trick in Python.
- `f"Average     : {average_score:.1f}"` → The `:.1f` inside the curly braces tells Python to format the number to 1 decimal place.
- The rest uses f-strings to neatly display each piece of information.

---

### Stage 5 — Full Project Code (All Together)

```python
# =============================================
# STUDENT PROFILE CARD — Mini Project
# =============================================

# Student personal information
student_name = "Fatima Bello"
student_age = 16
student_gender = "Female"
student_class = "JSS3"
student_school = "Unity Secondary School"

# Subject scores
english_score = 78
mathematics_score = 91
science_score = 85

# Calculate the average score
average_score = (english_score + mathematics_score + science_score) / 3

# Define the passing mark
passing_mark = 50

# Global variable: overall pass/fail status
status = "Not determined"

def evaluate_student():
    global status
    if average_score >= passing_mark:
        status = "PASSED"
    else:
        status = "FAILED"

evaluate_student()

# =============================================
# PRINTING THE PROFILE CARD
# =============================================

print("=" * 40)
print("        STUDENT PROFILE CARD")
print("=" * 40)
print(f"Name        : {student_name}")
print(f"Age         : {student_age}")
print(f"Gender      : {student_gender}")
print(f"Class       : {student_class}")
print(f"School      : {student_school}")
print("-" * 40)
print(f"English     : {english_score}")
print(f"Mathematics : {mathematics_score}")
print(f"Science     : {science_score}")
print(f"Average     : {average_score:.1f}")
print("-" * 40)
print(f"Result      : {status}")
print("=" * 40)
```

---

### Reflection Questions

1. What would happen if you changed `mathematics_score = 91` to `mathematics_score = 20`? Would the student still pass?
2. Why did we use a `global status` keyword inside `evaluate_student()`?
3. What is the benefit of storing `passing_mark = 50` in a variable instead of writing `50` directly in the `if` condition?
4. Try adding a fourth subject: `civic_score = 72`. How would you update the average calculation?

### Optional Advanced Extension

- Add a variable `student_id` that stores a unique ID number for the student.
- Add a subject called `physical_education_score`.
- Change the program to print `"DISTINCTION"` if the average is 80 or above, `"CREDIT"` if 60–79, `"PASS"` if 50–59, and `"FAIL"` below 50.

---

## PART 9 — Common Beginner Mistakes

---

### Mistake 1: Starting a Variable Name with a Number

```python
# WRONG
2name = "Amara"   # SyntaxError

# CORRECT
name2 = "Amara"   # Number at the end is fine
```

---

### Mistake 2: Using Spaces in Variable Names

```python
# WRONG
student name = "Amara"   # SyntaxError

# CORRECT
student_name = "Amara"   # Use underscore instead
```

---

### Mistake 3: Forgetting That Python is Case-Sensitive

```python
name = "Amara"
print(Name)     # NameError: 'Name' is not defined
print(name)     # This works — lowercase 'n'
```

---

### Mistake 4: Adding a Number and a String with `+`

```python
age = 18
message = "I am " + age + " years old."   # TypeError

# CORRECT — convert the number to a string first:
message = "I am " + str(age) + " years old."
print(message)
```

**Expected output:**
```
I am 18 years old.
```

---

### Mistake 5: Mismatched Variables and Values in Multiple Assignment

```python
# WRONG — 3 values, only 2 variable names
x, y = 1, 2, 3    # ValueError: too many values to unpack

# CORRECT — equal numbers on both sides
x, y, z = 1, 2, 3
```

---

### Mistake 6: Forgetting the `global` Keyword

```python
score = 0

def add_points():
    score = score + 10   # UnboundLocalError!

add_points()
```

Python sees that you're trying to use `score` before assigning it locally. Fix:

```python
score = 0

def add_points():
    global score
    score = score + 10   # Now it works

add_points()
print(score)
```

**Expected output:**
```
10
```

---

### Mistake 7: Commenting with `//` (That's JavaScript, Not Python!)

```python
// This is NOT a Python comment  # SyntaxError!
# This IS a Python comment        # Correct!
```

Python uses `#` for comments. `//` is used in JavaScript and other languages.

---

## PART 10 — Reflection Questions

Answer these in your notebook or in your head before moving on:

1. What is a comment and what are the three main reasons to use one?
2. What symbol starts a Python comment?
3. What does the `=` sign do when used with a variable? (Hint: it is not the same as "equals" in maths.)
4. What is the difference between `x = 5` and `x = "5"`? Are they the same?
5. Write two valid variable names for storing someone's date of birth.
6. What is the difference between a global and a local variable?
7. When do you need the `global` keyword inside a function?
8. If you write `x, y, z = 10, 20, 30`, what values do `x`, `y`, and `z` hold?
9. What does `type(x)` return when `x = 3.14`?
10. Why is `student_age` a better variable name than `a`?

---

## PART 11 — Completion Checklist

Before moving to Lesson 03, make sure you can tick off every item below:

- [ ] I can write a single-line comment using `#`
- [ ] I can write an inline comment at the end of a code line
- [ ] I can write a multi-line comment using `#` on each line
- [ ] I can write a multi-line comment using triple quotes `"""..."""`
- [ ] I can create a variable and assign a value to it
- [ ] I understand that Python variables do not need a type declaration
- [ ] I can use `type()` to check what kind of data a variable holds
- [ ] I can use `str()`, `int()`, and `float()` to cast (convert) variable types
- [ ] I know all the rules for valid variable names
- [ ] I know what snake_case naming style is and why Python uses it
- [ ] I can assign different values to multiple variables in one line
- [ ] I can assign the same value to multiple variables in one line
- [ ] I can unpack a list into multiple variables
- [ ] I can print multiple variables using commas in `print()`
- [ ] I can print variables and text together using f-strings
- [ ] I understand what a global variable is
- [ ] I understand what a local variable is
- [ ] I know when and how to use the `global` keyword
- [ ] I completed the Student Profile Card mini project

---

## Lesson Summary

In this lesson you learned two foundational skills for writing Python programs:

**Comments** are lines in your code that Python ignores. They begin with `#` for single lines, or use triple quotes `"""..."""` for blocks of text. Comments make your code readable, explainable, and easier to maintain. They also let you temporarily disable lines during testing.

**Variables** are named containers that store data in your computer's memory. You create a variable by writing `name = value`. Python is dynamically typed, meaning a variable can hold different kinds of data at different times. Variable names must follow strict rules: start with a letter or underscore, contain only letters, numbers, and underscores, and never be a Python reserved keyword.

You learned three ways to assign values: one at a time, multiple different values in a single line, and the same value to many variables at once. You also learned to print variables cleanly using f-strings.

Finally, you learned about **scope**: global variables live outside functions and are visible everywhere, while local variables live inside functions and disappear when the function finishes. Use the `global` keyword when you need to modify a global variable from inside a function.

These skills — commenting and using variables — are used in every single Python program ever written. Mastering them here gives you a rock-solid foundation for everything that comes next.

---

*Next lesson: Python Data Types — learning about the different kinds of values Python can store and work with.*
