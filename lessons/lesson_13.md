---
render_with_liquid: false
title: "Lesson 13: Advanced Conditionals — Shorthand If, Logical Operators, Nested If, Pass, and Match"
nav_order: 13
---

# Lesson 13: Advanced Conditionals — Shorthand If, Logical Operators, Nested If, Pass, and Match

---

## Lesson Introduction

Welcome to Lesson 13! So far you have been making decisions in Python using `if`, `elif`, and `else`. That is a great start. Now we are going to go deeper and discover five powerful tools that professional Python developers use every single day.

By the end of this lesson you will be able to:

- Write single-line `if` and `if/else` statements using Python shorthand
- Use the ternary (conditional expression) pattern to assign values in one line
- Combine multiple conditions with the logical operators `and`, `or`, and `not`
- Write `if` statements inside other `if` statements (nested conditions)
- Use the `pass` keyword as a safe placeholder when a code block is intentionally left empty
- Use the `match` statement to compare a single value against many possible options cleanly

These tools will make your code shorter, cleaner, and more professional — like the programs used to build Nigerian fintech apps, university portals, and school management systems.

---

## Prerequisite Concepts Recap

Before we begin, let us quickly review what you already know:

- **Variables** store values, for example: `score = 85`
- **Booleans** are `True` or `False` values
- **Comparison operators** compare values: `>`, `<`, `>=`, `<=`, `==`, `!=`
- **`if` / `elif` / `else`** — You already know how to make decisions over multiple lines

> **Quick reminder:** Every `if` block in Python must have at least one statement inside it. An empty block causes a `SyntaxError`. You will learn how `pass` solves this problem later in this lesson.

---

## Section 1: Shorthand If (One-Line If)

### What Is It and Why Does It Exist?

Normally when you write an `if` statement, you split it across two or more lines:

```python
score = 75
if score >= 50:
    print("You passed!")
```

This is perfectly fine. But sometimes, when the condition and the action are very simple, Python allows you to write the entire thing on a single line. This is called a **shorthand if** or **one-line if**.

Think of it like this: instead of writing "If the weather is fine, go outside" in two separate sentences, you can say it in one breath.

**Why use it?**
- It saves lines of code when the logic is simple
- It makes the code feel more natural for quick checks
- It is widely used in real Python projects for short guards and checks

> **Important rule:** You still need the colon (`:`) after the condition — even in a single line.

### Syntax

```
if condition: action
```

### Example 1: Simple One-Line If

```python
a = 5
b = 2
if a > b: print("a is greater than b")
```

**Expected output:**
```
a is greater than b
```

**Breaking it down line by line:**
- `a = 5` — we store the number 5 in a variable called `a`
- `b = 2` — we store 2 in `b`
- `if a > b:` — Python checks: is 5 greater than 2? Yes, it is `True`
- `print("a is greater than b")` — this runs immediately because the condition was `True`

> **Thinking prompt:** What would happen if `a = 1` and `b = 5`? Would anything be printed? Why not?

---

## Section 2: Shorthand If...Else (The Ternary Operator / Conditional Expression)

### What Is It and Why Does It Exist?

A **ternary operator** (also called a **conditional expression**) lets you write a full `if/else` choice on a single line. You use it when you want Python to pick between two outcomes based on a condition.

**Real-world analogy:** Think of it like asking "Will I order jollof rice or fried rice?" — you pick one based on what is available. In Python, you pick one value or action based on whether a condition is `True` or `False`.

### Syntax for Printing

```
print(value_if_true) if condition else print(value_if_false)
```

### Example 2: One-Line If/Else Printing

```python
a = 2
b = 330
print("A") if a > b else print("B")
```

**Expected output:**
```
B
```

**Breaking it down:**
- `a = 2`, `b = 330` — set up the two numbers
- `a > b` — is 2 greater than 330? No. So the condition is `False`
- Because it is `False`, Python runs `print("B")` (the `else` side)

---

### Syntax for Assigning a Value

The ternary is even more powerful when you use it to **assign a value to a variable**:

```
variable = value_if_true if condition else value_if_false
```

Think of this as: "Give me X if the condition is met, otherwise give me Y."

### Example 3: Assigning a Value With Ternary

```python
a = 10
b = 20
bigger = a if a > b else b
print("Bigger is", bigger)
```

**Expected output:**
```
Bigger is 20
```

**Breaking it down:**
- `a > b` checks if 10 > 20 → `False`
- Since it is `False`, Python picks `b` (which is 20) and stores it in `bigger`
- `print("Bigger is", bigger)` outputs the result

