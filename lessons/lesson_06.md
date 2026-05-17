---
render_with_liquid: false
title: "Lesson 06 – Python Operators: Comparison, Logical, Identity, Membership, Bitwise & Precedence"
nav_order: 6
---

# Lesson 06 – Python Operators: Comparison, Logical, Identity, Membership, Bitwise & Precedence

---

## Lesson Introduction

Every useful program must make **decisions**.

- Is this student's score high enough to pass?
- Did the user type the correct password?
- Is this item already in the shopping cart?
- Should the alarm fire right now?

To answer these questions, Python uses **operators** — special symbols and keywords that compare values, combine conditions, check identity, test membership, manipulate data at the binary level, and follow a strict order of evaluation.

This lesson covers all six remaining operator groups in Python:

| # | Operator Group | Purpose |
|---|---|---|
| 1 | **Comparison** | Compare two values → produces `True` or `False` |
| 2 | **Logical** | Combine multiple conditions → `and`, `or`, `not` |
| 3 | **Identity** | Check whether two variables point to the same object in memory → `is`, `is not` |
| 4 | **Membership** | Check whether a value exists inside a collection → `in`, `not in` |
| 5 | **Bitwise** | Manipulate individual binary bits of integers |
| 6 | **Precedence** | The fixed order Python uses to evaluate complex expressions |

By the end of this lesson you will understand every operator, write confident conditions and expressions, avoid the most common beginner errors, and build a mini-project that combines all six groups into a working program.

---

## Prerequisite Concepts

> If any of these feel unfamiliar, briefly review your earlier lessons before continuing.

| Concept | Quick reminder |
|---|---|
| Variables | `x = 10` — stores a value under a name |
| Data types | `int`, `float`, `str`, `bool` |
| `print()` | Displays output on the screen |
| `bool` | A value that is either `True` or `False` |
| `if` statement | Runs code only when a condition is `True` |
| Lists and strings | Ordered collections you can search through |

No other prior knowledge is required. Every new concept is taught from scratch here.

---

## Part 1 – Comparison Operators

### 1.1 What Are Comparison Operators?

A **comparison operator** compares two values and always produces a **boolean result** — either `True` or `False`.

> **Real-world analogy:** Imagine a bouncer at a concert checking IDs. They ask: "Is this person's age ≥ 18?" The answer is either YES (`True`) or NO (`False`). That check is a comparison.

Comparisons are the foundation of every decision, every `if` statement, every loop condition, and every filter in Python.

---

### 1.2 The Six Comparison Operators

| Operator | Name | Meaning | Example | Result |
|---|---|---|---|---|
| `==` | Equal to | Are the two values the same? | `5 == 5` | `True` |
| `!=` | Not equal to | Are the two values different? | `5 != 3` | `True` |
| `>` | Greater than | Is the left value larger? | `7 > 3` | `True` |
| `<` | Less than | Is the left value smaller? | `3 < 7` | `True` |
| `>=` | Greater than or equal to | Is left larger or the same? | `5 >= 5` | `True` |
| `<=` | Less than or equal to | Is left smaller or the same? | `4 <= 6` | `True` |

---

### 1.3 Simple Examples — Numbers

```python
a = 10
b = 5

print(a == b)    # Is 10 equal to 5?
print(a != b)    # Is 10 NOT equal to 5?
print(a > b)     # Is 10 greater than 5?
print(a < b)     # Is 10 less than 5?
print(a >= 10)   # Is 10 greater than or equal to 10?
print(a <= 9)    # Is 10 less than or equal to 9?
```

**Expected output:**
```
False
True
True
False
True
False
```

---

### 1.4 The Critical Difference: `=` vs `==`

> **Most common beginner mistake in all of Python.**

| Symbol | Meaning | Example |
|---|---|---|
| `=` | **Assignment** — stores a value into a variable | `x = 10` |
| `==` | **Comparison** — checks if two values are equal | `x == 10` → `True` |

```python
x = 10        # Assignment: x now holds the value 10
print(x == 10)  # Comparison: Is x equal to 10?  → True
print(x == 5)   # Comparison: Is x equal to 5?   → False
```

**Expected output:**
```
True
False
```

**Wrong version (causes an error inside a condition):**
```python
# WRONG
if x = 10:       # SyntaxError — you cannot use = inside an if condition
    print("yes")
```

**Correct version:**
```python
if x == 10:      # Correct — use == to compare
    print("yes")
```

---

### 1.5 Comparing Strings

Comparison operators work on strings too. Python compares strings **alphabetically** (technically, by Unicode code point value).

```python
print("apple" == "apple")   # Same string?
print("apple" == "Apple")   # Case-sensitive!
print("banana" > "apple")   # 'b' comes after 'a' alphabetically
print("cat" != "dog")
```

**Expected output:**
```
True
False
True
True
```

> **Why does this matter?** Password checks, name sorting, input validation, and search features all rely on string comparison.

---

### 1.6 Using Comparisons in `if` Statements

```python
score = 72

if score >= 50:
    print("Pass")
else:
    print("Fail")
```

**Expected output:**
```
Pass
```

```python
temperature = 38

if temperature > 37.5:
    print("Fever detected — please rest.")
else:
    print("Temperature is normal.")
```

