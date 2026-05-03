---
render_with_liquid: false
title: "Lesson 08 – Python Strings"
nav_order: 8
---

# Lesson 08 – Python Strings

---

## Lesson Introduction

Welcome to one of the most exciting lessons in this Python course! In this lesson, you will learn everything about **strings** — the way Python works with text.

Almost every real-world program deals with text: names, messages, addresses, product descriptions, usernames, and so much more. When your Python program reads a user's name, displays a greeting, formats a receipt, or processes a form, it is working with strings. This makes understanding strings absolutely essential.

By the end of this lesson, you will be able to:

- Create strings using single and double quotes
- Store strings in variables and display them
- Write multiline strings that span several lines
- Access individual characters inside a string using their position number (index)
- Slice out portions of a string using start and end positions
- Use negative indexing to count from the end of a string
- Modify strings using built-in methods: `upper()`, `lower()`, `strip()`, `replace()`, `split()`
- Join (concatenate) two strings together using `+`
- Format strings using f-strings to insert variable values neatly inside text
- Use escape characters to include special symbols like `\n`, `\t`, `\\`, `\"` inside strings
- Check if a word or character exists inside a string using `in` and `not in`
- Use Python's full library of string methods including `find()`, `count()`, `startswith()`, `endswith()`, `join()`, `isdigit()`, `isalpha()`, and many more

---

## Prerequisite Concepts

Before diving in, let's briefly recap what you already know — these ideas will come up frequently:

**Variables** — A variable is a named container that holds a value. You learned about these in Lesson 04. For example:

```python
city = "Lagos"
```

Here, `city` is the variable name and `"Lagos"` is the string value stored inside it.

**`print()` function** — You already know how to display output using `print()`. We will use it constantly in this lesson.

**Data types** — You learned in Lesson 06 that Python has different types of data: integers (whole numbers), floats (decimal numbers), and strings (text). A string is the data type for text.

If any of these feel unfamiliar, please review Lessons 04–06 before continuing.

---

## Section 1 — What Is a String?

### Why do we need strings?

Computers are very good at working with numbers. But the real world is full of text — names, sentences, addresses, product names, error messages, and much more. Python uses a special data type called a **string** to store and work with text.

**Analogy:** Think of a string like a necklace made of beads. Each bead is one character (letter, number, space, or symbol). The whole necklace put together is your string.

### What is a string, exactly?

A **string** in Python is a sequence of characters (letters, digits, spaces, punctuation symbols) enclosed in either single quotes (`'`) or double quotes (`"`).

Both of the following are exactly the same:

```python
'Eko Atlantic'
"Eko Atlantic"
```

Python treats them identically. You choose whichever quote style is more convenient for your specific situation.

### Creating your first string

```python
print("Hello")
print('Hello')
```

**Expected output in browser:**
```
Hello
Hello
```

Both lines print exactly the same result. Python does not care whether you use single or double quotes, as long as you use the same type at both the opening and closing of the string.

---

### 1.1 – Quotes Inside Strings

Sometimes you need to include a quote character as part of the text itself. For example: *It's raining* — that apostrophe is inside the string.

**The rule:** Use a different quote type on the outside from the one inside the string.

```python
print("It's alright")          # single quote inside, double quotes outside
print("He is called 'Johnny'") # single quotes inside double quotes
print('He is called "Johnny"') # double quotes inside single quotes
```

**Expected output:**
```
It's alright
He is called 'Johnny'
He is called "Johnny"
```

> 💡 **Tip:** If your text contains an apostrophe (like *It's* or *Lagos's*), wrap the whole string in double quotes so there's no confusion.

---

### 1.2 – Assigning a String to a Variable

You can store a string inside a variable using the `=` sign:

```python
city = "Abuja"
print(city)
```

**Expected output:**
```
Abuja
```

Let's break this down line by line:
- `city` — this is the **variable name**. You can choose any name you like (as long as it follows Python naming rules).
- `=` — this is the **assignment operator**. It tells Python: "store the value on the right inside the variable on the left."
- `"Abuja"` — this is the **string value** being stored.
- `print(city)` — this tells Python to display whatever is stored in `city`.

---

### 1.3 – Multiline Strings

What if your text is too long for one line? Python lets you write strings that span multiple lines using **triple quotes** — either `"""` (three double quotes) or `'''` (three single quotes).

```python
address = """No. 14 Broad Street,
Lagos Island,
Lagos State,
Nigeria."""
print(address)
```

**Expected output:**
```
No. 14 Broad Street,
Lagos Island,
Lagos State,
Nigeria.
```

The line breaks in your code are preserved exactly as you typed them. This is very useful for:
- Long messages
- Email templates
- Multi-paragraph text
- Documentation strings inside functions

You can also use three single quotes:

```python
menu = '''Today's menu:
Jollof Rice - ₦1,500
Egusi Soup - ₦2,000
Fried Plantain - ₦500'''
print(menu)
```

**Expected output:**
```
Today's menu:
Jollof Rice - ₦1,500
Egusi Soup - ₦2,000
Fried Plantain - ₦500
```

> 🤔 **Thinking Prompt:** What happens if you forget to close the triple quotes? Try it and observe the error Python gives you.

---

## Section 2 — Strings Are Arrays (Indexed Characters)

