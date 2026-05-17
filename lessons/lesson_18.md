---
render_with_liquid: false
title: "JSON, RegEx, PIP, Error Handling, and String Formatting in Python"
nav_order: 18
---

# Lesson 18 — JSON, RegEx, PIP, Error Handling, and String Formatting in Python

---

## Lesson Introduction

Welcome to Lesson 18! In this lesson you are going to learn five incredibly powerful Python skills that are used every single day by professional developers, data scientists, and engineers around the world.

By the end of this lesson you will be able to:

- Read and write **JSON** data — the universal language of the internet
- Use **Regular Expressions (RegEx)** — a superpower for searching and cleaning text
- Install and manage **third-party Python packages with PIP**
- Handle **errors gracefully** using `try`, `except`, `else`, `finally`, and `raise`
- Format **strings beautifully** using f-strings and the `format()` method

Think of this lesson as your toolkit upgrade. Right now you can build programs that work — after this lesson, your programs will also be able to talk to the internet, search text like a detective, survive errors without crashing, and display polished output.

> **Analogy:** JSON is like a universal container for shipping data between programs. RegEx is like a search engine for text patterns. PIP is like an app store for Python. Try/Except is like a safety net for your code. F-strings are like a smart fill-in-the-blank template.

---

## Prerequisites — What You Need to Know First

Before we start, let's make sure you are comfortable with these ideas:

**1. Variables and data types** — You know what strings, integers, floats, booleans, and `None` are.

**2. Dictionaries** — A dictionary is a collection of key-value pairs in Python. Example:

```python
person = {"name": "Alice", "age": 25}
print(person["name"])   # Alice
print(person["age"])    # 25
```

**3. Lists** — An ordered collection you can loop over:

```python
fruits = ["apple", "banana", "mango"]
print(fruits[0])   # apple
```

**4. Import statements** — You know how to bring a module into your program:

```python
import math
print(math.sqrt(16))   # 4.0
```

**5. Functions** — You can define and call functions:

```python
def greet(name):
    return "Hello, " + name

print(greet("Bisi"))   # Hello, Bisi
```

If any of the above feels unfamiliar, please review those topics before continuing. This lesson builds directly on top of them.

---

## Part 1 — JSON: Python's Universal Data Language

### What is JSON and Why Does It Exist?

Imagine two completely different systems need to share data. One is a Python program running on a computer in Lagos. The other is a JavaScript app running in a browser in London. They speak different programming languages — how can they share information?

The answer is **JSON** (pronounced "jay-son"). JSON stands for **JavaScript Object Notation**. It is a format for storing and exchanging data as plain text. Because it is just text, any programming language can read it and write it.

> **Real-world analogy:** JSON is like a standard shipping box. It does not matter if you are sending a parcel from Nigeria to Germany — both countries understand the same box shape, labels, and delivery rules. JSON is that "box" for data.

### What Does JSON Look Like?

JSON looks almost exactly like a Python dictionary. Here is a simple example:

```json
{
    "name": "John",
    "age": 30,
    "city": "New York"
}
```

Notice:
- Data is stored as **key-value pairs** just like Python dictionaries
- Keys are always **strings in double quotes**
- Values can be strings, numbers, booleans (`true`/`false`), `null`, lists, or other objects
- Items are separated by commas

### The `json` Module — Python's Built-in JSON Tool

Python comes with a built-in module called `json`. You do not need to install anything — just import it.

```python
import json
```

That one line gives you access to everything you need.

---

### Converting JSON Text INTO Python — `json.loads()`

**The Problem:** You receive data from a website. It comes as a long JSON text string. You want to use Python to work with it — access specific values, loop through items, etc. But it is just raw text right now; Python does not know it has structure.

**The Solution:** `json.loads()` — this function takes a JSON string and converts it into a Python dictionary (or list, depending on the data).

> **"loads" means "load string"** — it loads a JSON string into Python.

**Simple Example:**

```python
import json

# This is a JSON string - notice the outer quotes make it a string
json_string = '{"name": "Alice", "age": 22, "city": "Abuja"}'

# Convert it to a Python dictionary
python_dict = json.loads(json_string)

# Now we can use it like a regular dictionary!
print(python_dict["name"])   # Alice
print(python_dict["age"])    # 22
print(python_dict["city"])   # Abuja
```

**Expected Output:**
```
Alice
22
Abuja
```

> **Key insight:** Before `json.loads()`, your data is just a string of characters — Python cannot do `["name"]` on it. After `json.loads()`, it becomes a real Python dictionary you can work with.

**Thinking Prompt:** What would happen if you tried to do `json_string["name"]` directly, without converting it first? Try it — you will get a `TypeError`! That is because strings are indexed with numbers (0, 1, 2...), not text keys.

---

### Converting Python INTO JSON Text — `json.dumps()`

**The Problem:** You have a Python dictionary with data. You want to send it to a web API, save it to a file, or share it with another system. But those systems expect JSON text, not a Python object.

**The Solution:** `json.dumps()` — this converts a Python object into a JSON string.

> **"dumps" means "dump string"** — it dumps the Python data into a string format.

**Simple Example:**

```python
import json

# A Python dictionary
person = {
    "name": "Chidi",
    "age": 28,
    "city": "Lagos"
}

# Convert it to a JSON string
json_text = json.dumps(person)

print(json_text)
print(type(json_text))
```

**Expected Output:**
```
{"name": "Chidi", "age": 28, "city": "Lagos"}
<class 'str'>
```

Notice that `json.dumps()` returns a **string** (`<class 'str'>`). That is what JSON always is — just text.

---

### What Python Types Convert to What JSON Types?

Python and JSON are very similar, but not identical. Here is the conversion table:

| Python Type | Becomes JSON |
|---|---|
| `dict` | Object `{}` |
| `list` | Array `[]` |
| `tuple` | Array `[]` |
| `str` | String `"..."` |
| `int` | Number |
| `float` | Number |
| `True` | `true` (lowercase!) |
| `False` | `false` (lowercase!) |
| `None` | `null` |

**Example showing all types:**

```python
import json

print(json.dumps({"name": "John", "age": 30}))  # dict
print(json.dumps(["apple", "banana"]))           # list
print(json.dumps(("apple", "banana")))           # tuple
print(json.dumps("hello"))                       # string
print(json.dumps(42))                            # int
print(json.dumps(31.76))                         # float
print(json.dumps(True))                          # boolean
print(json.dumps(False))                         # boolean
print(json.dumps(None))                          # None
```

**Expected Output:**
```
{"name": "John", "age": 30}
["apple", "banana"]
["apple", "banana"]
"hello"
42
31.76
true
false
null
```

