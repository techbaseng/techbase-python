---
render_with_liquid: false
title: "Lesson 15 – Python Functions, Arguments, *args / **kwargs, and Scope"
nav_order: 15
---

# Lesson 15 – Python Functions, Arguments, \*args / \*\*kwargs, and Scope

---

## Lesson Introduction

Imagine you are baking a cake. Every time a customer orders one, you don't invent a brand-new recipe from scratch — you follow the **same recipe** each time, maybe swapping the flavour depending on what the customer wants. That recipe is a **function**.

In Python, a **function** is a reusable block of code that you write once and run as many times as you need, with different values each time if required. Functions are the single most important building block of any real program. Without them, you would copy and paste the same code over and over — messy, error-prone, and hard to fix.

This lesson covers **four closely connected topics** from the W3Schools Python tutorials, merged into one smooth, progressive lesson:

| Topic | What You Will Learn |
|---|---|
| **Functions** | How to create and call functions |
| **Arguments** | How to pass values into functions |
| **\*args and \*\*kwargs** | How to handle an unknown number of arguments |
| **Scope** | Where variables live and who can see them |

By the end of this lesson you will be able to write your own functions, pass data into them flexibly, and fully understand why variables sometimes seem to "disappear" — and why that is actually a good thing.

---

## Prerequisite Concepts

Before we begin, here are the concepts you must already understand. If any of these feel unfamiliar, take a few minutes to review them.

- **Variables** — storing a value in a name (e.g., `x = 5`)
- **`print()`** — displaying output in the terminal
- **Basic data types** — strings (`"hello"`), integers (`5`), floats (`3.14`), lists (`[1, 2, 3]`)
- **`if` / `else`** — making decisions in code
- **`for` loops** — repeating an action multiple times

No prior experience with functions or scope is needed.

---

## Part 1 – Python Functions

---

### 1.1 What Is a Function?

A **function** is a named, reusable block of code. You define it once, and then you can **call** (run) it as many times as you like from anywhere in your program.

**Real-world analogy:**  
Think of a function like a vending machine button. The machine (your function) is built once. Every time someone pushes the button (calls the function), the machine does the same job and delivers a result.

**Why do functions exist?**

- **DRY principle** — "Don't Repeat Yourself." Write the logic once, use it everywhere.
- **Readability** — Code broken into named functions is far easier to read and understand.
- **Maintenance** — If a rule changes, you fix it in one place instead of hunting through hundreds of lines.
- **Testing** — Small, focused functions are much easier to test and debug.

---

### 1.2 Defining a Function

In Python, you create a function using the `def` keyword.

**Syntax:**

```python
def function_name():
    # code that runs when the function is called
```

**Breaking down the syntax line by line:**

| Part | What It Means |
|---|---|
| `def` | Short for "define" — tells Python you are creating a function |
| `function_name` | The name you give your function (use lowercase and underscores) |
| `()` | Parentheses — this is where inputs (arguments) will go later |
| `:` | The colon signals the start of the function body |
| Indented block | All code indented underneath belongs to this function |

---

### 1.3 Your First Function

```python
def say_hello():
    print("Hello from inside a function!")
```

> **Important:** Defining a function does **not** run it. It just stores the recipe. Nothing appears on screen yet.

---

### 1.4 Calling a Function

To actually **run** the function, you **call** it by writing its name followed by parentheses:

```python
def say_hello():
    print("Hello from inside a function!")

say_hello()
```

**Expected output:**
```
Hello from inside a function!
```

You can call the same function multiple times:

```python
say_hello()
say_hello()
say_hello()
```

**Expected output:**
```
Hello from inside a function!
Hello from inside a function!
Hello from inside a function!
```

> 💡 **Think about it:** What happens if you never call the function? Try removing `say_hello()` from the code. What do you see?

---

### 1.5 Why Indentation Matters

Python uses **indentation** (spaces at the start of a line) to know which lines belong inside a function. This is not optional — it is the rule.

```python
def greet():
    print("Line 1 – inside the function")
    print("Line 2 – also inside the function")

print("Line 3 – OUTSIDE the function, runs immediately")
greet()
```

**Expected output:**
```
Line 3 – OUTSIDE the function, runs immediately
Line 1 – inside the function
Line 2 – also inside the function
```

> 🧠 **Notice:** `Line 3` runs first because it is outside the function and sits at the top level of the program. `Line 1` and `Line 2` only run when `greet()` is called.

