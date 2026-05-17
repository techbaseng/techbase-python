---
render_with_liquid: false
title: "Lesson 16 – Python Decorators, Lambda Functions, Recursion, and Generators"
nav_order: 16
---

# Lesson 16 – Python Decorators, Lambda Functions, Recursion, and Generators

---

## Lesson Introduction

Welcome to one of the most powerful lessons in your Python journey.

In earlier lessons you learned how to write functions — blocks of reusable code that take inputs and return outputs. In this lesson you will meet **four advanced functional programming tools** that Python developers use every single day in real-world projects:

| Tool | What it does |
|---|---|
| **Decorators** | Wrap a function to add extra behaviour without changing its code |
| **Lambda Functions** | Write tiny, one-line anonymous functions on the spot |
| **Recursion** | Write functions that solve problems by calling themselves |
| **Generators** | Produce values one at a time to save memory |

Each concept is a genuine superpower. By the end of this lesson you will understand them deeply, practise them with guided exercises, and combine them in a realistic mini-project.

> 💡 **Teacher's Note:** These topics are interconnected. Lambdas are often used inside decorators. Generators often use recursion. Take your time with each section before moving on.

---

## Prerequisite Concepts

Before diving in, make sure you are comfortable with the following. Each one is briefly reviewed below.

### Functions

A function is a named block of reusable code.

```python
def greet(name):
    return "Hello, " + name

print(greet("Alice"))
```

**Output:**
```
Hello, Alice
```

### Functions Are Objects in Python

This is the most important prerequisite for this lesson.

In Python, **a function is just an object** — exactly like a number, a string, or a list. That means you can:

- Store a function inside a variable
- Pass a function as an argument to another function
- Return a function from a function

```python
def say_hello():
    print("Hello!")

# Store the function in a variable (no parentheses = no call)
my_func = say_hello

# Call it through the variable
my_func()
```

**Output:**
```
Hello!
```

> 🔑 **Key insight:** `say_hello` (no parentheses) is the function **object**. `say_hello()` (with parentheses) **calls** it and runs it. This distinction is critical for decorators.

### Inner Functions

Python allows you to define a function **inside** another function.

```python
def outer():
    def inner():
        print("I am the inner function")
    inner()  # call the inner function

outer()
```

**Output:**
```
I am the inner function
```

---

## Part 1 — Python Decorators

---

### What Is a Decorator?

Imagine you have a function that does something useful. Now you want to add extra behaviour to it — like logging when it runs, checking if the user is logged in, or measuring how long it takes — **without changing the function's original code**.

A **decorator** is a function that wraps around another function and adds that extra behaviour automatically.

**Real-world analogy:** Think of a coffee cup (your original function) and a cup sleeve (the decorator). The sleeve adds insulation and a holder without changing the coffee inside. You can put the same sleeve on any cup.

---

### How a Decorator Works — Step by Step

Let's build one from scratch before using the shortcut syntax.

#### Step 1: A simple function we want to decorate

```python
def say_hello():
    print("Hello!")
```

#### Step 2: Write a decorator function

```python
def my_decorator(func):          # receives the function as an argument
    def wrapper():               # defines a new wrapping function
        print("Before the function runs")
        func()                   # calls the original function
        print("After the function runs")
    return wrapper               # returns the wrapper (not calling it!)
```

#### Step 3: Apply the decorator manually

```python
say_hello = my_decorator(say_hello)   # wrap say_hello
say_hello()                            # call the wrapped version
```

**Output:**
```
Before the function runs
Hello!
After the function runs
```

Let's trace exactly what happened:

1. `my_decorator(say_hello)` — passes `say_hello` as `func` into the decorator
2. Inside the decorator, `wrapper` is defined (but not called yet)
3. `wrapper` is returned — it is now the new `say_hello`
4. When we call `say_hello()`, we are actually calling `wrapper()`
5. `wrapper` prints "Before…", calls the original `func()` which prints "Hello!", then prints "After…"

---

### The `@` Shortcut Syntax

Python provides a cleaner way to apply a decorator using the `@` symbol. This is called **decorator syntax** or **pie syntax**.

```python
def my_decorator(func):
    def wrapper():
        print("Before the function runs")
        func()
        print("After the function runs")
    return wrapper

@my_decorator           # This is EXACTLY the same as: say_hello = my_decorator(say_hello)
def say_hello():
    print("Hello!")

say_hello()
```

**Output:**
```
Before the function runs
Hello!
After the function runs
```

> 💡 `@my_decorator` placed just above a function definition is a clean shorthand for wrapping it.

