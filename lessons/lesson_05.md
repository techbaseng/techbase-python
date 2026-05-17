---
render_with_liquid: false
title: "Lesson 05: Python String Methods, Operators, Arithmetic & Assignment Operators"
nav_order: 5
---

# Lesson 05: String Methods, Operators, Arithmetic & Assignment Operators

---

## Lesson Introduction

Welcome to Lesson 05! So far you have learned what strings are, how to create them, slice them, modify them, format them, and escape special characters inside them. In this lesson we close the chapter on strings by exploring the **full library of built-in string methods** Python gives you for free. You will then step into an entirely new territory — **operators** — the symbols Python uses to perform calculations, store results, and update values. By the end of this lesson you will be able to clean text, run arithmetic, and write update shorthand like a professional Python developer.

### What You Will Learn

By the end of this lesson you will be able to:

1. Identify and use the most important Python string methods.
2. Understand that string methods return new values and do NOT change the original string.
3. Explain what an operator is and name the seven groups Python provides.
4. Use all seven arithmetic operators to perform mathematical calculations.
5. Use assignment operators — including shorthand forms — to store and update variable values.
6. Combine string methods and operators in practical programs.

---

## Prerequisite Concepts

Before diving in, make sure you are comfortable with the following ideas from earlier lessons:

- **Variables:** A named container that stores a value (e.g., `market = "Lagos Island Market"`).
- **Strings:** Text enclosed in single or double quotes (e.g., `"Jollof rice is delicious"`).
- **print():** The function that displays output to the screen.
- **Data Types:** You know that `"hello"` is a string (`str`) and `10` is an integer (`int`).

If any of these feel unclear, revisit Lessons 02 to 04 before continuing.

---

## Part 1 — Python String Methods

### Section 1.1 — What Is a Method?

Imagine you have a brand-new Nokia phone fresh out of the box. The phone itself is the **object** — in Python terms, that is your string. The phone comes with buttons and features built in: you can call someone, take a photo, or send an SMS. Those built-in features are called **methods** in Python.

A **method** is a special function that is already built into an object. You call it by writing the object's name, then a dot `.`, then the method name, followed by parentheses `()`.

```
object.method()
```

For strings, a method is a tool you use **on** a piece of text to transform or examine it.

**One critical rule you must never forget:**

> **All string methods return a new value. They do NOT change the original string.**

This is unlike editing a document — it is more like making a photocopy and changing the copy. The original stays untouched.

---

### Section 1.2 — Case-Changing Methods

These methods change the capitalisation of text. They are incredibly useful when you receive user input that may be typed inconsistently — for example, someone types `"ABUJA"` or `"abuja"` when you want `"Abuja"`.

---

#### `upper()` — Convert Everything to UPPERCASE

**Why it exists:** Useful when you want to emphasise text, create headings, or standardise input for comparison.

**How it works:** Every letter in the string is converted to its capital form.

```python
city = "lagos"
print(city.upper())
```

**Expected output in the terminal:**

```
LAGOS
```

Notice that `city` still holds `"lagos"` — the original is untouched. Only the printed result changed.

---

#### `lower()` — Convert Everything to lowercase

**Why it exists:** Useful for normalising input. For example, when checking if an email address or username already exists, you want to compare everything in lowercase so `"Amaka@mail.com"` and `"amaka@mail.com"` are treated the same.

```python
email = "AMAKA@GMAIL.COM"
print(email.lower())
```

**Expected output:**

```
amaka@gmail.com
```

---

#### `capitalize()` — Capitalise ONLY the First Letter

**Why it exists:** Useful for proper names, titles, or the first word of a sentence when the input came in all-lowercase or mixed case.

**How it works:** The very first character of the entire string is made uppercase, and every other character is made lowercase.

```python
dish = "egusi soup"
print(dish.capitalize())
```

**Expected output:**

```
Egusi soup
```

> **Thinking Prompt:** What happens if the string is `"EGUSI SOUP"`? Try it mentally — capitalize() makes the first letter upper and ALL others lower. The result would still be `"Egusi soup"`.

---

#### `title()` — Capitalise the First Letter of Every Word

**Why it exists:** Perfect for formatting names, book titles, city names, or article headings.

**How it works:** The first character of **each word** is made uppercase.

```python
meal = "pounded yam and egusi soup"
print(meal.title())
```

**Expected output:**

```
Pounded Yam And Egusi Soup
```

---

#### `swapcase()` — Flip Every Letter's Case

**Why it exists:** Occasionally used for creative text effects or decoding puzzles.

**How it works:** Any uppercase letter becomes lowercase, and any lowercase letter becomes uppercase.

```python
greeting = "Good Morning Lagos"
print(greeting.swapcase())
```

**Expected output:**

```
gOOD mORNING lAGOS
```

---

#### `casefold()` — Aggressive Lowercase for Comparisons

**Why it exists:** `casefold()` goes even further than `lower()` when comparing strings across different languages and special characters. For everyday Python in English, it behaves the same as `lower()`, but it is the recommended method for text comparisons.

```python
name1 = "CHUKWUEMEKA"
name2 = "chukwuemeka"
print(name1.casefold() == name2.casefold())
```

**Expected output:**

```
True
```

---

### Section 1.3 — Searching Inside Strings

These methods let you look for something inside a string, similar to using Ctrl+F in a document editor.

---

#### `find()` — Find a Substring's Position

**Why it exists:** You need to know where a word or character appears inside a string — for example, scanning a customer complaint for the word "refund".

**How it works:** `find(substring)` searches the string from left to right. It returns the **index position** (position number) where the substring first appears. If it cannot find it, it returns **-1**.

> **Quick reminder:** Index positions in Python start at **0**, not 1. So the first character is at position 0, the second at position 1, and so on.

```python
message = "Please send the Ankara fabric to Kano"
position = message.find("Ankara")
print(position)
```

**Expected output:**

```
17
```

This means the word `"Ankara"` starts at position 17 in the string.

```python
# What if the word is not found?
print(message.find("Aso-Oke"))
```

