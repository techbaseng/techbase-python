---
render_with_liquid: false
title: "Lesson 19: Python None, User Input, Virtual Environments, and Arrays"
nav_order: 19
---

# Lesson 19: Python `None`, User Input, Virtual Environments, and Arrays

---

## Lesson Introduction

Welcome to Lesson 19! This lesson covers four important and very practical Python topics that every developer uses regularly:

1. **`None`** — Python's special value for "nothing" or "no value yet"
2. **User Input** — How to ask the person running your program to type something
3. **Virtual Environments** — How to keep your Python projects clean and organised
4. **Arrays** — How to store and work with multiple values in one place

These four topics naturally connect. In a real program, you often collect input from users, store the input in an array, check if values are `None` (missing or not yet set), and run the whole thing inside a safe virtual environment so your project doesn't break other projects on your computer.

By the end of this lesson you will have built a small but real interactive student grade tracker that uses all four concepts together.

---

## Prerequisites

Before starting, you should already understand:

- Python variables (storing values in named boxes)
- Python data types: strings (`"hello"`), integers (`42`), floats (`3.14`), booleans (`True`/`False`)
- Python `if`/`else` statements
- Python `for` loops
- Python functions (defining with `def` and calling them)
- Python `try`/`except` for handling errors

If any of these feel unfamiliar, review them before continuing — this lesson builds on them directly.

---

## Part 1 — Python `None`

### What Is `None`?

Imagine you have a form and one field is left blank. The field exists, but it has no value. In Python, we use the special keyword `None` to represent exactly that: **the absence of a value**.

`None` is not zero. It is not an empty string `""`. It is not `False`. It is its own unique thing that means "there is nothing here."

Think of it like this:

| Value | Meaning |
|-------|---------|
| `0` | The number zero — a value that happens to be zero |
| `""` | An empty string — a text value with no characters |
| `False` | A boolean that is false |
| `None` | There is no value at all — the slot is empty |

### The Data Type of `None`

Every value in Python has a data type. The type of `None` is called `NoneType`. There is only ever one `None` object in Python — it is a unique constant, not a number or string.

```python
x = None
print(x)
print(type(x))
```

**Expected Output:**
```
None
<class 'NoneType'>
```

Line-by-line explanation:
- `x = None` — we assign the value `None` to the variable `x`. The variable now holds "nothing".
- `print(x)` — prints the word `None` to the screen.
- `print(type(x))` — asks Python "what type is x?" and prints `<class 'NoneType'>`.

### Why Does `None` Exist? What Problem Does It Solve?

Without `None`, how would you say "this variable has been created but hasn't received a real value yet"?

**Real-world example:** A student registration system. When a student signs up, their final grade isn't known yet. You need a placeholder:

```python
student_name = "Ama"
final_grade = None   # grade not assigned yet

print(student_name)
print(final_grade)
```

**Expected Output:**
```
Ama
None
```

Later, when the grade is available, you update it:

```python
final_grade = 87.5
print(final_grade)
```

**Expected Output:**
```
87.5
```

### Comparing Values to `None` — Use `is`, Not `==`

This is very important! When you want to check if something is `None`, always use the **identity operator** `is` or `is not`. Do **not** use `==`.

**Why?** Because `is` checks if two things are literally the same object in memory. `None` is a singleton (there is only one of it), so `is` is the correct and most reliable way to test for it.

```python
result = None

if result is None:
    print("No result yet")
else:
    print("Result is ready")
```

**Expected Output:**
```
No result yet
```

Now with `is not`:

```python
result = None

if result is not None:
    print("Result is ready")
else:
    print("No result yet")
```

**Expected Output:**
```
No result yet
```

> **Thinking prompt:** What happens if you set `result = 0` instead of `result = None`? Try it! Does the output change? Why?

### `None` in a Boolean Context

In Python, values can be "truthy" (act like `True`) or "falsy" (act like `False`) even when they aren't booleans. `None` is falsy — it evaluates to `False`:

```python
print(bool(None))
```

**Expected Output:**
```
False
```

This is useful in if-statements:

```python
score = None

if not score:
    print("Score has not been entered yet.")
```

