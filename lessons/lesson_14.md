---
render_with_liquid: false
title: "Lesson 14: Python While Loops, For Loops, and the range() Function"
nav_order: 14
---

# Lesson 14: Python While Loops, For Loops, and the `range()` Function

---

## Lesson Introduction

Welcome to Lesson 14! Today we are going to learn one of the most powerful ideas in programming: **loops**.

Imagine you are at the Balogun Market in Lagos and you need to count every customer who enters the shop. Would you write a separate line of code for each customer? No — that would take forever! Instead, you use a **loop**: a tool that tells Python to repeat a set of instructions automatically.

Python has **two types of loops**:

1. **The `while` loop** — keeps repeating as long as a condition is true
2. **The `for` loop** — repeats once for each item in a sequence (like a list, string, or range of numbers)

We will also learn about the **`range()` function**, which is Python's built-in tool for generating sequences of numbers. It works hand-in-hand with loops and is used everywhere in real Python code.

### What You Will Learn in This Lesson

By the end of this lesson, you will be able to:

- Explain what a loop is and why it is useful
- Write a `while` loop with a proper condition and counter
- Use `break` and `continue` to control loop behaviour
- Add an `else` block to both `while` and `for` loops
- Write a `for` loop that iterates over lists, strings, and ranges of numbers
- Use `range()` with one, two, or three arguments
- Loop through a string character by character
- Write nested loops (a loop inside a loop)
- Use the `pass` statement inside an empty loop
- Convert a `range` to a list and slice it
- Test membership in a `range` using `in`
- Use `len()` to get the number of elements in a `range`
- Build a practical mini-project using all three tools

---

## Prerequisite Concepts

Before we continue, let us quickly review ideas you have already learned. These concepts will appear throughout this lesson.

### Variables and Assignment

A variable stores a value. You set it with `=`.

```python
i = 1       # i is a variable holding the integer 1
name = "Adaeze"
```

### Conditions and Comparison Operators

A **condition** is a question that Python answers with `True` or `False`. You already know these from the `if` statement lesson.

| Operator | Meaning | Example | Result |
|---|---|---|---|
| `<` | Less than | `3 < 6` | `True` |
| `>` | Greater than | `7 > 10` | `False` |
| `==` | Equal to | `5 == 5` | `True` |
| `!=` | Not equal to | `4 != 4` | `False` |
| `<=` | Less than or equal | `6 <= 6` | `True` |
| `>=` | Greater than or equal | `8 >= 9` | `False` |

### The `print()` Function

You use `print()` to display a value or message on the screen.

```python
print("Good morning Lagos!")
print(42)
```

### Lists

A list is an ordered collection of items.

```python
foods = ["jollof rice", "egusi soup", "suya"]
```

You already know all of this. Now let us put it to work inside loops!

---

## Section 1: What Is a Loop?

### Why Does a Loop Exist?

Imagine Emeka is a teacher at a secondary school in Abuja. He wants to print the name of every student in his class. The class has 30 students. Without a loop, he would have to write 30 separate `print()` lines. That is tedious, error-prone, and wastes time.

A **loop** is an instruction that tells Python:

> *"Run this block of code repeatedly. Keep going until I tell you to stop."*

This is the core idea. Everything else in this lesson builds on top of it.

---

## Section 2: The `while` Loop

### What Is a `while` Loop?

A **`while` loop** checks a condition **before** every repetition. As long as the condition is `True`, the loop body keeps running. The moment the condition becomes `False`, the loop stops.

Think of it like a security guard at a Lagos bank: *"While the queue has customers, keep serving the next person."*

### The Syntax (Structure)

```python
while condition:
    # code to repeat
```

- `while` — the keyword that starts the loop
- `condition` — any True/False expression (just like in an `if` statement)
- `:` — the colon that opens the loop body
- indented code — the instructions that run on every repetition

### Simple Example 1: Count from 1 to 5

```python
i = 1
while i < 6:
    print(i)
    i += 1
```

**Expected Output:**
```
1
2
3
4
5
```

Let us go **line by line**:

- `i = 1` — We create a variable `i` and start it at 1. This is called the **counter variable** or **loop variable**.
- `while i < 6:` — Python checks: "Is `i` less than 6?" If yes, enter the loop. If no, skip it entirely.
- `print(i)` — Print the current value of `i`.
- `i += 1` — This means `i = i + 1`. We **increase** `i` by 1. This is called **incrementing** the counter.
- After `i += 1`, Python goes back to `while i < 6:` and checks the condition again.
- When `i` reaches 6, the condition `i < 6` becomes `False`, and the loop ends.

> **Very Important:** You **must** update the counter variable inside the loop (`i += 1`). If you forget, `i` stays at 1 forever, and the condition `i < 6` is always `True`. This creates an **infinite loop** — a loop that never stops. Your program will freeze!

### Simple Example 2: Countdown from 5 to 1

Let us count **down** this time:

```python
i = 5
while i > 0:
    print(i)
    i -= 1   # i -= 1 means i = i - 1 (decrement)
print("Liftoff!")
```

**Expected Output:**
```
5
4
3
2
1
Liftoff!
```

Notice: the `print("Liftoff!")` line is **not** indented, so it runs **after** the loop finishes.

> 💡 **Thinking Prompt:** What happens if you change `i = 5` to `i = 3`? How many times will the loop run?

---

## Section 3: Controlling `while` Loops — `break`, `continue`, and `else`

### 3.1 The `break` Statement

The `break` keyword **immediately exits** the loop — even if the condition is still `True`. It is like an emergency exit.

**Real-life analogy:** Imagine Ngozi is sampling bottles of groundnut oil in a warehouse. She checks each bottle. The moment she finds a bad one, she **breaks** — she stops checking and reports the problem immediately.

#### Example: Stop the loop when `i` equals 3

```python
i = 1
while i < 6:
    print(i)
    if i == 3:
        break
    i += 1
```

**Expected Output:**
```
1
2
3
```

**Line-by-line explanation:**
- The loop starts with `i = 1` and counts up.
- On each repetition, it prints `i`, then checks `if i == 3`.
- When `i` becomes 3, Python hits `break` and immediately exits the loop.
- The numbers 4 and 5 are never printed.

> ⚠️ Notice that `i += 1` is **after** the `if` check. So when `i` is 3, Python prints 3, then hits `break`, and never reaches `i += 1`.

---

### 3.2 The `continue` Statement

The `continue` keyword **skips the rest of the current repetition** and jumps back to check the condition again. It does not exit the loop — it just skips one turn.

**Real-life analogy:** Amaka is reading through 10 exam papers. Whenever she sees a blank paper, she `continue`s — she skips it and moves on to the next one, without stopping the whole process.

#### Example: Skip number 3, print everything else from 1 to 5

```python
i = 0
while i < 6:
    i += 1
    if i == 3:
        continue
    print(i)
```

**Expected Output:**
```
1
2
4
5
6
```

**Careful study of this code:**
- `i = 0` — We start at 0 this time.
- `i += 1` — This is the **first line inside the loop**. It increments `i` before anything else.
- `if i == 3: continue` — When `i` is 3, Python jumps back to `while i < 6:` without reaching `print(i)`.
- All other values of `i` reach `print(i)` and get printed.

> 🔑 **Why does `i += 1` come before the `if` check here?** Because if `i += 1` were after `continue`, we would never increment `i` when `i == 3`. That would create an infinite loop! Always plan where your increment goes.

---

### 3.3 The `else` Statement in a `while` Loop

Python allows you to attach an `else` block to a `while` loop. The `else` block runs **once** — right after the loop condition becomes `False` (i.e., when the loop ends naturally).

**Important rule:** The `else` block does **NOT** run if the loop ends with `break`.

#### Example: Count from 1 to 5, then announce the end

```python
i = 1
while i < 6:
    print(i)
    i += 1
else:
    print("i is no longer less than 6")
```

**Expected Output:**
```
1
2
3
4
5
i is no longer less than 6
```

#### Example: The `else` block does NOT run after `break`

```python
i = 1
while i < 6:
    print(i)
    if i == 3:
        break
    i += 1
else:
    print("This will NOT print because break was used!")
```

**Expected Output:**
```
1
2
3
```