**Expected output:**

```
-1
```

The value `-1` is Python's way of saying "not found."

---

#### `index()` — Like find(), but Raises an Error if Not Found

**Why it exists:** When you are absolutely certain a word should be there and want Python to crash loudly if it is not (so you notice the bug immediately).

```python
text = "Dangote is a major Nigerian business group"
print(text.index("Nigerian"))
```

**Expected output:**

```
23
```

If the word is not there, `index()` raises a `ValueError` error — unlike `find()` which quietly returns -1. For beginners, `find()` is usually safer.

---

#### `count()` — Count How Many Times a Substring Appears

**Why it exists:** Useful in data analysis — for example, counting how many times a customer said "broken" in a product review.

```python
review = "The suya was good. The pepper was good. The service was good."
print(review.count("good"))
```

**Expected output:**

```
3
```

---

#### `startswith()` — Does the String Begin with This?

**Why it exists:** Quickly check if a filename, URL, phone number, or code starts with the expected characters.

```python
phone = "0801-234-5678"
print(phone.startswith("0801"))
```

**Expected output:**

```
True
```

```python
print(phone.startswith("0902"))
```

**Expected output:**

```
False
```

---

#### `endswith()` — Does the String Finish with This?

**Why it exists:** Check file types, extensions, or suffixes. For example, check if a filename is a PDF.

```python
filename = "WAEC_Result_2024.pdf"
print(filename.endswith(".pdf"))
```

**Expected output:**

```
True
```

---

#### `rfind()` — Find the LAST Occurrence of a Substring

**Why it exists:** If a word appears multiple times, sometimes you want the position of the last one, not the first.

```python
sentence = "Eko is great. Lagos is great. Nigeria is great."
print(sentence.rfind("great"))
```

**Expected output:**

```
40
```

---

### Section 1.4 — Replacing and Splitting Text

---

#### `replace()` — Swap One Word for Another

**Why it exists:** Update text without rewriting the whole thing — like Find & Replace in Microsoft Word.

**How it works:** `replace(old, new)` takes two arguments: the text to find, and the text to replace it with.

```python
menu = "We serve Jollof rice with chicken"
updated_menu = menu.replace("chicken", "catfish")
print(updated_menu)
```

**Expected output:**

```
We serve Jollof rice with catfish
```

```python
# Replace ALL occurrences
prices = "Price: ₦500. Discount Price: ₦500. Bulk Price: ₦500."
print(prices.replace("₦500", "₦450"))
```

**Expected output:**

```
Price: ₦450. Discount Price: ₦450. Bulk Price: ₦450.
```

You can also limit how many replacements are made by providing a third argument:

```python
print(prices.replace("₦500", "₦450", 1))  # Replace only the first occurrence
```

**Expected output:**

```
Price: ₦450. Discount Price: ₦500. Bulk Price: ₦500.
```

---

#### `split()` — Break a String into a List of Pieces

**Why it exists:** When you receive a string of comma-separated values, or a sentence of words, and you need to process each part separately.

**How it works:** `split(separator)` cuts the string at every point where the separator occurs, and returns a **list** (a collection of items).

```python
states = "Lagos,Abuja,Kano,Rivers,Enugu"
state_list = states.split(",")
print(state_list)
```

**Expected output:**

```
['Lagos', 'Abuja', 'Kano', 'Rivers', 'Enugu']
```

Without a separator, `split()` splits on any whitespace (spaces, tabs):

```python
sentence = "My name is Tunde"
words = sentence.split()
print(words)
```

**Expected output:**

```
['My', 'name', 'is', 'Tunde']
```

---

#### `join()` — Join a List of Strings into One

**Why it exists:** The opposite of `split()`. It takes a list of words and glues them together with a separator.

**How it works:** You call `join()` **on the separator string** and pass it the list.

```python
words = ["Fried", "plantain", "is", "delicious"]
sentence = " ".join(words)  # Join using a space
print(sentence)
```

**Expected output:**

```
Fried plantain is delicious
```

```python
items = ["beans", "yam", "palm oil"]
shopping = ", ".join(items)
print(shopping)
```

**Expected output:**

```
beans, yam, palm oil
```

---

#### `splitlines()` — Split a Multi-Line String at Line Breaks

**Why it exists:** When you read a text file or multi-line message, you often want to handle each line separately.

```python
address = "No. 12 Adeola Odeku Street\nVictoria Island\nLagos"
lines = address.splitlines()
print(lines)
```

**Expected output:**

```
['No. 12 Adeola Odeku Street', 'Victoria Island', 'Lagos']
```

---

### Section 1.5 — Stripping Whitespace and Padding Text

**Whitespace** means invisible characters like spaces, tabs, or newlines that appear at the beginning or end of a string. They are often the culprit when user input doesn't match what you expect.

---

#### `strip()` — Remove Whitespace from BOTH Ends

```python
name = "   Funmilayo   "
print(name.strip())
```

**Expected output:**

```
Funmilayo
```

---

#### `lstrip()` — Remove Whitespace from the LEFT Only

```python
name = "   Funmilayo   "
print(name.lstrip())
```

**Expected output:**

```
Funmilayo   
```

---

#### `rstrip()` — Remove Whitespace from the RIGHT Only

```python
name = "   Funmilayo   "
print(name.rstrip())
```

**Expected output:**

```
   Funmilayo
```

> **Real-world use:** When users type their name into a form and accidentally add spaces, `strip()` cleans the input before your program uses it. This prevents bugs like `"Lagos" != " Lagos"`.

---

#### `center()`, `ljust()`, `rjust()` — Aligning Text with Padding

These methods position text within a fixed-width field, filling empty space with a character (default is a space).

```python
# center() — centre the text in a field of 30 characters
print("LAGBAJA MARKET".center(30))
print("LAGBAJA MARKET".center(30, "-"))
```

**Expected output:**

```
        LAGBAJA MARKET        
--------LAGBAJA MARKET--------
```

```python
# ljust() — left-align in a field of 30 characters
print("Beans".ljust(20, "."))
print("Jollof Rice".ljust(20, "."))
print("Pounded Yam".ljust(20, "."))
```