**Expected Output:**
```
Score has not been entered yet.
```

> **Be careful!** `0` and `""` are also falsy. If you specifically need to distinguish `None` from `0`, use `is None` instead of just `if not score`.

### Functions That Return `None`

Here is something that surprises many beginners: if you write a function in Python and forget to add a `return` statement, Python automatically returns `None`.

```python
def greet():
    message = "Hello!"   # sets a variable but never returns it

result = greet()
print(result)
```

**Expected Output:**
```
None
```

The function ran, set `message = "Hello!"`, but since we never said `return message`, Python returned `None` by default.

**Corrected version:**

```python
def greet():
    message = "Hello!"
    return message       # now we return the value

result = greet()
print(result)
```

**Expected Output:**
```
Hello!
```

### Second Example: Using `None` as a Sentinel Value

A "sentinel value" is a placeholder that signals "not set yet". Here is a practical pattern you will see in real code:

```python
winner = None

scores = {"Alice": 95, "Bob": 88, "Carol": 91}

for name, score in scores.items():
    if winner is None or score > scores[winner]:
        winner = name

print(f"The winner is: {winner}")
```

**Expected Output:**
```
The winner is: Alice
```

Line-by-line:
- `winner = None` — start with no winner decided.
- We loop through each name and score.
- `if winner is None` — on the first loop, there is no winner yet, so we immediately set `winner = name`.
- `or score > scores[winner]` — on later loops, only update if we found a higher score.
- By the end, `winner` holds the name with the highest score.

---

## Part 2 — Python User Input

### What Is User Input?

So far, all the values in your programs have been hardcoded — you wrote them directly in the code. But real programs are interactive. A calculator should let you type numbers. A registration form should let you type your name. A quiz should let you type your answer.

**User input** is how your program pauses and waits for the person running it to type something.

### The `input()` Function

Python provides the built-in `input()` function for this purpose. When Python reaches `input()`, it:
1. Shows a prompt (optional message) to the user
2. Waits — the program pauses completely
3. Resumes when the user types something and presses Enter
4. Returns whatever the user typed as a **string**

```python
print("Enter your name:")
name = input()
print(f"Hello {name}")
```

**What happens when you run this:**
```
Enter your name:
> Ama        ← user types this and presses Enter
Hello Ama
```

Line-by-line:
- `print("Enter your name:")` — displays the prompt message.
- `name = input()` — pauses the program, waits for typing, then stores the typed text in `name`.
- `print(f"Hello {name}")` — uses an f-string to greet the user by name.

### Using the Prompt Parameter (Cleaner Way)

Instead of printing a message then calling `input()` separately, you can pass the prompt message directly into `input()`. This shows the message and the input cursor on the same line — much cleaner:

```python
name = input("Enter your name: ")
print(f"Hello {name}")
```

**What happens:**
```
Enter your name: Ama
Hello Ama
```

The text `"Enter your name: "` appears, then the cursor waits right after it on the same line.

> **Tip:** Notice the space before the closing quote: `"Enter your name: "`. Without it, the cursor would be right against the colon with no space.

### Multiple Inputs

You can call `input()` as many times as you need. Python will stop and wait at each one:

```python
name = input("Enter your name: ")
print(f"Hello {name}")
fav_animal = input("What is your favourite animal: ")
fav_colour = input("What is your favourite colour: ")
fav_number = input("What is your favourite number: ")
print(f"Do you want a {fav_colour} {fav_animal} with {fav_number} legs?")
```

**Sample Run:**
```
Enter your name: Kwame
Hello Kwame
What is your favourite animal: elephant
What is your favourite colour: blue
What is your favourite number: 4
Do you want a blue elephant with 4 legs?
```

### The Important Rule: Input Is Always a String!

This is the #1 beginner mistake with `input()`. **Whatever the user types, Python stores it as a string — even if it looks like a number.**

```python
x = input("Enter a number: ")
print(type(x))
```

**Output (even if the user types 42):**
```
Enter a number: 42
<class 'str'>
```

Python received `"42"` (a string), not `42` (an integer). If you try to do maths with it:

```python
x = input("Enter a number: ")
result = x + 10   # This will CRASH!
```

**Error:**
```
TypeError: can only concatenate str (not "int") to str
```

**Solution: Convert the input to the right type!**

Use `int()` to convert to a whole number, or `float()` to convert to a decimal number:

```python
x = input("Enter a number: ")
x = int(x)          # now x is an integer
result = x + 10
print(result)
```

**Sample Run:**
```
Enter a number: 5
15
```

Or for decimals (like grades or prices):

```python
import math

x = input("Enter a number: ")
y = math.sqrt(float(x))    # convert to float first, then find square root
print(f"The square root of {x} is {y}")
```

**Sample Run:**
```
Enter a number: 16
The square root of 16 is 4.0
```

Line-by-line:
- `import math` — loads Python's math library so we can use `math.sqrt()`.
- `x = input(...)` — gets the user's text.
- `float(x)` — converts the text `"16"` into the decimal number `16.0`.
- `math.sqrt(16.0)` — calculates the square root, which is `4.0`.
- `f"..."` — formats the output string.

### Validating Input (Handling Bad Input)

What if the user types `"hello"` when you need a number? `int("hello")` will crash with a `ValueError`. A good program should catch this and ask again.

We use a `while` loop combined with `try`/`except` to keep asking until valid input is received:

```python
valid = True

while valid:
    x = input("Enter a number: ")
    try:
        x = float(x)
        valid = False       # input was valid — stop the loop
    except:
        print("That was not a number. Please try again.")

print(f"You entered: {x}")
print("Thank you!")
```

**Sample Run:**
```
Enter a number: hello
That was not a number. Please try again.
Enter a number: abc
That was not a number. Please try again.
Enter a number: 7.5
You entered: 7.5
Thank you!
```

Line-by-line:
- `valid = True` — start the loop as "still waiting".
- `while valid:` — keep looping as long as we haven't got a valid number.
- `x = float(x)` — try to convert. If it fails, Python jumps to `except`.
- `valid = False` — conversion succeeded, so we can stop the loop.
- `except:` — if conversion failed (bad input), print an error and the loop repeats.

> **Real-world use:** Every well-built application validates input. A banking app checks that you entered a valid account number. A form checks that an email address contains `@`. This pattern is the foundation of that.

---

## Part 3 — Python Virtual Environments

### What Is a Virtual Environment?

Imagine you are a chef who works at two different restaurants. Restaurant A needs you to use only salt and pepper — no chilli. Restaurant B wants you to use lots of spices. If you mixed all your spices together in one bag, things would get confusing and messy.

A **virtual environment** is like having a separate spice bag for each restaurant. It is an isolated Python workspace for a specific project. Each virtual environment:

- Has its own Python interpreter
- Has its own set of installed packages (libraries)
- Is completely separate from other virtual environments
- Can have different versions of the same package

### Why Do You Need Virtual Environments?

Without virtual environments, all your Python projects share the same packages globally. This causes real problems:

- **Version conflicts:** Project A needs `pandas` version 1.0, but Project B needs version 2.0. You can only have one installed globally — so one project will break.
- **Messy global environment:** Installing packages for experiments permanently changes your system Python.
- **Collaboration problems:** Your colleague's computer may have different package versions, so code that works on your machine breaks on theirs.

Virtual environments solve all of these problems by giving each project its own private, self-contained world.

### Creating a Virtual Environment

Python comes with a built-in tool called `venv` for this. You run it from your terminal (command prompt).

First, open your terminal and go to the folder where you want your project:

```bash
# On Windows:
cd C:\Users\YourName\Documents\MyProjects

# On Mac/Linux:
cd ~/Documents/MyProjects
```

Then create the virtual environment:

```bash
# Windows:
python -m venv myfirstproject

# Mac/Linux:
python3 -m venv myfirstproject
```

**What this command does:**
- `python -m venv` — runs Python's built-in virtual environment module.
- `myfirstproject` — the name you give to this virtual environment (and the folder it creates).

**Result — a new folder is created with this structure:**

```
myfirstproject/
    Include/
    Lib/
    Scripts/       ← contains the activation script
    .gitignore
    pyvenv.cfg     ← configuration file
```

