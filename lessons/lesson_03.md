---
render_with_liquid: false
title: "Lesson 03 – Python Output: Printing Text and Numbers"
nav_order: 3
---

# Lesson 03 – Python Output: Printing Text and Numbers

---

## Lesson Introduction

Every program needs a way to **talk back to you** — to show you results, messages, and data. In Python, the tool we use to make the program "speak" is called `print()`.

Think of `print()` like a loudspeaker. You hand it something — a message, a number, a calculation — and it broadcasts it to the screen for you to read.

In this lesson you will learn:
- What the `print()` function is and why it exists
- How to print text (words and sentences)
- How to use single quotes and double quotes correctly
- How to print multiple lines
- How to print on the **same line** instead of separate lines
- How to print numbers
- How to do **math inside** `print()`
- How to mix text and numbers in one single output

By the end of this lesson you will be able to write Python programs that communicate clearly with anyone who runs them.

---

## Prerequisite Concepts

Before we dive in, let us make sure you understand a few small ideas that will make everything else make sense.

### What is a Program?

A program is a set of instructions you give a computer. The computer follows those instructions one step at a time, from top to bottom. When you write `print(...)`, that is one instruction saying: *"Show this on the screen right now."*

### What is a Function?

A **function** is a named tool that does a specific job. You activate a function by writing its name followed by round brackets `()`. Whatever you put inside those brackets is what you are giving to the function to work with.

`print` is a built-in function. Python already knows what it does — you do not have to teach it. You just use it.

### What is Output?

**Output** is anything your program sends to the screen for you to see. When a weather app shows you today's temperature, that is output. When a calculator shows you the answer to a sum, that is output. In Python, `print()` creates output.

---

## Part 1 – Printing Text

### What is Text in Python?

In programming, a piece of text is called a **string**. A string is simply any sequence of characters: letters, spaces, punctuation, numbers written as text, and so on.

**The most important rule:** In Python, text (strings) must always be wrapped inside quotation marks. This tells Python: *"Everything between these marks is just a piece of text — not a command, not a number, just words."*

You can use either:
- **Double quotes** → `"Hello World!"`
- **Single quotes** → `'Hello World!'`

Both work exactly the same way. You only need to pick one style and be consistent within a single string.

---

### Your Very First `print()` Statement

Here is the simplest possible Python output:

```python
print("Hello World!")
```

**Expected Output:**
```
Hello World!
```

Let us break this down character by character so nothing is mysterious:

| Part | What it means |
|---|---|
| `print` | The name of the built-in function that shows things on screen |
| `(` | Opens the function — everything inside here gets given to `print` |
| `"Hello World!"` | The text (string) you want to display, wrapped in double quotes |
| `)` | Closes the function |

When Python reads this line, it does three things: finds the `print` function, reads what is inside the brackets, and immediately displays it on your screen.

---

### Printing Multiple Lines

You can write as many `print()` calls as you want. Each one prints on its own **new line** by default. Python reads and runs them one at a time from top to bottom.

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

Think of each `print()` as pressing Enter on a typewriter. After it finishes one line, it moves the cursor to the start of the next line, ready for whatever comes next.

> 💡 **Thinking Prompt:** What would happen if you changed the order of these three lines? Try it and see — the output will also change order!

---

### Single Quotes vs Double Quotes

Both kinds of quotation marks are completely valid. You can use either one, as long as you open and close with the **same** kind of quote for each string.

```python
print("This will work!")
print('This will also work!')
```

**Expected Output:**
```
This will work!
This will also work!
```

Both lines produce identical results. It is simply a style choice. Many Python programmers use double quotes by habit — but either is fine.

---

### What Happens if You Forget the Quotes?

This is one of the most common beginner mistakes. Watch what happens when you forget to wrap text in quotes:

```python
print(This will cause an error)
```

**Expected Output:**
```
SyntaxError: invalid syntax
```

**Why does this happen?**

When Python sees `This will cause an error` without quotes, it tries to interpret those words as Python commands or variable names — not as text. Since `This`, `will`, `cause`, `an`, and `error` are not valid Python commands or known variables, Python gets confused and throws a `SyntaxError`.