---

### Decorating Functions That Have Arguments

What if the function you want to decorate takes arguments? You need to pass those arguments through the wrapper.

```python
def my_decorator(func):
    def wrapper(*args, **kwargs):    # accepts any arguments
        print("Something before")
        result = func(*args, **kwargs)   # passes them to the original function
        print("Something after")
        return result               # returns whatever the original function returned
    return wrapper

@my_decorator
def add(a, b):
    return a + b

total = add(3, 4)
print("Result:", total)
```

**Output:**
```
Something before
Something after
Result: 7
```

**What are `*args` and `**kwargs`?**

- `*args` — collects any number of **positional** arguments into a tuple
- `**kwargs` — collects any number of **keyword** arguments into a dictionary
- Together they allow your wrapper to work with **any function**, regardless of its parameter list

---

### A Practical Decorator: Timing a Function

Here is a decorator you would actually use in real code — measuring how long a function takes to run:

```python
import time

def timer_decorator(func):
    def wrapper(*args, **kwargs):
        start = time.time()           # record start time
        result = func(*args, **kwargs)
        end = time.time()             # record end time
        print(f"{func.__name__} took {end - start:.4f} seconds")
        return result
    return wrapper

@timer_decorator
def slow_task():
    time.sleep(1)   # simulate a slow operation
    print("Task done!")

slow_task()
```

**Output (approximate):**
```
Task done!
slow_task took 1.0012 seconds
```

> 🌍 **Real-world use:** Web frameworks like Flask and Django use decorators extensively for routing (`@app.route("/home")`), authentication (`@login_required`), and caching.

---

### A Practical Decorator: Access Control

```python
is_logged_in = True   # simulate login state

def require_login(func):
    def wrapper(*args, **kwargs):
        if is_logged_in:
            return func(*args, **kwargs)
        else:
            print("Access denied. Please log in.")
    return wrapper

@require_login
def view_dashboard():
    print("Welcome to your dashboard!")

view_dashboard()
```

**Output (when logged in):**
```
Welcome to your dashboard!
```

---

### Applying Multiple Decorators

You can stack decorators. They apply from **bottom to top** (closest to the function first).

```python
def bold(func):
    def wrapper():
        return "<b>" + func() + "</b>"
    return wrapper

def italic(func):
    def wrapper():
        return "<i>" + func() + "</i>"
    return wrapper

@bold        # applied second (outer)
@italic      # applied first (inner)
def greet():
    return "Hello"

print(greet())
```

**Output:**
```
<b><i>Hello</i></b>
```

> 🤔 **Thinking prompt:** What happens if you swap `@bold` and `@italic`? Try it — what output do you get?

---

### Common Beginner Mistakes with Decorators

**Mistake 1: Calling the function instead of passing it**

```python
# ❌ WRONG
decorated = my_decorator(say_hello())   # say_hello() calls it and passes None

# ✅ CORRECT
decorated = my_decorator(say_hello)     # pass the function object
```

**Mistake 2: Forgetting to return the wrapper**

```python
# ❌ WRONG — decorator returns None
def my_decorator(func):
    def wrapper():
        func()
    # forgot: return wrapper

# ✅ CORRECT
def my_decorator(func):
    def wrapper():
        func()
    return wrapper
```

**Mistake 3: Forgetting to call the original function inside wrapper**

```python
# ❌ WRONG — original function never runs
def my_decorator(func):
    def wrapper():
        print("Before")
        # forgot: func()
    return wrapper
```

---

## Part 2 — Lambda Functions

---

### What Is a Lambda Function?

A **lambda function** is a small, anonymous (nameless) function written in a single line.

- **Anonymous** means it has no `def` keyword and no name
- It is used when you need a short, throwaway function
- It can only contain a **single expression** (not multiple lines of code)

**Syntax:**

```
lambda arguments : expression
```

---

### Your First Lambda

```python
# Regular function
def double(x):
    return x * 2

# Equivalent lambda
double_lambda = lambda x: x * 2

print(double(5))          # Output: 10
print(double_lambda(5))   # Output: 10
```

**Output:**
```
10
10
```

Both do exactly the same thing. The lambda is just shorter.

---

### Lambda With Multiple Arguments

```python
add = lambda a, b: a + b

print(add(3, 7))
```

**Output:**
```
10
```

```python
full_name = lambda first, last: first + " " + last

print(full_name("Ada", "Lovelace"))
```

**Output:**
```
Ada Lovelace
```

---

### Why Use Lambda? — The Power Comes With Other Functions