The `else` block is skipped entirely because `break` ended the loop.

> 💡 **Real-world use:** The `while-else` pattern is great for search tasks. Loop while searching; if found, `break`. The `else` block runs only if you finished searching without finding it — which means "not found."

---

## Section 4: The `for` Loop

### What Is a `for` Loop?

A **`for` loop** is used to **iterate** over a sequence. "Iterate" means to go through each item, one by one.

Think of it like Fatimah checking every stall at a market. She visits **each** stall — no more, no less — and does something at each one.

A `for` loop works on:
- Lists
- Tuples
- Strings (every character is treated as a single item)
- Dictionaries
- Sets
- Ranges (we will cover this soon)

The **key difference from `while`:** A `for` loop does not need you to manage a counter variable manually. Python automatically picks up the next item from the sequence on each turn.

### The Syntax

```python
for variable in sequence:
    # code to run for each item
```

- `for` — keyword that starts the loop
- `variable` — a name you choose; Python puts the current item here on each turn
- `in` — keyword connecting the variable to the sequence
- `sequence` — the list, string, or range to loop through
- `:` — opens the loop body
- indented code — runs once for every item

### Simple Example 1: Loop through a list of Nigerian foods

```python
foods = ["jollof rice", "egusi soup", "suya", "puff puff"]
for food in foods:
    print(food)
```

**Expected Output:**
```
jollof rice
egusi soup
suya
puff puff
```

**What is happening here?**
- On Turn 1: Python sets `food = "jollof rice"` and runs `print(food)`.
- On Turn 2: Python sets `food = "egusi soup"` and runs `print(food)`.
- This continues until every item in the list has been visited.
- The loop ends automatically. No `i += 1` needed!

### Simple Example 2: Loop through names

```python
names = ["Chidi", "Aisha", "Emeka", "Ngozi"]
for name in names:
    print("Hello,", name)
```

**Expected Output:**
```
Hello, Chidi
Hello, Aisha
Hello, Emeka
Hello, Ngozi
```

---

## Section 5: Looping Through a String

Strings are sequences of characters, so you can loop through them letter by letter.

### Example: Print each letter in a city name

```python
for letter in "Lagos":
    print(letter)
```

**Expected Output:**
```
L
a
g
o
s
```

On each turn, `letter` holds the next character in the string `"Lagos"`. After the last character `"s"`, the loop ends.

### Example: Count vowels in a word

```python
word = "Abuja"
vowels = "aeiouAEIOU"
count = 0

for letter in word:
    if letter in vowels:
        count += 1

print("Number of vowels:", count)
```

**Expected Output:**
```
Number of vowels: 3
```

(The vowels in "Abuja" are: A, u, a)

> 💡 **Thinking Prompt:** What would happen if you change `"Abuja"` to `"Kano"`? How many vowels does "Kano" have? Try to predict before running the code.

---

## Section 6: `break` and `continue` in `for` Loops

Just like in `while` loops, you can use `break` and `continue` inside `for` loops.

### 6.1 `break` in a `for` Loop

`break` exits the loop immediately when a condition is met.

#### Example 1: Stop when you find "banana"

```python
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
    if fruit == "banana":
        break
```

**Expected Output:**
```
apple
banana
```

The loop prints `"apple"`, then `"banana"`, then hits `break` and stops. `"cherry"` is never printed.

#### Example 2: Break BEFORE printing

```python
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    if fruit == "banana":
        break
    print(fruit)
```

**Expected Output:**
```
apple
```

Here, the `if` check comes **before** `print`. So when `fruit == "banana"`, Python breaks before ever printing `"banana"`.

> 💡 **Thinking Prompt:** Why does Example 1 print "banana" but Example 2 does not? What changed?

---

### 6.2 `continue` in a `for` Loop

`continue` skips the current item and moves to the next one.

#### Example: Print all fruits except "banana"

```python
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    if fruit == "banana":
        continue
    print(fruit)
```

**Expected Output:**
```
apple
cherry
```

When `fruit == "banana"`, Python hits `continue`, skips `print(fruit)`, and immediately goes to the next item in the list — which is `"cherry"`.

---

## Section 7: The `range()` Function

