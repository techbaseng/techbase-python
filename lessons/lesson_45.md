---
render_with_liquid: false
title: "Lesson 45: Python How-Tos, Examples, Exercises, Challenges, Syllabus, Study Plan & Interview Prep"
nav_order: 45
---

# Lesson 45: Python How-Tos, Examples, Exercises, Challenges, Syllabus, Study Plan & Interview Prep

---

## 📖 Lesson Introduction

Welcome to **Lesson 45** — the grand consolidation lesson of your Python journey.

By now you have learned individual Python building blocks: variables, loops, functions, lists, dictionaries, and more. This lesson brings **everything together**.

Here is what you will accomplish in this lesson:

- Learn **how to solve common real-world Python problems** (remove duplicates, reverse a string, add numbers)
- Work through **practical Python examples** drawn from real usage
- Complete **beginner exercises** to test your understanding
- Take a **quiz** to identify what you truly know
- Tackle **challenges** that stretch your thinking
- Follow a **structured Python syllabus** — a complete map of Python topics
- Use a **study plan** to learn Python in an organised schedule
- Prepare for **Python interview questions** so you are job-ready
- Understand **bootcamp and training pathways** so you know how to continue growing

> 💡 **This lesson assumes you know nothing.** Every concept is taught from scratch. Even if you have seen some of these before, this lesson deepens your understanding through new examples and exercises.

---

## 🔑 Prerequisite Concepts

Before diving in, make sure you understand these terms. They are explained simply below.

| Term | Simple Meaning |
|---|---|
| **Variable** | A named box that stores a value, like `name = "Alice"` |
| **List** | An ordered collection of items, like `[1, 2, 3]` |
| **String** | A piece of text surrounded by quotes, like `"hello"` |
| **Loop** | A set of instructions that repeats, like `for x in list:` |
| **Function** | A reusable block of code given a name, like `def greet():` |
| **Integer** | A whole number like `5` or `100` |
| **Print** | The command that displays output on screen: `print("hello")` |

If any of these feel shaky, don't worry — each one is demonstrated freshly throughout this lesson.

---

# Part 1: Python How-To Guides

These "how-to" sections answer the most common practical Python questions beginners ask.

---

## 🔷 How-To 1: Remove Duplicates from a List

### What is a duplicate?

A **duplicate** is an item that appears more than once in a list.

**Example:**
```
fruits = ["apple", "banana", "apple", "cherry", "banana"]
```

Here, `"apple"` appears **twice** and `"banana"` appears **twice**. Those are duplicates.

### Why remove duplicates?

In real-world data — like survey responses, sensor readings, or product lists — duplicates often appear by mistake. Removing them gives you a **clean, unique set of values**.

**Real-world analogy:** Imagine a sign-up sheet where the same person signed their name three times. You only need to count them once. Removing duplicates is like counting each person only once.

---

### Method 1: Using a `set()`

A **set** in Python is a collection that **automatically removes duplicates**. Sets do not allow repeated values.

```python
# Step 1: Start with a list that has duplicates
my_list = [1, 2, 3, 2, 1, 4, 5, 3]

# Step 2: Convert it to a set (duplicates disappear automatically)
unique_set = set(my_list)

# Step 3: Convert it back to a list if you need a list
unique_list = list(unique_set)

print(unique_list)
```

**Expected Output:**
```
[1, 2, 3, 4, 5]
```

> ⚠️ **Important:** Sets are **unordered**. The output may appear in a different sequence each time you run the program. If order matters, use Method 2 below.

---

### Breaking Down the Code Line by Line

| Line | What it does |
|---|---|
| `my_list = [1, 2, 3, 2, 1, 4, 5, 3]` | Creates a list with some duplicate numbers |
| `unique_set = set(my_list)` | Converts the list to a set — Python automatically discards duplicates |
| `unique_list = list(unique_set)` | Converts the set back to a list so you can use list features again |
| `print(unique_list)` | Displays the result on screen |

---

### Method 2: Using a Loop (Preserves Order)

If the **order of items matters**, use a loop to manually build a new list without duplicates.

```python
# Original list with duplicates
my_list = ["banana", "apple", "banana", "cherry", "apple"]

# New empty list to collect unique items
unique_list = []

# Go through each item in the original list
for item in my_list:
    # Only add the item if it's NOT already in unique_list
    if item not in unique_list:
        unique_list.append(item)

print(unique_list)
```

**Expected Output:**
```
['banana', 'apple', 'cherry']
```

Notice the order is preserved — `"banana"` comes first because it appeared first.

---

### Line-by-Line Explanation

| Line | What it does |
|---|---|
| `unique_list = []` | Creates an empty list that will hold results |
| `for item in my_list:` | Loops through every item in the original list one by one |
| `if item not in unique_list:` | Checks if this item has already been added |
| `unique_list.append(item)` | If not already added, add it now |
| `print(unique_list)` | Shows the final deduplicated list |

---

### Method 3: Using `dict.fromkeys()` (Preserves Order, Very Compact)

```python
my_list = [3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5]

unique_list = list(dict.fromkeys(my_list))

print(unique_list)
```

**Expected Output:**
```
[3, 1, 4, 5, 9, 2, 6]
```

