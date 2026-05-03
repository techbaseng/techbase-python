---
render_with_liquid: false
title: "Lesson 04 — Python Comments & Variables"
nav_order: 4
---

# Lesson 04 — Python Comments & Variables

---

## Lesson Introduction

Welcome to Lesson 04! In this lesson you are going to learn two of the most important foundational skills in Python programming:

**Comments** — how to write notes inside your code that Python ignores but humans can read.

**Variables** — how to store, name, and work with information in your programs.

These two skills will appear in every single Python program you ever write. By the end of this lesson you will be able to:

- Write single-line and multi-line comments in Python.
- Create variables and assign values to them.
- Follow the rules for naming variables correctly.
- Assign multiple values at once using different techniques.
- Print (display) variables and combine them in output.
- Understand the difference between local variables and global variables.
- Use the `global` keyword correctly.

This lesson is for **absolute beginners**. Every concept is explained from scratch, with analogies, examples, and step-by-step walkthroughs.

---

## Prerequisite Concepts

Before we start, make sure you are comfortable with these ideas from previous lessons:

- You know how to use `print()` to display text on the screen.
- You understand that Python is case-sensitive (`name` ≠ `Name`).
- You understand that Python uses indentation (spaces) to define code blocks.

If any of those feel unclear, quickly review Lesson 01 and Lesson 02 before continuing.

---

## Part 1 — Python Comments

### What is a Comment?

A **comment** is a note you write inside your code. Python completely ignores it — comments are not instructions for the computer, they are messages for human beings (including your future self).

**Why do we need comments?**

Imagine you write a long, complex program today. Six months later you open the file again. Without comments, you might struggle to remember *why* you wrote certain parts the way you did. Comments act like sticky notes on your code, explaining what it does and why.

**Real-world analogy:** Think of comments like the margin notes a student writes in a textbook — the textbook (code) still works without them, but the notes help the reader understand the content much better.

**In professional software development**, comments are essential for team collaboration. If five developers are working on the same codebase, comments help each person understand what the others have written.

### Comments are also used to:
- Temporarily disable a line of code during testing (called "commenting out").
- Explain complex logic.
- Provide authorship or copyright information at the top of a file.
- Document what a function does.

---

### Single-Line Comments

The most common type of comment in Python is the **single-line comment**. You create one by placing a hash symbol (`#`) at the start of a line. Everything to the right of the `#` on that line is ignored by Python.

**Example 1 — A comment on its own line:**

```python
# This is a comment
print("Hello, World!")
```

**Expected Output:**
```
Hello, World!
```

Notice that the comment line produces no output — Python simply skips it. Only the `print()` line runs.

**Example 2 — A comment explaining a line of code:**

```python
# Print a greeting message to the user
print("Welcome to Python!")
```

**Expected Output:**
```
Welcome to Python!
```

**Example 3 — An inline comment (placed after code on the same line):**

You can also put a comment at the end of a line of code. Python will run the code, then ignore the rest of the line after the `#`.

```python
print("Hello, World!")   # This prints a greeting
```

**Expected Output:**
```
Hello, World!
```

The code runs normally. Python executes `print("Hello, World!")`, then sees `#` and ignores everything after it.

> **Thinking prompt:** What do you think happens if you put the `#` at the very start of a line that has `print()` in it?

**Example 4 — Commenting out a line of code:**

```python
# print("This line will NOT run")
print("This line WILL run")
```

**Expected Output:**
```
This line WILL run
```

The first `print()` is "commented out" — it is deactivated. This is incredibly useful when testing and debugging your programs.

---

### Multi-Line Comments

Sometimes you need a comment that spans more than one line. There are two approaches in Python.

#### Approach 1 — Multiple `#` symbols

Simply put a `#` at the start of each comment line.

```python
# This program calculates a student's average score.
# It takes three test scores as input.
# It adds them together and divides by three.
print("Student Grade Calculator")
```

**Expected Output:**
```
Student Grade Calculator
```

#### Approach 2 — Triple-Quoted Strings

Python does not have an official multi-line comment syntax, but developers commonly use **triple-quoted strings** (`"""` or `'''`) as a workaround. A string not assigned to any variable is simply created and immediately discarded — Python ignores it.

```python
"""
This is a multi-line comment.
It spans multiple lines.
Python will not execute any of this.
"""
print("Hello!")
```

**Expected Output:**
```
Hello!
```

> **Important note:** Triple-quoted strings are not *true* comments — they are string literals that Python technically evaluates but does not do anything with. For short notes, always prefer `#`. Triple quotes are more commonly used for **docstrings** (formal documentation inside functions and classes, which you will learn about in later lessons).

**Example — Using both styles together:**

```python
# ============================================
# Author  : Chidi Okafor
# Date    : 2026-05-03
# Purpose : Calculate monthly savings
# ============================================

print("Monthly Savings Calculator")
result = 500 * 12   # Multiply monthly savings by 12 months
print(result)
```

