---
render_with_liquid: false
title: "Python Object-Oriented Programming: Classes, Objects, __init__, and self"
nav_order: 20
---

# Lesson 20: Python Object-Oriented Programming — Classes, Objects, `__init__`, and `self`

---

## Lesson Introduction

Welcome to one of the most important lessons in your Python journey! By the end of this lesson, you will understand **Object-Oriented Programming (OOP)** — the style of writing code that is used in virtually every professional Python project in the world.

You will learn:
- What OOP is and **why** it exists
- What a **class** is and how to create one
- What an **object** is and how to create one from a class
- What the `__init__()` method does and why it is so important
- What `self` means and how it connects everything together

This is a big idea, but we will break it down one small step at a time. No prior knowledge of OOP is needed. Let's go!

---

## Prerequisite Concepts

Before diving into OOP, make sure you are comfortable with the following ideas. If any of these are new to you, read through the short explanation provided.

**Variables** — A variable stores a value in memory. Example: `name = "Alice"` stores the text `"Alice"` with the label `name`.

**Functions** — A function is a block of reusable code. Example:
```python
def say_hello():
    print("Hello!")
```

**Calling a function** — Running a function by writing its name followed by parentheses: `say_hello()`

**Passing arguments** — Giving information to a function when you call it: `greet("Alice")`

If you feel confident with those ideas, you are ready to begin.

---

## Part 1: What is Object-Oriented Programming (OOP)?

### Why Does OOP Exist?

Imagine you are building a school management system. You need to keep track of hundreds of students. Each student has a name, age, grade, and scores. Without OOP, you might write something like this:

```python
student1_name = "Amara"
student1_age = 14
student1_grade = "JSS2"

student2_name = "Emeka"
student2_age = 15
student2_grade = "JSS3"
```

This gets messy very quickly. What if you have 500 students? You would need 1,500 separate variables. Finding, changing, or using any student's data becomes a nightmare.

**OOP solves this problem** by letting you create a single "template" (called a **class**) that describes what a student looks like, and then produce as many individual students (called **objects**) as you need — each with their own data stored neatly inside them.

> **Analogy:** Think of a **class** as a **cookie cutter** and **objects** as the individual **cookies** made from that cutter. Every cookie has the same shape (from the same cutter), but each one can have different decorations (its own data).

### What Does OOP Give You?

OOP provides a **clear structure** to programs. It makes code:
- **Easier to maintain** — you fix one class, and all objects benefit
- **Easier to reuse** — you use the same class in many places
- **Easier to read** — code mirrors how the real world works

OOP also follows the **DRY principle** — **Don't Repeat Yourself**. Instead of writing the same logic over and over, you write it once inside a class and reuse it.

**Real-world connection:** Every modern software system uses OOP. When you use a banking app, each bank account is an object. When you shop online, each product in your cart is an object. When you play a video game, each character is an object.

---

## Part 2: Classes and Objects

### What is a Class?

A **class** is a **blueprint** or **template**. It defines what data an object will hold and what actions an object can perform.

Think of it this way:

| Class (Blueprint) | Objects (Real Things Made from It) |
|---|---|
| `Fruit` | Apple, Banana, Mango |
| `Car` | Toyota Camry, Honda Civic, Kia Rio |
| `Student` | Amara, Emeka, Fatima |
| `BankAccount` | Account #001, Account #002, Account #003 |

The **class** describes the category. The **objects** are the actual specific things.

### How to Create a Class

In Python, you create a class using the keyword `class`, followed by the name of the class (starting with a capital letter by convention), and a colon `:`.

```python
class MyClass:
    x = 5
```

Let's break this down line by line:

- `class` — this keyword tells Python: "I am about to define a class"
- `MyClass` — this is the name we give to our class (capital letter is the convention)
- `:` — the colon marks the beginning of the class body
- `x = 5` — this is a **property** (a variable that belongs to the class), with the value `5`

**Expected Output:** Nothing yet — defining a class doesn't produce output. It just creates the blueprint.