> **Tip:** The folder name (`myfirstproject`) can be anything. Many developers use `.venv` as the name so it stays hidden and is easy to find.

### Activating the Virtual Environment

Creating the folder is not enough. You must **activate** it. Activating tells your terminal "from now on, use Python and packages from this virtual environment, not the global one".

```bash
# Windows:
myfirstproject\Scripts\activate

# Mac/Linux:
source myfirstproject/bin/activate
```

**After activation, your prompt changes to show you are inside the environment:**

```
# Windows:
(myfirstproject) C:\Users\YourName>

# Mac/Linux:
(myfirstproject) user@computer:~$
```

The `(myfirstproject)` prefix tells you the virtual environment is active. Any Python packages you install now go into this environment only.

### Installing Packages Inside the Virtual Environment

With the environment active, use `pip` to install packages. Let us install a fun example package called `cowsay`:

```bash
(myfirstproject) pip install cowsay
```

**Output:**
```
Collecting cowsay
  Downloading cowsay-6.1-py3-none-any.whl (25 kB)
Installing collected packages: cowsay
Successfully installed cowsay-6.1
```

`cowsay` is now installed **only inside `myfirstproject`**. No other project or your global Python is affected.

### Using the Package

Create a file called `test.py` and write:

```python
import cowsay

cowsay.cow("Good Mooooorning!")
```

Run it while your virtual environment is active:

```bash
(myfirstproject) python test.py
```

**Output:**
```
  _________________
| Good Mooooorning! |
  =================
                 \
                  \
                    ^__^
                    (oo)\_______
                    (__)\       )\/\
                        ||----w |
                        ||     ||
```

### Deactivating the Virtual Environment

When you are done working on this project, deactivate the environment to return to your normal terminal:

```bash
(myfirstproject) deactivate
```

Your prompt returns to normal:

```
C:\Users\YourName>
```

If you now try to run `test.py` outside the virtual environment:

```bash
python test.py
```

**You get an error:**
```
Traceback (most recent call last):
  File "test.py", line 1, in <module>
    import cowsay
ModuleNotFoundError: No module named 'cowsay'
```

This proves isolation is working! `cowsay` only exists inside `myfirstproject`. Your global Python doesn't know about it.

> **The virtual environment still exists** — it is just not active. Activate it again any time with the `activate` command.

### Deleting a Virtual Environment

Since a virtual environment is just a folder, deleting it is simple:

```bash
# Windows:
rmdir /s /q myfirstproject

# Mac/Linux:
rm -rf myfirstproject
```

No other project is affected because the virtual environment was isolated.

### Professional Best Practice: `requirements.txt`

In real projects, developers save a list of all their project's packages so teammates can recreate the same environment. This file is called `requirements.txt`:

```bash
# Save your package list:
pip freeze > requirements.txt

# Someone else recreates the environment:
pip install -r requirements.txt
```

This is how open-source projects and professional teams share working environments.

---

## Part 4 — Python Arrays

### What Is an Array?

An **array** is a data structure that holds multiple values under one single name. Instead of creating dozens of separate variables, you group related values together.

**Without an array — messy and unscalable:**

```python
car1 = "Ford"
car2 = "Volvo"
car3 = "BMW"
```

What if you had 300 cars? You'd need 300 variables! And you couldn't loop through them easily.

**With an array — clean and scalable:**

```python
cars = ["Ford", "Volvo", "BMW"]
```

Now all three cars live in one named group. You can loop through them, find a specific one, add more, remove some — all with just one variable name.

### Arrays in Python: The Important Note

Python does not have a separate "array" data type built in. Instead, **Python uses Lists as arrays**. A Python list behaves exactly like an array for most purposes.

> For advanced scientific computing (like NumPy arrays), you would import a special library. But for everyday programming, lists are your arrays.

```python
# This IS an array in Python (using a list):
cars = ["Ford", "Volvo", "BMW"]
print(cars)
```

**Expected Output:**
```
['Ford', 'Volvo', 'BMW']
```

### Accessing Elements — Index Numbers