`dict.fromkeys()` creates a dictionary from the list (dictionaries can't have duplicate keys), then `list()` converts it back. This is a clean, Pythonic one-liner.

---

### 🤔 Thinking Prompt
What happens if you run `set(["a", "a", "b"])` — how many items will be in the result? Why?

---

### 🔁 Quick Recap — Remove Duplicates

| Method | Preserves Order? | Best For |
|---|---|---|
| `set()` | ❌ No | When order doesn't matter |
| Loop with `not in` | ✅ Yes | When order matters |
| `dict.fromkeys()` | ✅ Yes | Compact, readable code |

---

## 🔷 How-To 2: Reverse a String

### What does "reverse a string" mean?

It means flipping the text so the last character becomes the first.

- Original: `"hello"`
- Reversed: `"olleh"`

### Why would you reverse a string?

- Checking if a word is a **palindrome** (reads the same forwards and backwards, like "racecar")
- Text processing and data manipulation
- Puzzle and interview challenges
- Game mechanics (secret codes, encryption basics)

---

### Method 1: Slicing (The Pythonic Way)

Python's **slice notation** lets you extract parts of a string using `[start:stop:step]`.

To reverse: use `[::-1]` — which means "start from end, go backwards, step by -1."

```python
# Original string
text = "Hello, World!"

# Reverse using slicing
reversed_text = text[::-1]

print(reversed_text)
```

**Expected Output:**
```
!dlroW ,olleH
```

---

### Understanding `[::-1]` Step by Step

Think of a string as a row of numbered seats:

```
H  e  l  l  o
0  1  2  3  4
```

- `[start:stop:step]` = `[::-1]`
- No `start` → begin from wherever the step takes you (the end, since step is negative)
- No `stop` → go all the way to the other end
- `-1` step → move one position **backwards** each time

So Python visits: `o`, `l`, `l`, `e`, `H` → producing `"olleH"`.

---

### Method 2: Using the `reversed()` Function

```python
text = "Python"

# reversed() returns an iterator, join() combines the characters
reversed_text = "".join(reversed(text))

print(reversed_text)
```

**Expected Output:**
```
nohtyP
```

- `reversed(text)` — creates a reverse iterator over the characters
- `"".join(...)` — joins all the characters together with no separator between them

---

### Method 3: Using a Loop (Good for Understanding)

```python
text = "science"
reversed_text = ""

for char in text:
    reversed_text = char + reversed_text  # each new char goes to the FRONT

print(reversed_text)
```

**Expected Output:**
```
ecneics
```

Each loop iteration **prepends** the current character to the front of `reversed_text`.

---

### Palindrome Check — Practical Application

```python
word = "racecar"

if word == word[::-1]:
    print(word, "is a palindrome!")
else:
    print(word, "is NOT a palindrome.")
```

**Expected Output:**
```
racecar is a palindrome!
```

Try it with `"python"` — what do you get?

---

### 🤔 Thinking Prompt
What is `"12345"[::-1]`? Write it out by hand first, then test it.

---

## 🔷 How-To 3: Add Two Numbers

### What does "add two numbers" mean in Python?

This is the simplest form of arithmetic in Python. You use the `+` operator.

```python
x = 5
y = 3
result = x + y
print(result)
```

**Expected Output:**
```
8
```

Simple! But let's go deeper.

---

### Adding Numbers Entered by the User

In real programs, you usually don't know the numbers in advance — the **user types them in**.

```python
# Ask the user to type two numbers
num1 = input("Enter first number: ")
num2 = input("Enter second number: ")

# IMPORTANT: input() always returns a STRING, not a number
# We must convert to int (whole number) or float (decimal)
sum_result = int(num1) + int(num2)

print("The sum is:", sum_result)
```

**Example Interaction:**
```
Enter first number: 12
Enter second number: 7
The sum is: 19
```

---

### Why Must We Convert with `int()`?

When a user types `"5"` on the keyboard, Python stores it as the **text** `"5"`, not the number `5`.

Text + Text in Python does **concatenation** (joining), not addition:

```python
print("5" + "3")   # Output: 53  ← wrong! This joins strings
print(5 + 3)       # Output: 8   ← correct! This adds numbers
```

So `int("5")` converts the text `"5"` into the number `5`.

---

### Adding Floating-Point (Decimal) Numbers

```python
a = 4.5
b = 2.3

total = a + b
print("Total:", total)
```

**Expected Output:**
```
Total: 6.8
```

Use `float()` instead of `int()` when decimals are needed:

```python
num1 = float(input("Enter first decimal: "))
num2 = float(input("Enter second decimal: "))
print("Sum:", num1 + num2)
```

---

### Adding Numbers in a List

Sometimes you want to add all numbers in a collection:

```python
numbers = [10, 20, 30, 40, 50]
total = sum(numbers)
print("Total:", total)
```

**Expected Output:**
```
Total: 150
```

`sum()` is a built-in Python function that adds all values in a list.

---

# Part 2: Python Examples — Core Concepts Demonstrated

This section covers the most important Python examples that every beginner must know. These are drawn directly from real Python practice and professional usage.

---

## 🔷 Example Category 1: Print and Variables

### Printing Text

```python
print("Hello, World!")
```

**Output:**
```
Hello, World!
```

### Storing and Using Variables

```python
name = "Alice"
age = 25
city = "London"

print(name, "is", age, "years old and lives in", city)
```

**Output:**
```
Alice is 25 years old and lives in London
```

### Multiple Data Types

```python
text = "Python"          # String
whole_number = 42        # Integer
decimal = 3.14           # Float
is_fun = True            # Boolean

print(type(text))
print(type(whole_number))
print(type(decimal))
print(type(is_fun))
```

**Output:**
```
<class 'str'>
<class 'int'>
<class 'float'>
<class 'bool'>
```

---

## 🔷 Example Category 2: String Operations

### String Length

```python
sentence = "Hello, Python!"
print(len(sentence))
```

**Output:**
```
14
```

### Uppercase and Lowercase

```python
word = "Python"
print(word.upper())
print(word.lower())
```

**Output:**
```
PYTHON
python
```

### String Slicing

```python
text = "Programming"
print(text[0:4])    # First 4 characters
print(text[-3:])    # Last 3 characters
```

**Output:**
```
Prog
ing
```

### String Replacement

```python
sentence = "I love Java"
new_sentence = sentence.replace("Java", "Python")
print(new_sentence)
```

**Output:**
```
I love Python
```

### String Split

```python
data = "Alice,Bob,Charlie,Diana"
names = data.split(",")
print(names)
```

**Output:**
```
['Alice', 'Bob', 'Charlie', 'Diana']
```

---

## 🔷 Example Category 3: Lists

### Create and Access a List

```python
fruits = ["apple", "banana", "cherry"]
print(fruits[0])    # First item
print(fruits[-1])   # Last item
print(fruits[1:3])  # Slice: items at index 1 and 2
```

**Output:**
```
apple
cherry
['banana', 'cherry']
```

### Add, Remove, Sort

```python
numbers = [3, 1, 4, 1, 5, 9, 2, 6]

numbers.append(7)        # Add to end
numbers.remove(1)        # Remove first occurrence of 1
numbers.sort()           # Sort ascending

print(numbers)
```

**Output:**
```
[1, 2, 3, 4, 5, 6, 7, 9]
```

### Loop Through a List

```python
colours = ["red", "green", "blue"]

for colour in colours:
    print("Colour:", colour)
```

**Output:**
```
Colour: red
Colour: green
Colour: blue
```

---

## 🔷 Example Category 4: Dictionaries

### Create and Access

```python
student = {
    "name": "Bob",
    "age": 20,
    "grade": "A"
}

print(student["name"])
print(student["grade"])
```

**Output:**
```
Bob
A
```

### Loop Through a Dictionary

```python
person = {"name": "Carol", "city": "Paris", "job": "Engineer"}

for key, value in person.items():
    print(key, "→", value)
```

**Output:**
```
name → Carol
city → Paris
job → Engineer
```

---

## 🔷 Example Category 5: Conditionals (if/elif/else)

### Basic If-Else

```python
temperature = 35

if temperature > 30:
    print("It's hot outside!")
elif temperature > 20:
    print("It's warm.")
else:
    print("It's cool.")
```

**Output:**
```
It's hot outside!
```

### Grade Calculator

```python
score = 78

if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
elif score >= 60:
    grade = "D"
else:
    grade = "F"

print("Grade:", grade)
```

**Output:**
```
Grade: C
```

---

## 🔷 Example Category 6: Loops

### `for` Loop with `range()`

```python
for i in range(1, 6):
    print("Step", i)
```

**Output:**
```
Step 1
Step 2
Step 3
Step 4
Step 5
```

### `while` Loop

```python
count = 0

while count < 5:
    print("Count:", count)
    count += 1  # count = count + 1
```

**Output:**
```
Count: 0
Count: 1
Count: 2
Count: 3
Count: 4
```

### Loop with `break` and `continue`

```python
for num in range(1, 11):
    if num == 5:
        continue       # Skip number 5
    if num == 8:
        break          # Stop at number 8
    print(num)
```

**Output:**
```
1
2
3
4
6
7
```

---

## 🔷 Example Category 7: Functions

### Basic Function

```python
def greet(name):
    print("Hello,", name + "!")

greet("Alice")
greet("Bob")
```

**Output:**
```
Hello, Alice!
Hello, Bob!
```

### Function with Return Value

```python
def add(a, b):
    return a + b

result = add(10, 25)
print("Sum:", result)
```

**Output:**
```
Sum: 35
```

### Function with Default Parameter

```python
def greet(name, message="Welcome!"):
    print(name + ":", message)

greet("Alice")
greet("Bob", "Nice to meet you!")
```

**Output:**
```
Alice: Welcome!
Bob: Nice to meet you!
```

---

## 🔷 Example Category 8: Lambda Functions

A **lambda** is a small, anonymous (nameless) one-line function.

```python
# Regular function
def square(x):
    return x * x

# Equivalent lambda
square_lambda = lambda x: x * x

print(square(5))         # Output: 25
print(square_lambda(5))  # Output: 25
```

Lambdas are useful when you need a quick, short function without defining a full `def` block.

---

## 🔷 Example Category 9: Classes and Objects

### Define a Class

```python
class Dog:
    def __init__(self, name, breed):
        self.name = name
        self.breed = breed

    def bark(self):
        print(self.name, "says: Woof!")

# Create objects from the class
dog1 = Dog("Rex", "Labrador")
dog2 = Dog("Bella", "Poodle")

dog1.bark()
dog2.bark()
print(dog1.breed)
```

**Output:**
```
Rex says: Woof!
Bella says: Woof!
Labrador
```

---

## 🔷 Example Category 10: File Handling

### Write to a File

```python
with open("notes.txt", "w") as file:
    file.write("Hello, this is a note.\n")
    file.write("Python file handling is easy!")
```

### Read from a File

```python
with open("notes.txt", "r") as file:
    content = file.read()
    print(content)
```

**Output:**
```
Hello, this is a note.
Python file handling is easy!
```

---

# Part 3: Python Exercises

Exercises are how you truly learn. Reading is not enough — you must write code yourself.

The following exercises are arranged by difficulty: beginner → intermediate → applied.

---

## ✏️ Exercise Set 1: Variables and Print

### Exercise 1.1 — Store and Display Your Info

**Objective:** Create variables for your name, age, and favourite colour and print them in a sentence.

**Expected Output:**
```
My name is Sam, I am 22 years old, and my favourite colour is blue.
```

**Starter Template:**
```python
name = ___
age = ___
colour = ___

print("My name is", ___, "I am", ___, "years old, and my favourite colour is", ___ + ".")
```

**Solution:**
```python
name = "Sam"
age = 22
colour = "blue"

print("My name is", name + ", I am", age, "years old, and my favourite colour is", colour + ".")
```

---

### Exercise 1.2 — Calculate Your Birth Year

```python
current_year = 2025
age = int(input("How old are you? "))
birth_year = current_year - age
print("You were probably born in", birth_year)
```

**Example Interaction:**
```
How old are you? 20
You were probably born in 2005
```

---

## ✏️ Exercise Set 2: String Exercises

### Exercise 2.1 — Reverse and Check Palindrome

**Task:** Ask the user to enter a word. Check if it is a palindrome.

```python
word = input("Enter a word: ").lower()

if word == word[::-1]:
    print(word, "is a palindrome.")
else:
    print(word, "is not a palindrome.")
```

**Example 1:**
```
Enter a word: level
level is a palindrome.
```

**Example 2:**
```
Enter a word: hello
hello is not a palindrome.
```

---

### Exercise 2.2 — Count Vowels in a String

```python
text = input("Enter a sentence: ")
vowels = "aeiouAEIOU"
count = 0

for char in text:
    if char in vowels:
        count += 1

print("Number of vowels:", count)
```

**Example:**
```
Enter a sentence: Hello World
Number of vowels: 3
```

---

## ✏️ Exercise Set 3: List Exercises

### Exercise 3.1 — Find the Largest Number

```python
numbers = [45, 12, 78, 34, 90, 23]

largest = numbers[0]

for num in numbers:
    if num > largest:
        largest = num

print("Largest number:", largest)
```

**Output:**
```
Largest number: 90
```

---

### Exercise 3.2 — Remove Duplicates and Sort

```python
data = [5, 3, 8, 3, 1, 5, 9, 1, 7]

unique_data = list(set(data))
unique_data.sort()

print("Cleaned and sorted:", unique_data)
```

**Output:**
```
Cleaned and sorted: [1, 3, 5, 7, 8, 9]
```

---

### Exercise 3.3 — Sum and Average of a List

```python
scores = [85, 92, 76, 88, 91, 67, 73]

total = sum(scores)
average = total / len(scores)

print("Total:", total)
print("Average:", round(average, 2))
```

**Output:**
```
Total: 572
Average: 81.71
```

---

## ✏️ Exercise Set 4: Loop Exercises

### Exercise 4.1 — Multiplication Table

```python
number = int(input("Enter a number for its multiplication table: "))

for i in range(1, 11):
    print(number, "x", i, "=", number * i)
```

**Example (number = 7):**
```
7 x 1 = 7
7 x 2 = 14
...
7 x 10 = 70
```

---

### Exercise 4.2 — FizzBuzz (Classic Interview Challenge)

**Rules:**
- For multiples of 3, print `"Fizz"`
- For multiples of 5, print `"Buzz"`
- For multiples of both, print `"FizzBuzz"`
- Otherwise, print the number

```python
for i in range(1, 31):
    if i % 3 == 0 and i % 5 == 0:
        print("FizzBuzz")
    elif i % 3 == 0:
        print("Fizz")
    elif i % 5 == 0:
        print("Buzz")
    else:
        print(i)
```

**Output (first 15 lines):**
```
1
2
Fizz
4
Buzz
Fizz
7
8
Fizz
Buzz
11
Fizz
13
14
FizzBuzz
```

---

## ✏️ Exercise Set 5: Function Exercises

### Exercise 5.1 — Temperature Converter

```python
def celsius_to_fahrenheit(celsius):
    return (celsius * 9/5) + 32

def fahrenheit_to_celsius(fahrenheit):
    return (fahrenheit - 32) * 5/9

print(celsius_to_fahrenheit(100))   # Expected: 212.0
print(fahrenheit_to_celsius(32))    # Expected: 0.0
```

---

### Exercise 5.2 — Simple Calculator Function

```python
def calculate(a, b, operation):
    if operation == "add":
        return a + b
    elif operation == "subtract":
        return a - b
    elif operation == "multiply":
        return a * b
    elif operation == "divide":
        if b != 0:
            return a / b
        else:
            return "Error: Cannot divide by zero"
    else:
        return "Unknown operation"

print(calculate(10, 5, "add"))       # 15
print(calculate(10, 5, "subtract"))  # 5
print(calculate(10, 5, "multiply"))  # 50
print(calculate(10, 5, "divide"))    # 2.0
print(calculate(10, 0, "divide"))    # Error: Cannot divide by zero
```

---

# Part 4: Python Quiz — Test Your Knowledge

This quiz tests key Python concepts. Try answering each question before revealing the answer.

---

### Quiz Question 1
**What is the output of this code?**

```python
x = 10
y = 3
print(x % y)
```

<details>
<summary>Click to reveal answer</summary>

**Answer: `1`**

The `%` operator is the **modulus** (remainder) operator. `10 ÷ 3 = 3 remainder 1`. So `10 % 3 = 1`.
</details>

---

### Quiz Question 2
**What does this code print?**

```python
text = "Hello"
print(text[1])
```

<details>
<summary>Click to reveal answer</summary>

**Answer: `e`**

Python uses **zero-based indexing**. Index `0` = `H`, index `1` = `e`.
</details>

---

### Quiz Question 3
**What is the output?**

```python
numbers = [1, 2, 3, 4, 5]
print(numbers[-1])
```

<details>
<summary>Click to reveal answer</summary>

**Answer: `5`**

Negative indexing counts from the end. `-1` refers to the **last** element, which is `5`.
</details>

---

### Quiz Question 4
**What does `len("Python")` return?**

<details>
<summary>Click to reveal answer</summary>

**Answer: `6`**

`len()` counts characters. `P-y-t-h-o-n` = 6 characters.
</details>

---

### Quiz Question 5
**What is the output?**

```python
for i in range(0, 10, 2):
    print(i)
```

<details>
<summary>Click to reveal answer</summary>

**Answer:**
```
0
2
4
6
8
```

`range(0, 10, 2)` starts at `0`, ends before `10`, and steps by `2` (every other number).
</details>

---

### Quiz Question 6
**True or False: In Python, a list can hold items of different data types.**

<details>
<summary>Click to reveal answer</summary>

**Answer: TRUE**

A Python list can contain strings, integers, floats, booleans, and even other lists:
```python
mixed = [1, "hello", 3.14, True]
```
</details>

---

### Quiz Question 7
**What is the output?**

```python
def mystery(n):
    return n * 2 + 1

print(mystery(4))
```

<details>
<summary>Click to reveal answer</summary>

**Answer: `9`**

`mystery(4)` = `4 * 2 + 1` = `8 + 1` = `9`.
</details>

---

### Quiz Question 8
**What does `type(3.14)` return?**

<details>
<summary>Click to reveal answer</summary>

**Answer: `<class 'float'>`**

`3.14` has a decimal point, making it a floating-point number (`float`).
</details>

---

### Quiz Question 9
**What is the output?**

```python
my_dict = {"a": 1, "b": 2, "c": 3}
print(my_dict["b"])
```

<details>
<summary>Click to reveal answer</summary>

**Answer: `2`**

Dictionary values are accessed using their **key**. The key `"b"` maps to the value `2`.
</details>

---

### Quiz Question 10
**Which of these correctly defines a Python function?**

```
A) function greet():
B) def greet():
C) define greet():
D) func greet():
```

<details>
<summary>Click to reveal answer</summary>

**Answer: B) `def greet():`**