> **Watch carefully:** Python's `True` becomes JSON's `true` (lowercase). Python's `None` becomes JSON's `null`. These are the two most common sources of confusion for beginners!

---

### Making JSON Pretty — `indent` Parameter

By default, `json.dumps()` puts everything on one line. When the data gets complex, that becomes very hard to read. Use the `indent` parameter to add spaces and line breaks:

```python
import json

person = {
    "name": "John",
    "age": 30,
    "married": True,
    "children": ["Ann", "Billy"],
    "pets": None,
    "cars": [
        {"model": "BMW 230", "mpg": 27.5},
        {"model": "Ford Edge", "mpg": 24.1}
    ]
}

# Without indent — hard to read
print(json.dumps(person))
print()

# With indent=4 — easy to read
print(json.dumps(person, indent=4))
```

**Expected Output (with indent=4):**
```json
{
    "name": "John",
    "age": 30,
    "married": true,
    "children": [
        "Ann",
        "Billy"
    ],
    "pets": null,
    "cars": [
        {
            "model": "BMW 230",
            "mpg": 27.5
        },
        {
            "model": "Ford Edge",
            "mpg": 24.1
        }
    ]
}
```

The `indent=4` parameter tells Python to indent each level by 4 spaces. You can use any number you like.

---

### Sorting Keys — `sort_keys` Parameter

Sometimes you want the keys in alphabetical order (useful for comparing outputs, debugging, or displaying data consistently):

```python
import json

data = {"banana": 3, "apple": 5, "cherry": 1}

print(json.dumps(data, indent=4, sort_keys=True))
```

**Expected Output:**
```json
{
    "apple": 5,
    "banana": 3,
    "cherry": 1
}
```

---

### Custom Separators — `separators` Parameter

The default JSON output uses `", "` between items and `": "` between keys and values. You can change these:

```python
import json

data = {"name": "Ali", "age": 25}

# Default separators
print(json.dumps(data))
# Output: {"name": "Ali", "age": 25}

# Custom separators — no spaces (more compact)
print(json.dumps(data, separators=(",", ":")))
# Output: {"name":"Ali","age":25}

# Custom separators — different style
print(json.dumps(data, indent=4, separators=(". ", " = ")))
```

**Expected Output (last print):**
```json
{
    "name" = "Ali". 
    "age" = 25
}
```

---

### Real-World Use of JSON

JSON is everywhere in the real world:

- **Weather apps** receive weather data as JSON from online services
- **Social media platforms** send your feed data as JSON to your phone
- **Banking apps** send transaction records as JSON
- **Data science pipelines** store configuration files as JSON
- **Web APIs** (Application Programming Interfaces) almost universally use JSON

When you write Python code that connects to the internet (using the `requests` library), almost all the data you receive will be JSON.

---

## Part 2 — Regular Expressions (RegEx): Searching Text Like a Pro

### What is RegEx and Why Does It Exist?

Imagine you have a huge document — maybe 10,000 lines of customer data — and you need to find every phone number that matches the pattern `080-XXXX-XXXX`. Or you want to check if a user typed a valid email address. Or you want to replace all dates written as `DD/MM/YYYY` with the format `YYYY-MM-DD`.

You **could** write many lines of code with loops and if-statements to do this. But Python has a much more powerful tool: **Regular Expressions**, also called **RegEx** or **RE**.

> **What is RegEx?** A Regular Expression is a sequence of characters that defines a search pattern. Think of it like a very smart search-and-replace tool that understands patterns, not just exact text.

> **Real-world analogy:** Imagine you are searching a library for all books published in the 1990s. Instead of looking at each book individually, you ask the librarian "Give me everything with a year between 1990 and 1999 on the cover." That search instruction is like a RegEx — a pattern, not an exact match.

### The `re` Module

Python's RegEx tools live in the built-in `re` module:

```python
import re
```

---

### The Four Main RegEx Functions

The `re` module gives you four key functions. Let's understand each one:

#### 1. `re.search()` — Find if a pattern exists anywhere

`re.search()` looks through the entire string for the pattern. If it finds even one match, it returns a **Match object** (which is truthy — it means "yes, found it!"). If it finds nothing, it returns `None`.

```python
import re

txt = "The rain in Spain"
result = re.search("Spain", txt)

if result:
    print("Found it!")
else:
    print("Not found.")
```

**Expected Output:**
```
Found it!
```

**Second example — not found:**

```python
import re

txt = "The rain in Spain"
result = re.search("France", txt)

if result:
    print("Found it!")
else:
    print("Not found.")
```

**Expected Output:**
```
Not found.
```

---

#### 2. `re.findall()` — Find ALL matches and return a list

`re.findall()` finds every occurrence of the pattern and returns them as a Python list. If nothing is found, it returns an empty list `[]`.

```python
import re

txt = "The rain in Spain, the main domain"
matches = re.findall("ain")

print(matches)
print(len(matches), "matches found")
```

**Expected Output:**
```
['ain', 'ain', 'ain', 'ain']
4 matches found
```

---

#### 3. `re.split()` — Split a string at every match

`re.split()` works like the regular string `.split()` method, but it can split on patterns, not just fixed characters.

```python
import re

txt = "apple,banana;cherry mango"

# Split on comma, semicolon, or space
result = re.split("[,; ]", txt)
print(result)
```

**Expected Output:**
```
['apple', 'banana', 'cherry', 'mango']
```

You can also limit how many splits happen:

```python
import re

txt = "one two three four five"
result = re.split(" ", txt, maxsplit=2)
print(result)
```

**Expected Output:**
```
['one', 'two', 'three four five']
```

---

#### 4. `re.sub()` — Substitute (replace) matches with something else

`re.sub()` finds all matches and replaces them with a new string. This is like "Find and Replace" in a text editor, but for patterns.

```python
import re

txt = "The rain in Spain"

# Replace every "a" with "o"
result = re.sub("a", "o", txt)
print(result)
```

**Expected Output:**
```
The roin in Spoin
```

You can limit the number of replacements:

```python
import re

txt = "The rain in Spain"
result = re.sub("a", "o", txt, count=1)   # Only replace the FIRST match
print(result)
```

**Expected Output:**
```
The roin in Spain
```

---

### Metacharacters — The Special Characters of RegEx

This is where RegEx gets its real power. **Metacharacters** are special symbols that represent patterns rather than literal characters.

Think of regular letters in a pattern as "match this exact letter." Metacharacters are like wildcards — they match a whole category of characters.

Here are the most important ones:

| Symbol | What it means | Example Pattern | What it matches |
|---|---|---|---|
| `.` | Any single character (except newline) | `"he..o"` | "hello", "heBo", "he12o" |
| `^` | Start of the string | `"^Hello"` | "Hello world" (starts with Hello) |
| `$` | End of the string | `"world$"` | "Hello world" (ends with world) |
| `*` | Zero or more of the previous | `"ab*c"` | "ac", "abc", "abbc", "abbbc" |
| `+` | One or more of the previous | `"ab+c"` | "abc", "abbc" (NOT "ac") |
| `?` | Zero or one of the previous | `"ab?c"` | "ac" or "abc" only |
| `{n}` | Exactly n times | `"a{3}"` | "aaa" (exactly 3 a's) |
| `\|` | OR — match either side | `"cat\|dog"` | "cat" or "dog" |
| `[]` | A set of characters | `"[aeiou]"` | any single vowel |
| `()` | A group | `"(ha)+"` | "ha", "haha", "hahaha" |
| `\` | Escape special character | `"\."` | a literal dot `.` |

**Example — using `^` and `$` to match exact pattern:**

```python
import re

txt = "The rain in Spain"

# Check if text starts with "The" AND ends with "Spain"
result = re.search("^The.*Spain$", txt)

if result:
    print("Pattern matched!")
else:
    print("No match.")
```

**Expected Output:**
```
Pattern matched!
```

Here `^The` means "starts with The", `.*` means "any characters in between" (`.` = any char, `*` = zero or more), and `Spain$` means "ends with Spain".

---

### Special Sequences — Shorthand Patterns

Special sequences are backslash codes that match common categories of characters:

| Code | What it matches | Example |
|---|---|---|
| `\d` | Any digit 0–9 | `"\d"` matches "7" in "abc7def" |
| `\D` | Any NON-digit | `"\D"` matches "a" in "a7b" |
| `\w` | Any word character (letters, digits, underscore) | `"\w"` matches "a", "7", "_" |
| `\W` | Any NON-word character | `"\W"` matches " ", "!", "." |
| `\s` | Any whitespace (space, tab, newline) | `"\s"` matches the space in "hello world" |
| `\S` | Any non-whitespace | `"\S"` matches "h" in "hello" |
| `\b` | Word boundary (start or end of a word) | `r"\bcat\b"` matches "cat" but not "catalog" |
| `\A` | Start of string | `"\AThe"` matches only if string starts with "The" |
| `\Z` | End of string | `"Spain\Z"` matches only if string ends with "Spain" |

**Example — extract all numbers from a string:**

```python
import re

txt = "I have 3 cats and 12 dogs and 1 fish"
numbers = re.findall(r"\d+", txt)
print(numbers)
```

**Expected Output:**
```
['3', '12', '1']
```

Here `\d+` means "one or more digits". The `r` before the string makes it a **raw string** — this prevents Python from misinterpreting backslashes.

> **Important:** Always use `r"..."` (raw strings) for RegEx patterns that contain backslashes like `\d`, `\w`, `\s`, etc. Without the `r`, Python might interpret `\d` as an escape sequence.

---

### Sets — Character Sets in Square Brackets

A **set** is a group of characters inside `[...]`. The pattern matches ONE character from that set.

| Pattern | Matches |
|---|---|
| `[abc]` | "a", "b", or "c" |
| `[a-z]` | Any lowercase letter |
| `[A-Z]` | Any uppercase letter |
| `[0-9]` | Any digit (same as `\d`) |
| `[a-zA-Z]` | Any letter (upper or lower) |
| `[^abc]` | Any character EXCEPT "a", "b", "c" |

**Example — find all vowels:**

```python
import re

txt = "Hello World"
vowels = re.findall("[aeiouAEIOU]", txt)
print(vowels)
```

**Expected Output:**
```
['e', 'o', 'o']
```

---

### RegEx Flags — Modifying How Matching Works

Flags change the behaviour of the matching engine. The most useful ones:

| Flag | Shorthand | Effect |
|---|---|---|
| `re.IGNORECASE` | `re.I` | Makes matching case-insensitive |
| `re.MULTILINE` | `re.M` | Makes `^` and `$` match start/end of each LINE |
| `re.DOTALL` | `re.S` | Makes `.` match newlines too |

**Example — case-insensitive search:**

```python
import re

txt = "Hello WORLD hello World"
matches = re.findall("hello", txt, re.IGNORECASE)
print(matches)
```

**Expected Output:**
```
['Hello', 'hello', 'Hello']
```

---

### The Match Object

When `re.search()` or other functions find a match, they return a **Match object** — a special object with useful methods:

```python
import re

txt = "The rain in Spain"
match = re.search(r"\bS\w+", txt)   # Find a word starting with "S"

if match:
    print("Match found:", match.group())   # The matched text
    print("Start position:", match.start())
    print("End position:", match.end())
    print("Span:", match.span())
```

**Expected Output:**
```
Match found: Spain
Start position: 12
End position: 17
Span: (12, 17)
```

---

### Real-World Use of RegEx

- **Email validation:** Check if a user's email follows the pattern `name@domain.com`
- **Phone number extraction:** Pull all phone numbers from a document
- **Log file analysis:** Find all error lines in a 10,000-line server log
- **Data cleaning:** Remove all non-numeric characters from a price column
- **URL parsing:** Extract all links from a webpage's HTML
- **Password validation:** Ensure a password has at least one uppercase letter, one number, and one special character

---

## Part 3 — PIP: Python's Package Manager

### What is PIP and Why Does It Exist?

Python comes with many built-in tools (like `json` and `re`), but the Python community has also created tens of thousands of extra tools — called **packages** or **libraries**. These cover everything from web development to machine learning to image processing to sending emails.

**PIP** (which stands for "Pip Installs Packages") is the tool that lets you download and install these packages from the internet with a single command.

> **Analogy:** Imagine your phone came with some basic apps pre-installed (calculator, calendar, messages). But you want WhatsApp, Instagram, or a banking app. You go to the App Store or Google Play and download them. PIP is that App Store for Python packages.

The place where all these packages are stored is called **PyPI** — the Python Package Index — at `https://pypi.org/`. It currently hosts over 500,000 packages.

---

### Checking if PIP is Installed

If you have Python 3.4 or later (which is almost certainly the case), PIP is included automatically. To check:

Open your **terminal** or **command prompt** and type:

```
pip --version
```

You should see something like:

```
pip 23.0 from /usr/local/lib/python3.11/... (python 3.11)
```

If you see a version number, PIP is ready to use!

---

### Installing a Package

To download and install a package, use the `pip install` command in your terminal:

```
pip install camelcase
```

This downloads the `camelcase` package from PyPI and installs it on your computer. You only need to do this once — after installation, you can use the package in any Python program.

> **Note:** PIP commands are typed in your **terminal/command prompt**, NOT inside your Python program. Do not type `pip install` inside your `.py` file!

---

### Using an Installed Package

After installation, you use the package in your Python file with `import`:

```python
import camelcase

c = camelcase.CamelCase()

txt = "hello world from python"
print(c.hump(txt))
```

**Expected Output:**
```
Hello World From Python
```

Let's break down every line:
- `import camelcase` — loads the installed camelcase package
- `c = camelcase.CamelCase()` — creates a CamelCase object (a tool from the package)
- `c.hump(txt)` — calls the `hump()` method which capitalizes each word

---

### Removing a Package

To uninstall a package you no longer need:

```
pip uninstall camelcase
```

PIP will ask you to confirm:

```
Uninstalling camelcase-0.2:
  Would remove: ...
Proceed (y/n)?
```

Press `y` and the package is removed.

---

### Listing All Installed Packages

To see everything currently installed on your system:

```
pip list
```

Example output:

```
Package           Version
----------------- -------
camelcase         0.2
numpy             1.24.0
pandas            2.0.0
pip               23.0
requests          2.28.2
setuptools        65.5.0
```

This shows you every package and its version number.

---

### Popular Packages You Will Use

Here are some of the most widely used Python packages:

- **`requests`** — Send HTTP requests to websites and APIs
- **`numpy`** — Powerful numerical computing
- **`pandas`** — Data analysis and spreadsheet-like operations
- **`matplotlib`** — Creating charts and graphs
- **`flask`** — Building web applications
- **`django`** — Full-featured web framework
- **`scikit-learn`** — Machine learning algorithms
- **`pillow`** — Image processing
- **`beautifulsoup4`** — Web scraping (extracting data from websites)
- **`pytest`** — Writing and running tests

---

### Finding New Packages

Browse thousands of packages at **https://pypi.org/** — you can search by name or category.

---

## Part 4 — Try / Except: Handling Errors Gracefully

### What is Error Handling and Why Does It Exist?

Even well-written programs encounter unexpected situations:
- The user types text where a number was expected
- A file you try to open does not exist
- The internet connection drops while downloading data
- A calculation results in division by zero

When any of these happen in a normal Python program, Python **stops immediately** and prints an error message — the program crashes. This is terrible for real-world applications.

**Error handling** lets you say: "If something goes wrong, don't crash — do this instead."

> **Analogy:** Imagine a car that completely breaks down every time it hits a pothole. That would be terrible. Instead, a good car has **shock absorbers** — it detects the problem, handles it smoothly, and keeps going. Python's `try/except` is your code's shock absorber.

---

### Without Error Handling — The Problem

```python
# This will CRASH the program
print(x)
```

**Output (error):**
```
NameError: name 'x' is not defined
```

The program stops completely. If this was inside a larger application (like a web server), the entire application would crash.

---

### The `try` and `except` Blocks — Basic Syntax

The `try` block contains the code you want to run. The `except` block contains what to do if something goes wrong:

```python
try:
    print(x)             # This will fail — x doesn't exist
except:
    print("An error occurred!")   # This runs instead of crashing
```

**Expected Output:**
```
An error occurred!
```

The program does NOT crash. It detects the error, handles it, and continues running.

---

### Catching Specific Error Types

Python has many different types of errors. You can catch specific ones and handle them differently:

```python
try:
    print(x)
except NameError:
    print("Variable is not defined!")
except:
    print("Some other error occurred!")
```

**Expected Output:**
```
Variable is not defined!
```

Common Python error types:

| Error Type | When it Happens |
|---|---|
| `NameError` | You used a variable that doesn't exist |
| `TypeError` | Wrong type used in an operation (e.g., add string + number) |
| `ValueError` | Right type but wrong value (e.g., `int("abc")`) |
| `ZeroDivisionError` | You divided by zero |
| `FileNotFoundError` | You tried to open a file that doesn't exist |
| `IndexError` | You used an index that's out of range for a list |
| `KeyError` | You tried to access a dictionary key that doesn't exist |

**Example — catching division by zero:**

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("You cannot divide by zero!")
except:
    print("Something else went wrong.")
```

**Expected Output:**
```
You cannot divide by zero!
```

---

### The `else` Block — Code to Run When NO Error Occurs

Sometimes you want to do something only when the `try` block succeeds:

```python
try:
    print("Hello!")
except:
    print("Something went wrong.")
else:
    print("Everything worked perfectly!")
```

**Expected Output:**
```
Hello!
Everything worked perfectly!
```

The `else` block only runs if the `try` block had **no errors**.

**Thinking Prompt:** What would happen if you changed `print("Hello!")` to `print(undefined_var)`? Which blocks would run?

---

### The `finally` Block — Always Runs No Matter What

The `finally` block runs whether the code succeeded or failed. It is used for cleanup operations — things that must always happen regardless:

```python
try:
    print(x)
except:
    print("Something went wrong.")
finally:
    print("This always runs — no matter what!")
```

**Expected Output:**
```
Something went wrong.
This always runs — no matter what!
```

Even if there is an error, `finally` still executes.

---

### A Real-World Example — File Handling with `finally`

A classic use of `finally` is closing files. If you open a file but something goes wrong while writing, you still need to close the file:

```python
try:
    f = open("myfile.txt")
    try:
        f.write("Hello World")
    except:
        print("Could not write to the file.")
    finally:
        f.close()    # This ALWAYS runs — file is always closed
except:
    print("Could not open the file.")
```

Without `finally`, if writing fails, the file might stay open and become corrupted.

---

### Raising Your Own Exceptions — The `raise` Keyword

Sometimes you want to deliberately trigger an error when certain conditions are not met. This is called **raising an exception**.

```python
x = -5

if x < 0:
    raise Exception("Sorry, no negative numbers allowed!")

print(x)
```

**Expected Output (error):**
```
Exception: Sorry, no negative numbers allowed!
```

You can also raise specific error types:

```python
x = "hello"

if not type(x) is int:
    raise TypeError("Only integers are allowed!")
```

**Expected Output (error):**
```
TypeError: Only integers are allowed!
```

This is extremely useful when you are building functions and need to validate input:

```python
def calculate_square_root(n):
    if n < 0:
        raise ValueError("Cannot calculate square root of a negative number!")
    return n ** 0.5

try:
    result = calculate_square_root(-9)
except ValueError as e:
    print("Error:", e)
```

**Expected Output:**
```
Error: Cannot calculate square root of a negative number!
```

> **Note:** `except ValueError as e:` captures the error message in the variable `e`, which you can then print.

---

### Putting It All Together — Full Try/Except Structure

```python
try:
    # Code that might fail goes here
    number = int(input("Enter a number: "))
    result = 100 / number
except ValueError:
    print("That's not a valid number!")
except ZeroDivisionError:
    print("You can't divide by zero!")
except Exception as e:
    print(f"Unexpected error: {e}")
else:
    print(f"100 divided by {number} = {result}")
finally:
    print("Program finished.")
```

---

## Part 5 — String Formatting: Making Your Output Beautiful

### What is String Formatting and Why Does It Matter?

When your program needs to display information to a user, raw output is rarely good enough. Compare these two outputs:

Bad:
```
The price is 59.0 dollars
```

Better:
```
The price is $59.00
```

**String formatting** gives you control over exactly how values appear when printed: how many decimal places, alignment, adding commas to large numbers, percentage signs, and much more.

There are two main approaches in Python: **f-strings** (the modern, preferred way) and the **`format()` method** (the older way, still widely used).

---

### F-Strings — The Modern, Preferred Approach

F-strings were introduced in Python 3.6 and are now the recommended way to format strings. They are fast, readable, and powerful.

**How to create an f-string:** Put the letter `f` (or `F`) directly before the opening quote:

```python
txt = f"Hello, this is an f-string!"
print(txt)
```

**Expected Output:**
```
Hello, this is an f-string!
```

---

### Placeholders — Embedding Variables

The real power of f-strings is **placeholders** — curly braces `{}` where you insert variables directly into the string:

```python
name = "Amaka"
age = 24
city = "Enugu"

txt = f"My name is {name}, I am {age} years old, and I live in {city}."
print(txt)
```

**Expected Output:**
```
My name is Amaka, I am 24 years old, and I live in Enugu.
```

> **Why this is amazing:** Instead of messy string concatenation like `"My name is " + name + ", I am " + str(age) + "..."`, you just write it naturally with `{variable}` placeholders.

---

### Modifiers — Controlling How Values Look

A **modifier** is added after a `:` inside the placeholder. It controls formatting:

**Decimal places with `:.Nf`:**

```python
price = 59

# Show 2 decimal places
txt = f"The price is {price:.2f} dollars"
print(txt)
```

**Expected Output:**
```
The price is 59.00 dollars
```

Here `.2f` means:
- `.2` = two decimal places
- `f` = fixed-point (decimal) number format

**More decimal examples:**

```python
pi = 3.14159265358979

print(f"Pi to 2 decimal places: {pi:.2f}")
print(f"Pi to 4 decimal places: {pi:.4f}")
print(f"Pi to 0 decimal places: {pi:.0f}")
```

**Expected Output:**
```
Pi to 2 decimal places: 3.14
Pi to 4 decimal places: 3.1416
Pi to 0 decimal places: 3
```

---

### Performing Math Operations Inside F-Strings

You can put entire expressions inside `{}`:

```python
# Direct math
txt = f"5 times 12 equals {5 * 12}"
print(txt)
# Output: 5 times 12 equals 60

# Using variables in math
price = 59
tax_rate = 0.075
total = f"Total with tax: {price + (price * tax_rate):.2f} dollars"
print(total)
# Output: Total with tax: 63.43 dollars
```

---

### If/Else Inside F-Strings

You can embed conditional logic directly:

```python
price = 45

result = f"This item is {'Expensive' if price > 50 else 'Affordable'}"
print(result)
```

**Expected Output:**
```
This item is Affordable
```

---

### Calling Functions Inside F-Strings

```python
fruit = "mango"
print(f"I love {fruit.upper()}")
# Output: I love MANGO

name = "  alice  "
print(f"Hello, {name.strip().title()}!")
# Output: Hello, Alice!
```

You can even call your own custom functions:

```python
def dollars_to_naira(usd, rate=1500):
    return usd * rate

price_usd = 10
txt = f"${price_usd} USD = ₦{dollars_to_naira(price_usd):,} NGN"
print(txt)
```

**Expected Output:**
```
$10 USD = ₦15,000 NGN
```

---

### Formatting Types Reference

Here are the most commonly used format types:

| Modifier | What it does | Example | Output |
|---|---|---|---|
| `:.2f` | Fixed decimal, 2 places | `f"{3.14159:.2f}"` | `3.14` |
| `:.0f` | No decimal places (round) | `f"{3.7:.0f}"` | `4` |
| `:,` | Comma as thousands separator | `f"{1000000:,}"` | `1,000,000` |
| `:%` | Percentage | `f"{0.75:%}"` | `75.000000%` |
| `:.2%` | Percentage with 2 decimals | `f"{0.75:.2%}"` | `75.00%` |
| `:e` | Scientific notation (lowercase) | `f"{123456:e}"` | `1.234560e+05` |
| `:b` | Binary | `f"{10:b}"` | `1010` |
| `:o` | Octal | `f"{8:o}"` | `10` |
| `:x` | Hexadecimal (lowercase) | `f"{255:x}"` | `ff` |
| `:X` | Hexadecimal (uppercase) | `f"{255:X}"` | `FF` |
| `:<10` | Left-align in 10-char space | `f"{'hi':<10}!"` | `hi        !` |
| `:>10` | Right-align in 10-char space | `f"{'hi':>10}!"` | `        hi!` |
| `:^10` | Center in 10-char space | `f"{'hi':^10}!"` | `    hi    !` |

**Practical examples:**

```python
price = 1234567.891

print(f"Plain:       {price}")
print(f"2 decimals:  {price:.2f}")
print(f"With commas: {price:,.2f}")
print(f"As percent:  {0.854:.1%}")
print(f"Scientific:  {price:.2e}")
```

**Expected Output:**
```
Plain:       1234567.891
2 decimals:  1234567.89
With commas: 1,234,567.89
As percent:  85.4%
Scientific:  1.23e+06
```

---

### The `format()` Method — The Older Approach

Before f-strings, Python used the `.format()` method. You will see this in older code, so it is important to understand:

**Basic usage:**

```python
price = 49
txt = "The price is {} dollars"
print(txt.format(price))
```

**Expected Output:**
```
The price is 49 dollars
```

The `{}` is a placeholder that gets filled with the value passed to `.format()`.

**With formatting modifier:**

```python
price = 49.5
txt = "The price is {:.2f} dollars"
print(txt.format(price))
```

**Expected Output:**
```
The price is 49.50 dollars
```

**Multiple placeholders:**

```python
quantity = 3
item_number = 567
price = 49

order = "I want {} pieces of item {} for {:.2f} dollars."
print(order.format(quantity, item_number, price))
```

**Expected Output:**
```
I want 3 pieces of item 567 for 49.00 dollars.
```

---

### Index Numbers in `format()`

You can specify which argument goes where using index numbers:

```python
name = "John"
age = 36

txt = "His name is {1}. {1} is {0} years old."
print(txt.format(age, name))
```

**Expected Output:**
```
His name is John. John is 36 years old.
```

`{0}` refers to the first argument (`age`), `{1}` refers to the second (`name`). You can reuse the same index multiple times.

---

### Named Indexes in `format()`

You can use names inside the braces for more readable code:

```python
order = "I have a {carname}, it is a {model}."
print(order.format(carname="Ford", model="Mustang"))
```

**Expected Output:**
```
I have a Ford, it is a Mustang.
```

---

## Guided Practice Exercises

### Exercise 1 — JSON Roundtrip

**Objective:** Practice converting Python data to JSON and back.

**Scenario:** You are building a student record system. Convert student data to JSON for storage, then read it back.

**Steps:**
1. Create a Python dictionary for a student with name, age, grade, and subjects (a list)
2. Convert it to a formatted JSON string with `indent=4` and `sort_keys=True`
3. Print the JSON string
4. Convert the JSON string back to Python
5. Print just the student's subjects

**Starter code:**

```python
import json

# Step 1: Create student dictionary
student = {
    "name": "Fatima",
    "age": 17,
    "grade": "A",
    "subjects": ["Mathematics", "Physics", "Chemistry", "English"]
}

# Step 2 & 3: Convert to JSON and print
json_output = json.dumps(student, indent=4, sort_keys=True)
print("JSON output:")
print(json_output)

# Step 4 & 5: Convert back to Python
python_data = json.loads(json_output)
print("\nStudent's subjects:")
for subject in python_data["subjects"]:
    print(" -", subject)
```

**Expected Output:**
```json
JSON output:
{
    "age": 17,
    "grade": "A",
    "name": "Fatima",
    "subjects": [
        "Mathematics",
        "Physics",
        "Chemistry",
        "English"
    ]
}

Student's subjects:
 - Mathematics
 - Physics
 - Chemistry
 - English
```

**Self-check questions:**
- Why are the keys now in alphabetical order?
- What is the type of `json_output`?
- What is the type of `python_data`?

---

### Exercise 2 — RegEx Text Search

**Objective:** Use RegEx to extract and validate data from text.

**Scenario:** You have a block of contact information. Extract all email addresses.

```python
import re

contact_info = """
Name: Alice Johnson
Email: alice.johnson@example.com
Phone: 080-1234-5678

Name: Bob Smith
Email: bob.smith@company.org
Phone: 091-9876-5432

Name: Carol Davis
Email: carol@mydomain.co.uk
Phone: 070-5555-1234
"""

# Find all email addresses
emails = re.findall(r"[\w\.\-]+@[\w\.\-]+\.\w+", contact_info)
print("Found emails:")
for email in emails:
    print(" -", email)
```

**Expected Output:**
```
Found emails:
 - alice.johnson@example.com
 - bob.smith@company.org
 - carol@mydomain.co.uk
```

**Pattern Breakdown:**
- `[\w\.\-]+` — one or more word chars, dots, or hyphens (the username part)
- `@` — literal @ symbol
- `[\w\.\-]+` — domain name
- `\.` — literal dot
- `\w+` — top-level domain (com, org, uk, etc.)

**Optional challenge:** Modify the pattern to also extract all phone numbers.

---

### Exercise 3 — Error Handling in a Calculator

**Objective:** Build a division calculator that handles errors gracefully.

**Scenario:** Build a function that divides two numbers and handles all possible errors.

```python
def safe_divide(a, b):
    try:
        a = float(a)
        b = float(b)
        result = a / b
    except ValueError:
        print("Error: Both inputs must be numbers!")
        return None
    except ZeroDivisionError:
        print("Error: Cannot divide by zero!")
        return None
    else:
        print(f"{a} ÷ {b} = {result:.4f}")
        return result
    finally:
        print("--- calculation attempted ---")

# Test all scenarios
print("Test 1:")
safe_divide(10, 3)

print("\nTest 2:")
safe_divide(10, 0)

print("\nTest 3:")
safe_divide(10, "abc")
```

**Expected Output:**
```
Test 1:
10.0 ÷ 3.0 = 3.3333
--- calculation attempted ---

Test 2:
Error: Cannot divide by zero!
--- calculation attempted ---

Test 3:
Error: Both inputs must be numbers!
--- calculation attempted ---
```

**Self-check questions:**
- When does `else` run?
- When does `finally` run?
- What would happen if you removed `finally`?

---

### Exercise 4 — Beautiful Report with F-Strings

**Objective:** Format a sales report using f-strings.

**Scenario:** You have raw sales data. Display it as a professional report.

```python
# Sales data
products = [
    {"name": "Laptop", "qty": 12, "price": 850.00},
    {"name": "Mouse", "qty": 150, "price": 25.50},
    {"name": "Keyboard", "qty": 75, "price": 45.00},
    {"name": "Monitor", "qty": 30, "price": 320.00},
]

# Print header
print(f"{'PRODUCT':<15} {'QTY':>6} {'UNIT PRICE':>12} {'TOTAL':>12}")
print("-" * 48)

# Print rows
grand_total = 0
for product in products:
    total = product["qty"] * product["price"]
    grand_total += total
    print(f"{product['name']:<15} {product['qty']:>6} {product['price']:>12,.2f} {total:>12,.2f}")

# Print footer
print("-" * 48)
print(f"{'GRAND TOTAL':<24} {grand_total:>24,.2f}")
print(f"\nAverage sale value: ${grand_total / len(products):,.2f}")
```

**Expected Output:**
```
PRODUCT          QTY   UNIT PRICE        TOTAL
------------------------------------------------
Laptop            12       850.00    10,200.00
Mouse            150        25.50     3,825.00
Keyboard          75        45.00     3,375.00
Monitor           30       320.00     9,600.00
------------------------------------------------
GRAND TOTAL                             27,000.00

Average sale value: $6,750.00
```

---

## Mini Project — Student Report Card Generator

### Overview

Build a complete student report card system that uses JSON for data storage, RegEx for validation, error handling for robustness, and f-strings for beautiful output.

### Stage 1 — Setup the Data Structure

```python
import json
import re

# Our student database (as JSON-ready dictionaries)
students = [
    {
        "id": "STU001",
        "name": "Adaeze Okonkwo",
        "email": "adaeze@school.edu",
        "scores": {"Math": 87, "English": 92, "Science": 78, "History": 85, "Art": 94}
    },
    {
        "id": "STU002",
        "name": "Emeka Nwosu",
        "email": "emeka@school.edu",
        "scores": {"Math": 65, "English": 70, "Science": 88, "History": 55, "Art": 72}
    },
    {
        "id": "STU003",
        "name": "Blessing Adeyemi",
        "email": "blessing@school.edu",
        "scores": {"Math": 95, "English": 88, "Science": 91, "History": 97, "Art": 83}
    }
]

print("Data loaded successfully!")
print(f"Total students: {len(students)}")
```

**Expected Output:**
```
Data loaded successfully!
Total students: 3
```

---

### Stage 2 — Email Validation with RegEx

```python
def validate_email(email):
    """Check if an email address is valid using RegEx."""
    pattern = r"^[\w\.\-]+@[\w\-]+\.[a-z]{2,4}$"
    return bool(re.match(pattern, email))

# Validate all student emails
print("\n--- Email Validation ---")
for student in students:
    email = student["email"]
    is_valid = validate_email(email)
    status = "✓ Valid" if is_valid else "✗ Invalid"
    print(f"{student['name']:<20} {email:<30} {status}")

# Test with a bad email
bad_email = "not-an-email"
print(f"\nTesting bad email '{bad_email}': {'✓ Valid' if validate_email(bad_email) else '✗ Invalid'}")
```

**Expected Output:**
```
--- Email Validation ---
Adaeze Okonkwo       adaeze@school.edu              ✓ Valid
Emeka Nwosu          emeka@school.edu               ✓ Valid
Blessing Adeyemi     blessing@school.edu            ✓ Valid

Testing bad email 'not-an-email': ✗ Invalid
```

---

### Stage 3 — Grade Calculation with Error Handling

```python
def calculate_grade(average):
    """Convert numeric average to letter grade."""
    try:
        average = float(average)
        if average < 0 or average > 100:
            raise ValueError("Average must be between 0 and 100")
        if average >= 90:
            return "A+"
        elif average >= 80:
            return "A"
        elif average >= 70:
            return "B"
        elif average >= 60:
            return "C"
        elif average >= 50:
            return "D"
        else:
            return "F"
    except ValueError as e:
        print(f"Grade Error: {e}")
        return "N/A"
    except TypeError:
        print("Grade Error: Invalid input type")
        return "N/A"

def get_student_average(student):
    """Calculate a student's average score safely."""
    try:
        scores = list(student["scores"].values())
        if not scores:
            raise ValueError("No scores found!")
        return sum(scores) / len(scores)
    except KeyError:
        print(f"Error: Student {student.get('name', 'Unknown')} has no scores!")
        return 0
    except Exception as e:
        print(f"Unexpected error: {e}")
        return 0

# Test error handling
print("\n--- Grade Calculation Tests ---")
print(f"Score 95 → Grade: {calculate_grade(95)}")
print(f"Score 72 → Grade: {calculate_grade(72)}")
print(f"Score 101 → Grade: {calculate_grade(101)}")   # Error case
print(f"Score 'abc' → Grade: {calculate_grade('abc')}")  # Error case
```

**Expected Output:**
```
--- Grade Calculation Tests ---
Score 95 → Grade: A+
Score 72 → Grade: B
Grade Error: Average must be between 0 and 100
Score 101 → Grade: N/A
Grade Error: Invalid input type
Score 'abc' → Grade: N/A
```

---

### Stage 4 — Generate and Display Report Cards

```python
def generate_report_card(student):
    """Generate a formatted report card for one student."""
    average = get_student_average(student)
    grade = calculate_grade(average)
    
    # Header
    print("=" * 55)
    print(f"{'STUDENT REPORT CARD':^55}")
    print("=" * 55)
    print(f"  Name:    {student['name']}")
    print(f"  ID:      {student['id']}")
    print(f"  Email:   {student['email']}")
    print("-" * 55)
    print(f"  {'SUBJECT':<20} {'SCORE':>8} {'STATUS':>15}")
    print("-" * 55)
    
    for subject, score in student["scores"].items():
        status = "Pass" if score >= 50 else "Fail"
        bar = "█" * (score // 10) + "░" * (10 - score // 10)
        print(f"  {subject:<20} {score:>8}   {bar}  {status}")
    
    print("-" * 55)
    print(f"  {'AVERAGE':<20} {average:>8.1f}")
    print(f"  {'FINAL GRADE':<20} {'':>8}{grade:>8}")
    print("=" * 55)
    print()

# Generate reports for all students
print("\n" + "="*55)
print(f"{'GENERATING ALL REPORT CARDS':^55}")
print("="*55 + "\n")

for student in students:
    generate_report_card(student)
```

**Expected Output (for Adaeze):**
```
=======================================================
                  STUDENT REPORT CARD                  
=======================================================
  Name:    Adaeze Okonkwo
  ID:      STU001
  Email:   adaeze@school.edu
-------------------------------------------------------
  SUBJECT              SCORE          STATUS
-------------------------------------------------------
  Math                    87   ████████░░  Pass
  English                 92   █████████░  Pass
  Science                 78   ███████░░░  Pass
  History                 85   ████████░░  Pass
  Art                     94   █████████░  Pass
-------------------------------------------------------
  AVERAGE                 87.2
  FINAL GRADE                        A
=======================================================
```

---

### Stage 5 — Save Data as JSON

```python
def save_report_json(students):
    """Save all student data and computed grades to a JSON file."""
    report_data = []
    
    for student in students:
        average = get_student_average(student)
        grade = calculate_grade(average)
        
        report_data.append({
            "id": student["id"],
            "name": student["name"],
            "email": student["email"],
            "scores": student["scores"],
            "average": round(average, 2),
            "grade": grade,
            "email_valid": validate_email(student["email"])
        })
    
    # Convert to formatted JSON
    json_output = json.dumps(report_data, indent=4)
    
    print("\n--- Exported JSON Data ---")
    print(json_output)
    
    return json_output

# Save and display
json_data = save_report_json(students)
```

**The output will be a beautifully formatted JSON document with all student records.**

---

## Common Beginner Mistakes

### JSON Mistakes

**Mistake 1 — Confusing Python `True` with JSON `true`:**

```python
import json

# WRONG — Don't manually write JSON like this in Python
bad = '{"active": True}'    # This is NOT valid JSON!
# json.loads(bad)           # This will CRASH!

# RIGHT — Let Python convert it for you
data = {"active": True}
good = json.dumps(data)     # Python converts True to true automatically
print(good)                 # {"active": true}
```

**Mistake 2 — Using `json.load()` vs `json.loads()`:**
- `json.loads()` — loads from a **string** (the "s" = string)
- `json.load()` — loads from a **file object** (no "s")

If you pass a string to `json.load()` it will crash. Match the function to what you have.

---

### RegEx Mistakes

**Mistake 3 — Forgetting raw strings:**

```python
import re

# WRONG — \b is misinterpreted as backspace
result = re.search("\bcat\b", "my cat")

# RIGHT — Use raw string r"..."
result = re.search(r"\bcat\b", "my cat")
print(result)  # Match object
```

Always use `r"..."` for RegEx patterns containing backslashes!

**Mistake 4 — Not checking if the result is `None`:**

```python
import re

result = re.search("xyz", "hello world")   # No match

# WRONG — This will crash!
# print(result.group())   # AttributeError: 'NoneType' has no attribute 'group'

# RIGHT — Always check first!
if result:
    print(result.group())
else:
    print("No match found.")
```

---

### Try/Except Mistakes

**Mistake 5 — Catching too broadly and hiding real bugs:**

```python
# BAD — This hides ALL errors, including bugs you need to see!
try:
    result = do_complex_calculation()
except:
    pass   # Silent failure — you will never know what went wrong!

# BETTER — Be specific about what you are catching
try:
    result = do_complex_calculation()
except ValueError:
    print("Invalid value.")
except TypeError:
    print("Wrong type.")
```

**Mistake 6 — Using `try/except` as normal flow control:**

```python
# BAD — Don't use exceptions for normal situations
try:
    value = my_list[5]
except IndexError:
    value = None

# BETTER — Check first if possible
value = my_list[5] if len(my_list) > 5 else None
```

---

### F-String Mistakes

**Mistake 7 — Forgetting the `f` prefix:**

```python
name = "Alice"

# WRONG — Just a regular string, no substitution happens
txt = "Hello {name}"
print(txt)    # Hello {name}  ← NOT what you wanted!

# RIGHT
txt = f"Hello {name}"
print(txt)    # Hello Alice
```

**Mistake 8 — Incorrect modifier syntax:**

```python
price = 59.5

# WRONG — Missing the colon
# txt = f"{price.2f}"   # SyntaxError!

# RIGHT — Colon is required before the format spec
txt = f"{price:.2f}"
print(txt)   # 59.50
```

---

## Reflection Questions

1. You receive JSON data from a weather API. What function do you use to convert it to a Python dictionary? What type of Python object does it become?

2. You are searching a large text document for all words that start with a capital letter. Which RegEx pattern would work — `[A-Z]\w+` or `[a-z]\w+`? Why?

3. Without `try/except`, what happens when a Python program encounters a `ZeroDivisionError`?

4. What is the difference between the `except` block and the `else` block? In what situation does each one run?

5. What is the difference between `json.loads()` and `json.dumps()`? Which one gives you a Python dictionary?

6. You want to display the number `4523678.5` as `$4,523,678.50` using an f-string. Write the exact f-string that would produce this output.

7. Why should you almost always use raw strings (`r"..."`) when writing RegEx patterns? What can go wrong if you don't?

8. What is the purpose of PIP? What command would you use to install a package called `requests`?

9. If you have a `try` block with both `except` and `finally`, does `finally` run even when the `except` catches an error? Why is this useful?

10. You want to write a function that only accepts positive numbers and raises a `ValueError` if a negative number is passed. Write that function.

---

## Completion Checklist

Before moving to the next lesson, confirm you can do the following:

- [ ] Import the `json` module and use `json.loads()` to convert a JSON string to a Python dictionary
- [ ] Use `json.dumps()` to convert a Python dictionary to a JSON string
- [ ] Use `indent`, `sort_keys`, and `separators` parameters with `json.dumps()`
- [ ] Import the `re` module and use `re.search()`, `re.findall()`, `re.split()`, and `re.sub()`
- [ ] Understand and write basic metacharacters (`.`, `^`, `$`, `*`, `+`, `?`, `[]`)
- [ ] Use special sequences like `\d`, `\w`, `\s` in patterns with raw strings
- [ ] Use PIP from the command line to install, uninstall, and list packages
- [ ] Write a `try/except` block to handle errors without crashing
- [ ] Use multiple `except` clauses for different error types
- [ ] Use the `else` block (runs when no error) and `finally` block (always runs)
- [ ] Use `raise` to deliberately trigger an error with a custom message
- [ ] Create f-strings with variable placeholders
- [ ] Use format specifiers like `:.2f`, `:,`, `:.2%`, `:<`, `:>`, `:^`
- [ ] Perform operations and call functions inside f-string placeholders
- [ ] Use the `format()` method with positional and named arguments

---

## Lesson Summary

Congratulations on completing Lesson 18! Let's recap everything you have learned:

**JSON** is the universal text format for exchanging data between systems. Use `json.loads()` to convert JSON text into Python objects, and `json.dumps()` to convert Python objects into JSON text. Use `indent=4` for pretty formatting, `sort_keys=True` for alphabetical ordering.

**Regular Expressions** (RegEx) are pattern-matching tools for text. The `re` module provides `search()`, `findall()`, `split()`, and `sub()`. Metacharacters like `.`, `^`, `$`, `*`, `+`, and `[]` define patterns. Special sequences like `\d`, `\w`, `\s` match common categories. Always use raw strings `r"..."` with RegEx.

**PIP** is Python's package manager. Use `pip install package_name` in the terminal to install packages, `pip uninstall` to remove them, and `pip list` to see what's installed. Find packages at `https://pypi.org/`.

**Try/Except** lets your programs survive errors gracefully. The `try` block holds risky code. `except` handles specific errors. `else` runs when there is no error. `finally` always runs — perfect for cleanup. `raise` lets you deliberately trigger errors with custom messages.

**String Formatting** makes your output polished and professional. F-strings (the modern way) use `f"..."` with `{variable}` placeholders and powerful modifiers like `:.2f`, `:,`, `:.2%`. The older `format()` method uses `"{}".format(value)` and still works in all Python code.

These five tools — JSON, RegEx, PIP, error handling, and string formatting — form the backbone of professional Python development. Together they allow you to process real-world data, validate user input, extend Python's capabilities, build resilient applications, and display results in a clear, readable way.

---

*End of Lesson 18*