### Example 4: Setting a Default Value

This is very common in real apps — if a user does not supply a name, you show "Guest" instead:

```python
username = ""
display_name = username if username else "Guest"
print("Welcome,", display_name)
```

**Expected output:**
```
Welcome, Guest
```

**Breaking it down:**
- `username = ""` — an empty string is **falsy** in Python (it evaluates as `False`)
- `username if username` — since `username` is empty/falsy, this condition fails
- Python picks `"Guest"` (the else side)
- This pattern protects your app from crashing when a field is empty

> **Thinking prompt:** What would happen if you set `username = "Amaka"`? What would be printed then?

---

### Example 5: Chained Ternary (Three Outcomes in One Line)

You can chain ternary expressions to get three possible outcomes:

```python
a = 330
b = 330
print("A") if a > b else print("=") if a == b else print("B")
```

**Expected output:**
```
=
```

**Breaking it down:**
- First check: is `a > b`? (330 > 330) → `False`
- Second check: is `a == b`? (330 == 330) → `True`
- Since `True`, print `"="`

> **Important note:** Chained ternaries can become hard to read. Use them only when the logic stays simple. For three or more conditions with complex logic, use a regular `if/elif/else` block.

### When Should You Use Shorthand If?

Use shorthand if and the ternary when:
- The condition is very simple (one comparison)
- The action is just one short statement
- You want to assign one of two values to a variable
- Readability is not sacrificed

**Do NOT use it for complex multi-line logic** — regular `if/else` is cleaner in those cases.

---

## Section 3: Logical Operators — `and`, `or`, `not`

### What Are Logical Operators and Why Do They Exist?

Imagine you are at a supermarket entrance in Lagos. The sign says: "You may enter if you are wearing a mask AND have your receipt." Both conditions must be true at the same time.

Or another sign: "This lane is for senior citizens OR pregnant women." Only one needs to be true.

**Logical operators** let you combine multiple conditions in a single `if` statement. Without them, you would need to nest `if` inside `if` for every extra condition — which gets messy quickly.

Python has three logical operators:

| Operator | Meaning | Returns `True` when… |
|----------|---------|----------------------|
| `and` | Both must be true | Both conditions are `True` |
| `or` | At least one must be true | At least one condition is `True` |
| `not` | Reverses the result | The condition is `False` |

---

### 3.1 The `and` Operator

`and` returns `True` **only** when **both** conditions are `True`. If either one is `False`, the whole expression is `False`.

**Real-world analogy:** You can only withdraw money from your account if (1) you have enough balance AND (2) your PIN is correct. Both must be true.

### Example 6: `and` — Both Conditions True

```python
a = 200
b = 33
c = 500
if a > b and c > a:
    print("Both conditions are True")
```

**Expected output:**
```
Both conditions are True
```

**Breaking it down:**
- `a > b` → is 200 > 33? → `True`
- `c > a` → is 500 > 200? → `True`
- `True and True` → `True` → the body runs

### Example 7: `and` — One Condition is False

```python
score = 85
attendance = 60
if score >= 50 and attendance >= 75:
    print("Eligible for exam")
else:
    print("Not eligible — check attendance")
```

**Expected output:**
```
Not eligible — check attendance
```

**Breaking it down:**
- `score >= 50` → 85 >= 50 → `True`
- `attendance >= 75` → 60 >= 75 → `False`
- `True and False` → `False` → the `else` block runs

---

### 3.2 The `or` Operator

`or` returns `True` if **at least one** condition is `True`. It only returns `False` when **all** conditions are `False`.

**Real-world analogy:** You can get a student discount if you have a student ID OR if you show your school letter. Only one proof is enough.

### Example 8: `or` — At Least One True

```python
a = 200
b = 33
c = 500
if a > b or a > c:
    print("At least one of the conditions is True")
```

**Expected output:**
```
At least one of the conditions is True
```

**Breaking it down:**
- `a > b` → 200 > 33 → `True`
- `a > c` → 200 > 500 → `False`
- `True or False` → `True` (only one needs to be true) → body runs

### Example 9: Range Validation with `and`

Checking that a score is valid (between 0 and 100):

```python
score = 85

if score >= 0 and score <= 100:
    print("Valid score")
else:
    print("Invalid score")
```

**Expected output:**
```
Valid score
```

---

### 3.3 The `not` Operator

`not` **reverses** the result of a condition. If something is `True`, `not` makes it `False`, and vice versa.

**Real-world analogy:** A door that opens only when the alarm is NOT active.