Every item in an array has a numbered position called an **index**. Python starts counting from **0**, not 1. This is called zero-based indexing.

```
cars = ["Ford", "Volvo", "BMW"]
         ↑        ↑       ↑
       index 0  index 1  index 2
```

To access an element, write the array name followed by the index in square brackets:

```python
cars = ["Ford", "Volvo", "BMW"]

print(cars[0])    # first item
print(cars[1])    # second item
print(cars[2])    # third item
```

**Expected Output:**
```
Ford
Volvo
BMW
```

> **Thinking prompt:** What happens if you write `cars[3]`? There is no index 3 (only 0, 1, 2). Try it and see the error message!

### Modifying Elements

You can change an item by assigning a new value to its index:

```python
cars = ["Ford", "Volvo", "BMW"]
print(cars[0])    # Ford

cars[0] = "Toyota"
print(cars[0])    # Toyota
```

**Expected Output:**
```
Ford
Toyota
```

### Finding the Length

The `len()` function tells you how many items are in an array:

```python
cars = ["Ford", "Volvo", "BMW"]
x = len(cars)
print(x)
```

**Expected Output:**
```
3
```

> **Important note:** The length is always one more than the highest index. Length is 3, but the highest index is 2 (because we start at 0).

### Looping Through an Array

One of the biggest benefits of arrays is being able to process all items with a loop:

```python
cars = ["Ford", "Volvo", "BMW"]

for x in cars:
    print(x)
```

**Expected Output:**
```
Ford
Volvo
BMW
```

Line-by-line:
- `for x in cars:` — go through each item in `cars`, one at a time.
- On each loop, `x` holds the current item.
- `print(x)` — print that item.

**Practical use — printing a personalised list:**

```python
fruits = ["mango", "pineapple", "pawpaw", "guava"]

print("Today's available fruits:")
for fruit in fruits:
    print(f"  - {fruit}")
```

**Expected Output:**
```
Today's available fruits:
  - mango
  - pineapple
  - pawpaw
  - guava
```

### Adding Elements — `append()`

Use the `append()` method to add a new item to the end of the array:

```python
cars = ["Ford", "Volvo", "BMW"]
cars.append("Honda")
print(cars)
```

**Expected Output:**
```
['Ford', 'Volvo', 'BMW', 'Honda']
```

`append()` always adds to the **end** of the list.

### Removing Elements — `pop()` and `remove()`

**`pop(index)`** — removes the item at a specific index position:

```python
cars = ["Ford", "Volvo", "BMW"]
cars.pop(1)     # removes index 1, which is "Volvo"
print(cars)
```

**Expected Output:**
```
['Ford', 'BMW']
```

**`remove(value)`** — removes the first item that matches a specific value:

```python
cars = ["Ford", "Volvo", "BMW"]
cars.remove("Volvo")
print(cars)
```

**Expected Output:**
```
['Ford', 'BMW']
```

> **Note:** `remove()` only deletes the **first** matching item. If `"Volvo"` appeared twice, only the first one would be deleted.

### Full Reference of Array (List) Methods

| Method | What It Does | Example |
|--------|-------------|---------|
| `append(x)` | Adds `x` to the end | `cars.append("Honda")` |
| `clear()` | Removes all items | `cars.clear()` |
| `copy()` | Returns a copy of the list | `cars2 = cars.copy()` |
| `count(x)` | Counts how many times `x` appears | `cars.count("Ford")` |
| `extend(list2)` | Adds all items from another list | `cars.extend(["Kia", "Audi"])` |
| `index(x)` | Returns the index of the first `x` | `cars.index("BMW")` |
| `insert(i, x)` | Inserts `x` at position `i` | `cars.insert(1, "Audi")` |
| `pop(i)` | Removes item at index `i` | `cars.pop(0)` |
| `remove(x)` | Removes first occurrence of `x` | `cars.remove("Ford")` |
| `reverse()` | Reverses the order | `cars.reverse()` |
| `sort()` | Sorts the list | `cars.sort()` |

### Second Array Example: Storing Numbers and Calculating Average

Arrays work for numbers too. Here is a practical example:

```python
scores = [78, 92, 85, 67, 90]

total = 0
for score in scores:
    total = total + score

average = total / len(scores)
print(f"Total: {total}")
print(f"Number of scores: {len(scores)}")
print(f"Average: {average}")
```

**Expected Output:**
```
Total: 412
Number of scores: 5
Average: 82.4
```

> **Thinking prompt:** What happens if `scores` is an empty list `[]`? You'd be dividing by zero! How would you guard against that?

---

## Guided Practice Exercises

### Exercise 1: `None` Checker

**Objective:** Practice using `None` to represent missing data.

**Scenario:** A hospital patient registration system. A patient may not have a doctor assigned yet.

**Steps:**

1. Create variables for patient name and assigned doctor.
2. Set the doctor to `None` initially.
3. Check if the doctor is `None` and print an appropriate message.
4. Assign a doctor and check again.

**Your code:**

```python
patient_name = "Fatima"
assigned_doctor = None

if assigned_doctor is None:
    print(f"{patient_name} does not have a doctor assigned yet.")
else:
    print(f"{patient_name}'s doctor is {assigned_doctor}.")

# Now assign a doctor
assigned_doctor = "Dr. Mensah"

if assigned_doctor is None:
    print(f"{patient_name} does not have a doctor assigned yet.")
else:
    print(f"{patient_name}'s doctor is {assigned_doctor}.")
```

**Expected Output:**
```
Fatima does not have a doctor assigned yet.
Fatima's doctor is Dr. Mensah.
```

**Self-check:** Did you use `is None` and not `== None`?

---

### Exercise 2: Validated User Input

**Objective:** Practice collecting and validating user input.

**Scenario:** A simple quiz that asks the user to enter their age and confirms it is a valid number.

**Steps:**

1. Ask the user for their age.
2. Try to convert it to an integer.
3. If they type something that isn't a number, tell them and ask again.
4. Once valid, print their age and whether they are an adult (18 or older).

**Your code:**

```python
got_valid_input = True

while got_valid_input:
    age_text = input("Please enter your age: ")
    try:
        age = int(age_text)
        got_valid_input = False
    except:
        print("That is not a valid age. Please enter a whole number.")

if age >= 18:
    print(f"You are {age} years old. You are an adult.")
else:
    print(f"You are {age} years old. You are not yet an adult.")
```

**Sample Run:**
```
Please enter your age: twenty
That is not a valid age. Please enter a whole number.
Please enter your age: 16
You are 16 years old. You are not yet an adult.
```

**What-if challenge:** What if someone enters a negative age like `-5`? Add an extra check inside the `try` block to reject negative ages.

---

### Exercise 3: Building an Array from User Input

**Objective:** Combine user input and arrays.

**Scenario:** Collect the names of five students into an array, then display them.

**Steps:**

1. Create an empty array.
2. Use a loop to ask for 5 student names.
3. Append each name to the array.
4. Print all names from the array using another loop.

**Your code:**

```python
students = []

print("Enter the names of 5 students:")
for i in range(5):
    name = input(f"Student {i + 1}: ")
    students.append(name)

print("\nClass list:")
for student in students:
    print(f"  - {student}")

print(f"\nTotal students: {len(students)}")
```

**Sample Run:**
```
Enter the names of 5 students:
Student 1: Ama
Student 2: Kweku
Student 3: Fatima
Student 4: Chidi
Student 5: Zara

Class list:
  - Ama
  - Kweku
  - Fatima
  - Chidi
  - Zara

Total students: 5
```

---

## Mini Project: Interactive Student Grade Tracker

Now let us combine **all four concepts** — `None`, user input, and arrays — into a complete, useful program. (You would run this inside a virtual environment in real life!)

### Project Goal

Build a program that:
1. Asks the user how many students there are
2. Collects each student's name and grade (with validation)
3. Stores them in arrays
4. Calculates and displays the class average, highest grade, and lowest grade
5. Marks any student with `None` as their grade if their grade is missing

---

### Stage 1: Setup and Data Collection

