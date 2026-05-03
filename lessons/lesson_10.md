---
render_with_liquid: false
title: "Lesson 10 – Python Operators"
nav_order: 10
---

# Lesson 10 – Python Operators

---

## Lesson Introduction

Every useful computer program makes decisions, performs calculations, and compares values. To do all of this, Python relies on **operators** — special symbols and keywords that instruct Python to perform a specific action on one or more values.

Think of operators as the verbs of the Python language. Just like the word *"add"* or *"compare"* tells a person what action to take, an operator tells Python what to do with the values around it.

In this lesson, you will learn **seven categories** of Python operators, each with a different purpose:

1. **Arithmetic Operators** — perform mathematical calculations (`+`, `-`, `*`, `/`, `%`, `**`, `//`)
2. **Assignment Operators** — store or update values in variables (`=`, `+=`, `-=`, etc.)
3. **Comparison Operators** — compare two values and return `True` or `False` (`==`, `!=`, `>`, `<`, etc.)
4. **Logical Operators** — combine multiple conditions (`and`, `or`, `not`)
5. **Identity Operators** — check whether two variables point to the same object in memory (`is`, `is not`)
6. **Membership Operators** — check whether a value exists inside a collection (`in`, `not in`)
7. **Bitwise Operators** — work at the binary (bit-level) of numbers (`&`, `|`, `^`, `~`, `<<`, `>>`)

You will also learn the critical concept of **Operator Precedence** — what happens when multiple operators appear together in one expression, and which one Python handles first.

By the end of this lesson, you will be able to:

- Use all seven categories of Python operators correctly
- Write expressions that combine multiple operators
- Understand why `2 + 3 * 4` equals `14` and not `20`
- Use comparison and logical operators to control program flow
- Distinguish between `==` (equality check) and `=` (assignment)
- Distinguish between `is` (identity) and `==` (value equality)
- Apply compound assignment operators to write cleaner, shorter code
- Understand bitwise operators and when they are useful
- Read and apply Python's full operator precedence table

---

## Prerequisite Concepts

Before starting this lesson, you should be comfortable with:

**Variables** — Storing values: `x = 10` (covered in Lesson 04)

**Data Types** — Numbers (`int`, `float`) and booleans (`True`/`False`) — covered in Lessons 06 and 09

**The `print()` function** — Displaying results on screen (Lesson 01)

**Booleans** — The values `True` and `False`, which are the result of comparisons (Lesson 09). If you haven't studied Lesson 09 yet, know this: a **boolean** is a data type that holds only one of two values — `True` or `False`. Comparison operators always produce a boolean result.

---

## Section 1 — What Is an Operator?

### The concept

An **operator** is a symbol (or keyword) that tells Python to perform a specific operation on one or more **operands**. An **operand** is the value that the operator acts upon.

**Example:**

```python
result = 10 + 3
```

In this expression:
- `10` and `3` are the **operands**
- `+` is the **operator** (addition)
- `result` receives the **output** of the operation (which is `13`)

This pattern — operand, operator, operand — is called an **expression**. Python evaluates expressions and produces a result.

### The seven categories at a glance

| Category | Purpose | Example |
|----------|---------|---------|
| Arithmetic | Maths calculations | `5 + 3` → `8` |
| Assignment | Store/update variables | `x += 5` |
| Comparison | Compare two values | `5 > 3` → `True` |
| Logical | Combine conditions | `True and False` → `False` |
| Identity | Check same object in memory | `x is y` |
| Membership | Check if value is in collection | `"a" in "Lagos"` |
| Bitwise | Binary/bit manipulation | `5 & 3` → `1` |

---

## Section 2 — Arithmetic Operators

### What are arithmetic operators?

Arithmetic operators are used to perform **mathematical operations** on numbers — exactly like the operations you learned in primary school mathematics, extended with a few extras that are especially useful in programming.

Python has **seven** arithmetic operators.

---

### 2.1 — Addition: `+`

Adds two numbers together.

```python
price_suya = 1500
price_malt = 500
total = price_suya + price_malt
print(total)
```

**Expected output:**
```
2000
```

The `+` operator also works on strings (joining them) — you studied this in Lesson 08. But when used with numbers, it performs pure addition.

---

### 2.2 — Subtraction: `-`

Subtracts the right operand from the left operand.

```python
salary = 150000
rent = 45000
remaining = salary - rent
print(remaining)
```

**Expected output:**
```
105000
```

---

### 2.3 — Multiplication: `*`

Multiplies two numbers.

```python
daily_wage = 5000
days_worked = 22
total_pay = daily_wage * days_worked
print(total_pay)
```

**Expected output:**
```
110000
```

---

### 2.4 — Division: `/`

Divides the left number by the right number. The result is **always a float** (decimal number), even if the division is exact.

```python
total_items = 120
groups = 4
per_group = total_items / groups
print(per_group)
```

**Expected output:**
```
30.0
```

Notice `30.0` — not `30`. Division in Python always produces a float.

---

### 2.5 — Floor Division: `//`

Floor division divides two numbers and then **rounds DOWN** to the nearest whole number (discarding the decimal part). It always returns an integer.

**Analogy:** If you are sharing 7 pieces of puff-puff equally among 2 people, each person gets 3 whole pieces — and 1 is left over. Floor division gives you the "3" (the whole number each person receives).

```python
puff_puff = 7
people = 2
each_gets = puff_puff // people
print(each_gets)
```

**Expected output:**
```
3
```

Compare regular division vs floor division:

```python
print(7 / 2)    # Regular division → 3.5 (float)
print(7 // 2)   # Floor division  → 3   (integer, rounds down)
print(9 / 4)    # → 2.25
print(9 // 4)   # → 2
```

**Expected output:**
```
3.5
3
2.25
2
```

> 🤔 **Thinking Prompt:** What does `10 // 3` give? What about `-7 // 2`? (Hint: floor division always rounds *down*, not toward zero — try it!)

---

### 2.6 — Modulus: `%`

The **modulus** operator (also called the remainder operator) returns the **remainder** after division. It answers the question: *"After dividing as many whole times as possible, what is left over?"*

Using the same puff-puff analogy: after each person gets 3 pieces, 1 piece remains. The modulus gives you that remaining `1`.

```python
puff_puff = 7
people = 2
leftover = puff_puff % people
print(leftover)
```

**Expected output:**
```
1
```

More examples:

```python
print(10 % 3)   # 10 ÷ 3 = 3 remainder 1 → 1
print(15 % 5)   # 15 ÷ 5 = 3 remainder 0 → 0
print(17 % 4)   # 17 ÷ 4 = 4 remainder 1 → 1
```

**Expected output:**
```
1
0
1
```

**Real-world uses of modulus:**
- Check if a number is even (`number % 2 == 0` → no remainder → even)
- Check if a number is odd (`number % 2 == 1` → remainder 1 → odd)
- Cycling through a list repeatedly (wrapping around)
- Extracting individual digits from a number

```python
# Is 48 even or odd?
number = 48
if number % 2 == 0:
    print(f"{number} is even.")
else:
    print(f"{number} is odd.")
```

**Expected output:**
```
48 is even.
```

---

### 2.7 — Exponentiation: `**`

The `**` operator raises the left number to the **power** of the right number. This is the same as writing "x to the power of y" in mathematics.

**Analogy:** `2 ** 10` means "2 multiplied by itself 10 times" = 1024.

```python
print(2 ** 3)    # 2³ = 2 × 2 × 2 = 8
print(5 ** 2)    # 5² = 25
print(10 ** 6)   # 10⁶ = 1,000,000
```

**Expected output:**
```
8
25
1000000
```

Real-world use: calculating compound interest, population growth models, areas of squares, and exponential growth/decay in science.

```python
# Area of a square plot in Lekki with side = 15 metres
side = 15
area = side ** 2
print(f"Area: {area} square metres")
```

**Expected output:**
```
Area: 225 square metres
```

---

### Arithmetic Operators Summary Table

| Operator | Name | Example | Result |
|----------|------|---------|--------|
| `+` | Addition | `10 + 4` | `14` |
| `-` | Subtraction | `10 - 4` | `6` |
| `*` | Multiplication | `10 * 4` | `40` |
| `/` | Division | `10 / 4` | `2.5` |
| `//` | Floor Division | `10 // 4` | `2` |
| `%` | Modulus | `10 % 4` | `2` |
| `**` | Exponentiation | `10 ** 4` | `10000` |

---

## Section 3 — Assignment Operators

### What is an assignment operator?

An **assignment operator** stores a value into a variable. The most basic one is `=` which you have been using since Lesson 04.

```python
city = "Lagos"   # stores the string "Lagos" into city
score = 95       # stores the integer 95 into score
```

But Python also provides **compound assignment operators** — shortcuts that perform an arithmetic operation AND store the result back into the same variable, all in one step.

### Why compound assignment operators exist

Without compound operators, updating a variable requires writing it twice:

```python
score = 80
score = score + 10   # traditional way
print(score)         # 90
```

With compound assignment, you can shorten this to:

```python
score = 80
score += 10          # shortcut!
print(score)         # 90
```

Both do exactly the same thing — `score += 10` means *"take the current value of `score`, add 10 to it, and store the result back into `score`."*

---

### 3.1 — All Assignment Operators

Let's walk through each one with examples. We'll use a running example of a bank account balance:

```python
balance = 50000   # Starting balance: ₦50,000
```

**`=` — Simple assignment**
```python
balance = 50000
print(balance)   # 50000
```

**`+=` — Add and assign** (deposit money)
```python
balance = 50000
balance += 10000   # Same as: balance = balance + 10000
print(balance)     # 60000
```

**`-=` — Subtract and assign** (withdraw money)
```python
balance = 50000
balance -= 5000    # Same as: balance = balance - 5000
print(balance)     # 45000
```

**`*=` — Multiply and assign** (apply interest multiplier)
```python
balance = 50000
balance *= 2       # Same as: balance = balance * 2
print(balance)     # 100000
```

**`/=` — Divide and assign**
```python
balance = 50000
balance /= 4       # Same as: balance = balance / 4
print(balance)     # 12500.0
```

**`//=` — Floor divide and assign**
```python
score = 17
score //= 5        # Same as: score = score // 5
print(score)       # 3
```

**`%=` — Modulus and assign**
```python
items = 17
items %= 5         # Same as: items = items % 5
print(items)       # 2
```

**`**=` — Exponent and assign**
```python
side = 5
side **= 2         # Same as: side = side ** 2
print(side)        # 25
```

---

### 3.2 — Bitwise Assignment Operators

Python also has compound assignment versions of the bitwise operators. You will learn the full details of bitwise operators in Section 8, but here is the list for completeness:

| Operator | Example | Equivalent to |
|----------|---------|--------------|
| `&=` | `x &= 3` | `x = x & 3` |
| `\|=` | `x \|= 3` | `x = x \| 3` |
| `^=` | `x ^= 3` | `x = x ^ 3` |
| `>>=` | `x >>= 1` | `x = x >> 1` |
| `<<=` | `x <<= 1` | `x = x << 1` |

---

### Assignment Operators Summary Table

| Operator | Example | Equivalent to | Description |
|----------|---------|---------------|-------------|
| `=` | `x = 5` | — | Simple assignment |
| `+=` | `x += 5` | `x = x + 5` | Add and assign |
| `-=` | `x -= 5` | `x = x - 5` | Subtract and assign |
| `*=` | `x *= 5` | `x = x * 5` | Multiply and assign |
| `/=` | `x /= 5` | `x = x / 5` | Divide and assign |
| `//=` | `x //= 5` | `x = x // 5` | Floor divide and assign |
| `%=` | `x %= 5` | `x = x % 5` | Modulus and assign |
| `**=` | `x **= 5` | `x = x ** 5` | Exponentiate and assign |

---

## Section 4 — Comparison Operators

### What are comparison operators?

**Comparison operators** compare two values and return either `True` or `False`. They are the backbone of decision-making in Python — every `if` statement (coming in a future lesson) relies on comparison operators.

**Analogy:** Imagine a gateman at the University of Lagos. He has a list of rules: "Is this person a student? Is their age at least 18? Is their ID number correct?" Each rule is a comparison — it either passes (`True`) or fails (`False`).

---

### The Critical Distinction: `=` vs `==`

Before we begin, you must understand this crucial difference:

| Symbol | Name | Purpose |
|--------|------|---------|
| `=` | Assignment operator | **Stores** a value into a variable: `x = 5` |
| `==` | Equality operator | **Compares** two values and returns True or False: `x == 5` |

Confusing these two is one of the most common errors for beginners!

```python
x = 10        # Assignment: store 10 in x
print(x == 10)   # Comparison: is x equal to 10? → True
print(x == 5)    # Comparison: is x equal to 5?  → False
```

---

### 4.1 — Equal to: `==`