**Expected Output:**
```
Monthly Savings Calculator
6000
```

---

## Part 2 — Python Variables

### What is a Variable?

A **variable** is a named container that stores a piece of information in your program. Think of it like a labelled box: the label (the variable name) lets you find the box again later, and inside the box is the value (the information you stored).

**Analogy:** Imagine a shelf in a market stall with labelled containers:
- A box labelled `price` contains the value `500`
- A box labelled `customer_name` contains the value `"Ngozi"`
- A box labelled `quantity` contains the value `3`

At any point you can look at a box (read the variable), change what is inside (update the variable), or use the value in a calculation.

**Why do we need variables?**

Without variables, you would have to hard-code (write directly) every value in every place you need it. If a price changes, you would need to find and update every single place you wrote it. With a variable, you update it in one place and the change spreads everywhere automatically.

---

### Creating a Variable (Assignment)

In Python, you create a variable by simply writing its name, followed by `=`, followed by the value you want to store. This is called **assignment**.

```
variable_name = value
```

The `=` symbol here is the **assignment operator**. It does NOT mean "equals" in the mathematical sense — it means "store this value in this variable."

**Example 1 — Storing a number:**

```python
age = 25
print(age)
```

**Expected Output:**
```
25
```

**Line-by-line breakdown:**
- `age` — the name of our variable (the label on the box).
- `=` — the assignment operator ("put this into the box").
- `25` — the value we are storing (what goes into the box).
- `print(age)` — look inside the box labelled `age` and display what is there.

**Example 2 — Storing text:**

```python
name = "Fatima"
print(name)
```

**Expected Output:**
```
Fatima
```

**Example 3 — Storing a decimal number:**

```python
price = 149.99
print(price)
```

**Expected Output:**
```
149.99
```

**Example 4 — Multiple variables:**

```python
student_name = "Emeka"
student_age = 19
student_gpa = 3.75
print(student_name)
print(student_age)
print(student_gpa)
```

**Expected Output:**
```
Emeka
19
3.75
```

---

### Python Does Not Require a Type Declaration

In some other programming languages (like Java or C++), when you create a variable you must declare what *type* of data it will hold:

```java
// Java — you must say "int" (integer) before the variable name
int age = 25;
String name = "Emeka";
```

In Python, **you do not need to do this**. Python automatically figures out the type of data based on the value you assign. This makes Python much faster to write.

```python
# Python — no type needed, Python figures it out
age = 25          # Python knows this is a whole number (integer)
name = "Emeka"    # Python knows this is text (string)
price = 149.99    # Python knows this is a decimal number (float)
```

This feature is called **dynamic typing** — the type is determined at runtime based on what value you give the variable.

---

### Variables Can Change (That Is Why They Are Called "Variables"!)

A variable's value can be changed (updated) at any time by simply assigning a new value to it.

```python
x = 10
print(x)

x = 50
print(x)

x = x + 5    # Take the current value of x, add 5, store the result back in x
print(x)
```

**Expected Output:**
```
10
50
55
```

**Thinking prompt:** On the line `x = x + 5`, what is happening? The right side (`x + 5`) is evaluated first using the *current* value of x (which is 50), giving 55. Then that result is stored back into `x`. So `x` becomes 55.

---

### Variables Are Case-Sensitive

Remember from Lesson 01: Python treats uppercase and lowercase letters as completely different characters. So `age`, `Age`, and `AGE` are three entirely separate variables.

```python
age = 30
Age = 45
AGE = 99

print(age)   # prints 30
print(Age)   # prints 45
print(AGE)   # prints 99
```

**Expected Output:**
```
30
45
99
```

This is a frequent source of bugs for beginners! Always be consistent with how you write variable names.

---

## Part 3 — Python Variable Names (Naming Rules and Conventions)

### Why Naming Rules Matter

Variables must be named according to Python's rules. If you break these rules, Python will give you an error. Beyond the rules, there are also **conventions** — best practices that experienced programmers follow to make code readable.

---

### The Official Rules (You MUST Follow These)

These are not suggestions — breaking any of these will cause a `SyntaxError` or `NameError`.

**Rule 1 — A variable name must start with a letter or an underscore (`_`)**

```python
name = "Tunde"        # ✅ Starts with a letter
_score = 95           # ✅ Starts with underscore
2name = "Error"       # ❌ Starts with a number — INVALID
```

**Rule 2 — A variable name can only contain letters, numbers, and underscores**

No spaces, no hyphens, no dots, no special characters.

```python
student_name = "Amaka"    # ✅ Uses letters and underscore
studentName = "Amaka"     # ✅ Uses letters only
student-name = "Amaka"    # ❌ Hyphen not allowed
student name = "Amaka"    # ❌ Space not allowed
student.name = "Amaka"    # ❌ Dot not allowed
```