The fix is always simple: add your quotes!

```python
print("This will cause an error")   # ✅ Correct — text is inside quotes
```

**Expected Output:**
```
This will cause an error
```

> ⚠️ **Common Beginner Mistake:** Always remember — text must live inside quotes. Without quotes, Python thinks you are giving it a command, not a piece of text.

---

### Printing Multiple Separate Messages

Let us reinforce the idea of multiple `print()` calls with a second example, this time with a real-world feel:

```python
print("Student Name: Amara")
print("Subject: Mathematics")
print("Score: 87")
```

**Expected Output:**
```
Student Name: Amara
Subject: Mathematics
Score: 87
```

Each `print()` call produces exactly one line of output. Three calls → three lines.

---

## Part 2 – Printing on the Same Line (The `end` Parameter)

By default, `print()` always moves to the **next line** after printing. This is called the **newline behaviour** — it is the default ending of every `print()` statement.

But what if you want two `print()` calls to appear on the same line? Python gives you a special tool for this: the `end` parameter.

### What is a Parameter?

A **parameter** is an extra instruction you can give to a function to change how it behaves. Think of it like ordering food — instead of just saying "give me a burger", you say "give me a burger, but with extra sauce". The `end` parameter is the "extra sauce" instruction for `print()`.

### The Default Ending

Normally, Python automatically adds a special invisible character called `\n` (a newline) at the end of every `print()`. This is what causes the cursor to jump to the next line. When you write:

```python
print("Hello")
print("World")
```

Python secretly does this behind the scenes:
```
Hello\n
World\n
```

The `\n` forces a new line after each message.

### Changing the Ending with `end`

You can override this default by setting `end=" "` (a space) or any other character you prefer.

```python
print("Hello World!", end=" ")
print("I will print on the same line.")
```

**Expected Output:**
```
Hello World! I will print on the same line.
```

Here is what changed: instead of finishing with an invisible newline (`\n`), the first `print()` now finishes with a single space `" "`. So the second `print()` picks up right where the first one left off — on the same line — and they appear joined together.

> 💡 **Notice:** We added a space inside `end=" "` to keep the two messages readable. Without that space, the output would be: `Hello World!I will print on the same line.` — no gap between them!

---

### Experimenting with `end`

You can put any character inside `end`. Here are a few fun variations:

```python
print("Apple", end=", ")
print("Banana", end=", ")
print("Cherry")
```

**Expected Output:**
```
Apple, Banana, Cherry
```

Each `print()` ends with `", "` except the last one, which uses the default newline. This technique is very useful for printing lists of items on a single line.

> 💡 **Thinking Prompt:** What would the output look like if you changed `end=", "` to `end=" | "`? Try it mentally first, then test it!

---

## Part 3 – Printing Numbers

### Numbers Are Different from Text

So far you have been printing text (words and sentences). Python also lets you print **numbers** directly — but there is an important difference: **numbers do not go inside quotes**.

Why? Because putting a number inside quotes would make Python treat it as text, not as an actual number you can calculate with. Compare:

- `"35"` → This is the **text** thirty-five. Python treats it as characters, not a value.
- `35` → This is the **number** thirty-five. Python treats it as a real numeric value.

For now, remember: **numbers go directly inside `print()` without any quotes around them.**

---

### Printing Simple Numbers

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

Each number appears on its own line (because of the default newline ending we learned about). Notice there are no quotes around any of these numbers — they are raw numeric values.

---

### Doing Math Inside `print()`

This is where things get exciting. You can write a **calculation** (called an arithmetic expression) directly inside `print()`, and Python will compute the answer and display it for you.

Think of `print()` as a calculator display — you give it a sum, and it shows you the result.

```python
print(3 + 3)
print(2 * 5)
```

**Expected Output:**
```
6
10
```

Let us understand each line:

**Line 1: `print(3 + 3)`**
- Python first evaluates `3 + 3` → the result is `6`
- Then `print()` displays `6` on the screen

**Line 2: `print(2 * 5)`**
- The `*` symbol in Python means **multiplication**
- Python evaluates `2 * 5` → the result is `10`
- Then `print()` displays `10`

