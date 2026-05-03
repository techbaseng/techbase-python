---
render_with_liquid: false
title: "Python Syntax and Statements"
nav_order: 2
---

# Lesson 02 — Python Syntax and Statements

---

## Lesson Introduction

Welcome to Lesson 02! In Lesson 01 you installed Python and ran your very first program. Now it is time to go deeper and understand the **rules** that Python uses to read and run your code.

Every programming language has a **syntax** — a set of rules that tells the computer how to understand what you write. If you break those rules, the computer cannot understand you and will give you an error. Think of it like grammar in a spoken language: if you say "Cat the sat mat on the", no one understands you. But if you say "The cat sat on the mat", everyone does. Python is the same.

In this lesson you will learn:

- What Python syntax is and how it works
- Why **indentation** (spaces at the start of a line) is a critical rule in Python
- How to create and use **variables** to store information
- How to write **comments** to leave notes in your code
- What a **statement** is and how Python runs statements one by one
- How to correctly write multiple statements
- The optional use of semicolons and when they appear

By the end of this lesson you will be able to write clean, correctly structured Python code and understand exactly why each rule exists.

---

## Prerequisite Concepts

Before diving in, let's make sure you understand a few simple ideas. You do not need any prior programming experience — we will build everything from scratch.

### What is a Program?

A computer program is a list of instructions that you give to a computer. The computer reads each instruction one at a time and carries it out. Think of it like a recipe: you list the steps in order, and the cook (the computer) follows each step exactly.

### What is `print()`?

`print()` is a built-in Python instruction that tells the computer to display something on the screen. You will see it constantly in this lesson. Here is its simplest form:

```python
print("Hello!")
```

**Expected Output:**
```
Hello!
```

- `print` — the instruction name (called a **function**)
- `(` and `)` — parentheses that wrap what you want to print
- `"Hello!"` — the text to display, wrapped in quotation marks

### What is a File vs the Command Line?

You can run Python code in two ways:

1. **Directly in the terminal (Command Line):** Type one line at a time and see the result immediately.
2. **In a `.py` file:** Write your full program in a file called something like `myfile.py`, save it, then run it with: `python myfile.py`

Both ways work. In this lesson, all examples can be used either way.

---

## Part 1 — Python Syntax

### What Is Syntax?

**Syntax** means the set of rules that define how you must write code so that Python can understand it. Every programming language has its own syntax.

Python was designed to be easy to read. Its syntax is clean and minimal — meaning you don't need a lot of extra characters to make things work.

Let's look at a simple example of Python syntax in action:

```python
print("Hello, World!")
```

**Expected Output:**
```
Hello, World!
```

You can run this directly in the Command Line by typing it after `>>>`, or you can put it in a file and run the file.

---

## Part 2 — Python Indentation

### What Is Indentation?

**Indentation** means the blank spaces at the very beginning of a line of code.

Look at this line of text: notice the spaces before the words in a bullet list? That is indentation. In Python, indentation is not just for looks — **it is a rule**.

In most other programming languages (like Java or C), you use curly braces `{}` to group blocks of code together. Python does NOT use curly braces. Instead, Python uses indentation to know which lines of code belong together.

> 🧠 **Analogy:** Think of a recipe. When you write "If the water is boiling:" and then indent the next line "Add the pasta", the indent shows that adding pasta is part of the "if boiling" step. Python works exactly this way.

---

### Why Does Indentation Exist?

Without some way to group lines together, Python cannot tell which instructions belong together and which are separate. Indentation is Python's way of grouping related lines into a **block of code**.

---

### Example 1 — Correct Indentation

```python
if 5 > 2:
    print("Five is greater than two!")
```

**Expected Output:**
```
Five is greater than two!
```

**Line-by-line explanation:**

- `if 5 > 2:` — This is a **condition**. It checks whether 5 is greater than 2. The colon `:` at the end tells Python "a block of code is coming next."
- `    print("Five is greater than two!")` — The four spaces at the start of this line tell Python "this line belongs to the `if` block above." Python will only run this line if the condition above is True.

> 💡 **Note:** We will cover `if` statements in full detail in a later lesson. For now, just focus on understanding how indentation visually groups lines together.

---

### Example 2 — Missing Indentation (Error!)

```python
if 5 > 2:
print("Five is greater than two!")
```

**Expected Output:**
```
IndentationError: expected an indented block
```

**Why the error?** Python sees the `if 5 > 2:` line and expects the next line to be indented (part of the if-block). But `print(...)` starts at the very beginning of the line with no spaces. Python gets confused and crashes.

> ⚠️ **Common Beginner Mistake:** Forgetting to indent after a colon `:`. If you see `IndentationError`, look for a missing indent.