### What is an Object?

An **object** is a specific instance created from a class. It is the real "thing" built using the blueprint.

To create an object, you write the class name followed by parentheses `()`, just like calling a function:

```python
class MyClass:
    x = 5

p1 = MyClass()    # p1 is now an object created from MyClass
print(p1.x)       # access the property x of p1
```

**Expected Output:**
```
5
```

Let's trace through what happened:
- `MyClass()` — Python reads the class blueprint and creates a new object
- `p1 = MyClass()` — we store that object in the variable `p1`
- `p1.x` — we access the property `x` that belongs to `p1`
- The `.` (dot) is the way we access properties and methods of an object

> **Thinking Prompt:** What do you think would happen if you typed `print(p1.y)`? There is no `y` defined in the class — Python would raise an `AttributeError`. Try it!

### Creating Multiple Objects from the Same Class

One of the greatest powers of OOP is that you can create as many objects as you need from a single class. Each object is completely independent.

```python
class MyClass:
    x = 5

p1 = MyClass()
p2 = MyClass()
p3 = MyClass()

print(p1.x)
print(p2.x)
print(p3.x)
```

**Expected Output:**
```
5
5
5
```

All three objects have their own copy of `x`. Each object is independent — changing one does not change the others.

### Deleting an Object

You can remove an object from memory using the `del` keyword:

```python
class MyClass:
    x = 5

p1 = MyClass()
print(p1.x)   # works fine

del p1        # delete the object

# print(p1.x)  # this would now cause an error: NameError
```

**Expected Output:**
```
5
```

After `del p1`, the variable `p1` no longer exists. Trying to use it would raise a `NameError`.

### The `pass` Statement in Classes

A class definition cannot be completely empty — Python will give you an error. But sometimes you want to create a class as a placeholder for later. Use `pass` to create a valid empty class:

```python
class Person:
    pass   # pass means "do nothing, but this is valid"
```

`pass` is Python's way of saying: "I know this block is empty. That's intentional." It prevents errors in empty code blocks.

---

## Part 3: The `__init__()` Method

### The Problem: Every Object Looks the Same

With what we know so far, every object from `MyClass` has `x = 5`. But in real life, different students have different names, different cars have different brands. How do we give each object **its own unique data** when we create it?

The answer is the `__init__()` method.

### What is `__init__()`?

`__init__()` is a **special method** built into Python. The name has double underscores on both sides (called **dunder** — "double under"). It is sometimes called the **constructor**.

`__init__()` is **called automatically** every time you create a new object from a class. It runs immediately at the moment of object creation.

> **Analogy:** Think of `__init__()` as the **birth certificate form** that gets filled out automatically the moment a new object is "born". Every time you create a new `Person` object, Python automatically runs `__init__()` and fills in that person's name, age, and other details.

### Why Use `__init__()`?

Without `__init__()`, you would have to set properties one by one after creating the object — slow, repetitive, and easy to forget:

```python
# Without __init__() — the hard, repetitive way
class Person:
    pass

p1 = Person()
p1.name = "Tobias"
p1.age = 25

print(p1.name)
print(p1.age)
```

**Expected Output:**
```
Tobias
25
```

This works, but imagine doing this for 100 students. And what if you forget to set the `age` for one of them? Errors everywhere.

With `__init__()`, you set everything in one clean step:

```python
# With __init__() — the clean, professional way
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

p1 = Person("Emil", 36)

print(p1.name)
print(p1.age)
```

**Expected Output:**
```
Emil
36
```