**Rule 3 — Variable names are case-sensitive**

```python
colour = "blue"
Colour = "red"
COLOUR = "green"
# These are THREE different variables
```

**Rule 4 — Variable names cannot be Python keywords (reserved words)**

Python has special reserved words that have built-in meaning. You cannot use them as variable names. Examples:

`if`, `else`, `for`, `while`, `True`, `False`, `None`, `import`, `return`, `def`, `class`, `and`, `or`, `not`, `in`, `is`, `pass`, `break`, `continue`, `try`, `except`, `lambda`, `with`, `as`, `global`, `del`, `yield`, `raise`, `assert`, `from`

```python
if = 5        # ❌ 'if' is a reserved keyword
return = 10   # ❌ 'return' is a reserved keyword
for = "loop"  # ❌ 'for' is a reserved keyword
```

You can see the full list of Python keywords by running:
```python
import keyword
print(keyword.kwlist)
```

---

### Best Practice Conventions (You SHOULD Follow These)

These are not enforced by Python, but professional developers follow them for readability.

**Convention 1 — Use snake_case for variable names**

`snake_case` means all lowercase letters with underscores between words. This is the Python standard (defined in a style guide called PEP 8).

```python
# ✅ Recommended (snake_case)
student_age = 20
monthly_salary = 85000
total_score = 98.5

# ❌ Not recommended
StudentAge = 20         # This style is for class names in Python
monthlySalary = 85000   # This is camelCase — common in JavaScript but not Python
TOTAL_SCORE = 98.5      # ALL_CAPS is reserved for constants (values that never change)
```

**Convention 2 — Use meaningful, descriptive names**

A variable name should clearly describe what the variable contains.

```python
# ❌ Bad — what does 'x' or 'd' mean?
x = 85000
d = 365

# ✅ Good — instantly understandable
annual_salary = 85000
days_in_year = 365
```

**Convention 3 — Use ALL_CAPS for constants**

A **constant** is a variable whose value never changes (like the speed of light or the value of Pi). By convention, constants are written in ALL CAPS.

```python
PI = 3.14159
MAX_STUDENTS = 50
COUNTRY_CODE = "NG"
```

**Convention 4 — Keep names reasonably short but not cryptic**

```python
# Too short (cryptic)
n = "Adaeze"

# Too long (annoying to type)
the_full_name_of_the_student_enrolled_in_the_course = "Adaeze"

# Just right
student_name = "Adaeze"
```

---

### Valid and Invalid Name Examples

| Variable Name | Valid? | Why |
|---------------|--------|-----|
| `my_var` | ✅ Yes | Letters and underscore |
| `myvar` | ✅ Yes | All letters |
| `_myvar` | ✅ Yes | Starts with underscore |
| `myVar` | ✅ Yes | Letters only (camelCase — works but not recommended) |
| `MYVAR` | ✅ Yes | All caps — valid (use for constants) |
| `myvar2` | ✅ Yes | Letters and number |
| `my-var` | ❌ No | Hyphen not allowed |
| `my var` | ❌ No | Space not allowed |
| `2myvar` | ❌ No | Starts with a number |
| `my.var` | ❌ No | Dot not allowed |

---

## Part 4 — Assigning Multiple Values

Python offers several clever shortcuts for assigning values to multiple variables at once.

### Method 1 — Assign Multiple Values to Multiple Variables (One Line)

You can assign different values to different variables on a single line by separating them with commas.

```python
x, y, z = "Orange", "Banana", "Cherry"
print(x)
print(y)
print(z)
```

**Expected Output:**
```
Orange
Banana
Cherry
```

**How it works:** Python matches them up in order — `x` gets `"Orange"`, `y` gets `"Banana"`, `z` gets `"Cherry"`. The number of variables on the left must exactly match the number of values on the right.

**What happens if the counts do not match:**

```python
x, y = "Apple", "Banana", "Cherry"   # ❌ 2 variables, 3 values
```

**Error:**
```
ValueError: too many values to unpack (expected 2)
```

**Practical use case:**

```python
length, width, height = 10, 5, 3
volume = length * width * height
print(volume)
```

**Expected Output:**
```
150
```

---

### Method 2 — Assign One Value to Multiple Variables (One Line)

If you want all variables to start with the same value, you can chain assignment operators.

```python
x = y = z = 0
print(x)
print(y)
print(z)
```

**Expected Output:**
```
0
0
0
```

**Practical use case — resetting counters:**

```python
errors = warnings = skipped = 0
print(errors)
print(warnings)
print(skipped)
```

**Expected Output:**
```
0
0
0
```

---

### Method 3 — Unpacking a Collection

If you have a list (a collection of items), you can "unpack" it directly into individual variables.

```python
fruits = ["apple", "banana", "cherry"]
x, y, z = fruits
print(x)
print(y)
print(z)
```