In Python, functions are defined using the keyword `def`.
</details>

---

# Part 5: Python Challenges

Challenges are harder problems that require you to combine multiple concepts. These simulate real interview and problem-solving scenarios.

---

## 🏆 Challenge 1: Count Word Frequency

**Problem:** Given a sentence, count how many times each word appears.

```python
sentence = "the cat sat on the mat the cat"

words = sentence.split()
frequency = {}

for word in words:
    if word in frequency:
        frequency[word] += 1
    else:
        frequency[word] = 1

for word, count in frequency.items():
    print(word, ":", count)
```

**Output:**
```
the : 3
cat : 2
sat : 1
on : 1
mat : 1
```

---

## 🏆 Challenge 2: Fibonacci Sequence

**Problem:** Print the first `n` numbers of the Fibonacci sequence.

> **What is Fibonacci?** Each number is the sum of the two before it: 0, 1, 1, 2, 3, 5, 8, 13, 21...

```python
def fibonacci(n):
    a, b = 0, 1
    result = []
    for _ in range(n):
        result.append(a)
        a, b = b, a + b
    return result

print(fibonacci(10))
```

**Output:**
```
[0, 1, 1, 2, 3, 5, 8, 13, 21, 34]
```

---

## 🏆 Challenge 3: Check Prime Number