**Expected output:**

```
Beans...............
Jollof Rice.........
Pounded Yam.........
```

```python
# rjust() — right-align
print("₦1500".rjust(15))
print("₦200".rjust(15))
```

**Expected output:**

```
          ₦1500
           ₦200
```

---

#### `zfill()` — Pad a String on the Left with Zeros

**Why it exists:** Useful for formatting order numbers, student IDs, bank account numbers, or phone extension codes that must always have a fixed number of digits.

```python
order_id = "42"
print(order_id.zfill(6))   # Pad to 6 digits
```

**Expected output:**

```
000042
```

---

### Section 1.6 — Checking What a String Contains

These methods inspect a string and return either `True` or `False`. They are perfect for **validating input** — checking if what the user typed matches the expected format.

---

#### `isalpha()` — Are ALL Characters Letters?

```python
print("Ngozi".isalpha())      # True — only letters
print("Ngozi123".isalpha())   # False — has digits
print("Ngozi Obi".isalpha())  # False — has a space
```

**Expected output:**

```
True
False
False
```

---

#### `isdigit()` — Are ALL Characters Digits?

```python
print("12345".isdigit())    # True
print("123.45".isdigit())   # False — decimal point is not a digit
print("₦500".isdigit())     # False — currency symbol is not a digit
```

**Expected output:**

```
True
False
False
```

---

#### `isalnum()` — Are ALL Characters Letters OR Digits?

```python
print("Student123".isalnum())   # True
print("Student 123".isalnum())  # False — space is not allowed
```

**Expected output:**

```
True
False
```

---

#### `isnumeric()` — A Broader Check for Numeric Characters

Similar to `isdigit()` but also accepts characters like fractions and superscripts used in other writing systems.

---

#### `isspace()` — Is the String ONLY Whitespace?

```python
print("   ".isspace())    # True — only spaces
print("  a  ".isspace())  # False — contains a letter
```

**Expected output:**

```
True
False
```

---

#### `islower()` and `isupper()` — Check Letter Case

```python
print("hello".islower())   # True
print("HELLO".isupper())   # True
print("Hello".isupper())   # False
```

**Expected output:**

```
True
True
False
```

---

#### `istitle()` — Does It Follow Title Case Rules?

```python
print("The Lagos State Government".istitle())  # True
print("the lagos state government".istitle())  # False
```

**Expected output:**

```
True
False
```

---

### Section 1.7 — Encoding and Translating

#### `encode()` — Encode the String as Bytes

**Why it exists:** When you send data over a network or save it to a file, it is sometimes stored as raw bytes rather than human-readable text. This method converts the string into that byte format.

```python
text = "Abuja"
print(text.encode())
```

**Expected output:**

```
b'Abuja'
```

The `b` in front means "this is bytes, not a regular string."

---

#### `partition()` and `rpartition()` — Split a String into Exactly Three Parts

`partition(sep)` finds the **first** occurrence of a separator and returns a **tuple** (a fixed group) of three parts: the text before, the separator itself, and the text after.

```python
data = "Name: Emeka Eze"
result = data.partition(": ")
print(result)
```

**Expected output:**

```
('Name', ': ', 'Emeka Eze')
```

`rpartition()` does the same but from the right (last occurrence).

---

#### `format()` — Insert Values into a String Template

You have already used f-strings. The `format()` method does the same thing in a slightly older style using `{}` placeholders.

```python
template = "Hello, {}! You have {} new messages."
message = template.format("Chidinma", 5)
print(message)
```

**Expected output:**

```
Hello, Chidinma! You have 5 new messages.
```

---

#### `expandtabs()` — Control Tab Width

When strings contain tab characters (`\t`), this method sets how wide each tab should appear.

```python
text = "Name\tCity\tAge"
print(text.expandtabs(15))
```

**Expected output:**

```
Name           City           Age
```

---

#### `maketrans()` and `translate()` — Character Substitution Table

These two methods work together to create a character-by-character replacement map.

```python
# Replace 'a' → '4', 'e' → '3', 'o' → '0'
table = str.maketrans("aeo", "430")
text = "Suya and pepper soup"
print(text.translate(table))
```

**Expected output:**

```
Suy4 4nd p3pp3r s0up
```

---

### Section 1.8 — The Full String Methods Reference Table

Here is a complete reference of every built-in Python string method:

| Method | What It Does |
|---|---|
| `capitalize()` | Makes the first character uppercase; the rest lowercase |
| `casefold()` | Converts to lowercase (stronger than `lower()` for comparisons) |
| `center(width, char)` | Returns a centred string padded with `char` |
| `count(sub)` | Counts how many times `sub` appears |
| `encode(encoding)` | Returns an encoded version of the string as bytes |
| `endswith(suffix)` | Returns `True` if string ends with `suffix` |
| `expandtabs(tabsize)` | Sets tab size and expands tab characters |
| `find(sub)` | Returns the position of first occurrence, or -1 |
| `format(*args)` | Inserts values into placeholders `{}` |
| `format_map(mapping)` | Like `format()` but uses a dictionary |
| `index(sub)` | Like `find()` but raises an error if not found |
| `isalnum()` | `True` if all characters are letters or digits |
| `isalpha()` | `True` if all characters are letters |
| `isascii()` | `True` if all characters are ASCII |
| `isdecimal()` | `True` if all characters are decimal digits |
| `isdigit()` | `True` if all characters are digits |
| `isidentifier()` | `True` if the string is a valid Python identifier |
| `islower()` | `True` if all letters are lowercase |
| `isnumeric()` | `True` if all characters are numeric |
| `isprintable()` | `True` if all characters are printable |
| `isspace()` | `True` if all characters are whitespace |
| `istitle()` | `True` if string follows title case rules |
| `isupper()` | `True` if all letters are uppercase |
| `join(iterable)` | Joins items in an iterable with the string as separator |
| `ljust(width, char)` | Left-aligns string padded with `char` |
| `lower()` | Converts all letters to lowercase |
| `lstrip(chars)` | Removes leading characters (default: whitespace) |
| `maketrans(x, y, z)` | Creates a translation mapping |
| `partition(sep)` | Splits into 3 parts at the first `sep` |
| `replace(old, new)` | Replaces all occurrences of `old` with `new` |
| `rfind(sub)` | Finds the last occurrence of `sub`, or -1 |
| `rindex(sub)` | Like `rfind()` but raises an error if not found |
| `rjust(width, char)` | Right-aligns string padded with `char` |
| `rpartition(sep)` | Splits into 3 parts at the last `sep` |
| `rsplit(sep)` | Splits at `sep`, scanning from the right |
| `rstrip(chars)` | Removes trailing characters (default: whitespace) |
| `split(sep)` | Splits string into a list at each `sep` |
| `splitlines()` | Splits at line breaks and returns a list |
| `startswith(prefix)` | Returns `True` if string starts with `prefix` |
| `strip(chars)` | Removes leading and trailing characters |
| `swapcase()` | Flips uppercase to lowercase and vice versa |
| `title()` | Makes the first letter of each word uppercase |
| `translate(table)` | Translates characters using a mapping table |
| `upper()` | Converts all letters to uppercase |
| `zfill(width)` | Pads string with leading zeros to fill `width` |