**Expected Output:**
```
apple
banana
cherry
```

**How it works:** Python takes the items out of the list one by one and puts them into the variables in the same order.

> **Note:** We will learn much more about lists in a future lesson. For now, just know this technique exists.

**Swapping two variables in one line:**

Here is a beautiful Python trick — you can swap the values of two variables without needing a temporary third variable:

```python
a = 10
b = 20

print("Before swap:")
print(a)   # 10
print(b)   # 20

a, b = b, a   # Swap!

print("After swap:")
print(a)   # 20
print(b)   # 10
```

**Expected Output:**
```
Before swap:
10
20
After swap:
20
10
```

In most other languages you would need a temporary variable:
```python
temp = a
a = b
b = temp
```
Python's one-line swap is much more elegant.

---

## Part 5 — Output Variables (Printing Variables)

You already know the `print()` function. Now let us explore all the ways you can display variable values.

### Method 1 — Printing a Single Variable

The simplest way:

```python
name = "Ngozi"
print(name)
```

**Expected Output:**
```
Ngozi
```

---

### Method 2 — Printing Multiple Variables with Commas (Recommended)

You can pass multiple variables to `print()` by separating them with commas. Python automatically adds a space between them.

```python
first_name = "Emeka"
last_name = "Obi"
age = 22
print(first_name, last_name, age)
```

**Expected Output:**
```
Emeka Obi 22
```

You can also mix variables and literal text (strings) in the same print:

```python
name = "Amara"
age = 19
print("Name:", name, "| Age:", age)
```

**Expected Output:**
```
Name: Amara | Age: 19
```

---

### Method 3 — String Concatenation with `+`

You can join (concatenate) strings together using the `+` operator.

```python
first_name = "Chidi"
last_name = "Okafor"
print("Full name: " + first_name + " " + last_name)
```

**Expected Output:**
```
Full name: Chidi Okafor
```

> **Important warning:** The `+` operator can only join strings with strings. If you try to join a string with a number, Python will give an error:

```python
age = 25
print("Age: " + age)    # ❌ Error!
```

**Error:**
```
TypeError: can only concatenate str (not "int") to str
```

**Fix — convert the number to a string first using `str()`:**

```python
age = 25
print("Age: " + str(age))    # ✅ Works!
```

**Expected Output:**
```
Age: 25
```

---

### Method 4 — f-Strings (The Modern and Best Way) ⭐

**f-strings** (formatted string literals) are the most powerful and readable way to include variable values inside text. Just put the letter `f` before the opening quote, then write variable names inside `{}` curly brackets.

```python
name = "Tunde"
age = 21
city = "Lagos"

print(f"My name is {name}, I am {age} years old, and I live in {city}.")
```

**Expected Output:**
```
My name is Tunde, I am 21 years old, and I live in Lagos.
```

**Why f-strings are the best approach:**
- No type conversion needed — numbers, text, all types work directly.
- Easy to read — you can see exactly where each variable will appear.
- Can include expressions directly inside the `{}`:

```python
price = 200
quantity = 5
print(f"Total cost: {price * quantity} Naira")
```

**Expected Output:**
```
Total cost: 1000 Naira
```

The calculation `price * quantity` happens *inside* the f-string!

---

### Summary of Output Methods

```python
name = "Adaeze"
age = 23

# Method 1 — single variable
print(name)

# Method 2 — multiple variables with commas
print(name, age)

# Method 3 — concatenation (strings only, numbers need str())
print("Name: " + name + ", Age: " + str(age))

# Method 4 — f-string (recommended)
print(f"Name: {name}, Age: {age}")
```

**Expected Output:**
```
Adaeze
Adaeze 23
Name: Adaeze, Age: 23
Name: Adaeze, Age: 23
```

---

## Part 6 — Global Variables

### What is Scope?

Before we explain global variables, we need to understand the concept of **scope**. Scope refers to *where* in your code a variable can be accessed.

Think of it like rooms in a house. A variable created inside a specific room (a function) only exists inside that room. If you go outside that room, the variable is gone. A variable created in the main hallway (outside all rooms) can be seen from everywhere in the house.

### Local Variables

A variable created **inside a function** is called a **local variable**. It only exists while that function is running, and it can only be accessed from inside that function.

```python
def greet():
    message = "Hello from inside the function!"   # This is a LOCAL variable
    print(message)

greet()
# print(message)   # ← If you uncomment this, it would cause an error!
```

**Expected Output:**
```
Hello from inside the function!
```

If you tried to print `message` outside the function, Python would say `NameError: name 'message' is not defined` — because `message` only exists *inside* `greet()`.

> **Note:** We cover functions in detail in a later lesson. For now, just understand that a function is a block of code that does a specific job, defined with the `def` keyword.

---

### Global Variables

A variable created **outside all functions** — at the top level of your program — is called a **global variable**. It can be accessed from anywhere in the program, including from inside functions.