**Problem:** Write a function that returns `True` if a number is prime, otherwise `False`.

> **Prime number:** A number divisible only by 1 and itself (e.g., 2, 3, 5, 7, 11).

```python
def is_prime(n):
    if n < 2:
        return False
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0:
            return False
    return True

# Test it
for num in range(2, 20):
    if is_prime(num):
        print(num, "is prime")
```

**Output:**
```
2 is prime
3 is prime
5 is prime
7 is prime
11 is prime
13 is prime
17 is prime
19 is prime
```

---

## 🏆 Challenge 4: Flatten a Nested List

**Problem:** Given a list containing sublists, create a single flat list.

```python
nested = [[1, 2, 3], [4, 5], [6, 7, 8, 9]]

flat = []
for sublist in nested:
    for item in sublist:
        flat.append(item)

print(flat)
```

**Output:**
```
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

**One-liner using list comprehension:**
```python
flat = [item for sublist in nested for item in sublist]
print(flat)
```

---

## 🏆 Challenge 5: Anagram Checker

**Problem:** Check if two words are anagrams (contain the same letters).

```python
def are_anagrams(word1, word2):
    return sorted(word1.lower()) == sorted(word2.lower())

print(are_anagrams("listen", "silent"))   # True
print(are_anagrams("hello", "world"))     # False
print(are_anagrams("Triangle", "Integral"))  # True
```

**Output:**
```
True
False
True
```

`sorted()` converts a string to a sorted list of characters. If two words have the same characters in the same frequency, their sorted forms are identical.

---

## 🏆 Challenge 6: Find Missing Number

**Problem:** Given a list of numbers from 1 to n with one missing, find the missing number.

```python
def find_missing(numbers, n):
    expected_sum = n * (n + 1) // 2
    actual_sum = sum(numbers)
    return expected_sum - actual_sum

nums = [1, 2, 4, 5, 6, 7, 8, 9, 10]
print("Missing number:", find_missing(nums, 10))
```

**Output:**
```
Missing number: 3
```

**How it works:** The formula `n*(n+1)/2` gives the sum of all numbers from 1 to n. Subtract the actual sum to find the gap.

---

# Part 6: Python Practice — Building Real Skills

Practice is deliberate repetition with feedback. This section gives you structured practice tasks.

---

## 📝 Practice Task 1: Student Grade Tracker

**Scenario:** You are building a simple grade-tracking tool for a teacher.

```python
students = {}

# Add students and their scores
students["Alice"] = [85, 92, 78, 90]
students["Bob"] = [70, 65, 80, 75]
students["Carol"] = [95, 98, 92, 97]

# Calculate and display averages
for name, scores in students.items():
    average = sum(scores) / len(scores)
    print(name + ":", round(average, 1), "average")