---

## Part 2 — Python Operators

### Section 2.1 — What Is an Operator?

An **operator** is a symbol that tells Python to perform a specific action on one or more values. You already know the most famous one: `+`. When you write `5 + 3`, the `+` is the operator, and `5` and `3` are the **operands** (the values being operated on).

Think of operators like the buttons on your calculator. Each button tells the calculator what to do with the numbers you have entered.

```python
print(10 + 5)    # The + operator adds two numbers
```

**Expected output:**

```
15
```

Operators can also work with variables:

```python
naira_price = 100
vat = 50
total = naira_price + vat    # 100 + 50
print(total)
```

**Expected output:**

```
150
```

And variables can be combined with each other:

```python
cost_price = 5000
markup    = cost_price + 1000   # 6000
selling_price = markup + markup  # 12000
print(selling_price)
```

**Expected output:**

```
12000
```

---

### Section 2.2 — The Seven Groups of Python Operators

Python organises its operators into seven groups based on what they do:

1. **Arithmetic Operators** — do maths (`+`, `-`, `*`, `/`, etc.)
2. **Assignment Operators** — store values in variables (`=`, `+=`, etc.)
3. **Comparison Operators** — compare two values and return True or False (`==`, `>`, `<`, etc.)
4. **Logical Operators** — combine conditions (`and`, `or`, `not`)
5. **Identity Operators** — check if two variables point to the same object (`is`, `is not`)
6. **Membership Operators** — check if a value exists in a sequence (`in`, `not in`)
7. **Bitwise Operators** — work on binary representations of numbers (`&`, `|`, `^`, etc.)

In this lesson we cover Groups 1 and 2 in full depth. The other groups will be taught as they become relevant.

---

## Part 3 — Arithmetic Operators

### Section 3.1 — What Are Arithmetic Operators?

**Arithmetic operators** are used with **numeric values** to perform common mathematical operations — the same operations you learned in primary school. Python supports seven of them.

Here is the complete table:

| Operator | Name | Example |
|---|---|---|
| `+` | Addition | `x + y` |
| `-` | Subtraction | `x - y` |
| `*` | Multiplication | `x * y` |
| `/` | Division | `x / y` |
| `%` | Modulus (remainder) | `x % y` |
| `**` | Exponentiation (power) | `x ** y` |
| `//` | Floor Division (round down) | `x // y` |

Let us learn each one carefully.

---

### Section 3.2 — Addition `+`

**What it does:** Adds two numbers together.

```python
bags_of_rice = 20
bags_donated = 5
total_bags = bags_of_rice + bags_donated
print(total_bags)
```

**Expected output:**

```
25
```

The `+` operator also works on strings (it **concatenates** them — joins them together):

```python
first_name = "Amina"
last_name = " Bello"
full_name = first_name + last_name
print(full_name)
```

**Expected output:**

```
Amina Bello
```

---

### Section 3.3 — Subtraction `-`

**What it does:** Subtracts the second number from the first.

```python
budget = 50000      # ₦50,000 market budget
spent = 23500       # ₦23,500 spent
remaining = budget - spent
print(remaining)
```

**Expected output:**

```
26500
```

---

### Section 3.4 — Multiplication `*`

**What it does:** Multiplies two numbers.

```python
price_per_sachet = 50    # ₦50 per sachet of pure water
sachets_sold = 200
total_revenue = price_per_sachet * sachets_sold
print(total_revenue)
```

**Expected output:**

```
10000
```

The `*` operator also works on strings — it repeats them:

```python
print("Ha" * 3)
```

**Expected output:**

```
HaHaHa
```

---

### Section 3.5 — Division `/`

**What it does:** Divides the first number by the second.

> **Important:** Division in Python **always returns a float** (a decimal number), even if the result is a whole number.

```python
total_akara = 30
people = 6
each_person_gets = total_akara / people
print(each_person_gets)
```

**Expected output:**

```
5.0
```

Notice the `.0` at the end — that is the float. Even though 30 ÷ 6 = 5 exactly, Python still gives you `5.0`.

```python
# Another example showing float result
print(12 / 5)
```

**Expected output:**

```
2.4
```

---

### Section 3.6 — Modulus `%`

**What it does:** Returns the **remainder** left over after division. This is sometimes called the "modulo" operator.

Think back to primary school long division. When you divide 17 by 5, you get 3 with a remainder of 2. The modulus operator gives you that **remainder — which is 2**.

```python
print(17 % 5)
```

**Expected output:**

```
2
```

**Real-world examples:**

```python
# Sharing yam portions: 25 tubers among 4 families
tubers = 25
families = 4
leftover = tubers % families
print("Leftover tubers:", leftover)
```

**Expected output:**

```
Leftover tubers: 1
```