### Example 10: `not` — Reversing a Condition

```python
a = 33
b = 200
if not a > b:
    print("a is NOT greater than b")
```

**Expected output:**
```
a is NOT greater than b
```

**Breaking it down:**
- `a > b` → 33 > 200 → `False`
- `not False` → `True`
- Since the overall result is `True`, the body runs

---

### 3.4 Truth Tables

A **truth table** shows every possible combination of `True`/`False` and the result. This is exactly how Python evaluates your conditions internally.

**`and` Truth Table:**

| Condition 1 | Condition 2 | Result |
|-------------|-------------|--------|
| `True` | `True` | `True` |
| `True` | `False` | `False` |
| `False` | `True` | `False` |
| `False` | `False` | `False` |

**`or` Truth Table:**

| Condition 1 | Condition 2 | Result |
|-------------|-------------|--------|
| `True` | `True` | `True` |
| `True` | `False` | `True` |
| `False` | `True` | `True` |
| `False` | `False` | `False` |

---

### 3.5 Combining Multiple Operators

You can use `and`, `or`, and `not` together. Python evaluates them in this order: **`not` first, then `and`, then `or`**.

To avoid confusion and make your code readable, use **parentheses** to group conditions.

### Example 11: Combined Operators with Parentheses

```python
temperature = 25
is_raining = False
is_weekend = True

if (temperature > 20 and not is_raining) or is_weekend:
    print("Great day for outdoor activities!")
```

**Expected output:**
```
Great day for outdoor activities!
```

**Breaking it down:**
- `temperature > 20` → `True`
- `not is_raining` → `not False` → `True`
- `True and True` → `True` (inside the parentheses)
- `True or is_weekend` → `True or True` → `True`
- Body runs

### Example 12: Login Validation (Real-World Pattern)

```python
username = "Emeka"
password = "secure123"
is_verified = True

if username and password and is_verified:
    print("Login successful")
else:
    print("Login failed")
```

**Expected output:**
```
Login successful
```

**Breaking it down:**
- `username` → `"Emeka"` is truthy (non-empty string → `True`)
- `password` → `"secure123"` is truthy → `True`
- `is_verified` → `True`
- `True and True and True` → `True` → body runs

> **Thinking prompt:** What would happen if `password = ""`? An empty string is falsy — so the login would fail. This is exactly how login systems check credentials.

---

## Section 4: Nested If Statements

### What Is Nesting and Why Does It Exist?

A **nested `if`** is an `if` statement placed inside another `if` statement. This lets you check a condition, and then — only if that first condition passes — check an even more specific condition.

**Real-world analogy:** Imagine a security checkpoint at a government building in Abuja. First, the guard checks: "Do you have a valid ID?" (outer condition). Only if you pass that check does the guard ask: "Are you on the appointment list?" (inner condition). The second question is pointless without clearing the first.

### Syntax

```python
if outer_condition:
    # this runs only if outer_condition is True
    if inner_condition:
        # this runs only if BOTH are True
    else:
        # this runs if outer is True but inner is False
else:
    # this runs if outer_condition is False
```

---

### Example 13: Basic Nested If

```python
x = 41

if x > 10:
    print("Above ten,")
    if x > 20:
        print("and also above 20!")
    else:
        print("but not above 20.")
```

**Expected output:**
```
Above ten,
and also above 20!
```

**Breaking it down:**
- `x > 10` → 41 > 10 → `True` → enter the outer block
- `print("Above ten,")` runs
- `x > 20` → 41 > 20 → `True` → enter the inner block
- `print("and also above 20!")` runs

> **Thinking prompt:** What would the output be if `x = 15`? The outer condition (> 10) is still true, but the inner (> 20) is false. So you would see "Above ten," and "but not above 20."

---

### Example 14: Age and Licence Check (Driving Eligibility)

```python
age = 25
has_licence = True

if age >= 18:
    if has_licence:
        print("You can drive")
    else:
        print("You need a licence")
else:
    print("You are too young to drive")
```

**Expected output:**
```
You can drive
```

**Breaking it down:**
- `age >= 18` → 25 >= 18 → `True` → enter outer block
- `has_licence` → `True` → enter inner block
- `print("You can drive")` runs

---

### Example 15: Three Levels of Nesting (Student Eligibility)

A university portal in Enugu checks three conditions before certifying a student:

```python
score = 85
attendance = 90
submitted = True

if score >= 60:
    if attendance >= 80:
        if submitted:
            print("Pass with good standing")
        else:
            print("Pass but missing assignment")
    else:
        print("Pass but low attendance")
else:
    print("Fail")
```