```python
# Stage 1: Collect student data

students = []
grades = []

# Get the number of students
while True:
    count_text = input("How many students are in the class? ")
    try:
        count = int(count_text)
        if count > 0:
            break
        else:
            print("Please enter a positive number.")
    except:
        print("Please enter a whole number.")

print(f"\nEntering data for {count} students.\n")

for i in range(count):
    name = input(f"Enter name of student {i + 1}: ")
    students.append(name)

    while True:
        grade_text = input(f"Enter grade for {name} (or press Enter to skip): ")
        if grade_text == "":
            grades.append(None)   # No grade entered — use None
            print(f"  Grade for {name} set to: Not yet recorded")
            break
        try:
            grade = float(grade_text)
            if 0 <= grade <= 100:
                grades.append(grade)
                break
            else:
                print("Grade must be between 0 and 100.")
        except:
            print("Please enter a number or press Enter to skip.")
    print()
```

**Sample input/output for Stage 1:**
```
How many students are in the class? 3

Entering data for 3 students.

Enter name of student 1: Ama
Enter grade for Ama (or press Enter to skip): 88

Enter name of student 2: Kweku
Enter grade for Kweku (or press Enter to skip): 
  Grade for Kweku set to: Not yet recorded

Enter name of student 3: Fatima
Enter grade for Fatima (or press Enter to skip): 95
```

---

### Stage 2: Display Results

```python
# Stage 2: Display the class results

print("=" * 40)
print("        STUDENT GRADE REPORT")
print("=" * 40)

recorded_grades = []   # Only grades that are not None

for i in range(len(students)):
    name = students[i]
    grade = grades[i]

    if grade is None:
        print(f"{name}: Not yet recorded")
    else:
        print(f"{name}: {grade}")
        recorded_grades.append(grade)

print("-" * 40)

# Milestone output after Stage 2
if len(recorded_grades) == 0:
    print("No grades recorded yet.")
else:
    average = sum(recorded_grades) / len(recorded_grades)
    highest = max(recorded_grades)
    lowest = min(recorded_grades)

    print(f"Students with grades: {len(recorded_grades)}")
    print(f"Class average: {average:.1f}")
    print(f"Highest grade: {highest}")
    print(f"Lowest grade:  {lowest}")

print("=" * 40)
```

**Expected Output for Stage 2 (using sample data above):**
```
========================================
        STUDENT GRADE REPORT
========================================
Ama: 88.0
Kweku: Not yet recorded
Fatima: 95.0
----------------------------------------
Students with grades: 2
Class average: 91.5
Highest grade: 95.0
Lowest grade:  88.0
========================================
```

---

### Stage 3: Enhancements — Find the Top Student

```python
# Stage 3: Find the top student

if len(recorded_grades) > 0:
    top_grade = max(recorded_grades)
    top_index = grades.index(top_grade)
    top_student = students[top_index]
    print(f"\nTop student: {top_student} with {top_grade}")
```

**Expected Output:**
```
Top student: Fatima with 95.0
```

---

### Reflection Questions

1. Why did we use `None` instead of `0` for missing grades? What problem would `0` cause?
2. What happens if all grades are `None`? Does the program handle it correctly?
3. How would you add a feature to update a missing grade later?
4. Why would you run this program inside a virtual environment?

**Optional Extension:** Add a feature that shows all students who scored below average and suggests they need extra help.

---

## Common Beginner Mistakes

### Mistake 1: Using `== None` instead of `is None`

```python
# WRONG:
if x == None:
    print("No value")

# CORRECT:
if x is None:
    print("No value")
```

While `== None` often works, `is None` is the correct and Pythonic way. Some custom objects can override the `==` operator and give wrong results with `None`.

---

### Mistake 2: Forgetting that `input()` always returns a string

```python
# WRONG — crashes with TypeError:
age = input("Enter your age: ")
if age > 18:
    print("Adult")

# CORRECT:
age = int(input("Enter your age: "))
if age > 18:
    print("Adult")
```

Always convert input to the right type before using it in calculations or comparisons.

---

### Mistake 3: Forgetting to return a value from a function

```python
# WRONG — returns None accidentally:
def add(a, b):
    result = a + b
    # forgot to return!

total = add(5, 3)
print(total)    # prints: None

# CORRECT:
def add(a, b):
    result = a + b
    return result

total = add(5, 3)
print(total)    # prints: 8
```