---

### How Many Spaces?

The most common choice is **4 spaces** for one level of indentation. Python only requires at least 1 space, but you must be **consistent** — use the same number of spaces within the same block.

These both work:

```python
# 1 space — allowed but uncommon
if 5 > 2:
 print("Five is greater than two!")

# 4 spaces — recommended and most common
if 5 > 2:
    print("Five is greater than two!")
```

**Expected Output (both):**
```
Five is greater than two!
Five is greater than two!
```

---

### Example 3 — Mixing Spaces in the Same Block (Error!)

```python
if 5 > 2:
 print("Five is greater than two!")
        print("Five is greater than two!")
```

**Expected Output:**
```
IndentationError: unexpected indent
```

**Why the error?** The first `print` uses 1 space. The second `print` uses 8 spaces. Within the same block, you must use the **same** number of spaces every time.

> ✅ **Fix:** Use exactly 4 spaces for both lines:

```python
if 5 > 2:
    print("Five is greater than two!")
    print("Five is greater than two!")
```

**Expected Output:**
```
Five is greater than two!
Five is greater than two!
```

---

### Thinking Prompt

> 🤔 What do you think happens if you use **tabs** instead of spaces? (Hint: mixing tabs and spaces can cause errors. It is best to always use spaces.)

---

### Real-World Connection

In professional software development, consistent indentation is critical. When working in teams, everyone must follow the same indentation style so that the code is readable and understandable. Python forces this habit, which actually makes Python code easier to read than many other languages.

---

## Part 3 — Python Variables

### What Is a Variable?

A **variable** is like a labelled box in your computer's memory where you can store a piece of information. You give the box a name, and you put a value inside it. Later, you can look inside the box by using its name.

> 🧠 **Analogy:** Imagine you have a physical box with a label that says "my_age". You put the number 20 inside it. Any time you need your age, you look in the "my_age" box.

---

### Why Do Variables Exist?

Variables exist so that you can:
- **Store** information for later use
- **Change** that information as your program runs
- **Reuse** the same value many times without rewriting it

---

### How to Create a Variable in Python

In Python, you create a variable simply by giving it a name and assigning it a value using the `=` symbol.

```python
x = 5
y = "Hello, World!"
```

**What just happened?**

- `x = 5` — A variable named `x` is created and the number `5` is stored inside it.
- `y = "Hello, World!"` — A variable named `y` is created and the text `"Hello, World!"` is stored inside it.
- The `=` symbol here does **not** mean "equal to" in the mathematical sense. It means **"assign this value to this variable"**. Think of it as an arrow pointing left: put the value on the right into the box on the left.

> ⚠️ **Common Beginner Mistake:** Confusing `=` (assignment) with `==` (comparison). We will cover `==` in a later lesson.

---

### Using Variables

Once a variable is created, you can use its name anywhere:

```python
x = 5
y = "Hello, World!"
print(x)
print(y)
```

**Expected Output:**
```
5
Hello, World!
```

- `print(x)` — Python looks up the value stored in `x` (which is `5`) and prints it.
- `print(y)` — Python looks up the value stored in `y` (which is `"Hello, World!"`) and prints it.

---

### Example — Changing a Variable's Value

Variables can change! That is what makes them "variable" (changeable):

```python
score = 10
print(score)

score = 25
print(score)
```

**Expected Output:**
```
10
25
```

The value in `score` was first 10, then it was changed to 25.

---

### Important Notes About Variables in Python

- **Python has no command for declaring a variable.** In some other languages you must first say "I want to create a variable" before using it. In Python, the variable is created the moment you assign a value to it.
- Variable names are **case-sensitive**: `Score` and `score` are two different variables.
- Variable names cannot start with a number: `1score` is invalid, but `score1` is fine.
- Variable names cannot have spaces: use underscores instead, like `my_score`.

> 🔗 **Coming up:** You will learn much more about variable naming rules and types in upcoming lessons.

---

## Part 4 — Python Comments

### What Is a Comment?

A **comment** is a piece of text in your code that Python completely ignores when running your program. It is only there for humans to read — it is a note you leave for yourself or other programmers to explain what the code does.

---

### Why Do Comments Exist?

Imagine writing a long program and coming back to it six months later. Without comments, you might forget what each section does. Comments are like sticky notes inside your code.

They are also important in teams: when someone else reads your code, comments help them understand your thinking quickly.

---

### How to Write a Comment

In Python, a comment starts with the `#` symbol. Everything on that line after `#` is a comment:

```python
# This is a comment.
print("Hello, World!")
```

**Expected Output:**
```
Hello, World!
```