### Why Does `range()` Exist?

Imagine you want to print the numbers from 1 to 1000. You definitely do not want to type out a list of 1000 numbers! The `range()` function solves this: it generates a sequence of numbers automatically.

> **What is `range()`?**
> `range()` is a built-in Python function that returns an **immutable sequence of numbers**. "Immutable" means the sequence cannot be changed after it is created. It has its own special data type, also called `range`.

### The Syntax

```python
range(start, stop, step)
```

| Parameter | What it means | Is it required? | Default value |
|---|---|---|---|
| `start` | The first number in the sequence | Optional | `0` |
| `stop` | The sequence ends **before** this number | Required | — |
| `step` | How much to add each time | Optional | `1` |

### 7.1 `range()` with One Argument

When you call `range()` with only one number, that number is the **stop** value. The sequence starts at 0 and goes **up to but not including** the stop value.

```python
x = range(10)
print(list(x))
```

**Expected Output:**
```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

> ⚠️ `range(10)` gives you numbers 0 to **9**, not 0 to 10! The stop value is **exclusive** — it is not included.

> 💡 **Tip:** To display the contents of a `range`, we wrap it in `list()`. This converts it to a regular list that `print()` can show. You will learn more about this below.

### 7.2 `range()` with Two Arguments

When you call `range()` with two numbers, the first is **start** and the second is **stop**.

```python
x = range(3, 10)
print(list(x))
```

**Expected Output:**
```
[3, 4, 5, 6, 7, 8, 9]
```

The sequence starts at 3 and goes up to **9** (not 10).

### 7.3 `range()` with Three Arguments

When you call `range()` with three numbers, the third is the **step** — how much to add each time.

```python
x = range(2, 30, 3)
print(list(x))
```

**Expected Output:**
```
[2, 5, 8, 11, 14, 17, 20, 23, 26, 29]
```

Starting at 2, add 3 each time, stop before 30.

### 7.4 Using `range()` in a `for` Loop

This is the most common use of `range()`: to run a loop a specific number of times.

#### Example 1: Print numbers 0 to 5

```python
for x in range(6):
    print(x)
```

**Expected Output:**
```
0
1
2
3
4
5
```

#### Example 2: Print numbers 2 to 5 (using start and stop)

```python
for x in range(2, 6):
    print(x)
```

**Expected Output:**
```
2
3
4
5
```

#### Example 3: Print even numbers from 0 to 20 (using step)

```python
for x in range(0, 21, 2):
    print(x)
```

**Expected Output:**
```
0
2
4
6
8
10
12
14
16
18
20
```

#### Example 4: Count down using a negative step

```python
for x in range(10, 0, -1):
    print(x)
```

**Expected Output:**
```
10
9
8
7
6
5
4
3
2
1
```

When the step is **negative**, the sequence counts **down**. Start must be greater than stop for this to work.

---

## Section 8: Advanced `range()` — Converting, Slicing, Membership, and Length

### 8.1 Converting a `range` to a List

The `range` object itself is not a list — it just represents the numbers. To display all the values at once, convert it to a list using `list()`.

```python
print(list(range(5)))
print(list(range(1, 6)))
print(list(range(5, 20, 3)))
```

**Expected Output:**
```
[0, 1, 2, 3, 4]
[1, 2, 3, 4, 5]
[5, 8, 11, 14, 17]
```

### 8.2 Slicing a `range`

You can access individual elements of a `range` using index notation (just like a list), and you can also slice it.

```python
r = range(10)
print(r[2])     # the item at index 2
print(r[:3])    # a new range from index 0 up to (not including) 3
```

**Expected Output:**
```
2
range(0, 3)
```

- `r[2]` gives you the **value** at position 2, which is `2` (since the range starts at 0).
- `r[:3]` gives you a **new range object** — `range(0, 3)` — not a list.

### 8.3 Testing Membership with `in`

You can check whether a number is inside a `range` using the `in` operator.

```python
r = range(0, 10, 2)
print(list(r))
print(6 in r)
print(7 in r)
```

**Expected Output:**
```
[0, 2, 4, 6, 8]
True
False
```

- `6 in r` is `True` because 6 is in the sequence `[0, 2, 4, 6, 8]`.
- `7 in r` is `False` because 7 is not in that sequence (we skip odd numbers with step 2).

### 8.4 Getting the Length of a `range`

Use `len()` to find out how many numbers are in a range.

```python
r = range(0, 10, 2)
print(len(r))
```

**Expected Output:**
```
5
```

The range `[0, 2, 4, 6, 8]` has 5 numbers, so `len(r)` returns 5.

---

## Section 9: `else` in a `for` Loop

Just like with `while`, you can add an `else` block to a `for` loop. It runs **once** after the loop has finished iterating through all items — but only if the loop was not ended by a `break`.

### Example 1: Normal completion — `else` runs

```python
for x in range(6):
    print(x)