### Why does this matter?

This is a very important concept. Python treats a string as an ordered list of characters. Each character has a position number called an **index**. This means you can access any individual character by referring to its index number.

**Real-world analogy:** Imagine you have the name "AMAKA" written on 5 separate cards, placed in a row. Each card has a number starting from 0. So the card with "A" is card 0, "M" is card 1, "A" is card 2, "K" is card 3, and "A" is card 4. This is exactly how Python indexes a string.

```
String:  A  M  A  K  A
Index:   0  1  2  3  4
```

**Important:** In Python, counting always starts from **0**, not 1. The first character is at index 0.

### Accessing a character by index

You use square brackets `[]` after the variable name, with the index number inside:

```python
name = "AMAKA"
print(name[0])   # first character
print(name[1])   # second character
print(name[4])   # fifth (last) character
```

**Expected output:**
```
A
M
A
```

Let's trace through each line:
- `name[0]` → looks at position 0 → finds `'A'` → prints `A`
- `name[1]` → looks at position 1 → finds `'M'` → prints `M`
- `name[4]` → looks at position 4 → finds `'A'` → prints `A`

### Another example with a Nigerian phrase

```python
greeting = "Ekabo"
print(greeting[0])  # E
print(greeting[2])  # a
```

**Expected output:**
```
E
a
```