Python always **calculates first, then prints**. You never see the raw formula — only the result.

---

### Common Arithmetic Symbols in Python

Here is a quick reference for the basic math symbols you can use inside `print()`:

| Symbol | Operation | Example | Result |
|---|---|---|---|
| `+` | Addition | `print(10 + 5)` | `15` |
| `-` | Subtraction | `print(10 - 3)` | `7` |
| `*` | Multiplication | `print(4 * 6)` | `24` |
| `/` | Division | `print(15 / 3)` | `5.0` |

> 💡 **Notice:** Division with `/` always gives a decimal answer even if it divides evenly. So `15 / 3` gives `5.0`, not `5`. This is expected Python behaviour — we will explore this more in later lessons on numbers.

---

### More Math Examples

```python
print(100 - 37)
print(8 * 9)
print(20 / 4)
```

**Expected Output:**
```
63
72
5.0
```

> 💡 **Thinking Prompt:** What do you think `print(2 + 3 * 4)` would output? Does Python multiply first, or add first? Think about it — we will explore this concept fully in the lesson on operators!

---

## Part 4 – Mixing Text and Numbers

In real programs, you often want to show a message alongside a number. For example: *"Your score is 95"* — there is both text and a number in that same output.

Python makes this easy. You can combine text and numbers inside a single `print()` by **separating them with a comma**.

### Basic Mix Example

```python
print("I am", 35, "years old.")
```

**Expected Output:**
```
I am 35 years old.
```

Here is what is happening:
- `"I am"` → text (string), shown first
- `,` → a comma tells `print()` to move on to the next item
- `35` → a number, shown in the middle
- `,` → another comma
- `"years old."` → more text, shown last

Python automatically puts a single **space** between each item when you separate them with commas. That is why the output reads naturally as `I am 35 years old.` and not `I am35years old.`

---

### Two More Mix Examples

```python
print("Temperature today:", 28, "degrees Celsius")
```

**Expected Output:**
```
Temperature today: 28 degrees Celsius
```

```python
print("There are", 7, "days in a week and", 24, "hours in a day.")
```

**Expected Output:**
```
There are 7 days in a week and 24 hours in a day.
```

> 💡 **Real-World Connection:** This technique of mixing text and numbers is used constantly in data science, engineering reports, and dashboards. Whenever you see "Server uptime: 99.9%" or "Units sold: 1,427", a developer used exactly this kind of output logic.

---

### Mixing Text with a Calculation

You can even mix text with a math expression in one `print()`:

```python
print("The result of 12 times 5 is", 12 * 5)
```

**Expected Output:**
```
The result of 12 times 5 is 60
```

Python calculates `12 * 5` first (giving `60`), then combines it with the text and prints the whole thing together.

---

## Guided Practice Exercises

Work through these exercises one by one. Each one builds on the previous. Try to predict the output before you run the code!

---

### Exercise 1 – Print a Simple Greeting

**Objective:** Practice writing your first `print()` statements.

**Scenario:** A school registration system needs to display a welcome message when students log in.

**Steps:**
1. Print the text: `Welcome to Python School!`
2. Print the text: `Please follow the instructions carefully.`
3. Print the text: `Good luck and have fun!`

**Your Code:**
```python
print("Welcome to Python School!")
print("Please follow the instructions carefully.")
print("Good luck and have fun!")
```

**Expected Output:**
```
Welcome to Python School!
Please follow the instructions carefully.
Good luck and have fun!
```

**Self-check Questions:**
- Did each message appear on its own line?
- What would happen if you removed one `print()` line?
- What would happen if you accidentally removed the closing quote?

---

### Exercise 2 – Fix the Broken Code

**Objective:** Identify and correct common beginner mistakes.

**Scenario:** A student wrote this code, but it has errors. Find and fix all the mistakes.

**Broken Code:**
```python
print(Hello, my name is Chukwuemeka!)
print('I am learning Python")
print(25)
print("My score is 98)
```

**Identified Mistakes:**
1. Line 1: Text is not inside quotes at all → `Hello, my name is Chukwuemeka!`
2. Line 2: Opening single quote `'` but closing double quote `"` — mismatched!
3. Line 3: This is actually correct! `25` is a number and does not need quotes.
4. Line 4: Missing closing quote before the `)` — string is not properly closed.