Notice that Python printed `Hello, World!` but completely ignored the comment line. The `#This is a comment.` line produced no output.

---

### Inline Comments

You can also put a comment at the end of a line of code:

```python
print("Hello!")  # This prints a greeting
x = 10           # This stores the number 10 in x
```

**Expected Output:**
```
Hello!
```

The code still works normally. Python only ignores the part after `#`.

---

### Example — Multiple Comments

```python
# Step 1: Store the student's name
name = "Amina"

# Step 2: Store the student's score
score = 85

# Step 3: Print the result
print(name)
print(score)
```

**Expected Output:**
```
Amina
85
```

Each comment explains the purpose of the line below it. This makes the code much easier to follow.

---

### What If You Comment Out Code?

Comments are also used to temporarily disable a line of code without deleting it:

```python
print("This line runs.")
# print("This line is commented out and will NOT run.")
print("This line also runs.")
```

**Expected Output:**
```
This line runs.
This line also runs.
```

The middle line was commented out, so Python skipped it entirely.

---

### Real-World Connection

Professional programmers write comments constantly — especially when the logic is complex. In data science projects, comments explain which column is being processed. In web applications, they explain what each function does. Good commenting habits are a hallmark of a professional coder.

---

## Part 5 — Python Statements

### What Is a Statement?

A **statement** is one complete instruction that you give to Python.

Think of it this way: a program is like a to-do list for the computer. Each item on that list is a **statement** — one instruction for the computer to carry out.

```python
print("Python is fun!")
```

This single line is one statement. It tells Python: "Print the text Python is fun! to the screen."

**Expected Output:**
```
Python is fun!
```

---

### Statements Are Executed One by One, In Order

When Python runs your program, it reads each statement from top to bottom and executes them one at a time, in the exact order they are written.

This is called **sequential execution** — like reading a book from page 1 to the last page, in order.

---

### Example — Multiple Statements in Order

```python
print("Hello World!")
print("Have a good day.")
print("Learning Python is fun!")
```

**Expected Output:**
```
Hello World!
Have a good day.
Learning Python is fun!
```

**Step-by-step breakdown:**

1. Python starts at the top and runs `print("Hello World!")` — Output: `Hello World!`
2. Python moves to the next line and runs `print("Have a good day.")` — Output: `Have a good day.`
3. Python moves to the final line and runs `print("Learning Python is fun!")` — Output: `Learning Python is fun!`

The order matters! If you rearranged the lines, the output would also rearrange.

---

### Try It — What If You Reverse the Order?

```python
print("Learning Python is fun!")
print("Have a good day.")
print("Hello World!")
```

**Expected Output:**
```
Learning Python is fun!
Have a good day.
Hello World!
```

> 🤔 **Thinking Prompt:** What does this tell you about how Python reads your code? Does Python skip around, or does it always go line by line from top to bottom?

---

### How Does a Statement End in Python?

In Python, a statement **ends when the line ends**. You simply press Enter to finish a statement. That is all.

This is different from many other programming languages (like Java and C) where you must put a **semicolon** `;` at the end of every statement. Python does not require this.

**Python:**
```python
print("Hello")
```

**Java (just for comparison — you do not need to learn this):**
```java
System.out.println("Hello");
```

Notice the `;` at the end of the Java line. In Python, no semicolon is needed.

---

### Semicolons — Optional and Rarely Used

Even though Python does not require semicolons, you are **allowed** to use them to put multiple statements on one line. However, this is strongly discouraged because it makes code harder to read:

```python
print("Hello"); print("How are you?"); print("Bye bye!")
```

**Expected Output:**
```
Hello
How are you?
Bye bye!
```

This works, but it is messy. Compare it to the cleaner version:

```python
print("Hello")
print("How are you?")
print("Bye bye!")
```

**Expected Output:**
```
Hello
How are you?
Bye bye!
```

Both produce identical results, but the second version is much easier to read at a glance.

> ✅ **Best Practice:** Always put each statement on its own separate line.

---

### What Happens Without a Separator?

If you put two statements on the same line without using a semicolon or a newline, Python gives an error:

```python
print("Python is fun!") print("Really!")
```

**Expected Output:**
```
SyntaxError: invalid syntax
```

Python sees `print("Python is fun!")` and then immediately sees `print(` right after it on the same line with no separator. It does not know what to do and crashes.

> ✅ **Fix:** Put each statement on its own line:

```python
print("Python is fun!")
print("Really!")
```

**Expected Output:**
```
Python is fun!
Really!
```

---

## Part 6 — Putting It All Together

Now let's combine everything we have learned: indentation, variables, comments, and statements — all in one example.