**Expected output:**
```
Pass with good standing
```

**Breaking it down:**
- Level 1: `score >= 60` → 85 >= 60 → `True` → enter
- Level 2: `attendance >= 80` → 90 >= 80 → `True` → enter
- Level 3: `submitted` → `True` → enter
- Output: "Pass with good standing"

> **Thinking prompt:** Change `submitted = False`. What output do you get?

---

### 4.1 Nested If vs. Logical Operators — Which Should You Use?

Sometimes you can express the same logic using `and` instead of nested `if`. Which is better?

**Option A — Nested If:**

```python
temperature = 25
is_sunny = True

if temperature > 20:
    if is_sunny:
        print("Perfect beach weather!")
```

**Option B — Using `and`:**

```python
temperature = 25
is_sunny = True

if temperature > 20 and is_sunny:
    print("Perfect beach weather!")
```

Both produce the same output:
```
Perfect beach weather!
```

**Rule of thumb:**
- Use `and` when both conditions are simple and equally important
- Use nested `if` when the inner logic is more complex, has its own `else`, or depends heavily on the outer condition

---

### Example 16: Grade with Extra Credit (Nested with elif)

```python
score = 92
extra_credit = 5

if score >= 90:
    if extra_credit > 0:
        print("A+ grade")
    else:
        print("A grade")
elif score >= 80:
    print("B grade")
else:
    print("C grade or below")
```

**Expected output:**
```
A+ grade
```

---

## Section 5: The `pass` Statement

### What Is `pass` and Why Does It Exist?

In Python, every code block must contain at least one statement. If you write an `if` statement but leave the body empty, Python will throw a **`SyntaxError`** (a crash at startup).

The `pass` keyword solves this. It is a **do-nothing placeholder** — it tells Python "yes, I know this block is here, I just haven't written the code for it yet."

**Real-world analogy:** Think of `pass` as a "Coming Soon" sign on a shop front. The shop structure is built and the sign is there, but the goods have not arrived yet.

---

### Example 17: The Problem Without `pass`

```python
# This will CRASH with IndentationError or SyntaxError:
a = 33
b = 200

if b > a:
    # forgot to put code here!
```

Python does NOT allow an empty code block. You must put something.

---

### Example 18: Solving It with `pass`

```python
a = 33
b = 200

if b > a:
    pass
```

**Expected output:**
```
(nothing — the program runs without error)
```

**Breaking it down:**
- `b > a` → 200 > 33 → `True` → enter the block
- `pass` → Python sees this, does absolutely nothing, and moves on
- No crash, no error

---

### Example 19: Using `pass` During Development

When you are planning a system — say, an Abuja transport fee calculator — you might sketch the structure first and fill it in later:

```python
age = 16

if age < 18:
    pass  # TODO: Add underage discount logic later
else:
    print("Full fare applies")
```

**Expected output:**
```
Full fare applies
```

This is extremely useful when building large programs. You outline all your conditions first, then fill them in one by one.

---

### 5.1 `pass` vs Comments — What Is the Difference?

This is a common beginner confusion.

```python
# This CRASHES — a comment alone does not count as a statement:
score = 85
if score > 90:
    # This is excellent
```

```python
# This WORKS — pass is an actual statement:
score = 85
if score > 90:
    pass  # This is excellent
print("Score processed")
```

**Expected output:**
```
Score processed
```

**Key difference:**
- A **comment** (`#`) is completely ignored by Python — it is for human readers only
- `pass` is an **actual Python statement** that gets executed (it just does nothing)

---

### Example 20: `pass` in a Multi-Branch Statement

```python
value = 50

if value < 0:
    print("Negative value")
elif value == 0:
    pass  # Zero case — no special action needed right now
else:
    print("Positive value")
```

**Expected output:**
```
Positive value
```

---

## Section 6: The `match` Statement

### What Is `match` and Why Does It Exist?

Imagine you have a variable — say, the number of a day of the week — and you want to do something different depending on which exact value it holds. You could write a long chain of `if/elif/elif/elif...` statements. But Python 3.10 introduced a much cleaner tool for this: the **`match` statement**.

The `match` statement is like a professional menu system:
- You present a value to the menu
- Python compares it against each "option" (called a `case`)
- When it finds a match, it runs that option's code
- If nothing matches, you can provide a default

**Real-world analogy:** Think of a USSD bank menu in Nigeria: Press 1 for Balance, Press 2 for Transfer, Press 3 for Airtime. Each number pressed triggers a specific action.

