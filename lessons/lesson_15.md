---
render_with_liquid: false
title: "Python If...Else – Conditional Statements Complete Guide"
nav_order: 15
---

# Lesson 15: Python If…Else — Making Decisions in Code

---

## 📌 Lesson Introduction

Every useful program makes **decisions**. Should we let this user log in? Is the temperature high enough to turn on the fan? Did the student pass or fail? Has the shopping cart exceeded the budget limit?

In real life, you make hundreds of decisions every day without even thinking about it: *"If it is raining, I'll take an umbrella. Otherwise, I won't."* Python lets you give your programs the same power — the ability to **look at a situation and choose what to do**.

This entire ability is built on one simple idea: **conditional statements**, and the most fundamental one is the `if` statement.

By the end of this lesson, you will be able to:
- Write `if` statements to run code only when a condition is true
- Use `else` to handle the "otherwise" case
- Use `elif` to handle multiple different conditions in sequence
- Write compact one-line shorthand conditions
- Combine multiple conditions with `and`, `or`, and `not`
- Build nested `if` statements (decisions inside decisions)
- Use the `pass` statement as a placeholder
- Apply all of these in realistic exercises and a complete mini project

Let's start from the very beginning.

---

## 🔑 Prerequisite Concepts

Before we dive in, let's quickly review a few things from earlier lessons that we'll use throughout this lesson.

### What is a Boolean?

A **Boolean** is a value that is either `True` or `False` — nothing else. It is named after the mathematician George Boole.

```python
is_raining = True
has_money = False

print(is_raining)   # True
print(has_money)    # False
```

### What are Comparison Operators?

Comparison operators compare two values and produce a Boolean result (`True` or `False`):

| Operator | Meaning | Example | Result |
|---|---|---|---|
| `==` | Equal to | `5 == 5` | `True` |
| `!=` | Not equal to | `5 != 3` | `True` |
| `>` | Greater than | `10 > 7` | `True` |
| `<` | Less than | `3 < 8` | `True` |
| `>=` | Greater than or equal to | `5 >= 5` | `True` |
| `<=` | Less than or equal to | `4 <= 3` | `False` |

```python
print(10 > 5)    # True
print(10 == 5)   # False
print(10 != 5)   # True
```

**Output:**
```
True
False
True
```

These comparison results — `True` or `False` — are exactly what `if` statements use to decide what code to run.

---

## 🧠 Part 1: The `if` Statement

### 1.1 What is an `if` Statement?

An `if` statement says: **"Only run this block of code IF this condition is True."**

If the condition is `False`, the code inside the `if` block is simply skipped.