```python
# This program greets a student and shows their score

name = "Chidi"         # Store the student's name
score = 92             # Store the student's score

# Print the greeting and result
print("Student Name:")
print(name)
print("Score:")
print(score)
```

**Expected Output:**
```
Student Name:
Chidi
Score:
92
```

**What happened?**

- Comments explain each section of the code.
- Variables store data that is reused later.
- Each `print()` is a separate statement, executed top to bottom.
- No indentation is needed here because we have no blocks yet (no `if`, no loop).

---

## Guided Practice Exercises

### Exercise 1 — Fix the Syntax Error

The following code has an error. Find it and fix it.

**Broken Code:**
```python
print("Hello")
print("My name is Tunde") print("Nice to meet you!")
```

**Hint:** Look at which line has two statements on it without a separator.

**Fixed Code:**
```python
print("Hello")
print("My name is Tunde")
print("Nice to meet you!")
```

**Expected Output:**
```
Hello
My name is Tunde
Nice to meet you!
```

---

### Exercise 2 — Fix the Indentation Error

**Broken Code:**
```python
if 10 > 3:
print("Ten is greater than three!")
```

**Hint:** The line inside the `if` block needs to be indented.

**Fixed Code:**
```python
if 10 > 3:
    print("Ten is greater than three!")
```

**Expected Output:**
```
Ten is greater than three!
```

---

### Exercise 3 — Write Your Own Program

**Objective:** Write a Python program that stores your name, your city, and your favourite subject in three variables, then prints each one.

**Steps:**
1. Create a variable called `my_name` and assign your name to it as a string (text in quotes).
2. Create a variable called `my_city` and assign your city name.
3. Create a variable called `my_subject` and assign your favourite subject.
4. Write a comment above each variable to describe what it stores.
5. Print each variable using `print()`.

**Example Solution:**
```python
# Store the user's name
my_name = "Funmilayo"

# Store the user's city
my_city = "Ibadan"

# Store the user's favourite subject
my_subject = "Mathematics"

# Print everything
print(my_name)
print(my_city)
print(my_subject)
```

**Expected Output:**
```
Funmilayo
Ibadan
Mathematics
```

**Self-check Questions:**
- Did each variable name clearly describe what it holds?
- Did you add comments above each variable?
- Did each `print()` appear on its own line?
- Did your program run without any errors?

**What-if Challenge:** What happens if you change `my_name = "Funmilayo"` to `my_name = "Amara"`? Run it and check!

---

### Exercise 4 — Write a Multi-Statement Story

**Objective:** Write a program with at least 5 `print()` statements that tells a short story about a student's day at school.

**Scenario:** Imagine a student named Emeka arrives at school, attends a maths class, eats lunch, plays football, then goes home.

**Example Solution:**
```python
# Emeka's school day story

print("Emeka arrived at school at 8am.")
print("He attended his Maths class and solved 10 problems.")
print("At noon, he ate rice and stew for lunch.")
print("After school, he played football with his friends.")
print("He went home at 4pm feeling happy and tired.")
```

**Expected Output:**
```
Emeka arrived at school at 8am.
He attended his Maths class and solved 10 problems.
At noon, he ate rice and stew for lunch.
After school, he played football with his friends.
He went home at 4pm feeling happy and tired.
```

**Optional Challenge:** Add a variable called `student_name = "Emeka"` at the top. Can you replace the word "Emeka" in the first print statement with that variable? (Hint: you will need to learn about **f-strings** in a later lesson — but try thinking about how you might combine text and variables!)

---

## Mini Project — Personal Info Card Generator

In this mini project, you will use everything from this lesson to build a simple program that prints a personal information card to the screen.

### Stage 1 — Setup

Create variables to hold personal information.

```python
# --- Personal Info Card ---

# Store personal details
full_name = "Adaeze Okonkwo"
age = 17
city = "Lagos"
school = "Federal Government College"
favourite_colour = "Blue"
favourite_food = "Jollof Rice"
```

**Milestone:** Run this. You should see no output yet — you only created variables. That's correct!

---

### Stage 2 — Core Logic (Print the Card)

Now print everything neatly.

```python
# --- Personal Info Card ---

full_name = "Adaeze Okonkwo"
age = 17
city = "Lagos"
school = "Federal Government College"
favourite_colour = "Blue"
favourite_food = "Jollof Rice"

# Print the card header
print("==========================")
print("   MY PERSONAL INFO CARD  ")
print("==========================")

# Print personal details
print("Name:")
print(full_name)
print("Age:")
print(age)
print("City:")
print(city)
print("School:")
print(school)
print("Favourite Colour:")
print(favourite_colour)
print("Favourite Food:")
print(favourite_food)

# Print card footer
print("==========================")
```