---

### 1.6 Common Beginner Mistake — Forgetting the Call

```python
# ❌ WRONG – defines the function but never calls it
def show_score():
    print("Your score is 100")

# Nothing is printed because we forgot to call it!
```

**Corrected version:**

```python
# ✅ CORRECT
def show_score():
    print("Your score is 100")

show_score()  # This line actually runs the function
```

**Expected output:**
```
Your score is 100
```

---

### 1.7 Common Beginner Mistake — Indentation Error

```python
# ❌ WRONG – missing indentation inside function body
def greet():
print("Hello")  # IndentationError!
```

**Corrected version:**

```python
# ✅ CORRECT
def greet():
    print("Hello")  # 4 spaces of indentation
```

---

### 1.8 The `pass` Statement

Sometimes you want to create a function skeleton now and fill in the logic later. An empty function body causes a syntax error — use `pass` as a placeholder:

```python
def my_future_function():
    pass  # Does nothing, but Python is happy

my_future_function()  # No output, no error
```

This is common in professional development when planning out a project structure before writing all the logic.

---

## Part 2 – Arguments and Parameters

---

### 2.1 What Are Arguments?

So far our functions do the exact same thing every time. But real functions need to work with **different data** each time — like a calculator that can add any two numbers, not just 2 + 2.

**Parameters** and **arguments** let you pass information into a function.

**The difference:**

| Word | Meaning | Where |
|---|---|---|
| **Parameter** | The variable name listed in the function definition | Inside `def` parentheses |
| **Argument** | The actual value you pass when calling the function | Inside the call parentheses |

Think of a parameter as an empty slot, and an argument as the value you drop into that slot.

---

### 2.2 A Function with One Parameter

```python
def greet_person(name):       # 'name' is the parameter
    print("Hello, " + name + "!")

greet_person("Alice")         # "Alice" is the argument
greet_person("Bob")           # "Bob" is the argument
greet_person("Dr. Johnson")   # "Dr. Johnson" is the argument
```

**Expected output:**
```
Hello, Alice!
Hello, Bob!
Hello, Dr. Johnson!
```

> 🧠 **What changed?** The same function ran three times. Each time, the `name` parameter held a different value. The function code never changed — only the input did.

---

### 2.3 A Function with Multiple Parameters

You can define as many parameters as you need, separated by commas:

```python
def describe_student(first_name, subject, grade):
    print(first_name + " studies " + subject + " and scored " + str(grade) + "%.")

describe_student("Maria", "Maths", 94)
describe_student("James", "Biology", 78)
```

**Expected output:**
```
Maria studies Maths and scored 94%.
James studies Biology and scored 78%.
```

> **Note:** `str(grade)` converts the number `94` into the string `"94"` so it can be joined with the other strings using `+`. This is called **type conversion**.

---

### 2.4 Positional Arguments

When you pass arguments in order, Python matches them to parameters by **position**:

```python
def show_order(item, quantity, price):
    print(item + " × " + str(quantity) + " = £" + str(price))

show_order("Apples", 6, 3.00)
# item = "Apples", quantity = 6, price = 3.00
```

**Expected output:**
```
Apples × 6 = £3.0
```

> ⚠️ **Order matters!** If you mix up the order, you get incorrect results — or an error:

```python
show_order(6, "Apples", 3.00)   # quantity and item are swapped!
```

**Incorrect output:**
```
6 × Apples = £3.0
```

---

### 2.5 Keyword Arguments

You can also pass arguments using the **parameter name** so order does not matter:

```python
def show_order(item, quantity, price):
    print(item + " × " + str(quantity) + " = £" + str(price))

show_order(quantity=6, price=3.00, item="Apples")
```

**Expected output:**
```
Apples × 6 = £3.0
```

Using keyword arguments makes your code **self-documenting** — anyone reading it knows exactly what each value means.

---

### 2.6 Default Parameter Values

You can give a parameter a **default value**. If the caller does not provide that argument, the default is used automatically:

```python
def greet(name, language="English"):
    if language == "English":
        print("Hello, " + name + "!")
    elif language == "Spanish":
        print("Hola, " + name + "!")
    elif language == "French":
        print("Bonjour, " + name + "!")

greet("Alice")               # uses default: English
greet("Carlos", "Spanish")   # overrides default
greet("Marie", "French")     # overrides default
```