```python
# Checking if a number is even (remainder when divided by 2 is 0)
number = 46
print(number % 2)    # Even numbers have remainder 0
```

**Expected output:**

```
0
```

```python
number = 47
print(number % 2)    # Odd numbers have remainder 1
```

**Expected output:**

```
1
```

This is one of the most useful tricks in programming — checking whether a number is even or odd by seeing if `number % 2` equals 0.

---

### Section 3.7 — Exponentiation `**`

**What it does:** Raises a number to a power. In mathematics, this is written as x^y (x to the power of y).

```python
# 2 to the power of 10
print(2 ** 10)
```

**Expected output:**

```
1024
```

```python
# Area of a square plot of land with side 15 metres
side = 15
area = side ** 2    # Side squared
print("Area:", area, "square metres")
```

**Expected output:**

```
Area: 225 square metres
```

```python
# Volume of a cube
side = 4
volume = side ** 3
print("Volume:", volume, "cubic metres")
```

**Expected output:**

```
Volume: 64 cubic metres
```

---

### Section 3.8 — Floor Division `//`

**What it does:** Divides and then **rounds DOWN** to the nearest whole number (integer). This is also called "integer division."

**Why it exists:** Sometimes you need a whole-number result, not a decimal. For example, if you are distributing items, you cannot give someone half a loaf of bread.

```python
# Regular division — gives a float
print(12 / 5)
```

**Expected output:**

```
2.4
```

```python
# Floor division — rounds DOWN to an integer
print(12 // 5)
```

**Expected output:**

```
2
```

Notice that `12 // 5` gives **2**, not 3 — it always rounds **down**, never up.

```python
# Sharing kola nuts: 25 nuts among 4 people
total_kola = 25
guests = 4
per_person = total_kola // guests   # How many each person gets (whole number)
leftover = total_kola % guests      # How many are left over
print("Each person gets:", per_person)
print("Left over:", leftover)
```

**Expected output:**

```
Each person gets: 6
Left over: 1
```

> **Thinking Prompt:** What is the relationship between `//` and `%`? If `25 // 4 = 6`, and `6 * 4 = 24`, then `25 - 24 = 1`, which is exactly what `25 % 4` gives us. Floor division and modulus are two sides of the same coin!

---

### Section 3.9 — Using All Arithmetic Operators Together

```python
x = 15
y = 4

print("Addition:       ", x + y)    # 15 + 4
print("Subtraction:    ", x - y)    # 15 - 4
print("Multiplication: ", x * y)    # 15 × 4
print("Division:       ", x / y)    # 15 ÷ 4
print("Modulus:        ", x % y)    # Remainder of 15 ÷ 4
print("Exponentiation: ", x ** y)   # 15 to the power of 4
print("Floor Division: ", x // y)   # 15 ÷ 4 rounded down
```

**Expected output:**

```
Addition:        19
Subtraction:     11
Multiplication:  60
Division:        3.75
Modulus:         3
Exponentiation:  50625
Floor Division:  3
```

---

## Part 4 — Assignment Operators

### Section 4.1 — What Is an Assignment Operator?

You have been using the basic assignment operator since Lesson 02:

```python
city = "Abuja"
```

That `=` is the **assignment operator**. It takes the value on the right side and stores it into the variable on the left side.

But Python also gives you **shorthand assignment operators** that combine arithmetic with assignment. These save you from writing the variable name twice when updating its value.

**The problem they solve:**

Imagine you have ₦500 in a variable and you want to add ₦200 to it. The long way is:

```python
balance = 500
balance = balance + 200   # Take the old value, add 200, store it back
print(balance)
```

**Expected output:**

```
700
```

That works, but you have to write `balance` twice. The shorthand operator `+=` does the same thing more cleanly:

```python
balance = 500
balance += 200    # Same as: balance = balance + 200
print(balance)
```

**Expected output:**

```
700
```

---

### Section 4.2 — The Complete Assignment Operators Table

Here is every assignment operator Python provides:

| Operator | Example | Equivalent To | Meaning |
|---|---|---|---|
| `=` | `x = 5` | `x = 5` | Assign the value 5 to x |
| `+=` | `x += 3` | `x = x + 3` | Add 3 to x and store the result back |
| `-=` | `x -= 3` | `x = x - 3` | Subtract 3 from x and store back |
| `*=` | `x *= 3` | `x = x * 3` | Multiply x by 3 and store back |
| `/=` | `x /= 3` | `x = x / 3` | Divide x by 3 and store back (gives float) |
| `%=` | `x %= 3` | `x = x % 3` | Get remainder of x ÷ 3 and store back |
| `//=` | `x //= 3` | `x = x // 3` | Floor-divide x by 3 and store back |
| `**=` | `x **= 3` | `x = x ** 3` | Raise x to the power 3 and store back |
| `&=` | `x &= 3` | `x = x & 3` | Bitwise AND (advanced — covered later) |
| `\|=` | `x \|= 3` | `x = x \| 3` | Bitwise OR (advanced — covered later) |
| `^=` | `x ^= 3` | `x = x ^ 3` | Bitwise XOR (advanced — covered later) |
| `>>=` | `x >>= 3` | `x = x >> 3` | Bitwise right shift (advanced) |
| `<<=` | `x <<= 3` | `x = x << 3` | Bitwise left shift (advanced) |
| `:=` | `x := 5` | (see below) | Walrus operator — assigns AND evaluates |

The bitwise operators (`&=`, `|=`, `^=`, `>>=`, `<<=`) work on the binary representation of numbers and are used in advanced topics. For now, master the first eight.

---

### Section 4.3 — Each Assignment Operator with Examples

Let us go through each of the main ones with a practical Nigerian example.

---

#### `=` — Basic Assignment

```python
kola_nuts = 30   # Assign 30 to kola_nuts
print(kola_nuts)
```

**Expected output:**

```
30
```

---

#### `+=` — Add and Assign

You receive more kola nuts in the market:

```python
kola_nuts = 30
kola_nuts += 12   # Someone brings 12 more
print(kola_nuts)
```