Returns `True` if both sides have the **same value**.

```python
score = 75
print(score == 75)   # True
print(score == 80)   # False

name = "Amaka"
print(name == "Amaka")   # True
print(name == "amaka")   # False (case-sensitive!)
```

**Expected output:**
```
True
False
True
False
```

---

### 4.2 — Not equal to: `!=`

Returns `True` if the two values are **different**.

```python
city = "Lagos"
print(city != "Abuja")   # True (they are different)
print(city != "Lagos")   # False (they are the same)
```

**Expected output:**
```
True
False
```

---

### 4.3 — Greater than: `>`

Returns `True` if the left value is **greater than** the right value.

```python
price = 2500
budget = 2000
print(price > budget)    # True (2500 is greater than 2000)
print(budget > price)    # False
```

**Expected output:**
```
True
False
```

---

### 4.4 — Less than: `<`

Returns `True` if the left value is **less than** the right value.

```python
age = 15
minimum_age = 18
print(age < minimum_age)    # True (15 is less than 18)
print(minimum_age < age)    # False
```

**Expected output:**
```
True
False
```

---

### 4.5 — Greater than or equal to: `>=`

Returns `True` if the left value is **greater than OR equal to** the right.

```python
score = 50
pass_mark = 50
print(score >= pass_mark)   # True (50 is equal to 50, so >= is True)

score = 49
print(score >= pass_mark)   # False (49 < 50)
```

**Expected output:**
```
True
False
```

---

### 4.6 — Less than or equal to: `<=`

Returns `True` if the left value is **less than OR equal to** the right.

```python
temperature = 30
heat_alert_level = 35
print(temperature <= heat_alert_level)   # True (30 ≤ 35)
```

**Expected output:**
```
True
```

---

### Comparison Operators Summary Table

| Operator | Name | Example | Result |
|----------|------|---------|--------|
| `==` | Equal to | `5 == 5` | `True` |
| `!=` | Not equal to | `5 != 3` | `True` |
| `>` | Greater than | `5 > 3` | `True` |
| `<` | Less than | `3 < 5` | `True` |
| `>=` | Greater than or equal to | `5 >= 5` | `True` |
| `<=` | Less than or equal to | `3 <= 5` | `True` |

---

### Combining comparisons in a real scenario

```python
# JAMB score eligibility check
jamb_score = 230
minimum_jamb = 200
maximum_age = 35
applicant_age = 24

score_ok = jamb_score >= minimum_jamb
age_ok = applicant_age <= maximum_age

print(f"Score qualifies: {score_ok}")
print(f"Age qualifies:   {age_ok}")
```

**Expected output:**
```
Score qualifies: True
Age qualifies:   True
```

---

## Section 5 — Logical Operators

### What are logical operators?

**Logical operators** allow you to combine multiple conditions into one. Instead of only asking "Is A true?", you can ask "Is A true AND is B also true?" or "Is A true OR is B true?"

Python has three logical operators: `and`, `or`, and `not`.

---

### 5.1 — `and` — Both must be True

The `and` operator returns `True` only if **both** conditions are `True`. If even one condition is `False`, the result is `False`.

**Analogy:** To be admitted to study Medicine at UNILAG, you must BOTH have a high JAMB score AND pass your post-UTME. Both conditions must be satisfied.

```python
jamb_score = 280
post_utme = 75

qualifies = jamb_score >= 250 and post_utme >= 60
print(qualifies)
```

**Expected output:**
```
True
```

Let's trace this:
- `jamb_score >= 250` → `280 >= 250` → `True`
- `post_utme >= 60` → `75 >= 60` → `True`
- `True and True` → `True`

What if the post-UTME score was 45?

```python
jamb_score = 280
post_utme = 45

qualifies = jamb_score >= 250 and post_utme >= 60
print(qualifies)
```

**Expected output:**
```
False
```

- `True and False` → `False` (because both must be True)

**Truth table for `and`:**

| A | B | A and B |
|---|---|---------|
| True | True | **True** |
| True | False | False |
| False | True | False |
| False | False | False |

---

### 5.2 — `or` — At least one must be True

The `or` operator returns `True` if **at least one** of the conditions is `True`. It only returns `False` when **both** conditions are `False`.

**Analogy:** To qualify for a student discount at a Lagos cinema, you need to show either a valid student ID OR a school uniform. Either one is acceptable.

```python
has_id = False
wearing_uniform = True

gets_discount = has_id or wearing_uniform
print(gets_discount)
```

**Expected output:**
```
True
```

**Truth table for `or`:**

| A | B | A or B |
|---|---|--------|
| True | True | True |
| True | False | True |
| False | True | True |
| False | False | **False** |

```python
# Real example: check if a number is outside a valid range
temperature = 42
is_extreme = temperature < 10 or temperature > 40
print(f"Extreme temperature alert: {is_extreme}")
```

**Expected output:**
```
Extreme temperature alert: True
```

---

### 5.3 — `not` — Reverses the result

The `not` operator takes a single boolean value and **flips it**: `True` becomes `False`, and `False` becomes `True`.

```python
is_raining = True
print(not is_raining)    # False

is_sunny = False
print(not is_sunny)      # True
```

**Expected output:**
```
False
True
```

**Truth table for `not`:**

| A | not A |
|---|-------|
| True | False |
| False | True |

Practical use:

```python
user_logged_in = False

if not user_logged_in:
    print("Please log in first.")
```

**Expected output:**
```
Please log in first.
```

---

### 5.4 — Combining `and`, `or`, and `not`