else:
    print("Finally finished!")
```

**Expected Output:**
```
0
1
2
3
4
5
Finally finished!
```

### Example 2: Loop broken early — `else` does NOT run

```python
for x in range(6):
    if x == 3:
        break
    print(x)
else:
    print("Finally finished!")
```

**Expected Output:**
```
0
1
2
```

The `else` block is skipped because `break` ended the loop at `x == 3`.

> 💡 **Real-world use:** This pattern is common in search tasks. You loop through a list looking for something. If you find it, you `break`. The `else` block runs only if you went through the entire list and never found it.

---

## Section 10: Nested Loops

A **nested loop** is a loop inside another loop. The inner loop runs **completely** for every single step of the outer loop.

**Real-life analogy:** Think of Damilola visiting every floor of a building in Lagos, and on each floor she knocks on every office door. For each floor (outer loop), she knocks on every door (inner loop).

### The Syntax

```python
for outer_item in outer_sequence:
    for inner_item in inner_sequence:
        # this code runs for every combination
```

### Example 1: Print combinations of colours and items

```python
colours = ["red", "green", "blue"]
items = ["bag", "shoe"]

for colour in colours:
    for item in items:
        print(colour, item)
```

**Expected Output:**
```
red bag
red shoe
green bag
green shoe
blue bag
blue shoe
```

For every colour (3 colours), Python goes through all items (2 items). Total combinations: 3 × 2 = 6 lines.

### Example 2: Multiplication table for 3 using nested loops

```python
for i in range(1, 4):        # outer loop: i goes 1, 2, 3
    for j in range(1, 6):    # inner loop: j goes 1, 2, 3, 4, 5
        print(i, "x", j, "=", i * j)
    print("---")             # printed after each inner loop finishes
```

**Expected Output:**
```
1 x 1 = 1
1 x 2 = 2
1 x 3 = 3
1 x 4 = 4
1 x 5 = 5
---
2 x 1 = 2
2 x 2 = 4
2 x 3 = 6
2 x 4 = 8
2 x 5 = 10
---
3 x 1 = 3
3 x 2 = 6
3 x 3 = 9
3 x 4 = 12
3 x 5 = 15
---
```

---

## Section 11: The `pass` Statement in Loops

A `for` loop (or `while` loop) **cannot be empty**. If you write a loop with no body, Python will give you a `SyntaxError`. But sometimes, while you are planning your code, you want to create a loop body you have not written yet. The `pass` statement acts as a placeholder.

```python
for x in [0, 1, 2]:
    pass
```

This runs without any output and without any errors. `pass` tells Python: "There is nothing to do here — just continue."

> 💡 This is useful when you are building a program in stages. You sketch out the loop first with `pass`, then come back to fill in the body later.

---

## Guided Practice Exercises

### Exercise 1: The Patient Bus Driver

**Scenario:** Alhaji Musa drives a danfo bus on the Lagos–Ibadan expressway. He wants to track how many trips he has made. He will keep driving until he completes 5 trips.

**Objective:** Use a `while` loop to simulate 5 bus trips.

**Steps:**
1. Create a variable `trips = 0`
2. Write a `while` loop that runs as long as `trips < 5`
3. Inside the loop, print the current trip number, then increment `trips`
4. After the loop, print "All trips complete!"

**Expected Output:**
```
Trip 1 in progress...
Trip 2 in progress...
Trip 3 in progress...
Trip 4 in progress...
Trip 5 in progress...
All trips complete!
```

**Solution:**

```python
trips = 0
while trips < 5:
    trips += 1
    print("Trip", trips, "in progress...")