### Breaking Down the `__init__()` Code Line by Line

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
```

- `def __init__(self, name, age):` — defines the `__init__` method. It takes three parameters: `self` (explained in the next section), `name`, and `age`
- `self.name = name` — stores the value passed as `name` into this object's own property called `name`
- `self.age = age` — stores the value passed as `age` into this object's own property called `age`

```python
p1 = Person("Emil", 36)
```

- `Person("Emil", 36)` — creates a new `Person` object and automatically calls `__init__()` with `name = "Emil"` and `age = 36`
- `p1` — the new object is stored in `p1`

```python
print(p1.name)   # "Emil"
print(p1.age)    # 36
```

`p1.name` goes to `p1`'s personal storage and retrieves the name we gave it.

> **Thinking Prompt:** What happens if you write `p1 = Person("Emil")` — leaving out the age? Python will give a `TypeError` because `__init__()` expects both `name` and `age`.

### Creating Multiple Objects with Different Data

Now the power becomes clear:

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

p1 = Person("Amara", 14)
p2 = Person("Emeka", 15)
p3 = Person("Fatima", 13)

print(p1.name, p1.age)
print(p2.name, p2.age)
print(p3.name, p3.age)
```

**Expected Output:**
```
Amara 14
Emeka 15
Fatima 13
```

Three students, each with their own individual data, all from the same class. No repetitive variable names. Clean, organised, professional.

### Default Values in `__init__()`

You can give parameters **default values** so that if the caller doesn't provide one, it falls back to the default:

```python
class Person:
    def __init__(self, name, age=18):   # age defaults to 18
        self.name = name
        self.age = age

p1 = Person("Emil")           # age not given, uses default 18
p2 = Person("Tobias", 25)    # age given, uses 25

print(p1.name, p1.age)
print(p2.name, p2.age)
```

**Expected Output:**
```
Emil 18
Tobias 25
```

- `p1` didn't get an age, so it used the default `18`
- `p2` got `25`, which overrode the default

> **Thinking Prompt:** What would happen if you switched the order and put `def __init__(self, age=18, name):`? Python would raise a `SyntaxError` — parameters with defaults must always come **after** parameters without defaults.

### Multiple Parameters in `__init__()`

`__init__()` can accept as many parameters as you need:

```python
class Person:
    def __init__(self, name, age, city, country):
        self.name = name
        self.age = age
        self.city = city
        self.country = country

p1 = Person("Linus", 30, "Lagos", "Nigeria")

print(p1.name)
print(p1.age)
print(p1.city)
print(p1.country)
```

**Expected Output:**
```
Linus
30
Lagos
Nigeria
```

Each piece of data is stored inside the object and accessible through the dot notation (`p1.city`, etc.).

---

## Part 4: The `self` Parameter

### What is `self`?

`self` is the first parameter you see in almost every method inside a class. It is a **reference to the current object** — the specific instance that the method is being called on.

In plain English: `self` means **"this particular object right now"**.

> **Analogy:** Imagine a class is a job description for an employee. The job description says "The employee will introduce themselves by name." But when an actual employee (an object) follows that description, `self` is that specific employee. When Amara introduces herself, `self` is Amara. When Emeka introduces himself, `self` is Emeka.

### Why Does `self` Exist?

Python needs `self` to know **which object's data** to use when a method is called. Without `self`, a method inside a class would have no way to access the properties of a specific object.

Here's the point illustrated clearly:

```python
class Person:
    def __init__(self, name):
        self.name = name    # store name in THIS object

    def printname(self):
        print(self.name)    # print THIS object's name

p1 = Person("Tobias")
p2 = Person("Linus")

p1.printname()    # self refers to p1 here
p2.printname()    # self refers to p2 here
```

**Expected Output:**
```
Tobias
Linus
```

When you call `p1.printname()`, Python automatically passes `p1` as `self`. So `self.name` becomes `p1.name` which is `"Tobias"`. When you call `p2.printname()`, `self` becomes `p2`, so `self.name` is `"Linus"`.

This is how Python knows which object's data to work with!

### `self` Must Always Be First

`self` must always be the **first parameter** of any method defined inside a class. You cannot skip it or move it elsewhere.

```python
class Person:
    def __init__(self, name, age):    # self is first
        self.name = name
        self.age = age

    def greet(self):                  # self is first here too
        print("Hello, my name is " + self.name)

p1 = Person("Emil", 25)
p1.greet()
```