The real power of lambda appears when you use it **inside** other functions that accept a function as an argument. The most common examples are `map()`, `filter()`, and `sorted()`.

#### Lambda with `map()`

`map(function, list)` applies a function to **every item** in a list.

```python
numbers = [1, 2, 3, 4, 5]

doubled = list(map(lambda x: x * 2, numbers))

print(doubled)
```

**Output:**
```
[2, 4, 6, 8, 10]
```

**Without lambda**, you'd need to write a separate function:

```python
def double(x):
    return x * 2

doubled = list(map(double, numbers))
```

Lambda makes this a one-liner.

---

#### Lambda with `filter()`

`filter(function, list)` keeps only the items where the function returns `True`.

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

evens = list(filter(lambda x: x % 2 == 0, numbers))

print(evens)
```

**Output:**
```
[2, 4, 6, 8, 10]
```

---

#### Lambda with `sorted()`

`sorted(list, key=function)` sorts a list using a custom key.

```python
students = [
    {"name": "Alice", "grade": 85},
    {"name": "Bob",   "grade": 72},
    {"name": "Carol", "grade": 91},
]

# Sort by grade
sorted_students = sorted(students, key=lambda s: s["grade"])

for s in sorted_students:
    print(s["name"], s["grade"])
```

**Output:**
```
Bob 72
Alice 85
Carol 91
```

---

### Lambda Inside a Function (Returning Lambda)

One common pattern: a function that **returns** a lambda. This lets you create customised functions on the fly.

```python
def multiplier(n):
    return lambda x: x * n      # returns a lambda that multiplies by n

double  = multiplier(2)
triple  = multiplier(3)
times10 = multiplier(10)

print(double(5))    # 10
print(triple(5))    # 15
print(times10(5))   # 50
```

**Output:**
```
10
15
50
```

> 🌍 **Real-world use:** Sorting e-commerce products by price, name, or rating. Filtering customer lists. Transforming data in data science pipelines.

---

### Lambda Limitations

Lambda can only hold **one expression**. It cannot contain:

- Multiple statements
- `if/else` blocks (only inline ternary expressions)
- Loops
- `return` keyword (the expression IS the return value)

```python
# ✅ Inline if/else IS allowed
classify = lambda x: "positive" if x > 0 else "non-positive"
print(classify(5))    # positive
print(classify(-3))   # non-positive
```

---

### Common Beginner Mistakes with Lambda

**Mistake 1: Using `return` inside lambda**

```python
# ❌ WRONG
f = lambda x: return x * 2    # SyntaxError

# ✅ CORRECT
f = lambda x: x * 2
```

**Mistake 2: Using lambda for complex logic**

```python
# ❌ Bad practice — hard to read
f = lambda x, y: x**2 + 2*x*y + y**2 if x > 0 and y > 0 else 0

# ✅ Better — use a regular function for clarity
def compute(x, y):
    if x > 0 and y > 0:
        return x**2 + 2*x*y + y**2
    return 0
```

> 💡 **Rule of thumb:** If the lambda is hard to read in one line, write a regular function instead.

---

## Part 3 — Python Recursion

---

### What Is Recursion?

**Recursion** is when a function calls **itself** inside its own body to solve a smaller version of the same problem.

**Real-world analogy:** Imagine you're in a long line at a cinema and you can't see the front. You ask the person in front of you, "What number are you in line?" They don't know either, so they ask the person in front of *them*, and so on. Eventually someone at the front says "I'm number 1!" Then the answer travels back: "I'm number 2", "I'm number 3", until the answer reaches you.

That chain of asking-then-reporting-back is **recursion**.

---

### The Two Required Parts of Any Recursive Function

Every recursive function must have:

1. **Base case** — the condition where the function stops calling itself (the "bottom of the line")
2. **Recursive case** — where the function calls itself with a smaller/simpler input

Without a base case, the function calls itself forever → **infinite recursion** → Python crashes with a `RecursionError`.

---

### Your First Recursive Function: Counting Down

```python
def countdown(n):
    if n <= 0:          # Base case: stop here
        print("Go!")
    else:
        print(n)
        countdown(n - 1)   # Recursive case: call with smaller n

countdown(5)
```

**Output:**
```
5
4
3
2
1
Go!
```

Let's trace the calls:

```
countdown(5) → prints 5, calls countdown(4)
  countdown(4) → prints 4, calls countdown(3)
    countdown(3) → prints 3, calls countdown(2)
      countdown(2) → prints 2, calls countdown(1)
        countdown(1) → prints 1, calls countdown(0)
          countdown(0) → prints "Go!" — BASE CASE, stops