```

**Output:**
```
Alice: 86.2 average
Bob: 72.5 average
Carol: 95.5 average
```

**Enhancement:** Add a grade letter (A/B/C/D/F) based on the average.

---

## 📝 Practice Task 2: Shopping Cart Calculator

```python
cart = {
    "Milk": 1.50,
    "Bread": 2.00,
    "Eggs": 3.25,
    "Butter": 4.75,
    "Coffee": 6.99
}

total = 0
print("=== Shopping Cart ===")

for item, price in cart.items():
    print(f"  {item}: £{price:.2f}")
    total += price

tax = total * 0.20  # 20% VAT
grand_total = total + tax

print("-------------------")
print(f"Subtotal: £{total:.2f}")
print(f"Tax (20%): £{tax:.2f}")
print(f"Total: £{grand_total:.2f}")
```

**Output:**
```
=== Shopping Cart ===
  Milk: £1.50
  Bread: £2.00
  Eggs: £3.25
  Butter: £4.75
  Coffee: £6.99
-------------------
Subtotal: £18.49
Tax (20%): £3.70
Total: £22.19
```

---

## 📝 Practice Task 3: Number Guessing Game

```python
import random

secret = random.randint(1, 100)
attempts = 0

print("Guess the number between 1 and 100!")

while True:
    guess = int(input("Your guess: "))
    attempts += 1

    if guess < secret:
        print("Too low! Try higher.")
    elif guess > secret:
        print("Too high! Try lower.")
    else:
        print(f"Correct! You got it in {attempts} attempts.")
        break
```

---

# Part 7: Python Syllabus — Your Complete Learning Map

This is the official map of all Python topics, organised from beginner to advanced. Use this as your **learning checklist**.

---

## 📚 Module 1: Python Basics (Beginner)

| # | Topic | Description |
|---|---|---|
| 1.1 | Python Introduction | What Python is, where it's used, how to install |
| 1.2 | Python Syntax | Indentation, comments, basic structure |
| 1.3 | Variables | Creating and naming variables |
| 1.4 | Data Types | str, int, float, bool, list, dict, tuple, set |
| 1.5 | Numbers | Arithmetic operators: +, -, *, /, //, %, ** |
| 1.6 | Strings | Creating, slicing, formatting, methods |
| 1.7 | Booleans | True/False, comparison operators |
| 1.8 | Operators | Arithmetic, assignment, comparison, logical |
| 1.9 | Type Casting | Converting between types: int(), str(), float() |
| 1.10 | User Input | `input()`, reading from the keyboard |

---

## 📚 Module 2: Control Flow

| # | Topic | Description |
|---|---|---|
| 2.1 | If...Else | Conditional branching |
| 2.2 | elif | Multiple condition branches |
| 2.3 | Nested If | If inside if |
| 2.4 | While Loop | Repeat while a condition is True |
| 2.5 | For Loop | Iterate over sequences |
| 2.6 | range() | Generating number sequences |
| 2.7 | break | Exit a loop early |
| 2.8 | continue | Skip to next iteration |
| 2.9 | pass | Placeholder for empty code blocks |

---

## 📚 Module 3: Data Structures

| # | Topic | Description |
|---|---|---|
| 3.1 | Lists | Ordered, mutable sequences |
| 3.2 | Tuples | Ordered, immutable sequences |
| 3.3 | Sets | Unordered, unique collections |
| 3.4 | Dictionaries | Key-value pairs |
| 3.5 | List Comprehension | Compact list creation |
| 3.6 | Dictionary Comprehension | Compact dictionary creation |

---

## 📚 Module 4: Functions

| # | Topic | Description |
|---|---|---|
| 4.1 | Functions | Defining and calling functions |
| 4.2 | Arguments | Positional, keyword, default parameters |
| 4.3 | *args | Variable number of positional arguments |
| 4.4 | **kwargs | Variable number of keyword arguments |
| 4.5 | Return | Returning values from functions |
| 4.6 | Lambda | Anonymous one-line functions |
| 4.7 | Recursion | Functions that call themselves |
| 4.8 | Scope | Local vs global variables |

---

## 📚 Module 5: Object-Oriented Programming (OOP)

| # | Topic | Description |
|---|---|---|
| 5.1 | Classes | Blueprints for objects |
| 5.2 | Objects | Instances of a class |
| 5.3 | `__init__` | The constructor method |
| 5.4 | Methods | Functions inside a class |
| 5.5 | Inheritance | One class extending another |
| 5.6 | Polymorphism | Same method, different behaviour |
| 5.7 | Encapsulation | Hiding internal data |
| 5.8 | Abstraction | Hiding complexity |
| 5.9 | Iterators | Objects with `__iter__` and `__next__` |

---

## 📚 Module 6: Working with Files and Errors

| # | Topic | Description |
|---|---|---|
| 6.1 | File Open/Read | Reading files with `open()` |
| 6.2 | File Write | Writing to files |
| 6.3 | File Delete | Removing files with `os` module |
| 6.4 | Try/Except | Handling errors gracefully |
| 6.5 | Raise | Triggering custom errors |
| 6.6 | Finally | Code that always runs |

---

## 📚 Module 7: Advanced Python

| # | Topic | Description |
|---|---|---|
| 7.1 | Modules | Importing standard and third-party modules |
| 7.2 | Dates | Working with `datetime` module |
| 7.3 | Math | Using the `math` module |
| 7.4 | JSON | Parsing and generating JSON data |
| 7.5 | RegEx | Pattern matching with `re` module |
| 7.6 | PIP | Installing external packages |
| 7.7 | Virtual Environments | Isolated project environments |
| 7.8 | NumPy | Numerical computing library |
| 7.9 | Pandas | Data analysis library |
| 7.10 | Matplotlib | Data visualisation library |

---

# Part 8: Python Study Plan — Learn Python in 8 Weeks

This structured plan takes you from zero to confident Python programmer in 8 weeks, studying approximately **1–2 hours per day**.

---

## 🗓️ Week 1: Python Foundations

| Day | Topic | Goal |
|---|---|---|
| Day 1 | Install Python + Write First Program | Print "Hello, World!" |
| Day 2 | Variables & Data Types | Store and display different types of data |
| Day 3 | Strings & String Methods | Manipulate text |
| Day 4 | Numbers & Math Operations | Perform calculations |
| Day 5 | User Input & Type Casting | Build interactive programs |
| Day 6 | Review + Practice Exercises | Reinforce Week 1 topics |
| Day 7 | Mini-Project: Personal Profile Printer | Apply all Week 1 concepts |

**Week 1 Mini-Project:**
```python
name = input("Enter your name: ")
age = int(input("Enter your age: "))
city = input("Enter your city: ")
hobby = input("Enter your hobby: ")

