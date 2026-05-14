---
render_with_liquid: false
title: "Lesson 01 — Introduction to Python: What It Is, How to Set It Up, and How to Use It"
nav_order: 1
---

# Lesson 01 — Introduction to Python: What It Is, How to Set It Up, and How to Use It

---

## Welcome to Your Python Journey

Imagine being able to tell a computer exactly what to do — step by step — and have it follow your instructions perfectly every single time. That is exactly what programming is. And **Python** is one of the friendliest languages to start learning how to do it.

This lesson is designed for absolute beginners. You do not need any previous experience with programming, computers, or mathematics beyond basic arithmetic. Every single concept will be explained from scratch, with real examples and expected outputs so you always know what to expect.

By the end of this lesson you will:
- Know what Python is and why it is worth learning
- Have Python installed and running on your computer
- Understand how Python reads and runs your code
- Write your first Python programs
- Understand how Python statements, syntax, indentation, and output work
- Print text and numbers to the screen confidently

Let's begin.

---

## Prerequisite Concepts

Before we dive into Python, let's quickly cover two foundational ideas you need to understand. Don't worry — these are very simple.

### What is a Program?

A **program** is a list of instructions written for a computer. Just like a recipe tells a cook what to do step by step, a program tells a computer what to do step by step.

**Analogy:** Imagine you are directing a robot helper. You cannot just say "make breakfast." You have to say:
1. Open the fridge.
2. Take out two eggs.
3. Turn on the stove.
4. Crack the eggs into the pan.
5. Wait 3 minutes.
6. Turn off the stove.

A computer program works the same way — precise, step-by-step instructions.

### What is a Programming Language?

Computers do not understand human language (like English or Yoruba). They only understand numbers (0s and 1s). A **programming language** is a special language that sits between human language and machine language. You write instructions in a programming language, and a tool called an **interpreter** or **compiler** translates those instructions into something the computer can understand.

Python is one of the most popular and beginner-friendly programming languages in the world.

---

## Section 1 — What is Python?

### The History and Purpose

Python is a **general-purpose programming language** created by a Dutch programmer named **Guido van Rossum**. It was first released to the public in **1991** — over 30 years ago! Since then, it has grown into one of the most widely used languages in the world.

The word "Python" comes not from the snake, but from Guido's love of the British comedy show *Monty Python's Flying Circus*.

### What Can Python Do?

Python is like a Swiss army knife for programmers — it can be used for many different things:

- **Web development (server-side):** Python can power the behind-the-scenes logic of websites. Big platforms like Instagram and Pinterest were built using Python.
- **Software development:** You can build desktop applications, games, and tools.
- **Mathematics and data analysis:** Python is widely used by scientists, engineers, and data analysts to crunch numbers, draw charts, and find patterns in data.
- **Automation:** Python can automate repetitive tasks, like renaming thousands of files, sending emails, or scraping data from websites.
- **Machine learning and artificial intelligence:** Python powers most of the AI tools you hear about today — from recommendation systems to image recognition.
- **Connecting to databases:** Python can read from and write to databases like MySQL and MongoDB.
- **Big data:** Python handles and processes enormous datasets.
- **Rapid prototyping:** You can quickly test ideas without writing hundreds of lines of code first.

### Why Should You Learn Python?

Here are the key reasons Python is such a great first language:

- **Simple syntax:** Python's code reads almost like plain English. Compare this to languages like Java or C++ which require much more complex setup just to print "Hello World".
- **Fewer lines of code:** Python lets you accomplish the same task with far fewer lines than most other languages, saving you time.
- **Cross-platform:** Python runs on Windows, Mac, Linux, Raspberry Pi, and many other systems without any changes to your code.
- **Interpreted language:** Python runs code line by line as soon as it is written, so you see results immediately. There is no long "compile" wait like in some other languages.
- **Flexible programming styles:** Python can be written in a procedural way (step-by-step instructions), an object-oriented way (using classes and objects), or a functional way (using pure functions). You learn more about these styles as you grow.
- **Huge community:** Millions of programmers use Python. Whatever problem you face, someone has probably solved it and shared the solution online.

### Python in the Real World

