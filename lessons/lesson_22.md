---
render_with_liquid: false
title: "Lesson 22: Python Encapsulation, Inner Classes, and File Handling"
nav_order: 22
---

# Lesson 22: Python Encapsulation, Inner Classes, and File Handling

---

## Lesson Introduction

Welcome to Lesson 22! This lesson covers three powerful topics that every serious Python programmer needs to understand deeply.

We start with **Encapsulation** — the art of protecting your data inside a class so it cannot be changed accidentally from outside. Then we move to **Inner Classes** — classes that live inside other classes, useful for grouping related things together neatly. Finally, we open the door to one of the most practical programming skills of all: **File Handling** — how Python reads files stored on your computer.

By the end of this lesson you will be able to:

- Understand what encapsulation is, why it matters, and how to use private and protected properties in Python
- Create getter and setter methods to safely read and change private data
- Understand name mangling — how Python secretly renames private attributes
- Create inner classes and understand how they relate to outer classes
- Open a file using Python's built-in `open()` function
- Read the full contents of a file, read specific numbers of characters, and read files line by line
- Use the `with` statement to open files safely and automatically close them

This lesson connects directly to the real world: from banking systems that protect your account balance, to software that reads and processes log files, sensor data, or student records.

---

## Prerequisite Concepts

Before starting, make sure you are comfortable with these ideas from earlier lessons:

- **Classes and Objects** — you know how to define a class, create an object, and use `self`
- **The `__init__` method** — you know how to set up a class with starting properties
- **Class methods** — you know how to define functions inside a class
- **Inheritance and Polymorphism** — you have seen how classes can share and override behaviour (Lessons 20–21)

If any of these feel shaky, quickly re-read those lessons before continuing. This lesson builds directly on them.

---

## Part 1: Python Encapsulation

---

### 1.1 What Is Encapsulation?

Let us start with a real-life story.

Imagine you walk into a bank in Lagos and ask the teller to see a customer's account balance. The teller refuses — that information is protected. You cannot just reach into the filing cabinet and read it yourself. Instead, you must go through the proper channels: fill a form, verify your identity, and only then does the bank give you what you are allowed to see.

This is exactly what encapsulation does in programming.

**Encapsulation** means keeping data (properties) and methods (functions) bundled inside a class, while controlling how that data can be accessed or changed from outside the class.

**Why does it exist?**

Without encapsulation, any part of your program can directly change any variable in your class — even by accident. Imagine a `Student` class where the student's grade can be changed to `500` by mistake. Encapsulation stops this by protecting the grade behind a controlled gate.

**What problem does it solve?**

