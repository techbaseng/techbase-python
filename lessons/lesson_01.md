---
render_with_liquid: false
title: "Lesson 01 — Introduction to Python & Getting Started"
nav_order: 1
---

# Lesson 01 — Introduction to Python & Getting Started

---

## Lesson Introduction

Welcome to your very first Python lesson! 🎉

You are about to learn one of the most popular, beginner-friendly, and powerful programming languages in the world. Python is used every single day by students, engineers, scientists, data analysts, web developers, and AI researchers all over the world — including here in Nigeria and across Africa.

By the end of this lesson you will:

- Understand what Python is and why it was created
- Know what Python is used for in the real world
- Have Python installed and running on your computer (or use it directly in your browser — no install needed!)
- Have written and successfully run your very first Python program
- Understand how Python differs from other programming languages

This lesson is designed for **absolute beginners**. You do not need to know anything at all about programming before reading this. Every word, every symbol, every concept will be explained clearly.

---

## Prerequisite Concepts

Before we dive into Python itself, let us make sure we understand a few everyday ideas that will make this lesson much easier.

### What is a Programming Language?

Think of a programming language as a set of instructions you give to a computer. A computer cannot understand human language like English or Yoruba on its own. It only understands a very low-level language made of 0s and 1s (called "binary"). Programming languages like Python are the **bridge** between human thinking and computer action.

**Analogy:** Imagine you want to teach a robot to make jollof rice. You cannot just say "make jollof rice" — the robot needs very specific, step-by-step instructions: "Add 2 cups of rice. Add 1 litre of tomato sauce. Set the temperature to 180 degrees." A programming language lets you write those precise instructions for a computer.

### What is a Program?

A program is simply a list of instructions that a computer follows from top to bottom, one step at a time. Python programs are text files that you write, and then Python reads and carries them out.

### What is a Syntax?

Just like English has grammar rules (capital letters at the start of sentences, full stops at the end), programming languages have **syntax** rules — the rules that say how code must be written so the computer can understand it. We will explore Python's syntax in this lesson.

---

## Part 1 — What is Python?

### A Brief History

Python was created by a Dutch programmer named **Guido van Rossum**. He started working on it in the late 1980s and released the first version in **1991**. The name "Python" was not inspired by a snake — Guido was a fan of the British comedy group *Monty Python's Flying Circus* and wanted a name that was short and a little bit fun.

Python was designed with one core idea in mind: **code should be easy to read and write**. Guido wanted a language that looked almost like reading plain English.

### What is Python Used For?

Python is incredibly versatile. Here are the main areas where Python is used today:

**1. Web Development (Server-Side)**
Large websites and web apps use Python on the back end (the part you do not see). Platforms like Instagram, Pinterest, and Dropbox are built with Python.

**2. Software Development**
Python is used to build tools, automation scripts, and standalone software programs.

**3. Data Science and Mathematics**
Scientists, engineers, and analysts use Python to crunch numbers, analyse large datasets, draw graphs, and run statistical models. This is one of the most popular uses of Python in universities and research centres.

**4. Machine Learning and Artificial Intelligence**
Python is the dominant language for AI research. Tools like TensorFlow, PyTorch, and Scikit-learn — all used for training AI models — are Python libraries.

**5. System Scripting and Automation**
Python can automate repetitive tasks. For example, automatically renaming 1,000 files, sending scheduled emails, or scraping information from websites.

**6. Database Interaction**
Python can connect to databases (like MySQL or MongoDB), read data from them, and write new data into them.

**7. Rapid Prototyping**
Because Python is quick to write, many developers use it to build a working "draft" of an idea before implementing it in another language.

> **Real-world tip:** If you are studying Engineering, Biology, Economics, or any STEM subject, Python can help you analyse experimental data, build simulations, and create charts — skills that are increasingly required in the job market.

---

## Part 2 — Why Python? (The Big Advantages)

Let us look at why Python has become one of the most popular languages in the world.

### 1. It Works on Every Platform

Python runs on Windows, Mac, Linux, Raspberry Pi, and many other systems. Write your code once, run it anywhere.

### 2. Simple Syntax That Looks Like English

Compare these two programs that do the same thing — printing "Hello" five times:

**In Java (another popular language):**

```java
public class Hello {
    public static void main(String[] args) {
        for (int i = 0; i < 5; i++) {
            System.out.println("Hello");
        }
    }
}
```

**In Python:**

```python
for i in range(5):
    print("Hello")
```

Python does the same job in far fewer lines. Notice how the Python version almost reads like English: "for i in range 5, print Hello."

### 3. Fewer Lines of Code