| Field | How Python is Used |
|---|---|
| Data Science | Analysing stock prices, weather patterns, election data |
| Medicine | Modelling virus spread, genomics research |
| Finance | Automated trading bots, risk analysis |
| Engineering | Simulating physical systems, robotics |
| Education | Teaching programming, e-learning platforms |
| Social Media | Recommending posts, detecting spam |

> **Thinking Prompt:** Which of these use cases interests you most? As you learn Python, keep that application in mind — it will motivate you.

---

## Section 2 — Getting Started: Installing and Running Python

### Option A: Try Python Online (No Installation Needed)

If you just want to start experimenting right now without installing anything, you can use an online Python editor. Websites like [https://www.w3schools.com/python/trypython.asp](https://www.w3schools.com/python/trypython.asp) let you type Python code in your browser and see the result immediately.

This is a great way to follow along with the examples in this lesson.

### Option B: Install Python on Your Computer

To run Python on your own machine, follow these steps.

#### Step 1: Check if Python is Already Installed

Many computers already have Python installed. Let's check.

**On Windows:**
1. Press the **Windows key**, type `cmd`, and open the Command Prompt.
2. Type the following and press Enter:

```
python --version
```

**On Mac or Linux:**
1. Open the **Terminal**.
2. Type:

```
python --version
```

If you see something like `Python 3.12.0`, you already have Python! If not, move to Step 2.

#### Step 2: Download Python

Go to the official Python website: **https://www.python.org/**

Click **Download Python** and follow the installer instructions. Make sure you are downloading **Python 3** (not Python 2, which is outdated).

> **Important for Windows users:** During installation, tick the box that says **"Add Python to PATH"**. This makes Python accessible from your Command Prompt.

#### Step 3: Verify the Installation

After installation, open your Command Prompt or Terminal again and type:

```
python --version
```

You should now see a version number printed, like:

```
Python 3.12.0
```

Congratulations — Python is installed!

### Writing and Running Your First Python File

Now let's write our very first Python program.

**Step 1:** Open any plain-text editor (Notepad on Windows, TextEdit on Mac, or any code editor like VS Code).

**Step 2:** Type the following:

```python
print("Hello, World!")
```

**Step 3:** Save the file as `hello.py` (the `.py` extension tells the computer this is a Python file).

**Step 4:** Open your Command Prompt or Terminal, navigate to the folder where you saved the file, and type:

```
python hello.py
```

**Expected Output:**
```
Hello, World!
```

You just ran your first Python program! Let's unpack exactly what happened.

- `print` is a **function** — a built-in tool in Python that displays output.
- The parentheses `()` tell Python "here comes what I want to print."
- `"Hello, World!"` is the **text** you want to display. The quotation marks tell Python this is a piece of text (called a **string**).

### Using the Python Command Line (Interactive Mode)

Python also has a special **interactive mode** where you can type one line of code at a time and see the result immediately. This is perfect for quick experiments.

Open your Command Prompt or Terminal and type:

```
python
```

(On some systems, use `py` instead of `python`.)

You will see something like:

```
Python 3.12.0 (main, Oct  3 2023, ...) on win32
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

The `>>>` symbol is called the **prompt**. It means Python is ready and waiting for your instruction.

Type this and press Enter:

```python
>>> print("Hello, World!")
```

**Expected Output:**
```
Hello, World!
```

To exit the Python command line, type:

```python
exit()
```

### Checking Your Python Version From Inside Code

You can also find out which version of Python is running directly from your program:

```python
import sys

print(sys.version)
```

**Expected Output (will vary depending on your version):**
```
3.12.0 (main, Oct  3 2023, 08:56:10) [GCC 11.4.0]
```

- `import sys` loads a built-in Python **module** (a collection of extra tools). `sys` is the system module.
- `sys.version` is a piece of information stored in that module — your Python version.

> You will learn a lot more about modules later in the course. For now, just know they are extra toolkits you can bring into your program.

---

## Section 3 — Python Syntax: The Rules of the Language

Just like English has grammar rules (sentences start with a capital letter, end with a full stop, etc.), Python has **syntax rules**. Syntax means the correct way to write code so that Python can understand it.

Think of syntax as the grammar of your programming language. Break the rules, and Python gives you an error — just like how a teacher might mark a sentence wrong if you break grammar rules.

### Rule 1: Python Executes Code Line by Line

Python reads your code from the very first line to the very last line, one line at a time. Each line is a new instruction.

```python
print("First line runs first")
print("Second line runs second")
print("Third line runs third")
```

**Expected Output:**
```
First line runs first
Second line runs second
Third line runs third
```

This is called **sequential execution** — instructions run in the order you write them. This is very important: if you want something to happen first, you must write it first.

### Rule 2: Python Uses Indentation (Spaces) to Define Blocks

This is one of Python's most important and unique rules.

**What is indentation?**
Indentation means the spaces at the beginning of a line. Look at this:

```
This line has no spaces at the start.
    This line has 4 spaces at the start.
```

In many other programming languages, indentation is optional — just for humans to read more easily. But in Python, **indentation is mandatory**. It is how Python knows which lines of code belong together.

Let's see this with a simple example. You will not fully understand the `if` statement yet (we cover that in a later lesson), but focus on the indentation:

**Correct — with indentation:**

```python
if 5 > 2:
    print("Five is greater than two!")
```

**Expected Output:**
```
Five is greater than two!
```

**Incorrect — without indentation:**

```python
if 5 > 2:
print("Five is greater than two!")
```

**Expected Output (Error!):**
```
IndentationError: expected an indented block after 'if' statement on line 1
```

Do you see the difference? The second example is missing the 4 spaces before `print(...)`. Python sees this as a syntax error because the `if` statement needs at least one indented line after it.

**How many spaces?**

You can use any number of spaces, as long as you are consistent within a block. The standard is **4 spaces**, which most professional programmers and style guides recommend.

```python
if 5 > 2:
    print("Using 4 spaces — this works!")

if 5 > 2:
        print("Using 8 spaces — this also works!")
```

**Expected Output:**
```
Using 4 spaces — this works!
Using 8 spaces — this also works!
```

**Mixing spaces in the same block causes an error:**

```python
if 5 > 2:
    print("Four spaces here")
        print("Eight spaces here — ERROR!")
```

**Expected Output (Error!):**
```
IndentationError: unexpected indent
```

> **Golden Rule:** Always use the same number of spaces for each level of indentation. Using 4 spaces consistently is the best practice.

> **Thinking Prompt:** What do you think would happen if you used a tab (`Tab` key) instead of spaces? In Python, mixing tabs and spaces causes errors. Always pick one and stick with it. The recommended choice is **spaces**.

### Rule 3: Variables Are Created by Assignment

A **variable** is a named storage box in your computer's memory. You put a value into it, and you can use that value later by calling its name.

In Python, you create a variable simply by writing its name, the `=` sign, and the value:

```python
x = 5
y = "Hello, World!"
```

Let's break this down:
- `x` is the variable **name** (you choose this name).
- `=` is the **assignment operator** — it means "store this value into this variable."
- `5` is the **value** being stored. Since it has no quotes, Python knows it is a number.
- `y` is another variable name.
- `"Hello, World!"` is the value stored in `y`. Since it has quotes, Python knows it is text (a string).

Unlike some other languages, you do not need to tell Python in advance what type of value a variable will hold. Python figures it out automatically.

```python
age = 25
name = "Adaora"
height = 1.72
is_student = True
```

> You will explore variables much more deeply in Lesson 02. For now, just know they exist and how to create them.

### Rule 4: Comments Explain Your Code

A **comment** is a note written in your code for humans to read. Python completely ignores comments when running the program.

Comments start with the `#` (hash) symbol:

```python
# This is a comment. Python ignores this line.
print("Hello, World!")  # This comment is at the end of a line
```

**Expected Output:**
```
Hello, World!
```

Notice that the comment on line 1 produces no output — Python just skips it.

**Why are comments important?**
- They help you (and others) remember why you wrote a piece of code.
- They are essential for collaboration with other programmers.
- They help when you return to your code weeks or months later.

```python
# Calculate the area of a rectangle
length = 10   # length in centimetres
width = 5     # width in centimetres
area = length * width
print(area)
```

**Expected Output:**
```
50
```

---

## Section 4 — Python Statements: The Building Blocks

### What is a Statement?

A **statement** is a single instruction in a Python program. It is the most basic unit of a program — one action the computer performs.

Here is a very simple statement:

```python
print("Python is fun!")
```

**Expected Output:**
```
Python is fun!
```

This is one statement. It does one thing: print the text "Python is fun!" to the screen.

### Programs Contain Many Statements

Real programs contain many statements. Each statement runs in order, from top to bottom:

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

Let's trace through this step by step:
1. Python reads line 1: `print("Hello World!")` → It prints "Hello World!" → moves on.
2. Python reads line 2: `print("Have a good day.")` → It prints "Have a good day." → moves on.
3. Python reads line 3: `print("Learning Python is fun!")` → It prints "Learning Python is fun!" → program ends.

> **Thinking Prompt:** What would happen if you swapped line 1 and line 3? Try it and see!

### In Python, Each Statement Goes on Its Own Line

Unlike many other languages (like Java or C++), Python does **not** require a semicolon (`;`) at the end of each statement. Just pressing Enter (a new line) is enough to end a statement:

**Python (correct — no semicolons needed):**
```python
print("Statement one")
print("Statement two")
```

**Java (requires semicolons):**
```java
System.out.println("Statement one");
System.out.println("Statement two");
```

This is one reason Python is much cleaner and easier to read.

### Optional: Multiple Statements on One Line with Semicolons

Python does allow you to put multiple statements on one line by separating them with semicolons, but this is considered bad practice and is rarely done. It makes code hard to read:

```python
print("Hello"); print("How are you?"); print("Bye bye!")
```

**Expected Output:**
```
Hello
How are you?
Bye bye!
```

This works, but the best practice is to put each statement on its own line:

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

The second version is much cleaner. Follow this rule: **one statement per line**.

### What Happens if You Put Two Statements on One Line Without a Separator?

```python
print("Python is fun!") print("Really!")
```

**Expected Output (Error!):**
```
SyntaxError: invalid syntax
```

Python sees the second `print` and does not know what to do with it because there is no separator (newline or semicolon). This is a **SyntaxError** — you have broken a syntax rule.

---

## Section 5 — Python Output: Displaying Information

### What is Output?

In computing, **output** means information that a program sends out to be seen or used. The most common form of output in Python for beginners is text or numbers displayed in the terminal (the black Command Prompt or Terminal window).

Think of output as your program talking to you.

### The `print()` Function

The `print()` function is the most fundamental output tool in Python. It displays whatever you give it on the screen.

**Syntax:**
```python
print(something_to_display)
```

The word `print` is the function name. The parentheses `()` contain what you want to display. That content inside the parentheses is called the **argument**.

#### Printing Text

Text in Python must always be wrapped in quotes. You can use either double quotes (`"..."`) or single quotes (`'...'`) — both work:

```python
print("This will work!")
print('This will also work!')
```

**Expected Output:**
```
This will work!
This will also work!
```

**What happens without quotes?**

```python
print(This will cause an error)
```

**Expected Output (Error!):**
```
SyntaxError: invalid syntax
```

Python sees `This will cause an error` without quotes and tries to treat each word as a variable name or function. Since these variables do not exist, it throws an error.

> **Golden Rule:** Text (strings) must always be wrapped in quotes.

#### Printing Multiple Lines of Text

You can call `print()` multiple times to display multiple lines:

```python
print("Hello World!")
print("I am learning Python.")
print("It is awesome!")
```

**Expected Output:**
```
Hello World!
I am learning Python.
It is awesome!
```

Each `print()` call automatically moves to a **new line** before printing the next item. This is the default behaviour — it happens automatically.

#### Printing on the Same Line (Removing the New Line)

Sometimes you want multiple prints to appear on the same line. You can do this using the `end` parameter:

```python
print("Hello World!", end=" ")
print("I will print on the same line.")
```

**Expected Output:**
```
Hello World! I will print on the same line.
```

Let's break this down:
- By default, `print()` adds a newline character (`\n`) at the end of its output, which moves the cursor to the next line.
- When you write `end=" "`, you are telling Python: "Instead of ending with a newline, end with a space." So the next `print()` call continues on the same line.

> **Thinking Prompt:** What do you think would happen if you wrote `end=""` (with nothing inside the quotes)?

---

## Section 6 — Printing Numbers

### Numbers vs. Text: A Key Difference

In Python, there is an important distinction between **text (strings)** and **numbers**:

- Text must be surrounded by quotes: `"Hello"` or `'42'`
- Numbers must NOT have quotes: `42` or `3.14`

If you put a number inside quotes, Python treats it as text, not as a number. This matters a lot when you want to do maths with it.

```python
print(42)        # This is the number 42
print("42")      # This is the TEXT "42" — not a number!
```

**Expected Output:**
```
42
42
```

They look the same when printed! But internally Python treats them very differently. The first can be used in maths; the second cannot.

### Printing Numbers Directly

You can print numbers without any quotes:

```python
print(3)
print(358)
print(50000)
```

**Expected Output:**
```
3
358
50000
```

### Doing Mathematics Inside print()

One of the most useful beginner tricks: you can perform calculations directly inside `print()`:

```python
print(3 + 3)
print(2 * 5)
```

**Expected Output:**
```
6
10
```

Let's trace through:
- Line 1: Python sees `3 + 3`, **evaluates** it (calculates it), gets `6`, then prints `6`.
- Line 2: Python sees `2 * 5`, evaluates it, gets `10`, then prints `10`.

Python supports all the basic arithmetic operations:

| Operator | Meaning | Example | Result |
|---|---|---|---|
| `+` | Addition | `3 + 4` | `7` |
| `-` | Subtraction | `10 - 3` | `7` |
| `*` | Multiplication | `4 * 5` | `20` |
| `/` | Division | `10 / 4` | `2.5` |
| `**` | Exponentiation (power) | `2 ** 3` | `8` |
| `//` | Integer (floor) division | `10 // 3` | `3` |
| `%` | Modulus (remainder) | `10 % 3` | `1` |

Let's try a few:

```python
print(10 + 5)
print(10 - 5)
print(10 * 5)
print(10 / 5)
print(2 ** 4)
print(10 // 3)
print(10 % 3)
```

**Expected Output:**
```
15
5
50
2.0
16
3
1
```

> **Notice:** `10 / 5` gives `2.0` (with a decimal point), not just `2`. Python's `/` operator always returns a decimal (float). If you want a whole number result, use `//`.

### Mixing Text and Numbers in One Output

You can combine text and numbers in a single `print()` by separating them with a comma:

```python
print("I am", 35, "years old.")
```

**Expected Output:**
```
I am 35 years old.
```

Let's break this down:
- `"I am"` — this is a text string.
- `35` — this is a number.
- `"years old."` — this is another text string.
- The commas `,` inside `print()` separate multiple items to display. Python automatically puts a space between each item.

Another example:

```python
print("The answer is", 5 + 7, "and that is correct!")
```

**Expected Output:**
```
The answer is 12 and that is correct!
```

Python first evaluates `5 + 7` to get `12`, then combines everything and prints it.

---

## Section 7 — Guided Practice Exercises

Now it is time to practise what you have learned. Work through each exercise carefully.

### Exercise 1: Your First Program (Warm-Up)

**Objective:** Print three lines of text about yourself.

**Scenario:** Imagine you are introducing yourself to your Python teacher. Write a program that prints your name, your city, and one thing you want to learn with Python.

**Steps:**
1. Open your text editor or Python command line.
2. Write three `print()` statements.
3. Run the program.

**Example Solution:**

```python
print("My name is Chidi.")
print("I live in Ibadan, Nigeria.")
print("I want to learn Python to build data analysis tools.")
```

**Expected Output:**
```
My name is Chidi.
I live in Ibadan, Nigeria.
I want to learn Python to build data analysis tools.
```

**Self-check Question:** Did each line print on its own line? Did you use quotes around your text?

---

### Exercise 2: Maths with print()

**Objective:** Use Python as a calculator.

**Scenario:** A student scored 45 out of 60 in a maths test and 38 out of 50 in an English test. Use Python's `print()` to calculate and display:
1. The total marks scored across both subjects.
2. The total possible marks.
3. The difference between the highest possible and actual marks.

**Steps:**
1. Write a `print()` for each calculation.
2. Use arithmetic operators inside `print()`.

**Solution:**

```python
print("Maths score:", 45)
print("English score:", 38)
print("Total scored:", 45 + 38)
print("Total possible:", 60 + 50)
print("Marks missed:", (60 + 50) - (45 + 38))
```

**Expected Output:**
```
Maths score: 45
English score: 38
Total scored: 83
Total possible: 110
Marks missed: 27
```

**Self-check Question:** What would the output look like if you wrote `print("Total scored:", "45 + 38")` instead? Try it!

---

### Exercise 3: Comments and Readability

**Objective:** Write a well-commented program.

**Scenario:** Write a program that prints the name of a product, its price, and a discount percentage. Add comments explaining what each line does.

**Solution:**

```python
# Program to display product pricing information
print("Product: Rice (25kg bag)")   # Print the product name
print("Original Price: N12,500")    # Print the original price
print("Discount: 10%")              # Print the discount
print("You save: N1,250")           # Print the savings amount
```

**Expected Output:**
```
Product: Rice (25kg bag)
Original Price: N12,500
Discount: 10%
You save: N1,250
```

**Self-check Question:** If you deleted the `#` from line 1, what would happen when you run the program?

---

### Exercise 4: Indentation Awareness

**Objective:** Understand the importance of indentation.

**Scenario:** Identify the error in each code snippet and fix it.

**Buggy Code 1:**
```python
if 10 > 5:
print("Ten is greater!")
```

**What is wrong?** There is no indentation before `print`. The line inside the `if` block must be indented.

**Fixed Code:**
```python
if 10 > 5:
    print("Ten is greater!")
```

**Expected Output:**
```
Ten is greater!
```

**Buggy Code 2:**
```python
if 3 > 1:
    print("First line")
        print("Second line — wrong indentation!")
```

**What is wrong?** Both `print` statements are inside the same `if` block, but they have different levels of indentation (4 spaces vs. 8 spaces).

**Fixed Code:**
```python
if 3 > 1:
    print("First line")
    print("Second line — correct now!")
```

**Expected Output:**
```
First line
Second line — correct now!
```

---

### Exercise 5: Mixing Text and Numbers

**Objective:** Use commas inside `print()` to mix text and calculated numbers.

**Scenario:** A STEM student is measuring the dimensions of a rectangular plot of land. Length is 12 metres, width is 8 metres. Print a sentence showing the area.

**Solution:**

```python
length = 12
width = 8
print("The area of the plot is", length * width, "square metres.")
```

**Expected Output:**
```
The area of the plot is 96 square metres.
```

**What-if challenge:** Change `length` to 15 and `width` to 10. What does the output become?

---

## Section 8 — Mini Project: Personal Greetings Display

Now let's combine everything you've learned into one small, realistic project.

### Project Description

You will build a simple **greeting card program**. When you run it, it will display a neatly formatted greeting message with your name, today's date, a motivational quote, and a maths result.

### Stage 1: Setup — Basic Output

Start with just printing your name and a welcome message:

```python
# Stage 1: Basic greeting
print("==============================")
print("Welcome to My Python Program!")
print("==============================")
```

**Expected Output:**
```
==============================
Welcome to My Python Program!
==============================
```

**Milestone Achieved:** You can print decorative separators using repeated characters inside strings.

### Stage 2: Core Logic — Personal Information

Add your personal details:

```python
# Stage 2: Personal information display
print("==============================")
print("Welcome to My Python Program!")
print("==============================")
print("Name: Chidi Okonkwo")
print("City: Ibadan, Nigeria")
print("Course: Python Fundamentals")
print("Lesson: 01 — Introduction")
print("==============================")
```

**Expected Output:**
```
==============================
Welcome to My Python Program!
==============================
Name: Chidi Okonkwo
City: Ibadan, Nigeria
Course: Python Fundamentals
Lesson: 01 — Introduction
==============================
```

**Milestone Achieved:** Your program produces a structured, readable layout.

### Stage 3: Enhancements — Adding Calculations

Now add a maths calculation to show that Python works as a calculator:

```python
# Stage 3: Full greeting card with calculation
print("==============================")
print("Welcome to My Python Program!")
print("==============================")
print("Name: Chidi Okonkwo")
print("City: Ibadan, Nigeria")
print("Course: Python Fundamentals")
print("Lesson: 01 — Introduction")
print("==============================")
print("Fun Fact: 2 to the power of 10 =", 2 ** 10)
print("Fun Fact: 365 days in a year x 24 hours =", 365 * 24, "hours")
print("==============================")
print("Keep learning! Every expert was once a beginner.")
print("==============================")
```

**Expected Output:**
```
==============================
Welcome to My Python Program!
==============================
Name: Chidi Okonkwo
City: Ibadan, Nigeria
Course: Python Fundamentals
Lesson: 01 — Introduction
==============================
Fun Fact: 2 to the power of 10 = 1024
Fun Fact: 365 days in a year x 24 hours = 8760 hours
==============================
Keep learning! Every expert was once a beginner.
==============================
```

**Reflection Questions:**
- How would you change this to display someone else's name?
- What other fun facts could you add using Python maths?
- How could you make the banner wider?

### Optional Extension: Printing on the Same Line

Try creating a horizontal banner using `end`:

```python
print("* ", end="")
print("* ", end="")
print("* ", end="")
print("* ", end="")
print("*")
```

**Expected Output:**
```
* * * * *
```

> **Advanced Optional:** How could you print 20 stars on one line using only two lines of code? (Hint: think about multiplying strings — you will learn this in a future lesson!)

---

## Section 9 — Common Beginner Mistakes

Let's look at the most common mistakes new Python learners make — and how to fix them.

### Mistake 1: Forgetting Quotes Around Text

**Wrong:**
```python
print(Hello World)
```

**Error:**
```
SyntaxError: invalid syntax
```

**Fixed:**
```python
print("Hello World")
```

**Why:** Text that is not a number must be wrapped in quotes. Without quotes, Python thinks you are referencing a variable called `Hello`, which does not exist.

---

### Mistake 2: Using the Wrong Quote Style (Mixing Quotes)

**Wrong:**
```python
print("Hello World')
```

**Error:**
```
SyntaxError: EOL while scanning string literal
```

**Fixed:**
```python
print("Hello World")
# OR
print('Hello World')
```

**Why:** You must open and close with the same type of quote. If you open with `"`, you must close with `"`. If you open with `'`, you must close with `'`.

---

### Mistake 3: Missing Indentation

**Wrong:**
```python
if 5 > 2:
print("Five is greater!")
```

**Error:**
```
IndentationError: expected an indented block
```

**Fixed:**
```python
if 5 > 2:
    print("Five is greater!")
```

**Why:** Python requires at least one indented line inside blocks like `if` statements. The indentation tells Python which code belongs inside the block.

---

### Mistake 4: Inconsistent Indentation

**Wrong:**
```python
if 5 > 2:
    print("Line one")
      print("Line two — extra spaces!")
```

**Error:**
```
IndentationError: unexpected indent
```

**Fixed:**
```python
if 5 > 2:
    print("Line one")
    print("Line two — consistent now!")
```

**Why:** All lines inside the same block must have the exact same indentation level.

---

### Mistake 5: Putting Numbers Inside Quotes When You Want to Do Maths

**Wrong (if you want to add numbers):**
```python
print("5" + "3")
```

**Unexpected Output:**
```
53
```

**What you probably wanted:**
```python
print(5 + 3)
```

**Expected Output:**
```
8
```

**Why:** When numbers are inside quotes, Python treats them as text (strings). Adding two text strings with `+` joins them together (called **concatenation**), not adds them mathematically. So `"5" + "3"` becomes `"53"`, not `8`.

---

### Mistake 6: Running Two Statements on the Same Line Without a Separator

**Wrong:**
```python
print("Hello") print("World")
```

**Error:**
```
SyntaxError: invalid syntax
```

**Fixed:**
```python
print("Hello")
print("World")
```

**Why:** Python expects one statement per line. If you must put two on one line, separate them with a semicolon (but the recommended practice is always one statement per line).

---

### Mistake 7: Case Sensitivity — `Print` Is Not `print`

**Wrong:**
```python
Print("Hello World!")
```

**Error:**
```
NameError: name 'Print' is not defined
```

**Fixed:**
```python
print("Hello World!")
```

**Why:** Python is **case-sensitive**. `print`, `Print`, and `PRINT` are three completely different names in Python. The built-in function is all lowercase: `print`.

---

## Section 10 — Reflection Questions

Take a moment to think about these questions. You do not need to write code — just think through the answers:

1. What is the difference between `print(5)` and `print("5")`? When would each be useful?

2. If you wrote `print("Hello")` and then `print("World")` — what is the output? Now what if you used `end=" "` on the first `print`?

3. Why do you think Python uses indentation to define blocks instead of curly braces `{}` like Java and C? What advantage does indentation give to human readers?

4. A friend writes `print(10 / 3)`. What will they see in the output? Why?

5. You want to calculate how many seconds are in a week. How would you write that as a single `print()` statement? (Hint: 7 days, 24 hours per day, 60 minutes per hour, 60 seconds per minute.)

6. Look at this code:
```python
# Calculate total cost
items = 3
price = 250
print("Total cost:", items * price, "Naira")
```
What does each line do? What is the output?

---

## Section 11 — Completion Checklist

Use this checklist to confirm you have mastered Lesson 01. Tick each item as you feel confident with it:

- [ ] I can explain what Python is and list at least 3 things it can be used for.
- [ ] I know when Python was created and by whom.
- [ ] I have installed Python on my computer (or know how to access it online).
- [ ] I can check the Python version from the command line.
- [ ] I can create a `.py` file and run it from the terminal.
- [ ] I know what a statement is and can write multiple statements.
- [ ] I understand that Python runs statements from top to bottom.
- [ ] I understand that each statement goes on its own line.
- [ ] I know what indentation is and why Python requires it.
- [ ] I know how to write single-line comments with `#`.
- [ ] I can use `print()` to display text.
- [ ] I know that text must be wrapped in quotes.
- [ ] I can use both double (`"`) and single (`'`) quotes.
- [ ] I can use `print()` to display numbers without quotes.
- [ ] I can perform arithmetic operations inside `print()`.
- [ ] I can use commas inside `print()` to mix text and numbers.
- [ ] I can use the `end` parameter to control line endings.
- [ ] I can identify and fix the 7 common beginner mistakes listed in this lesson.
- [ ] I have completed the mini project greeting card program.
- [ ] I can answer at least 4 of the 6 reflection questions.

---

## Section 12 — Lesson Summary

Here is a concise summary of everything covered in this lesson.

**Python is a general-purpose programming language** created by Guido van Rossum and released in 1991. It is used for web development, software, data analysis, automation, AI, and much more. Its simple, readable syntax makes it ideal for beginners.

**Installing Python:** Download from python.org. Check installation with `python --version` in your terminal. Python files use the `.py` extension and are run with `python filename.py`.

**Python Syntax Rules:**
- Code executes line by line, top to bottom.
- **Indentation is mandatory** to define code blocks (4 spaces is standard).
- Each statement goes on its own line.
- Python is case-sensitive (`print` ≠ `Print`).

**Variables** are created simply by assigning a value: `x = 5`.

**Comments** start with `#` and are ignored by Python — they are for humans only.

**Statements** are individual instructions. Python does not require semicolons. One statement per line is best practice.

**The `print()` function:**
- Displays text (must be in quotes) or numbers (no quotes needed).
- Each call prints on a new line by default.
- Use `end=" "` to print on the same line.
- Commas inside `print()` separate multiple items and automatically add spaces.
- Arithmetic expressions like `print(5 + 3)` are evaluated before printing.

**Common mistakes:**
- Forgetting quotes around text → `SyntaxError`
- Mixing quote types → `SyntaxError`
- Missing indentation → `IndentationError`
- Treating numbers as text by adding quotes → wrong maths behaviour
- Wrong capitalisation of function names → `NameError`

---

## What Comes Next?

In **Lesson 02**, you will dive deep into **Python Variables and Data Types** — you will learn how to store, name, and manipulate different kinds of information including text, whole numbers, decimals, and true/false values. This is where Python programming truly begins to come alive!

Keep practising the examples from this lesson. The more you type code yourself (rather than copy-pasting), the faster your muscle memory and understanding will grow. Every expert programmer started exactly where you are now.

---

*Sources: W3Schools Python Tutorial (python_intro, python_getstarted, python_syntax, python_statements, python_output, python_output_numbers) — https://www.w3schools.com/python/*