print("\n=== Your Profile ===")
print("Name:", name)
print("Age:", age)
print("City:", city)
print("Hobby:", hobby)
print("In 10 years you'll be:", age + 10)
```

---

## 🗓️ Week 2: Control Flow

| Day | Topic | Goal |
|---|---|---|
| Day 8 | If/Elif/Else | Make decisions in code |
| Day 9 | Comparison & Logical Operators | Combine conditions |
| Day 10 | For Loops + range() | Repeat actions |
| Day 11 | While Loops | Loop with conditions |
| Day 12 | Break, Continue, Pass | Control loop flow |
| Day 13 | Review + Exercises | FizzBuzz, grade calculator |
| Day 14 | Mini-Project: Number Guessing Game | Apply control flow |

---

## 🗓️ Week 3: Data Structures

| Day | Topic | Goal |
|---|---|---|
| Day 15 | Lists (Create, Access, Modify) | Store ordered data |
| Day 16 | List Methods | Sort, append, remove |
| Day 17 | Tuples & Sets | Immutable and unique collections |
| Day 18 | Dictionaries | Key-value data storage |
| Day 19 | Nested Data Structures | Dicts inside lists, etc. |
| Day 20 | Review + Exercises | Remove duplicates, word count |
| Day 21 | Mini-Project: Student Grade Tracker | Use lists and dicts |

---

## 🗓️ Week 4: Functions

| Day | Topic | Goal |
|---|---|---|
| Day 22 | Defining Functions | Create reusable code blocks |
| Day 23 | Arguments & Return | Pass data in and out |
| Day 24 | Default & Keyword Args | Flexible function calls |
| Day 25 | *args and **kwargs | Variable arguments |
| Day 26 | Lambda Functions | Quick anonymous functions |
| Day 27 | Scope & Recursion | Understand variable visibility |
| Day 28 | Mini-Project: Calculator App | Build a functional tool |

---

## 🗓️ Week 5: Object-Oriented Programming

| Day | Topic | Goal |
|---|---|---|
| Day 29 | Classes and Objects | Create blueprints and instances |
| Day 30 | `__init__` and Methods | Object initialisation |
| Day 31 | Inheritance | Extend existing classes |
| Day 32 | Polymorphism | Flexible method behaviour |
| Day 33 | Encapsulation & Properties | Protect data |
| Day 34 | Review + Exercises | Build a Bank Account class |
| Day 35 | Mini-Project: Library System | Books, Members, Borrowing |

---

## 🗓️ Week 6: Files, Errors & Modules

| Day | Topic | Goal |
|---|---|---|
| Day 36 | Reading & Writing Files | Persist data to disk |
| Day 37 | Try/Except Error Handling | Prevent crashes |
| Day 38 | Standard Library Modules | math, random, datetime, os |
| Day 39 | JSON Data | Read/write structured data |
| Day 40 | RegEx Basics | Pattern matching in strings |
| Day 41 | Review + Practice | File-based programs |
| Day 42 | Mini-Project: CSV Contact Book | Store contacts in a file |

---

## 🗓️ Week 7: Intermediate Python

| Day | Topic | Goal |
|---|---|---|
| Day 43 | List Comprehensions | Compact list operations |
| Day 44 | Dictionary Comprehensions | Compact dictionary operations |
| Day 45 | Generators & Iterators | Memory-efficient sequences |
| Day 46 | Decorators | Modify function behaviour |
| Day 47 | Context Managers (with) | Resource management |
| Day 48 | Virtual Environments & PIP | Manage packages |
| Day 49 | Mini-Project: Data Filter Tool | Process and clean data |

---

## 🗓️ Week 8: Real-World Python Applications

| Day | Topic | Goal |
|---|---|---|
| Day 50 | NumPy Basics | Arrays and maths |
| Day 51 | Pandas Basics | DataFrames and data analysis |
| Day 52 | Matplotlib Basics | Charts and visualisations |
| Day 53 | Web Scraping (requests + BeautifulSoup) | Collect web data |
| Day 54 | APIs (requests library) | Connect to external services |
| Day 55 | Introduction to Flask | Build a simple web app |
| Day 56 | Final Capstone Project | Build a complete data-driven app |

---

# Part 9: Python Interview Questions — Be Job-Ready

These are the most commonly asked Python questions in technical job interviews. Each includes a clear answer and code where relevant.

---

## 🎯 Beginner-Level Interview Questions

### Q1: What is Python and what are its main uses?

**Answer:**
Python is a high-level, interpreted, general-purpose programming language created by Guido van Rossum in 1991. It is known for its clean, readable syntax.

**Main uses:**
- Web development (Django, Flask)
- Data analysis (Pandas, NumPy)
- Machine learning (TensorFlow, scikit-learn)
- Automation and scripting
- Scientific computing
- Game development
- Cybersecurity

---

### Q2: What are Python's key features?

**Answer:**
- **Readable syntax** — looks almost like plain English
- **Interpreted** — runs line by line, no need to compile
- **Dynamically typed** — no need to declare variable types
- **Object-oriented** — supports classes and objects
- **Large standard library** — hundreds of built-in modules
- **Cross-platform** — runs on Windows, Mac, Linux
- **Open-source** — free to use and distribute

---

### Q3: What is the difference between a list and a tuple?

| Feature | List | Tuple |
|---|---|---|
| Syntax | `[1, 2, 3]` | `(1, 2, 3)` |
| Mutable? | ✅ Yes (can change) | ❌ No (fixed) |
| Speed | Slower | Faster |
| Use case | Data that changes | Fixed data (coordinates, config) |

```python
my_list = [1, 2, 3]
my_list[0] = 99    # Works fine

my_tuple = (1, 2, 3)
my_tuple[0] = 99   # TypeError! Tuples are immutable
```

---

### Q4: What is the difference between `==` and `is`?

- `==` checks if two values are **equal**
- `is` checks if two variables point to the **same object in memory**

```python
a = [1, 2, 3]
b = [1, 2, 3]

print(a == b)   # True  (same values)
print(a is b)   # False (different objects in memory)

c = a
print(a is c)   # True  (same object)
```

---

### Q5: What are Python's built-in data types?

| Category | Types |
|---|---|
| Text | `str` |
| Numeric | `int`, `float`, `complex` |
| Sequence | `list`, `tuple`, `range` |
| Mapping | `dict` |
| Set | `set`, `frozenset` |
| Boolean | `bool` |
| Binary | `bytes`, `bytearray` |
| None | `NoneType` |

---

### Q6: What is `None` in Python?

`None` is Python's way of representing **nothing** or **no value**. It is similar to `null` in other languages.

```python
result = None

if result is None:
    print("No result yet")
```

---

### Q7: What is a dictionary in Python?

A dictionary stores **key-value pairs**. Keys must be unique and immutable. Values can be anything.

```python
person = {
    "name": "Alice",
    "age": 30,
    "job": "Engineer"
}

print(person["name"])     # Alice
print(person.get("age"))  # 30
person["city"] = "London" # Add a new key
```

---

### Q8: Explain the difference between `append()` and `extend()`

- `append()` adds **one item** to the end of a list
- `extend()` adds **all items** from another iterable

```python
list1 = [1, 2, 3]
list1.append([4, 5])
print(list1)   # [1, 2, 3, [4, 5]] ← nested list added

list2 = [1, 2, 3]
list2.extend([4, 5])
print(list2)   # [1, 2, 3, 4, 5] ← items added individually
```

---

### Q9: What is a list comprehension?

A compact way to create a new list from an existing one.

**Traditional loop:**
```python
squares = []
for x in range(1, 6):
    squares.append(x ** 2)