> **Note:** `match` was introduced in Python 3.10. Make sure you are using Python 3.10 or newer to use this feature.

---

### Syntax

```python
match expression:
    case value1:
        # code block
    case value2:
        # code block
    case _:
        # default — runs if nothing else matched
```

**How it works step by step:**
1. Python evaluates the `expression` once
2. It compares that value against each `case`, from top to bottom
3. When it finds a matching `case`, it runs that block and stops
4. `_` (underscore) acts as the "catch-all" default — like `else`

---

### Example 21: Days of the Week

```python
day = 4
match day:
    case 1:
        print("Monday")
    case 2:
        print("Tuesday")
    case 3:
        print("Wednesday")
    case 4:
        print("Thursday")
    case 5:
        print("Friday")
    case 6:
        print("Saturday")
    case 7:
        print("Sunday")
```

**Expected output:**
```
Thursday
```

**Breaking it down:**
- `day = 4`
- Python checks `case 1` → 4 ≠ 1 → skip
- Python checks `case 2` → 4 ≠ 2 → skip
- Python checks `case 3` → 4 ≠ 3 → skip
- Python checks `case 4` → 4 == 4 → **match!**
- `print("Thursday")` runs
- Python stops checking further

---

### 6.1 Default Case with `_`

If no `case` matches, Python does nothing by default. But you can add a catch-all case using `_` (underscore) — it matches anything that wasn't already matched.

**Always place `_` last**, because it will match everything.

### Example 22: Default with `_`

```python
day = 9
match day:
    case 6:
        print("Today is Saturday")
    case 7:
        print("Today is Sunday")
    case _:
        print("Looking forward to the Weekend")
```

**Expected output:**
```
Looking forward to the Weekend
```

**Breaking it down:**
- `day = 9`
- `case 6` → 9 ≠ 6 → skip
- `case 7` → 9 ≠ 7 → skip
- `case _` → this matches everything → runs

---

### 6.2 Combining Multiple Values with `|` (OR in Match)

You can check for more than one value in a single `case` using the pipe symbol `|`, which means "or" inside a `match` statement.

### Example 23: Weekday vs Weekend

```python
day = 4
match day:
    case 1 | 2 | 3 | 4 | 5:
        print("Today is a weekday")
    case 6 | 7:
        print("I love weekends!")
```

**Expected output:**
```
Today is a weekday
```

**Breaking it down:**
- `day = 4`
- `case 1 | 2 | 3 | 4 | 5` → does 4 match any of these? Yes! → runs

---

### 6.3 Guards — Adding `if` Conditions Inside `case`

You can add extra conditions to a `case` using a **guard** — an `if` statement written right inside the case line. The case only matches if the value matches AND the guard condition is `True`.

### Example 24: Weekday in a Specific Month

```python
month = 5
day = 4
match day:
    case 1 | 2 | 3 | 4 | 5 if month == 4:
        print("A weekday in April")
    case 1 | 2 | 3 | 4 | 5 if month == 5:
        print("A weekday in May")
    case _:
        print("No match")
```

**Expected output:**
```
A weekday in May
```

**Breaking it down:**
- `day = 4`
- First case: `day` is in 1–5 but `month == 4` → 5 ≠ 4 → guard fails → skip
- Second case: `day` is in 1–5 AND `month == 5` → 5 == 5 → guard passes → **match!**
- Output: "A weekday in May"

---

### 6.4 `match` vs `if/elif/else` — When Should You Use Which?

| Situation | Use |
|-----------|-----|
| Comparing one variable against many specific exact values | `match` |
| Checking ranges, complex logic, or combined conditions | `if/elif/else` |
| Checking two or three conditions only | `if/elif/else` |
| Building a menu system or command dispatcher | `match` |

---

## Guided Practice Exercises

### Exercise 1: Transport Fare Calculator (Shorthand + Ternary)

**Scenario:** You are building a quick bus fare checker for a Lagos ride-sharing app. If a passenger is a senior citizen (age 65 or above), they pay ₦200; otherwise they pay ₦500.

**Objective:** Use the ternary operator to assign the correct fare.

**Steps:**
1. Store the passenger's age in a variable
2. Use the ternary operator to assign the fare based on age
3. Print the result

**Solution:**

```python
age = 70
fare = 200 if age >= 65 else 500
print("Your fare is ₦", fare)
```

**Expected output:**
```
Your fare is ₦ 200
```

**Self-check questions:**
- What would the output be if `age = 30`?
- How would you extend this to also check if the passenger is a student (aged below 18)?