else:
    print("All trips complete!")
```

**Self-check:**
- Did the loop run exactly 5 times?
- What would happen if you changed the condition to `trips < 10`?
- Did the `else` block print at the end?

---

### Exercise 2: Market Price Checker

**Scenario:** Adaeze is at Wuse Market in Abuja checking prices of vegetables. She has a list of prices in Naira. She wants to print each price, but skip any price that is exactly 500 (she thinks it is a pricing error).

**Objective:** Use a `for` loop with `continue` to skip a specific value.

**Steps:**
1. Create a list: `prices = [200, 350, 500, 420, 180, 500, 650]`
2. Write a `for` loop over `prices`
3. If the current price is 500, use `continue` to skip it
4. Otherwise, print the price

**Expected Output:**
```
200
350
420
180
650
```

**Solution:**

```python
prices = [200, 350, 500, 420, 180, 500, 650]

for price in prices:
    if price == 500:
        continue
    print(price)
```

**What-if challenge:** Change `continue` to `break`. What happens? Why?

---

### Exercise 3: Finding a Ripe Mango

**Scenario:** Chukwuemeka is checking a crate of mangoes to find the first ripe one. Once he finds it, he stops — he does not need to check the rest.

**Objective:** Use a `for` loop with `break` and the `for-else` pattern.

**Steps:**
1. Create a list: `mangoes = ["unripe", "unripe", "ripe", "unripe", "ripe"]`
2. Write a `for` loop over `mangoes` with an index using `range(len(mangoes))`
3. Print which position is being checked
4. If the mango is "ripe", print a success message and `break`
5. Add an `else` block that runs only if no ripe mango was found

**Solution:**

```python
mangoes = ["unripe", "unripe", "ripe", "unripe", "ripe"]

for i in range(len(mangoes)):
    print("Checking mango at position", i)
    if mangoes[i] == "ripe":
        print("Found a ripe mango at position", i, "!")
        break
else:
    print("No ripe mango found in this crate.")
```

**Expected Output:**
```
Checking mango at position 0
Checking mango at position 1
Checking mango at position 2
Found a ripe mango at position 2 !
```

**What-if challenge:** Change all mangoes to "unripe". Does the `else` block run now?

---

## Mini Project: Nigerian JAMB Score Analyser

In this project, you will build a simple tool that analyses JAMB exam scores for a group of students. You will use `for` loops, `range()`, `if` statements, and loops with `break`.

### Stage 1: Setup — Define the Student Scores

```python
students = [
    ("Emeka", 280),
    ("Aisha", 195),
    ("Chioma", 315),
    ("Tunde", 150),
    ("Ngozi", 260),
    ("Yusuf", 330)
]
```

Each item is a **tuple** containing a name and a score.

**Expected Output:** (nothing yet — we are setting up)

---

### Stage 2: Print All Scores

Use a `for` loop to print every student's name and score.

```python
print("=== JAMB Results ===")
for name, score in students:
    print(name, "->", score)
```

**Expected Output:**
```
=== JAMB Results ===
Emeka -> 280
Aisha -> 195
Chioma -> 315
Tunde -> 150
Ngozi -> 260
Yusuf -> 330
```

---

### Stage 3: Classify Each Score

Add a grade classification based on the score.

```python
print("\n=== Score Classification ===")
for name, score in students:
    if score >= 300:
        grade = "Excellent"
    elif score >= 250:
        grade = "Good"
    elif score >= 200:
        grade = "Pass"
    else:
        grade = "Below Cut-off"
    print(name, ":", score, "->", grade)
```

**Expected Output:**
```
=== Score Classification ===
Emeka : 280 -> Good
Aisha : 195 -> Below Cut-off
Chioma : 315 -> Excellent
Tunde : 150 -> Below Cut-off
Ngozi : 260 -> Good
Yusuf : 330 -> Excellent
```

---

### Stage 4: Calculate the Average Score

Use a `for` loop and `range()` to compute the average.

```python
total = 0
for name, score in students:
    total += score