```

**List comprehension:**
```python
squares = [x ** 2 for x in range(1, 6)]
print(squares)   # [1, 4, 9, 16, 25]
```

---

### Q10: What is the difference between `break`, `continue`, and `pass`?

```python
# break: exits the loop entirely
for i in range(10):
    if i == 5:
        break
    print(i)        # Prints 0 1 2 3 4

# continue: skips the current iteration, continues loop
for i in range(10):
    if i == 5:
        continue
    print(i)        # Prints 0 1 2 3 4 6 7 8 9

# pass: does nothing, placeholder
for i in range(3):
    pass            # No output, but no error either
```

---

## 🎯 Intermediate Interview Questions

### Q11: What is a lambda function?

A lambda is a small, unnamed function defined with the `lambda` keyword.

```python
double = lambda x: x * 2
print(double(5))    # 10

# Common use: sort a list of tuples by second element
pairs = [(1, 'b'), (3, 'a'), (2, 'c')]
pairs.sort(key=lambda pair: pair[1])
print(pairs)   # [(3, 'a'), (1, 'b'), (2, 'c')]
```

---

### Q12: What is the difference between `*args` and `**kwargs`?

- `*args` — collects extra **positional** arguments into a tuple
- `**kwargs` — collects extra **keyword** arguments into a dictionary

```python
def show_args(*args):
    for item in args:
        print(item)

show_args(1, 2, 3)   # Prints 1, 2, 3 each on a new line

def show_kwargs(**kwargs):
    for key, value in kwargs.items():
        print(key, "=", value)

show_kwargs(name="Alice", age=25)
# name = Alice
# age = 25
```

---

### Q13: What is a Python decorator?

A decorator is a function that wraps another function to modify its behaviour **without changing its code**.

```python
def my_decorator(func):
    def wrapper():
        print("Before the function runs")
        func()
        print("After the function runs")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()
```

**Output:**
```
Before the function runs
Hello!
After the function runs
```

---

### Q14: What is the difference between shallow copy and deep copy?

- **Shallow copy**: Copies the outer object but shares inner objects
- **Deep copy**: Copies everything, including nested objects

```python
import copy

original = [[1, 2], [3, 4]]

shallow = copy.copy(original)
deep = copy.deepcopy(original)

original[0][0] = 99

print(original)   # [[99, 2], [3, 4]]
print(shallow)    # [[99, 2], [3, 4]] ← affected!
print(deep)       # [[1, 2], [3, 4]]  ← NOT affected
```

---

### Q15: What is a Python generator?

A generator produces values **one at a time** using `yield` instead of `return`. It is memory-efficient for large datasets.

```python
def count_up(n):
    for i in range(n):
        yield i

gen = count_up(5)

for value in gen:
    print(value)
```

**Output:**
```
0
1
2
3
4
```

Unlike a list, which creates all values at once, a generator creates each value only when needed.

---

### Q16: Explain inheritance in Python.

Inheritance allows a **child class** to inherit attributes and methods from a **parent class**.

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        print(self.name, "makes a sound")

class Dog(Animal):    # Dog inherits from Animal
    def speak(self):  # Override parent method
        print(self.name, "says: Woof!")

class Cat(Animal):
    def speak(self):
        print(self.name, "says: Meow!")

dog = Dog("Rex")
cat = Cat("Whiskers")

dog.speak()   # Rex says: Woof!
cat.speak()   # Whiskers says: Meow!
```

---

### Q17: What is the GIL (Global Interpreter Lock)?

The **GIL** is a mutex (lock) in CPython (the standard Python implementation) that allows only **one thread** to execute Python bytecode at a time. This means Python threads do not run truly in parallel for CPU-bound tasks.

**Impact:**
- Good for I/O-bound tasks (file reading, web requests)
- Limiting for CPU-heavy parallel computing
- Solution: Use `multiprocessing` module for true parallelism

---

### Q18: What is the difference between `range()` and `xrange()`?

- In **Python 3**, `xrange()` **no longer exists**. `range()` behaves like Python 2's `xrange()`.
- `range()` in Python 3 is **lazy** — it generates numbers on demand without creating a full list in memory.

```python
r = range(1_000_000)  # Does NOT create 1 million numbers in memory immediately
print(r[0])   # 0 — only computed when accessed
```

---

### Q19: How does Python manage memory?

Python uses:
1. **Reference counting** — tracks how many variables point to an object
2. **Garbage collection** — cleans up objects with circular references
3. **Memory pools** — reuses freed memory for efficiency

When no variable references an object, Python automatically frees its memory.

---

### Q20: What is `__init__` in a class?

`__init__` is the **constructor method** — it runs automatically when an object is created from a class.

```python
class Car:
    def __init__(self, brand, model, year):
        self.brand = brand
        self.model = model
        self.year = year

    def describe(self):
        print(f"{self.year} {self.brand} {self.model}")

car1 = Car("Toyota", "Corolla", 2022)
car1.describe()   # 2022 Toyota Corolla
```

---

# Part 10: Mini-Project — Python Practice Consolidator

This mini-project combines everything from this lesson into one working program.

---

## 🛠️ Project: Student Data Processor

**Goal:** Build a program that:
1. Stores student names and their test scores
2. Removes any duplicate names
3. Calculates averages
4. Assigns letter grades
5. Displays a formatted report
6. Finds the top student

---

### Stage 1: Setup Data

```python
# Stage 1: Create student data
students_raw = [
    {"name": "Alice", "scores": [85, 92, 78]},
    {"name": "Bob", "scores": [70, 65, 80]},
    {"name": "Carol", "scores": [95, 98, 91]},
    {"name": "Alice", "scores": [85, 92, 78]},   # duplicate
    {"name": "Dave", "scores": [60, 55, 70]},
]

print("Raw student count:", len(students_raw))
```

**Output:**
```
Raw student count: 5
```

---

### Stage 2: Remove Duplicate Names

```python
# Stage 2: Remove duplicate students by name
seen_names = []
students = []

for student in students_raw:
    if student["name"] not in seen_names:
        seen_names.append(student["name"])
        students.append(student)

print("After removing duplicates:", len(students), "students")
```

**Output:**
```
After removing duplicates: 4 students
```

---

### Stage 3: Calculate Averages and Assign Grades

```python
# Stage 3: Add average and grade to each student
def get_grade(average):
    if average >= 90:
        return "A"
    elif average >= 80:
        return "B"
    elif average >= 70:
        return "C"
    elif average >= 60:
        return "D"
    else:
        return "F"

for student in students:
    avg = sum(student["scores"]) / len(student["scores"])
    student["average"] = round(avg, 1)
    student["grade"] = get_grade(avg)
```

---

### Stage 4: Display Report

```python
# Stage 4: Print formatted report
print("\n" + "="*40)
print("      STUDENT PERFORMANCE REPORT")
print("="*40)

for student in students:
    print(f"Name:    {student['name']}")
    print(f"Scores:  {student['scores']}")
    print(f"Average: {student['average']}")
    print(f"Grade:   {student['grade']}")
    print("-"*40)
```

---

### Stage 5: Find Top Student

```python
# Stage 5: Find top performer
top_student = max(students, key=lambda s: s["average"])

print(f"\n🏆 Top Student: {top_student['name']}")
print(f"   Average: {top_student['average']} | Grade: {top_student['grade']}")
```