```

---

### Classic Example: Factorial

The **factorial** of a number n (written n!) is:

```
5! = 5 × 4 × 3 × 2 × 1 = 120
```

It has a natural recursive definition:
- `0! = 1` (base case — defined mathematically)
- `n! = n × (n-1)!` (recursive case)

```python
def factorial(n):
    if n == 0:              # Base case
        return 1
    else:
        return n * factorial(n - 1)   # Recursive case

print(factorial(5))   # 120
print(factorial(6))   # 720
print(factorial(0))   # 1
```

**Output:**
```
120
720
1
```

**Tracing factorial(5):**

```
factorial(5)
  = 5 * factorial(4)
  = 5 * 4 * factorial(3)
  = 5 * 4 * 3 * factorial(2)
  = 5 * 4 * 3 * 2 * factorial(1)
  = 5 * 4 * 3 * 2 * 1 * factorial(0)
  = 5 * 4 * 3 * 2 * 1 * 1
  = 120
```

---

### Classic Example: Fibonacci Sequence

The **Fibonacci sequence** is: 0, 1, 1, 2, 3, 5, 8, 13, 21, …

Each number is the sum of the two before it.

- `fib(0) = 0` (base case)
- `fib(1) = 1` (base case)
- `fib(n) = fib(n-1) + fib(n-2)` (recursive case)

```python
def fib(n):
    if n == 0:
        return 0
    elif n == 1:
        return 1
    else:
        return fib(n - 1) + fib(n - 2)

for i in range(10):
    print(f"fib({i}) = {fib(i)}")
```

**Output:**
```
fib(0) = 0
fib(1) = 1
fib(2) = 1
fib(3) = 2
fib(4) = 3
fib(5) = 5
fib(6) = 8
fib(7) = 13
fib(8) = 21
fib(9) = 34
```

---

### Classic Example: Power Function

Calculate `base ** exponent` recursively:

```python
def power(base, exp):
    if exp == 0:              # anything to the power 0 is 1
        return 1
    else:
        return base * power(base, exp - 1)

print(power(2, 10))   # 1024
print(power(3, 4))    # 81
```

**Output:**
```
1024
81
```

---

### Visualising the Call Stack

Every time a recursive function calls itself, Python pushes a new **stack frame** onto the **call stack**. When the base case is reached, the frames unwind in reverse order.

```
factorial(3)           ← frame 1
  factorial(2)         ← frame 2
    factorial(1)       ← frame 3
      factorial(0)     ← frame 4 → returns 1
    ← returns 1 * 1 = 1
  ← returns 2 * 1 = 2
← returns 3 * 2 = 6
```

Python has a default **recursion limit of 1000** to prevent infinite recursion from crashing your system.

---

### Recursion vs Loops

Both can solve the same problems. Here is the same task done two ways:

**Loop version (sum 1 to n):**

```python
def sum_loop(n):
    total = 0
    for i in range(1, n + 1):
        total += i
    return total

print(sum_loop(5))   # 15
```

**Recursive version:**

```python
def sum_recursive(n):
    if n == 0:
        return 0
    return n + sum_recursive(n - 1)

print(sum_recursive(5))   # 15
```

**Output:**
```
15
```

> 🌍 **Real-world use:** Recursion shines in tasks with **naturally nested structure**: file systems (folders inside folders), HTML/XML trees, organisation charts, mathematical proofs, sorting algorithms (merge sort, quicksort), and graph traversal (GPS routing, social networks).

---

### Common Beginner Mistakes with Recursion

**Mistake 1: Missing base case (infinite recursion)**

```python
# ❌ WRONG — never stops
def countdown(n):
    print(n)
    countdown(n - 1)   # No base case → RecursionError

# ✅ CORRECT
def countdown(n):
    if n <= 0:          # base case!
        return
    print(n)
    countdown(n - 1)
```

**Mistake 2: Base case never reached**

```python
# ❌ WRONG — n grows instead of shrinks
def countdown(n):
    if n == 0:
        return
    countdown(n + 1)   # Wrong direction — never reaches 0

# ✅ CORRECT — move toward the base case
def countdown(n):
    if n == 0:
        return
    countdown(n - 1)
```

**Mistake 3: Forgetting to return the recursive result**

```python
# ❌ WRONG
def factorial(n):
    if n == 0:
        return 1
    n * factorial(n - 1)   # result computed but not returned!