**Expected output:**
```
Fever detected — please rest.
```

---

> **Thinking prompt:** What would happen if `score = 49`? What would happen if `temperature = 37.5` exactly?

---

## Part 2 – Logical Operators

### 2.1 What Are Logical Operators?

**Logical operators** let you combine two or more comparison results into one overall condition. They are the glue between multiple questions.

> **Real-world analogy:** A bank approves a loan only if the applicant earns enough **AND** has a good credit score. Both conditions must be true at the same time. That word "AND" is a logical operator.

---

### 2.2 The Three Logical Operators

| Operator | Meaning | Result is `True` when… |
|---|---|---|
| `and` | Both conditions must be true | **All** conditions are `True` |
| `or` | At least one condition must be true | **At least one** condition is `True` |
| `not` | Flips/reverses a boolean value | The condition is `False` |

---

### 2.3 The `and` Operator

`and` returns `True` only when **every** condition on both sides is `True`.

**Truth table for `and`:**

| Left | Right | Result |
|---|---|---|
| `True` | `True` | **`True`** |
| `True` | `False` | `False` |
| `False` | `True` | `False` |
| `False` | `False` | `False` |

```python
x = 8

print(x > 5 and x < 10)   # Is 8 greater than 5 AND less than 10?
print(x > 5 and x < 7)    # Is 8 greater than 5 AND less than 7?
```

**Expected output:**
```
True
False
```

**Real-world example — age and height check for a ride:**

```python
age    = 14
height = 140   # cm

if age >= 12 and height >= 130:
    print("You may ride.")
else:
    print("Sorry, you do not meet both requirements.")
```

**Expected output:**
```
You may ride.
```

---

### 2.4 The `or` Operator

`or` returns `True` when **at least one** condition is `True`.

**Truth table for `or`:**

| Left | Right | Result |
|---|---|---|
| `True` | `True` | `True` |
| `True` | `False` | `True` |
| `False` | `True` | `True` |
| `False` | `False` | **`False`** |

```python
x = 3

print(x == 3 or x == 7)   # Is x equal to 3 OR equal to 7?
print(x == 1 or x == 2)   # Is x equal to 1 OR equal to 2?
```

**Expected output:**
```
True
False
```

**Real-world example — accepting two valid payment methods:**

```python
payment = "card"

if payment == "cash" or payment == "card":
    print("Payment accepted.")
else:
    print("Payment method not supported.")
```

**Expected output:**
```
Payment accepted.
```

---

### 2.5 The `not` Operator

`not` reverses (flips) a boolean value. `True` becomes `False`; `False` becomes `True`.

**Truth table for `not`:**

| Input | Result |
|---|---|
| `True` | `False` |
| `False` | `True` |

```python
x = 5

print(not (x > 3))    # x > 3 is True, so not True = False
print(not (x > 10))   # x > 10 is False, so not False = True
```

**Expected output:**
```
False
True
```

**Real-world example — checking if a user is NOT logged in:**

```python
logged_in = False

if not logged_in:
    print("Please log in to continue.")
else:
    print("Welcome back!")
```

**Expected output:**
```
Please log in to continue.
```

---

### 2.6 Combining All Three Logical Operators

```python
age      = 20
has_id   = True
is_banned = False

if age >= 18 and has_id and not is_banned:
    print("Entry granted.")
else:
    print("Entry denied.")
```

**Expected output:**
```
Entry granted.
```

> **Step through this:** `age >= 18` → `True`. `has_id` → `True`. `not is_banned` → `not False` → `True`. All three are `True`, so `and` gives `True` overall.

---

### 2.7 Short-Circuit Evaluation (Important Concept)

Python is **lazy** — it stops evaluating a logical expression as soon as the result is certain:

- For `and`: if the **first** condition is `False`, Python skips the rest (the whole thing must be `False`).
- For `or`: if the **first** condition is `True`, Python skips the rest (the whole thing must be `True`).

```python
x = 0

# Without short-circuit, dividing by x would crash.
# But Python's 'and' stops at the first False:
if x != 0 and 10 / x > 2:
    print("condition met")
else:
    print("safe — short-circuit prevented division by zero")
```

**Expected output:**
```
safe — short-circuit prevented division by zero
```

---

## Part 3 – Identity Operators

### 3.1 What Are Identity Operators?

**Identity operators** do NOT check whether two values are equal. They check whether two variables point to **the exact same object in memory**.

> **Analogy:** Two photocopies of a document look identical (`==`), but they are not the *same physical document* (`is`). Identity operators check for the same physical object, not just the same appearance.

| Operator | Meaning |
|---|---|
| `is` | Returns `True` if both variables refer to the **same memory object** |
| `is not` | Returns `True` if they refer to **different memory objects** |

---

### 3.2 `is` vs `==` — The Key Difference

```python
a = [1, 2, 3]
b = [1, 2, 3]
c = a

print(a == b)    # Do they have the same VALUE?
print(a is b)    # Are they the SAME object in memory?
print(a is c)    # c was assigned from a — same object?
```

**Expected output:**
```
True
False
True
```