**Fixed Code:**
```python
print("Hello, my name is Chukwuemeka!")
print('I am learning Python')
print(25)
print("My score is 98")
```

**Expected Output:**
```
Hello, my name is Chukwuemeka!
I am learning Python
25
My score is 98
```

---

### Exercise 3 – A Mini Student Report

**Objective:** Practice mixing text and numbers in output.

**Scenario:** You are building a simple student report printer. Display the following information for a student named Fatima.

**Requirements:**
- Name: Fatima
- Age: 14
- English Score: 82
- Maths Score: 91
- Average: (82 + 91) / 2 = 86.5 (let Python calculate this for you!)

**Your Code:**
```python
print("Student Name: Fatima")
print("Age:", 14)
print("English Score:", 82)
print("Maths Score:", 91)
print("Average Score:", (82 + 91) / 2)
```

**Expected Output:**
```
Student Name: Fatima
Age: 14
English Score: 82
Maths Score: 91
Average Score: 86.5
```

**What to Notice:**
- `(82 + 91) / 2` is a calculation — Python works it out before printing
- The brackets `()` around `82 + 91` make sure addition happens before division
- The result `86.5` is a decimal number — that is fine and expected

**Self-check Questions:**
- What happens if you write `print("Average Score:", 82 + 91 / 2)` without the brackets around `82 + 91`? Try it — the answer will be different!
- Why does Python put a space between `"Age:"` and `14` automatically?

---

### Exercise 4 – Same-Line Output Challenge

**Objective:** Practice using the `end` parameter to control line breaks.

**Scenario:** A shop checkout system needs to print item names all on one line, separated by arrows.

**Your Code:**
```python
print("Rice", end=" → ")
print("Beans", end=" → ")
print("Oil", end=" → ")
print("Sugar")
```

**Expected Output:**
```
Rice → Beans → Oil → Sugar
```

**What-if Challenge:** What would the output be if you changed all `end=" → "` to `end="\n"`? Think first — then test it!

---

### Exercise 5 – A Simple Budget Calculator

**Objective:** Use math operations inside `print()` to build a mini budget tool.

**Scenario:** A market trader wants to calculate daily profits. Sales today were ₦15,000. Costs were ₦9,500. Help them see their profit, and their profit doubled if they had two stalls.

**Your Code:**
```python
print("Sales Today:", 15000)
print("Costs Today:", 9500)
print("Profit:", 15000 - 9500)
print("Profit with Two Stalls:", (15000 - 9500) * 2)
```

**Expected Output:**
```
Sales Today: 15000
Costs Today: 9500
Profit: 5500
Profit with Two Stalls: 11000
```

**Self-check Questions:**
- Why did we put brackets around `(15000 - 9500)` before multiplying by 2?
- What would happen if we wrote `print("Profit:", 15000 - 9500 * 2)` instead?

---

## Mini Project – Python Personal Profile Card

Now let us combine everything you have learned into one small, complete project. You will build a **Personal Profile Card** that displays all your key information cleanly.

### Project Goal

Create a Python program that displays a formatted profile card for a fictional person — like the kind of output a student management system, an employee database, or a social app might produce.

---

### Stage 1 – Setup: Display a Header

First, let us create a visible section divider to make the output look clean.

```python
print("============================")
print("     STUDENT PROFILE CARD   ")
print("============================")
```

**Expected Output:**
```
============================
     STUDENT PROFILE CARD   
============================
```

The `=` signs are just regular text characters inside a string — we are printing them to create a visual border.

---

### Stage 2 – Core Information

Now add the student's personal details. Mix text labels with numbers where appropriate.

```python
print("Name:    Adaeze Okonkwo")
print("Age:    ", 16)
print("School:  Lagos Future Academy")
print("Class:   Year 10")
```

**Expected Output:**
```
Name:    Adaeze Okonkwo
Age:     16
School:  Lagos Future Academy
Class:   Year 10
```