**Expected Output:**
```
Hello, my name is Emil
```

Notice that when you **call** `p1.greet()`, you do NOT pass `self` yourself. Python fills it in automatically. But when you **define** the method, `self` must be there.

### Using `self` to Access Properties

`self` lets you reach into the object and retrieve or modify any property:

```python
class Car:
    def __init__(self, brand, model, year):
        self.brand = brand
        self.model = model
        self.year = year

    def display_info(self):
        print(f"{self.year} {self.brand} {self.model}")

car1 = Car("Toyota", "Corolla", 2020)
car1.display_info()
```

**Expected Output:**
```
2020 Toyota Corolla
```

Inside `display_info`, `self.year`, `self.brand`, and `self.model` all refer to the specific car that called the method.

### Using `self` to Call Other Methods

You can use `self` to call one method from inside another method of the same class:

```python
class Person:
    def __init__(self, name):
        self.name = name

    def greet(self):
        return "Hello, " + self.name

    def welcome(self):
        message = self.greet()         # calling greet() from welcome()
        print(message + "! Welcome to our website.")

p1 = Person("Tobias")
p1.welcome()
```

**Expected Output:**
```
Hello, Tobias! Welcome to our website.
```

`self.greet()` calls the `greet` method on the same object (`p1`), which returns the greeting string, which is then used in `welcome`.

### Can `self` Be Named Something Else?

Technically, yes — `self` is just a convention. Python does not enforce the name. You could use any valid variable name:

```python
class Person:
    def __init__(myobject, name, age):   # using "myobject" instead
        myobject.name = name
        myobject.age = age

    def greet(abc):                      # using "abc" instead
        print("Hello, my name is " + abc.name)

p1 = Person("Emil", 36)
p1.greet()
```

**Expected Output:**
```
Hello, my name is Emil
```

This works exactly the same. BUT — **never actually do this in real code**. Using `self` is a universal Python convention. Every Python programmer expects to see `self`. Using something else makes your code confusing and harder for others (and your future self) to read. Always use `self`.

---

## Guided Practice Exercises

### Exercise 1 — Warm-Up: Build a Simple Dog Class

**Objective:** Practice creating a class and objects with `__init__()`.

**Scenario:** You are building a pet registration system. Create a `Dog` class.

**Steps:**
1. Create a class called `Dog`
2. Add `__init__()` that accepts `name` and `breed`
3. Store both values using `self`
4. Create two Dog objects with different names and breeds
5. Print both dogs' names and breeds

**Starter code:**
```python
class Dog:
    def __init__(self, name, breed):
        # your code here

dog1 = Dog("Rex", "German Shepherd")
dog2 = Dog("Bella", "Labrador")

# print dog1's name and breed
# print dog2's name and breed
```

**Expected Output:**
```
Rex German Shepherd
Bella Labrador
```

**Solution:**
```python
class Dog:
    def __init__(self, name, breed):
        self.name = name
        self.breed = breed

dog1 = Dog("Rex", "German Shepherd")
dog2 = Dog("Bella", "Labrador")

print(dog1.name, dog1.breed)
print(dog2.name, dog2.breed)
```

**Self-check Questions:**
- What would happen if you forgot `self` in `__init__`?
- What does `dog1.name` mean — what is the `.` doing?

---

### Exercise 2 — Adding a Method with `self`

**Objective:** Practice using `self` inside a method to access properties.

**Scenario:** Extend the `Dog` class with a method that makes the dog introduce itself.

**Steps:**
1. Keep the `Dog` class from Exercise 1
2. Add a method called `introduce()` that prints: `"Woof! My name is [name] and I am a [breed]."`
3. Create two Dog objects and call `introduce()` on both

**Solution:**
```python
class Dog:
    def __init__(self, name, breed):
        self.name = name
        self.breed = breed

    def introduce(self):
        print("Woof! My name is " + self.name + " and I am a " + self.breed + ".")

dog1 = Dog("Rex", "German Shepherd")
dog2 = Dog("Bella", "Labrador")

dog1.introduce()
dog2.introduce()
```