You can combine all three in a single expression. Python evaluates `not` first, then `and`, then `or` (you'll learn the full order in Section 9).

```python
age = 20
has_invitation = True
is_vip = False

can_enter = age >= 18 and (has_invitation or is_vip)
print(can_enter)
```

**Expected output:**
```
True
```

Trace:
- `age >= 18` → `True`
- `has_invitation or is_vip` → `True or False` → `True`
- `True and True` → `True`

---

## Section 6 — Identity Operators

### What are identity operators?

**Identity operators** check whether two variables point to the **exact same object in memory** — not just whether they have the same value.

This is a subtle but important distinction. Two variables might hold equal values but be stored in different memory locations, or they might share the exact same memory location.

**Analogy:** Two students, Emeka and Tunde, both own a copy of the same textbook. They have **equal** books (same content), but they are **not identical** books (not the same physical object). Identity operators check whether two variables are pointing to the very same book, not just whether the books look the same.

Python has two identity operators: `is` and `is not`.

---

### 6.1 — `is` — Same object in memory?

```python
a = [1, 2, 3]
b = a          # b and a point to the SAME list object
c = [1, 2, 3]  # c is a NEW list with the same values

print(a is b)   # True (same object)
print(a is c)   # False (different objects, even though values are equal)
print(a == c)   # True (values are equal)
```

**Expected output:**
```
True
False
True
```

This reveals an important insight: `is` checks **identity** (same object), while `==` checks **equality** (same value). They are not the same thing!

---

### 6.2 — `is not` — Different objects in memory?

```python
x = [10, 20]
y = [10, 20]

print(x is not y)    # True (different objects)
print(x != y)        # False (values are equal)
```

**Expected output:**
```
True
False
```

---

### 6.3 — Identity and `None`

The most common real-world use of `is` is checking whether a variable holds the special value `None` (Python's way of representing "nothing" or "no value").

The Python style guide (PEP 8) specifically recommends using `is` instead of `==` when comparing to `None`:

```python
result = None

if result is None:
    print("No result was returned yet.")
else:
    print(f"Result: {result}")
```

**Expected output:**
```
No result was returned yet.
```

---

### 6.4 — Small integers behave differently (a detail worth knowing)

Python caches (pre-creates and reuses) small integers (typically -5 to 256) for efficiency. This can create surprising results:

```python
a = 5
b = 5
print(a is b)   # True! Python reuses the same object for small integers

x = 1000
y = 1000
print(x is y)   # May be False! Large integers are separate objects
```

This is a quirk of CPython (the standard Python implementation), not something you typically design around. For checking equality, always use `==`. Reserve `is` for checking `None` or object identity.

---

### Identity Operators Summary Table

| Operator | Name | Example | Checks |
|----------|------|---------|--------|
| `is` | Identity | `x is y` | Are `x` and `y` the same object in memory? |
| `is not` | Non-identity | `x is not y` | Are `x` and `y` different objects in memory? |

---

## Section 7 — Membership Operators

### What are membership operators?

**Membership operators** check whether a value exists **inside** a collection — a string, a list, a tuple, a dictionary, or a set. They return `True` or `False`.

You have already used membership operators in Lesson 08 to check whether a word exists in a string. Now we formalise this concept.

Python has two membership operators: `in` and `not in`.

---

### 7.1 — `in` — Is the value inside the collection?

**In a string:**
```python
state = "Rivers State"
print("Rivers" in state)    # True
print("Lagos" in state)     # False
```

**Expected output:**
```
True
False
```

**In a list:**
```python
nigerian_capitals = ["Abuja", "Lagos", "Kano", "Ibadan", "Enugu"]
print("Abuja" in nigerian_capitals)    # True
print("Accra" in nigerian_capitals)   # False (that's Ghana's capital)
```

**Expected output:**
```
True
False
```

**In a string of characters:**
```python
vowels = "aeiouAEIOU"
letter = "E"
print(letter in vowels)   # True
```

---

### 7.2 — `not in` — Is the value absent from the collection?

```python
allergens = ["peanuts", "shellfish", "dairy"]
food = "wheat"

print(food not in allergens)    # True (wheat is not in the list)
print("dairy" not in allergens)  # False (dairy IS in the list)
```

**Expected output:**
```
True
False
```

---

### 7.3 — Practical example: menu ordering system

```python
available_dishes = ["Jollof Rice", "Egusi Soup", "Suya", "Puff Puff", "Ofada Rice"]

customer_order = "Banga Soup"

if customer_order in available_dishes:
    print(f"Your order for {customer_order} has been placed!")
else:
    print(f"Sorry, {customer_order} is not on today's menu.")
```

**Expected output:**
```
Sorry, Banga Soup is not on today's menu.
```

---

### Membership Operators Summary Table

| Operator | Name | Example | Returns |
|----------|------|---------|---------|
| `in` | Membership | `"a" in "Amaka"` | `True` if value found in collection |
| `not in` | Non-membership | `"z" not in "Amaka"` | `True` if value NOT in collection |

---

## Section 8 — Bitwise Operators

### What are bitwise operators?

**Bitwise operators** work on **binary representations** of integers — they operate on the individual bits (0s and 1s) that make up a number at the lowest level of computing.

Before learning the operators, you need a brief foundation in how numbers are stored in binary.

### Prerequisite: Binary Numbers

Every integer you use in Python is stored internally as a sequence of bits (binary digits: 0 or 1). A **bit** is the smallest unit of computer storage — it holds either a 0 or a 1.

| Decimal | Binary |
|---------|--------|
| 0 | `0000` |
| 1 | `0001` |
| 2 | `0010` |
| 3 | `0011` |
| 4 | `0100` |
| 5 | `0101` |
| 6 | `0110` |
| 7 | `0111` |
| 8 | `1000` |
| 9 | `1001` |
| 10 | `1010` |

Think of binary as a number system that only uses two digits: 0 and 1. Each position from right to left represents a power of 2: `1, 2, 4, 8, 16, 32, ...`

For example: `5` in binary is `0101`, which means `(0×8) + (1×4) + (0×2) + (1×1) = 5`.

Bitwise operators apply operations to each corresponding pair of bits across two numbers.

---

### 8.1 — Bitwise AND: `&`

Compares each bit position. Returns `1` only if **both** bits are `1`. (Similar to logical `and`, but for individual bits.)

```python
print(5 & 3)
```

Working it out:
```
  5 = 0101
  3 = 0011
  & = 0001  (only where both are 1)
      = 1
```

**Expected output:**
```
1
```

---

### 8.2 — Bitwise OR: `|`

Returns `1` if **at least one** bit is `1`. (Similar to logical `or`, but for individual bits.)

```python
print(5 | 3)
```

Working it out:
```
  5 = 0101
  3 = 0011
  | = 0111  (wherever either is 1)
      = 7
```

**Expected output:**
```
7
```

---

### 8.3 — Bitwise XOR: `^`

Returns `1` if the bits are **different** (one is 0 and the other is 1). Returns `0` if both bits are the same.

```python
print(5 ^ 3)
```

Working it out:
```
  5 = 0101
  3 = 0011
  ^ = 0110  (where bits differ)
      = 6
```

**Expected output:**
```
6
```

---

### 8.4 — Bitwise NOT: `~`

Inverts all the bits. The result is `-(x + 1)` for any integer `x`. This is due to how computers represent negative numbers using a method called "two's complement."

```python
print(~5)    # -(5+1) = -6
print(~0)    # -(0+1) = -1
print(~-1)   # -(-1+1) = 0
```

**Expected output:**
```
-6
-1
0
```

---

### 8.5 — Left Shift: `<<`

Shifts all bits to the **left** by the specified number of positions. Each left shift effectively **multiplies by 2**.

```python
print(5 << 1)    # 0101 → 1010 = 10  (5 × 2)
print(5 << 2)    # 0101 → 10100 = 20 (5 × 4)
print(3 << 3)    # 011  → 011000 = 24 (3 × 8)
```

**Expected output:**
```
10
20
24
```

---

### 8.6 — Right Shift: `>>`

Shifts all bits to the **right** by the specified number of positions. Each right shift effectively **divides by 2** (integer division).

```python
print(20 >> 1)   # 20 ÷ 2 = 10
print(20 >> 2)   # 20 ÷ 4 = 5
print(7 >> 1)    # 7 ÷ 2 = 3  (floor division)
```

**Expected output:**
```
10
5
3
```

---

### Bitwise Operators Summary Table

| Operator | Name | Example | Result | Description |
|----------|------|---------|--------|-------------|
| `&` | AND | `5 & 3` | `1` | 1 if both bits are 1 |
| `\|` | OR | `5 \| 3` | `7` | 1 if at least one bit is 1 |
| `^` | XOR | `5 ^ 3` | `6` | 1 if bits are different |
| `~` | NOT | `~5` | `-6` | Invert all bits |
| `<<` | Left shift | `5 << 1` | `10` | Shift bits left (×2 per shift) |
| `>>` | Right shift | `20 >> 1` | `10` | Shift bits right (÷2 per shift) |

### When are bitwise operators used?

Bitwise operators are used in:
- **Systems programming** — directly manipulating hardware registers or flags
- **Cryptography** — encoding and decoding data
- **Network programming** — working with IP addresses and subnet masks
- **Performance optimisation** — multiplying or dividing by powers of 2 very quickly
- **Embedded systems** — controlling hardware pins on microcontrollers
- **Permissions systems** — Linux file permissions use bitwise flags

For everyday Python scripting and data analysis, you will rarely need bitwise operators. But understanding them is important for a complete knowledge of the language.

---

## Section 9 — Operator Precedence

### What is operator precedence?

When you write an expression with multiple operators, Python must decide **which operation to perform first**. The rules that determine this order are called **operator precedence** — similar to the mathematical rules of BODMAS/PEMDAS you learned in secondary school.

### The problem this solves

Consider:

```python
result = 2 + 3 * 4
print(result)
```

Should Python do `2 + 3` first (getting `5`) and then `5 * 4` = `20`? Or should it do `3 * 4` first (getting `12`) and then `2 + 12` = `14`?

```
Expected output:
14
```

Python correctly gives `14`, because multiplication (`*`) has **higher precedence** than addition (`+`), so `3 * 4 = 12` is evaluated first, then `2 + 12 = 14`.

This is exactly the same as BODMAS: **Brackets, Orders (powers), Division/Multiplication, Addition/Subtraction**.

---

### 9.1 — Python's Full Precedence Table

The table below lists operators from **highest precedence** (evaluated first) to **lowest precedence** (evaluated last). When two operators have the same precedence level, Python evaluates them **left to right** (with some exceptions noted).

| Priority | Operator(s) | Description |
|----------|-------------|-------------|
| 1 (Highest) | `()` | Parentheses / grouping |
| 2 | `**` | Exponentiation |
| 3 | `+x`, `-x`, `~x` | Unary plus, minus, bitwise NOT |
| 4 | `*`, `/`, `//`, `%` | Multiplication, division, floor div, modulus |
| 5 | `+`, `-` | Addition, subtraction |
| 6 | `<<`, `>>` | Bitwise shifts |
| 7 | `&` | Bitwise AND |
| 8 | `^` | Bitwise XOR |
| 9 | `\|` | Bitwise OR |
| 10 | `==`, `!=`, `>`, `<`, `>=`, `<=`, `is`, `is not`, `in`, `not in` | Comparisons, identity, membership |
| 11 | `not` | Logical NOT |
| 12 | `and` | Logical AND |
| 13 (Lowest) | `or` | Logical OR |

---

### 9.2 — Worked Examples

**Example 1: Arithmetic precedence**
```python
print(2 + 3 * 4)       # 3 * 4 = 12 first, then 2 + 12 = 14
print((2 + 3) * 4)     # 2 + 3 = 5 first (parentheses), then 5 * 4 = 20
print(2 ** 3 + 1)      # 2 ** 3 = 8 first, then 8 + 1 = 9
print(10 - 2 * 3 + 1)  # 2 * 3 = 6, then 10 - 6 + 1 = 5
```

**Expected output:**
```
14
20
9
5
```

**Example 2: Comparison and logical precedence**
```python
x = 5
print(x > 2 and x < 10)
# Evaluated as: (x > 2) and (x < 10)
# → True and True → True
```

**Expected output:**
```
True
```

**Example 3: Mixing arithmetic and comparison**
```python
print(2 + 3 > 4)
# 2 + 3 = 5 first (arithmetic before comparison)
# then 5 > 4 → True
```

**Expected output:**
```
True
```

**Example 4: `not` before `and` before `or`**
```python
print(True or False and False)
# and evaluates before or
# False and False = False first
# True or False = True
print(True)
```

**Expected output:**
```
True
```

```python
print(not True or True)
# not evaluates before or
# not True = False first
# False or True = True
```

**Expected output:**
```
True
```

---

### 9.3 — The Golden Rule: Use Parentheses When in Doubt

Even experienced programmers sometimes forget exact precedence rules. The safest practice is to use **parentheses `()`** to make your intention absolutely clear:

```python
# Hard to read — relies on knowing precedence:
result = 2 + 3 ** 2 * 4 - 1

# Clear and unambiguous — parentheses tell the story:
result = 2 + ((3 ** 2) * 4) - 1
print(result)   # 2 + (9 * 4) - 1 = 2 + 36 - 1 = 37
```

Using parentheses also makes your code easier for other people (and your future self) to understand.

---

### 9.4 — Left-to-Right Evaluation at the Same Level

When operators have equal precedence, Python evaluates them **left to right** (this is called left-associativity):

```python
print(20 - 5 - 3)   # (20 - 5) - 3 = 15 - 3 = 12
print(8 / 4 / 2)    # (8 / 4) / 2 = 2.0 / 2 = 1.0
```

**Expected output:**
```
12
1.0
```

**Exception — Exponentiation is right-associative:**

The `**` operator evaluates **right to left**:

```python
print(2 ** 3 ** 2)
# Evaluated as: 2 ** (3 ** 2) = 2 ** 9 = 512  (NOT (2**3)**2 = 64)
```

**Expected output:**
```
512
```

---

## Section 10 — Guided Practice Exercises

### Exercise 1 — Market Calculator

**Objective:** Use arithmetic and assignment operators to build a simple market shopping calculator.

**Scenario:** Mama Kemi goes to Oyingbo Market in Lagos. Build a program that calculates her total spending, tracks her remaining budget, and tells her whether she can afford an extra item.

```python
# Starting budget
budget = 25000

# Prices of items
tomatoes = 1200
pepper = 800
palm_oil = 2500
stockfish = 4500
garri = 1800

# Calculate total spending
total_spent = tomatoes + pepper + palm_oil + stockfish + garri
print(f"Total spent:     ₦{total_spent}")

# Update budget using compound assignment
budget -= total_spent
print(f"Remaining budget: ₦{budget}")

# Can she afford a ₦3,000 extra item?
extra_item_cost = 3000
can_afford = budget >= extra_item_cost
print(f"Can afford extra item: {can_afford}")

# How many ₦200 sachets of spices can she buy with what's left?
spice_cost = 200
spices_affordable = budget // spice_cost
remainder = budget % spice_cost
print(f"Spices affordable: {spices_affordable} sachets (₦{remainder} left over)")
```

**Expected output:**
```
Total spent:     ₦10800
Remaining budget: ₦14200
Can afford extra item: True
Spices affordable: 71 sachets (₦0 left over)
```

**Self-check questions:**
- What does `budget -= total_spent` mean in long form?
- Why does `budget // spice_cost` give a whole number?
- What operator would you use to check if `total_spent` is less than the full budget?

---

### Exercise 2 — Student Eligibility Checker

**Objective:** Use comparison and logical operators to determine whether a student meets multiple scholarship conditions.

**Scenario:** The Babatunde Educational Foundation awards scholarships to students who: (a) have a GPA of at least 3.5 out of 5.0, AND (b) come from Ogun, Oyo, Ekiti, or Ondo state, AND (c) are between 16 and 25 years old (inclusive).

```python
# Student details
student_name = "Chioma Adaeze"
gpa = 3.8
state = "Ondo"
age = 21

# Condition checks
gpa_ok = gpa >= 3.5
eligible_states = ["Ogun", "Oyo", "Ekiti", "Ondo"]
state_ok = state in eligible_states
age_ok = age >= 16 and age <= 25

# Combined eligibility
is_eligible = gpa_ok and state_ok and age_ok

# Display results
print(f"Student: {student_name}")
print(f"GPA condition met:   {gpa_ok}")
print(f"State condition met: {state_ok}")
print(f"Age condition met:   {age_ok}")
print(f"Overall eligible:    {is_eligible}")

if is_eligible:
    print(f"\n✓ Congratulations, {student_name.split()[0]}! You qualify for the scholarship.")
else:
    print(f"\n✗ Sorry, {student_name.split()[0]}. You do not qualify at this time.")
```

**Expected output:**
```
Student: Chioma Adaeze
GPA condition met:   True
State condition met: True
Age condition met:   True
Overall eligible:    True

✓ Congratulations, Chioma! You qualify for the scholarship.
```

Try changing `gpa = 3.2` and observe how the output changes.

**Self-check questions:**
- Why did we use `in` rather than multiple `==` checks for the state condition?
- What is the difference between `and` and `or` when combining the three conditions?
- Rewrite `age >= 16 and age <= 25` using Python's chained comparison syntax: `16 <= age <= 25`. Do they produce the same result?

---

### Exercise 3 — Bit-Level Permission System

**Objective:** Use bitwise operators to implement a simple Unix-style file permission system.

**Background:** In Unix/Linux systems (including the servers that run most Nigerian banks, universities, and tech companies), file permissions are stored as binary flags. Each user type (Owner, Group, Others) gets 3 bits — one for Read (4), Write (2), and Execute (1). The full permission is often expressed as a combination using bitwise OR.

```python
# Permission bit values
READ    = 4   # binary: 100
WRITE   = 2   # binary: 010
EXECUTE = 1   # binary: 001

# Assign permissions to owner (can read, write, execute)
owner_perms = READ | WRITE | EXECUTE
print(f"Owner permissions:  {owner_perms}")   # 4 | 2 | 1 = 7

# Assign permissions to group (can read and execute only)
group_perms = READ | EXECUTE
print(f"Group permissions:  {group_perms}")   # 4 | 1 = 5

# Assign permissions to others (read only)
other_perms = READ
print(f"Other permissions:  {other_perms}")   # 4

# Check if owner has write permission using bitwise AND
has_write = owner_perms & WRITE
print(f"Owner can write:    {bool(has_write)}")   # True (non-zero = True)

# Check if group has write permission
group_has_write = group_perms & WRITE
print(f"Group can write:    {bool(group_has_write)}")   # False (0 = False)

# Remove execute from group using XOR (toggle off)
group_perms_no_exec = group_perms ^ EXECUTE
print(f"Group (no execute): {group_perms_no_exec}")   # 4 (read only)
```

**Expected output:**
```
Owner permissions:  7
Group permissions:  5
Other permissions:  4
Owner can write:    True
Group can write:    False
Group (no execute): 4
```

**Self-check questions:**
- Why does `4 | 2 | 1` equal 7? Work it out in binary.
- What does `bool(0)` return in Python? What about `bool(4)`?
- What would `READ | WRITE` equal? What does the result mean?

---

## Section 11 — Mini Project: Comprehensive Grade and Scholarship Evaluator

### Project Description

Build a Python program that evaluates a student's academic record and determines their grade classification, scholarship eligibility, and fee discount using all the operator types covered in this lesson.

**Skills covered:** All 7 operator types + precedence + f-strings + compound assignment.

---

### Stage 1 — Collect and Display Student Data

```python
# Student academic record
student_name = "Adebayo Olamide Akinwale"
matric_number = "CSC/2022/0047"
department = "Computer Science"

score_maths      = 78
score_english    = 85
score_cs         = 92
score_physics    = 67
score_stats      = 73

num_courses = 5
```

**Milestone output:** Display the student's name and all five scores before proceeding.

---

### Stage 2 — Calculate GPA and Classify

```python
# Calculate total and average
total_score = score_maths + score_english + score_cs + score_physics + score_stats
average = total_score / num_courses

print(f"Total score:  {total_score}")
print(f"Average:      {average:.1f}%")

# Determine classification using comparison and logical operators
is_first_class      = average >= 70
is_second_upper     = average >= 60 and average < 70
is_second_lower     = average >= 50 and average < 60
is_third_class      = average >= 40 and average < 50
is_fail             = average < 40

if is_first_class:
    classification = "First Class"
elif is_second_upper:
    classification = "Second Class Upper"
elif is_second_lower:
    classification = "Second Class Lower"
elif is_third_class:
    classification = "Third Class"
else:
    classification = "Fail"

print(f"Classification: {classification}")
```

**Expected output (with given scores):**
```
Total score:  395
Average:      79.0%
Classification: First Class
```

---

### Stage 3 — Scholarship and Discount Eligibility

```python
# Scholarship eligibility: First Class AND at least one score >= 90
has_distinction = score_maths >= 90 or score_english >= 90 or score_cs >= 90 or score_physics >= 90 or score_stats >= 90
scholarship_eligible = is_first_class and has_distinction

# Fee discount: Second Class or above (not fail, not third class)
qualifies_for_discount = not is_fail and not is_third_class

# Calculate discount amount (10% for second lower, 20% for second upper, 30% for first class)
base_fee = 150000   # ₦150,000 tuition
discount_rate = 0

if is_first_class:
    discount_rate = 30
elif is_second_upper:
    discount_rate = 20
elif is_second_lower:
    discount_rate = 10

discount_amount = (base_fee * discount_rate) // 100
fee_payable = base_fee - discount_amount
```

---

### Stage 4 — Final Report Card

```python
separator = "=" * 50

print()
print(separator)
print("     FEDERAL UNIVERSITY OTUOKE")
print("     STUDENT ACADEMIC REPORT")
print(separator)
print(f"  Name:           {student_name}")
print(f"  Matric No:      {matric_number}")
print(f"  Department:     {department}")
print(separator)
print(f"  {'Subject':<20} {'Score':>6}")
print(f"  {'-'*28}")
print(f"  {'Mathematics':<20} {score_maths:>6}")
print(f"  {'English':<20} {score_english:>6}")
print(f"  {'Computer Science':<20} {score_cs:>6}")
print(f"  {'Physics':<20} {score_physics:>6}")
print(f"  {'Statistics':<20} {score_stats:>6}")
print(f"  {'-'*28}")
print(f"  {'Total':<20} {total_score:>6}")
print(f"  {'Average':<20} {average:>5.1f}%")
print(separator)
print(f"  Classification:     {classification}")
print(f"  Scholarship:        {'AWARDED ✓' if scholarship_eligible else 'Not awarded'}")
print(f"  Fee Discount:       {discount_rate}%")
print(f"  Base Tuition:       ₦{base_fee:,}")
print(f"  Discount Amount:    ₦{discount_amount:,}")
print(f"  Fee Payable:        ₦{fee_payable:,}")
print(separator)
```

**Expected final output:**
```
==================================================
     FEDERAL UNIVERSITY OTUOKE
     STUDENT ACADEMIC REPORT
==================================================
  Name:           Adebayo Olamide Akinwale
  Matric No:      CSC/2022/0047
  Department:     Computer Science
==================================================
  Subject              Score
  ----------------------------
  Mathematics             78
  English                 85
  Computer Science        92
  Physics                 67
  Statistics              73
  ----------------------------
  Total                  395
  Average               79.0%
==================================================
  Classification:     First Class
  Scholarship:        AWARDED ✓
  Fee Discount:       30%
  Base Tuition:       ₦150,000
  Discount Amount:    ₦45,000
  Fee Payable:        ₦105,000
==================================================
```

### Stage 5 — Reflection Questions

1. Why did we use `//` instead of `/` when calculating `discount_amount`?
2. In the scholarship check, why did we use `or` to combine the individual score comparisons?
3. What operator type determines `not is_fail and not is_third_class`? Could you rewrite this more simply?
4. What would happen to the output if you change `score_cs = 92` to `score_cs = 55`?
5. Where in this project did left-to-right evaluation matter?

### Optional Extension Challenges

- Add a Cumulative Grade Point Average (CGPA) on a 5.0 scale using: `cgpa = (average / 100) * 5`
- Use bitwise operators to encode three boolean flags (scholarship, discount, distinction) into a single integer status code
- Add a check: if ALL five scores are above 60, display "Consistent Performer" on the card
- Apply a 15% late-submission penalty (multiply by 0.85) if `submitted_late = True`

---

## Section 12 — Common Beginner Mistakes

### Mistake 1 — Using `=` Instead of `==` in a Condition

**Wrong:**
```python
score = 75
if score = 75:      # SyntaxError!
    print("Pass")
```

**Correct:**
```python
score = 75
if score == 75:     # == is the comparison operator
    print("Pass")
```

`=` stores a value. `==` compares values. This is one of the most frequent errors in all of programming.

---

### Mistake 2 — Confusing `//` (Floor Division) with `/` (Regular Division)

**Wrong assumption:** "Both give the same result."

```python
print(7 / 2)    # 3.5  (float — keeps the decimal)
print(7 // 2)   # 3    (integer — discards the decimal)
```

Use `//` when you need a whole number result (e.g., how many full portions fit, how many complete weeks in N days).

---

### Mistake 3 — Misunderstanding `%` (Modulus)

Many beginners think `%` means "percentage." It does not — it means **remainder after division**.

```python
print(10 % 3)    # 1  (remainder when 10 is divided by 3)
print(15 % 5)    # 0  (15 divides evenly by 5, no remainder)
```

---

### Mistake 4 — Confusing `is` with `==`

```python
a = [1, 2, 3]
b = [1, 2, 3]

print(a == b)   # True  (same values)
print(a is b)   # False (different objects in memory)
```

Use `==` to compare **values**. Use `is` only to check **object identity** (most commonly: `value is None`).

---

### Mistake 5 — Assuming `and`/`or` Return Only `True`/`False`

In Python, `and` and `or` don't always return a pure boolean — they return one of their operands:

```python
print(0 or "hello")    # "hello" (0 is falsy, so Python returns the second)
print(5 and "hello")   # "hello" (5 is truthy, so Python returns the second)
print(0 and "hello")   # 0 (0 is falsy, so Python returns it immediately)
```

This is called **short-circuit evaluation** and is an advanced detail — for now, always use `and`/`or` with explicit boolean expressions.

---

### Mistake 6 — Forgetting Precedence (Especially `not` and `and` vs `or`)

**Wrong thinking:** "Python evaluates left to right, always."

```python
print(True or False and False)
# Python evaluates 'and' before 'or'
# → True or (False and False)
# → True or False
# → True
```

Use parentheses whenever you combine `and`, `or`, and `not` to make the intended order explicit.

---

### Mistake 7 — Using Arithmetic Operators on Incompatible Types

```python
age = 25
print("My age: " + age)     # TypeError! Can't add str and int
print("My age: " + str(age))  # Correct
print(f"My age: {age}")        # Best practice with f-strings
```

---

## Reflection Questions

Think through these before moving on:

1. In your own words, what is an operator? What is an operand? Give an example of each.
2. What is the difference between `/` and `//`? When would you choose floor division?
3. Explain with an example why `a == b` and `a is b` can give different results.
4. A student has marks: 45, 62, 71, 38, 55. Using only arithmetic operators, how would you find their average? What classification would they get?
5. If `x = 10`, what is the value of `x` after executing `x **= 2`? Then `x //= 3`?
6. Write a single Python expression using `and` and `or` that returns `True` if a number is between 18 and 65 (inclusive) OR is exactly 0.
7. What does `not (True and False)` evaluate to? Trace through it step by step.
8. Why is it important to know operator precedence? Give a real-world example where getting the order wrong would produce a wrong result.

---

## Completion Checklist

Before moving on to the next lesson, confirm you can confidently tick each item:

- [ ] I understand what an operator and an operand are
- [ ] I can use all 7 arithmetic operators: `+`, `-`, `*`, `/`, `//`, `%`, `**`
- [ ] I know the difference between `/` (float result) and `//` (integer result)
- [ ] I understand what the modulus `%` operator returns
- [ ] I can use all compound assignment operators: `+=`, `-=`, `*=`, `/=`, `//=`, `%=`, `**=`
- [ ] I understand the critical difference between `=` (assign) and `==` (compare)
- [ ] I can use all 6 comparison operators: `==`, `!=`, `>`, `<`, `>=`, `<=`
- [ ] I can use `and`, `or`, and `not` to combine conditions
- [ ] I understand the truth tables for `and`, `or`, and `not`
- [ ] I know the difference between `is`/`is not` and `==`/`!=`
- [ ] I can use `in` and `not in` to check membership in strings and lists
- [ ] I can explain what bitwise operators do at the bit level
- [ ] I understand operator precedence and can use parentheses to control evaluation order
- [ ] I completed all three guided exercises and the mini project

---

## Lesson Summary

In this lesson, you mastered all seven categories of Python operators — the core tools Python uses to process data, make decisions, and perform calculations.

**Arithmetic operators** (`+`, `-`, `*`, `/`, `//`, `%`, `**`) perform mathematical operations. Key distinctions: `/` always returns a float; `//` returns an integer (floor division); `%` returns the remainder.

**Assignment operators** store values into variables. Compound operators like `+=` and `-=` update a variable in one clean step instead of two.

**Comparison operators** (`==`, `!=`, `>`, `<`, `>=`, `<=`) compare values and always return `True` or `False`. Never confuse `=` (store) with `==` (compare).

**Logical operators** (`and`, `or`, `not`) combine boolean conditions. `and` requires both to be True; `or` requires at least one to be True; `not` inverts the result.

**Identity operators** (`is`, `is not`) check whether two variables point to the same object in memory — not just whether they hold equal values. Use `is` primarily with `None`.

**Membership operators** (`in`, `not in`) check whether a value exists within a string, list, or other collection. They return `True` or `False`.

**Bitwise operators** (`&`, `|`, `^`, `~`, `<<`, `>>`) work directly on binary representations of integers. Used in systems programming, cryptography, and performance-critical applications.

**Operator precedence** determines the order in which Python evaluates a multi-operator expression. The order, from highest to lowest, is roughly: parentheses → exponent → unary → multiply/divide → add/subtract → shifts → bitwise → comparisons → `not` → `and` → `or`. Use parentheses whenever you want to be explicit or are unsure.

---

## Quick Reference Card

```python
# ── ARITHMETIC ──────────────────────────────────────────
10 + 4     # 14  — Addition
10 - 4     # 6   — Subtraction
10 * 4     # 40  — Multiplication
10 / 4     # 2.5 — Division (always float)
10 // 4    # 2   — Floor division (integer)
10 % 4     # 2   — Modulus (remainder)
2 ** 8     # 256 — Exponentiation

# ── ASSIGNMENT ──────────────────────────────────────────
x = 10     # Simple assignment
x += 5     # x = x + 5  → 15
x -= 3     # x = x - 3  → 12
x *= 2     # x = x * 2  → 24
x /= 4     # x = x / 4  → 6.0
x //= 2    # x = x // 2 → 3
x %= 2     # x = x % 2  → 1
x **= 3    # x = x ** 3 → 1

# ── COMPARISON ──────────────────────────────────────────
5 == 5     # True  — Equal to
5 != 3     # True  — Not equal to
5 > 3      # True  — Greater than
3 < 5      # True  — Less than
5 >= 5     # True  — Greater than or equal to
3 <= 5     # True  — Less than or equal to

# ── LOGICAL ─────────────────────────────────────────────
True and True      # True
True and False     # False
False or True      # True
False or False     # False
not True           # False
not False          # True

# ── IDENTITY ────────────────────────────────────────────
x is y             # True if x and y are the same object
x is not y         # True if different objects
result is None     # Common use: checking for None

# ── MEMBERSHIP ──────────────────────────────────────────
"a" in "Amaka"             # True
"z" not in "Lagos"         # True
"Kano" in ["Lagos", "Kano"] # True

# ── BITWISE ─────────────────────────────────────────────
5 & 3      # 1  — AND (both bits must be 1)
5 | 3      # 7  — OR (at least one bit is 1)
5 ^ 3      # 6  — XOR (bits must differ)
~5         # -6 — NOT (invert all bits)
5 << 1     # 10 — Left shift (× 2)
20 >> 1    # 10 — Right shift (÷ 2)

# ── PRECEDENCE (highest → lowest) ───────────────────────
# ()  →  **  →  unary  →  * / // %  →  + -
# →  << >>  →  &  →  ^  →  |
# →  == != > < >= <= is is not in not in
# →  not  →  and  →  or
```

---

*End of Lesson 10 — Python Operators*

*Next Lesson: Lesson 11 — Python Lists*