**What-if challenge:** Add a third condition — students (under 18) pay ₦150. Use a chained ternary or convert to `if/elif/else`.

---

### Exercise 2: Student Exam Eligibility (Logical Operators)

**Scenario:** A university in Lagos requires a student to meet THREE conditions before sitting for an exam: a minimum score of 40, attendance of at least 75%, and all assignments submitted.

**Objective:** Use `and` to check all three conditions at once.

**Steps:**
1. Store the three values as variables
2. Write a single `if` using `and` to check all three
3. Print an appropriate message for pass and fail

**Solution:**

```python
score = 55
attendance = 80
assignments_submitted = True

if score >= 40 and attendance >= 75 and assignments_submitted:
    print("Eligible to sit for the exam")
else:
    print("Not eligible. Check requirements.")
```

**Expected output:**
```
Eligible to sit for the exam
```

**Self-check questions:**
- What would happen if `attendance = 60`?
- Why is `and` more appropriate here than `or`?

**What-if challenge:** Change it so a student can ALSO be eligible if they have a letter from the Dean's office (`has_deans_letter = True`), even if they don't meet all three conditions. Which operator would you add?

---

### Exercise 3: Bank Account Access Checker (Nested If)

**Scenario:** A Nigerian bank app checks access in two stages. First: is the account active? If yes, it then checks: is the PIN correct?

**Objective:** Use nested `if` to model this two-stage check.

**Steps:**
1. Set `account_active` and `correct_pin` variables
2. Write an outer `if` for account status
3. Write an inner `if` for PIN verification
4. Handle all four possible combinations with appropriate messages

**Solution:**

```python
account_active = True
correct_pin = False

if account_active:
    if correct_pin:
        print("Access granted. Welcome!")
    else:
        print("Wrong PIN. Please try again.")
else:
    print("Account is inactive. Contact your branch.")
```

**Expected output:**
```
Wrong PIN. Please try again.
```

**Self-check questions:**
- What message appears when `account_active = False`?
- Could you rewrite this using `and`? What would you lose?

---

### Exercise 4: Jollof Rice Order System with `match`

**Scenario:** A popular bukka (restaurant) in Abuja takes orders by number. You are building their ordering system.

**Objective:** Use `match` to print the correct dish based on the order number.

**Steps:**
1. Set an order number variable
2. Write a `match` statement with cases for dishes 1–4
3. Add a default `_` case for invalid orders
4. Add a lunch-hour guard for premium dishes

**Solution:**

```python
order = 3
is_lunch_hour = True

match order:
    case 1:
        print("You ordered: Jollof Rice")
    case 2:
        print("You ordered: Fried Rice")
    case 3 if is_lunch_hour:
        print("You ordered: Egusi Soup (Lunch Special!)")
    case 3:
        print("You ordered: Egusi Soup")
    case 4:
        print("You ordered: Pepper Soup")
    case _:
        print("Invalid order number. Please choose 1–4.")
```

**Expected output:**
```
You ordered: Egusi Soup (Lunch Special!)
```

**Self-check questions:**
- What prints if `order = 5`?
- What prints if `order = 3` but `is_lunch_hour = False`?

---

## Mini Project: Student Portal Decision System

### Project Overview

You are building the core decision engine for a secondary school portal in Lagos. The system automatically determines a student's status, recommends actions, and directs them to the right handler based on their data.

---

### Stage 1: Basic Eligibility Check

**Goal:** Determine if a student passed or failed using a one-line ternary.

```python
student_name = "Chidinma"
score = 68

result = "Passed" if score >= 50 else "Failed"
print(f"{student_name}: {result}")
```

**Milestone output:**
```
Chidinma: Passed
```

---

### Stage 2: Full Eligibility with Logical Operators

**Goal:** Check score, attendance, and assignment completion together.

```python
student_name = "Chidinma"
score = 68
attendance = 82
assignments_done = True

if score >= 50 and attendance >= 75 and assignments_done:
    print(f"{student_name} is eligible to proceed to the next term.")
else:
    print(f"{student_name} has unmet requirements. Please see your teacher.")
```

**Milestone output:**
```
Chidinma is eligible to proceed to the next term.
```

---

### Stage 3: Grade Classification with Nested If

**Goal:** After confirming eligibility, determine the student's exact grade.