> **Real-life analogy:** Think of a bouncer at the door of a club. The bouncer checks your ID. **If** you are 18 or older → you get in. If not → nothing happens (you don't get in). The `if` statement works exactly like that bouncer.

### 1.2 Syntax

```
if condition:
    code to run if condition is True
```

Key rules:
- The `if` keyword must be lowercase
- The condition is followed by a **colon** `:`
- The code to run **must be indented** (shifted right by 4 spaces or 1 tab)
- Python uses **indentation** (whitespace) to define which lines belong inside the `if` block

### 1.3 Your First `if` Statement

```python
a = 33
b = 200

if b > a:
    print("b is greater than a")
```

**Output:**
```
b is greater than a
```

Let's trace through it:
- `a = 33` and `b = 200`
- The condition is `b > a`, which is `200 > 33`
- `200 > 33` is `True`
- Because the condition is `True`, Python runs the indented code: `print("b is greater than a")`

What if the condition were `False`?

```python
a = 200
b = 33

if b > a:
    print("b is greater than a")

print("This line always runs")
```

**Output:**
```
This line always runs
```

Because `b > a` is `33 > 200` which is `False`, the `print("b is greater than a")` line is **skipped entirely**. The unindented line below always runs regardless.

---

### 1.4 Indentation — The Most Important Rule

Python is unique: it uses **indentation** (blank space at the start of a line) to group code together. This is not optional — it is the rule.

```python
# ✅ CORRECT — the print is indented inside the if block
score = 80
if score >= 50:
    print("You passed!")
```

```python
# ❌ WRONG — IndentationError
score = 80
if score >= 50:
print("You passed!")    # no indent = error!
```

**Error:**
```
IndentationError: expected an indented block
```

> **Rule:** Everything that should run as part of the `if` block must be indented by the **same amount** — conventionally 4 spaces.

You can have multiple lines inside an `if` block — they all just need the same indentation:

```python
score = 80
if score >= 50:
    print("Congratulations!")
    print("You passed the exam.")
    print("Keep up the good work!")

print("End of report.")
```

**Output:**
```
Congratulations!
You passed the exam.
Keep up the good work!
End of report.
```

The last line is unindented, so it always runs regardless of the condition.

---

## 🧠 Part 2: The `else` Statement

### 2.1 What is `else`?

The `if` statement handles "what to do when the condition is True". But what about "what to do when the condition is False"? That's exactly what `else` is for.

> **Real-life analogy:** "If it is raining, take an umbrella. **Else** (otherwise), wear sunglasses."

### 2.2 `if...else` Syntax

```
if condition:
    code to run if condition is True
else:
    code to run if condition is False
```

- `else` is written at the same indentation level as `if`
- `else` also ends with a colon `:`
- The code inside `else` must be indented

### 2.3 Simple `if...else` Example

```python
a = 200
b = 33

if b > a:
    print("b is greater than a")
else:
    print("b is not greater than a")
```

**Output:**
```
b is not greater than a
```

- `b > a` is `33 > 200` which is `False`
- The `if` block is skipped
- The `else` block runs instead: `print("b is not greater than a")`

### 2.4 Another Example — Pass or Fail

```python
score = 72

if score >= 50:
    print("Result: PASS")
else:
    print("Result: FAIL")
```

**Output:**
```
Result: PASS
```

Change `score` to `40`:

```python
score = 40

if score >= 50:
    print("Result: PASS")
else:
    print("Result: FAIL")
```

**Output:**
```
Result: FAIL
```

Only one of the two blocks ever runs — never both. Python checks the condition, picks the matching path, and skips the other.

---

## 🧠 Part 3: The `elif` Statement

### 3.1 What Problem Does `elif` Solve?

Imagine you want to assign letter grades: A, B, C, D, or F. A simple `if...else` only gives you two options. For more options, you need `elif` (short for "**else if**").

`elif` lets you check **another condition** if the previous `if` (or `elif`) condition was `False`.

### 3.2 `elif` Syntax

```
if condition_1:
    code if condition_1 is True
elif condition_2:
    code if condition_2 is True
else:
    code if none of the above are True
```

You can have **as many `elif` blocks as you need** between the `if` and the `else`.

### 3.3 Basic `elif` Example

```python
a = 33
b = 33

if b > a:
    print("b is greater than a")
elif a == b:
    print("a and b are equal")
```

**Output:**
```
a and b are equal
```

- `b > a` is `33 > 33` which is `False` → skip this block
- `a == b` is `33 == 33` which is `True` → run this block

### 3.4 `if...elif...else` — The Full Chain

```python
a = 200
b = 33

if b > a:
    print("b is greater than a")
elif a == b:
    print("a and b are equal")
else:
    print("a is greater than b")
```

**Output:**
```
a is greater than b
```

- `b > a` → False (skip)
- `a == b` → False (skip)
- `else` → runs: `a is greater than b`

### 3.5 Grade Assignment with Multiple `elif`

This is one of the most common real-world uses of `elif` chains:

```python
score = 76

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

print(f"Score: {score} → Grade: {grade}")
```

**Output:**
```
Score: 76 → Grade: C
```

Let's trace through this carefully:
- `score >= 90` → `76 >= 90` → False → skip
- `score >= 80` → `76 >= 80` → False → skip
- `score >= 70` → `76 >= 70` → **True** → `grade = "C"` → **STOP checking further**
- Python immediately stops checking the remaining `elif` and `else` blocks once a match is found

> **Key insight:** Python checks `elif` conditions **from top to bottom** and stops as soon as one is True. The order matters! If you put `score >= 50` first, every passing score would match it and nothing more specific would ever be reached.

### 3.6 Multiple `elif` — Season Identifier

```python
month = 7

if month in (12, 1, 2):
    season = "Winter"
elif month in (3, 4, 5):
    season = "Spring"
elif month in (6, 7, 8):
    season = "Summer"
elif month in (9, 10, 11):
    season = "Autumn"
else:
    season = "Invalid month"

print(f"Month {month} is in {season}")
```

**Output:**
```
Month 7 is in Summer
```

> **Thinking Prompt:** What happens if you set `month = 13`? Try it and see which branch runs.

---

## 🧠 Part 4: Shorthand `if` (One-Liner)

### 4.1 What is Shorthand `if`?

Sometimes your condition and its action are very simple — just one line each. Python lets you write the entire `if` statement on a **single line**. This is called the **shorthand** or **ternary** form.

### 4.2 One-Line `if`

Standard form:
```python
a = 10
b = 5
if a > b:
    print("a is greater than b")
```

Shorthand form (exact same logic, one line):
```python
a = 10
b = 5
if a > b: print("a is greater than b")
```

**Output (both):**
```
a is greater than b
```

You just put the action right after the colon on the same line.

### 4.3 One-Line `if...else` — The Ternary Operator

You can also write a complete `if...else` on one line using this structure:

```
value_if_true if condition else value_if_false
```

```python
a = 2
b = 330

print("A") if a > b else print("B")
```

**Output:**
```
B
```

Because `a > b` is `2 > 330` which is `False`, Python executes `print("B")`.

### 4.4 Ternary with Three Options

You can even chain a three-way decision in one line:

```python
a = 330
b = 330

print("A") if a > b else print("=") if a == b else print("B")
```

**Output:**
```
=
```

Reading this left to right:
- `if a > b` → False → move to the `else` part
- `if a == b` → True → `print("=")`

### 4.5 Assigning Values with Ternary

The ternary operator is very useful for assigning one of two values to a variable:

```python
age = 20
status = "Adult" if age >= 18 else "Minor"
print(status)
```

**Output:**
```
Adult
```

```python
score = 45
result = "Pass" if score >= 50 else "Fail"
print(result)
```

**Output:**
```
Fail
```

> **When to use shorthand:** Use it for simple, readable one-liners. If the logic gets complex, switch back to the full multi-line form — readability always wins.

---

## 🧠 Part 5: Logical Operators — Combining Conditions

### 5.1 Why Do We Need Logical Operators?

Sometimes one condition isn't enough. You might need:
- "If age is over 18 **AND** has a valid ID → let in"
- "If temperature is below 0 **OR** above 40 → send a warning"
- "If the user is **NOT** banned → allow login"

Python has three **logical operators** for exactly this:

| Operator | Meaning | Returns True when... |
|---|---|---|
| `and` | Both conditions must be True | **both** sides are True |
| `or` | At least one condition must be True | **at least one** side is True |
| `not` | Reverses the Boolean | the condition is False |

---

### 5.2 The `and` Operator

```python
a = 200
b = 33
c = 500

if a > b and c > a:
    print("Both conditions are True")
```

**Output:**
```
Both conditions are True
```

- `a > b` → `200 > 33` → True
- `c > a` → `500 > 200` → True
- `True and True` → **True** → the block runs

What if one is False?

```python
a = 200
b = 33
c = 100

if a > b and c > a:
    print("Both conditions are True")
else:
    print("At least one condition is False")
```

**Output:**
```
At least one condition is False
```

- `a > b` → True
- `c > a` → `100 > 200` → **False**
- `True and False` → **False** → else block runs

> **Rule for `and`:** If **any** part is False, the entire `and` expression is False.

**Real-world example:** Check if a student qualifies for an honour roll (score above 90 AND attendance above 95%):

```python
score = 92
attendance = 97

if score > 90 and attendance > 95:
    print("Qualifies for Honour Roll")
else:
    print("Does not qualify for Honour Roll")
```

**Output:**
```
Qualifies for Honour Roll
```

---

### 5.3 The `or` Operator

```python
a = 200
b = 33
c = 500

if a > b or a > c:
    print("At least one condition is True")
```

**Output:**
```
At least one condition is True
```

- `a > b` → `200 > 33` → **True**
- `a > c` → `200 > 500` → False
- `True or False` → **True** → block runs

`or` only needs **one** side to be True.

**Real-world example:** Trigger an alert if temperature is too cold or too hot:

```python
temperature = 42

if temperature < 0 or temperature > 40:
    print("⚠️ Extreme temperature! Take action.")
else:
    print("Temperature is within normal range.")
```

**Output:**
```
⚠️ Extreme temperature! Take action.
```

`or` truth table:

| A | B | A or B |
|---|---|---|
| True | True | **True** |
| True | False | **True** |
| False | True | **True** |
| False | False | **False** |

---

### 5.4 The `not` Operator

`not` **flips** a Boolean — it turns `True` into `False` and `False` into `True`.

```python
a = 33
b = 200

if not a > b:
    print("a is NOT greater than b")
```

**Output:**
```
a is NOT greater than b
```

- `a > b` → `33 > 200` → False
- `not False` → **True** → block runs

Another example:

```python
is_logged_in = False

if not is_logged_in:
    print("Please log in to continue.")
```

**Output:**
```
Please log in to continue.
```

`not is_logged_in` is `not False` which is `True`, so the print runs.

---

### 5.5 Combining `and`, `or`, `not` Together

You can combine all three in one condition. Python evaluates them in this precedence order: `not` first, then `and`, then `or`.

```python
age = 25
has_ticket = True
is_vip = False

if age >= 18 and (has_ticket or is_vip):
    print("Entry granted!")
else:
    print("Entry denied.")
```

**Output:**
```
Entry granted!
```

- `age >= 18` → True
- `has_ticket or is_vip` → `True or False` → True
- `True and True` → **True** → entry granted

> **Tip:** Use parentheses `( )` to make the grouping of your conditions obvious, just like in maths. This prevents surprises and makes your code easier to read.

---

## 🧠 Part 6: Nested `if` Statements

### 6.1 What is a Nested `if`?

A **nested `if`** is an `if` statement that lives **inside** another `if` statement. When the outer condition is True, the inner condition is then also checked.

> **Real-life analogy:** "If it's the weekend → if it's sunny → go to the beach." The second decision (sunny or not) only matters if the first decision (weekend) is already confirmed.

### 6.2 Basic Nested `if` Example

```python
x = 41

if x > 10:
    print("Above ten,")
    if x > 20:
        print("and also above 20!")
    else:
        print("but not above 20.")
```

**Output:**
```
Above ten,
and also above 20!
```

Trace through:
- `x > 10` → `41 > 10` → True → enter the outer block
- `print("Above ten,")` → prints
- `x > 20` → `41 > 20` → True → enter the inner block
- `print("and also above 20!")` → prints

Change `x = 15`:

```python
x = 15

if x > 10:
    print("Above ten,")
    if x > 20:
        print("and also above 20!")
    else:
        print("but not above 20.")
```

**Output:**
```
Above ten,
but not above 20.
```

The inner `else` runs because `x > 20` is now False.

Change `x = 5`:

```python
x = 5

if x > 10:
    print("Above ten,")
    if x > 20:
        print("and also above 20!")
    else:
        print("but not above 20.")
```

**Output:**
```
(nothing)
```

The outer condition `x > 10` is False, so nothing at all runs — including the inner `if`.

### 6.3 Nested `if` — Practical Example: Login System

```python
username = "admin"
password = "secret123"

input_user = "admin"
input_pass = "secret123"

if input_user == username:
    print("Username found.")
    if input_pass == password:
        print("Password correct. Welcome!")
    else:
        print("Wrong password. Access denied.")
else:
    print("Username not found. Access denied.")
```

**Output:**
```
Username found.
Password correct. Welcome!
```

Change `input_pass = "wrongpass"`:

**Output:**
```
Username found.
Wrong password. Access denied.
```

Change `input_user = "hacker"`:

**Output:**
```
Username not found. Access denied.
```

### 6.4 Three-Level Nested `if` — Ticket Pricing

```python
age = 25
is_student = False
is_member = True

if age >= 60:
    ticket_price = 5.00
    category = "Senior"
elif age < 12:
    ticket_price = 3.00
    category = "Child"
else:
    if is_student:
        ticket_price = 8.00
        category = "Student"
    elif is_member:
        ticket_price = 10.00
        category = "Member"
    else:
        ticket_price = 15.00
        category = "Regular Adult"

print(f"Category: {category}")
print(f"Ticket Price: ${ticket_price:.2f}")
```

**Output:**
```
Category: Member
Ticket Price: $10.00
```

> **Thinking Prompt:** Change `age = 8` and trace through the code. Which branch runs? What is the price?

---

## 🧠 Part 7: The `pass` Statement

### 7.1 Why Does `pass` Exist?

In Python, an `if` block **cannot be empty**. If you write an `if` with no code inside, Python will give you a `SyntaxError`.

But there are times when:
- You are writing your code structure first and filling in details later
- You intentionally want a condition to do nothing (a placeholder)
- You are testing and haven't decided what to put inside yet

For all these situations, Python provides the `pass` statement — a keyword that means **"do nothing here"** and simply satisfies Python's requirement that the block must contain something.

### 7.2 The Problem Without `pass`

```python
# ❌ This causes a SyntaxError — empty if block not allowed
a = 33
b = 200

if b > a:
    # TODO: handle this case later

print("Done")
```

**Error:**
```
SyntaxError: expected an indented block after 'if' statement
```

### 7.3 The Solution — Using `pass`

```python
# ✅ CORRECT — pass acts as a placeholder
a = 33
b = 200

if b > a:
    pass    # nothing happens here — will be filled in later

print("Done")
```

**Output:**
```
Done
```

The `pass` statement does nothing — it just prevents the empty-block error. The program continues normally to `print("Done")`.

### 7.4 `pass` in `elif` and `else`

```python
score = 72

if score >= 90:
    print("Grade A")
elif score >= 70:
    pass    # placeholder — will add logging code later
elif score >= 50:
    print("Grade C")
else:
    print("Grade F")
```

**Output:**
```
(nothing)
```

The score `72` matches `score >= 70`, so `pass` runs — which does nothing — and the program ends.

### 7.5 Real-World Use of `pass`

`pass` is very common when writing a program's skeleton structure before filling in the details:

```python
user_role = "guest"

if user_role == "admin":
    pass    # TODO: show admin dashboard
elif user_role == "editor":
    pass    # TODO: show editor tools
elif user_role == "guest":
    print("Welcome, guest! Limited access only.")
else:
    pass    # TODO: handle unknown roles
```

**Output:**
```
Welcome, guest! Limited access only.
```

The code structure is in place; `pass` keeps it syntactically valid while you develop each branch.

---

## 🛠️ Guided Practice Exercises

### Exercise 1: Temperature Checker

**Objective:** Use `if`, `elif`, and `else` to classify a temperature.

**Scenario:** Build a simple weather advisory system.

```python
temperature = 38  # degrees Celsius

if temperature > 40:
    print("Extreme heat! Stay indoors and drink water.")
elif temperature > 30:
    print("Hot day. Stay hydrated.")
elif temperature > 20:
    print("Warm and comfortable.")
elif temperature > 10:
    print("Cool. A light jacket is recommended.")
elif temperature > 0:
    print("Cold. Wear a coat.")
else:
    print("Freezing! Below zero temperatures.")
```

**Expected Output:**
```
Hot day. Stay hydrated.
```

**What-if Challenge:** Run the code with temperatures of: `-5`, `5`, `15`, `25`, `35`, `45`. Confirm each message is correct.

**Self-check Questions:**
- How many `elif` branches are in this code?
- What happens if two conditions could both be True? Which one runs?
- Why must `temperature > 40` be checked before `temperature > 30`?

---

### Exercise 2: Voting Eligibility Checker

**Objective:** Combine `and`, `or`, `not` to validate multiple requirements.

**Scenario:** A person can vote if they are 18 or older AND are a registered citizen.

```python
age = 20
is_citizen = True
is_registered = False

print("=== Voting Eligibility Check ===")

if age >= 18 and is_citizen:
    if is_registered:
        print("✅ You are eligible and registered to vote!")
    else:
        print("⚠️  You are eligible but NOT registered. Please register first.")
else:
    if not is_citizen:
        print("❌ You must be a citizen to vote.")
    elif age < 18:
        print(f"❌ You must be at least 18. You are {age}.")
    else:
        print("❌ You do not meet voting requirements.")
```

**Expected Output:**
```
=== Voting Eligibility Check ===
⚠️  You are eligible but NOT registered. Please register first.
```

**What-if Challenges:**
- Change `is_registered = True`. What output do you get?
- Change `age = 16`. What output do you get?
- Change `is_citizen = False`. What output do you get?

---

### Exercise 3: ATM Machine Simulation

**Objective:** Use nested `if` statements with multiple conditions.

**Scenario:** Simulate a simple ATM withdrawal.

```python
balance = 5000.00
pin_correct = True
withdrawal_amount = 2000

print("=== ATM Machine ===")

if pin_correct:
    print("PIN accepted.")
    if withdrawal_amount <= 0:
        print("❌ Invalid amount. Enter a positive number.")
    elif withdrawal_amount > balance:
        print(f"❌ Insufficient funds. Your balance is ₦{balance:.2f}")
    elif withdrawal_amount > 3000:
        print("❌ Withdrawal limit is ₦3,000 per transaction.")
    else:
        balance -= withdrawal_amount
        print(f"✅ Dispensing ₦{withdrawal_amount:.2f}")
        print(f"   New balance: ₦{balance:.2f}")
else:
    print("❌ Incorrect PIN. Card retained.")
```

**Expected Output:**
```
=== ATM Machine ===
PIN accepted.
✅ Dispensing ₦2000.00
   New balance: ₦3000.00
```

**What-if Challenges:**
- Set `withdrawal_amount = 4000`. Which error runs?
- Set `balance = 500`. Which error runs?
- Set `pin_correct = False`. What happens?

---

### Exercise 4: Shorthand Practice

**Objective:** Rewrite conditions as one-liners.

Rewrite these multi-line blocks as shorthand:

**Problem 1:**
```python
x = 15

# Long form
if x > 10:
    print("Greater")
else:
    print("Not greater")
```

**Shorthand solution:**
```python
x = 15
print("Greater") if x > 10 else print("Not greater")
```

**Output:**
```
Greater
```

**Problem 2:** Assign a label based on a number.

```python
number = -5

# Long form
if number > 0:
    label = "Positive"
elif number < 0:
    label = "Negative"
else:
    label = "Zero"
print(label)
```

**Shorthand solution:**
```python
number = -5
label = "Positive" if number > 0 else "Negative" if number < 0 else "Zero"
print(label)
```

**Output:**
```
Negative
```

---

## 🚀 Mini Project: Student Report Card Generator

Let's combine every concept from this lesson into one complete project.

**Project Goal:** Build an interactive report card generator that takes a student's scores, assigns grades, and produces a formatted report with comments.

---

### Stage 1: Setup — Define the Student Data

```python
student_name = "Adaeze Okonkwo"
scores = {
    "Mathematics":   78,
    "English":       85,
    "Science":       91,
    "History":       62,
    "Computer":      95,
}
```

---

### Stage 2: Grade and Comment Assignment Function

```python
def get_grade_and_comment(score):
    if score >= 90:
        grade = "A"
        comment = "Excellent"
    elif score >= 80:
        grade = "B"
        comment = "Very Good"
    elif score >= 70:
        grade = "C"
        comment = "Good"
    elif score >= 60:
        grade = "D"
        comment = "Pass"
    elif score >= 50:
        grade = "E"
        comment = "Fair"
    else:
        grade = "F"
        comment = "Fail — Needs Support"
    return grade, comment
```

---

### Stage 3: Calculate Statistics

```python
total = 0
highest_score = 0
lowest_score = 100
highest_subject = ""
lowest_subject = ""

for subject, score in scores.items():
    total += score
    if score > highest_score:
        highest_score = score
        highest_subject = subject
    if score < lowest_score:
        lowest_score = score
        lowest_subject = subject

average = total / len(scores)
```

---

### Stage 4: Overall Performance Decision

```python
if average >= 80:
    overall = "DISTINCTION"
    overall_comment = "Outstanding performance!"
elif average >= 65:
    overall = "CREDIT"
    overall_comment = "Good performance. Keep it up!"
elif average >= 50:
    overall = "PASS"
    overall_comment = "Adequate performance. Room for improvement."
else:
    overall = "FAIL"
    overall_comment = "Needs significant improvement."

# Attendance bonus check
attendance = 98
if attendance >= 95 and overall != "FAIL":
    attendance_note = "✅ Perfect attendance bonus applied."
else:
    attendance_note = "⚠️  Attendance below 95%. No bonus."
```

---

### Stage 5: Print the Report

```python
print("=" * 52)
print("           STUDENT REPORT CARD")
print("=" * 52)
print(f"  Student:  {student_name}")
print(f"  Attendance: {attendance}%")
print("=" * 52)
print(f"  {'SUBJECT':<16} {'SCORE':>6} {'GRADE':>6}  COMMENT")
print("-" * 52)

for subject, score in scores.items():
    grade, comment = get_grade_and_comment(score)
    print(f"  {subject:<16} {score:>6} {grade:>6}  {comment}")

print("-" * 52)
print(f"  {'TOTAL':<16} {total:>6}")
print(f"  {'AVERAGE':<16} {average:>6.1f}")
print("=" * 52)
print(f"  Overall Result:  {overall}")
print(f"  Comment:         {overall_comment}")
print(f"  {attendance_note}")
print(f"  Top Subject:     {highest_subject} ({highest_score})")
print(f"  Weakest Subject: {lowest_subject} ({lowest_score})")
print("=" * 52)
```

---

### Complete Final Output

```
====================================================
           STUDENT REPORT CARD
====================================================
  Student:  Adaeze Okonkwo
  Attendance: 98%
====================================================
  SUBJECT          SCORE  GRADE  COMMENT
----------------------------------------------------
  Mathematics         78      C  Good
  English             85      B  Very Good
  Science             91      A  Excellent
  History             62      D  Pass
  Computer            95      A  Excellent
----------------------------------------------------
  TOTAL              411
  AVERAGE           82.2
====================================================
  Overall Result:  DISTINCTION
  Comment:         Outstanding performance!
  ✅ Perfect attendance bonus applied.
  Top Subject:     Computer (95)
  Weakest Subject: History (62)
====================================================
```

**Reflection Questions:**
- Which concept (`if`, `elif`, `else`, `and`, nested `if`) did the grade function use?
- Why did we check `overall != "FAIL"` in the attendance bonus condition?
- What would happen if all 5 subjects had a score of 40?
- Can you add a **merit badge** that prints only if the student scored above 90 in at least 2 subjects?

---

## ⚠️ Common Beginner Mistakes

### Mistake 1: Using `=` Instead of `==`

```python
# ❌ WRONG — single = is assignment, not comparison
x = 5
if x = 5:       # SyntaxError!
    print("Five")

# ✅ CORRECT — double == for comparison
if x == 5:
    print("Five")
```

**Output:**
```
Five
```

---

### Mistake 2: Forgetting the Colon `:`

```python
# ❌ WRONG — missing colon causes SyntaxError
if x > 0
    print("Positive")

# ✅ CORRECT
if x > 0:
    print("Positive")
```

---

### Mistake 3: Wrong Indentation

```python
# ❌ WRONG — mixed indentation levels cause IndentationError
x = 10
if x > 5:
    print("Greater")      # 4 spaces
      print("than five")  # 6 spaces — mismatch!

# ✅ CORRECT — all lines in the same block have the same indentation
if x > 5:
    print("Greater")
    print("than five")
```

---

### Mistake 4: `elif` / `else` Without a Preceding `if`

```python
# ❌ WRONG — else without if
score = 80
else:
    print("Fail")   # SyntaxError — else must follow an if block

# ✅ CORRECT
if score >= 50:
    print("Pass")
else:
    print("Fail")
```

---

### Mistake 5: Wrong Order in `elif` Chains

```python
# ❌ WRONG — least specific condition first swallows everything
score = 95
if score >= 50:
    print("Pass")    # This prints for ALL passing scores!
elif score >= 90:
    print("A")       # This NEVER runs — already caught above

# ✅ CORRECT — most specific condition first
if score >= 90:
    print("A")
elif score >= 50:
    print("Pass")
```

**Output of correct version:**
```
A
```

---

### Mistake 6: Confusing `and` / `or` Logic

```python
# ❌ WRONG — thinking "not zero and not negative" means both conditions
x = -5
if x != 0 and x > 0:    # This means POSITIVE (not zero AND greater than zero)
    print("Positive non-zero")
else:
    print("Zero or negative")   # This runs for x = -5

# If you want "not zero OR not negative" — be explicit:
if x != 0 or x > 0:
    print("Non-zero or positive")
```

---

### Mistake 7: Empty `if` Block (Forgetting `pass`)

```python
# ❌ WRONG — empty block causes SyntaxError
temperature = 25
if temperature > 100:
    # TODO: handle extreme heat
print("Done")   # Python sees this and gets confused

# ✅ CORRECT — use pass as a placeholder
if temperature > 100:
    pass    # intentionally empty for now
print("Done")
```

**Output:**
```
Done
```

---

## 💭 Reflection Questions

Test your understanding before moving on:

1. What is the difference between `=` and `==` in Python?
2. Why does Python use **indentation** to define code blocks instead of curly braces `{ }`?
3. In an `if...elif...else` chain, how many blocks can ever run at one time?
4. What is the output of this code?
   ```python
   x = 50
   if x > 100:
       print("A")
   elif x > 50:
       print("B")
   elif x == 50:
       print("C")
   else:
       print("D")
   ```
5. What does `not True` evaluate to?
6. When would you choose `and` over `or`?
7. Write a one-line ternary expression that prints `"Even"` if a number is divisible by 2, else `"Odd"`.
8. What is the purpose of the `pass` statement?
9. Can an `if` statement exist inside another `if` statement? What is this called?
10. Why is the order of `elif` conditions important? Give an example where the wrong order produces a bug.

---

## ✅ Completion Checklist

Before moving to the next lesson, confirm you can:

- [ ] Write a basic `if` statement that runs code only when a condition is True
- [ ] Use `else` to handle the False case
- [ ] Use `elif` for multiple alternative conditions
- [ ] Correctly order `elif` conditions from most specific to least specific
- [ ] Write shorthand one-line `if` and `if...else` expressions
- [ ] Use the ternary form to assign a value based on a condition
- [ ] Combine conditions with `and` (both must be True)
- [ ] Combine conditions with `or` (at least one must be True)
- [ ] Flip a Boolean with `not`
- [ ] Write nested `if` statements (an `if` inside an `if`)
- [ ] Use `pass` as a placeholder for empty blocks
- [ ] Avoid the 7 common mistakes listed above
- [ ] Complete all 4 guided exercises
- [ ] Complete the Student Report Card mini project

---

## 📋 Lesson Summary

Here's everything from Lesson 15, condensed for quick review:

**The `if` statement — run code only when True:**
```python
if condition:
    code runs here
```

**The `else` — run code when condition is False:**
```python
if condition:
    runs if True
else:
    runs if False
```

**The `elif` — check multiple conditions in order:**
```python
if condition_1:
    runs if condition_1 is True
elif condition_2:
    runs if condition_2 is True (and condition_1 was False)
else:
    runs if nothing above matched
```

**Shorthand — one-liner forms:**
```python
if condition: action                            # one-line if
print("A") if condition else print("B")        # one-line if/else
x = "Yes" if condition else "No"               # ternary assignment
```

**Logical operators — combining conditions:**
```python
if a > 0 and b > 0:    # both must be True
if a > 0 or b > 0:     # at least one must be True
if not condition:       # reverses True/False
```

**Nested `if` — decisions inside decisions:**
```python
if outer_condition:
    if inner_condition:
        code runs only if BOTH are True
```

**`pass` — an empty placeholder:**
```python
if condition:
    pass    # does nothing — prevents SyntaxError in empty blocks
```

**Key rules to always remember:**
- Use `==` for comparison, `=` for assignment
- Every `if` / `elif` / `else` line ends with a colon `:`
- Code inside a block must be consistently indented
- `elif` order matters — most specific conditions go first
- `else` is optional; `elif` is optional; `if` is required

---

*You are now ready for Lesson 16: Python While Loops!*