**Expected output:**
```
Hello, Alice!
Hola, Carlos!
Bonjour, Marie!
```

> 💡 **Rule:** Parameters with defaults must come **after** parameters without defaults in the function definition.

```python
# ❌ WRONG
def greet(language="English", name):   # SyntaxError
    pass

# ✅ CORRECT
def greet(name, language="English"):
    pass
```

---

### 2.7 Returning Values with `return`

So far our functions have printed things. But often you want a function to **calculate** a result and **send it back** so your program can use it elsewhere.

The `return` keyword sends a value back to wherever the function was called:

```python
def add(a, b):
    result = a + b
    return result

total = add(10, 25)
print("The total is:", total)
```

**Expected output:**
```
The total is: 35
```

**What happens line by line:**

1. `add(10, 25)` is called — `a = 10`, `b = 25`
2. Inside: `result = 10 + 25` → `result = 35`
3. `return result` sends `35` back to the caller
4. `total` receives the returned value `35`
5. `print(...)` displays it

> 🛑 **After `return`, the function stops.** Any code after `return` in the same function body will never run.

```python
def demo():
    return "I am returned"
    print("This line never runs!")  # unreachable code

value = demo()
print(value)
```

**Expected output:**
```
I am returned
```

---

### 2.8 Practical Example — Temperature Converter

```python
def celsius_to_fahrenheit(celsius):
    fahrenheit = (celsius * 9 / 5) + 32
    return fahrenheit

temp_c = 100
temp_f = celsius_to_fahrenheit(temp_c)
print(str(temp_c) + "°C = " + str(temp_f) + "°F")

print(str(0) + "°C = " + str(celsius_to_fahrenheit(0)) + "°F")
print(str(37) + "°C = " + str(celsius_to_fahrenheit(37)) + "°F")
```

**Expected output:**
```
100°C = 212.0°F
0°C = 32.0°F
37°C = 98.6°F
```

> 💡 **Real-world use:** Weather apps, scientific instruments, and cooking sites use this exact type of function. Write it once, use it everywhere.

---

### 2.9 Passing a List as an Argument

Any data type can be passed as an argument, including lists:

```python
def show_fruits(fruits):
    for fruit in fruits:
        print("🍎 " + fruit)

my_fruits = ["Apple", "Banana", "Mango", "Grape"]
show_fruits(my_fruits)
```

**Expected output:**
```
🍎 Apple
🍎 Banana
🍎 Mango
🍎 Grape
```

---

## Part 3 – \*args and \*\*kwargs

---

### 3.1 The Problem: What If You Don't Know How Many Arguments There Will Be?

Imagine writing a function that adds numbers. How many numbers should it accept? Two? Five? Twenty?

If you hard-code three parameters, a caller who wants to sum six numbers is stuck. Python solves this with **arbitrary arguments**.

---

### 3.2 \*args — Arbitrary Positional Arguments

Adding a single `*` before a parameter name tells Python: "collect all the extra positional arguments into a **tuple**."

By convention, the name used is `*args`, but any name after `*` works.

```python
def add_all(*numbers):
    total = 0
    for n in numbers:
        total = total + n
    return total

print(add_all(1, 2))
print(add_all(1, 2, 3, 4, 5))
print(add_all(10, 20, 30, 40, 50, 60))
```

**Expected output:**
```
3
15
210
```

**What is `numbers` here?** It is a **tuple** — an immutable, ordered collection of all the values passed in:

```python
def inspect_args(*items):
    print(type(items))   # <class 'tuple'>
    print(items)

inspect_args("cat", "dog", "fish")
```

**Expected output:**
```
<class 'tuple'>
('cat', 'dog', 'fish')
```

---

### 3.3 \*args With Other Parameters

`*args` can be combined with regular parameters. Regular parameters must come **before** `*args`:

```python
def show_menu(restaurant_name, *dishes):
    print("Restaurant: " + restaurant_name)
    print("Today's menu:")
    for dish in dishes:
        print("  - " + dish)

show_menu("La Piazza", "Pasta", "Pizza", "Tiramisu", "Risotto")
```

**Expected output:**
```
Restaurant: La Piazza
Today's menu:
  - Pasta
  - Pizza
  - Tiramisu
  - Risotto
```