> 💡 **Design tip:** We added extra spaces after the labels like `"Age:    "` to make the values line up neatly. This is a simple way to improve readability.

---

### Stage 3 – Academic Scores and Calculated Average

Now display her subject scores and have Python calculate her average automatically.

```python
print("----------------------------")
print("         EXAM SCORES        ")
print("----------------------------")
print("English:     ", 85)
print("Mathematics: ", 91)
print("Science:     ", 78)
print("History:     ", 83)
print("----------------------------")
print("Average Score:", (85 + 91 + 78 + 83) / 4)
```

**Expected Output:**
```
----------------------------
         EXAM SCORES        
----------------------------
English:      85
Mathematics:  91
Science:      78
History:      83
----------------------------
Average Score: 84.25
```

Python calculates `(85 + 91 + 78 + 83) / 4` = `337 / 4` = `84.25` automatically. You did not have to work that out yourself — the program did!

---

### Stage 4 – Footer and Complete Program

Finish with a motivational footer and combine all stages into your final program.

```python
print("============================")
print("     STUDENT PROFILE CARD   ")
print("============================")
print("Name:    Adaeze Okonkwo")
print("Age:    ", 16)
print("School:  Lagos Future Academy")
print("Class:   Year 10")
print("----------------------------")
print("         EXAM SCORES        ")
print("----------------------------")
print("English:     ", 85)
print("Mathematics: ", 91)
print("Science:     ", 78)
print("History:     ", 83)
print("----------------------------")
print("Average Score:", (85 + 91 + 78 + 83) / 4)
print("============================")
print("Keep up the excellent work!")
print("============================")
```

**Expected Output:**
```
============================
     STUDENT PROFILE CARD   
============================
Name:    Adaeze Okonkwo
Age:     16
School:  Lagos Future Academy
Class:   Year 10
----------------------------
         EXAM SCORES        
----------------------------
English:      85
Mathematics:  91
Science:      78
History:      83
----------------------------
Average Score: 84.25
============================
Keep up the excellent work!
============================
```

---

### Milestone Reflection

Pause and think about what you just built:

- You wrote a multi-section program that produces structured, readable output
- You used `print()` to display both text and numbers
- You let Python calculate the average automatically — no manual arithmetic needed
- You used visual dividers made of `=` and `-` characters to make the output look professional

---

### Optional Extensions

Want to push further? Try these additions on your own:

1. Add a `"Pass"` or `"Fail"` message using what you currently know (hint: just add a `print("Pass")` line for now — we will learn to make this automatic using conditions in a future lesson)
2. Add a fifth subject and recalculate the average
3. Use `end=" | "` to print all four subject names on a single line before showing their scores

---

## Common Beginner Mistakes

Here is a handy reference of the mistakes beginners most often make in this topic, along with how to fix them.

---

### Mistake 1 – Forgetting Quotes Around Text

**Wrong:**
```python
print(Hello World)
```
**Error:** `SyntaxError: invalid syntax`

**Right:**
```python
print("Hello World")
```

**Why:** Python needs quotes to know where text begins and ends. Without them, it tries to interpret the words as code — and fails.

---

### Mistake 2 – Mismatching Quotes

**Wrong:**
```python
print("Hello World')
```
**Error:** `SyntaxError: EOL while scanning string literal`

**Right:**
```python
print("Hello World")
# or
print('Hello World')
```

**Why:** Every string must open and close with the **same** type of quote. Mixing them confuses Python.

---

### Mistake 3 – Putting Numbers in Quotes When You Want to Calculate

**Wrong (for math purposes):**
```python
print("3 + 3")
```
**Output:** `3 + 3`  ← Python prints it as-is text, no calculation happens!

**Right:**
```python
print(3 + 3)
```
**Output:** `6`  ← Python calculates and prints the result

**Why:** Quotes turn everything inside them into plain text. A number inside quotes is just the character "3", not the mathematical value 3.

---

### Mistake 4 – Missing the Closing Parenthesis

**Wrong:**
```python
print("Hello World!"
```
**Error:** `SyntaxError: unexpected EOF while parsing`

**Right:**
```python
print("Hello World!")
```

**Why:** Every `print(` must be closed with a matching `)`. Think of them like a pair of hands — they always come together.