```python
student_name = "Chidinma"
score = 68
attendance = 82
assignments_done = True

if score >= 50 and attendance >= 75 and assignments_done:
    print(f"{student_name} is eligible.")
    if score >= 80:
        print("Grade: A — Excellent")
    elif score >= 70:
        print("Grade: B — Very Good")
    elif score >= 60:
        print("Grade: C — Good")
    else:
        print("Grade: D — Pass")
else:
    print(f"{student_name} does not meet requirements.")
```

**Milestone output:**
```
Chidinma is eligible.
Grade: C — Good
```

---

### Stage 4: Portal Menu with `match`

**Goal:** After classification, direct the student to the correct portal section based on their status code.

```python
student_name = "Chidinma"
status_code = 2  # 1=Honours, 2=Pass, 3=Probation, 4=Expelled

match status_code:
    case 1:
        print(f"{student_name}: Congratulations! You are on the Honours List.")
    case 2:
        print(f"{student_name}: You passed. Collect your result slip from the office.")
    case 3:
        print(f"{student_name}: You are on academic probation. See your counsellor.")
    case 4:
        print(f"{student_name}: Account suspended. Visit the admin block.")
    case _:
        print(f"Unknown status code for {student_name}. Contact IT support.")
```

**Milestone output:**
```
Chidinma: You passed. Collect your result slip from the office.
```

---

### Stage 5: Full Portal System

**Goal:** Combine everything into one complete, working portal decision engine.

```python
student_name = "Chidinma"
score = 68
attendance = 82
assignments_done = True
has_fees_paid = True

# Step 1: Quick status check using ternary
quick_status = "Active" if has_fees_paid else "Fee Defaulter"
print(f"Account Status: {quick_status}")

# Step 2: Eligibility check using logical operators
if score >= 50 and attendance >= 75 and assignments_done:
    eligible = True
    print(f"{student_name} meets all academic requirements.")
else:
    eligible = False
    print(f"{student_name} does not meet requirements.")

# Step 3: Nested grading (only if eligible)
if eligible:
    if score >= 80:
        grade = "A"
        status_code = 1
    elif score >= 70:
        grade = "B"
        status_code = 2
    elif score >= 60:
        grade = "C"
        status_code = 2
    else:
        grade = "D"
        status_code = 3
    print(f"Grade: {grade}")
else:
    status_code = 3

# Step 4: Portal routing with match
match status_code:
    case 1:
        print("Honours List — Certificate ready for collection.")
    case 2:
        print("Standard Pass — Collect result slip at the office.")
    case 3:
        print("On Probation — Visit your academic adviser.")
    case _:
        print("Status unclear — Contact administration.")
```

**Final output:**
```
Account Status: Active
Chidinma meets all academic requirements.
Grade: C
Standard Pass — Collect result slip at the office.
```

**Reflection questions:**
- Which section of the code handles the "what if fees are not paid" case? How would you expand it?
- What would happen if `score = 40`? Trace through the code step by step.
- Could you replace the nested grading `if/elif` with a `match` + guards? Try it!

**Optional extension:** Add a `not` operator to show a warning if the student is NOT from the science department: `is_science = False`

---

## Common Beginner Mistakes

### Mistake 1: Forgetting the Colon in Shorthand If

**Wrong:**
```python
if a > b  print("yes")
```

**Correct:**
```python
if a > b: print("yes")
```

The colon is mandatory, even in one-line form.

---

### Mistake 2: Confusing `and` with `or`

**Wrong logic:**
```python
# Trying to allow senior citizens or students
age = 70
if age >= 65 and age <= 18:  # This will NEVER be True!
    print("Discount applies")
```

**Correct:**
```python
age = 70
if age >= 65 or age <= 18:
    print("Discount applies")
```

A person cannot be both 65+ AND 18 or younger at the same time. Use `or`.

---

### Mistake 3: Wrong Indentation in Nested If

**Wrong:**
```python
if x > 10:
print("Above 10")  # IndentationError — not indented!
    if x > 20:
        print("Above 20")
```

**Correct:**
```python
if x > 10:
    print("Above 10")
    if x > 20:
        print("Above 20")
```

Every level of nesting requires exactly 4 spaces of indentation.

---

### Mistake 4: Leaving an Empty If Block Without `pass`

**Wrong:**
```python
if age < 18:
    # handle later
```

This crashes because a comment alone is not a valid Python statement.

**Correct:**
```python
if age < 18:
    pass  # handle later
```

---

### Mistake 5: Putting the Default `_` Case First in `match`

**Wrong:**
```python
match day:
    case _:
        print("Unknown day")  # This runs IMMEDIATELY — other cases never checked
    case 1:
        print("Monday")
```