It protects data from:
- Accidental changes (a bug sets age to a negative number)
- Invalid values (someone sets a student's score to `999` out of `100`)
- Unauthorised access (outside code reading sensitive information)

**How does it work?**

Python uses special naming rules to mark properties as private or protected.

---

### 1.2 Public, Protected, and Private Properties

Python has three levels of access for class properties:

| Level | Prefix | Meaning |
|---|---|---|
| Public | `name` | Anyone can access it |
| Protected | `_name` | Intended for internal/subclass use only |
| Private | `__name` | Strongly restricted — only the class itself can use it |

Let us explore each one.

---

### 1.3 Public Properties (No Prefix)

A normal property with no underscore is **public**. Anyone can read or change it freely.

```python
class Student:
    def __init__(self, name):
        self.name = name  # Public property — anyone can access this

s = Student("Amaka")
print(s.name)       # Access directly from outside — this is fine
s.name = "Ngozi"    # Change directly — also fine for public data
print(s.name)
```

**Expected output in terminal:**
```
Amaka
Ngozi
```

Public properties are simple and fine for data that does not need protection.

---

### 1.4 Protected Properties (Single Underscore `_`)

A single underscore `_` before a property name signals: **"This is intended for internal use. Be careful with it."**

```python
class BankAccount:
    def __init__(self, owner, balance):
        self.owner = owner
        self._balance = balance  # Protected — a gentle warning, not enforced

account = BankAccount("Emeka", 50000)
print(account.owner)     # Fine — public
print(account._balance)  # Works, but it is a signal: "you shouldn't do this"
```

**Expected output in terminal:**
```
Emeka
50000
```

> **Important:** A single underscore is **only a convention** — a polite message to other programmers. Python does NOT actually stop anyone from accessing `_balance`. It is like a sign on a door that says "Staff Only" — people can still walk in, but they know they probably shouldn't.

---

### 1.5 Private Properties (Double Underscore `__`)

A double underscore `__` before a property name makes it **private**. Python enforces this much more strongly using a technique called **name mangling** (we will explain this shortly).

```python
class Person:
    def __init__(self, name, age):
        self.name = name       # Public
        self.__age = age       # Private — cannot be accessed directly from outside

p1 = Person("Tunde", 30)
print(p1.name)    # Works fine
print(p1.__age)   # This will CAUSE AN ERROR
```

**Expected output in terminal:**
```
Tunde
AttributeError: 'Person' object has no attribute '__age'
```

The line `print(p1.__age)` crashes because Python has hidden `__age` under a different internal name. This is intentional — Python is protecting your data.

> **Think about it:** Why did `__age` cause an error but `_balance` did not? The double underscore triggers Python's name mangling system, which we explore in Section 1.8.

---

### 1.6 Getter Methods — Reading Private Data Safely

Since private properties cannot be read directly from outside, we create a **getter method** — a specially named function inside the class that returns the private value.

**What is a getter?** It is simply a method that "gets" (retrieves) the value of a private property and hands it to whoever asks, in a controlled way.

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.__age = age       # Private property

    def get_age(self):         # Getter method
        return self.__age      # Returns the private value safely

p1 = Person("Chioma", 25)
print(p1.name)         # Direct access to public property — fine
print(p1.get_age())    # Using the getter to access private age — safe and controlled
```

**Expected output in terminal:**
```
Chioma
25
```

Line by line explanation:
- `self.__age = age` — stores age as a private property; the double underscore hides it
- `def get_age(self)` — defines a method inside the class; only this method can touch `__age`
- `return self.__age` — the getter reads `__age` from inside the class (where it is allowed) and returns it
- `p1.get_age()` — from outside the class, we call the getter and receive the age safely

---

### 1.7 Setter Methods — Changing Private Data Safely (With Validation)

A **setter method** "sets" (changes) the value of a private property. The setter's real power is that it can **validate** the new value before saving it, rejecting any bad input.

**Why is this powerful?** Without a setter, if someone types `p1.__age = -5`, age becomes negative — which makes no real-world sense. With a setter, you write rules that reject invalid input.

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.__age = age

    def get_age(self):
        return self.__age

    def set_age(self, age):         # Setter method
        if age > 0:                 # Validate: age must be a positive number
            self.__age = age        # Only update if the value is valid
        else:
            print("Age must be a positive number!")  # Reject invalid input

p1 = Person("Tobi", 25)
print(p1.get_age())     # 25

p1.set_age(26)          # Valid change
print(p1.get_age())     # 26

p1.set_age(-10)         # Invalid — should be rejected
print(p1.get_age())     # Still 26 — the bad value was blocked
```

**Expected output in terminal:**
```
25
26
Age must be a positive number!
26
```

This is encapsulation at work: the data is protected, changes go through a validation gate, and bad values are rejected cleanly.

---

### 1.8 Practical Encapsulation with Validation — A Student Grade System

Let us see encapsulation solving a real problem: protecting a student's grade so that no invalid score can be saved.

```python
class Student:
    def __init__(self, name):
        self.name = name
        self.__grade = 0          # Private grade, starts at 0

    def set_grade(self, grade):
        if 0 <= grade <= 100:     # Grade must be between 0 and 100
            self.__grade = grade
        else:
            print("Grade must be between 0 and 100!")

    def get_grade(self):
        return self.__grade

    def get_status(self):
        if self.__grade >= 50:    # Nigerian passing mark
            return "Passed"
        else:
            return "Failed"

# Testing the Student class
student = Student("Babajide")
student.set_grade(78)
print(f"Name: {student.name}")
print(f"Grade: {student.get_grade()}")
print(f"Status: {student.get_status()}")

student.set_grade(120)           # Invalid — should be rejected
print(f"Grade after invalid attempt: {student.get_grade()}")  # Still 78
```

**Expected output in terminal:**
```
Name: Babajide
Grade: 78
Status: Passed
Grade must be between 0 and 100!
Grade after invalid attempt: 78
```

> **Real-world connection:** School management systems, university portals (like JUPEB or JAMB), and hospital patient record systems all use encapsulation to prevent invalid data from entering their databases.

---

### 1.9 Private Methods — Hiding Internal Logic

Just like private properties, you can also make **methods** private. A private method can only be called from inside the class itself — not from outside.

**Why would you want this?** Sometimes a method is just a helper that does internal work that outside code should never call directly. Think of it as a factory machine's internal gears — the public only presses the button (public method), not the individual gears (private methods).

```python
class Calculator:
    def __init__(self):
        self.result = 0

    def __validate(self, num):         # Private method — only used inside the class
        if not isinstance(num, (int, float)):
            return False               # Not a valid number
        return True

    def add(self, num):                # Public method — anyone can call this
        if self.__validate(num):       # Calls the private validator internally
            self.result += num
        else:
            print(f"Invalid input: {num} is not a number!")

# Using the Calculator
calc = Calculator()
calc.add(10)
calc.add(5.5)
calc.add("hello")         # Invalid — will be caught
print(calc.result)        # Should be 15.5

# Trying to call the private method directly
calc.__validate(5)        # This will CAUSE AN ERROR
```

**Expected output in terminal:**
```
Invalid input: hello is not a number!
15.5
AttributeError: 'Calculator' object has no attribute '__validate'
```

The `__validate` method is invisible from outside the class — exactly as intended.

---

### 1.10 Name Mangling — The Secret Behind `__`

You now know that `__age` causes an `AttributeError` when accessed from outside the class. But here is an interesting technical detail: Python does NOT delete `__age`. Instead, it **renames it** automatically.

When you write `__age` inside a class called `Person`, Python secretly renames it to `_Person__age`. This is called **name mangling**.

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.__age = age          # Python internally stores this as _Person__age

p1 = Person("Kemi", 30)

# Normal access — causes an error
# print(p1.__age)               # AttributeError

# Name mangling — accessing the renamed version (NOT recommended!)
print(p1._Person__age)           # This works, but it is bad practice
```

**Expected output in terminal:**
```
30
```

> **Important:** Even though name mangling lets you access `_Person__age`, you should **never** do this in real code. It defeats the entire purpose of encapsulation. The rule exists only so Python's own internal systems (like inheritance) can still function properly.

---

### 1.11 Summary: Why Use Encapsulation?

| Benefit | Explanation |
|---|---|
| **Data Protection** | Private data cannot be changed accidentally from outside |
| **Validation** | Setters can reject invalid values before they are stored |
| **Flexibility** | You can change internal logic later without breaking external code |
| **Control** | You decide exactly what outside code is allowed to see and change |

---

## Part 2: Python Inner Classes

---

### 2.1 What Is an Inner Class?

An **inner class** is a class that is defined **inside** another class.

Think of it like a house (outer class) that contains rooms (inner classes). The rooms exist inside the house and belong to it. Rooms are not visible from the street — you have to enter the house first.

**Why do inner classes exist?**

When a class is only useful inside one specific class and nowhere else, it makes sense to define it *inside* that class. This keeps your code organised and makes it clear that the inner class is a private helper belonging to the outer class.

---

### 2.2 Defining a Basic Inner Class

```python
class Outer:
    def __init__(self):
        self.name = "I am the Outer Class"

    class Inner:                           # Inner class defined inside Outer
        def __init__(self):
            self.name = "I am the Inner Class"

        def display(self):
            print("Hello from the inner class!")

# Create an object of the outer class
outer = Outer()
print(outer.name)    # Access the outer class property directly
```

**Expected output in terminal:**
```
I am the Outer Class
```

Notice that printing `outer.name` only gives us the outer class's name. The inner class has not been used yet — it is just defined, waiting to be accessed.

---

### 2.3 Accessing the Inner Class from Outside

To use the inner class, you first create an outer object, then use that outer object to create an inner object.

```python
class Outer:
    def __init__(self):
        self.name = "Outer"

    class Inner:
        def __init__(self):
            self.name = "Inner"

        def display(self):
            print("Hello from the inner class!")

# Step 1: Create an object of the outer class
outer = Outer()

# Step 2: Use the outer object to create an inner class object
inner = outer.Inner()    # Note the syntax: outer_object.InnerClassName()

# Step 3: Now use the inner object normally
inner.display()
print(inner.name)
```

**Expected output in terminal:**
```
Hello from the inner class!
Inner
```

Line by line:
- `outer = Outer()` — creates the outer object as usual
- `inner = outer.Inner()` — creates an inner class object; notice we access `Inner` through the outer object
- `inner.display()` — calls the method on the inner object

---

### 2.4 Passing the Outer Object to the Inner Class

By default, an inner class **cannot** automatically see the outer class's properties. If you want the inner class to access the outer class's data, you must **pass the outer object in** as a parameter.

```python
class Outer:
    def __init__(self):
        self.name = "Emeka"           # Outer property

    class Inner:
        def __init__(self, outer):    # Accept the outer object as parameter
            self.outer = outer        # Store the reference

        def display(self):
            print(f"The outer class name is: {self.outer.name}")  # Access outer data

# Create outer object
outer = Outer()

# Pass the outer object into the inner class
inner = outer.Inner(outer)    # outer is passed as the argument

inner.display()
```

**Expected output in terminal:**
```
The outer class name is: Emeka
```

> **Think about it:** Why do you have to pass `outer` explicitly? Because unlike some other languages, Python inner classes do NOT automatically share a reference with their outer class. You must make the connection manually.

---

### 2.5 A Practical Example — Car and Engine

Inner classes are very useful when you have a "contains" relationship. For example, a car **contains** an engine. The engine on its own means nothing — it only makes sense inside a car.

```python
class Car:
    def __init__(self, brand, model):
        self.brand = brand
        self.model = model
        self.engine = self.Engine()    # Create an Engine object as part of the Car

    class Engine:
        def __init__(self):
            self.status = "Off"        # Engine starts off

        def start(self):
            self.status = "Running"
            print("Engine started!")

        def stop(self):
            self.status = "Off"
            print("Engine stopped!")

    def drive(self):
        if self.engine.status == "Running":
            print(f"Driving the {self.brand} {self.model}. Vroom!")
        else:
            print("Start the engine first!")

# Creating and using the Car
toyota = Car("Toyota", "Camry")

toyota.drive()              # Engine is off — cannot drive yet
toyota.engine.start()       # Start the engine
toyota.drive()              # Now we can drive
toyota.engine.stop()        # Stop engine
```

**Expected output in terminal:**
```
Start the engine first!
Engine started!
Driving the Toyota Camry. Vroom!
Engine stopped!
```

Notice how the `Engine` class is defined inside `Car`. From outside, you access it as `toyota.engine.start()`. This feels natural — you are saying "the car's engine, start."

---

### 2.6 Multiple Inner Classes

A single outer class can contain multiple inner classes.

```python
class Computer:
    def __init__(self):
        self.cpu = self.CPU()    # Create a CPU object
        self.ram = self.RAM()    # Create a RAM object

    class CPU:
        def process(self):
            print("CPU is processing data...")

    class RAM:
        def store(self):
            print("RAM is storing data temporarily...")

# Using the Computer
my_pc = Computer()
my_pc.cpu.process()
my_pc.ram.store()
```

**Expected output in terminal:**
```
CPU is processing data...
RAM is storing data temporarily...
```

This pattern is useful when modelling systems that have multiple distinct components — a computer with a CPU and RAM, a hospital with a Reception and a Laboratory, or an e-commerce order with a Cart and a Payment system.

---

### 2.7 A Nigerian Context Example — Hospital System

```python
class Hospital:
    def __init__(self, name, location):
        self.name = name
        self.location = location
        self.reception = self.Reception()
        self.lab = self.Laboratory()

    class Reception:
        def check_in(self, patient_name):
            print(f"Welcome, {patient_name}! Please take a seat.")

    class Laboratory:
        def run_test(self, test_name):
            print(f"Running {test_name} test. Please wait...")

# Using the Hospital system
lasuth = Hospital("LASUTH", "Ikeja, Lagos")
lasuth.reception.check_in("Adaeze Okafor")
lasuth.lab.run_test("Malaria Parasite")
```

**Expected output in terminal:**
```
Welcome, Adaeze Okafor! Please take a seat.
Running Malaria Parasite test. Please wait...
```

---

## Part 3: Python File Handling

---

### 3.1 Why File Handling Matters

So far, all the data in your programs disappears when the program stops running. Variables, lists, and class objects — they all live in the computer's memory and vanish when you close the program.

**File handling** solves this problem. It lets Python programs:

- Read data saved in `.txt`, `.csv`, or other files
- Save results and reports to files that persist after the program ends
- Process large datasets (like patient records, sales data, or school results) stored on disk

In the real world, file handling is used in every domain: banks process transaction logs, schools process result sheets, weather stations log temperature data, and mobile apps store user preferences.

---

### 3.2 The Four File Modes

When you open a file in Python, you must tell Python **what you intend to do** with it. This is called the **mode**.

| Mode | Symbol | Meaning |
|---|---|---|
| Read | `"r"` | Open file for reading. Error if file does not exist. (Default) |
| Append | `"a"` | Open file to add new content at the end. Creates file if missing. |
| Write | `"w"` | Open file to write (overwrite). Creates file if missing. |
| Create | `"x"` | Create a new file. Error if file already exists. |

There are also two format modes you can combine:

| Format | Symbol | Meaning |
|---|---|---|
| Text | `"t"` | Read or write as plain text. (Default) |
| Binary | `"b"` | Read or write as raw bytes (for images, PDFs, etc.) |

---

### 3.3 The `open()` Function — The Gateway to Files

The `open()` function is Python's built-in way to open any file.

**Syntax:**

```python
open(filename, mode)
```

The simplest usage:

```python
f = open("demofile.txt")          # Opens in read mode ("r") and text mode ("t") by default
```

This is exactly the same as:

```python
f = open("demofile.txt", "rt")    # "r" = read, "t" = text — these are the defaults
```

> **Important:** If the file does not exist when using `"r"` mode, Python raises a `FileNotFoundError`. Always make sure the file exists before reading it.

---

### 3.4 Reading a File — The `read()` Method

Once you have opened a file, use the `read()` method to get all of its contents as one big string.

**First, create the file to work with.** Imagine this file called `demofile.txt` exists in the same folder as your Python script, with these contents:

```
Hello! Welcome to demofile.txt
This file is for testing purposes.
Good Luck!
```

Now let us read it:

```python
f = open("demofile.txt")    # Open the file
content = f.read()           # Read ALL contents into a string
print(content)               # Print the contents
f.close()                    # Always close the file when done!
```

**Expected output in terminal:**
```
Hello! Welcome to demofile.txt
This file is for testing purposes.
Good Luck!
```

Line by line:
- `f = open("demofile.txt")` — opens the file and returns a **file object** stored in `f`
- `f.read()` — reads the entire content of the file as one string
- `print(content)` — displays the content
- `f.close()` — closes the file; very important! Unclosed files can waste resources or cause data loss

---

### 3.5 Reading a File from a Different Location

If the file is not in the same folder as your Python script, you must provide the full file path.

```python
# On Windows:
f = open("C:\\Users\\Babatunde\\Documents\\demofile.txt")
print(f.read())
f.close()

# On Mac/Linux:
f = open("/home/babatunde/Documents/demofile.txt")
print(f.read())
f.close()
```

> **Note:** On Windows, use double backslash `\\` or a raw string `r"C:\path\to\file.txt"` to avoid Python misreading the backslash as an escape character.

---

### 3.6 The `with` Statement — The Safe Way to Open Files

The safest and most Pythonic way to open files is using the `with` statement. When you use `with`, Python automatically closes the file for you when the block finishes — even if an error occurs.

```python
with open("demofile.txt") as f:     # File opens here
    content = f.read()               # Read the content
    print(content)
# File is automatically closed here — no need to call f.close()
```

**Expected output in terminal:**
```
Hello! Welcome to demofile.txt
This file is for testing purposes.
Good Luck!
```

> **Best Practice:** Always use the `with` statement when working with files. It is cleaner, safer, and prevents common mistakes like forgetting to close the file.

---

### 3.7 Reading a Specific Number of Characters

Instead of reading the whole file at once, you can tell `read()` exactly how many characters to return.

```python
with open("demofile.txt") as f:
    print(f.read(5))    # Read only the first 5 characters
```

**Expected output in terminal:**
```
Hello
```

"Hello" is the first 5 characters of `"Hello! Welcome to demofile.txt"`. The rest of the file is not touched.

Another example:

```python
with open("demofile.txt") as f:
    print(f.read(12))   # Read first 12 characters
```

**Expected output in terminal:**
```
Hello! Welcom
```

> **Think about it:** What would happen if you called `f.read(5)` twice in a row? Try to predict the answer before looking at the next section!

---

### 3.8 Reading One Line at a Time — The `readline()` Method

The `readline()` method reads one line from the file each time you call it.

**Reading one line:**

```python
with open("demofile.txt") as f:
    print(f.readline())    # Reads the first line
```

**Expected output in terminal:**
```
Hello! Welcome to demofile.txt
```

**Reading two lines:**

```python
with open("demofile.txt") as f:
    print(f.readline())    # First line
    print(f.readline())    # Second line
```

**Expected output in terminal:**
```
Hello! Welcome to demofile.txt
This file is for testing purposes.
```

Each call to `readline()` moves forward by one line. Think of it like a cursor that moves down the page one line at a time.

---

### 3.9 Reading All Lines — Looping Through the File

To read the entire file line by line (useful for processing large files), loop through the file object directly using a `for` loop.

```python
with open("demofile.txt") as f:
    for line in f:
        print(line)
```

**Expected output in terminal:**
```
Hello! Welcome to demofile.txt

This file is for testing purposes.

Good Luck!
```

> **Why are there blank lines between each line?** Each line in the file already ends with a newline character (`\n`). Then `print()` adds another newline by default. Use `print(line, end="")` to remove the extra blank lines.

```python
with open("demofile.txt") as f:
    for line in f:
        print(line, end="")    # end="" prevents double spacing
```

**Expected output in terminal:**
```
Hello! Welcome to demofile.txt
This file is for testing purposes.
Good Luck!
```

---

### 3.10 Closing Files Manually

If you are **not** using the `with` statement, you **must** close the file manually using `f.close()`.

```python
f = open("demofile.txt")
print(f.readline())
f.close()               # ALWAYS close the file when you are done
```

**Expected output in terminal:**
```
Hello! Welcome to demofile.txt
```

> **Why is closing important?** When a file is open, the operating system "locks" it in memory. Unclosed files waste memory, can cause data not to be saved properly, and may prevent other programs from accessing the same file. Always close files when you are done — or better, use `with` and let Python handle it.

---

## Guided Practice Exercises

---

### Exercise 1: Encapsulation — Building a Bank Account

**Objective:** Apply encapsulation to protect sensitive financial data.

**Scenario:** You are building a simple bank account system for First Bank Nigeria. The account balance must be private. No one should be able to directly change the balance — all deposits and withdrawals must go through validated methods.

**Steps:**

1. Create a `BankAccount` class with:
   - A public property: `owner` (the account holder's name)
   - A private property: `__balance` (starting balance)
2. Add a getter `get_balance()` that returns the balance
3. Add a method `deposit(amount)` that adds to the balance (reject amounts ≤ 0)
4. Add a method `withdraw(amount)` that subtracts from the balance (reject if amount > balance or ≤ 0)
5. Test your class with deposits and withdrawals

**Hint:** Use `if amount > 0` to validate before changing `__balance`.

**Solution:**

```python
class BankAccount:
    def __init__(self, owner, initial_balance):
        self.owner = owner
        self.__balance = initial_balance    # Private — cannot be changed directly

    def get_balance(self):
        return self.__balance

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount
            print(f"Deposited ₦{amount:,}. New balance: ₦{self.__balance:,}")
        else:
            print("Deposit amount must be greater than zero!")

    def withdraw(self, amount):
        if amount <= 0:
            print("Withdrawal amount must be greater than zero!")
        elif amount > self.__balance:
            print("Insufficient funds!")
        else:
            self.__balance -= amount
            print(f"Withdrew ₦{amount:,}. New balance: ₦{self.__balance:,}")

# Testing the BankAccount
account = BankAccount("Ngozi Adeyemi", 100000)
print(f"Account owner: {account.owner}")
print(f"Opening balance: ₦{account.get_balance():,}")

account.deposit(50000)
account.withdraw(20000)
account.withdraw(200000)     # Should fail — insufficient funds
account.deposit(-5000)       # Should fail — invalid amount
print(f"Final balance: ₦{account.get_balance():,}")
```

**Expected output in terminal:**
```
Account owner: Ngozi Adeyemi
Opening balance: ₦100,000
Deposited ₦50,000. New balance: ₦150,000
Withdrew ₦20,000. New balance: ₦130,000
Insufficient funds!
Deposit amount must be greater than zero!
Final balance: ₦130,000
```

**Self-check questions:**
- What happens if you try `account.__balance`? Why?
- Could you change the balance to `999999999` without going through `deposit()`? Why not?
- What makes `deposit()` and `withdraw()` better than direct access?

---

### Exercise 2: Inner Classes — University Department System

**Objective:** Use inner classes to model a university with departments.

**Scenario:** University of Lagos (UNILAG) needs a class to represent a department. Each department has a `Lecturer` inner class and a `Course` inner class.

**Steps:**

1. Create a `Department` class with properties: `name` and `faculty`
2. Create an inner class `Lecturer` with: `lecturer_name` and a `teach()` method
3. Create an inner class `Course` with: `course_title`, `course_code`, and a `describe()` method
4. Pass the outer `Department` object to `Lecturer` so the lecturer knows which department they belong to
5. Create a Department, some Lecturers, and some Courses, and print information about them

**Solution:**

```python
class Department:
    def __init__(self, name, faculty):
        self.name = name
        self.faculty = faculty

    class Lecturer:
        def __init__(self, lecturer_name, outer_dept):
            self.lecturer_name = lecturer_name
            self.department = outer_dept       # Reference to the outer class

        def teach(self):
            print(f"Dr. {self.lecturer_name} is teaching in the {self.department.name} department.")

    class Course:
        def __init__(self, course_title, course_code):
            self.course_title = course_title
            self.course_code = course_code

        def describe(self):
            print(f"Course: {self.course_title} ({self.course_code})")

# Creating the Department
cs_dept = Department("Computer Science", "Science and Technology")

# Creating Lecturers (passing the outer department object)
lecturer1 = cs_dept.Lecturer("Adewale Ogundimu", cs_dept)
lecturer2 = cs_dept.Lecturer("Fatima Bello", cs_dept)

# Creating Courses
course1 = cs_dept.Course("Introduction to Python", "CSC 101")
course2 = cs_dept.Course("Data Structures", "CSC 202")

# Using everything
lecturer1.teach()
lecturer2.teach()
course1.describe()
course2.describe()
```

**Expected output in terminal:**
```
Dr. Adewale Ogundimu is teaching in the Computer Science department.
Dr. Fatima Bello is teaching in the Computer Science department.
Course: Introduction to Python (CSC 101)
Course: Data Structures (CSC 202)
```

---

### Exercise 3: File Reading — Student Results Processor

**Objective:** Practice reading a file line by line and processing each line.

**Scenario:** Your school in Abuja keeps student results in a text file called `results.txt`. You need to read it and display each student's result.

**Step 1:** First create the file. In your terminal or text editor, create `results.txt` with this content:

```
Adaobi Nwosu: 85
Kayode Fashola: 72
Zainab Musa: 91
Emeka Obi: 65
Halima Yusuf: 55
```

**Step 2:** Write Python to read and process this file.

**Steps:**

1. Open `results.txt` using a `with` statement
2. Loop through the file line by line
3. Print each line cleanly (remove extra spaces with `.strip()`)
4. Identify students who passed (score ≥ 50) and who failed

**Solution:**

```python
# Reading and processing student results

print("=== STUDENT RESULTS ===\n")

with open("results.txt") as f:
    for line in f:
        line = line.strip()          # Remove any leading/trailing whitespace or newlines
        if line:                     # Only process non-empty lines
            # Split at the colon to get name and score
            parts = line.split(": ")
            name = parts[0]
            score = int(parts[1])

            if score >= 50:
                status = "PASSED"
            else:
                status = "FAILED"

            print(f"{name}: {score}/100 — {status}")
```

**Expected output in terminal:**
```
=== STUDENT RESULTS ===

Adaobi Nwosu: 85/100 — PASSED
Kayode Fashola: 72/100 — PASSED
Zainab Musa: 91/100 — PASSED
Emeka Obi: 65/100 — PASSED
Halima Yusuf: 55/100 — PASSED
```

**Self-check questions:**
- What does `.strip()` do? What would happen without it?
- Why does the loop not need `f.close()`?
- How would you change the passing mark to 60?

---

## Mini Project: Student Profile Management System

In this project, you will combine encapsulation, inner classes, and file reading to build a simple student management system.

---

### Project Overview

You will create a `School` class that:
- Has a private `__school_name` property (encapsulation)
- Contains a `Student` inner class with private `__grade` (encapsulation within inner class)
- Loads student data from a file and displays a formatted report

---

### Stage 1 — Setup: Build the Core Classes

```python
class School:
    def __init__(self, school_name, location):
        self.__school_name = school_name    # Private
        self.location = location

    def get_school_name(self):
        return self.__school_name

    class Student:
        def __init__(self, name, student_id):
            self.name = name
            self.student_id = student_id
            self.__grade = 0                # Private

        def set_grade(self, grade):
            if 0 <= grade <= 100:
                self.__grade = grade
            else:
                print(f"Invalid grade for {self.name}!")

        def get_grade(self):
            return self.__grade

        def get_status(self):
            if self.__grade >= 50:
                return "PASSED"
            return "FAILED"

        def display(self):
            print(f"  ID: {self.student_id} | Name: {self.name} | "
                  f"Grade: {self.__grade}/100 | Status: {self.get_status()}")
```

**Milestone 1 checkpoint:** Create a School and two Student objects manually and call `display()` on each.

```python
school = School("Government Secondary School", "Abuja")
print(f"\nSchool: {school.get_school_name()}, {school.location}\n")

s1 = school.Student("Amara Eze", "SS001")
s1.set_grade(78)
s1.display()

s2 = school.Student("Musa Aliyu", "SS002")
s2.set_grade(45)
s2.display()
```

**Expected output in terminal:**
```
School: Government Secondary School, Abuja

  ID: SS001 | Name: Amara Eze | Grade: 78/100 | Status: PASSED
  ID: SS002 | Name: Musa Aliyu | Grade: 45/100 | Status: FAILED
```

---

### Stage 2 — Enhancement: Load Students from a File

Create a file called `students.txt` with this content:

```
SS001,Amara Eze,78
SS002,Musa Aliyu,45
SS003,Chidinma Okafor,92
SS004,Yusuf Garba,38
SS005,Blessing Okonkwo,65
```

Now add a method to `School` that reads this file and builds a list of Student objects:

```python
    def load_students_from_file(self, filename):
        students = []
        with open(filename) as f:
            for line in f:
                line = line.strip()
                if line:
                    parts = line.split(",")
                    student_id = parts[0]
                    name = parts[1]
                    grade = int(parts[2])

                    student = self.Student(name, student_id)
                    student.set_grade(grade)
                    students.append(student)
        return students
```

---

### Stage 3 — Final Output: Generate a Full Report

```python
school = School("Government Secondary School", "Abuja")
print(f"\n{'='*50}")
print(f"  SCHOOL: {school.get_school_name()}")
print(f"  LOCATION: {school.location}")
print(f"{'='*50}")

students = school.load_students_from_file("students.txt")

print("\nSTUDENT RESULTS REPORT:")
print("-" * 50)

passed = 0
failed = 0

for student in students:
    student.display()
    if student.get_status() == "PASSED":
        passed += 1
    else:
        failed += 1

print("-" * 50)
print(f"\nTotal Students: {len(students)}")
print(f"Passed: {passed}")
print(f"Failed: {failed}")
print(f"Pass Rate: {(passed/len(students))*100:.1f}%")
```

**Expected output in terminal:**
```
==================================================
  SCHOOL: Government Secondary School
  LOCATION: Abuja
==================================================

STUDENT RESULTS REPORT:
--------------------------------------------------
  ID: SS001 | Name: Amara Eze | Grade: 78/100 | Status: PASSED
  ID: SS002 | Name: Musa Aliyu | Grade: 45/100 | Status: FAILED
  ID: SS003 | Name: Chidinma Okafor | Grade: 92/100 | Status: PASSED
  ID: SS004 | Name: Yusuf Garba | Grade: 38/100 | Status: FAILED
  ID: SS005 | Name: Blessing Okonkwo | Grade: 65/100 | Status: PASSED
--------------------------------------------------

Total Students: 5
Passed: 3
Failed: 2
Pass Rate: 60.0%
```

**Reflection questions:**
- What would happen if `__grade` was public and a bug set it to `500`?
- Why is the `Student` class defined as an inner class of `School` rather than a separate class?
- What other data might a real school system want to load from a file?

**Optional extension:** Add a `highest_scorer()` method to `School` that returns the name of the student with the highest grade.

---

## Common Beginner Mistakes

---

### Mistake 1: Trying to access a private property directly

**Wrong:**
```python
class Person:
    def __init__(self, age):
        self.__age = age

p = Person(25)
print(p.__age)    # AttributeError!
```

**Correct:**
```python
class Person:
    def __init__(self, age):
        self.__age = age

    def get_age(self):
        return self.__age   # Use a getter

p = Person(25)
print(p.get_age())    # Works correctly
```

---

### Mistake 2: Confusing `_` (single underscore) with `__` (double underscore)

**Common confusion:** Students think `_salary` is the same as `__salary`. They are not. Single underscore is a convention with no enforcement. Double underscore triggers name mangling.

```python
class Staff:
    def __init__(self, salary):
        self._salary = salary     # Only a convention — still accessible
        self.__secret = "hidden"  # Enforced — triggers name mangling

s = Staff(50000)
print(s._salary)    # Works (just a warning to developers)
print(s.__secret)   # AttributeError
```

---

### Mistake 3: Forgetting to pass the outer object to the inner class

**Wrong:**
```python
class Outer:
    def __init__(self):
        self.city = "Lagos"

    class Inner:
        def show(self):
            print(self.city)   # ERROR — Inner doesn't know about 'city'

o = Outer()
i = o.Inner()
i.show()    # AttributeError
```

**Correct:**
```python
class Outer:
    def __init__(self):
        self.city = "Lagos"

    class Inner:
        def __init__(self, outer):
            self.outer = outer       # Store the outer reference

        def show(self):
            print(self.outer.city)   # Access through the stored reference

o = Outer()
i = o.Inner(o)    # Pass the outer object
i.show()          # Lagos
```

---

### Mistake 4: Forgetting to close a file (when not using `with`)

**Wrong:**
```python
f = open("myfile.txt")
print(f.read())
# Forgot to close! Bad practice.
```

**Correct Option A — Manual close:**
```python
f = open("myfile.txt")
print(f.read())
f.close()    # Always close
```

**Correct Option B — Using `with` (recommended):**
```python
with open("myfile.txt") as f:
    print(f.read())
# Automatically closed — no need to call f.close()
```

---

### Mistake 5: Reading a file that does not exist

**Wrong:**
```python
f = open("missing_file.txt")    # FileNotFoundError if the file doesn't exist
```

**Correct:** Always check the file exists, or handle the error:
```python
try:
    with open("missing_file.txt") as f:
        print(f.read())
except FileNotFoundError:
    print("Sorry, the file was not found. Please check the filename.")
```

---

### Mistake 6: Double-spacing in output when reading lines

**Wrong (double spacing):**
```python
with open("myfile.txt") as f:
    for line in f:
        print(line)    # Each line already has \n, and print adds another
```

**Correct:**
```python
with open("myfile.txt") as f:
    for line in f:
        print(line, end="")    # Prevents the extra blank line
        # OR
        print(line.strip())    # Strips the \n before printing
```

---

## Reflection Questions

Take a moment to think through these:

1. If you remove the double underscore from `__grade` in a Student class, what risk does this create? Can you think of a real-world scenario where this goes badly wrong?

2. You have a `Hospital` outer class with a `Patient` inner class and a `Doctor` inner class. Why would `Patient` be a good inner class rather than a standalone class?

3. The `with` statement automatically closes files. Why do you think Python was designed to make this the recommended approach rather than relying on programmers to remember `f.close()`?

4. What is the difference between `f.read()` and `f.readline()`? When would you choose one over the other?

5. Could you use encapsulation in a file-reading context? For example, could you build a class that reads a file but keeps its internal file handle private? What benefits would this have?

---

## Completion Checklist

Before moving to the next lesson, confirm you can:

- [ ] Explain encapsulation in your own words using a real-life analogy
- [ ] Create a class with a private property using `__`
- [ ] Write a getter method that returns a private property's value
- [ ] Write a setter method that validates input before updating a private property
- [ ] Explain what name mangling is and why it exists
- [ ] Create an inner class inside an outer class
- [ ] Access an inner class object from outside the outer class
- [ ] Pass an outer object into an inner class to share data
- [ ] Open a file using both `open()` with manual `close()` and the `with` statement
- [ ] Read a file's full content using `f.read()`
- [ ] Read a specific number of characters using `f.read(n)`
- [ ] Read one line at a time using `f.readline()`
- [ ] Loop through a file line by line
- [ ] Explain the four file opening modes: `r`, `a`, `w`, `x`

---

## Lesson Summary

This lesson covered three important Python skills that work powerfully together:

**Encapsulation** protects your class's data by marking properties as private (`__`) or protected (`_`). Getter methods read private data safely, and setter methods change it with built-in validation. This prevents bugs, accidental corruption, and invalid values from entering your system. Python implements privacy through **name mangling** — renaming `__attr` to `_ClassName__attr` internally.

**Inner Classes** are classes defined inside other classes. They are useful when a class is only meaningful in the context of its parent class. You must create an outer object first, then use it to create inner objects (`outer.Inner()`). To let the inner class access the outer class's data, you pass the outer object as a parameter. Multiple inner classes can exist inside one outer class.

**File Handling** lets Python work with files stored on disk. The `open()` function opens a file and returns a file object. The four main modes are read (`r`), append (`a`), write (`w`), and create (`x`). The safest way to open files is using the `with` statement, which auto-closes the file. You can read all content at once (`read()`), read a set number of characters (`read(n)`), or read one line at a time (`readline()` or a `for` loop).

---

## Quick Reference Card

```
ENCAPSULATION
─────────────────────────────────────────
Public property:    self.name = value
Protected property: self._name = value     (convention only)
Private property:   self.__name = value    (enforced by Python)

Getter:  def get_name(self): return self.__name
Setter:  def set_name(self, val):
             if valid: self.__name = val
             else: print("Error!")

Name mangling: __age → _ClassName__age

─────────────────────────────────────────
INNER CLASSES
─────────────────────────────────────────
class Outer:
    class Inner:
        def method(self): ...

outer = Outer()
inner = outer.Inner()          # Access inner class via outer object
inner.method()

# Sharing outer data with inner:
class Inner:
    def __init__(self, outer):
        self.outer = outer
inner = outer.Inner(outer)     # Pass outer object explicitly

─────────────────────────────────────────
FILE MODES
─────────────────────────────────────────
"r"  → Read (default)
"a"  → Append
"w"  → Write (overwrite)
"x"  → Create new file

"t"  → Text mode (default)
"b"  → Binary mode

─────────────────────────────────────────
FILE READING
─────────────────────────────────────────
# Open and read all
with open("file.txt") as f:
    print(f.read())

# Read specific characters
with open("file.txt") as f:
    print(f.read(10))

# Read one line
with open("file.txt") as f:
    print(f.readline())

# Read all lines (loop)
with open("file.txt") as f:
    for line in f:
        print(line.strip())

# Manual open and close
f = open("file.txt")
print(f.read())
f.close()
─────────────────────────────────────────
```