---

### Mistake 5 – Forgetting the Space in `end=" "`

**Wrong (no space between printed items):**
```python
print("Hello", end="")
print("World")
```
**Output:** `HelloWorld`

**Right:**
```python
print("Hello", end=" ")
print("World")
```
**Output:** `Hello World`

**Why:** When using `end`, Python does not add any space automatically. You must include whatever separator you want inside the `end` value.

---

### Mistake 6 – Using `*` to Mean "to the power of" (It Does Not!)

**Wrong assumption:**
```python
print(2 * 2)   # Thinking this means 2 squared = 4... by accident it is correct!
print(2 * 3)   # But thinking this means 2³... NO, this is 2×3 = 6, not 8
```

**Right for powers (we will cover this in numbers lesson):**
```python
print(2 ** 3)  # This means 2 to the power of 3 = 8
```

**Why:** In Python, `*` is multiply. `**` is the exponent (power) operator. This is a very common point of confusion for beginners coming from maths notation.

---

## Reflection Questions

Take a moment to think through these questions. You do not need to write code — just think!

1. Why does Python need quotation marks around text, but not around numbers?
2. If you write `print("100 + 200")`, what will Python display? Why?
3. What is the difference between `print("Hello", "World")` and `print("Hello World")`?
4. You want to print a shopping receipt with three items on separate lines. How many `print()` calls do you need?
5. A friend says: "I want to show the result of 5 times 12 on screen." What single line of Python code would you write?
6. What does the `end` parameter do, and when is it useful?
7. If you want all your output on one single line separated by dashes, what value would you set `end` to?

---

## Completion Checklist

Before you move on, check that you can confidently do all of the following:

- [ ] Write a `print()` statement that displays text on the screen
- [ ] Use both double quotes and single quotes correctly
- [ ] Write multiple `print()` calls to display multiple lines
- [ ] Understand why Python gives a `SyntaxError` when quotes are missing or mismatched
- [ ] Use the `end` parameter to print on the same line
- [ ] Print a number directly (without quotes)
- [ ] Write a math expression inside `print()` and get the calculated result
- [ ] Mix text and numbers in one `print()` using commas
- [ ] Identify and fix common beginner mistakes related to output
- [ ] Build a simple multi-line formatted output like a profile card

---

## Lesson Summary

Here is everything you learned in this lesson, presented as a quick reference:

**The `print()` function** is Python's main tool for displaying output. It can print text, numbers, calculations, and combinations of all three.

**Printing text** requires wrapping your text in either double quotes `"..."` or single quotes `'...'`. Both work identically. Forgetting the quotes causes a `SyntaxError`.

**Multiple `print()` calls** each start a new line by default. Three `print()` calls produce three lines.

**The `end` parameter** lets you change what goes at the end of a `print()` statement. Setting `end=" "` keeps the next output on the same line with a space separator.

**Printing numbers** is done by placing the number directly inside `print()` — no quotes needed. Numbers inside quotes become text and cannot be calculated.

**Math inside `print()`** is fully supported. Python always evaluates the calculation first and then displays the result.

**Mixing text and numbers** is done with commas inside `print()`. Python automatically adds a space between each comma-separated item.

```python
# Quick Reference Examples

print("Hello World!")                        # Print text
print('Single quotes work too!')             # Single quotes
print("Line 1")                              # Multiple lines
print("Line 2")

print("Same line", end=" ")                  # Same-line printing
print("continued here")

print(42)                                    # Print a number
print(10 + 5)                               # Print result of a calculation
print(3 * 7)                                # Multiplication

print("I am", 25, "years old")              # Mix text and number
print("Total:", 100 + 200)                  # Mix text and a calculation
```

**Expected Output of the above:**
```
Hello World!
Single quotes work too!
Line 1
Line 2
Same line continued here
42
15
21
I am 25 years old
Total: 300
```

---

> 🎉 **Congratulations!** You have completed Lesson 03. You now know how to make Python communicate — and that is the foundation of every program ever written. In the next lesson, you will learn about **Python Comments** — how to leave notes in your code that Python ignores but humans find helpful!