```python
country = "Nigeria"   # This is a GLOBAL variable

def show_country():
    print(country)    # Accessing the global variable from inside a function

show_country()
print(country)        # Accessing it from outside the function too
```

**Expected Output:**
```
Nigeria
Nigeria
```

Both the function and the main code can read the global variable `country`.

---

### The Problem: Modifying a Global Variable from Inside a Function

Here is an important and tricky situation. If you try to *change* (reassign) a global variable from inside a function, Python does not modify the global one — it creates a *new local variable* with the same name instead.

```python
score = 100    # Global variable

def update_score():
    score = 200    # Python creates a NEW local variable called 'score'
    print(f"Inside function: {score}")

update_score()
print(f"Outside function: {score}")   # The global 'score' is unchanged!
```

**Expected Output:**
```
Inside function: 200
Outside function: 100
```

This can be confusing! The function seems to have changed `score`, but it actually just created its own private copy. The global `score` is still 100.

---

### The `global` Keyword

To tell Python "I want to modify the actual global variable from inside this function", use the `global` keyword before the variable name.

```python
score = 100    # Global variable

def update_score():
    global score       # ← "I want to work with the GLOBAL 'score'"
    score = 200        # Now this modifies the actual global variable
    print(f"Inside function: {score}")

update_score()
print(f"Outside function: {score}")   # Global 'score' IS now changed!
```

**Expected Output:**
```
Inside function: 200
Outside function: 200
```

Now the global variable is truly updated.

---

### Creating a Global Variable Inside a Function

You can even *create* a global variable from inside a function using the `global` keyword:

```python
def create_greeting():
    global greeting      # Declare 'greeting' as global
    greeting = "Hello!"  # Create it and assign a value

create_greeting()        # Run the function to create the variable
print(greeting)          # Now accessible outside the function
```

**Expected Output:**
```
Hello!
```

---

### When to Use Global Variables

**Use global variables sparingly.** Overusing them makes programs harder to understand and debug because any function can change them at any time. As a beginner, a good rule of thumb is:

- Use global variables only for values that truly need to be shared across your entire program (like configuration settings).
- For everything else, pass values to functions as **arguments** (you will learn about this in the functions lesson).

---

### Comparing Local vs. Global — A Full Example

```python
# ========================================
# Global variable — accessible everywhere
# ========================================
school_name = "Ibadan Polytechnic"

def display_student():
    # Local variable — only accessible inside this function
    student_name = "Blessing"
    print(f"Student: {student_name}")
    print(f"School : {school_name}")   # Can read the global variable

def display_school():
    # This function also accesses the global variable
    print(f"Welcome to {school_name}!")

display_student()
display_school()

# print(student_name)  # ← Would cause NameError — student_name is local to display_student
```

**Expected Output:**
```
Student: Blessing
School : Ibadan Polytechnic
Welcome to Ibadan Polytechnic!
```

---

## Part 7 — Variable Exercises (From W3Schools)

The following exercises are based on the W3Schools Python Variable Exercises. Try each one yourself before reading the solution.

---

### Exercise A — Create and Print a Variable

**Task:** Create a variable called `carname` and assign the value `"Volvo"` to it.

**Your code should produce this output:**
```
Volvo
```

**Solution:**
```python
carname = "Volvo"
print(carname)
```

---

### Exercise B — Change the Value of a Variable

**Task:** Create a variable called `x` with value `50`. Change the value of `x` to `80`.

**Expected Output (after the change):**
```
80
```

**Solution:**
```python
x = 50
x = 80
print(x)
```

---

### Exercise C — Assign Multiple Variables in One Line

**Task:** Create three variables `x`, `y`, `z` in one line. Assign values `1`, `2`, `3` respectively.

**Expected Output:**
```
1
2
3
```

**Solution:**
```python
x, y, z = 1, 2, 3
print(x)
print(y)
print(z)
```

---

### Exercise D — Assign the Same Value to Multiple Variables

**Task:** Assign the value `"Orange"` to all three variables `x`, `y`, `z` in one line.

**Expected Output:**
```
Orange
Orange
Orange
```

**Solution:**
```python
x = y = z = "Orange"
print(x)
print(y)
print(z)
```

---

### Exercise E — Unpack a List

**Task:** Given the list `fruits = ["apple", "banana", "cherry"]`, unpack the list into variables `x`, `y`, `z`.

**Expected Output:**
```
apple
banana
cherry
```

**Solution:**
```python
fruits = ["apple", "banana", "cherry"]
x, y, z = fruits
print(x)
print(y)
print(z)
```

---

### Exercise F — Global Variable with `global` Keyword

**Task:** Call the function below and make sure the global variable `x` is changed to `"Python"` inside the function.

```python
x = "awesome"

def myfunc():
    # Your code here — make x = "Python" and update the global variable
    pass

myfunc()
print("Python is " + x)
```