**Expected Output:**
```
Woof! My name is Rex and I am a German Shepherd.
Woof! My name is Bella and I am a Labrador.
```

**What-if challenge:** What if you add `age` to the class and print it in the `introduce()` method too?

---

### Exercise 3 — Student Grade Tracker

**Objective:** Apply all concepts together in a realistic scenario.

**Scenario:** You are building a student result system for a school.

**Requirements:**
- A `Student` class with `name`, `subject`, and `score` properties
- A method called `result()` that prints: `"[name] scored [score] in [subject]."`
- A method called `grade()` that prints: `"Grade: A"` if score >= 70, `"Grade: B"` if score >= 50, otherwise `"Grade: F"`

**Solution:**
```python
class Student:
    def __init__(self, name, subject, score):
        self.name = name
        self.subject = subject
        self.score = score

    def result(self):
        print(self.name + " scored " + str(self.score) + " in " + self.subject + ".")

    def grade(self):
        if self.score >= 70:
            print("Grade: A")
        elif self.score >= 50:
            print("Grade: B")
        else:
            print("Grade: F")

s1 = Student("Amara", "Mathematics", 85)
s2 = Student("Emeka", "English", 55)
s3 = Student("Fatima", "Science", 42)

s1.result()
s1.grade()

s2.result()
s2.grade()

s3.result()
s3.grade()
```

**Expected Output:**
```
Amara scored 85 in Mathematics.
Grade: A
Emeka scored 55 in English.
Grade: B
Fatima scored 42 in Science.
Grade: F
```

**Self-check Questions:**
- Why do we write `str(self.score)` instead of just `self.score` in the `result()` method?
- What does `self.score >= 70` compare? Whose score is it referring to?

---

## Mini Project: Student Report Card System

Now let's combine everything into a realistic mini-project.

**Project Goal:** Build a Student Report Card System that manages multiple students, tracks multiple subjects, and generates a report.

### Stage 1 — Setup: Define the Student Class

```python
class Student:
    def __init__(self, name, student_id):
        self.name = name
        self.student_id = student_id
        self.scores = {}      # dictionary to store subject → score pairs

    def add_score(self, subject, score):
        self.scores[subject] = score

    def display_info(self):
        print("Student Name: " + self.name)
        print("Student ID: " + self.student_id)
```

**Milestone 1 Test:**
```python
s1 = Student("Amara Okafor", "STU001")
s1.display_info()
```

**Expected Output:**
```
Student Name: Amara Okafor
Student ID: STU001
```

### Stage 2 — Core Logic: Add Scores and Calculate Average

```python
class Student:
    def __init__(self, name, student_id):
        self.name = name
        self.student_id = student_id
        self.scores = {}

    def add_score(self, subject, score):
        self.scores[subject] = score

    def calculate_average(self):
        if len(self.scores) == 0:
            return 0
        total = sum(self.scores.values())
        return total / len(self.scores)

    def display_info(self):
        print("Student Name: " + self.name)
        print("Student ID: " + self.student_id)
```

**Milestone 2 Test:**
```python
s1 = Student("Amara Okafor", "STU001")
s1.add_score("Mathematics", 88)
s1.add_score("English", 74)
s1.add_score("Science", 91)

average = s1.calculate_average()
print("Average score:", average)
```

**Expected Output:**
```
Average score: 84.33333333333333
```

### Stage 3 — Enhancements: Full Report Generation