**Expected Output:**
```
==========================
   MY PERSONAL INFO CARD  
==========================
Name:
Adaeze Okonkwo
Age:
17
City:
Lagos
School:
Federal Government College
Favourite Colour:
Blue
Favourite Food:
Jollof Rice
==========================
```

---

### Stage 3 — Reflection Questions

After completing the project, ask yourself:

1. Which part of the code are the **variables**?
2. Which part of the code are the **statements**?
3. Which lines are **comments**?
4. Does the indentation matter in this program? (There are no `if` blocks here, so no indentation is needed — can you see why?)
5. What would happen if you accidentally put two `print()` statements on the same line without a semicolon?

---

### Stage 4 — Optional Enhancements

- Add more variables: `hobby`, `favourite_subject`, `dream_job`
- Print a separator line like `"---"` between each item
- Change the values in the variables to your own real information and share the output with a friend

---

## Common Beginner Mistakes

Here is a summary of the most common mistakes beginners make in this lesson, along with how to fix them:

**Mistake 1 — Forgetting to indent after a colon**

```python
# WRONG
if 5 > 2:
print("Hello")

# CORRECT
if 5 > 2:
    print("Hello")
```

**Mistake 2 — Mixing different numbers of spaces in the same block**

```python
# WRONG
if 5 > 2:
 print("Hello")
    print("World")

# CORRECT
if 5 > 2:
    print("Hello")
    print("World")
```

**Mistake 3 — Putting two statements on the same line without a separator**

```python
# WRONG
print("Hello") print("World")

# CORRECT
print("Hello")
print("World")
```

**Mistake 4 — Using `=` when you mean comparison (we'll cover this fully later)**

```python
# Creating a variable (correct use of =)
x = 5

# This assigns 10 to x, not compares (common confusion)
x = 10
```

**Mistake 5 — Forgetting quotes around text**

```python
# WRONG — Python thinks "Hello" is a variable name
print(Hello)

# CORRECT — Quotes tell Python this is text
print("Hello")
```

**Mistake 6 — Starting a variable name with a number**

```python
# WRONG
1score = 95

# CORRECT
score1 = 95
```

---

## Reflection Questions

Take a moment to think about what you have learned:

1. In your own words, what is **syntax**? Why does every programming language have its own syntax?
2. Why does Python use **indentation** instead of curly braces `{}` like other languages?
3. What does the `#` symbol do in Python?
4. What is the difference between a **variable** and a **statement**?
5. In what order does Python execute statements — random order or top to bottom?
6. You saw that semicolons are optional in Python. Why is it still better practice to avoid them?
7. What would you use a **comment** for in a real-world project?

---

## Completion Checklist

Before moving on to the next lesson, confirm that you can do each of the following:

- [ ] Explain what Python syntax means in simple words
- [ ] Write an `if` block with correct indentation
- [ ] Identify and fix an `IndentationError`
- [ ] Create a variable and assign a value to it
- [ ] Print the value stored in a variable
- [ ] Write a single-line comment using `#`
- [ ] Write a program with multiple statements in the correct order
- [ ] Explain why two statements on the same line without a separator causes an error
- [ ] Identify and fix a `SyntaxError` caused by missing newline between statements
- [ ] Complete the Personal Info Card mini project

---

## Lesson Summary

Here is everything you learned in Lesson 02:

**Python Syntax** is the set of rules that define how Python code must be written. Breaking these rules causes errors.

**Indentation** is the spaces at the start of a line. Unlike other languages, Python uses indentation to group lines of code into blocks. You must indent at least one space after a colon `:`, and you must use the same number of spaces within the same block. The most common choice is 4 spaces.

**Variables** are named containers for storing values. You create a variable by writing its name, then `=`, then the value. Python creates the variable automatically — no special declaration command is needed.

**Comments** start with `#` and are completely ignored by Python. They exist purely as notes for human readers.

**Statements** are individual instructions to Python. A program is a list of statements executed one at a time, from top to bottom, in order. In Python, a statement ends when the line ends — you do not need a semicolon. Multiple statements can technically be placed on one line using `;`, but this is discouraged. Two statements on the same line without any separator causes a `SyntaxError`.

---

> 🎉 **Well done!** You have completed Lesson 02. You now understand the core structure of every Python program. In the next lesson, you will explore **Python Output** — learning different ways to print text and numbers to the screen with much more control. Keep going!

---

*Sources: W3Schools Python Syntax (https://www.w3schools.com/python/python_syntax.asp) and Python Statements (https://www.w3schools.com/python/python_statements.asp)*