> 🤔 **Thinking Prompt:** What happens if you try `greeting[10]` when the string only has 5 characters? Try it. Python will raise an `IndexError`. This tells you the index is out of range (doesn't exist).

---

### 2.1 – String Length with `len()`

The `len()` function counts the total number of characters in a string and returns that number. Spaces count too!

```python
food = "Jollof Rice"
print(len(food))
```

**Expected output:**
```
11
```

Why 11? Let's count: `J-o-l-l-o-f- -R-i-c-e` = 11 characters, including the space in the middle.

```python
name = "Babatunde Okonkwo"
print(len(name))
```

**Expected output:**
```
17
```

`len()` is incredibly useful in real programs. For example: checking if a password is at least 8 characters long, or verifying that a phone number has exactly 11 digits.

---

### 2.2 – Looping Through a String

Because a string is an ordered sequence of characters, you can use a `for` loop to visit each character one by one. (You will study `for` loops in detail in a later lesson, but here's a preview.)

```python
city = "KANO"
for letter in city:
    print(letter)
```

**Expected output:**
```
K
A
N
O
```

What happened here:
- The `for` loop picks up one character at a time from the string `"KANO"`
- Each time through the loop, the variable `letter` holds the current character
- `print(letter)` displays that character

This is useful for processing text character by character — for example, counting vowels or checking for specific letters.

---

### 2.3 – Checking if a Word Is IN a String

You can check whether a particular word, letter, or phrase exists inside a string using the `in` keyword. It returns `True` or `False`.

```python
message = "The best things in life are free!"
print("free" in message)
print("expensive" in message)
```

**Expected output:**
```
True
False
```

You can also use this in an `if` statement to make decisions:

```python
receipt = "Order: Suya, Malt, Puff Puff"
if "Suya" in receipt:
    print("Suya is on the receipt.")
```

**Expected output:**
```
Suya is on the receipt.
```

### Checking if a word is NOT in a string

Use `not in` to check whether something is **absent**:

```python
order = "Eba and Egusi Soup"
print("Semovita" not in order)
```

**Expected output:**
```
True
```

Because "Semovita" is not part of the string `"Eba and Egusi Soup"`, the result is `True` (it is indeed NOT there).

---

## Section 3 — Slicing Strings

### What is slicing?

Slicing means cutting out a specific portion of a string — like slicing a piece of suya from a full skewer. You tell Python where to start and where to stop, and it returns only that part of the string.

### The slice syntax

```
string_variable[start : end]
```

- `start` = the index where the slice begins (the character **at** this position IS included)
- `end` = the index where the slice stops (the character **at** this position is **NOT** included)

### Example: Basic slice

```python
name = "Babatunde"
print(name[0:4])
```

**Expected output:**
```
Baba
```

Let's trace this carefully:
```
B  a  b  a  t  u  n  d  e
0  1  2  3  4  5  6  7  8
```
- Start at index 0 → `B`
- End at index 4 → stop just before `t`
- So the result is `B`, `a`, `b`, `a` → `"Baba"`

### Another example

```python
city = "Lagos Island"
print(city[6:12])
```

**Expected output:**
```
Island
```

---

### 3.1 – Slicing from the Start (Omitting Start Index)

If you leave out the start index, Python assumes you want to start from the very beginning (index 0):

```python
food = "Jollof Rice"
print(food[:6])
```

**Expected output:**
```
Jollof
```

This is the same as writing `food[0:6]`.

---

### 3.2 – Slicing to the End (Omitting End Index)

If you leave out the end index, Python slices all the way to the last character:

```python
food = "Jollof Rice"
print(food[7:])
```

**Expected output:**
```
Rice
```

This is the same as writing `food[7:11]` (since the string has 11 characters, index 11 is just past the end).

---

### 3.3 – Negative Indexing

Python also lets you count from the **end** of the string using negative numbers. The last character is always at index `-1`, the second to last at `-2`, and so on.

```
B  a  b  a  t  u  n  d  e
-9 -8 -7 -6 -5 -4 -3 -2 -1
```

```python
name = "Babatunde"
print(name[-1])    # last character
print(name[-3])    # third from the end
```

**Expected output:**
```
e
d
```

You can also slice using negative indexes:

```python
name = "Babatunde"
print(name[-4:-1])
```

**Expected output:**
```
und
```

**Breakdown:**
- `-4` points to `u`
- `-1` points to `e`, but we stop just **before** it
- So we get `u`, `n`, `d` → `"und"`

> 🤔 **Thinking Prompt:** Try `name[-9:]` — what do you expect? What about `name[:-1]`?

---

### 3.4 – Slice Summary Table

| Syntax | What it does |
|--------|-------------|
| `s[2:5]` | Characters from index 2 up to (not including) 5 |
| `s[:5]` | Characters from the start up to (not including) 5 |
| `s[2:]` | Characters from index 2 to the end |
| `s[-3:-1]` | Third and second characters from the end |
| `s[:]` | The entire string (a copy) |

---

## Section 4 — Modifying Strings

### An important note first

In Python, **strings are immutable** — this means you cannot change a string after it is created. The string `"Lagos"` will always be `"Lagos"`. However, you can create a *new* string that is a modified version of the original and store it in the same (or a different) variable. Python provides many built-in **methods** for this purpose.

**What is a method?** A method is a function that belongs to a specific type of object. String methods are functions built into every string. You call them using the **dot notation**: `variable_name.method_name()`.

---

### 4.1 – `upper()` — Convert to Uppercase

The `upper()` method returns a new string where all letters have been converted to UPPERCASE.

```python
city = "lagos"
print(city.upper())
```

**Expected output:**
```
LAGOS
```

Nothing happened to the original variable `city` — it still contains `"lagos"`. The method returned a new string. To save the result, assign it:

```python
city = "lagos"
city_upper = city.upper()
print(city_upper)
```

**Real-world use:** Converting user names to uppercase before comparing, so that "amaka", "Amaka", and "AMAKA" are treated as the same name.

---

### 4.2 – `lower()` — Convert to Lowercase

The `lower()` method returns a new string where all letters are in lowercase:

```python
name = "CHUKWUEMEKA ONYEKACHI"
print(name.lower())
```

**Expected output:**
```
chukwuemeka onyekachi
```

**Real-world use:** Storing emails in lowercase so that "User@Gmail.com" and "user@gmail.com" match correctly.

---

### 4.3 – `strip()` — Remove Extra Whitespace

Whitespace is invisible space characters (spaces, tabs) at the beginning or end of a string. It often appears when users type input carelessly. The `strip()` method removes these automatically.

```python
name = "   Ngozi   "
print(name.strip())
```

**Expected output:**
```
Ngozi
```

Notice that the spaces around the word have been removed, but the letters themselves are untouched.

You can also use:
- `lstrip()` — removes whitespace from the **left** side only
- `rstrip()` — removes whitespace from the **right** side only

```python
name = "   Ngozi   "
print(name.lstrip())   # "Ngozi   "
print(name.rstrip())   # "   Ngozi"
```

**Real-world use:** Cleaning up form input data before saving it to a database.

---

### 4.4 – `replace()` — Replace Part of a String

The `replace()` method searches for a specific word or character and replaces it with something else. It returns a new string.

```python
slogan = "Lagos is the best city in Africa"
print(slogan.replace("Lagos", "Abuja"))
```

**Expected output:**
```
Abuja is the best city in Africa
```

Nothing was permanently changed — the original variable `slogan` still holds the original text. The method returned a modified copy.

Another example:

```python
order = "I want pounded yam and egusi soup"
updated = order.replace("pounded yam", "eba")
print(updated)
```

**Expected output:**
```
I want eba and egusi soup
```

---

### 4.5 – `split()` — Split a String into Parts

The `split()` method divides a string into multiple pieces and returns them as a **list** (a collection of items). You tell it what character to split on — the **separator**.

```python
states = "Lagos,Abuja,Kano,Ibadan,Enugu"
print(states.split(","))
```

**Expected output:**
```
['Lagos', 'Abuja', 'Kano', 'Ibadan', 'Enugu']
```

Python found each comma and used it as a cutting point. The result is a list of five strings.

By default (if you don't give a separator), `split()` splits on any whitespace:

```python
sentence = "Eko  o ni baje"
print(sentence.split())
```

**Expected output:**
```
['Eko', 'o', 'ni', 'baje']
```

**Real-world use:** Reading a CSV (comma-separated values) file, breaking up a full name into first name and last name, parsing command-line arguments.

---

## Section 5 — Concatenating Strings

### What is concatenation?

**Concatenation** means joining two or more strings together to create one longer string. Think of it like linking train carriages together. In Python, you use the `+` operator to concatenate strings.

```python
first = "Babatunde"
last = "Okonkwo"
full_name = first + " " + last
print(full_name)
```

**Expected output:**
```
Babatunde Okonkwo
```

Let's trace this:
- `first` contains `"Babatunde"`
- `" "` is a string containing just one space
- `last` contains `"Okonkwo"`
- `first + " " + last` joins all three → `"Babatunde Okonkwo"`

Notice that Python does not add a space automatically. You must include the space as a separate string `" "` between the name parts.

### Another concatenation example

```python
greeting = "Good morning"
name = "Mama Ngozi"
message = greeting + ", " + name + "!"
print(message)
```

**Expected output:**
```
Good morning, Mama Ngozi!
```

---

### 5.1 – You Cannot Concatenate a String and a Number Directly

This is one of the most common beginner mistakes. If you try to join a string and a number using `+`, Python will raise a `TypeError`.

```python
age = 25
# WRONG:
# print("My age is " + age)  # This will cause an error!

# CORRECT:
print("My age is " + str(age))
```

**Expected output:**
```
My age is 25
```

The `str()` function converts a number to a string so that it can be joined with other strings. You learned about this in the casting lesson!

---

## Section 6 — Formatting Strings (f-strings)

### Why do we need string formatting?

Imagine you want to print a personalised greeting like: *"Welcome, Adaeze! You have 3 new messages."* The name and number of messages will change depending on the user. Building this message using `+` (concatenation) is possible but awkward:

```python
name = "Adaeze"
messages = 3
print("Welcome, " + name + "! You have " + str(messages) + " new messages.")
```

This works but is clunky and easy to get wrong. Python offers a much cleaner solution: **f-strings** (formatted string literals).

### How f-strings work

An f-string is created by putting the letter `f` immediately before the opening quote. Inside the string, you can embed variable names or expressions inside **curly braces `{}`**. Python will automatically replace `{variable}` with the value of that variable.

```python
name = "Adaeze"
messages = 3
print(f"Welcome, {name}! You have {messages} new messages.")
```

**Expected output:**
```
Welcome, Adaeze! You have 3 new messages.
```

Clean, simple, and easy to read!

### More f-string examples

```python
food = "Jollof Rice"
price = 1500
print(f"Today's special: {food} costs ₦{price}.")
```

**Expected output:**
```
Today's special: Jollof Rice costs ₦1500.
```

---

### 6.1 – F-strings Can Do Arithmetic

You can put calculations directly inside the curly braces:

```python
quantity = 4
unit_price = 500
print(f"Total cost: ₦{quantity * unit_price}")
```

**Expected output:**
```
Total cost: ₦2000
```

Python evaluates the expression `quantity * unit_price` (which is `4 * 500 = 2000`) and inserts the result into the string.

---

### 6.2 – The Older `.format()` Method

Before f-strings were introduced in Python 3.6, programmers used the `.format()` method. You will still see this in older codebases, so it is important to recognise it.

```python
name = "Emeka"
age = 22
print("My name is {} and I am {} years old.".format(name, age))
```

**Expected output:**
```
My name is Emeka and I am 22 years old.
```

The `{}` are placeholders. Python replaces them in order with the values passed to `.format()`. F-strings are generally preferred in modern Python because they are more readable, but both approaches work correctly.

---

## Section 7 — Escape Characters

### What is an escape character?

Sometimes you need to include a character inside a string that Python would normally misinterpret. For example, how do you include a double quote inside a double-quoted string? Python would see the second `"` and think the string has ended.

The solution is to use **escape characters**. An escape character is a backslash `\` followed by a specific letter. The backslash tells Python: "the next character is special — treat it differently."

### The most important escape characters

| Escape Code | What it produces |
|-------------|-----------------|
| `\"` | A double quote mark |
| `\'` | A single quote (apostrophe) |
| `\\` | A literal backslash |
| `\n` | A new line (line break) |
| `\t` | A horizontal tab (indentation) |
| `\r` | Carriage return |

---

### 7.1 – `\"` — Include a Double Quote

```python
print("She said, \"Eko o ni baje!\"")
```

**Expected output:**
```
She said, "Eko o ni baje!"
```

The `\"` tells Python: this `"` is part of the text, not the end of the string.

---

### 7.2 – `\'` — Include an Apostrophe

```python
print('It\'s a beautiful day in Lagos.')
```

**Expected output:**
```
It's a beautiful day in Lagos.
```

(Alternatively, you could just use double quotes on the outside: `"It's a beautiful day in Lagos."` — and then no escape is needed.)

---

### 7.3 – `\\` — Include a Backslash

This is useful for file paths on Windows:

```python
print("File path: C:\\Users\\Babatunde\\Documents")
```

**Expected output:**
```
File path: C:\Users\Babatunde\Documents
```

Each `\\` produces a single `\` in the output.

---

### 7.4 – `\n` — New Line

```python
print("Name: Adaeze\nCity: Enugu\nCountry: Nigeria")
```

**Expected output:**
```
Name: Adaeze
City: Enugu
Country: Nigeria
```

The `\n` causes Python to move to a new line at that exact point.

---

### 7.5 – `\t` — Tab (Indent)

```python
print("Item\t\tPrice")
print("Suya\t\t₦500")
print("Puff Puff\t₦200")
```

**Expected output:**
```
Item		Price
Suya		₦500
Puff Puff	₦200
```

The `\t` inserts a tab space, which is useful for aligning text in columns.

---

## Section 8 — String Methods Reference

Python has a very rich library of string methods. You have already learned `upper()`, `lower()`, `strip()`, `replace()`, and `split()`. Here is a comprehensive tour of all the important ones.

### 8.1 – `capitalize()` — Capitalise the First Letter

```python
name = "ngozi adaeze"
print(name.capitalize())
```

**Expected output:**
```
Ngozi adaeze
```

Only the very first letter of the entire string is capitalised. All other letters become lowercase.

---

### 8.2 – `title()` — Capitalise the First Letter of Every Word

```python
name = "babatunde okonkwo abubakar"
print(name.title())
```

**Expected output:**
```
Babatunde Okonkwo Abubakar
```

This is very useful for formatting names and headings.

---

### 8.3 – `count()` — Count How Many Times a Word or Letter Appears

```python
sentence = "Jollof rice is the best rice in all of Africa"
print(sentence.count("rice"))
```

**Expected output:**
```
2
```

The word "rice" appears twice in the sentence, so `count()` returns `2`. This method is case-sensitive — "Rice" and "rice" are counted separately.

---

### 8.4 – `find()` — Find the Position of a Substring

`find()` searches for a word or character inside a string and returns the **index** (position number) where it first appears. If the word is not found, it returns `-1`.

```python
text = "My name is Amaka Obi"
print(text.find("Amaka"))
print(text.find("Tunde"))
```

**Expected output:**
```
11
-1
```

`"Amaka"` starts at index 11. `"Tunde"` is not in the string, so `-1` is returned.

---

### 8.5 – `index()` — Like `find()` but Raises an Error if Not Found

`index()` works like `find()` but instead of returning `-1` when the word is not found, it raises a `ValueError` error. Use `find()` when you're not sure if the word exists; use `index()` when you are sure it exists.

```python
text = "I love suya"
print(text.index("suya"))
```

**Expected output:**
```
7
```

---

### 8.6 – `startswith()` and `endswith()` — Check the Start or End

```python
email = "adaeze@gmail.com"
print(email.startswith("adaeze"))   # True
print(email.endswith(".com"))        # True
print(email.endswith(".ng"))         # False
```

**Expected output:**
```
True
True
False
```

These are incredibly useful for validating data — for example, checking if an email address ends with `.com` or `.ng`.

---

### 8.7 – `isdigit()` — Check if All Characters Are Numbers

```python
phone = "08012345678"
print(phone.isdigit())

code = "A12B"
print(code.isdigit())
```

**Expected output:**
```
True
False
```

Returns `True` only if every character in the string is a digit (0–9). Very useful for validating phone numbers or ID numbers.

---

### 8.8 – `isalpha()` — Check if All Characters Are Letters

```python
name = "Babatunde"
print(name.isalpha())    # True (only letters)

mixed = "Lagos123"
print(mixed.isalpha())   # False (contains digits)
```

**Expected output:**
```
True
False
```

---

### 8.9 – `isalnum()` — Check if All Characters Are Letters or Numbers

```python
username = "user123"
print(username.isalnum())   # True

with_space = "user 123"
print(with_space.isalnum()) # False (contains a space)
```

**Expected output:**
```
True
False
```

---

### 8.10 – `isspace()` — Check if the String is Only Spaces

```python
blank = "   "
print(blank.isspace())   # True

not_blank = "  a  "
print(not_blank.isspace())  # False
```

**Expected output:**
```
True
False
```

---

### 8.11 – `join()` — Join a List of Strings into One String

`join()` is the opposite of `split()`. It takes a **list** of strings and joins them together into one string, with a separator of your choice placed between each item.

```python
states = ["Lagos", "Abuja", "Kano", "Enugu"]
result = ", ".join(states)
print(result)
```

**Expected output:**
```
Lagos, Abuja, Kano, Enugu
```

The string `", "` is the separator — it is placed between each item from the list.

Another example using a hyphen:

```python
parts = ["08", "01", "234", "5678"]
phone = "-".join(parts)
print(phone)
```

**Expected output:**
```
08-01-234-5678
```

---

### 8.12 – `zfill()` — Pad a String with Zeros

`zfill()` fills the left side of a string with zeros until it reaches the specified total length:

```python
number = "7"
print(number.zfill(4))
```

**Expected output:**
```
0007
```

Useful when you need IDs or codes with a fixed number of digits — like student ID: `"0042"`.

---

### 8.13 – `center()`, `ljust()`, `rjust()` — Align Text

These methods add padding (spaces) to align text within a given width.

```python
name = "Amaka"
print(name.center(15))   # Centres text in 15 characters
print(name.ljust(15))    # Aligns to the left
print(name.rjust(15))    # Aligns to the right
```

**Expected output:**
```
     Amaka     
Amaka          
          Amaka
```

---

### 8.14 – `swapcase()` — Swap Upper and Lower Case

```python
text = "Lagos Is GREAT"
print(text.swapcase())
```

**Expected output:**
```
lAGOS iS great
```

Every uppercase letter becomes lowercase and vice versa.

---

### Complete String Methods Quick Reference

| Method | What it does |
|--------|-------------|
| `upper()` | All letters UPPERCASE |
| `lower()` | All letters lowercase |
| `capitalize()` | First letter of string capitalised |
| `title()` | First letter of every word capitalised |
| `strip()` | Remove whitespace from both ends |
| `lstrip()` | Remove whitespace from left only |
| `rstrip()` | Remove whitespace from right only |
| `replace(old, new)` | Replace all occurrences of `old` with `new` |
| `split(sep)` | Split into a list using `sep` as the separator |
| `join(list)` | Join list items into one string |
| `find(sub)` | Return index of first occurrence (or -1) |
| `index(sub)` | Return index of first occurrence (error if not found) |
| `count(sub)` | Count how many times `sub` appears |
| `startswith(sub)` | True if string starts with `sub` |
| `endswith(sub)` | True if string ends with `sub` |
| `isdigit()` | True if all characters are digits |
| `isalpha()` | True if all characters are letters |
| `isalnum()` | True if all characters are letters or digits |
| `isspace()` | True if all characters are whitespace |
| `zfill(width)` | Pad with zeros on the left |
| `center(width)` | Centre the string in a field of given width |
| `ljust(width)` | Left-align in a field of given width |
| `rjust(width)` | Right-align in a field of given width |
| `swapcase()` | Swap upper and lower case letters |

---

## Section 9 — Guided Practice Exercises

### Exercise 1 — Student Name Formatter

**Objective:** Use string methods to clean and format a student's name properly.

**Scenario:** A school system receives student name input that may have inconsistent capitalisation and extra spaces. You need to clean it up.

**Steps:**

1. Store the messy name in a variable
2. Use `strip()` to remove extra whitespace
3. Use `title()` to capitalise each word properly
4. Print the cleaned name
5. Print the length of the cleaned name
6. Print just the first name (assume first name ends before the first space — hint: use `split()`)

**Starter code:**

```python
raw_name = "  chioma adannaya okonkwo  "

# Step 1: Strip whitespace
clean_name = raw_name.strip()

# Step 2: Title case
formatted_name = clean_name.title()

# Step 3: Print the formatted name
print(formatted_name)

# Step 4: Print its length
print(len(formatted_name))

# Step 5: Split and get first name
parts = formatted_name.split()
first_name = parts[0]
print("First name:", first_name)
```

**Expected output:**
```
Chioma Adannaya Okonkwo
23
First name: Chioma
```

**Self-check questions:**
- Why did we `strip()` before `title()`? Does the order matter?
- What would `parts[2]` give you?
- What happens if you call `split()` without any argument?

---

### Exercise 2 — Receipt Generator

**Objective:** Use f-strings and string concatenation to generate a formatted receipt.

**Scenario:** Mama Ngozi's shop in Yaba Market needs a Python program to print a simple receipt.

**Steps:**

1. Store three items, their quantities, and unit prices in variables
2. Calculate the total for each item
3. Calculate the overall total
4. Use f-strings to print a formatted receipt

```python
item1 = "Garri"
qty1 = 2
price1 = 800

item2 = "Palm Oil"
qty2 = 1
price2 = 1200

item3 = "Stockfish"
qty3 = 3
price3 = 600

total1 = qty1 * price1
total2 = qty2 * price2
total3 = qty3 * price3
grand_total = total1 + total2 + total3

print("=" * 30)
print("MAMA NGOZI'S SHOP - YABA")
print("=" * 30)
print(f"{item1:<15} x{qty1}  ₦{total1}")
print(f"{item2:<15} x{qty2}  ₦{total2}")
print(f"{item3:<15} x{qty3}  ₦{total3}")
print("-" * 30)
print(f"{'TOTAL':<15}      ₦{grand_total}")
print("=" * 30)
```

**Expected output:**
```
==============================
MAMA NGOZI'S SHOP - YABA
==============================
Garri           x2  ₦1600
Palm Oil        x1  ₦1200
Stockfish       x3  ₦1800
------------------------------
TOTAL                ₦4600
==============================
```

> 💡 **New concept in this exercise:** `f"{item1:<15}"` means "print `item1` in a space that is 15 characters wide, aligned to the LEFT". This is a formatting shortcut inside f-strings that helps create neat columns. The `*` operator used with a string (like `"=" * 30`) repeats the string 30 times.

**Self-check questions:**
- What is the value of `grand_total`?
- What does `"=" * 30` produce?
- How would you change the receipt to show prices in full naira with kobo (decimals)?

---

### Exercise 3 — Phone Number Validator

**Objective:** Use string methods to validate a Nigerian phone number.

**Scenario:** A registration form collects phone numbers. You need to check whether the input looks like a valid Nigerian number: starts with `"0"`, contains only digits, and is exactly 11 characters long.

```python
phone = "08012345678"

# Validation checks
correct_length = len(phone) == 11
starts_correctly = phone.startswith("0")
only_digits = phone.isdigit()

if correct_length and starts_correctly and only_digits:
    print(f"✓ '{phone}' is a valid Nigerian phone number.")
else:
    print(f"✗ '{phone}' is NOT a valid phone number.")
    if not correct_length:
        print(f"  → It has {len(phone)} digits. It should have 11.")
    if not starts_correctly:
        print("  → It should start with 0.")
    if not only_digits:
        print("  → It should contain only digits.")
```

**Expected output (valid number):**
```
✓ '08012345678' is a valid Nigerian phone number.
```

Try changing `phone` to `"0801234"` and run again:

```
✗ '0801234' is NOT a valid phone number.
  → It has 7 digits. It should have 11.
```

**Self-check questions:**
- What does `and` mean when combining conditions?
- What happens if the phone number contains a hyphen like `"0801-234-5678"`?

---

## Section 10 — Mini Project: Student Profile Generator

**Project description:** Build a Python program that generates a neat, formatted student profile card. This project combines everything you have learned in this lesson.

**Skills covered:** String creation, variables, `upper()`, `title()`, `strip()`, f-strings, `len()`, `replace()`, slicing, escape characters.

### Stage 1 — Store Raw Data

```python
# Raw student data (as it might come from a form)
raw_full_name = "  adaeze chioma obi  "
raw_email = "ADAEZE.OBI@UNILAG.EDU.NG"
raw_phone = "08054321987"
state_of_origin = "Anambra"
level = 200
gpa = 4.52
department = "Computer Science"
```

**Milestone checkpoint:** At this point you should have 7 variables with raw data. Nothing is printed yet.

### Stage 2 — Clean and Format the Data

```python
# Clean and format
full_name = raw_full_name.strip().title()       # "Adaeze Chioma Obi"
email = raw_email.lower()                       # "adaeze.obi@unilag.edu.ng"
first_name = full_name.split()[0]              # "Adaeze"
initials = full_name[0] + full_name.split()[1][0] + full_name.split()[2][0]  # "ACO"
student_id = "CSC" + raw_phone[-4:].zfill(6)  # "CSC001987"
```

**Milestone checkpoint:** Print each cleaned variable to verify it looks correct before moving on.

### Stage 3 — Generate the Profile Card

```python
separator = "=" * 45

print(separator)
print("       UNIVERSITY OF LAGOS")
print("       STUDENT PROFILE CARD")
print(separator)
print(f"  Full Name    : {full_name}")
print(f"  Student ID   : {student_id}")
print(f"  Initials     : {initials}")
print(f"  Department   : {department}")
print(f"  Level        : {level}L")
print(f"  State        : {state_of_origin}")
print(f"  Email        : {email}")
print(f"  Phone        : {raw_phone}")
print(f"  GPA          : {gpa}")
print(separator)
print(f"  Welcome, {first_name}! Keep up the great work.")
print(separator)
```

**Expected final output:**
```
=============================================
       UNIVERSITY OF LAGOS
       STUDENT PROFILE CARD
=============================================
  Full Name    : Adaeze Chioma Obi
  Student ID   : CSC001987
  Initials     : ACO
  Department   : Computer Science
  Level        : 200L
  State        : Anambra
  Email        : adaeze.obi@unilag.edu.ng
  Phone        : 08054321987
  GPA          : 4.52
=============================================
  Welcome, Adaeze! Keep up the great work.
=============================================
```

### Stage 4 — Reflection Questions

1. How did slicing help extract the last 4 digits of the phone number?
2. Why did we use `.lower()` on the email address?
3. What does `full_name.split()[1][0]` do exactly? Break it down step by step.
4. How would you modify the program to display the GPA as a percentage instead?

### Optional Extension Challenge

- Add a check: if GPA is above 4.5, add the line `"  Status: FIRST CLASS DISTINCTION"` to the card.
- Add the student's year of admission by subtracting the level from the current year.
- Use `replace()` to mask part of the phone number for privacy: show `"0805***1987"`.

---

## Section 11 — Common Beginner Mistakes

### Mistake 1 — Mismatched Quotes

**Wrong:**
```python
name = "Adaeze'   # Error! Started with double quote, ended with single
```

**Correct:**
```python
name = "Adaeze"
# OR
name = 'Adaeze'
```

Always use the **same** quote type at both ends.

---

### Mistake 2 — Off-By-One Indexing

**Wrong thinking:** "The first character is at index 1."

**Correct:** The first character is ALWAYS at index **0** in Python.

```python
name = "Kola"
print(name[0])  # Correct: K
print(name[1])  # This is the SECOND character: o
```

---

### Mistake 3 — Forgetting the End Index is Exclusive

When slicing `[2:5]`, you get characters at index 2, 3, 4 — but **NOT** 5.

```python
text = "Lagos"
print(text[1:4])  # 'ago' — NOT 'agos'
```

---

### Mistake 4 — Trying to Concatenate a String and a Number

**Wrong:**
```python
age = 25
print("I am " + age + " years old")   # TypeError!
```

**Correct:**
```python
age = 25
print("I am " + str(age) + " years old")   # Works!
# OR use an f-string:
print(f"I am {age} years old")             # Better!
```

---

### Mistake 5 — Thinking `replace()` Changes the Original String

**Wrong thinking:** "After `a.replace('H', 'J')`, the variable `a` now contains the modified string."

**Correct:** `replace()` returns a NEW string. The original is unchanged unless you reassign:

```python
a = "Hello"
a.replace("H", "J")  # Does nothing useful — result is discarded!
print(a)              # Still prints: Hello

# Correct way:
a = a.replace("H", "J")
print(a)              # Now prints: Jello
```

---

### Mistake 6 — Forgetting `f` Before an F-String

**Wrong:**
```python
name = "Emeka"
print("Hello, {name}")   # Prints: Hello, {name}  (literally)
```

**Correct:**
```python
name = "Emeka"
print(f"Hello, {name}")  # Prints: Hello, Emeka
```

Without the `f` prefix, Python treats `{name}` as plain text, not a variable reference.

---

### Mistake 7 — Case Sensitivity in `find()` and `in`

String operations are **case-sensitive**. `"Lagos"` and `"lagos"` are different strings!

```python
city = "Lagos"
print("lagos" in city)         # False! (lowercase 'l')
print("Lagos" in city)         # True
print(city.find("lagos"))      # -1 (not found)
```

To search case-insensitively, convert both strings to the same case first:

```python
print("lagos" in city.lower())   # True
```

---

## Reflection Questions

Think carefully about these before moving on:

1. In your own words, what is a Python string? How is it different from a number?
2. Why does Python start indexing at 0 instead of 1? Can you think of any real-world system that also counts from zero?
3. What is the difference between `find()` and `index()`? When would you choose one over the other?
4. Explain the difference between `split()` and `join()` — how are they opposites of each other?
5. You have a variable `phone = "080 123 45678"`. What steps would you take to clean it so it only contains digits and is ready for validation?
6. Why are f-strings considered better than concatenation using `+`? Can you think of a situation where `+` might still be useful?
7. What does "strings are immutable" mean? How does this affect how you use string methods?

---

## Completion Checklist

Before you move on to the next lesson, make sure you can confidently tick each item:

- [ ] I can create strings using single quotes, double quotes, and triple quotes
- [ ] I understand that Python starts counting character positions from index 0
- [ ] I can access an individual character using its index: `name[0]`
- [ ] I can find the length of a string using `len()`
- [ ] I can slice a string using `[start:end]` syntax
- [ ] I understand that the end index in a slice is NOT included
- [ ] I can use negative indexing to count from the end of a string
- [ ] I can convert a string to uppercase with `.upper()` and lowercase with `.lower()`
- [ ] I can remove whitespace using `.strip()`
- [ ] I can replace text using `.replace(old, new)`
- [ ] I can split a string into a list using `.split()`
- [ ] I can join strings using the `+` operator (and I know I must convert numbers with `str()` first)
- [ ] I can use f-strings to insert variable values into text
- [ ] I can use escape characters like `\n`, `\t`, `\\`, `\"`
- [ ] I can check if a word is inside a string using `in` and `not in`
- [ ] I know at least 5 additional string methods beyond the basics
- [ ] I completed all three guided exercises and the mini project

---

## Lesson Summary

In this lesson, you took a deep dive into Python strings — one of the most used data types in all of programming. Here is a concise recap:

**What a string is:** A string is an ordered sequence of characters enclosed in single, double, or triple quotes. Python treats each character in a string like an item in an indexed list, starting from position 0.

**Accessing characters:** Use square brackets with an index to access any character: `name[0]` gives the first character. Use negative indexes to count from the end: `name[-1]` gives the last character.

**Slicing:** Use `[start:end]` to extract a portion. The start index is included but the end index is not. Omit start to begin from position 0; omit end to go to the last character.

**Checking membership:** Use `in` to check if a substring exists (`"a" in "Amaka"` → `True`). Use `not in` for the opposite.

**Modifying strings:** Strings are immutable — methods return new strings rather than changing the original. Key methods: `upper()`, `lower()`, `strip()`, `replace()`, `split()`, `title()`, `capitalize()`, `count()`, `find()`, `startswith()`, `endswith()`, `join()`, `isdigit()`, `isalpha()`.

**Concatenation:** Join strings with `+`. Numbers must be converted with `str()` first.

**F-strings:** The cleanest way to embed variable values inside strings. Prefix the string with `f` and use `{variable_name}` inside. You can also put expressions inside the braces.

**Escape characters:** Use `\n` for newline, `\t` for tab, `\\` for backslash, `\"` for double quote inside a double-quoted string.

---

## Quick Reference Card

```python
# Creating strings
s = "Hello, Lagos!"
s = 'Hello, Lagos!'
s = """Multi
line"""

# Accessing characters
s[0]        # First character
s[-1]       # Last character
s[2:5]      # Characters from index 2 to 4
s[:4]       # First 4 characters
s[4:]       # Everything from index 4 onwards

# Key functions and methods
len(s)               # Number of characters
s.upper()            # ALL CAPS
s.lower()            # all lowercase
s.title()            # Title Case
s.strip()            # Remove leading/trailing spaces
s.replace("a", "b")  # Replace 'a' with 'b'
s.split(",")         # Split by comma → list
",".join(list)       # Join list items with commas
s.find("word")       # Index of first occurrence (-1 if absent)
s.count("a")         # Count occurrences
s.startswith("La")   # True/False
s.endswith(".ng")    # True/False
s.isdigit()          # True if all digits
s.isalpha()          # True if all letters

# Concatenation
full = "Babatunde" + " " + "Okonkwo"

# F-strings
name = "Emeka"
age = 30
msg = f"My name is {name} and I am {age} years old."

# Escape characters
"\n"   # New line
"\t"   # Tab
"\\"   # Backslash
"\""   # Double quote

# Check membership
"Abuja" in "Abuja is the capital"   # True
"Kano" not in "Lagos and Abuja"     # True
```

---

*End of Lesson 08 — Python Strings*

*Next Lesson: Lesson 09 — Python Booleans*
