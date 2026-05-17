---
render_with_liquid: false
title: "Lesson 04 – Python Strings: From Basics to Formatting Mastery"
nav_order: 4
---

# Lesson 04 – Python Strings: From Basics to Formatting Mastery

---

## Lesson Introduction

In nearly every program ever written, text plays a central role. Programs greet users by name, display error messages, format reports, read files, send emails, and present results — all using **text**. In Python, text is stored and handled using a data type called a **string**.

This lesson takes you from the very ground floor — _what a string even is_ — all the way through slicing, modifying, joining, formatting, and using special characters inside strings. By the end, you will have a complete, confident understanding of one of the most important tools in all of Python programming.

**What you will learn in this lesson:**

- What strings are and how to create them
- How to access individual characters and ranges of characters (slicing)
- How to modify string content using built-in Python methods
- How to join strings together (concatenation)
- How to build clean, dynamic text using string formatting
- How to include special characters like tabs, newlines, and quotes inside strings

---

## Prerequisite Concepts

> **Before you begin**, this lesson assumes you have completed Lessons 01–03. You should be comfortable with:
> - Running Python code in a script or interpreter
> - What a **variable** is and how to assign values with `=`
> - What **print()** does
> - Basic Python data types: integers (`int`) and floats (`float`)

If any of these feel unfamiliar, briefly review the earlier lessons before continuing. Every concept in this lesson builds on them.

---

## Part 1 – What Is a String?

### 1.1 Understanding Strings in Everyday Terms

Think of a string like a **necklace made of letter-beads**. Each bead is one character — a letter, a number, a space, a punctuation mark, or even an emoji. String them all together and you get a piece of text.

In Python, a **string** is a sequence of characters enclosed in quotation marks.