**Correct:**
```python
match day:
    case 1:
        print("Monday")
    case _:
        print("Unknown day")  # Always last
```

The `_` case is a catch-all. Place it LAST, just like `else`.

---

### Mistake 6: Using `=` Instead of `==` in Conditions

**Wrong:**
```python
if score = 85:  # SyntaxError — this is assignment, not comparison
    print("Pass")
```

**Correct:**
```python
if score == 85:  # == is comparison
    print("Pass")
```

---

### Mistake 7: Over-Nesting When `and` Would Be Cleaner

**Harder to read:**
```python
if is_active:
    if has_funds:
        if is_verified:
            print("Transaction approved")
```

**Cleaner:**
```python
if is_active and has_funds and is_verified:
    print("Transaction approved")
```

Use `and` when all conditions are at the same level of importance and there are no separate `else` branches needed.

---

## Reflection Questions

1. You need to assign "Day" or "Night" to a variable based on whether `hour` is less than 18. Write this using the ternary operator in one line.

2. A hospital system approves treatment only if: the patient has insurance (`has_insurance = True`) AND the doctor has confirmed the diagnosis (`doctor_confirmed = True`) OR the case is an emergency (`is_emergency = True`). Write the `if` condition using logical operators with parentheses.

3. What is the difference between `pass` and a `#` comment inside an `if` block? When do you actually need `pass`?

4. If you have a variable `command` that can be `"start"`, `"stop"`, `"pause"`, or anything else, which is cleaner — a `match` statement or an `if/elif/else` chain? Why?

5. Trace this code manually and write down the output:
```python
x = 15
y = 15
result = "X wins" if x > y else "Tie" if x == y else "Y wins"
print(result)
```

---

## Completion Checklist

Before moving to the next lesson, confirm you can:

- [ ] Write a one-line `if` statement using shorthand syntax
- [ ] Write a ternary expression to choose between two values
- [ ] Use `and` to require all conditions to be true
- [ ] Use `or` to require at least one condition to be true
- [ ] Use `not` to reverse a condition
- [ ] Write an `if` inside another `if` (nested)
- [ ] Explain when to prefer nested `if` over `and`
- [ ] Use `pass` to safely create an empty `if` block
- [ ] Explain why a comment alone cannot replace `pass`
- [ ] Write a `match` statement with multiple `case` options
- [ ] Add a default `_` case at the bottom of a `match`
- [ ] Combine multiple values in one `case` using `|`
- [ ] Add a guard (`if`) inside a `case`
- [ ] Identify common mistakes and know how to fix them

---

## Lesson Summary

In this lesson you expanded far beyond basic `if/else` into the full toolkit of Python conditional programming:

**Shorthand If** — Write simple one-line `if` and `if/else` statements when the logic is short and readable.

**Ternary (Conditional Expression)** — Choose between two values or actions in a single line using `value_if_true if condition else value_if_false`.

**Logical Operators** — Combine conditions with `and` (both must be true), `or` (at least one must be true), and `not` (reverse the result). Use parentheses for clarity.

**Nested If** — Place `if` statements inside other `if` statements when decisions depend on each other. Prefer `and` for flat conditions; use nesting when inner logic needs its own `else`.

**`pass` Statement** — A safe, do-nothing placeholder that prevents `SyntaxError` in empty code blocks. Essential during development when sketching program structure.

**`match` Statement (Python 3.10+)** — A clean, readable alternative to long `if/elif` chains when comparing one variable against many exact values. Supports multiple values per case (`|`), a default case (`_`), and guards (inline `if` conditions).

Together, these tools give you precise, expressive control over how your Python programs make decisions — from a quick one-liner in a ride-hailing app to a full multi-stage portal system for a Nigerian university.

---

## Quick Reference Card

| Feature | Syntax | When to Use |
|---------|--------|-------------|
| Shorthand if | `if condition: action` | Simple one-action check |
| Ternary | `val1 if condition else val2` | Choose between two values/actions |
| `and` | `cond1 and cond2` | Both must be true |
| `or` | `cond1 or cond2` | At least one must be true |
| `not` | `not condition` | Reverse a condition |
| Nested if | `if a:` then inside `if b:` | Inner check depends on outer |
| `pass` | `if cond: pass` | Empty block placeholder |
| `match` basic | `match x: case y: ...` | One value vs many exact options |
| `match` default | `case _:` | Fallback for unmatched values |
| `match` multiple | `case 1 \| 2 \| 3:` | Multiple values, one action |
| `match` guard | `case x if condition:` | Value match + extra check |