Python allows you to accomplish complex tasks with much less writing. This means less chance of making mistakes and faster development.

### 4. Immediate Execution (Interpreted Language)

Python is an **interpreted** language. This is an important concept.

- **Compiled languages** (like C or Java) must be fully translated into machine code before running. This is like translating an entire book before reading it.
- **Interpreted languages** (like Python) are translated and run **line by line**, one instruction at a time. This is like reading and translating a book sentence by sentence as you go.

The advantage? You can test and run your code almost instantly. You do not have to wait for a full compilation step. This makes experimenting and learning very fast.

### 5. Multiple Programming Styles

Python supports three main ways of organising your code:

- **Procedural** — writing step-by-step instructions (what we will start with)
- **Object-Oriented** — organising code into objects that have properties and behaviours (more advanced)
- **Functional** — treating code as a series of mathematical functions (advanced)

Do not worry about understanding all three right now. We start procedural, and everything else will come naturally.

### 6. A Huge Community and Ecosystem

Millions of developers use Python. This means there are countless free libraries (ready-made tools), endless tutorials, and a huge community ready to help you when you get stuck.

---

## Part 3 — Python Syntax: How Python Looks Different

### Python Uses Indentation to Define Structure

Most programming languages use **curly brackets `{}`** to show where a block of code begins and ends. Python does it differently — it uses **indentation** (spaces or tabs at the start of a line).

**Indentation** simply means the empty space at the beginning of a line. In Python, this space is not just for looks — it is part of the language itself.

**Example — using indentation:**

```python
if 5 > 3:
    print("Five is greater than three")
```

**Expected Output:**
```
Five is greater than three
```

The `print` line is indented (moved inward) because it is *inside* the `if` block. Python uses this to know which lines belong together.

**What happens if you forget the indentation?**

```python
if 5 > 3:
print("Five is greater than three")   # ← No indentation — this will CRASH
```

**Output (error):**
```
IndentationError: expected an indented block after 'if' statement
```

> **Key takeaway:** Always indent consistently in Python. Use 4 spaces per level (this is the standard).

### Python Uses New Lines to End Commands

In many other languages, each command must end with a semicolon `;`. Not in Python. A new line is enough.

**Python:**
```python
print("Hello")
print("World")
```

**A language like JavaScript:**
```javascript
console.log("Hello");
console.log("World");
```

Both do the same thing, but Python is cleaner.

### Python is Case-Sensitive

This is very important. `print` and `Print` and `PRINT` are completely different things in Python. The built-in function is only recognised as `print` (all lowercase).

```python
print("This works!")    # ✅ Correct
Print("This crashes!")  # ❌ Will give an error — capital P
```

---

## Part 4 — Getting Started with Python

Now that you understand what Python is, let us get it up and running!

### Option A — Use Python Directly in Your Browser (No Installation Needed)

The fastest way to start is to use an **online Python editor**. You do not need to install anything on your computer. Just visit:

👉 [https://www.w3schools.com/python/trypython.asp](https://www.w3schools.com/python/trypython.asp)

This editor lets you type Python code and run it instantly. We will use this approach for all the examples in this lesson.

### Option B — Install Python on Your Computer

If you want to run Python on your own machine, follow these steps.

#### Step 1 — Check if Python is Already Installed

Many computers already have Python! Let us check.

**On Windows:**
1. Press the Windows key, type `cmd`, and press Enter to open the Command Prompt.
2. Type the following command and press Enter:

```
python --version
```

**On Mac or Linux:**
1. Open the Terminal application.
2. Type:

```
python --version
```

**Expected Output (if Python is installed):**
```
Python 3.12.0
```

(The exact version number may differ, but any version starting with `3.` is fine.)

**If you see "command not found" or "Python is not recognized":**
Python is not installed. Go to Step 2.

#### Step 2 — Download and Install Python

1. Go to the official Python website: [https://www.python.org/](https://www.python.org/)
2. Click the big yellow **"Download Python"** button.
3. Run the installer file that downloads.
4. **IMPORTANT (Windows only):** During installation, tick the checkbox that says **"Add Python to PATH"** before clicking Install. This is very important — without it, Python will not be found by the command line.
5. Click "Install Now" and wait for it to finish.

After installation, repeat the `python --version` check from Step 1 to confirm it worked.

#### Step 3 — Choose Where to Write Python Code

You write Python code in a plain text file with a `.py` extension. You can use:

- **Notepad** (Windows) — built-in, simple, no colour coding
- **TextEdit** (Mac) — built-in but make sure to save as plain text
- **VS Code** — free, powerful, shows errors in real time (recommended): [https://code.visualstudio.com/](https://code.visualstudio.com/)
- **Thonny** — free, designed specifically for Python beginners: [https://thonny.org/](https://thonny.org/)
- **PyCharm** — professional-grade Python IDE, free community edition available

> **Beginner recommendation:** Start with Thonny. It is the simplest to set up and use.

---

## Part 5 — Your First Python Program

### The Classic "Hello, World!"

By tradition, the very first program every programmer writes in a new language is one that displays the words "Hello, World!" on the screen. It sounds simple, but it is a powerful moment — it is proof that your setup works and that you are officially a programmer.

Let us write it.

**Code:**

```python
print("Hello, World!")
```

**Expected Output:**
```
Hello, World!
```

That's it! One line. Let us break it down completely.

#### Line-by-Line Explanation

| Part | What it is | What it does |
|------|-----------|--------------|
| `print` | A **built-in function** | Tells Python to display something on the screen |
| `(` | Opening **parenthesis** | Marks the start of what we want to print |
| `"Hello, World!"` | A **string** (text) | The text we want to display, wrapped in quotation marks |
| `)` | Closing **parenthesis** | Marks the end of what we want to print |

**What is a function?** Think of a function like a machine. You feed something into it (the input), and it does a job and gives you a result. `print` is Python's built-in "display machine" — you feed it text, and it puts that text on the screen.

**What are quotation marks for?** In Python, any text (called a **string**) must be wrapped in quotation marks so that Python knows it is text and not a command. You can use either single quotes `'Hello, World!'` or double quotes `"Hello, World!"` — both work the same way.

```python
print("Hello, World!")   # Using double quotes
print('Hello, World!')   # Using single quotes — same result!
```

**Expected Output (both lines):**
```
Hello, World!
Hello, World!
```

> **Thinking prompt:** What do you think happens if you remove the quotation marks? Try it!

---

### Running Your First Program — Step by Step

#### Method 1: Using the Online Editor

1. Go to [https://www.w3schools.com/python/trypython.asp](https://www.w3schools.com/python/trypython.asp)
2. You will see a code box on the left and a result box on the right.
3. Clear whatever is there and type: `print("Hello, World!")`
4. Click the "Run" button.
5. You should see `Hello, World!` appear in the result box.

#### Method 2: Using a File on Your Computer

1. Open Notepad (or any text editor).
2. Type: `print("Hello, World!")`
3. Save the file as `hello.py` (not `hello.py.txt` — make sure the extension is `.py`).
4. Open your Command Prompt or Terminal.
5. Navigate to the folder where you saved the file. For example, if it is on your Desktop:

**Windows:**
```
cd Desktop
```

**Mac/Linux:**
```
cd ~/Desktop
```

6. Run the file by typing:
```
python hello.py
```

7. Press Enter. You should see:
```
Hello, World!
```

🎉 Congratulations — you just ran your first Python program!

#### Method 3: Using the Python Interactive Command Line

Python has a special interactive mode where you can type commands and see results immediately — no file needed. Think of it as a live conversation with Python.

To open it:

**Windows:**
```
python
```

(If `python` does not work, try `py` instead.)

**Mac/Linux:**
```
python3
```

You will see something like this:

```
Python 3.12.0 (main, Oct 2 2023, 00:00:00)
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

The `>>>` symbol means Python is ready and waiting for your instruction. Type your command and press Enter:

```
>>> print("Hello, World!")
Hello, World!
>>>
```

Python immediately shows the result! This is a great way to experiment with small pieces of code.

To exit the interactive mode, type:
```
>>> exit()
```

And press Enter.

---

## Part 6 — Checking Your Python Version in Code

Sometimes you need to know which version of Python is running your code. Here is how to check it from inside a Python program:

```python
import sys

print(sys.version)
```

**Expected Output (example — your version may differ):**
```
3.12.0 (main, Oct 2 2023, 00:00:00) [MSC v.1900 64 bit (AMD64)]
```

**Line-by-line explanation:**

- `import sys` — This loads a built-in Python **module** called `sys`. A module is like a toolbox of extra features. The word `import` means "bring this toolbox into my program so I can use it."
- `sys.version` — This accesses the `version` information stored inside the `sys` module. Think of it like opening the toolbox and picking out the tool labelled `version`.
- `print(sys.version)` — Displays that version information on the screen.

Do not worry about fully understanding `import` right now — we cover modules in detail in a later lesson. The important thing is that you can run this code and see your Python version.

> **Why does the version matter?** This tutorial uses Python 3. Python 2 (an older version) works differently in some areas and is no longer actively developed. Always make sure you are using Python 3.

---

## Guided Practice Exercises

Now it is time to practise! These exercises help you build confidence by applying what you have just learned.

---

### Exercise 1 — Your First Print Statement

**Objective:** Print your own name and a greeting message.

**Scenario:** Imagine you are writing a program that introduces itself to the user.

**Steps:**
1. Open the online editor or your text editor.
2. Write a Python program that prints two lines:
   - Your name
   - The message: "Welcome to Python!"

**Hints:**
- Use `print()` twice, once on each line.
- Wrap your text in quotation marks.
- Each `print()` call goes on its own line.

**Expected Output (example for a person named Amara):**
```
Amara
Welcome to Python!
```

**Self-check Questions:**
- Did both lines print correctly?
- What happens if you put both texts in one `print()` — separated by a comma?
- What happens if you remove the quotation marks from one of them?

---

### Exercise 2 — Multiple Print Statements

**Objective:** Display a short poem or story using multiple print statements.

**Scenario:** You are building a simple text-based storybook program.

**Steps:**
1. Write a Python program with at least 4 `print()` statements.
2. Each `print()` should contain one sentence of a short story about yourself.

**Example:**
```python
print("My name is Emeka.")
print("I live in Ibadan, Nigeria.")
print("I am learning Python.")
print("One day I will build great software.")
```

**Expected Output:**
```
My name is Emeka.
I live in Ibadan, Nigeria.
I am learning Python.
One day I will build great software.
```

**What-if challenge:** What happens if you add an empty `print()` (with nothing inside the brackets)? Try it and observe the output.

---

### Exercise 3 — Checking Python Version

**Objective:** Write a program that imports `sys` and displays the Python version.

**Steps:**
1. Write a program with `import sys` on the first line.
2. On the second line, print the version.

**Expected Output (example):**
```
3.12.0 (main, Oct 2 2023, ...)
```

**Self-check:** What does the number after `Python` tell you?

---

## Mini Project — Personal Introduction Card

Now let us combine everything from this lesson into a small but satisfying project!

### Project: Your Python Profile Card

**Goal:** Build a program that acts like a personal introduction card — it prints your name, location, what you are studying, and why you are learning Python.

**Stage 1 — Setup**

Create a new file called `profile_card.py`.

**Stage 2 — Core Logic**

Write print statements that display each piece of information. Add a decorative line of dashes to make it look like a card.

```python
print("========================================")
print("           MY PYTHON PROFILE CARD       ")
print("========================================")
print("Name    : Adaeze Okonkwo")
print("City    : Ibadan, Nigeria")
print("Course  : Computer Science, Year 1")
print("Goal    : To build apps that help people")
print("Motto   : Start small. Think big.")
print("========================================")
```

**Milestone Output:**
```
========================================
           MY PYTHON PROFILE CARD       
========================================
Name    : Adaeze Okonkwo
City    : Ibadan, Nigeria
Course  : Computer Science, Year 1
Goal    : To build apps that help people
Motto   : Start small. Think big.
========================================
```

**Stage 3 — Enhancement**

Add one more section below the card that prints today's date using Python's built-in `datetime` module (just copy this for now — we cover it in a later lesson):

```python
import datetime
print("Date    :", datetime.date.today())
```

**Stage 4 — Final Output**

Run the complete program. Your final output should look like a proper card with your real information filled in.

**Reflection Questions:**
- How does changing the number of `=` signs affect the look?
- What else could you add to your profile card?
- How could this idea be extended to a simple contact book?

**Optional Advanced Extension:** Try printing the card in a different language for the label names (e.g., use Yoruba or Igbo labels like `Orukọ :` for "Name").

---

## Common Beginner Mistakes

Here are the most common mistakes beginners make in their very first Python programs — along with the corrected versions.

---

### Mistake 1 — Forgetting Quotation Marks

**Wrong:**
```python
print(Hello, World!)
```

**Error:**
```
SyntaxError: invalid syntax
```

**Why it fails:** Python thinks `Hello` is a variable name or command, not text. Text must always be in quotes.

**Correct:**
```python
print("Hello, World!")
```

---

### Mistake 2 — Using the Wrong Case for `print`

**Wrong:**
```python
Print("Hello, World!")
```

**Error:**
```
NameError: name 'Print' is not defined
```

**Why it fails:** Python is case-sensitive. The function is `print`, not `Print` or `PRINT`.

**Correct:**
```python
print("Hello, World!")
```

---

### Mistake 3 — Missing the Closing Parenthesis

**Wrong:**
```python
print("Hello, World!"
```

**Error:**
```
SyntaxError: '(' was never closed
```

**Why it fails:** Every opening `(` must have a matching closing `)`.

**Correct:**
```python
print("Hello, World!")
```

---

### Mistake 4 — Mixing Single and Double Quotes

**Wrong:**
```python
print("Hello, World!')
```

**Error:**
```
SyntaxError: EOL while scanning string literal
```

**Why it fails:** You opened with double quotes `"` but tried to close with a single quote `'`. They must match.

**Correct — either of these:**
```python
print("Hello, World!")    # Both double
print('Hello, World!')    # Both single
```

---

### Mistake 5 — Adding Extra Spaces Before `print` at the Top Level

**Wrong:**
```python
    print("Hello, World!")
```

**Error:**
```
IndentationError: unexpected indent
```

**Why it fails:** The very first line of a simple Python program should not be indented. Indentation is only used inside blocks like `if`, `for`, and functions.

**Correct:**
```python
print("Hello, World!")
```

---

### Mistake 6 — Saving the File Without the `.py` Extension

If you save your file as `hello.txt` instead of `hello.py`, running `python hello.txt` may work in some setups but is bad practice. The `.py` extension tells editors and the system that this is a Python file.

**Always name your files:** `something.py`

---

## Reflection Questions

Take a moment to think about these questions. Try to answer them in your own words — this will solidify your understanding.

1. In your own words, what is Python? Who created it and when?
2. Name three things Python can be used for in the real world.
3. What does "interpreted language" mean? How is it different from a compiled language?
4. Why does Python use indentation instead of curly brackets?
5. What does the `print()` function do? What would happen if Python did not have it?
6. Why must text be wrapped in quotation marks in Python?
7. If you type `Print("Hello")` in Python, what happens and why?
8. What is the difference between running Python interactively (`>>>`) and running a `.py` file?
9. Why is Python popular for data science and artificial intelligence?
10. What is the significance of the `import` keyword? (Think of an analogy.)

---

## Completion Checklist

Use this checklist to confirm you have mastered Lesson 01. Tick each item only when you can do it comfortably without looking at notes.

- [ ] I can explain what Python is in simple terms.
- [ ] I can name at least 4 real-world uses of Python.
- [ ] I can explain what an interpreted language is.
- [ ] I know why Python uses indentation and what happens when you forget it.
- [ ] I can check whether Python is installed on my computer.
- [ ] I can install Python from the official website.
- [ ] I have successfully written and run `print("Hello, World!")`.
- [ ] I understand what quotation marks do in a `print()` statement.
- [ ] I can explain why `Print("Hello")` causes an error.
- [ ] I can use the Python interactive command line (`>>>`).
- [ ] I can check my Python version using `import sys`.
- [ ] I have completed all three practice exercises.
- [ ] I have built and run my Personal Introduction Card mini project.
- [ ] I can describe at least 5 common beginner mistakes and their fixes.
- [ ] I have answered the reflection questions in my own words.

---

## Lesson Summary

Here is everything you learned in Lesson 01, summarised clearly.

**What Python is:** Python is a high-level, interpreted programming language created by Guido van Rossum and released in 1991. It is designed to be readable and concise.

**What Python does:** It is used for web development, data science, machine learning, automation, database work, software development, and rapid prototyping.

**Why Python is special:**
- Works on Windows, Mac, and Linux.
- Has simple, English-like syntax.
- Uses fewer lines of code than most other languages.
- Is interpreted — runs immediately, line by line.
- Supports procedural, object-oriented, and functional programming styles.

**Key syntax rules:**
- Python uses **indentation** (spaces) to define code blocks — not curly brackets.
- Python uses **new lines** to end statements — not semicolons.
- Python is **case-sensitive** — `print` is not the same as `Print`.
- Text (strings) must always be wrapped in **matching quotation marks**.

**Your first program:**
```python
print("Hello, World!")
```
Output: `Hello, World!`

**Three ways to run Python:**
1. An online editor (browser-based, no install needed).
2. A `.py` file run from the command line: `python hello.py`
3. The Python interactive shell: type `python` in the terminal.

**Checking your Python version:**
```python
import sys
print(sys.version)
```

---

> **What comes next?** In Lesson 02, we will explore Python Syntax in depth — how to write proper Python statements, use comments to add notes in your code, and start working with variables (containers for storing information). Keep going — you are off to a great start!

---

*Sources: W3Schools Python Tutorial — [python/default.asp](https://www.w3schools.com/python/default.asp), [python/python_intro.asp](https://www.w3schools.com/python/python_intro.asp), [python/python_getstarted.asp](https://www.w3schools.com/python/python_getstarted.asp)*