**Expected Output:**
```
Python is Python
```

**Solution:**
```python
x = "awesome"

def myfunc():
    global x
    x = "Python"

myfunc()
print("Python is " + x)
```

---

## Guided Practice Exercises

Now let us practise with more realistic scenarios.

---

### Practice 1 — Student Report Card (Variables + Output)

**Objective:** Store student information in variables and display it in a formatted report.

**Scenario:** You are building a simple student report system for a school.

**Steps:**
1. Create variables for: `student_name`, `subject`, `score_1`, `score_2`, `score_3`.
2. Calculate the `average` (sum of three scores divided by 3).
3. Print a formatted report using f-strings.
4. Add comments explaining each section.

**Starter code:**

```python
# ============================================
# Student Report Card
# ============================================

# Student information
student_name = "Adaobi Nwosu"
subject = "Mathematics"
score_1 = 78
score_2 = 85
score_3 = 91

# Calculate average
average = (score_1 + score_2 + score_3) / 3

# Display the report
print("============================================")
print(f"  STUDENT REPORT CARD")
print("============================================")
print(f"Name    : {student_name}")
print(f"Subject : {subject}")
print(f"Test 1  : {score_1}")
print(f"Test 2  : {score_2}")
print(f"Test 3  : {score_3}")
print(f"Average : {average:.1f}")   # :.1f means 1 decimal place
print("============================================")
```

**Expected Output:**
```
============================================
  STUDENT REPORT CARD
============================================
Name    : Adaobi Nwosu
Subject : Mathematics
Test 1  : 78
Test 2  : 85
Test 3  : 91
Average : 84.7
============================================
```

**Self-check questions:**
- What is `:.1f` inside the f-string? (It formats the number to 1 decimal place.)
- What would the average be if all three scores were 100?
- Try changing the scores and see if the average updates automatically.

**What-if challenge:** Add a `grade` variable:
- Average 90–100 → `grade = "A"`
- Average 80–89 → `grade = "B"`
- Average 70–79 → `grade = "C"`

We will learn `if/else` statements in a future lesson to make this dynamic, but for now you can set it manually.

---

### Practice 2 — Swapping Prices (Multiple Assignment)

**Objective:** Use Python's one-line swap technique in a practical scenario.

**Scenario:** A market data analyst accidentally recorded two prices in the wrong variables. Fix it.

```python
# These values were entered in the wrong order
price_of_rice = 350
price_of_garri = 120

print("Before correction:")
print(f"Rice  : {price_of_rice} Naira")
print(f"Garri : {price_of_garri} Naira")

# Swap the values using Python's one-line swap
price_of_rice, price_of_garri = price_of_garri, price_of_rice

print("\nAfter correction:")
print(f"Rice  : {price_of_rice} Naira")
print(f"Garri : {price_of_garri} Naira")
```

**Expected Output:**
```
Before correction:
Rice  : 350 Naira
Garri : 120 Naira

After correction:
Rice  : 120 Naira
Garri : 350 Naira
```

---

### Practice 3 — Global Counter (Global Variables)

**Objective:** Use a global variable to count how many times a function has been called.

**Scenario:** A simple page view counter for a website.

```python
# Global variable — shared across all function calls
page_views = 0

def visit_page():
    global page_views
    page_views += 1    # Increase the counter by 1
    print(f"Page visited! Total views: {page_views}")

visit_page()
visit_page()
visit_page()
print(f"\nFinal page view count: {page_views}")
```

**Expected Output:**
```
Page visited! Total views: 1
Page visited! Total views: 2
Page visited! Total views: 3

Final page view count: 3
```

**Self-check:** What would happen to `page_views` after each `visit_page()` call if you removed the `global page_views` line?

---

## Mini Project — Personal Budget Tracker

Let us bring everything together into one realistic project.

### Project: Monthly Budget Calculator

**Goal:** Build a program that tracks monthly income, lists expenses with comments, calculates the total spending, and displays a budget summary.

**Stage 1 — Setup (Variables and Comments)**

```python
# ============================================
# MONTHLY BUDGET TRACKER
# Author : [Your Name]
# Date   : May 2026
# ============================================

# --- Income ---
monthly_income = 150000    # Salary in Naira

# --- Fixed Expenses ---
rent = 35000
electricity = 5000
internet = 8000
transport = 12000

# --- Variable Expenses ---
food = 25000
clothing = 10000
entertainment = 7000
miscellaneous = 5000
```

**Stage 2 — Calculations**

```python
# Calculate total expenses
total_expenses = (rent + electricity + internet + transport +
                  food + clothing + entertainment + miscellaneous)

# Calculate savings
savings = monthly_income - total_expenses

# Calculate savings percentage
savings_percentage = (savings / monthly_income) * 100
```

**Stage 3 — Display the Report**