**Expected output:**

```
42
```

`+=` also works on strings — it appends (adds to the end):

```python
greeting = "Good"
greeting += " morning"
greeting += ", Sade!"
print(greeting)
```

**Expected output:**

```
Good morning, Sade!
```

---

#### `-=` — Subtract and Assign

Customers buy some items:

```python
stock = 100          # 100 bags of garri in the store
stock -= 35          # 35 bags sold today
print(stock)
```

**Expected output:**

```
65
```

---

#### `*=` — Multiply and Assign

Price doubles due to market inflation:

```python
price = 800      # ₦800 per kg of beef
price *= 2       # Price doubles
print(price)
```

**Expected output:**

```
1600
```

---

#### `/=` — Divide and Assign

Splitting a pot of money among partners:

```python
partnership_profit = 900000   # ₦900,000 total profit
partnership_profit /= 3       # Split equally among 3 partners
print(partnership_profit)
```

**Expected output:**

```
300000.0
```

Note the `.0` because `/=` always produces a float.

---

#### `%=` — Modulus and Assign

Check what is left after packing into complete groups:

```python
akara_count = 47
akara_count %= 10    # How many remain after packing into groups of 10?
print(akara_count)   # 47 = 4 groups of 10, plus 7 remaining
```

**Expected output:**

```
7
```

---

#### `//=` — Floor Divide and Assign

How many complete cartons can be filled?

```python
bottles = 250
bottles //= 12        # 12 bottles per carton
print(bottles)        # 250 ÷ 12 = 20 complete cartons (with 10 left over)
```

**Expected output:**

```
20
```

---

#### `**=` — Exponentiate and Assign

Investment grows (this is a simplified model):

```python
investment = 10000    # ₦10,000 invested
investment **= 2      # Just for illustration
print(investment)
```

**Expected output:**

```
100000000
```

---

### Section 4.4 — The Walrus Operator `:=`

Python 3.8 introduced the **walrus operator** `:=`. Its nickname comes from the fact that `:=` looks a little like a walrus — two eyes (`:`) and a pair of tusks (`=`).

**What it does:** It assigns a value to a variable **and** uses that value in the same expression — all in one step. Previously, you needed two separate lines.

**The old way (two lines):**

```python
numbers = [1, 2, 3, 4, 5]
count = len(numbers)          # Line 1: count how many
if count > 3:                 # Line 2: check the count
    print(f"List has {count} elements")
```

**The walrus way (one step):**

```python
numbers = [1, 2, 3, 4, 5]
if (count := len(numbers)) > 3:    # Assign AND check in one go
    print(f"List has {count} elements")
```

**Expected output (both examples):**

```
List has 5 elements
```

> **Note for beginners:** The walrus operator is an advanced feature. You do not need to use it right away. Understand what it does, and you will encounter it when reading other people's code.

---

## Part 5 — Guided Practice Exercises

### Exercise 1 — Cleaning Market Data

**Scenario:** You work at Balogun Market's record office. Customer names arrive in the database with inconsistent capitalisation and stray spaces. Write code to clean and format each entry.

**Step 1 — Warm-up:**

```python
raw_name = "  okonkwo Chukwuemeka  "
print(raw_name.strip())
```

**Expected output:**

```
okonkwo Chukwuemeka
```

**Step 2 — Full exercise:**

```python
# Raw data from the form
raw_name  = "  amaka OKAFOR  "
raw_email = "  AMAKA.OKAFOR@GMAIL.COM  "
raw_city  = "lagos island"

# Clean and format
clean_name  = raw_name.strip().title()
clean_email = raw_email.strip().lower()
clean_city  = raw_city.strip().title()

print("Name:", clean_name)
print("Email:", clean_email)
print("City:", clean_city)
```

**Expected output:**

```
Name: Amaka Okafor
Email: amaka.okafor@gmail.com
City: Lagos Island
```

**Self-check questions:**
- Why did we call `.strip()` before `.title()`?
- What would happen if we swapped the order?
- What does `.lower()` return for an already-lowercase string?

---

### Exercise 2 — Supermarket Receipt Calculator

**Scenario:** You are building a simple receipt calculator for a supermarket in Abuja.

**Objective:** Calculate the subtotal, apply a 10% discount, add 7.5% VAT, and display a formatted receipt.

```python
# Product prices
jollof_rice_price  = 3500
grilled_chicken    = 2500
soft_drink         = 500
bottled_water      = 200

# Step 1: Calculate subtotal using +
subtotal = jollof_rice_price + grilled_chicken + soft_drink + bottled_water
print("Subtotal: ₦" + str(subtotal))

# Step 2: Apply 10% discount using *
discount_rate  = 0.10
discount_amount = subtotal * discount_rate
discounted_total = subtotal - discount_amount
print("Discount (10%): -₦" + str(discount_amount))
print("After Discount: ₦" + str(discounted_total))

# Step 3: Add 7.5% VAT
vat_rate    = 0.075
vat_amount  = discounted_total * vat_rate
final_total = discounted_total + vat_amount
print("VAT (7.5%): +₦" + str(vat_amount))
print("TOTAL:      ₦" + str(final_total))
```

**Expected output:**

```
Subtotal: ₦6700
Discount (10%): -₦670.0
After Discount: ₦6030.0
VAT (7.5%): +₦452.25
TOTAL:      ₦6482.25
```

**Self-check questions:**
- Why did we use `str(subtotal)` inside the print with `+`?
- What would the total be if the discount rate were 15% instead?

---

### Exercise 3 — Student Score Accumulator

**Scenario:** A teacher at a school in Enugu wants to add up student test scores as she marks them. She starts with 0 and uses `+=` to add each score.

```python
teacher_total = 0    # Start at 0

# Student scores come in one by one
teacher_total += 78   # Adaeze's score
teacher_total += 91   # Emeka's score
teacher_total += 65   # Bello's score
teacher_total += 88   # Ngozi's score
teacher_total += 72   # Yusuf's score

number_of_students = 5
average = teacher_total / number_of_students

print("Total score:", teacher_total)
print("Number of students:", number_of_students)
print("Class average:", average)
```