> 🧠 **How it works:** `"La Piazza"` fills the `restaurant_name` parameter. Everything else — `"Pasta"`, `"Pizza"`, `"Tiramisu"`, `"Risotto"` — is collected into the `dishes` tuple.

---

### 3.4 \*\*kwargs — Arbitrary Keyword Arguments

`**kwargs` does the same thing as `*args`, but for **keyword arguments** (name=value pairs). The double `**` collects them into a **dictionary**.

By convention the name is `**kwargs` (keyword arguments), but you can use any name after `**`.

```python
def describe_person(**details):
    print("Person Profile:")
    for key, value in details.items():
        print("  " + key + ": " + str(value))

describe_person(name="Sarah", age=28, city="London", job="Engineer")
```

**Expected output:**
```
Person Profile:
  name: Sarah
  age: 28
  city: London
  job: Engineer
```

**What is `details` here?** It is a **dictionary**:

```python
def inspect_kwargs(**info):
    print(type(info))   # <class 'dict'>
    print(info)

inspect_kwargs(colour="blue", size=12)
```

**Expected output:**
```
<class 'dict'>
{'colour': 'blue', 'size': 12}
```

---

### 3.5 \*\*kwargs — Practical Example: Product Builder

```python
def create_product(**specs):
    print("=== New Product ===")
    for spec, value in specs.items():
        print(spec.capitalize() + ": " + str(value))
    print()

create_product(name="Laptop", brand="TechPro", ram="16GB", price=999.99)
create_product(name="Headphones", brand="SoundWave", colour="Black", wireless=True)
```

**Expected output:**
```
=== New Product ===
Name: Laptop
Brand: TechPro
Ram: 16GB
Price: 999.99

=== New Product ===
Name: Headphones
Brand: SoundWave
Colour: Black
Wireless: True
```

> 💡 **Real-world use:** Web frameworks like Flask and Django use `**kwargs` everywhere. When you create a database model or an HTML element with attributes, the framework accepts them as keyword arguments.

---

### 3.6 Combining Regular, \*args, and \*\*kwargs

You can use all three together in one function. The order **must** be:

```
def function(regular_params, *args, **kwargs):
```

```python
def full_order(table_number, *items, **extras):
    print("Table " + str(table_number) + " ordered:")
    for item in items:
        print("  - " + item)
    if extras:
        print("  Special requests:")
        for key, val in extras.items():
            print("    " + key + ": " + str(val))

full_order(7, "Pizza", "Salad", "Water", sauce="extra", gluten_free=True)
```

**Expected output:**
```
Table 7 ordered:
  - Pizza
  - Salad
  - Water
  Special requests:
    sauce: extra
    gluten_free: True
```

---

### 3.7 The \* and \*\* Unpacking Operators in Function Calls

The `*` and `**` can also be used when **calling** a function, to **unpack** a list or dictionary into separate arguments:

```python
def add(a, b, c):
    return a + b + c

numbers = [1, 2, 3]
print(add(*numbers))   # unpacks list into: add(1, 2, 3)
```

**Expected output:**
```
6
```

```python
def greet(name, language):
    print("Hello " + name + " in " + language)

settings = {"name": "Aiko", "language": "Japanese"}
greet(**settings)   # unpacks dict into: greet(name="Aiko", language="Japanese")
```

**Expected output:**
```
Hello Aiko in Japanese
```

---

### 3.8 Common Beginner Mistakes with \*args and \*\*kwargs

**Mistake 1 — Wrong order:**

```python
# ❌ WRONG – **kwargs before *args
def bad_func(**kwargs, *args):   # SyntaxError
    pass

# ✅ CORRECT – *args always before **kwargs
def good_func(*args, **kwargs):
    pass
```