---

### Mistake 4: Accessing an array index that doesn't exist

```python
cars = ["Ford", "Volvo", "BMW"]

# WRONG — IndexError! There is no index 3:
print(cars[3])

# CORRECT — highest valid index is len(cars) - 1:
print(cars[len(cars) - 1])   # last item
print(cars[-1])               # Python shortcut for last item
```

---

### Mistake 5: Confusing `pop(index)` with `remove(value)`

```python
cars = ["Ford", "Volvo", "BMW"]

# pop() takes an INDEX (position number):
cars.pop(1)           # removes "Volvo" (index 1)

# remove() takes a VALUE:
cars.remove("Ford")   # removes "Ford" (the value)

# MISTAKE — mixing them up:
cars.remove(0)        # Error! 0 is not a value in this list
cars.pop("BMW")       # Error! "BMW" is not an index number
```

---

### Mistake 6: Running `python` globally when you meant to use the virtual environment

Always check that your virtual environment is active before installing packages or running code. The `(envname)` prefix in your terminal prompt confirms it is active.

```bash
# Not active — packages install globally:
pip install requests

# Active (correct way):
(myfirstproject) pip install requests
```

---

## Reflection Questions

Answer these to check your understanding:

1. What is the difference between `None`, `0`, `""`, and `False` in Python?
2. Why should you use `is None` instead of `== None`?
3. What data type does `input()` always return, no matter what the user types?
4. If a function has no `return` statement, what does it return?
5. What is a virtual environment and why is it important for professional projects?
6. How do you activate a virtual environment on Windows? On Mac/Linux?
7. What is the index of the first element in a Python array/list?
8. What is the difference between `append()`, `insert()`, `pop()`, and `remove()`?
9. Why is `len(my_list) - 1` the index of the last item?
10. How would you store 100 student names without creating 100 separate variables?

---

## Completion Checklist

Before moving to the next lesson, confirm you can do each of the following:

- [ ] Assign `None` to a variable and check if it is `None` using `is`
- [ ] Explain the difference between `None`, `0`, `""`, and `False`
- [ ] Understand why a function with no `return` statement returns `None`
- [ ] Use `input()` to collect text from a user
- [ ] Use the prompt parameter in `input()` to show a message on the same line
- [ ] Convert user input from a string to an integer or float
- [ ] Use a `while` loop with `try`/`except` to validate user input
- [ ] Create a virtual environment with `python -m venv name`
- [ ] Activate and deactivate a virtual environment
- [ ] Install a package with `pip install` inside a virtual environment
- [ ] Understand why packages installed in a virtual environment don't affect other projects
- [ ] Create a Python array (list) with values
- [ ] Access elements by index number (remembering it starts at 0)
- [ ] Use `len()` to find the number of elements
- [ ] Loop through all array elements with a `for` loop
- [ ] Add elements with `append()` and remove with `pop()` or `remove()`
- [ ] Complete the Student Grade Tracker mini-project

---

## Lesson Summary

In this lesson you learned four important and interconnected Python concepts:

**`None`** is Python's special constant for "no value". Its type is `NoneType`. Use `is None` and `is not None` to test for it. Functions without a `return` statement automatically return `None`. It is useful as a placeholder or sentinel value.

**User Input** is captured with the `input()` function. It always returns a string, so always convert to `int()` or `float()` when you need a number. Use `while` + `try`/`except` loops to validate input and keep asking until you get a good response.

**Virtual Environments** are isolated Python workspaces. Create one with `python -m venv name`, activate it with the `activate` command, and install packages with `pip` inside it. Each project gets its own packages, preventing conflicts. Delete the folder when you no longer need the environment.

**Arrays (Lists)** store multiple values under one name. Access them with index numbers starting at `0`. Loop through them with `for`. Add items with `append()`, remove with `pop(index)` or `remove(value)`. Use `len()` for the count.

Together, these tools let you build interactive programs that collect real data, store it efficiently, handle missing values gracefully, and run cleanly in a professional development environment.