# ✅ CORRECT
def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n - 1)
```

> 🤔 **Thinking prompt:** What is the largest number you can pass to `factorial()` before Python raises a RecursionError? Try it!

---

## Part 4 — Python Generators

---

### What Is a Generator?

Imagine you need to process 10 million numbers. If you put them all in a list, Python stores all 10 million in memory at once — that's enormous. A **generator** produces values **one at a time**, on demand, without storing them all in memory.

**Real-world analogy:** A list is like printing a whole book before reading it. A generator is like a printing press that prints one page at a time as you read.

**Key properties:**
- Defined like a function, but uses `yield` instead of `return`
- Returns a **generator object**
- Values are produced **lazily** — only when asked for
- Once a value is yielded, the function **pauses** there and resumes next time

---

### `yield` vs `return`

| `return` | `yield` |
|---|---|
| Returns a value and the function **ends** | Returns a value and the function **pauses** |
| Called once | Can be called many times |
| Produces one result | Produces a series of results |
| Regular function | Generator function |

---

### Your First Generator

```python
def my_generator():
    yield 1
    yield 2
    yield 3

gen = my_generator()    # creates a generator object (nothing runs yet)

print(next(gen))   # runs until first yield → 1
print(next(gen))   # resumes, runs until second yield → 2
print(next(gen))   # resumes, runs until third yield → 3
```

**Output:**
```
1
2
3
```

**What happens if you call `next()` again?**

```python
print(next(gen))   # StopIteration error — no more values
```

---

### Looping Over a Generator

The most common way to consume a generator is with a `for` loop. Python calls `next()` automatically and stops when `StopIteration` is raised.

```python
def count_up(n):
    i = 1
    while i <= n:
        yield i
        i += 1

for number in count_up(5):
    print(number)
```

**Output:**
```
1
2
3
4
5
```

---

### Generator with an Infinite Sequence

Generators are perfect for sequences that go on forever — something you cannot do with a list.

```python
def infinite_counter(start=0):
    n = start
    while True:         # runs forever
        yield n
        n += 1

counter = infinite_counter(10)

for _ in range(5):
    print(next(counter))
```

**Output:**
```
10
11
12
13
14
```

> 💡 No list of infinite length could ever exist — but a generator can represent one.

---

### Generator Expressions (One-Liners)

Just as list comprehensions build lists in one line, **generator expressions** build generators in one line. Use parentheses `()` instead of square brackets `[]`.

```python
# List comprehension — creates ALL values in memory NOW
squares_list = [x**2 for x in range(10)]

# Generator expression — creates values one at a time on demand
squares_gen = (x**2 for x in range(10))

print(squares_list)       # [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
print(squares_gen)        # <generator object <genexpr> at 0x...>

for val in squares_gen:
    print(val, end=" ")
```

**Output:**
```
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
0 1 4 9 16 25 36 49 64 81
```

---

### Memory Comparison: List vs Generator

```python
import sys

nums_list = [x for x in range(1000000)]
nums_gen  = (x for x in range(1000000))

print("List size:", sys.getsizeof(nums_list), "bytes")
print("Generator size:", sys.getsizeof(nums_gen), "bytes")
```

**Output (approximate):**
```
List size: 8056624 bytes    (~8 MB)
Generator size: 104 bytes   (~0.0001 MB)
```

The generator uses almost **no memory** regardless of how many values it will produce.

---

### A Practical Generator: Reading a Large File Line by Line

```python
def read_large_file(filepath):
    with open(filepath, "r") as f:
        for line in f:
            yield line.strip()

# Usage — only one line in memory at a time
for line in read_large_file("huge_log_file.txt"):
    print(line)
```

> 🌍 **Real-world use:** Log analysis, streaming database results, processing CSV files too large to fit in RAM, real-time sensor data, network packet processing.

---

### Generator with Multiple `yield` Statements

```python
def weather_report():
    yield "Morning: Sunny, 18°C"
    yield "Noon: Partly cloudy, 24°C"
    yield "Evening: Windy, 20°C"
    yield "Night: Clear, 15°C"

for report in weather_report():
    print(report)
```

**Output:**
```
Morning: Sunny, 18°C
Noon: Partly cloudy, 24°C
Evening: Windy, 20°C
Night: Clear, 15°C
```

---

### The `send()` Method — Two-Way Communication

Generators can also **receive** values while running using `.send()`.

```python
def accumulator():
    total = 0
    while True:
        value = yield total     # yields total, then receives a new value
        total += value

acc = accumulator()
next(acc)           # prime the generator (runs to first yield)

