---
title: "Lesson 01 – Introduction to Python"
nav_order: 1
---

# Lesson 01 — Introduction to Python

**Course:** Python Programming · Techbase STEM Academy  
**Instructor:** Babatunde Awolaja — [Techbase Consultant Services](https://techbasengr.com.ng)

---

## 🎯 Learning Objectives

By the end of this lesson you will be able to:

- [ ] Explain what Python is and why it is popular
- [ ] Set up Python on your computer (or use an online editor)
- [ ] Write and run your very first Python program
- [ ] Understand what `print()` does and how to use it

---

## 1. What is Python?

Python is a **programming language** — a way of giving instructions to a computer so it can carry out tasks for you.

Python was created in 1991 by Guido van Rossum. Today it is used by:

- **Data scientists** analysing weather, agriculture, and satellite data
- **Web developers** building websites and APIs
- **Automation engineers** writing scripts that handle repetitive tasks
- **Students and teachers** all over Nigeria and around the world

Python is popular because its code reads almost like plain English, which makes it one of the easiest languages to learn as a beginner.

---

## 2. Setting Up Python

### Option A — Online (Recommended for Beginners)

No installation needed. Go to one of these free sites and start coding immediately:

- 🌐 [Replit](https://replit.com/new/python3) — create a free account and choose Python
- 🌐 [Python Tutor](https://pythontutor.com/python-debugger.html) — paste code and see it run step by step

### Option B — Install Locally

1. Go to [python.org/downloads](https://www.python.org/downloads/)
2. Download **Python 3.x** (the latest version)
3. During installation on Windows, check ✅ **"Add Python to PATH"**
4. Open your terminal or Command Prompt and type:

```bash
python --version
```

If you see something like `Python 3.11.4` you are ready to go. ✅

---

## 3. Your First Program

Open your editor (Replit or VS Code) and type this exactly:

```python
print("Hello, World!")
```

Click **Run**. You should see:

```
Hello, World!
```

🎉 **Congratulations — you just wrote your first Python program!**

---

## 4. What is `print()`?

`print()` is a **built-in function** — a ready-made command that tells Python to display something on the screen.

Whatever you put inside the brackets and inside quotation marks will be shown as output:

```python
print("Hello from Ibadan!")
print("Welcome to Techbase STEM Academy")
print("Python is fun!")
```

**Output:**
```
Hello from Ibadan!
Welcome to Techbase STEM Academy
Python is fun!
```

You can use as many `print()` lines as you like. Each one starts on a new line.

---

## 5. Python is Case-Sensitive

`print` must always be lowercase. These will cause errors:

```python
Print("Hello")   # ❌ NameError
PRINT("Hello")   # ❌ NameError
print("Hello")   # ✅ Correct
```

---

## 6. Comments

A **comment** is a note in your code that Python completely ignores when running the program. Use the `#` symbol to write one:

```python
# This is a comment — Python skips this line
print("This line will run")

# Calculate price of garri in Naira
print(200)  # price per cup in Naira
```

Comments help you (and others) understand what your code is doing. Good programmers write comments that explain *why* something is written, not just *what* it does.

---

## 7. Printing Numbers

You can also print numbers directly — without quotation marks:

```python
print(100)
print(3.14)
print(2 + 5)    # Python calculates this: output is 7
print(10 * 50)  # output is 500
```

**Output:**
```
100
3.14
7
500
```

Notice: text goes inside quotes, numbers do not.

---

## ✏️ Exercises

Complete these tasks in your editor. Run the code and check your output.

**Exercise 1 — Hello, Nigeria!**  
Write a program that prints exactly this:
```
Hello, Nigeria!
I am learning Python.
Techbase STEM Academy, Ibadan.
```

**Exercise 2 — About You**  
Write a program that prints your name, city, and one thing you want to build with Python. Example:
```
My name is Tunde
I live in Ibadan
I want to build a student records system with Python!
```

**Exercise 3 — Maths with print**  
What will each of these lines print? First guess, then run it and check:
```python
print(5 + 3)
print(20 - 7)
print(4 * 6)
print(15 / 2)
```

**Exercise 4 — Add comments**  
Take this code and add a comment above each `print()` line to explain what it does:
```python
print("Techbase STEM Academy")
print(2025)
print(6 * 10)
```

---

## 📝 Lesson Summary

| Concept | What It Does |
|---------|-------------|
| `print()` | Displays output on the screen |
| `#` | Marks a comment — Python ignores this line |
| Text output | Always goes inside quotation marks `" "` |
| Number output | No quotation marks needed |
| Python | Case-sensitive — `print` not `Print` |

---

## ➡️ What's Next?

In **Lesson 02** you will learn about **Variables and Data Types** — how to store information like a student's name, age, or score so you can use it and change it later in your program.

---

[→ Lesson 02 — Variables & Data Types](lesson_02.md) &nbsp;|&nbsp; [← Back to Course Overview](../README.md)

---

*Techbase Consultant Services · Ibadan, Nigeria · [techbasengr.com.ng](https://techbasengr.com.ng)*