**Mistake 2 — Treating \*args as a list (it's a tuple):**

```python
def my_func(*numbers):
    numbers.append(99)   # AttributeError! Tuples don't have append

# ✅ CORRECT – convert to list if you need to modify it
def my_func(*numbers):
    nums_list = list(numbers)
    nums_list.append(99)
    print(nums_list)

my_func(1, 2, 3)
```

**Expected output:**
```
[1, 2, 3, 99]
```

---

## Part 4 – Python Scope

---

### 4.1 What Is Scope?

**Scope** describes **where in your code a variable is visible and accessible**. Not every variable can be seen from every part of a program — and this is intentional.

**Why does scope exist?**  
Imagine a huge program with hundreds of functions. If every variable was visible everywhere, any function could accidentally overwrite another function's `total` or `count`. Scope creates **walls** between different parts of code, preventing accidental interference.

**Analogy:** Think of scope like rooms in a house. A lamp in your bedroom (local scope) only lights your bedroom. It does not light the kitchen. The main electricity supply (global scope) powers the entire house.

Python has **four levels of scope**, remembered with the acronym **LEGB**:

| Letter | Name | Where |
|---|---|---|
| **L** | Local | Inside the current function |
| **E** | Enclosing | Inside an outer function (for nested functions) |
| **G** | Global | At the top level of the file |
| **B** | Built-in | Python's built-in names (e.g., `print`, `len`, `range`) |

We will focus on Local and Global — the two you will encounter most.

---

### 4.2 Local Scope

A variable created **inside a function** is **local** — it only exists while the function is running, and it is invisible outside.

```python
def my_function():
    local_variable = "I only exist inside this function"
    print(local_variable)

my_function()
print(local_variable)   # NameError! local_variable doesn't exist here
```

**Expected output:**
```
I only exist inside this function
Traceback (most recent call last):
  ...
NameError: name 'local_variable' is not defined
```

> 🧠 **Why?** When `my_function()` finishes, Python destroys all local variables. They are temporary — like writing on a whiteboard that gets erased when the meeting ends.

---

### 4.3 Local Variables in Different Functions Don't Interfere

Each function has its **own private workspace**. Two functions can both use a variable called `x` without conflict:

```python
def function_a():
    x = 100
    print("Inside function_a, x =", x)

def function_b():
    x = 999
    print("Inside function_b, x =", x)

function_a()
function_b()
```

**Expected output:**
```
Inside function_a, x = 100
Inside function_b, x = 999
```

Both functions have their own `x`. They never interfere with each other. This is the power of local scope.

---

### 4.4 Global Scope

A variable created **outside all functions** is **global** — it is visible to all code in the file:

```python
greeting = "Good morning"   # global variable

def say_it():
    print(greeting)         # can READ the global variable

def shout_it():
    print(greeting.upper()) # can also READ it

say_it()
shout_it()
```

**Expected output:**
```
Good morning
GOOD MORNING
```

---

### 4.5 Can a Function Modify a Global Variable?

By default, **reading** a global variable inside a function is fine. But **modifying** it is blocked — Python creates a new local variable instead:

```python
counter = 0   # global

def increment():
    counter = counter + 1   # ❌ UnboundLocalError!

increment()
```

**Why the error?** Python sees `counter =` on the left side of `=` inside the function, assumes you mean a new **local** variable, then tries to read the (not-yet-created local) `counter` on the right side — and fails.

---

### 4.6 The `global` Keyword

To tell Python "I want to modify the actual global variable, not create a local one," use the `global` keyword:

```python
counter = 0   # global

def increment():
    global counter             # declare intent to use the global
    counter = counter + 1
    print("Counter:", counter)

increment()
increment()
increment()
print("Final counter:", counter)
```

**Expected output:**
```
Counter: 1
Counter: 2
Counter: 3
Final counter: 3
```

> ⚠️ **Use `global` sparingly.** Overusing `global` is considered bad practice because it makes code hard to trace and debug. The professional approach is to **pass values as arguments** and **return results** instead.

**Professional alternative to `global`:**

```python
# ❌ Using global (not ideal)
total = 0
def add_to_total(n):
    global total
    total += n

# ✅ Better approach – pass and return
def add_to_total(current_total, n):
    return current_total + n

total = 0
total = add_to_total(total, 5)
total = add_to_total(total, 10)
print(total)  # 15
```

---

### 4.7 Local Takes Priority Over Global

If a local variable and a global variable share the same name, the **local one wins inside the function**:

```python
name = "Global Name"

def show_name():
    name = "Local Name"   # this is a NEW local variable
    print(name)

show_name()
print(name)   # global variable unchanged
```

**Expected output:**
```
Local Name
Global Name
```

> 🧠 **Notice:** Assigning inside the function did NOT change the global `name`. The global is completely untouched.

---

### 4.8 The `nonlocal` Keyword (Bonus: Enclosing Scope)

When you have a function **inside another function** (a nested function), the inner function can access the outer function's variables as **enclosing scope**. To modify them, use `nonlocal`:

```python
def outer():
    message = "Hello from outer"

    def inner():
        nonlocal message
        message = "Modified by inner"
        print("Inner says:", message)

    inner()
    print("Outer says:", message)

outer()
```

**Expected output:**
```
Inner says: Modified by inner
Outer says: Modified by inner
```

> This is an advanced pattern. You will encounter it when learning about **closures** and **decorators** — but `nonlocal` follows exactly the same logic as `global`, just one level in.

---

### 4.9 Built-in Scope

Python has many **built-in** names that are always available — like `print`, `len`, `range`, `type`, `int`, `str`, `list`. These live in the **built-in scope**, the outermost layer:

```python
print(len("Hello"))   # 'len' and 'print' are built-in
print(type(42))       # 'type' is built-in
```

**Expected output:**
```
5
<class 'int'>
```

> ⚠️ **Never shadow built-in names!** Don't create variables called `list`, `print`, `input`, `id`, etc. — this overwrites the built-in and causes confusing errors.

```python
# ❌ WRONG – never do this
list = [1, 2, 3]       # You've now overwritten the built-in 'list'
print(list([1,2,3]))   # TypeError – list is now just a list object, not a function

# ✅ CORRECT – use a descriptive name
my_list = [1, 2, 3]
```

---

## Guided Practice Exercises

---

### Exercise 1 – Grading Function

**Objective:** Write a function that takes a student's score and returns a letter grade.

**Scenario:** A teacher needs a quick tool to convert any numeric score to a grade.

**Steps:**

1. Define a function called `get_grade` that accepts one parameter: `score`
2. Inside, use `if / elif / else` to determine the grade:
   - 90–100 → `"A"`
   - 80–89 → `"B"`
   - 70–79 → `"C"`
   - 60–69 → `"D"`
   - Below 60 → `"F"`
3. Return the grade letter
4. Call the function with at least five different scores and print each result

**Hint:** Use `return` to send the grade back, then `print()` outside the function.

**Solution:**

```python
def get_grade(score):
    if score >= 90:
        return "A"
    elif score >= 80:
        return "B"
    elif score >= 70:
        return "C"
    elif score >= 60:
        return "D"
    else:
        return "F"

scores = [95, 83, 72, 61, 45, 100, 59]
for s in scores:
    print("Score:", s, "→ Grade:", get_grade(s))
```

**Expected output:**
```
Score: 95 → Grade: A
Score: 83 → Grade: B
Score: 72 → Grade: C
Score: 61 → Grade: D
Score: 45 → Grade: F
Score: 100 → Grade: A
Score: 59 → Grade: F
```

**Self-check questions:**
- What grade does `get_grade(60)` return? Why?
- What happens if you pass `get_grade(105)`? What should you do to handle that?

---

### Exercise 2 – Shopping Bill with \*args

**Objective:** Use `*args` to calculate a total from any number of prices.

**Scenario:** A checkout system needs to add up a variable number of item prices.

```python
def calculate_bill(customer_name, *prices):
    total = sum(prices)
    print("Customer: " + customer_name)
    print("Items: " + str(len(prices)))
    print("Total: £" + str(round(total, 2)))
    print()

calculate_bill("Alice", 4.99, 1.49, 7.25)
calculate_bill("Bob", 12.99, 3.49, 8.00, 2.50, 1.99)
calculate_bill("Carol", 35.00)
```

**Expected output:**
```
Customer: Alice
Items: 3
Total: £13.73

Customer: Bob
Items: 5
Total: £28.97

Customer: Carol
Items: 1
Total: £35.0
```

**What-if challenge:** What happens if you call `calculate_bill("Dave")` with no prices? Try it. Is the result sensible? How would you handle an empty bill?

---

### Exercise 3 – User Profile with \*\*kwargs

**Objective:** Use `**kwargs` to build flexible user profiles.

```python
def create_profile(username, **attributes):
    print("=== Profile: " + username + " ===")
    for key, value in attributes.items():
        print("  " + key.replace("_", " ").title() + ": " + str(value))
    print()

create_profile("coder99", age=22, city="Berlin", language="Python", years_experience=3)
create_profile("data_queen", age=30, field="Data Science", tools=["pandas", "numpy", "sklearn"])
```

**Expected output:**
```
=== Profile: coder99 ===
  Age: 22
  City: Berlin
  Language: Python
  Years Experience: 3

=== Profile: data_queen ===
  Age: 30
  Field: Data Science
  Tools: ['pandas', 'numpy', 'sklearn']
```

---

### Exercise 4 – Scope Experiment

**Objective:** Understand what happens when local and global variables share a name.

```python
x = "I am global"

def test_local():
    x = "I am local"
    print("Inside function:", x)

test_local()
print("Outside function:", x)
```

**Expected output:**
```
Inside function: I am local
Outside function: I am global
```

**Questions:**
- Did the function change the global `x`? Why not?
- What would you add to the function to actually change the global `x`?

---

## Mini Project – Student Report Generator

This project combines functions, arguments, `*args`, `**kwargs`, and scope into one realistic application.

---

### Project Goal

Build a **Student Report Generator** that:
1. Accepts student data (name, scores for multiple subjects, personal notes)
2. Calculates the average score
3. Assigns a letter grade
4. Prints a formatted report

---

### Stage 1 – Helper Functions (Setup)

```python
def calculate_average(*scores):
    """Calculate the average of any number of scores."""
    if len(scores) == 0:
        return 0
    return round(sum(scores) / len(scores), 1)

def get_grade(average):
    """Convert an average score to a letter grade."""
    if average >= 90:
        return "A – Excellent"
    elif average >= 80:
        return "B – Good"
    elif average >= 70:
        return "C – Satisfactory"
    elif average >= 60:
        return "D – Needs Improvement"
    else:
        return "F – Unsatisfactory"

# Test Stage 1
avg = calculate_average(85, 90, 78, 92)
print("Average:", avg)
print("Grade:", get_grade(avg))
```

**Expected milestone output:**
```
Average: 86.2
Grade: B – Good
```

---

### Stage 2 – Report Builder (Core Logic)

```python
def generate_report(student_name, *scores, **subject_scores):
    """
    Generate a full student report.
    
    student_name  : the student's name (str)
    *scores       : optional raw scores as positional args
    **subject_scores : subject name = score pairs as keyword args
    """
    print("=" * 40)
    print("STUDENT REPORT")
    print("=" * 40)
    print("Name: " + student_name)
    print()

    # Show subject-by-subject breakdown if provided
    if subject_scores:
        print("Subject Scores:")
        all_scores = []
        for subject, score in subject_scores.items():
            print("  " + subject.capitalize() + ": " + str(score) + "%")
            all_scores.append(score)
        avg = calculate_average(*all_scores)

    # Fall back to raw positional scores
    elif scores:
        print("Scores: " + str(scores))
        avg = calculate_average(*scores)
    else:
        print("No scores provided.")
        avg = 0

    print()
    print("Average Score: " + str(avg) + "%")
    print("Final Grade:   " + get_grade(avg))
    print("=" * 40)
    print()

# Test Stage 2
generate_report("Emma Clarke",
                maths=88, science=92, english=75, history=84, art=97)

generate_report("Liam Patel",
                maths=65, science=70, english=60, history=55, art=72)
```

**Expected milestone output:**
```
========================================
STUDENT REPORT
========================================
Name: Emma Clarke

Subject Scores:
  Maths: 88%
  Science: 92%
  English: 75%
  History: 84%
  Art: 97%

Average Score: 87.2%
Final Grade:   B – Good
========================================

========================================
STUDENT REPORT
========================================
Name: Liam Patel

Subject Scores:
  Maths: 65%
  Science: 70%
  English: 60%
  History: 55%
  Art: 72%

Average Score: 64.4%
Final Grade:   D – Needs Improvement
========================================
```

---

### Stage 3 – Batch Reporting (Final Output)

```python
def print_class_summary(class_name, *student_reports):
    """Print a summary table for all students."""
    print()
    print("CLASS SUMMARY: " + class_name)
    print("-" * 40)
    for student in student_reports:
        name, avg = student
        print("  {:<20} {:.1f}%  {}".format(name, avg, get_grade(avg)[:1]))
    print("-" * 40)
    print()

# Full batch run
students = [
    ("Emma Clarke", 88, 92, 75, 84, 97),
    ("Liam Patel", 65, 70, 60, 55, 72),
    ("Sofia Nguyen", 95, 98, 91, 93, 96),
    ("Marcus Webb", 72, 68, 80, 74, 78),
]

summaries = []
for name, *scores in students:
    avg = calculate_average(*scores)
    summaries.append((name, avg))

print_class_summary("Year 10 Science Group", *summaries)
```

**Expected final output:**
```
CLASS SUMMARY: Year 10 Science Group
----------------------------------------
  Emma Clarke         87.2%  B
  Liam Patel          64.4%  D
  Sofia Nguyen        94.6%  A
  Marcus Webb         74.4%  C
----------------------------------------
```

**Reflection questions:**
- Where is `calculate_average` defined, and why can all functions call it?
- What scope does `class_name` belong to inside `print_class_summary`?
- How would you modify the project to also calculate and print the class average?

**Optional extensions:**
- Add a `pass_fail` field based on whether the average is ≥ 60
- Sort students from highest to lowest average before printing
- Allow the teacher to add a custom comment per student using `**kwargs`

---

## Common Beginner Mistakes — Full Summary

| Mistake | Example | Fix |
|---|---|---|
| Defining but not calling a function | `def greet(): print("Hi")` with no call | Add `greet()` after the definition |
| Wrong indentation | `def f():` then `print(...)` at column 0 | Indent the body with 4 spaces |
| Passing wrong number of arguments | `def add(a, b): ...` called as `add(1)` | Match the number of arguments to parameters |
| Confusing `print` with `return` | Function prints but you try to store the result | Use `return` for values you need to use later |
| Wrong order: \*\*kwargs before \*args | `def f(**kw, *ar)` | Must be `def f(*ar, **kw)` |
| Modifying a global without `global` keyword | `count = 0` → `def f(): count += 1` | Add `global count` inside the function |
| Shadowing built-in names | `list = [1,2,3]` | Use descriptive names like `my_list` |
| Treating \*args as a list | `args.append(x)` | `args` is a tuple; convert with `list(args)` first |
| Default parameter before non-default | `def f(x=1, y)` | Non-defaults must come first: `def f(y, x=1)` |

---

## Reflection Questions

1. What is the difference between a **parameter** and an **argument**? Give your own example.
2. When would you choose `*args` over a regular list parameter?
3. When would `**kwargs` be more useful than a regular dictionary parameter?
4. Why is it generally better to use `return` than `global`?
5. A local variable has the same name as a global variable. Which one does the function use? Why?
6. What does LEGB stand for, and in what order does Python search these scopes?
7. What error do you get if you try to use a local variable outside its function?
8. Why is it a bad idea to name your variable `list` or `print`?

---

## Completion Checklist

Before moving on, confirm you can do all of the following:

- [ ] Define and call a function using `def` and `()`
- [ ] Pass one or more arguments to a function
- [ ] Use both positional and keyword arguments
- [ ] Set default parameter values
- [ ] Use `return` to send a value back from a function
- [ ] Use `*args` to accept a variable number of positional arguments
- [ ] Use `**kwargs` to accept a variable number of keyword arguments
- [ ] Combine regular parameters, `*args`, and `**kwargs` in the correct order
- [ ] Explain the difference between local and global scope
- [ ] Use the `global` keyword correctly (and know when NOT to)
- [ ] Explain the LEGB rule
- [ ] Avoid shadowing Python built-in names

---

## Lesson Summary

| Concept | Key Point | Keyword |
|---|---|---|
| **Function definition** | Write once, run many times | `def` |
| **Calling a function** | Execute the function by name + `()` | `function_name()` |
| **Parameters** | Named slots in the function definition | `def f(param):` |
| **Arguments** | Values passed when calling | `f(value)` |
| **Positional args** | Matched by order | `f(1, 2)` |
| **Keyword args** | Matched by name | `f(x=1, y=2)` |
| **Default values** | Used when no argument provided | `def f(x=5):` |
| **Return value** | Send a result back to the caller | `return` |
| **\*args** | Collect extra positional args into a tuple | `*args` |
| **\*\*kwargs** | Collect extra keyword args into a dict | `**kwargs` |
| **Local scope** | Variable exists only inside its function | — |
| **Global scope** | Variable exists at the top level | — |
| **`global` keyword** | Modify a global variable from inside a function | `global x` |
| **LEGB rule** | Python's scope search order | Local → Enclosing → Global → Built-in |

---

> ✅ **You have completed Lesson 15.** You can now define reusable functions, pass any amount of data into them flexibly, and fully understand where your variables live in a Python program. These skills are the foundation of every real Python project — from data analysis scripts to web applications.