---

### Complete Output:

```
Raw student count: 5
After removing duplicates: 4 students

========================================
      STUDENT PERFORMANCE REPORT
========================================
Name:    Alice
Scores:  [85, 92, 78]
Average: 85.0
Grade:   B
----------------------------------------
Name:    Bob
Scores:  [70, 65, 80]
Average: 71.7
Grade:   C
----------------------------------------
Name:    Carol
Scores:  [95, 98, 91]
Average: 94.7
Grade:   A
----------------------------------------
Name:    Dave
Scores:  [60, 55, 70]
Average: 61.7
Grade:   D
----------------------------------------

🏆 Top Student: Carol
   Average: 94.7 | Grade: A
```

---

### Optional Enhancements

- Save the report to a `.txt` file
- Add a function to reverse each student's name (practice string reversal)
- Sort students by average (highest first)
- Calculate class average across all students
- Count how many students passed (grade C or above)

---

# Part 11: Common Beginner Mistakes

These are the most frequent errors Python beginners make. Learn them now to avoid frustration later.

---

### Mistake 1: Forgetting to Convert Input

```python
# ❌ Wrong
age = input("Enter age: ")
next_year = age + 1        # TypeError: can only concatenate str (not "int") to str

# ✅ Correct
age = int(input("Enter age: "))
next_year = age + 1
print(next_year)
```

---

### Mistake 2: Off-by-One in range()

```python
# ❌ Wrong — wants to print 1 to 10 but...
for i in range(10):
    print(i)    # Prints 0 to 9! Not 1 to 10.

# ✅ Correct
for i in range(1, 11):
    print(i)    # Prints 1 to 10
```

---

### Mistake 3: Modifying a List While Iterating

```python
# ❌ Wrong — skips items
nums = [1, 2, 3, 4, 5]
for n in nums:
    if n % 2 == 0:
        nums.remove(n)   # Unexpected behaviour

# ✅ Correct — iterate over a copy
nums = [1, 2, 3, 4, 5]
for n in nums[:]:
    if n % 2 == 0:
        nums.remove(n)

print(nums)   # [1, 3, 5]
```

---

### Mistake 4: Using `=` Instead of `==` in Conditions

```python
# ❌ Wrong — assignment, not comparison
if x = 5:     # SyntaxError

# ✅ Correct — comparison
if x == 5:
    print("x is 5")
```

---

### Mistake 5: Forgetting Indentation

```python
# ❌ Wrong
def greet():
print("Hello")   # IndentationError

# ✅ Correct
def greet():
    print("Hello")
```

Python uses **indentation** (spaces or tabs) to define code blocks. This is mandatory, not optional.

---

### Mistake 6: Confusing Append vs Extend

```python
# ❌ If you want to add items individually
my_list = [1, 2, 3]
my_list.append([4, 5])     # Adds a nested list: [1, 2, 3, [4, 5]]

# ✅ Use extend to add items individually
my_list = [1, 2, 3]
my_list.extend([4, 5])     # Adds items: [1, 2, 3, 4, 5]
```

---

### Mistake 7: Mutable Default Arguments in Functions

```python
# ❌ Wrong — the list persists between calls!
def add_item(item, lst=[]):
    lst.append(item)
    return lst

print(add_item("a"))   # ['a']
print(add_item("b"))   # ['a', 'b'] ← Bug! Expected ['b']

# ✅ Correct — use None as default
def add_item(item, lst=None):
    if lst is None:
        lst = []
    lst.append(item)
    return lst
```

---

# Part 12: Reflection Questions

Use these questions to deepen your understanding. Write your answers in a notebook or try them in code.

1. What are three different ways to remove duplicates from a list? When would you choose one over another?

2. What is the difference between `text[::-1]` and `reversed(text)`? When might you prefer each?

3. Why does Python's `input()` always return a string? What would happen if you forgot to convert it?

4. You have a list `[1, 2, 3, 4, 5]`. What does `my_list[-2]` return? Why?

5. What is the difference between a `for` loop and a `while` loop? Give a real-world example where each is more appropriate.

6. Why might a set be faster than a list for checking if an item exists?

7. In an interview, you are asked to write FizzBuzz. What is your approach? Write it out.

8. What is the purpose of `__init__` in a class? What would happen if you left it out?

9. If you were building a data analysis pipeline, which Python libraries would you use and why?

10. Looking at the 8-week study plan: which week do you think will be the hardest for you? Why? What can you do to prepare?

---

# Part 13: Completion Checklist

Use this checklist to confirm you have mastered Lesson 45.

- [ ] I can remove duplicates from a list using at least two different methods
- [ ] I can reverse a string using slicing `[::-1]`
- [ ] I can check if a word is a palindrome
- [ ] I can add two numbers entered by the user (handling type conversion)
- [ ] I can write a for loop and a while loop
- [ ] I can define a function with parameters and a return value
- [ ] I can use a dictionary to store and retrieve key-value data
- [ ] I completed at least 5 exercises from Part 3
- [ ] I attempted at least 3 challenges from Part 5
- [ ] I answered at least 5 quiz questions correctly
- [ ] I completed (or planned) the Student Data Processor mini-project
- [ ] I reviewed the full Python syllabus and know where I am in it
- [ ] I have a personal study schedule based on the 8-week plan
- [ ] I reviewed the interview questions and can answer 10+ without help
- [ ] I identified my 3 most common beginner mistakes and know how to fix them

---

# Lesson Summary

Congratulations! You have completed **Lesson 45** — the most comprehensive consolidation lesson of your Python journey.

Here is everything you covered:

| Section | What You Learned |
|---|---|
| **How-To: Remove Duplicates** | `set()`, loops, `dict.fromkeys()` |
| **How-To: Reverse a String** | `[::-1]`, `reversed()`, loops, palindrome check |
| **How-To: Add Two Numbers** | `input()`, `int()`, `float()`, `sum()` |
| **Python Examples** | Strings, lists, dicts, loops, functions, classes, files |
| **Exercises** | Variables, strings, lists, loops, functions |
| **Quiz** | 10 knowledge-check questions with answers |
| **Challenges** | Word frequency, Fibonacci, prime check, anagram, missing number |
| **Practice Tasks** | Grade tracker, shopping cart, number game |
| **Syllabus** | Complete 7-module Python learning map |
| **Study Plan** | 8-week schedule from beginner to advanced |
| **Interview Questions** | 20 beginner-to-intermediate Q&As |
| **Mini-Project** | Student Data Processor combining all concepts |
| **Common Mistakes** | 7 critical beginner errors with fixes |

---

> 🎓 **Next Steps:**
> - Follow the 8-week study plan systematically
> - Practice on real coding platforms (HackerRank, LeetCode, CodeWars)
> - Build personal projects that solve real problems you care about
> - Review Python documentation at [docs.python.org](https://docs.python.org)
> - Keep this lesson as a reference — return to it whenever you need a reminder

**You now have the knowledge, the practice, the roadmap, and the interview preparation to move forward as a confident Python programmer. The rest is practice. Write code every day, even if it's just 15 minutes. Small daily actions build unstoppable skill.**