print(acc.send(10))   # sends 10 → total = 10
print(acc.send(20))   # sends 20 → total = 30
print(acc.send(5))    # sends 5  → total = 35
```

**Output:**
```
10
30
35
```

---

### Common Beginner Mistakes with Generators

**Mistake 1: Trying to index a generator like a list**

```python
gen = (x for x in range(10))

# ❌ WRONG
print(gen[0])   # TypeError: 'generator' object is not subscriptable

# ✅ CORRECT — convert to list first if you need indexing
lst = list(gen)
print(lst[0])   # 0
```

**Mistake 2: Consuming a generator twice**

```python
gen = (x for x in range(5))
list1 = list(gen)   # consumes all values
list2 = list(gen)   # generator is exhausted — empty!

print(list1)   # [0, 1, 2, 3, 4]
print(list2)   # []
```

**Mistake 3: Confusing `yield` with `return`**

```python
# ❌ Using return — gives only ONE value, function ends
def give_numbers():
    return 1
    return 2    # never reached

# ✅ Using yield — gives multiple values, function pauses
def give_numbers():
    yield 1
    yield 2
```

---

## Guided Practice Exercises

---

### Exercise 1 — Decorator: Logging Function Calls

**Objective:** Write a decorator that logs when a function starts and ends.

**Scenario:** You are building a data processing pipeline and need to track which functions run and when.

**Steps:**

1. Write a decorator called `log_call`
2. It should print `"Calling: [function name]"` before the function runs
3. It should print `"Finished: [function name]"` after it finishes
4. Decorate a function called `process_data(items)` that prints each item

**Hint:** Use `func.__name__` to get the function's name.

**Solution:**

```python
def log_call(func):
    def wrapper(*args, **kwargs):
        print(f"Calling: {func.__name__}")
        result = func(*args, **kwargs)
        print(f"Finished: {func.__name__}")
        return result
    return wrapper

@log_call
def process_data(items):
    for item in items:
        print(f"  Processing: {item}")

process_data(["order_1", "order_2", "order_3"])
```

**Expected Output:**
```
Calling: process_data
  Processing: order_1
  Processing: order_2
  Processing: order_3
Finished: process_data
```

**Self-check questions:**
- What would happen if you forgot `*args, **kwargs` in the wrapper?
- How would you modify the decorator to also log the arguments passed?

---

### Exercise 2 — Lambda: Sorting Products

**Objective:** Use lambda to sort a list of product dictionaries.

**Scenario:** An online shop needs to display products sorted by price (cheapest first), then by rating (highest first).

```python
products = [
    {"name": "Keyboard",  "price": 49.99, "rating": 4.5},
    {"name": "Mouse",     "price": 29.99, "rating": 4.8},
    {"name": "Monitor",   "price": 299.99, "rating": 4.2},
    {"name": "Headphones","price": 79.99, "rating": 4.7},
    {"name": "Webcam",    "price": 49.99, "rating": 4.3},
]

# Sort by price ascending
by_price = sorted(products, key=lambda p: p["price"])

# Sort by rating descending
by_rating = sorted(products, key=lambda p: p["rating"], reverse=True)

print("Sorted by price:")
for p in by_price:
    print(f"  {p['name']}: £{p['price']}")

print("\nSorted by rating:")
for p in by_rating:
    print(f"  {p['name']}: {p['rating']} stars")
```

**Expected Output:**
```
Sorted by price:
  Mouse: £29.99
  Keyboard: £49.99
  Webcam: £49.99
  Headphones: £79.99
  Monitor: £299.99

Sorted by rating:
  Mouse: 4.8 stars
  Headphones: 4.7 stars
  Keyboard: 4.5 stars
  Webcam: 4.3 stars
  Monitor: 4.2 stars
```

**What-if challenge:** Add a third sort: cheapest AND highest-rated first. Hint: `key=lambda p: (p["price"], -p["rating"])`

---

### Exercise 3 — Recursion: Sum of Digits

**Objective:** Write a recursive function that sums all digits of a number.

**Example:** `sum_digits(1234) → 1 + 2 + 3 + 4 = 10`

**Hint:** A number's last digit is `n % 10`. The rest of the number is `n // 10`.

```python
def sum_digits(n):
    if n < 10:             # Base case: single digit
        return n
    return (n % 10) + sum_digits(n // 10)   # last digit + recurse on the rest

print(sum_digits(1234))   # 10
print(sum_digits(9999))   # 36
print(sum_digits(7))      # 7
```

**Expected Output:**
```
10
36
7
```