```python
class Student:
    def __init__(self, name, student_id):
        self.name = name
        self.student_id = student_id
        self.scores = {}

    def add_score(self, subject, score):
        self.scores[subject] = score

    def calculate_average(self):
        if len(self.scores) == 0:
            return 0
        total = sum(self.scores.values())
        return total / len(self.scores)

    def get_grade(self, average):
        if average >= 70:
            return "A — Excellent"
        elif average >= 50:
            return "B — Satisfactory"
        else:
            return "F — Needs Improvement"

    def print_report(self):
        print("=" * 40)
        print("STUDENT REPORT CARD")
        print("=" * 40)
        print("Name:       " + self.name)
        print("Student ID: " + self.student_id)
        print("-" * 40)
        print("Subjects and Scores:")
        for subject, score in self.scores.items():
            print("  " + subject + ": " + str(score))
        print("-" * 40)
        avg = self.calculate_average()
        print("Average Score: " + str(round(avg, 2)))
        print("Overall Grade: " + self.get_grade(avg))
        print("=" * 40)
```

### Stage 4 — Final Output

```python
# Create students
s1 = Student("Amara Okafor", "STU001")
s1.add_score("Mathematics", 88)
s1.add_score("English", 74)
s1.add_score("Science", 91)

s2 = Student("Emeka Nwosu", "STU002")
s2.add_score("Mathematics", 55)
s2.add_score("English", 63)
s2.add_score("Science", 48)

s3 = Student("Fatima Bello", "STU003")
s3.add_score("Mathematics", 35)
s3.add_score("English", 41)
s3.add_score("Science", 38)

# Print all reports
s1.print_report()
s2.print_report()
s3.print_report()
```

**Expected Output:**
```
========================================
STUDENT REPORT CARD
========================================
Name:       Amara Okafor
Student ID: STU001
----------------------------------------
Subjects and Scores:
  Mathematics: 88
  English: 74
  Science: 91
----------------------------------------
Average Score: 84.33
Overall Grade: A — Excellent
========================================
========================================
STUDENT REPORT CARD
========================================
Name:       Emeka Nwosu
Student ID: STU002
----------------------------------------
Subjects and Scores:
  Mathematics: 55
  English: 63
  Science: 48
----------------------------------------
Average Score: 55.33
Overall Grade: B — Satisfactory
========================================
========================================
STUDENT REPORT CARD
========================================
Name:       Fatima Bello
Student ID: STU003
----------------------------------------
Subjects and Scores:
  Mathematics: 35
  English: 41
  Science: 38
----------------------------------------
Average Score: 38.0
Overall Grade: F — Needs Improvement
========================================
```

**Reflection Questions:**
- How many lines would this have taken without OOP?
- What would happen if you wanted to add 50 more students?
- Can you add a method that checks if the student passed or failed?

**Optional Extension:** Add a `highest_score()` method that returns the subject where the student scored the most.

---

## Common Beginner Mistakes

### Mistake 1 — Forgetting `self` in a Method Definition

```python
# WRONG
class Dog:
    def __init__(name, breed):      # missing self!
        self.name = name

# RIGHT
class Dog:
    def __init__(self, name, breed):
        self.name = name
```

Python will raise a `TypeError` because without `self`, Python doesn't know which object to assign the name to.

---

### Mistake 2 — Passing `self` When Calling a Method

```python
class Dog:
    def __init__(self, name):
        self.name = name

    def bark(self):
        print(self.name + " says: Woof!")

dog1 = Dog("Rex")

dog1.bark(dog1)   # WRONG — passing self manually
dog1.bark()       # RIGHT — Python handles self automatically
```

Python fills in `self` automatically when you call a method on an object. Never pass it yourself.

---

### Mistake 3 — Forgetting to Use `self.` When Accessing Properties

```python
# WRONG
class Dog:
    def __init__(self, name):
        self.name = name

    def bark(self):
        print(name + " says: Woof!")   # 'name' doesn't exist here!

# RIGHT
class Dog:
    def __init__(self, name):
        self.name = name

    def bark(self):
        print(self.name + " says: Woof!")   # self.name is correct
```

Inside a method, you must use `self.name` to reach the object's property. Just `name` by itself is a completely different (non-existent) variable inside the method's local scope.

---

### Mistake 4 — Leaving a Class Body Completely Empty