> **Explanation:**
> - `a == b` is `True` because both lists contain the same values `[1, 2, 3]`.
> - `a is b` is `False` because Python created **two separate list objects** in memory, even though they look the same.
> - `a is c` is `True` because `c = a` did not create a new list — it made `c` point to the **same** list object as `a`.

---

### 3.3 Visualising Memory

```
Memory:
┌─────────────┐         ┌─────────────┐
│  [1, 2, 3]  │ ← a, c  │  [1, 2, 3]  │ ← b
└─────────────┘         └─────────────┘
     Object A                Object B

a == b   → True  (same content)
a is b   → False (different objects)
a is c   → True  (same object)
```

---

### 3.4 `is not` Operator

```python
a = [1, 2, 3]
b = [1, 2, 3]

print(a is not b)   # Are they different objects?
```

**Expected output:**
```
True
```

---

### 3.5 Identity with `None`

The most common real-world use of `is` is checking whether a variable is `None` (Python's way of saying "no value").

```python
result = None

if result is None:
    print("No result yet — calculation has not run.")
else:
    print("Result:", result)
```

**Expected output:**
```
No result yet — calculation has not run.
```

> **Best practice:** Always use `is None` and `is not None` — never use `== None`. This is the official Python style (PEP 8).

---

### 3.6 Small Integer Caching (Interesting Edge Case)

Python internally **reuses** objects for small integers (typically -5 to 256) to save memory. This can make `is` return surprising results:

```python
x = 100
y = 100
print(x is y)    # True — Python reuses the same object for small ints

x = 1000
y = 1000
print(x is y)    # False — large integers get separate objects
```

**Expected output:**
```
True
False
```

> **Important:** Do not rely on this behaviour. For comparing values, always use `==`. Reserve `is` for identity checks (especially `None`).

---

## Part 4 – Membership Operators

### 4.1 What Are Membership Operators?

**Membership operators** check whether a value exists **inside** a collection such as a list, tuple, string, set, or dictionary.

> **Analogy:** You are at a VIP event. The bouncer checks a guest list: "Is your name *in* the list?" That is exactly what the `in` operator does.

| Operator | Meaning |
|---|---|
| `in` | Returns `True` if the value **is found** in the collection |
| `not in` | Returns `True` if the value is **NOT found** in the collection |

---

### 4.2 `in` with Lists

```python
fruits = ["apple", "banana", "cherry"]

print("banana" in fruits)    # Is "banana" in the list?
print("grape"  in fruits)    # Is "grape" in the list?
```

**Expected output:**
```
True
False
```

---

### 4.3 `not in` with Lists

```python
fruits = ["apple", "banana", "cherry"]

print("mango" not in fruits)    # Is "mango" absent from the list?
print("apple" not in fruits)    # Is "apple" absent from the list?
```

**Expected output:**
```
True
False
```

---

### 4.4 `in` with Strings

When used on a string, `in` checks whether one string is a **substring** of another:

```python
sentence = "The quick brown fox"

print("quick"  in sentence)    # Is "quick" inside the sentence?
print("slow"   in sentence)    # Is "slow" inside the sentence?
print("The"    in sentence)    # Case-sensitive!
print("the"    in sentence)    # Lowercase "the" — not the same
```

**Expected output:**
```
True
False
True
False
```

---

### 4.5 `in` with Tuples, Sets, and Dictionaries

```python
# Tuple
colours = ("red", "green", "blue")
print("green" in colours)     # True

# Set
primes = {2, 3, 5, 7, 11}
print(4 in primes)            # False

# Dictionary — checks KEYS by default
person = {"name": "Alice", "age": 30}
print("name"  in person)      # True  — "name" is a key
print("Alice" in person)      # False — "Alice" is a value, not a key
print("Alice" in person.values())  # True — now checking values
```

**Expected output:**
```
True
False
True
False
True
```

---

### 4.6 Real-World Examples

**Checking if a username is already taken:**

```python
existing_users = ["alice", "bob", "charlie"]
new_user = "bob"

if new_user in existing_users:
    print("Username already taken. Please choose another.")
else:
    print("Username available!")
```

**Expected output:**
```
Username already taken. Please choose another.
```

---

**Checking for forbidden words:**

```python
forbidden = ["spam", "scam", "fake"]
message = "This is not a scam, I promise"

for word in forbidden:
    if word in message.lower():
        print(f"Warning: message contains the word '{word}'")
        break
```

**Expected output:**
```
Warning: message contains the word 'scam'
```

---

> **Thinking prompt:** What happens when you use `in` on a very large list with millions of items? (Hint: Python searches from the beginning. For huge datasets, a `set` or `dict` is much faster because lookup is near-instant.)

---

## Part 5 – Bitwise Operators

### 5.1 What Are Bitwise Operators?

**Bitwise operators** work directly on the **binary (base-2) representation** of integers — they manipulate individual **bits** (the 0s and 1s that all data is stored as inside a computer).

> **Analogy:** Imagine a row of light switches, each either ON (1) or OFF (0). Bitwise operators let you flip, combine, or check individual switches without touching the others.

This is a more advanced topic. You may not use bitwise operators every day, but they are essential in:
- Systems programming and hardware control
- Network programming (IP address masks)
- Cryptography and security
- Graphics and game engines
- Compressing and storing flags efficiently

---

### 5.2 Binary Refresher (Essential Foundation)

Every integer in a computer is stored as a series of bits (binary digits). Each bit is either `0` or `1`.

| Decimal | Binary |
|---|---|
| 0 | `0000` |
| 1 | `0001` |
| 2 | `0010` |
| 3 | `0011` |
| 4 | `0100` |
| 5 | `0101` |
| 6 | `0110` |
| 7 | `0111` |
| 8 | `1000` |
| 10 | `1010` |
| 12 | `1100` |

**How to read binary:** Each position is a power of 2, starting from the right.

```
1010 in binary:
  1 × 2³  +  0 × 2²  +  1 × 2¹  +  0 × 2⁰
=  8      +  0       +  2       +  0
=  10
```

Python can show you a number's binary form:

```python
print(bin(10))   # 0b1010
print(bin(5))    # 0b101
print(bin(12))   # 0b1100
```

**Expected output:**
```
0b1010
0b101
0b1100
```

> The `0b` prefix means "this is binary". The actual bits are after it.

---

### 5.3 The Six Bitwise Operators

| Operator | Name | What it does |
|---|---|---|
| `&` | AND | Bit is `1` only if **both** bits are `1` |
| `\|` | OR | Bit is `1` if **at least one** bit is `1` |
| `^` | XOR | Bit is `1` if the bits are **different** |
| `~` | NOT | Flips every bit (inverts all 0s and 1s) |
| `<<` | Left shift | Shifts bits to the left (multiplies by powers of 2) |
| `>>` | Right shift | Shifts bits to the right (divides by powers of 2) |

---

### 5.4 Bitwise AND (`&`)

Compares each bit position. Result bit is `1` only when **both** input bits are `1`.

```
  6  =  0110
  3  =  0011
& ─────────
      0010  = 2
```

```python
a = 6   # 0110
b = 3   # 0011

print(a & b)       # 2
print(bin(a & b))  # 0b10
```

**Expected output:**
```
2
0b10
```

---

### 5.5 Bitwise OR (`|`)

Result bit is `1` when **at least one** input bit is `1`.

```
  6  =  0110
  3  =  0011
| ─────────
      0111  = 7
```

```python
a = 6   # 0110
b = 3   # 0011

print(a | b)       # 7
print(bin(a | b))  # 0b111
```

**Expected output:**
```
7
0b111
```

---

### 5.6 Bitwise XOR (`^`)

Result bit is `1` when the input bits are **different** (one is 0, the other is 1).

```
  6  =  0110
  3  =  0011
^ ─────────
      0101  = 5
```

```python
a = 6   # 0110
b = 3   # 0011

print(a ^ b)       # 5
print(bin(a ^ b))  # 0b101
```

**Expected output:**
```
5
0b101
```

---

### 5.7 Bitwise NOT (`~`)

Inverts every bit. The result in Python is `-(n + 1)` due to how Python stores negative numbers (two's complement):

```python
a = 6

print(~a)    # -(6 + 1) = -7
```

**Expected output:**
```
-7
```

---

### 5.8 Left Shift (`<<`)

Shifts all bits **left** by the specified number of positions. Zeros fill in on the right. Each left shift by 1 **doubles** the number (multiplies by 2).

```
  3  =  011
3 << 1:   110  = 6   (shifted left 1 → doubled)
3 << 2:  1100  = 12  (shifted left 2 → quadrupled)
```

```python
a = 3

print(a << 1)   # 6   (3 × 2¹)
print(a << 2)   # 12  (3 × 2²)
print(a << 3)   # 24  (3 × 2³)
```

**Expected output:**
```
6
12
24
```

---

### 5.9 Right Shift (`>>`)

Shifts all bits **right** by the specified number of positions. Each right shift by 1 **halves** the number (integer division by 2).

```
  12 =  1100
12 >> 1:   0110  = 6
12 >> 2:   0011  = 3
```

```python
a = 12

print(a >> 1)   # 6   (12 ÷ 2¹)
print(a >> 2)   # 3   (12 ÷ 2²)
```

**Expected output:**
```
6
3
```

---

### 5.10 Real-World Use: Permission Flags

A very practical use of bitwise operators is storing multiple `True/False` flags in a single integer. Each bit represents one permission:

```python
READ    = 0b100   # 4 — bit position 2
WRITE   = 0b010   # 2 — bit position 1
EXECUTE = 0b001   # 1 — bit position 0

# Give a user READ and WRITE permissions:
user_permissions = READ | WRITE
print(bin(user_permissions))   # 0b110 = 6

# Check if user has READ permission:
if user_permissions & READ:
    print("User can read.")

# Check if user has EXECUTE permission:
if user_permissions & EXECUTE:
    print("User can execute.")
else:
    print("User cannot execute.")
```

**Expected output:**
```
0b110
User can read.
User cannot execute.
```

---

### Bitwise Summary Table with Examples

| Operator | Example | Binary | Result |
|---|---|---|---|
| `&` | `6 & 3` | `0110 & 0011` | `2` |
| `\|` | `6 \| 3` | `0110 \| 0011` | `7` |
| `^` | `6 ^ 3` | `0110 ^ 0011` | `5` |
| `~` | `~6` | invert all bits | `-7` |
| `<<` | `3 << 1` | `011 → 110` | `6` |
| `>>` | `12 >> 2` | `1100 → 0011` | `3` |

---

## Part 6 – Operator Precedence

### 6.1 What Is Operator Precedence?

When Python evaluates an expression with multiple operators, it does not simply read from left to right. Instead, it follows a **fixed priority ranking** called **operator precedence** — similar to the mathematical rule "multiplication before addition" (BODMAS / PEMDAS).

> **Analogy:** In maths, `2 + 3 × 4` equals `14`, not `20`. Multiplication has higher precedence than addition, so `3 × 4` is computed first. Python follows the same idea — but for a much larger set of operators.

---

### 6.2 Why Does Precedence Matter?

```python
result = 2 + 3 * 4
print(result)
```

**Expected output:**
```
14
```

> `3 * 4 = 12` is evaluated first (multiplication has higher precedence), then `2 + 12 = 14`.

```python
result = (2 + 3) * 4
print(result)
```

**Expected output:**
```
20
```

> Parentheses have the **highest** precedence — everything inside them is evaluated first.

---

### 6.3 Python's Full Precedence Table

Listed from **highest** (evaluated first) to **lowest** (evaluated last):

| Priority | Operator(s) | Description |
|---|---|---|
| 1 (highest) | `()` | Parentheses — grouping |
| 2 | `**` | Exponentiation (power) |
| 3 | `+x`, `-x`, `~x` | Unary plus, unary minus, bitwise NOT |
| 4 | `*`, `/`, `//`, `%` | Multiplication, division, floor division, modulo |
| 5 | `+`, `-` | Addition, subtraction |
| 6 | `<<`, `>>` | Bitwise shifts |
| 7 | `&` | Bitwise AND |
| 8 | `^` | Bitwise XOR |
| 9 | `\|` | Bitwise OR |
| 10 | `==`, `!=`, `>`, `<`, `>=`, `<=`, `is`, `is not`, `in`, `not in` | Comparisons, identity, membership |
| 11 | `not` | Logical NOT |
| 12 | `and` | Logical AND |
| 13 (lowest) | `or` | Logical OR |

> **Key insight:** Arithmetic operators are evaluated before comparisons, comparisons are evaluated before logical operators, and `not` is evaluated before `and`, which is evaluated before `or`.

---

### 6.4 Step-Through Examples

**Example 1:**

```python
result = 5 + 2 * 3 - 1
print(result)
```

Step-by-step:
1. `2 * 3 = 6`  (multiplication first)
2. `5 + 6 = 11` (addition left to right)
3. `11 - 1 = 10` (subtraction)

**Expected output:**
```
10
```

---

**Example 2:**

```python
result = 2 ** 3 + 4 * 2
print(result)
```

Step-by-step:
1. `2 ** 3 = 8`  (exponent before multiply)
2. `4 * 2 = 8`   (multiply)
3. `8 + 8 = 16`  (addition)

**Expected output:**
```
16
```

---

**Example 3 — Comparison and logical operators together:**

```python
x = 10
result = x > 5 and x < 20 or x == 100
print(result)
```

Step-by-step:
1. `x > 5`    → `True`
2. `x < 20`   → `True`
3. `x == 100` → `False`
4. `True and True` → `True`  (and before or)
5. `True or False` → `True`

**Expected output:**
```
True
```

---

**Example 4 — Precedence trap:**

```python
print(2 + 3 == 5)
print(2 + (3 == 5))
```

Step-by-step for line 1:
1. `2 + 3 = 5`  (addition first — higher precedence than `==`)
2. `5 == 5`  → `True`

Step-by-step for line 2:
1. `3 == 5`  → `False` (parentheses first)
2. `2 + False` → `2 + 0 = 2` (in Python, `False` equals `0`)

**Expected output:**
```
True
2
```

---

**Example 5 — `not` before `and`:**

```python
x = True
y = False

print(not x and y)    # (not x) and y  →  False and False  →  False
print(not (x and y))  # not (True and False)  →  not False  →  True
```

**Expected output:**
```
False
True
```

---

### 6.5 The Golden Rule: Use Parentheses for Clarity

When in doubt, add parentheses. They cost nothing and make your intent crystal clear — both to Python and to other people reading your code.

```python
# Harder to read and easy to misinterpret:
if age >= 18 and not is_banned or is_admin:
    pass

# Much clearer with parentheses:
if (age >= 18 and not is_banned) or is_admin:
    pass
```

> **Professional advice:** Even experienced Python programmers add parentheses to complex conditions. Clarity always beats cleverness.

---

### 6.6 Same-Precedence Operators: Left-to-Right Evaluation

When two operators have the **same** precedence level, Python evaluates them **left to right** (called *left associativity*). The one exception is `**` (exponentiation), which is evaluated **right to left**.

```python
# Same precedence → left to right
print(10 - 3 - 2)     # (10 - 3) - 2 = 5
print(10 / 2 / 5)     # (10 / 2) / 5 = 1.0

# Exponentiation → right to left
print(2 ** 3 ** 2)    # 2 ** (3 ** 2) = 2 ** 9 = 512
```

**Expected output:**
```
5
1.0
512
```

---

## Part 7 – Guided Practice Exercises

### Exercise 1 – Access Control System

**Objective:** Practise comparison and logical operators.

**Scenario:** A secure office door grants entry only if the employee has a valid badge **and** is not on the blocked list **and** the time is within office hours (9 to 18).

```python
has_badge    = True
is_blocked   = False
current_hour = 14    # 2 pm in 24-hour format

# Write the condition for entry:
if has_badge and not is_blocked and 9 <= current_hour <= 18:
    print("Access granted. Welcome!")
else:
    print("Access denied.")
```

**Expected output:**
```
Access granted. Welcome!
```

**Self-check questions:**
1. What would happen if `current_hour = 20`?
2. What would happen if `is_blocked = True`?
3. Rewrite the time condition using two separate comparisons joined by `and` instead of Python's chained comparison.

---

### Exercise 2 – Product Search

**Objective:** Practise membership operators.

**Scenario:** An online store needs to check stock and category membership.

```python
in_stock    = ["laptop", "mouse", "keyboard", "monitor", "webcam"]
electronics = ["laptop", "phone", "tablet", "monitor"]

item = "mouse"

print(f"Is '{item}' in stock?         ", item in in_stock)
print(f"Is '{item}' electronics?      ", item in electronics)
print(f"Is '{item}' NOT electronics?  ", item not in electronics)

# Only recommend if in stock AND is electronics:
if item in in_stock and item in electronics:
    print(f"Recommended: {item}")
else:
    print(f"Cannot recommend: {item}")
```

**Expected output:**
```
Is 'mouse' in stock?          True
Is 'mouse' electronics?       False
Is 'mouse' NOT electronics?   True
Cannot recommend: mouse
```

---

### Exercise 3 – Identity Check

**Objective:** Understand the difference between `==` and `is`.

```python
list_a = [10, 20, 30]
list_b = [10, 20, 30]
list_c = list_a

print("list_a == list_b :", list_a == list_b)   # Same values?
print("list_a is list_b :", list_a is list_b)   # Same object?
print("list_a is list_c :", list_a is list_c)   # Same object?

# Modify list_c and see what happens to list_a:
list_c.append(40)
print("After modifying list_c:")
print("list_a :", list_a)
print("list_c :", list_c)
```

**Expected output:**
```
list_a == list_b : True
list_a is list_b : False
list_a is list_c : True
After modifying list_c:
list_a : [10, 20, 30, 40]
list_c : [10, 20, 30, 40]
```

> **What just happened?** `list_c` and `list_a` are the same object. Changing one changes the other. This is a critical concept for avoiding bugs.

---

### Exercise 4 – Bitwise Flag System

**Objective:** Use bitwise operators to manage user permissions.

```python
READ    = 0b100   # 4
WRITE   = 0b010   # 2
EXECUTE = 0b001   # 1

# Assign READ + EXECUTE to user:
user = READ | EXECUTE
print(f"Permissions (binary): {bin(user)}")
print(f"Permissions (decimal): {user}")

# Check each permission:
print("Can READ:   ", bool(user & READ))
print("Can WRITE:  ", bool(user & WRITE))
print("Can EXECUTE:", bool(user & EXECUTE))

# Grant WRITE permission:
user = user | WRITE
print(f"\nAfter granting WRITE: {bin(user)}")

# Revoke READ permission using XOR:
user = user ^ READ
print(f"After revoking READ:  {bin(user)}")
```

**Expected output:**
```
Permissions (binary): 0b101
Permissions (decimal): 5
Can READ:    True
Can WRITE:   False
Can EXECUTE: True

After granting WRITE: 0b111
After revoking READ:  0b11
```

---

### Exercise 5 – Precedence Prediction

**Objective:** Predict the output *before* running the code, then verify.

Predict the output of each line, write your answer, then run:

```python
print(3 + 4 * 2)
print((3 + 4) * 2)
print(2 ** 2 ** 3)
print(10 > 5 and 3 < 7)
print(not True or False)
print(not (True or False))
print(5 + 3 == 8 and 2 * 4 == 8)
print(True or False and False)
```

**Expected output:**
```
11
14
256
True
False
False
True
True
```

> For line 8: `and` has higher precedence than `or`, so `False and False` = `False` is evaluated first, then `True or False` = `True`.

---

## Part 8 – Mini-Project: Smart Student Evaluation System

### Project Overview

You will build a **Student Evaluation System** that uses all six operator types to:
- Compare exam scores against grade boundaries
- Apply logic to multiple conditions
- Check identity and membership
- Use precedence correctly in complex expressions

---

### Stage 1 – Setup and Data

```python
# Stage 1 – Student data
student_name  = "Jordan"
exam_score    = 74
attendance    = 88      # percentage
submitted_all = True    # submitted all assignments
on_watchlist  = False   # flagged for academic issues

grade_boundaries = {
    "A": 90,
    "B": 75,
    "C": 60,
    "D": 50,
}

passed_scores = [55, 74, 88, 91, 63]   # historical passing scores
```

---

### Stage 2 – Comparison: Grade Calculation

```python
# Stage 2 – Assign a letter grade using comparison operators
if exam_score >= grade_boundaries["A"]:
    grade = "A"
elif exam_score >= grade_boundaries["B"]:
    grade = "B"
elif exam_score >= grade_boundaries["C"]:
    grade = "C"
elif exam_score >= grade_boundaries["D"]:
    grade = "D"
else:
    grade = "F"

print(f"\n{'='*40}")
print(f"  STUDENT: {student_name}")
print(f"  Score  : {exam_score}")
print(f"  Grade  : {grade}")
```

**Milestone output:**
```
========================================
  STUDENT: Jordan
  Score  : 74
  Grade  : C
```

---

### Stage 3 – Logical Operators: Pass/Fail Decision

```python
# Stage 3 – Full pass/fail decision using logical operators
passed = (exam_score >= 50) and (attendance >= 75) and submitted_all and (not on_watchlist)

print(f"\n  Exam passed (≥50)      : {exam_score >= 50}")
print(f"  Attendance OK (≥75%)   : {attendance >= 75}")
print(f"  Submitted all          : {submitted_all}")
print(f"  Not on watchlist       : {not on_watchlist}")
print(f"\n  OVERALL RESULT: {'PASS ✓' if passed else 'FAIL ✗'}")
```

**Milestone output:**
```
  Exam passed (≥50)      : True
  Attendance OK (≥75%)   : True
  Submitted all          : True
  Not on watchlist       : True

  OVERALL RESULT: PASS ✓
```

---

### Stage 4 – Membership: Historical Record Check

```python
# Stage 4 – Check if today's score matches a historical passing score
if exam_score in passed_scores:
    print(f"\n  Score {exam_score} matches a historical passing score.")
else:
    print(f"\n  Score {exam_score} is a new entry in the records.")

# Check if grade is in the premium grade set
top_grades = {"A", "B"}
if grade in top_grades:
    print(f"  Grade {grade} qualifies for Honours mention.")
else:
    print(f"  Grade {grade} does not qualify for Honours mention.")
```

**Milestone output:**
```
  Score 74 matches a historical passing score.
  Grade C does not qualify for Honours mention.
```

---

### Stage 5 – Identity: Watchlist Check

```python
# Stage 5 – Identity check for None and watchlist status
review_flag = None

if review_flag is None:
    print("\n  No review flag set — proceeding normally.")
else:
    print(f"\n  Review flag active: {review_flag}")

default_status = on_watchlist
print(f"  Watchlist flag (is same object): {on_watchlist is default_status}")
```

**Milestone output:**
```
  No review flag set — proceeding normally.
  Watchlist flag (is same object): True
```

---

### Stage 6 – Bitwise: Permission Flags

```python
# Stage 6 – Use bitwise flags to encode student permissions
VIEW_RESULTS  = 0b100   # 4
RESUBMIT      = 0b010   # 2
APPEAL        = 0b001   # 1

# Jordan can view results and appeal, but not resubmit:
jordan_permissions = VIEW_RESULTS | APPEAL
print(f"\n  Permissions (binary)  : {bin(jordan_permissions)}")
print(f"  Can view results      : {bool(jordan_permissions & VIEW_RESULTS)}")
print(f"  Can resubmit          : {bool(jordan_permissions & RESUBMIT)}")
print(f"  Can appeal            : {bool(jordan_permissions & APPEAL)}")
```

**Milestone output:**
```
  Permissions (binary)  : 0b101
  Can view results      : True
  Can resubmit          : False
  Can appeal            : True
```

---

### Stage 7 – Final Report

```python
# Stage 7 – Print the full summary report
print(f"\n{'='*40}")
print(f"       FINAL EVALUATION REPORT")
print(f"{'='*40}")
print(f"  Student    : {student_name}")
print(f"  Score      : {exam_score}/100")
print(f"  Grade      : {grade}")
print(f"  Attendance : {attendance}%")
print(f"  Result     : {'PASS' if passed else 'FAIL'}")
print(f"  Permissions: {bin(jordan_permissions)}")
print(f"{'='*40}")
```

**Final output:**
```
========================================
       FINAL EVALUATION REPORT
========================================
  Student    : Jordan
  Score      : 74/100
  Grade      : C
  Attendance : 88%
  Result     : PASS
  Permissions: 0b101
========================================
```

---

### Reflection Questions

1. In Stage 3, why did we wrap `not on_watchlist` in the `and` chain rather than using `or`?
2. Why is `is None` preferred over `== None` in Stage 5?
3. In Stage 6, what single bitwise operation would grant **all three** permissions at once?
4. How would the grade calculation in Stage 2 change if you reversed the order of `elif` conditions?
5. Which operator has higher precedence: `and` or `or`? How does this affect Stage 3?

### Optional Extensions

- Add a function that accepts any student's data and returns their full report
- Store multiple students in a list of dictionaries and loop through them
- Add a grade weighting system (e.g., attendance counts for 20% of the final result)
- Use `<<` to create permission levels (1 = basic, 2 = standard, 4 = premium) and check them with `>>`

---

## Part 9 – Common Beginner Mistakes (All Operators)

### Mistake 1 – Using `=` instead of `==` in a condition

```python
# WRONG
x = 10
if x = 10:         # SyntaxError
    print("yes")
```

```python
# CORRECT
if x == 10:
    print("yes")
```

---

### Mistake 2 – Using `==` instead of `is` for `None`

```python
# Not recommended
if result == None:
    pass

# Correct (PEP 8 standard)
if result is None:
    pass
```

---

### Mistake 3 – Assuming `is` checks value equality

```python
a = [1, 2, 3]
b = [1, 2, 3]

# WRONG assumption
if a is b:
    print("same")    # Will NOT print — they are different objects

# CORRECT
if a == b:
    print("same values")    # Will print
```

---

### Mistake 4 – Forgetting `not in` — using `not x in` instead

```python
fruits = ["apple", "banana"]

# Works, but not Pythonic
if not "mango" in fruits:
    print("no mango")

# Preferred — cleaner and more readable
if "mango" not in fruits:
    print("no mango")
```

---

### Mistake 5 – Misunderstanding `not` precedence with `and`/`or`

```python
x = True
y = True

print(not x and y)    # = (not x) and y  = False and True = False
print(not (x and y))  # = not (True)     = False
# Both give False here — but they are NOT equivalent in general!

x = True
y = False

print(not x and y)    # = (not True) and False = False and False = False
print(not (x and y))  # = not (True and False) = not False = True
```

---

### Mistake 6 – Misreading bitwise `&` and `|` as logical `and`/`or`

```python
a = 4
b = 3

print(a and b)   # Logical and → returns b (3) because a is truthy
print(a & b)     # Bitwise AND → 100 & 011 = 000 = 0
```

**Expected output:**
```
3
0
```

> These operators look similar but behave very differently. Use `and`/`or` for True/False logic. Use `&`/`|` for integer bit manipulation.

---

### Mistake 7 – Ignoring precedence and getting wrong results

```python
# WRONG assumption: evaluated left to right
result = True or False and False
# Actual: (True) or (False and False) = True or False = True
print(result)   # True — but a beginner might expect False
```

**Fix:** Use parentheses to make intent explicit:

```python
result = (True or False) and False   # Now evaluates left part first → False
print(result)   # False
```

---

## Reflection Questions

1. What is the difference between `==` (equality) and `is` (identity)?
2. Why does `and` return `False` if only one condition is `False`?
3. When would you use `or` instead of `and`?
4. What does `not` do to a `True` value?
5. Why is `is None` better style than `== None`?
6. What does `in` check for when used on a dictionary?
7. What is the binary representation of the number `13`?
8. What is the result of `8 >> 2`?
9. Which has higher precedence: `and` or `or`?
10. If you write `2 + 3 * 4`, what is evaluated first and why?
11. How do parentheses affect operator precedence?
12. What does "short-circuit evaluation" mean in the context of `and`?

---

## Completion Checklist

Before moving to Lesson 07, confirm you can:

- [ ] Use all six comparison operators (`==`, `!=`, `>`, `<`, `>=`, `<=`)
- [ ] Explain and demonstrate the difference between `=` and `==`
- [ ] Use `and`, `or`, and `not` to combine conditions
- [ ] Describe short-circuit evaluation
- [ ] Explain the difference between `is` and `==`
- [ ] Use `is None` and `is not None` correctly
- [ ] Use `in` and `not in` on lists, strings, tuples, sets, and dictionaries
- [ ] Explain what a bit is and convert small numbers to binary
- [ ] Apply `&`, `|`, `^`, `~`, `<<`, and `>>` to integers
- [ ] Explain Python's operator precedence order
- [ ] Use parentheses to control evaluation order
- [ ] Predict the output of mixed-operator expressions
- [ ] Complete the Student Evaluation System mini-project

---

## Lesson Summary

In this lesson you mastered all six remaining Python operator groups — the tools that power every decision, condition, and expression in real Python programs.

**Comparison operators** (`==`, `!=`, `>`, `<`, `>=`, `<=`) compare two values and produce `True` or `False`. The single most important rule: never confuse `=` (assignment) with `==` (comparison).

**Logical operators** (`and`, `or`, `not`) combine conditions. `and` requires all conditions to be `True`; `or` requires at least one; `not` reverses a boolean. Python uses short-circuit evaluation to skip unnecessary checks.

**Identity operators** (`is`, `is not`) check whether two variables point to the *same object in memory*, not just the same value. Use `is None` for None checks — never `== None`.

**Membership operators** (`in`, `not in`) check whether a value exists inside a list, string, tuple, set, or dictionary. On dictionaries, `in` checks keys by default.

**Bitwise operators** (`&`, `|`, `^`, `~`, `<<`, `>>`) manipulate the individual binary bits of integers. They are essential in systems programming, permissions management, network operations, and performance-critical code.

**Operator precedence** defines the order in which Python evaluates a complex expression: parentheses first, then exponentiation, then arithmetic, then shifts, then bitwise, then comparisons, then `not`, then `and`, then `or`. When in doubt, add parentheses to make your intent clear.

---

*End of Lesson 06 – Python Operators*