**Self-check:** Trace `sum_digits(456)` step by step on paper.

---

### Exercise 4 — Generator: Student Grade Report

**Objective:** Write a generator that yields student report lines one at a time.

**Scenario:** A school system needs to print student reports without loading all 10,000 student records into memory at once.

```python
students = [
    {"name": "Alice",  "score": 88},
    {"name": "Bob",    "score": 62},
    {"name": "Carol",  "score": 95},
    {"name": "David",  "score": 74},
    {"name": "Eve",    "score": 55},
]

def grade_report(student_list):
    for student in student_list:
        score = student["score"]
        grade = "A" if score >= 90 else "B" if score >= 80 else "C" if score >= 70 else "D" if score >= 60 else "F"
        yield f"{student['name']}: {score}/100 — Grade {grade}"

print("=== STUDENT GRADE REPORT ===")
for report_line in grade_report(students):
    print(report_line)
```

**Expected Output:**
```
=== STUDENT GRADE REPORT ===
Alice: 88/100 — Grade B
Bob: 62/100 — Grade D
Carol: 95/100 — Grade A
David: 74/100 — Grade C
Eve: 55/100 — Grade F
```

---

## Mini-Project — Smart Budget Analyser

In this project you will combine **all four concepts** — decorators, lambda, recursion, and generators — to build a simple budget analysis tool.

---

### Project Overview

**Scenario:** You are building a personal finance tool. Given a list of transactions, you need to:

1. Log every major function call (decorator)
2. Filter and sort transactions (lambda)
3. Calculate running totals recursively (recursion)
4. Stream the report line by line (generator)

---

### Stage 1 — Setup and Decorator

```python
# Stage 1: Logging decorator
def log_operation(func):
    def wrapper(*args, **kwargs):
        print(f"\n[LOG] Running: {func.__name__}")
        result = func(*args, **kwargs)
        print(f"[LOG] Completed: {func.__name__}")
        return result
    return wrapper
```

**Milestone check:** Can you decorate a simple function and see the log messages?

---

### Stage 2 — Transaction Data and Lambda Filtering

```python
# Stage 2: Sample transactions
transactions = [
    {"desc": "Rent",          "amount": -1200, "category": "Housing"},
    {"desc": "Salary",        "amount":  3000, "category": "Income"},
    {"desc": "Groceries",     "amount":  -150, "category": "Food"},
    {"desc": "Freelance",     "amount":   800, "category": "Income"},
    {"desc": "Electricity",   "amount":   -95, "category": "Utilities"},
    {"desc": "Restaurant",    "amount":   -60, "category": "Food"},
    {"desc": "Gym",           "amount":   -40, "category": "Health"},
    {"desc": "Netflix",       "amount":   -15, "category": "Entertainment"},
]

# Lambda filters
income    = list(filter(lambda t: t["amount"] > 0, transactions))
expenses  = list(filter(lambda t: t["amount"] < 0, transactions))

# Sort expenses by amount (most expensive first)
sorted_expenses = sorted(expenses, key=lambda t: t["amount"])

print("Income sources:")
for t in income:
    print(f"  {t['desc']}: +£{t['amount']}")

print("\nExpenses (largest first):")
for t in sorted_expenses:
    print(f"  {t['desc']}: £{t['amount']}")
```

**Milestone output:**
```
Income sources:
  Salary: +£3000
  Freelance: +£800

Expenses (largest first):
  Rent: £-1200
  Groceries: £-150
  Electricity: £-95
  Restaurant: £-60
  Gym: £-40
  Netflix: £-15
```

---

### Stage 3 — Recursive Total

```python
# Stage 3: Recursive sum of transaction amounts
def total_recursive(txns, index=0):
    if index == len(txns):          # base case: past the last item
        return 0
    return txns[index]["amount"] + total_recursive(txns, index + 1)

@log_operation
def compute_balance(txns):
    return total_recursive(txns)

balance = compute_balance(transactions)
print(f"\nNet balance: £{balance}")
```

**Milestone output:**
```
[LOG] Running: compute_balance
[LOG] Completed: compute_balance

Net balance: £2240
```

---

### Stage 4 — Generator Report

```python
# Stage 4: Generator-based report
def budget_report(txns):
    yield "=" * 40
    yield "       MONTHLY BUDGET REPORT"
    yield "=" * 40
    for t in txns:
        sign = "+" if t["amount"] > 0 else ""
        yield f"  [{t['category']:<15}] {t['desc']:<15}: {sign}£{t['amount']}"
    yield "-" * 40
    net = total_recursive(txns)
    yield f"  Net Balance: £{net}"
    yield "=" * 40

@log_operation
def print_report(txns):
    for line in budget_report(txns):
        print(line)

print_report(transactions)
```