```python
# Display the budget report
print("=" * 45)
print("       MONTHLY BUDGET SUMMARY")
print("=" * 45)
print(f"Monthly Income    : ₦{monthly_income:,}")
print("-" * 45)
print("  FIXED EXPENSES")
print(f"  Rent            : ₦{rent:,}")
print(f"  Electricity     : ₦{electricity:,}")
print(f"  Internet        : ₦{internet:,}")
print(f"  Transport       : ₦{transport:,}")
print("  VARIABLE EXPENSES")
print(f"  Food            : ₦{food:,}")
print(f"  Clothing        : ₦{clothing:,}")
print(f"  Entertainment   : ₦{entertainment:,}")
print(f"  Miscellaneous   : ₦{miscellaneous:,}")
print("-" * 45)
print(f"Total Expenses    : ₦{total_expenses:,}")
print(f"Monthly Savings   : ₦{savings:,}")
print(f"Savings Rate      : {savings_percentage:.1f}%")
print("=" * 45)
```

**Stage 4 — Milestone Output**

```
=============================================
       MONTHLY BUDGET SUMMARY
=============================================
Monthly Income    : ₦150,000
---------------------------------------------
  FIXED EXPENSES
  Rent            : ₦35,000
  Electricity     : ₦5,000
  Internet        : ₦8,000
  Transport       : ₦12,000
  VARIABLE EXPENSES
  Food            : ₦25,000
  Clothing        : ₦10,000
  Entertainment   : ₦7,000
  Miscellaneous   : ₦5,000
---------------------------------------------
Total Expenses    : ₦107,000
Monthly Savings   : ₦43,000
Savings Rate      : 28.7%
=============================================
```

**Reflection Questions:**
- Which variable represents your net financial position each month?
- What would you need to change to update just the food budget?
- How does using variables (instead of raw numbers) make this program easier to maintain?
- What would happen to the `savings` variable if `monthly_income` decreased by 20,000?

**Optional Advanced Extensions:**
1. Add an `annual_savings` variable that multiplies `savings` by 12.
2. Add a comment that flags whether the savings rate is healthy (financial experts recommend at least 20%).
3. Create a global variable called `currency_symbol` and use it throughout all the print statements.

---

## Common Beginner Mistakes

---

### Mistake 1 — Using a Variable Before Creating It

**Wrong:**
```python
print(city)    # Used before being created!
city = "Ibadan"
```

**Error:**
```
NameError: name 'city' is not defined
```

**Fix — always assign before using:**
```python
city = "Ibadan"
print(city)
```

---

### Mistake 2 — Using a Python Keyword as a Variable Name

**Wrong:**
```python
for = 10       # 'for' is a keyword!
type = "dog"   # 'type' is a built-in function — avoid using it!
```

**Error:**
```
SyntaxError: invalid syntax
```

**Fix — choose a descriptive alternative:**
```python
loop_count = 10
animal_type = "dog"
```

---

### Mistake 3 — Starting a Variable Name with a Number

**Wrong:**
```python
1st_place = "Gold"    # Starts with a number!
```

**Error:**
```
SyntaxError: invalid syntax
```

**Fix:**
```python
first_place = "Gold"
place_1 = "Gold"
```

---

### Mistake 4 — Using `+` to Concatenate a String and a Number

**Wrong:**
```python
score = 95
print("Your score is: " + score)
```

**Error:**
```
TypeError: can only concatenate str (not "int") to str
```

**Fix — use `str()` to convert, or use an f-string:**
```python
score = 95
print("Your score is: " + str(score))   # Option 1
print(f"Your score is: {score}")        # Option 2 (better)
```

---

### Mistake 5 — Forgetting `global` When Trying to Modify a Global Variable

**Wrong:**
```python
total = 0

def add_item():
    total = total + 1    # This creates a LOCAL 'total', doesn't modify global
    print(total)

add_item()
```

**Error:**
```
UnboundLocalError: local variable 'total' referenced before assignment
```

**Fix:**
```python
total = 0

def add_item():
    global total
    total = total + 1
    print(total)

add_item()
```

---

### Mistake 6 — Mismatched Variable Count in Multi-Assignment

**Wrong:**
```python
x, y = 1, 2, 3    # 2 variables but 3 values
```

**Error:**
```
ValueError: too many values to unpack (expected 2)
```

**Fix — make the counts match:**
```python
x, y, z = 1, 2, 3
```

---

### Mistake 7 — Inconsistent Capitalisation

**Wrong (hard-to-catch bug):**
```python
studentName = "Kemi"
print(StudentName)    # Capital S — different variable!
```

**Error:**
```
NameError: name 'StudentName' is not defined
```

**Fix — be consistent:**
```python
student_name = "Kemi"
print(student_name)
```

---

## Reflection Questions