average = total / len(students)
print("\nAverage Score:", average)
```

**Expected Output:**
```
Average Score: 255.0
```

---

### Stage 5: Find the Top Scorer

Loop through the students and track the highest score.

```python
top_name = ""
top_score = 0

for name, score in students:
    if score > top_score:
        top_score = score
        top_name = name

print("\nTop Scorer:", top_name, "with", top_score, "points")
```

**Expected Output:**
```
Top Scorer: Yusuf with 330 points
```

---

### Stage 6: Count Students Above Cut-off (using `range()`)

```python
cutoff = 200
above_cutoff = 0

for i in range(len(students)):
    name, score = students[i]
    if score >= cutoff:
        above_cutoff += 1

print("\nStudents above cut-off of", cutoff, ":", above_cutoff)
```

**Expected Output:**
```
Students above cut-off of 200 : 4
```

---

### Final Combined Output

```
=== JAMB Results ===
Emeka -> 280
Aisha -> 195
Chioma -> 315
Tunde -> 150
Ngozi -> 260
Yusuf -> 330

=== Score Classification ===
Emeka : 280 -> Good
Aisha : 195 -> Below Cut-off
Chioma : 315 -> Excellent
Tunde : 150 -> Below Cut-off
Ngozi : 260 -> Good
Yusuf : 330 -> Excellent

Average Score: 255.0

Top Scorer: Yusuf with 330 points

Students above cut-off of 200 : 4
```

**Extension Challenges:**
- Add a loop that counts how many students scored "Excellent".
- Use a `while` loop to let the user keep entering student names until they type "done".
- Use `range(len(students) - 1, -1, -1)` to print the results in reverse order.

---

## Common Beginner Mistakes

### Mistake 1: Forgetting to Increment in a `while` Loop

```python
# WRONG — infinite loop!
i = 1
while i < 6:
    print(i)
    # i never changes! i stays at 1 forever

# CORRECT
i = 1
while i < 6:
    print(i)
    i += 1   # always update the counter!
```

**How to spot it:** Your program prints the same number over and over and never stops. Press `Ctrl + C` to force-quit.

---

### Mistake 2: Off-by-One Error with `range()`

```python
# WRONG — only prints 1 to 4, not 1 to 5
for i in range(1, 5):
    print(i)

# CORRECT — to include 5, stop must be 6
for i in range(1, 6):
    print(i)
```

**Rule to remember:** `range(start, stop)` includes `start` but **excludes** `stop`. If you want to include a number `n`, write `range(1, n + 1)`.

---

### Mistake 3: Wrong Indentation in Loop Body

```python
# WRONG — the print is outside the loop!
for i in range(3):
    pass
print(i)   # this only runs once, after the loop

# CORRECT — print is inside the loop
for i in range(3):
    print(i)   # this runs 3 times
```

In Python, **indentation is everything**. The loop body must be indented (4 spaces or 1 tab) consistently.

---

### Mistake 4: Expecting `continue` to Exit the Loop

```python
# WRONG thinking — continue does NOT exit the loop
for i in range(5):
    if i == 3:
        continue   # this SKIPS 3, but the loop keeps going
    print(i)

# If you want to EXIT at 3, use break:
for i in range(5):
    if i == 3:
        break
    print(i)
```

---

### Mistake 5: Confusing `range(n)` with a List

```python
# WRONG — range is not a list; you cannot do this directly
r = range(5)
print(r)   # Output: range(0, 5) — NOT [0, 1, 2, 3, 4]

# CORRECT — convert to a list to see all values
print(list(r))   # Output: [0, 1, 2, 3, 4]
```

---

### Mistake 6: Empty `for` Loop Body

```python
# WRONG — this causes a SyntaxError
for x in range(5):
    # nothing here

# CORRECT — use pass as a placeholder
for x in range(5):
    pass
```

---

### Mistake 7: Expecting `else` to Run After `break`

```python
# WRONG expectation
for x in range(5):
    if x == 3:
        break
else:
    print("This runs!")   # This does NOT run after break