```python
# WRONG
class Dog:
    # no code here — syntax error!

# RIGHT
class Dog:
    pass    # use pass as a placeholder
```

Python requires at least something in a class body. `pass` is the correct placeholder.

---

### Mistake 5 — Confusing the Class with the Object

```python
class Dog:
    def __init__(self, name):
        self.name = name

# WRONG — accessing property on the class, not an object
print(Dog.name)    # AttributeError!

# RIGHT — create an object first
dog1 = Dog("Rex")
print(dog1.name)   # Rex
```

The class (`Dog`) is the blueprint. You must create an object (`dog1`) to have actual data.

---

### Mistake 6 — Using a Different Name for `self` Without Understanding It

```python
# This works but is confusing for everyone
class Dog:
    def __init__(x, name):
        x.name = name
```

This technically runs, but it confuses other programmers and your future self. Always use `self`.

---

## Real-World Use Cases

OOP with classes is used everywhere in the real world:

**Banking systems** — Each bank account is a `BankAccount` object with properties like `account_number`, `balance`, and methods like `deposit()` and `withdraw()`.

**E-commerce** — Each product is a `Product` object. Each customer is a `Customer` object. Each order is an `Order` object.

**Games** — Each game character is a `Character` object with properties like `name`, `health`, `level`, and methods like `attack()` and `defend()`.

**School management** — Each student, teacher, and course is its own object — exactly like the project you just built.

**Data science** — Libraries like Pandas and NumPy are built entirely using classes. The `DataFrame` you create in Pandas is an object.

---

## Reflection Questions

Take a moment to think through these questions before moving on:

1. In your own words, what is the difference between a **class** and an **object**?
2. What does `__init__()` do, and when is it called?
3. Why is `self` the first parameter in every method?
4. If you have two students `s1` and `s2` created from the same class, and you call `s1.greet()`, how does Python know to print `s1`'s name and not `s2`'s?
5. Why is OOP better than creating separate variables for each piece of data?
6. What would happen to your code if you needed to add a `phone_number` field to every student? With OOP, how easy is that change?

---

## Completion Checklist

Use this to confirm you have mastered the lesson. Check off each item:

- [ ] I can explain what OOP is and why it exists
- [ ] I understand the difference between a class and an object
- [ ] I can create a class using the `class` keyword
- [ ] I can create objects from a class using `ClassName()`
- [ ] I know what `__init__()` is and when it runs automatically
- [ ] I can add properties to an object using `self.property = value` inside `__init__()`
- [ ] I understand what `self` refers to and why it is the first parameter
- [ ] I can define methods inside a class that use `self` to access properties
- [ ] I can use the dot notation (`.`) to access an object's properties and methods
- [ ] I know how to use default values in `__init__()`
- [ ] I completed all three guided exercises
- [ ] I completed the mini-project
- [ ] I understand all six common beginner mistakes
- [ ] All source tutorial content preserved

---

## Lesson Summary

In this lesson, you learned the foundations of **Object-Oriented Programming** in Python.

**OOP** is a style of programming that organises code around objects — self-contained units that bundle data (properties) and behaviour (methods) together. It makes code cleaner, easier to reuse, and mirrors how the real world works.

A **class** is a blueprint or template. An **object** is a specific instance created from that blueprint. You create a class with the `class` keyword and objects by calling the class like a function.

The **`__init__()` method** is a special method that runs automatically every time a new object is created. It is used to set up the object's initial data by assigning values to properties using `self`.

The **`self` parameter** is a reference to the current object. It is always the first parameter of any method and is how the method knows which object's data to read or modify. Python fills in `self` automatically when you call a method — you never pass it manually.

Together, classes, objects, `__init__()`, and `self` form the backbone of how professional Python code is written. In the next lessons, you will build on this foundation to learn about class properties, class methods, inheritance, and more.

---

*Sources: W3Schools Python OOP, Classes/Objects, __init__ Method, and self Parameter tutorials.*