1. What is a comment in Python? Give two reasons why comments are important.
2. What symbol do you use to write a single-line comment?
3. Can a comment appear at the end of a line of code? Show an example.
4. What is a variable? Describe it using a real-world analogy.
5. What does the `=` symbol do in Python? Is it the same as "equals" in mathematics?
6. Why is Python called a "dynamically typed" language?
7. Write three valid variable names and three invalid variable names, and explain why each is valid or invalid.
8. What is the difference between `name`, `Name`, and `NAME` in Python?
9. What does "snake_case" mean? Give two examples.
10. Show two ways to assign the value `0` to variables `a`, `b`, and `c` on a single line.
11. What is the difference between a local variable and a global variable?
12. Why do we need the `global` keyword? What problem does it solve?
13. What is an f-string? How does it improve on concatenation with `+`?
14. What error do you get if you try to use `+` to join a string and an integer?
15. What is a constant, and how is it named by convention in Python?

---

## Completion Checklist

Tick each item when you can do it comfortably without looking at your notes.

- [ ] I can write a single-line comment using `#`.
- [ ] I can write an inline comment on the same line as code.
- [ ] I can write multi-line comments using multiple `#` lines.
- [ ] I understand what triple-quoted strings are and when to use them.
- [ ] I can create a variable and assign a value to it.
- [ ] I understand that Python uses dynamic typing (no need to declare the type).
- [ ] I can reassign a new value to an existing variable.
- [ ] I know the four rules for valid variable names.
- [ ] I know the conventions (snake_case, ALL_CAPS for constants, descriptive names).
- [ ] I can tell valid variable names from invalid ones.
- [ ] I can assign multiple values to multiple variables on one line.
- [ ] I can assign the same value to multiple variables on one line.
- [ ] I can unpack a list into individual variables.
- [ ] I can swap two variables using Python's one-line swap.
- [ ] I can print variables using commas, concatenation, and f-strings.
- [ ] I know when to use `str()` and why.
- [ ] I can explain the difference between local and global variables.
- [ ] I can use the `global` keyword correctly inside a function.
- [ ] I can identify and fix all 7 common beginner mistakes from this lesson.
- [ ] I have completed all the guided practice exercises.
- [ ] I have built and run the Monthly Budget Tracker mini project.

---

## Lesson Summary

Here is everything you learned in Lesson 04, summarised clearly.

**Comments:**

| Type | Syntax | Use Case |
|------|--------|----------|
| Single-line | `# This is a comment` | Short notes on any line |
| Inline | `code  # comment` | Explaining a specific line |
| Multi-line | Multiple `#` lines | Longer explanations |
| Triple-quoted string | `"""..."""` | Often used for docstrings |

**Variables:**
- A variable is a named container that stores a value.
- Created with `=` (the assignment operator): `name = "Kemi"`
- Python automatically detects the type (dynamic typing).
- Variables are case-sensitive: `age ≠ Age ≠ AGE`.
- Values can be changed (reassigned) at any time.

**Naming rules (MUST follow):**
- Must start with a letter or `_`
- Can only contain letters, numbers, `_`
- Cannot be a Python keyword
- Case-sensitive

**Naming conventions (SHOULD follow):**
- Use `snake_case` for variable names
- Use `ALL_CAPS` for constants
- Use descriptive, meaningful names

**Multiple Assignment:**

```python
x, y, z = 1, 2, 3          # Different values to different variables
x = y = z = 0               # Same value to all variables
a, b = b, a                 # Swap two variables in one line
x, y, z = ["a", "b", "c"]  # Unpack a list
```

**Output Methods (best to least preferred):**

```python
print(f"Name: {name}, Age: {age}")         # f-string ⭐ best
print("Name:", name, "Age:", age)           # comma-separated
print("Name: " + name + ", Age: " + str(age))  # concatenation
```

**Global Variables:**
- Defined outside all functions — accessible everywhere.
- To *modify* a global variable from inside a function, use the `global` keyword.
- Use sparingly — prefer passing values as function arguments.

```python
count = 0

def increment():
    global count
    count += 1
```

---

> **What comes next?** In Lesson 05 we will explore **Python Data Types** — the different kinds of values Python works with, including integers, floats, strings, and booleans. Understanding data types is the key to understanding how Python does calculations, makes decisions, and handles information.

---

*Sources: W3Schools Python Tutorial — [python_comments.asp](https://www.w3schools.com/python/python_comments.asp), [python_variables.asp](https://www.w3schools.com/python/python_variables.asp), [python_variables_names.asp](https://www.w3schools.com/python/python_variables_names.asp), [python_variables_multiple.asp](https://www.w3schools.com/python/python_variables_multiple.asp), [python_variables_output.asp](https://www.w3schools.com/python/python_variables_output.asp), [python_variables_global.asp](https://www.w3schools.com/python/python_variables_global.asp), [python_variables_exercises.asp](https://www.w3schools.com/python/python_variables_exercises.asp)*