# The else block only runs if the loop completed WITHOUT break
```

---

## Reflection Questions

Take a moment to think through these questions. Try to answer them in your own words before checking your notes.

1. What is the key difference between a `while` loop and a `for` loop?
2. In a `while` loop, what happens if you forget to increment the counter variable?
3. What does `break` do? How is it different from `continue`?
4. What does `range(3, 15, 3)` produce? List the numbers without running the code.
5. Why does `range(10)` give you numbers 0–9 and not 1–10?
6. When does the `else` block in a loop run? When does it NOT run?
7. In a nested loop, how many times does the inner loop run in total if the outer loop runs 4 times and the inner loop runs 3 times each?
8. What is the purpose of the `pass` statement inside a loop?
9. How do you check if the number 15 is in `range(0, 30, 5)` without converting it to a list?
10. Why is `range()` more efficient than writing out a full list of numbers?

---

## Completion Checklist

Before moving to the next lesson, confirm you can do all of these:

- [ ] I can explain what a loop is in simple language
- [ ] I can write a `while` loop with a counter that increments correctly
- [ ] I can use `break` to exit a loop early
- [ ] I can use `continue` to skip one iteration
- [ ] I can attach an `else` block to both `while` and `for` loops and explain when it runs
- [ ] I can write a `for` loop that iterates over a list
- [ ] I can loop through the characters of a string
- [ ] I can use `range()` with 1, 2, and 3 arguments
- [ ] I can use a negative step in `range()` to count downward
- [ ] I can convert a `range` to a list with `list()`
- [ ] I can slice a `range` and access elements by index
- [ ] I can test membership in a `range` using `in`
- [ ] I can find the length of a `range` with `len()`
- [ ] I can write a nested `for` loop and explain how it works
- [ ] I can use `pass` in an empty loop body
- [ ] I completed the JAMB Score Analyser mini-project

---

## Lesson Summary

Congratulations! You have just mastered Python's three fundamental looping tools. Here is a recap of everything we covered:

**`while` loops** repeat a block of code as long as a condition is `True`. They require you to manage a counter variable manually. Always remember to increment the counter to avoid an infinite loop.

**`break`** immediately exits any loop. **`continue`** skips the current iteration and jumps to the next. Both work in `while` and `for` loops.

**`else` in loops** runs once after the loop ends naturally, but is skipped if `break` was used. This is useful for "not found" scenarios.

**`for` loops** iterate over every item in a sequence (lists, strings, tuples, ranges) without needing a manual counter. Python handles the stepping automatically.

**`range()`** generates sequences of numbers. It takes 1, 2, or 3 arguments (`start`, `stop`, `step`). The stop value is always excluded. It supports indexing, slicing, membership testing with `in`, and length with `len()`.

**Nested loops** are loops inside loops. The inner loop completes fully for each step of the outer loop.

**`pass`** is a placeholder for an empty loop body, preventing `SyntaxError`.

---

## Quick-Reference Card

| Feature | Syntax | Notes |
|---|---|---|
| `while` loop | `while condition:` | Runs while condition is `True`; needs manual counter |
| `for` loop | `for item in sequence:` | Iterates over every item automatically |
| `break` | `break` | Immediately exits the loop |
| `continue` | `continue` | Skips current iteration; continues to next |
| Loop `else` | `else:` after loop | Runs after loop ends, NOT after `break` |
| `range(n)` | `range(5)` → `0,1,2,3,4` | One argument: stop only; starts at 0 |
| `range(a, b)` | `range(2, 6)` → `2,3,4,5` | Two arguments: start and stop |
| `range(a, b, s)` | `range(0, 10, 2)` → `0,2,4,6,8` | Three arguments: start, stop, step |
| Negative step | `range(5, 0, -1)` → `5,4,3,2,1` | Counts downward |
| Convert range | `list(range(5))` | Shows all values in the range |
| Test membership | `7 in range(0, 10, 2)` → `False` | Checks if a number is in the range |
| Range length | `len(range(0, 10, 2))` → `5` | Count of numbers in the range |
| Nested loops | `for x in ...: for y in ...:` | Inner loop runs fully for each outer iteration |
| `pass` | `pass` | Placeholder for empty loop body |

---

*End of Lesson 14 — Next up: Python Functions*