**Why does Python need a special type for text?**  
Numbers can be added, subtracted, and multiplied mathematically. But text works differently — you cannot multiply "hello" by 3 in a mathematical sense (though Python does have a fun trick for that, which you'll see shortly). Python uses a dedicated string type so it knows to treat that data as text, not as arithmetic.

---

### 1.2 Creating a String

You create a string by surrounding characters with:

- **Single quotes:** `'hello'`
- **Double quotes:** `"hello"`
- **Triple quotes:** `"""hello"""` or `'''hello'''` (for multi-line text)

Both single and double quotes produce identical strings. Triple quotes are used when your text needs to span multiple lines.

**Simple Example 1 – Your first string:**

```python
greeting = "Hello, World!"
print(greeting)
```

**Expected Output:**
```
Hello, World!
```

**Line-by-line explanation:**
- `greeting` — a variable name we chose to hold our text
- `=` — the assignment operator; stores the value on the right into the variable on the left
- `"Hello, World!"` — the string value; the double quotes tell Python "this is text, not code"
- `print(greeting)` — displays the value stored in `greeting` to the screen

---

**Simple Example 2 – Single quotes work too:**

```python
name = 'Alice'
print(name)
```

**Expected Output:**
```
Alice
```

> **Tip:** Single and double quotes are interchangeable for single-line strings. Most Python programmers pick one style and stay consistent. This lesson uses double quotes as the default.

---

**Simple Example 3 – Multi-line string with triple quotes:**

```python
address = """123 Maple Street
Springfield
USA"""
print(address)
```

**Expected Output:**
```
123 Maple Street
Springfield
USA
```

**Why triple quotes?** When your text naturally contains line breaks — like an address, a poem, or a block of instructions — triple quotes let you write exactly that without any extra tricks. Python preserves every line break you type.

---

### 1.3 Strings Are Sequences — Characters Have Positions

Here is a crucial idea: **every character in a string has a numbered position called an index**. Python starts counting at **zero**, not one.

Consider the string `"Python"`:

| Character | P | y | t | h | o | n |
|-----------|---|---|---|---|---|---|
| Index     | 0 | 1 | 2 | 3 | 4 | 5 |

You access a single character using **square brackets** with the index number inside.

**Example – Accessing individual characters:**

```python
word = "Python"
print(word[0])   # first character
print(word[1])   # second character
print(word[5])   # last character
```

**Expected Output:**
```
P
y
n
```

> **Common Beginner Mistake:** Trying `word[6]` on a 6-character string causes an **IndexError** because valid indexes are 0 through 5. There is no position 6.

```python
word = "Python"
print(word[6])  # ❌ IndexError: string index out of range
```

**Fix:** Always remember — for a string of length `n`, the valid indexes are `0` to `n-1`.

---

### 1.4 Negative Indexing — Counting from the End

Python also allows **negative indexes**. Think of it as counting backwards from the end of the necklace.

- `-1` is the last character
- `-2` is the second-to-last
- And so on...

```python
word = "Python"
print(word[-1])   # last character
print(word[-2])   # second to last
print(word[-6])   # first character (same as index 0)
```

**Expected Output:**
```
n
o
P
```

> **Why is this useful?** When you don't know how long a string is — imagine reading a filename from a folder — negative indexing lets you reliably grab the last few characters without calculating the exact length first.

---

### 1.5 Finding the Length of a String

The built-in `len()` function returns the number of characters in a string (including spaces and punctuation).

```python
sentence = "Hello, World!"
print(len(sentence))
```

**Expected Output:**
```
13
```

Every character — the comma, the space, the exclamation mark — counts. Spaces are characters too.

```python
print(len(""))     # empty string
print(len("Hi"))   # two characters
```

**Expected Output:**
```
0
2
```

> **Thinking prompt:** What does `len("Hello, World!") - 1` give you? Why is that useful when working with indexes?

---

## Part 2 – Slicing Strings

### 2.1 What Is Slicing?

Accessing one character with `word[0]` is useful, but what if you need a **portion** of a string — the first five letters, the last three, or everything from position 4 to position 10?

**Slicing** is the technique for extracting a **substring** (a smaller piece of a string). You specify a start position and a stop position, and Python gives you everything in between.

**The slicing syntax:**

```python
string[start:stop]
```

- `start` — the index where the slice **begins** (this character **is included**)
- `stop` — the index where the slice **ends** (this character **is NOT included** — Python stops just before it)

This "up to but not including" behaviour is a common Python convention. It can feel odd at first, but it makes many calculations very clean.

---

### 2.2 Basic Slicing Examples

**Example – Slicing "Hello, World!":**

```python
text = "Hello, World!"

print(text[0:5])    # characters at index 0, 1, 2, 3, 4
print(text[7:12])   # characters at index 7, 8, 9, 10, 11
```

**Expected Output:**
```
Hello
World
```

**Visualising the positions:**

```
H  e  l  l  o  ,     W  o  r  l  d  !
0  1  2  3  4  5  6  7  8  9 10 11 12
```

`text[0:5]` captures positions 0, 1, 2, 3, 4 → `Hello`  
`text[7:12]` captures positions 7, 8, 9, 10, 11 → `World`

---

### 2.3 Omitting Start or Stop

Python lets you leave out either end of the slice:

- **Omit `start`** → Python assumes you mean "from the very beginning"
- **Omit `stop`** → Python assumes you mean "all the way to the end"

```python
text = "Hello, World!"

print(text[:5])    # from start up to (not including) index 5
print(text[7:])    # from index 7 to the end
print(text[:])     # the entire string
```

**Expected Output:**
```
Hello
World!
Hello, World!
```

> **Real-world use:** If you have a filename like `"report_2024.csv"` and you want just the name without the extension, you can slice off the last 4 characters: `filename[:-4]` → `"report_2024"`. This works regardless of how long the filename is!

---

### 2.4 Slicing with a Step

Slicing has an optional third value called a **step** (also called a stride):

```python
string[start:stop:step]
```

The step controls **how many positions to jump** between each character taken.

```python
text = "Hello, World!"

print(text[0:13:2])   # every second character
print(text[::3])      # every third character, whole string
```

**Expected Output:**
```
Hlo ol!
HlWl
```

**The famous reverse trick:**

```python
text = "Python"
print(text[::-1])   # step of -1 means go backwards
```

**Expected Output:**
```
nohtyP
```

Step `-1` walks backwards through the entire string from end to start — a popular Python trick for reversing a string in one line.

---

### 2.5 Negative Indexes in Slices

You can mix negative indexes into slices freely:

```python
text = "Hello, World!"
print(text[-6:-1])   # five characters before the last one
```

**Expected Output:**
```
World
```

---

> **Thinking prompt:** What slice would give you just the `","` from `"Hello, World!"`? Work it out using the position table above.

---

## Part 3 – Modifying Strings

### 3.1 Strings Are Immutable — A Critical Concept

Before learning modification methods, you must understand one very important rule:

> **Strings in Python are immutable.** This means once a string is created, you cannot change individual characters inside it.

```python
word = "Hello"
word[0] = "J"   # ❌ This causes a TypeError
```

**Error:**
```
TypeError: 'str' object does not support item assignment
```

**Why?** Immutability is a design decision that makes Python strings safe, efficient, and predictable. When you "modify" a string, Python actually creates a **brand-new string** with the changes applied and gives it to you.

**Fix:** Assign the result to a new (or the same) variable:

```python
word = "Hello"
new_word = "J" + word[1:]   # build a new string
print(new_word)
```

**Expected Output:**
```
Jello
```

---

### 3.2 Changing Case

Python strings come with built-in **methods** — think of a method as a specialised function that belongs to strings and can be called using a dot (`.`).

**`upper()` — Convert all letters to UPPERCASE:**

```python
text = "hello world"
print(text.upper())
```

**Expected Output:**
```
HELLO WORLD
```

---

**`lower()` — Convert all letters to lowercase:**

```python
text = "PYTHON IS FUN"
print(text.lower())
```

**Expected Output:**
```
python is fun
```

---

**`title()` — Capitalise the First Letter of Each Word:**

```python
text = "learning python is great"
print(text.title())
```

**Expected Output:**
```
Learning Python Is Great
```

---

**`capitalize()` — Capitalise only the very first letter:**

```python
text = "python programming"
print(text.capitalize())
```

**Expected Output:**
```
Python programming
```

---

**`swapcase()` — Flip every letter's case:**

```python
text = "Hello World"
print(text.swapcase())
```

**Expected Output:**
```
hELLO wORLD
```

> **Real-world use:** `lower()` is extremely common when comparing user input. If a user types "YES", "Yes", or "yes", converting both sides to lowercase before comparing ensures your code treats them identically.

---

### 3.3 Removing Whitespace

**Whitespace** means spaces, tabs, and newlines — invisible characters. They often sneak into data from user input, file reads, or copy-paste.

| Method | What it removes |
|--------|----------------|
| `strip()` | Whitespace from both ends |
| `lstrip()` | Whitespace from the left end only |
| `rstrip()` | Whitespace from the right end only |

```python
messy = "   hello world   "

print(messy.strip())    # removes both sides
print(messy.lstrip())   # removes left side only
print(messy.rstrip())   # removes right side only
```

**Expected Output:**
```
hello world
hello world   
   hello world
```

> **Real-world use:** When reading names or emails from a form or CSV file, `strip()` is almost always the first step to clean the data before using it.

---

### 3.4 Replacing Parts of a String

`replace(old, new)` finds all occurrences of `old` and swaps them for `new`:

```python
sentence = "I love cats. Cats are great."
result = sentence.replace("cats", "dogs")
print(result)
```

**Expected Output:**
```
I love dogs. Cats are great.
```

Notice: `replace()` is **case-sensitive**. It replaced `"cats"` but left `"Cats"` (capital C) untouched. To replace both, you would need `sentence.lower().replace(...)` or two separate replace calls.

**Replacing multiple characters:**

```python
text = "banana"
print(text.replace("a", "o"))
```

**Expected Output:**
```
bonono
```

---

### 3.5 Splitting a String into a List

`split(separator)` breaks a string apart at every occurrence of the separator and returns a **list** (a collection of parts):

```python
sentence = "apple,banana,cherry"
fruits = sentence.split(",")
print(fruits)
```

**Expected Output:**
```
['apple', 'banana', 'cherry']
```

Without a separator argument, `split()` splits on any whitespace:

```python
sentence = "The quick brown fox"
words = sentence.split()
print(words)
```

**Expected Output:**
```
['The', 'quick', 'brown', 'fox']
```

> **Real-world use:** CSV (Comma Separated Values) files store data as text with commas between fields. `split(",")` is a fundamental tool for reading that data into Python.

---

### 3.6 Checking String Content

These methods return `True` or `False` and are excellent for validation:

```python
print("Hello123".isalnum())   # letters and digits only?
print("Hello".isalpha())      # letters only?
print("12345".isdigit())      # digits only?
print("hello".islower())      # all lowercase?
print("HELLO".isupper())      # all uppercase?
print("   ".isspace())        # only whitespace?
```

**Expected Output:**
```
True
True
True
True
True
True
```

---

### 3.7 Finding and Counting Substrings

**`find(substring)` — Returns the index where a substring first appears (or `-1` if not found):**

```python
text = "Hello, World!"
print(text.find("World"))   # where does "World" start?
print(text.find("xyz"))     # not found
```

**Expected Output:**
```
7
-1
```

**`count(substring)` — Counts how many times a substring appears:**

```python
text = "banana"
print(text.count("a"))
```

**Expected Output:**
```
3
```

---

### 3.8 Checking Start and End

```python
filename = "report_2024.csv"

print(filename.startswith("report"))   # does it start with this?
print(filename.endswith(".csv"))       # does it end with this?
```

**Expected Output:**
```
True
True
```

> **Real-world use:** When scanning a folder of files, `endswith(".csv")` is a clean way to filter for only spreadsheet files.

---

## Part 4 – Concatenating Strings

### 4.1 What Is Concatenation?

**Concatenation** means **joining two or more strings together into one**. The word comes from a Latin root meaning "to chain together" — just like linking those letter-beads on the necklace.

In Python, the `+` operator joins strings:

```python
first = "Hello"
second = "World"
result = first + " " + second
print(result)
```

**Expected Output:**
```
Hello World
```

Notice: `+` does **not** automatically add a space. You must include it yourself as `" "` between the two strings.

---

### 4.2 Concatenation Rules

**Rule 1: Both values must be strings.**

```python
name = "Alice"
age = 30
print("Name: " + name)          # ✅ Both strings
print("Age: " + age)            # ❌ TypeError: can only concatenate str to str
print("Age: " + str(age))       # ✅ Convert age to string first
```

**Expected Output (lines 3 and 5):**
```
Name: Alice
Age: 30
```

**`str()` converts a non-string value into its text representation.** This is essential whenever you want to include a number inside a string using `+`.

---

### 4.3 Repeating Strings with `*`

The `*` operator repeats a string a given number of times:

```python
line = "-" * 20
print(line)

laugh = "ha" * 3
print(laugh)
```

**Expected Output:**
```
--------------------
hahaha
```

> **Real-world use:** Creating separator lines in terminal output or padding fields to a fixed width.

---

### 4.4 Building Strings in a Loop

A common pattern is to start with an empty string and add to it piece by piece:

```python
result = ""
words = ["Python", "is", "awesome"]

for word in words:
    result = result + word + " "

print(result.strip())
```

**Expected Output:**
```
Python is awesome
```

> **Thinking prompt:** What happens if you remove `.strip()` from the last line? Why?

---

## Part 5 – Formatting Strings

### 5.1 Why String Formatting?

Concatenation works, but it becomes clunky when mixing many variables and text:

```python
name = "Alice"
age = 30
city = "London"

# Clunky concatenation:
print("My name is " + name + ", I am " + str(age) + " years old, and I live in " + city + ".")
```

This is hard to read and error-prone. Python offers cleaner, more powerful alternatives: **f-strings** (the modern, recommended method) and `format()`.

---

### 5.2 F-Strings (Formatted String Literals) — The Modern Way

An **f-string** is a string that starts with the letter `f` before the opening quote. Inside the string, you place variable names (or any expression) inside **curly braces `{}`**. Python automatically inserts the value there.

```python
name = "Alice"
age = 30
print(f"My name is {name} and I am {age} years old.")
```

**Expected Output:**
```
My name is Alice and I am 30 years old.
```

**Line-by-line:**
- `f"..."` — the `f` prefix activates f-string mode
- `{name}` — Python replaces this with the value of the variable `name`
- `{age}` — Python replaces this with the value of `age` (automatically converted to text — no `str()` needed!)

---

### 5.3 F-Strings with Expressions

You can put any valid Python expression inside `{}`:

```python
price = 49.99
quantity = 3

print(f"Total cost: ${price * quantity:.2f}")
```

**Expected Output:**
```
Total cost: $149.97
```

**What is `:.2f`?**  
This is a **format specifier**. The `:` separates the expression from formatting instructions. `.2f` means: display as a **f**loating-point number with exactly **2** decimal places. This is invaluable for money, measurements, and scientific values.

---

**More format specifiers:**

```python
pi = 3.14159265

print(f"Pi to 2 decimal places: {pi:.2f}")
print(f"Pi to 4 decimal places: {pi:.4f}")
print(f"Pi as integer: {pi:.0f}")
```

**Expected Output:**
```
Pi to 2 decimal places: 3.14
Pi to 4 decimal places: 3.1416
Pi as integer: 3
```

---

### 5.4 The `format()` Method — The Classic Way

Before f-strings existed (prior to Python 3.6), `format()` was the standard approach. You will encounter it in older codebases, so it is important to recognise it.

The `format()` method uses `{}` as placeholders inside the string, then fills them in order with the arguments passed to `format()`:

```python
name = "Bob"
age = 25
print("My name is {} and I am {} years old.".format(name, age))
```

**Expected Output:**
```
My name is Bob and I am 25 years old.
```

---

**Using numbered placeholders:**

```python
print("First: {0}, Second: {1}, First again: {0}".format("apple", "banana"))
```

**Expected Output:**
```
First: apple, Second: banana, First again: apple
```

The `{0}` means "insert the first argument", `{1}` the second. You can reuse them.

---

**Using named placeholders:**

```python
print("Name: {n}, Age: {a}".format(n="Carol", a=28))
```

**Expected Output:**
```
Name: Carol, Age: 28
```

---

### 5.5 The `%` Operator — The Legacy Way

The oldest Python string formatting method uses `%`. You will see it in older tutorials and legacy Python 2 code:

```python
name = "Dave"
age = 35
print("Name: %s, Age: %d" % (name, age))
```

**Expected Output:**
```
Name: Dave, Age: 35
```

- `%s` → string placeholder
- `%d` → integer placeholder
- `%f` → float placeholder

> **Recommendation:** Use f-strings in all new code. They are the most readable, flexible, and efficient of the three methods.

---

### 5.6 F-String Alignment and Padding

F-strings can align text within a fixed-width field — extremely useful for making neat columns in terminal output:

```python
item1 = "Apple"
item2 = "Banana"
item3 = "Kiwi"

print(f"{'Item':<10} {'Price':>8}")
print(f"{item1:<10} {'$1.20':>8}")
print(f"{item2:<10} {'$0.85':>8}")
print(f"{item3:<10} {'$2.50':>8}")
```

**Expected Output:**
```
Item          Price
Apple         $1.20
Banana        $0.85
Kiwi          $2.50
```

- `:<10` — left-align within a 10-character wide field
- `:>8` — right-align within an 8-character wide field

---

## Part 6 – Escape Characters

### 6.1 The Problem: Special Characters Inside Strings

Imagine you want to print:
```
She said "Hello!"
```

If you write:

```python
print("She said "Hello!"")   # ❌ SyntaxError
```

Python gets confused — the second `"` ends the string prematurely, then `Hello` is unparseable code. You need a way to tell Python "this quote is part of the text, not the end of the string."

The solution is **escape characters**.

---

### 6.2 What Is an Escape Character?

An **escape character** is a **backslash `\`** placed before a special character. The backslash tells Python: _"Do not treat the next character normally — interpret it as a special instruction or literal character."_

The backslash + the following character form an **escape sequence** — two characters that Python reads as one special instruction.

---

### 6.3 The Escape Sequences Table

| Escape Sequence | What it produces | Description |
|-----------------|-----------------|-------------|
| `\'` | `'` | Single quote inside a string |
| `\"` | `"` | Double quote inside a string |
| `\\` | `\` | A literal backslash |
| `\n` | (newline) | Moves to a new line |
| `\t` | (tab) | Inserts a horizontal tab |
| `\r` | (carriage return) | Returns cursor to start of line |
| `\b` | (backspace) | Moves back one character |
| `\0` | (null character) | Null / empty character |
| `\ooo` | (octal value) | Character from octal code |
| `\xhh` | (hex value) | Character from hex code |

---

### 6.4 Escape Sequences in Detail with Examples

#### `\"` — Double quote inside a double-quoted string

```python
print("She said \"Hello!\"")
```

**Expected Output:**
```
She said "Hello!"
```

---

#### `\'` — Single quote inside a single-quoted string

```python
print('It\'s a beautiful day.')
```

**Expected Output:**
```
It's a beautiful day.
```

> **Alternative:** When you need a single quote inside the string, you can also use double quotes on the outside (and vice versa):
> ```python
> print("It's a beautiful day.")   # No escape needed
> print('She said "Hello!"')       # No escape needed
> ```

---

#### `\n` — Newline (the most commonly used escape sequence)

```python
print("Line one\nLine two\nLine three")
```

**Expected Output:**
```
Line one
Line two
Line three
```

`\n` is the standard way to create line breaks within a single string — critical for generating multi-line output in reports, emails, and files.

---

#### `\t` — Tab (horizontal indentation)

```python
print("Name:\tAlice")
print("Age:\t30")
print("City:\tLondon")
```

**Expected Output:**
```
Name:	Alice
Age:	30
City:	London
```

`\t` jumps forward to the next tab stop, creating neatly aligned columns.

---

#### `\\` — Literal backslash

A backslash by itself is an escape character, so to print an actual backslash you need two:

```python
print("C:\\Users\\Alice\\Documents")
```

**Expected Output:**
```
C:\Users\Alice\Documents
```

This is especially important when working with Windows file paths.

---

### 6.5 Raw Strings — Disabling Escape Sequences

Sometimes you want Python to treat backslashes as literal characters and ignore all escape sequences. This is common with Windows file paths and **regular expressions** (a text-searching tool).

Prefix the string with `r` to create a **raw string**:

```python
path = r"C:\Users\Alice\new_folder"
print(path)
```

**Expected Output:**
```
C:\Users\Alice\new_folder
```

Without `r`, `\n` would have been a newline and `\f` a form-feed character. With `r`, every `\` is treated as a plain backslash.

---

## Guided Practice Exercises

### Exercise 1 – Student Profile Card

**Objective:** Use string creation, indexing, `len()`, and f-strings to build a formatted profile card.

**Scenario:** You are building a simple student management system. Create a profile card for one student.

**Steps:**

1. Create variables: `first_name`, `last_name`, `age`, `grade`, `city`
2. Combine first and last name into a `full_name` variable using concatenation
3. Print how many characters are in the full name (including the space)
4. Print the first letter of the first name and the first letter of the last name (their initials)
5. Print a formatted profile card using an f-string

**Starter code:**

```python
first_name = "Maria"
last_name = "Santos"
age = 17
grade = "11B"
city = "Melbourne"

# Step 2: Combine names
full_name = first_name + " " + last_name

# Step 3: Name length
print(f"Full name character count: {len(full_name)}")

# Step 4: Initials
print(f"Initials: {first_name[0]}.{last_name[0]}.")

# Step 5: Profile card
print("=" * 30)
print(f"  Name  : {full_name}")
print(f"  Age   : {age}")
print(f"  Grade : {grade}")
print(f"  City  : {city}")
print("=" * 30)
```

**Expected Output:**
```
Full name character count: 12
Initials: M.S.
==============================
  Name  : Maria Santos
  Age   : 17
  Grade : 11B
  City  : Melbourne
==============================
```

**Self-check questions:**
- Why is the character count 12 and not 11?
- What would `full_name[-1]` give you? Why?
- What change would you make to print initials in lowercase?

---

### Exercise 2 – Temperature Data Cleaner

**Objective:** Use `strip()`, `replace()`, `upper()`, `split()`, and f-strings together.

**Scenario:** You receive messy temperature readings from a sensor log file. Clean and report them.

```python
raw_data = "  24.5C, 19.0C, 31.2C, 22.8C,  "

# Step 1: Strip whitespace from both ends
cleaned = raw_data.strip()
print(f"After strip: '{cleaned}'")

# Step 2: Remove the degree symbol 'C' and split into a list
values = cleaned.replace("C", "").split(", ")
print(f"Values list: {values}")

# Step 3: Convert to floats and compute the average
temperatures = [float(v) for v in values if v.strip()]
average = sum(temperatures) / len(temperatures)

# Step 4: Report
print(f"\n--- Temperature Report ---")
print(f"Readings : {temperatures}")
print(f"Count    : {len(temperatures)}")
print(f"Average  : {average:.1f}°C")
print(f"Highest  : {max(temperatures):.1f}°C")
print(f"Lowest   : {min(temperatures):.1f}°C")
```

**Expected Output:**
```
After strip: '24.5C, 19.0C, 31.2C, 22.8C,'
Values list: ['24.5', '19.0', '31.2', '22.8', '']

--- Temperature Report ---
Readings : [24.5, 19.0, 31.2, 22.8]
Count    : 4
Average  : 23.9°C
Highest  : 31.2°C
Lowest   : 19.0°C
```

**What-if challenge:** What happens if you add an extra comma at the end of `raw_data` and don't filter empty strings with `if v.strip()`? Try it!

---

### Exercise 3 – Escape Character Postcard

**Objective:** Use `\n`, `\t`, `\"`, and f-strings to format a postcard message.

```python
sender = "Alice"
recipient = "Bob"
city = "Paris"
weather = "sunny"
temperature = 22

postcard = (
    f"To: {recipient}\n"
    f"From: {sender}\n"
    f"\n"
    f"\tGreetings from {city}!\n"
    f"\tThe weather here is {weather} and {temperature}°C.\n"
    f"\tWish you were here!\n"
    f"\n"
    f"\t\t\t\t- {sender}"
)

print(postcard)
```

**Expected Output:**
```
To: Bob
From: Alice

	Greetings from Paris!
	The weather here is sunny and 22°C.
	Wish you were here!

				- Alice
```

---

## Mini Project — Personal Receipt Generator

### Project Overview

You will build a Python program that generates a formatted shop receipt — a real-world document that combines nearly every string concept from this lesson.

**Skills used:** string creation, f-strings, `.upper()`, `.ljust()`, `.rjust()`, `*` repetition, `\n`, concatenation, `:.2f` formatting.

---

### Stage 1 – Setup: Store and Customer Information

```python
store_name = "Green Valley Market"
store_address = "42 Oak Lane, Riverside"
cashier = "Jamie"
customer_name = "Alice Brown"

# Print header
print("=" * 40)
print(store_name.upper().center(40))
print(store_address.center(40))
print("=" * 40)
print(f"Cashier : {cashier}")
print(f"Customer: {customer_name}")
print("-" * 40)
```

**Milestone Output:**
```
========================================
       GREEN VALLEY MARKET       
     42 Oak Lane, Riverside      
========================================
Cashier : Jamie
Customer: Alice Brown
----------------------------------------
```

---

### Stage 2 – Core Logic: Items and Prices

```python
items = [
    ("Apples (1kg)", 2.99),
    ("Whole Milk (2L)", 1.85),
    ("Sourdough Bread", 3.50),
    ("Cheddar Cheese", 4.20),
    ("Orange Juice (1L)", 2.75),
]

subtotal = 0

print(f"{'ITEM':<25} {'PRICE':>10}")
print("-" * 40)

for name, price in items:
    print(f"{name:<25} ${price:>8.2f}")
    subtotal += price
```

**Milestone Output:**
```
ITEM                          PRICE
----------------------------------------
Apples (1kg)              $    2.99
Whole Milk (2L)           $    1.85
Sourdough Bread           $    3.50
Cheddar Cheese            $    4.20
Orange Juice (1L)         $    2.75
```

---

### Stage 3 – Enhancements: Tax and Total

```python
tax_rate = 0.10   # 10% tax
tax = subtotal * tax_rate
total = subtotal + tax

print("-" * 40)
print(f"{'Subtotal':<25} ${subtotal:>8.2f}")
print(f"{'Tax (10%)':<25} ${tax:>8.2f}")
print("=" * 40)
print(f"{'TOTAL':<25} ${total:>8.2f}")
print("=" * 40)
```

**Milestone Output:**
```
----------------------------------------
Subtotal                  $   15.29
Tax (10%)                 $    1.53
========================================
TOTAL                     $   16.82
========================================
```

---

### Stage 4 – Final Output: Thank You Message

```python
print(f"\n  Thank you, {customer_name.split()[0]}!")
print(f"  Please keep this receipt for your records.")
print(f"\n{'- Green Valley Market -'.center(40)}")
```

**Final Output:**
```

  Thank you, Alice!
  Please keep your receipt for your records.

       - Green Valley Market -       
```

---

### Full Project Reflection Questions

1. Why did we use `customer_name.split()[0]` to get just "Alice" from "Alice Brown"?
2. What does `.center(40)` do? Where else in everyday life do you see centred text?
3. What would you change to add a 20% discount for loyalty card holders?
4. How would you save this receipt to a text file instead of printing it? (Hint: look up Python's `open()` function for the next lesson.)

**Optional Extensions:**
- Add a date and time to the receipt header (look up Python's `datetime` module)
- Add an item quantity column and compute `quantity × unit_price` per line
- Allow the user to input item names and prices interactively using `input()`

---

## Common Beginner Mistakes

### Mistake 1 – Forgetting strings are zero-indexed

```python
word = "Python"
print(word[6])   # ❌ IndexError — valid indexes are 0–5
```

**Fix:** The last valid index is always `len(string) - 1`, or use `word[-1]` for the last character.

---

### Mistake 2 – Trying to concatenate a string and a number

```python
age = 25
print("I am " + age + " years old.")   # ❌ TypeError
```

**Fix:**
```python
print("I am " + str(age) + " years old.")   # ✅ convert with str()
print(f"I am {age} years old.")              # ✅ f-string handles it automatically
```

---

### Mistake 3 – Expecting `replace()` to modify the original string

```python
text = "Hello World"
text.replace("World", "Python")   # ❌ Nothing changes!
print(text)                        # Still "Hello World"
```

**Fix:** Assign the result back:
```python
text = text.replace("World", "Python")   # ✅
print(text)                              # "Hello Python"
```

---

### Mistake 4 – Off-by-one errors in slices

```python
text = "Python"
print(text[0:6])   # ✅ Correct — gives "Python"
print(text[1:6])   # Gives "ython", not "Python"
print(text[0:5])   # Gives "Pytho", not "Python"
```

Remember: `stop` is **excluded**. To get all 6 characters (indexes 0–5), use `[0:6]` or just `[:]`.

---

### Mistake 5 – Missing the `f` prefix on an f-string

```python
name = "Alice"
print("Hello, {name}!")   # ❌ Prints literally: Hello, {name}!
print(f"Hello, {name}!")  # ✅ Prints: Hello, Alice!
```

---

### Mistake 6 – Forgetting to escape backslashes in Windows paths

```python
path = "C:\new_folder\test"   # ❌ \n is a newline, \t is a tab!
print(path)
```

**Expected (broken) Output:**
```
C:
ew_folder	est
```

**Fix:**
```python
path = r"C:\new_folder\test"      # ✅ raw string
# or
path = "C:\\new_folder\\test"     # ✅ escaped backslashes
```

---

### Mistake 7 – Using `+` to concatenate many strings in a loop (performance issue)

```python
result = ""
for i in range(1000):
    result = result + str(i)   # ⚠️ Creates 1000 new strings — slow!
```

**Better fix:** Use `"".join()` for building strings from many parts:
```python
result = "".join(str(i) for i in range(1000))   # ✅ Fast and memory-efficient
```

---

## Reflection Questions

1. What is the difference between `"hello"[0]` and `"hello"[0:1]`? Are they the same type?
2. Can you have a negative step in a slice? What does `text[10:2:-1]` mean?
3. Why do `upper()` and `strip()` return a new string instead of modifying the original? What Python principle does this relate to?
4. If `format()` and f-strings both work, why do most modern Python developers prefer f-strings?
5. What would happen if you used `\\n` in a string? What about `r"\n"`?
6. How would you check if a username entered by a user contains only letters and digits (no spaces or symbols)?

---

## Completion Checklist

Before moving on to Lesson 05, confirm you can:

- [ ] Create strings using single quotes, double quotes, and triple quotes
- [ ] Access individual characters using positive and negative indexes
- [ ] Use `len()` to find a string's length
- [ ] Slice a string with `[start:stop]` and `[start:stop:step]`
- [ ] Reverse a string using `[::-1]`
- [ ] Use `.upper()`, `.lower()`, `.title()`, `.capitalize()`, `.swapcase()`
- [ ] Use `.strip()`, `.lstrip()`, `.rstrip()` to clean whitespace
- [ ] Use `.replace()` to swap parts of a string
- [ ] Use `.split()` to break a string into a list
- [ ] Use `.find()` and `.count()` to search within a string
- [ ] Concatenate strings with `+` and repeat them with `*`
- [ ] Use f-strings with `{}` to insert variables and expressions
- [ ] Apply format specifiers like `:.2f`, `:<10`, `:>8`
- [ ] Use `format()` with positional and named placeholders
- [ ] Use escape sequences: `\n`, `\t`, `\"`, `\'`, `\\`
- [ ] Use raw strings with the `r` prefix
- [ ] Explain why strings are immutable and what that means in practice

---

## Lesson Summary

In this lesson, you mastered Python strings from the ground up. Here is a concise reference of everything covered:

### String Creation
| Method | Example | Result |
|--------|---------|--------|
| Double quotes | `"Hello"` | `Hello` |
| Single quotes | `'Hello'` | `Hello` |
| Triple quotes | `"""Hello\nWorld"""` | Multi-line |

### Indexing & Slicing
| Operation | Example | Result |
|-----------|---------|--------|
| Single char | `"Python"[0]` | `P` |
| Negative index | `"Python"[-1]` | `n` |
| Slice | `"Python"[1:4]` | `yth` |
| From start | `"Python"[:3]` | `Pyt` |
| To end | `"Python"[3:]` | `hon` |
| With step | `"Python"[::2]` | `Pto` |
| Reverse | `"Python"[::-1]` | `nohtyP` |

### Key Methods
| Method | Purpose |
|--------|---------|
| `upper()` / `lower()` | Change case |
| `strip()` | Remove edge whitespace |
| `replace(a, b)` | Swap substring |
| `split(sep)` | Break into list |
| `find(sub)` | Find position |
| `count(sub)` | Count occurrences |
| `startswith()` / `endswith()` | Check edges |
| `len()` | String length |

### String Formatting
| Method | Example |
|--------|---------|
| f-string | `f"Hello {name}"` |
| format() | `"Hello {}".format(name)` |
| % operator | `"Hello %s" % name` |

### Escape Sequences
| Sequence | Meaning |
|----------|---------|
| `\n` | New line |
| `\t` | Tab |
| `\\` | Backslash |
| `\"` | Double quote |
| `\'` | Single quote |

---

> **Up Next — Lesson 05:** In the next lesson, you will learn about Python **Lists** — ordered, changeable collections that let you store and work with multiple values at once. Everything you learned about indexing and slicing strings applies directly to lists too, so you are already well prepared!