**Expected output:**

```
Total score: 394
Number of students: 5
Class average: 78.8
```

**Optional challenge:** Change two scores and recalculate. Does the average change as expected?

---

## Part 6 — Code Challenges

### Challenge 1

What is the output of the following code?

```python
text = "  Nigerian Naira  "
print(text.strip().upper().replace("NAIRA", "₦"))
```

**Answer:**

```
NIGERIAN ₦
```

**Explanation:** `strip()` removes the spaces, `upper()` capitalises everything, and `replace()` swaps the word "NAIRA" with the currency symbol.

---

### Challenge 2

What is the output?

```python
x = 17
x %= 5
x += 1
print(x)
```

**Answer:**

```
3
```

**Explanation:** `17 % 5 = 2` (remainder), then `2 + 1 = 3`.

---

### Challenge 3

Fill in the blank so the output is `"Akara"`:

```python
foods = "akara,puff-puff,boli,moimoi"
first_item = foods.split(",")[_]
print(first_item.capitalize())
```

**Answer:** Replace `_` with `0` (the first item in the list is at index 0).

---

### Challenge 4

Write a single line of code that converts `"welcome to lagos"` to `"WELCOME TO LAGOS"`.

**Answer:**

```python
print("welcome to lagos".upper())
```

---

## Part 7 — Mini Project: Market Sales Summary Tool

Build a simple sales reporting tool for a market trader in Lagos.

---

### Stage 1 — Setup: Define Products and Prices

```python
# --- MARKET SALES SUMMARY TOOL ---
# Trader: Mama Tola's Provisions Store, Oshodi Market

trader_name = "mama tola"
store_name  = "mama tola's provisions"

# Format the names properly
trader_name = trader_name.title()
store_name  = store_name.title()

print("=".center(40, "="))
print(store_name.center(40))
print("Oshodi Market, Lagos".center(40))
print("=".center(40, "="))
```

**Milestone 1 output:**

```
========================================
      Mama Tola'S Provisions      
          Oshodi Market, Lagos         
========================================
```

---

### Stage 2 — Core Logic: Record Sales

```python
# Daily sales
total_sales = 0

# Morning sales
total_sales += 4500   # Semo flour
total_sales += 1200   # Maggi cubes
total_sales += 800    # Palm oil (small)
total_sales += 3000   # Rice (small bag)

print("Morning sales total: ₦" + str(total_sales))

# Afternoon sales
total_sales += 2500   # Beans
total_sales += 600    # Salt and seasoning

print("Afternoon sales total: ₦" + str(total_sales))
```

**Milestone 2 output:**

```
Morning sales total: ₦9500
Afternoon sales total: ₦12600
```

---

### Stage 3 — Enhancement: Apply Calculations

```python
# Cost of goods (60% of revenue)
cost_of_goods  = total_sales * 0.60
gross_profit   = total_sales - cost_of_goods

# Market dues and transport (flat fee)
expenses = 1500
net_profit = gross_profit - expenses

print("\n--- DAILY SUMMARY ---")
print("Total Revenue:   ₦" + str(total_sales))
print("Cost of Goods:   ₦" + str(cost_of_goods))
print("Gross Profit:    ₦" + str(gross_profit))
print("Expenses:        ₦" + str(expenses))
print("Net Profit:      ₦" + str(net_profit))
```

**Milestone 3 output:**

```
--- DAILY SUMMARY ---
Total Revenue:   ₦12600
Cost of Goods:   ₦7560.0
Gross Profit:    ₦5040.0
Expenses:        ₦1500
Net Profit:      ₦3540.0
```

---

### Stage 4 — Final Output: Formatted Report

```python
print()
print("=".center(40, "="))
print("REPORT FOR: " + trader_name)
days_worked   = 26
monthly_estimate = net_profit * days_worked
print("Daily Net Profit:    ₦" + str(net_profit))
print("Estimated Monthly:   ₦" + str(monthly_estimate))
print("Report ends.".rjust(40))
print("=".center(40, "="))
```

**Milestone 4 output:**

```
========================================
REPORT FOR: Mama Tola
Daily Net Profit:    ₦3540.0
Estimated Monthly:   ₦92040.0
                     Report ends.
========================================
```

**Reflection questions:**
- What would happen to the monthly estimate if `days_worked` changed to 22?
- How would you add a 5% savings goal on the net profit?
- What string method would help you format ₦92040.0 as `"92,040.00"`?

**Optional advanced extension:** Research Python's `format()` function with `,.2f` to display currency with comma separators and two decimal places.

---

## Common Beginner Mistakes

### Mistake 1 — Thinking string methods change the original

**Wrong assumption:**

```python
name = "emeka"
name.upper()          # This does NOT change name
print(name)           # Still prints "emeka"
```

**Correct approach:**

```python
name = "emeka"
name = name.upper()   # Reassign the result back to name
print(name)           # Now prints "EMEKA"
```

---

### Mistake 2 — Confusing `=` and `==`

`=` means **assign** (store a value). `==` means **compare** (check if two things are equal).

**Wrong:**

```python
# This tries to ASSIGN inside a condition — causes an error in most contexts
if score = 90:
    print("Excellent")
```

**Correct:**

```python
score = 90            # Assign with =
if score == 90:       # Compare with ==
    print("Excellent")
```

---

### Mistake 3 — Using `/` when you want a whole number

```python
apples = 10
people = 3
each_gets = apples / people   # Returns 3.3333...
print(each_gets)
```

**Output:**

```
3.3333333333333335
```

If you want whole-number division, use `//`:

```python
each_gets = apples // people   # Returns 3
print(each_gets)
```

**Output:**

```
3
```

---

### Mistake 4 — Forgetting that `find()` returns -1, not False

```python
sentence = "I love suya"
result = sentence.find("pizza")

# Beginner mistake: testing result as True/False
if result:
    print("Found!")
else:
    print("Not found")
```

**Output (incorrect logic):**

```
Not found
```