**Final output:**
```
[LOG] Running: print_report
========================================
       MONTHLY BUDGET REPORT
========================================
  [Housing        ] Rent           : -£1200
  [Income         ] Salary         : +£3000
  [Food           ] Groceries      : -£150
  [Income         ] Freelance      : +£800
  [Utilities      ] Electricity    : -£95
  [Food           ] Restaurant     : -£60
  [Health         ] Gym            : -£40
  [Entertainment  ] Netflix        : -£15
----------------------------------------
  Net Balance: £2240
========================================
[LOG] Completed: print_report
```

---

### Optional Enhancements

- Add a decorator that measures how long the report takes to generate
- Use a generator expression to yield only expense lines
- Add recursion to find the single largest expense
- Group transactions by category using a dictionary

---

## Common Beginner Mistakes — Consolidated Reference

| Mistake | Wrong | Correct |
|---|---|---|
| Calling function when passing to decorator | `decorator(func())` | `decorator(func)` |
| Forgetting to return wrapper | `def dec(f): def w(): f()` | `def dec(f): def w(): f(); return w` |
| `return` inside lambda | `lambda x: return x*2` | `lambda x: x*2` |
| Missing base case in recursion | No `if` to stop | Always include `if n == base: return value` |
| Wrong recursion direction | `countdown(n+1)` | `countdown(n-1)` |
| Indexing a generator | `gen[0]` | `list(gen)[0]` |
| Consuming a generator twice | `list(gen); list(gen)` | Create a new generator each time |
| Stacking decorators wrong order | Confusing inner/outer | Remember: bottom `@` applies first |

---

## Reflection Questions

1. **Decorators:** Why is it useful to add behaviour to a function without modifying its source code? Can you think of a real project where you would use a `@retry` decorator that automatically retries a failed network request?

2. **Lambda:** What is the difference between `map()` and a `for` loop? When is `map()` with lambda cleaner, and when is a regular loop clearer?

3. **Recursion:** Every recursive function can be rewritten as a loop. If that's true, why do we use recursion at all? When does recursion make code *much* simpler?

4. **Generators:** If you needed to process a 10 GB log file, would you use a list or a generator? Why? What would happen if you used a list?

5. **Combined thinking:** In the mini-project, the `log_operation` decorator was applied to `print_report`, which itself uses a generator internally. How do these two interact?

---

## Completion Checklist

Before moving to the next lesson, confirm you can:

- [ ] Write a decorator function from scratch, with and without `@` syntax
- [ ] Decorate a function that takes arguments using `*args, **kwargs`
- [ ] Write a lambda function with one or more arguments
- [ ] Use lambda with `map()`, `filter()`, and `sorted()`
- [ ] Write a recursive function with a clear base case and recursive case
- [ ] Trace a recursive function call by hand on paper
- [ ] Write a generator function using `yield`
- [ ] Loop over a generator with `for` and with `next()`
- [ ] Write a generator expression using `()`
- [ ] Explain the memory advantage of generators over lists
- [ ] Identify and fix the common mistakes for each concept
- [ ] Complete all four practice exercises with correct output
- [ ] Complete all four stages of the mini-project

---

## Lesson Summary

In this lesson you mastered four powerful Python tools:

**Decorators** allow you to wrap a function and extend its behaviour without modifying its code. You write a function that accepts a function, defines an inner `wrapper`, and returns that wrapper. The `@decorator_name` syntax is a clean shorthand.

**Lambda functions** are anonymous one-liner functions written as `lambda args: expression`. They shine when passed as arguments to `map()`, `filter()`, or `sorted()`, making code concise and readable.

**Recursion** is a technique where a function solves a problem by calling itself on a simpler version of the same problem. Every recursive function needs a base case (where it stops) and a recursive case (where it calls itself). Classic applications include factorials, Fibonacci numbers, and tree traversals.

**Generators** are functions that use `yield` to produce values one at a time, pausing between each. They are extraordinarily memory-efficient and essential for working with large datasets, infinite sequences, or streaming data.

Together, these tools form the backbone of functional and advanced Python programming. You will encounter all four in web frameworks, data science, automation, and system programming.

---

> 🎉 **Congratulations!** You have completed Lesson 16. You now have the skills to write professional-grade Python code using decorators, lambda functions, recursion, and generators.