This accidentally works for -1 because `-1` is "truthy" in Python, but `0` is "falsy". If the word appears at position 0, `result` would be `0`, and the `if` block would incorrectly skip! Always compare explicitly:

```python
if result != -1:
    print("Found!")
else:
    print("Not found")
```

---

### Mistake 5 — Confusing `*` and `**`

```python
print(3 * 3)    # 9 — multiplication: 3 × 3
print(3 ** 3)   # 27 — exponentiation: 3³ (3 to the power of 3)
```

One star = multiply. Two stars = power.

---

### Mistake 6 — Expecting `+=` to work before the variable is defined

```python
# This causes an error: NameError
total += 500    # Python doesn't know what total was before
```

**Correct:**

```python
total = 0       # Define the variable first
total += 500    # Now it works
```

---

## Reflection Questions

Take a moment to think about these before moving on:

1. What is the difference between `lower()` and `casefold()`? When would you prefer one over the other?
2. If `split()` breaks a string into a list, what method does the opposite?
3. Why does division (`/`) in Python always return a float, even when the result is a whole number?
4. If `x = 10` and you write `x **= 3`, what is the new value of `x`?
5. What does the walrus operator `:=` allow you to do in one line that would normally take two lines?
6. You have the string `" 0815-234-5678 "`. Which methods would you combine to clean it and check if it starts with `"0815"`?

---

## Completion Checklist

Before moving to Lesson 06, confirm you can answer "yes" to every item below:

- [ ] I understand that string methods return new values and do not change the original string.
- [ ] I can use `upper()`, `lower()`, `capitalize()`, `title()`, and `swapcase()` correctly.
- [ ] I can use `find()`, `count()`, `startswith()`, and `endswith()` to search inside strings.
- [ ] I can use `replace()`, `split()`, and `join()` to manipulate string content.
- [ ] I can use `strip()`, `lstrip()`, and `rstrip()` to remove whitespace.
- [ ] I can use `center()`, `ljust()`, `rjust()`, and `zfill()` to pad and align text.
- [ ] I can use `isalpha()`, `isdigit()`, `isalnum()`, `islower()`, `isupper()`, and `isspace()` to validate input.
- [ ] I understand what an operator is and can name the seven groups Python uses.
- [ ] I can apply all seven arithmetic operators: `+`, `-`, `*`, `/`, `%`, `**`, `//`.
- [ ] I understand the difference between `/` (float division) and `//` (floor division).
- [ ] I understand what `%` (modulus) does and why it is useful.
- [ ] I can use all common assignment operators: `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `//=`, `**=`.
- [ ] I know what the walrus operator `:=` does, even if I don't use it yet.

---

## Lesson Summary

In this lesson you covered two major topics that power almost every Python program:

**String Methods:**
Python provides a rich built-in library of string methods — over 45 in total. They fall into clear groups: case-changing (`.upper()`, `.lower()`, `.title()`), searching (`.find()`, `.count()`, `.startswith()`), transforming (`.replace()`, `.split()`, `.join()`), stripping whitespace (`.strip()`), padding and aligning (`.center()`, `.zfill()`), and validating content (`.isalpha()`, `.isdigit()`). All of them return a **new** value and leave the original string unchanged.

**Operators:**
Python divides its operators into seven groups. This lesson focused on the two most immediately useful: **Arithmetic operators** perform maths (`+`, `-`, `*`, `/`, `%`, `**`, `//`), and **Assignment operators** store values in variables (`=`) plus shorthand forms that combine arithmetic and storage in one step (`+=`, `-=`, etc.). The walrus operator `:=` is a modern addition that assigns and evaluates in a single expression.

---

## Quick-Reference Card

```
STRING METHODS — CASE
  .upper()        → "abuja" → "ABUJA"
  .lower()        → "ABUJA" → "abuja"
  .capitalize()   → "abuja" → "Abuja"
  .title()        → "abuja state" → "Abuja State"
  .swapcase()     → "Abuja" → "aBUJA"
  .casefold()     → "NAIRA" → "naira" (best for comparisons)

STRING METHODS — SEARCH
  .find("x")      → position of first "x", or -1
  .index("x")     → position of first "x", raises error if missing
  .rfind("x")     → position of LAST "x"
  .count("x")     → number of times "x" appears
  .startswith("x")→ True / False
  .endswith("x")  → True / False

STRING METHODS — TRANSFORM
  .replace("a","b")→ swap all "a" with "b"
  .split(",")      → break into list at ","
  .join(list)      → glue list items together
  .strip()         → remove whitespace both ends
  .lstrip()        → remove whitespace left only
  .rstrip()        → remove whitespace right only

STRING METHODS — PAD & ALIGN
  .center(n, c)    → centre in n-wide field, fill with c
  .ljust(n, c)     → left-align in n-wide field
  .rjust(n, c)     → right-align in n-wide field
  .zfill(n)        → pad left with zeros to width n

STRING METHODS — VALIDATE
  .isalpha()       → only letters?
  .isdigit()       → only digits?
  .isalnum()       → only letters or digits?
  .isspace()       → only whitespace?
  .islower()       → all lowercase letters?
  .isupper()       → all uppercase letters?
  .istitle()       → title case?

ARITHMETIC OPERATORS
  +   Addition        5 + 3 = 8
  -   Subtraction     5 - 3 = 2
  *   Multiplication  5 * 3 = 15
  /   Division        5 / 2 = 2.5  (always float)
  %   Modulus         5 % 2 = 1    (remainder)
  **  Exponentiation  5 ** 2 = 25  (power)
  //  Floor Division  5 // 2 = 2   (round down)

ASSIGNMENT OPERATORS
  =    x = 5        Assign
  +=   x += 3       x = x + 3
  -=   x -= 3       x = x - 3
  *=   x *= 3       x = x * 3
  /=   x /= 3       x = x / 3
  %=   x %= 3       x = x % 3
  //=  x //= 3      x = x // 3
  **=  x **= 3      x = x ** 3
  :=   (x := 5)     Assign AND use in one expression (walrus)
```
