---
render_with_liquid: false
title: "Lesson 21: Python OOP — Class Properties, Methods, Inheritance & Polymorphism"
nav_order: 21
---

# Lesson 21: Python OOP — Class Properties, Methods, Inheritance & Polymorphism

---

## Lesson Introduction

Welcome to one of the most powerful lessons in your Python journey.

So far you have learned how to write functions, use loops, work with lists, and perhaps even create your first simple class. Now you are about to discover four core ideas that professional Python developers use every single day:

- **Class Properties** — giving every object its own personal data
- **Class Methods** — giving every object its own personal actions
- **Inheritance** — letting new classes borrow and extend the work of existing classes
- **Polymorphism** — letting different objects respond to the same instruction in their own unique ways

Together, these four ideas form the heart of **Object-Oriented Programming (OOP)** — the way most real-world Python software is designed.

By the end of this lesson, you will be able to build a small but realistic multi-class Python program from scratch, understand how professional libraries and frameworks are structured, and feel genuinely confident reading and writing OOP code.

Let's start from the very beginning.

---

## Prerequisite Concepts

Before diving in, let's make sure you have the foundations you need. If you already know these, great — skim and move on. If they are new, read carefully.

### What Is a Class?

Think of a class as a **blueprint** or a **template**.

Imagine you work in a car factory. Before building a car, engineers draw a detailed blueprint showing what every car should look like — how many wheels it has, what colour options exist, what the engine size is, what buttons are on the dashboard.

That blueprint is the **class**.

Each actual car that rolls off the production line using that blueprint is an **object** (also called an **instance**).

```python
class Car:
    pass  # An empty blueprint — we will fill it in very soon
```

### What Is an Object?

An object is a **specific thing** created from a class blueprint.

```python
my_car = Car()      # Create one Car object
your_car = Car()    # Create another Car object
```

Both `my_car` and `your_car` are **objects** of the `Car` class. They are two separate things built from the same blueprint.

### What Is `__init__`?

The `__init__` method is a special function that runs **automatically** the moment you create an object. It lets you set up the object's starting data.

```python
class Car:
    def __init__(self, brand, colour):
        self.brand = brand
        self.colour = colour

my_car = Car("Toyota", "Red")
print(my_car.brand)   # Output: Toyota
print(my_car.colour)  # Output: Red
```

Don't worry if `self` looks strange. We will explain it thoroughly very soon.

---

## Part 1: Class Properties

---

### What Are Class Properties?

A **property** (also called an **attribute**) is a piece of data that belongs to an object.

Think of it as a variable that lives *inside* an object and describes it.

Real-world analogy:

| Object | Properties |
|--------|-----------|
| A person | name, age, height, eye colour |
| A bank account | account number, balance, owner name |
| A book | title, author, number of pages |
| A dog | name, breed, age |

In Python, we store these properties on objects using the keyword `self`.

---

### What Is `self`?

This is the single biggest question beginners have about OOP. Let's answer it completely.

When Python creates an object, it needs a way for that object to refer to **itself**. That is what `self` is — it is the object's own reference to itself.

Think of it like this: if you are in a room full of people and someone says "raise your own hand," every person raises *their own* hand. `self` is how each object knows which "hand" is theirs.

```python
class Dog:
    def __init__(self, name, age):
        self.name = name   # This dog's name
        self.age = age     # This dog's age

dog1 = Dog("Rex", 3)
dog2 = Dog("Buddy", 7)

print(dog1.name)   # Output: Rex
print(dog2.name)   # Output: Buddy
```

`dog1.name` and `dog2.name` are completely separate values — each dog object has its own copy.

---

### Two Types of Properties

There are two places you can define properties on a class:

#### 1. Instance Properties (unique to each object)

These are created inside `__init__` using `self`. Every object gets its own copy.

```python
class Student:
    def __init__(self, name, grade):
        self.name = name     # Each student has their own name
        self.grade = grade   # Each student has their own grade

student1 = Student("Alice", "A")
student2 = Student("Bob", "B")

print(student1.name)   # Output: Alice
print(student2.name)   # Output: Bob
```

> **Why this matters:** `student1.name` and `student2.name` are completely independent. Changing one does not affect the other.

#### 2. Class Properties (shared by ALL objects)

These are created directly inside the class body, outside any method. Every object of that class shares the same value.

```python
class Student:
    school_name = "Sunrise Academy"   # Shared by all students

    def __init__(self, name):
        self.name = name

student1 = Student("Alice")
student2 = Student("Bob")

print(student1.school_name)   # Output: Sunrise Academy
print(student2.school_name)   # Output: Sunrise Academy
print(Student.school_name)    # Output: Sunrise Academy
```

> **Real-world analogy:** Think of instance properties as each student's own locker. Think of class properties as the school name printed on the building — it belongs to the school, not any one student.

---

### Creating, Reading, and Changing Properties

Once an object exists, you can interact with its properties at any time.

#### Reading a property:

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

p = Person("Maria", 28)
print(p.name)   # Output: Maria
print(p.age)    # Output: 28
```

#### Changing a property:

```python
p.age = 29
print(p.age)    # Output: 29
```

#### Adding a new property after creation:

```python
p.city = "London"
print(p.city)   # Output: London
```

#### Deleting a property:

```python
del p.city
# print(p.city)  # This would now cause an AttributeError
```

---

### The `__str__` Property: Making Objects Readable

By default, printing an object gives an ugly technical output like `<__main__.Dog object at 0x7f...>`. You can fix this with `__str__`.

```python
class Dog:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"{self.name} is {self.age} years old"

my_dog = Dog("Rex", 3)
print(my_dog)    # Output: Rex is 3 years old
```

> **Tip:** Always add `__str__` to your classes. It makes debugging and displaying objects much easier.

---

### Worked Example: A Bank Account Class

```python
class BankAccount:
    bank_name = "PythonBank"   # Class property — shared by all accounts

    def __init__(self, owner, balance):
        self.owner = owner        # Instance property
        self.balance = balance    # Instance property

    def __str__(self):
        return f"{self.owner}'s account at {BankAccount.bank_name} — Balance: £{self.balance}"

account1 = BankAccount("Alice", 1500)
account2 = BankAccount("Bob", 3200)

print(account1)
# Output: Alice's account at PythonBank — Balance: £1500

print(account2)
# Output: Bob's account at PythonBank — Balance: £3200

account1.balance = 1800
print(account1.balance)
# Output: 1800
```

---

### 💡 Thinking Prompt

What would happen if you changed `BankAccount.bank_name = "NewBank"` after creating the accounts? Try it — what do you observe?

---

### Common Beginner Mistake 1: Forgetting `self` when setting properties

```python
# WRONG
class Car:
    def __init__(self, brand):
        brand = brand   # This creates a local variable, NOT a property!

car = Car("Toyota")
# print(car.brand)  # AttributeError: 'Car' object has no attribute 'brand'
```

```python
# CORRECT
class Car:
    def __init__(self, brand):
        self.brand = brand   # self.brand attaches it to the object

car = Car("Toyota")
print(car.brand)   # Output: Toyota
```

---

## Part 2: Class Methods

---

### What Are Class Methods?

If properties are the *data* that describe an object, then methods are the *actions* that an object can perform.

A **method** is simply a function defined inside a class.

Real-world analogy:

| Object | Properties | Methods |
|--------|-----------|---------|
| A bank account | balance, owner | deposit, withdraw, check_balance |
| A dog | name, age | bark, sit, fetch |
| A car | brand, speed | accelerate, brake, honk |

---

### Defining and Calling a Method

```python
class Dog:
    def __init__(self, name):
        self.name = name

    def bark(self):                        # A method
        print(f"{self.name} says: Woof!")

my_dog = Dog("Rex")
my_dog.bark()    # Output: Rex says: Woof!
```

Every method receives `self` as its first parameter. This gives the method access to the object's own data.

---

### Methods That Work With Properties

Methods become powerful when they read or modify the object's properties.

```python
class BankAccount:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    def deposit(self, amount):
        self.balance += amount
        print(f"Deposited £{amount}. New balance: £{self.balance}")

    def withdraw(self, amount):
        if amount > self.balance:
            print("Insufficient funds!")
        else:
            self.balance -= amount
            print(f"Withdrew £{amount}. New balance: £{self.balance}")

    def show_balance(self):
        print(f"{self.owner}'s balance: £{self.balance}")

account = BankAccount("Alice", 1000)
account.show_balance()    # Output: Alice's balance: £1000
account.deposit(500)      # Output: Deposited £500. New balance: £1500
account.withdraw(200)     # Output: Withdrew £200. New balance: £1300
account.withdraw(2000)    # Output: Insufficient funds!
```

---

### Methods That Return Values

Methods can also calculate and return something, just like regular functions.

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

    def perimeter(self):
        return 2 * (self.width + self.height)

    def is_square(self):
        return self.width == self.height

rect = Rectangle(5, 3)
print(rect.area())         # Output: 15
print(rect.perimeter())    # Output: 16
print(rect.is_square())    # Output: False

square = Rectangle(4, 4)
print(square.is_square())  # Output: True
```

---

### The `__str__` Method (Revisited as a Method)

We introduced `__str__` earlier as a property tool, but it is actually a special method. Python calls it automatically whenever you use `print()` on an object.

```python
class Product:
    def __init__(self, name, price):
        self.name = name
        self.price = price

    def __str__(self):
        return f"Product: {self.name} | Price: £{self.price:.2f}"

p = Product("Laptop", 799.99)
print(p)    # Output: Product: Laptop | Price: £799.99
```

---

### Modifying Properties Through Methods

Using methods to change properties (rather than changing them directly from outside) is a core OOP best practice. It lets you add rules and validation.

```python
class Temperature:
    def __init__(self, celsius):
        self.celsius = celsius

    def set_temperature(self, new_temp):
        if new_temp < -273.15:
            print("Temperature below absolute zero is not possible!")
        else:
            self.celsius = new_temp
            print(f"Temperature set to {self.celsius}°C")

    def to_fahrenheit(self):
        return (self.celsius * 9/5) + 32

t = Temperature(25)
print(t.to_fahrenheit())    # Output: 77.0

t.set_temperature(-300)     # Output: Temperature below absolute zero is not possible!
t.set_temperature(100)      # Output: Temperature set to 100°C
print(t.to_fahrenheit())    # Output: 212.0
```

> **Real-world use:** Databases use this idea constantly. Instead of changing values directly, you call a method that validates the data first.

---

### Common Beginner Mistake 2: Forgetting `self` in the method signature

```python
# WRONG
class Dog:
    def __init__(self, name):
        self.name = name

    def bark():   # Missing self!
        print("Woof!")

d = Dog("Rex")
# d.bark()   # TypeError: bark() takes 0 positional arguments but 1 was given
```

```python
# CORRECT
class Dog:
    def __init__(self, name):
        self.name = name

    def bark(self):   # Always include self
        print(f"{self.name} says: Woof!")

d = Dog("Rex")
d.bark()    # Output: Rex says: Woof!
```

---

### Common Beginner Mistake 3: Calling `self.method()` without `self` inside the class

```python
# WRONG
class Circle:
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14159 * self.radius ** 2

    def describe(self):
        print(f"Area is: {area()}")   # Missing self.area()
```

```python
# CORRECT
class Circle:
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14159 * self.radius ** 2

    def describe(self):
        print(f"Area is: {self.area()}")   # self.area() is correct

c = Circle(5)
c.describe()    # Output: Area is: 78.53975
```

---

### 💡 Thinking Prompt

What would happen if `withdraw()` allowed you to make the balance go negative? Could you modify the method to prevent that? Try writing the fix.

---

## Part 3: Inheritance

---

### What Is Inheritance?

**Inheritance** is the ability of one class to **receive all the properties and methods** of another class automatically.

This is one of the most powerful ideas in all of programming.

Real-world analogy:

Think about animals. All animals share certain characteristics — they breathe, they move, they eat. But a `Dog` also barks, a `Cat` meows, and a `Bird` flies.

In OOP:
- `Animal` is the **parent class** (also called the **base class** or **superclass**)
- `Dog`, `Cat`, `Bird` are **child classes** (also called **subclasses** or **derived classes**)

The child classes **inherit** everything from the parent, and then add their own unique stuff on top.

---

### Why Does Inheritance Exist?

Without inheritance, you would have to copy-paste the same code into every class. That is messy, hard to maintain, and a source of bugs.

With inheritance, you write shared behaviour **once** in the parent, and all children get it for free.

> **Developer principle:** DRY — Don't Repeat Yourself. Inheritance is one of the main tools for following this rule.

---

### Creating a Child Class

The syntax is simple — put the parent class name inside parentheses:

```python
class Animal:
    def __init__(self, name, sound):
        self.name = name
        self.sound = sound

    def speak(self):
        print(f"{self.name} says {self.sound}")

class Dog(Animal):   # Dog inherits from Animal
    pass

class Cat(Animal):   # Cat inherits from Animal
    pass

dog = Dog("Rex", "Woof")
cat = Cat("Whiskers", "Meow")

dog.speak()    # Output: Rex says Woof
cat.speak()    # Output: Whiskers says Meow
```

Even though `Dog` and `Cat` are completely empty (`pass`), they already have the `speak()` method — because they inherited it from `Animal`.

---

### Adding New Properties and Methods to a Child Class

Child classes can add their own unique properties and methods.

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def breathe(self):
        print(f"{self.name} breathes air")

class Dog(Animal):
    def __init__(self, name, breed):
        self.name = name     # Must set name manually (we'll fix this with super() shortly)
        self.breed = breed   # New property unique to Dog

    def fetch(self):         # New method unique to Dog
        print(f"{self.name} the {self.breed} fetches the ball!")

my_dog = Dog("Rex", "Labrador")
my_dog.breathe()    # Output: Rex breathes air  (inherited from Animal)
my_dog.fetch()      # Output: Rex the Labrador fetches the ball!  (Dog's own method)
```

---

### The `super()` Function

Notice above we had to manually set `self.name = name` in the child class even though the parent already does this. That is repetitive.

`super()` solves this. It calls the **parent class's `__init__`** so you don't duplicate the setup code.

```python
class Animal:
    def __init__(self, name, age):
        self.name = name
        self.age = age
        print(f"Animal created: {self.name}")

class Dog(Animal):
    def __init__(self, name, age, breed):
        super().__init__(name, age)   # Run Animal's __init__ first
        self.breed = breed             # Then add Dog-specific property
        print(f"Dog created: {self.breed}")

my_dog = Dog("Rex", 3, "Labrador")
# Output:
# Animal created: Rex
# Dog created: Labrador

print(my_dog.name)    # Output: Rex   (set by Animal's __init__)
print(my_dog.age)     # Output: 3     (set by Animal's __init__)
print(my_dog.breed)   # Output: Labrador  (set by Dog's __init__)
```

> **Rule of thumb:** Always call `super().__init__(...)` at the start of a child's `__init__`. It keeps the parent properly set up.

---

### Method Overriding

A child class can **redefine** a method it inherited from the parent. This is called **method overriding**.

The child's version replaces the parent's version for that specific class.

```python
class Animal:
    def speak(self):
        print("Some generic animal sound")

class Dog(Animal):
    def speak(self):                      # Overrides Animal's speak
        print("Woof! Woof!")

class Cat(Animal):
    def speak(self):                      # Overrides Animal's speak
        print("Meow!")

class Fish(Animal):
    pass                                   # No override — uses Animal's speak

generic_animal = Animal()
generic_animal.speak()   # Output: Some generic animal sound

dog = Dog()
dog.speak()              # Output: Woof! Woof!

cat = Cat()
cat.speak()              # Output: Meow!

fish = Fish()
fish.speak()             # Output: Some generic animal sound  (no override)
```

---

### Calling the Parent's Method in an Override

Sometimes you want to override a method but **also** include the parent's original behaviour. Use `super()` again.

```python
class Vehicle:
    def __init__(self, brand):
        self.brand = brand

    def describe(self):
        print(f"Brand: {self.brand}")

class ElectricCar(Vehicle):
    def __init__(self, brand, battery_capacity):
        super().__init__(brand)
        self.battery_capacity = battery_capacity

    def describe(self):
        super().describe()                             # Call parent's describe first
        print(f"Battery: {self.battery_capacity} kWh") # Then add extra info

ev = ElectricCar("Tesla", 100)
ev.describe()
# Output:
# Brand: Tesla
# Battery: 100 kWh
```

---

### Checking Inheritance with `isinstance()` and `issubclass()`

Python gives you tools to check relationships between classes and objects.

```python
class Animal:
    pass

class Dog(Animal):
    pass

my_dog = Dog()

print(isinstance(my_dog, Dog))      # Output: True   (my_dog IS a Dog)
print(isinstance(my_dog, Animal))   # Output: True   (my_dog IS ALSO an Animal!)
print(issubclass(Dog, Animal))      # Output: True   (Dog IS a subclass of Animal)
print(issubclass(Animal, Dog))      # Output: False  (Animal is NOT a subclass of Dog)
```

> **Key insight:** An instance of `Dog` is *also* an instance of `Animal`. This is because `Dog` inherits from `Animal`, so every Dog is a type of Animal.

---

### Multi-Level Inheritance

Classes can inherit from classes that themselves inherit from other classes. This creates a chain.

```python
class LivingThing:
    def breathe(self):
        print("Breathing...")

class Animal(LivingThing):
    def move(self):
        print("Moving...")

class Dog(Animal):
    def bark(self):
        print("Woof!")

rex = Dog()
rex.breathe()   # Output: Breathing...  (from LivingThing)
rex.move()      # Output: Moving...     (from Animal)
rex.bark()      # Output: Woof!         (from Dog)
```

> **Analogy:** Think of a family tree. A grandchild inherits traits from both parent and grandparent.

---

### A Realistic Inheritance Example: Employees

```python
class Employee:
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    def display_info(self):
        print(f"Name: {self.name} | Salary: £{self.salary}/yr")

    def give_raise(self, amount):
        self.salary += amount
        print(f"{self.name} received a raise. New salary: £{self.salary}/yr")

class Manager(Employee):
    def __init__(self, name, salary, department):
        super().__init__(name, salary)
        self.department = department

    def display_info(self):
        super().display_info()
        print(f"Department: {self.department}")

    def hold_meeting(self):
        print(f"{self.name} is holding a meeting for the {self.department} team.")

class Developer(Employee):
    def __init__(self, name, salary, language):
        super().__init__(name, salary)
        self.language = language

    def write_code(self):
        print(f"{self.name} is writing {self.language} code.")

emp = Employee("Carol", 30000)
mgr = Manager("Dave", 60000, "Engineering")
dev = Developer("Eve", 55000, "Python")

emp.display_info()
# Output:
# Name: Carol | Salary: £30000/yr

mgr.display_info()
# Output:
# Name: Dave | Salary: £60000/yr
# Department: Engineering

dev.write_code()      # Output: Eve is writing Python code.
mgr.hold_meeting()    # Output: Dave is holding a meeting for the Engineering team.

dev.give_raise(5000)  # Output: Eve received a raise. New salary: £60000/yr
```

---

### Common Beginner Mistake 4: Forgetting `super().__init__()` in the child

```python
# WRONG
class Animal:
    def __init__(self, name):
        self.name = name

class Dog(Animal):
    def __init__(self, name, breed):
        # Forgot to call super().__init__(name)
        self.breed = breed

d = Dog("Rex", "Labrador")
# print(d.name)   # AttributeError: 'Dog' object has no attribute 'name'
```

```python
# CORRECT
class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)   # Always call super first
        self.breed = breed

d = Dog("Rex", "Labrador")
print(d.name)    # Output: Rex
print(d.breed)   # Output: Labrador
```

---

### 💡 Thinking Prompt

If `Cat` and `Dog` both inherit from `Animal`, and `Animal` has a `feed()` method, what happens when you call `my_cat.feed()`? What about if `Cat` overrides `feed()`?

---

## Part 4: Polymorphism

---

### What Is Polymorphism?

The word **polymorphism** comes from Greek and means "many forms."

In Python, polymorphism means that **different classes can respond to the same method name in their own unique ways**.

Real-world analogy:

Think about the instruction "make a sound." You could give that instruction to:
- A dog → it barks
- A cat → it meows
- A car horn → it honks
- A phone → it rings

Every one of them responds to "make a sound" differently. That is polymorphism.

In Python, you write the same method name across different classes, and when you call it, each class does its own version.

---

### Why Does Polymorphism Matter?

Without polymorphism, you would need to write separate code for every type of object:

```python
# Without polymorphism — messy and not scalable
if type(animal) == Dog:
    animal.bark()
elif type(animal) == Cat:
    animal.meow()
elif type(animal) == Bird:
    animal.chirp()
```

With polymorphism, you write it once:

```python
# With polymorphism — clean and scalable
animal.speak()   # Each animal handles it in its own way
```

---

### Polymorphism Through Method Overriding (Inherited Classes)

This is the most common form. Each child class overrides a parent method differently.

```python
class Animal:
    def speak(self):
        return "..."

class Dog(Animal):
    def speak(self):
        return "Woof!"

class Cat(Animal):
    def speak(self):
        return "Meow!"

class Duck(Animal):
    def speak(self):
        return "Quack!"

animals = [Dog(), Cat(), Duck(), Dog()]   # A list of different animals

for animal in animals:
    print(animal.speak())

# Output:
# Woof!
# Meow!
# Quack!
# Woof!
```

Notice: the `for` loop code is identical for all animals. Python automatically calls the correct `speak()` for each object. That is polymorphism in action.

---

### Polymorphism With Functions That Accept Different Objects

You can write a single function that works with many different types of objects, as long as they share a method name.

```python
class Dog:
    def speak(self):
        return "Woof!"

class Cat:
    def speak(self):
        return "Meow!"

class Person:
    def speak(self):
        return "Hello!"

def make_it_speak(thing):   # Works with ANY object that has speak()
    print(thing.speak())

make_it_speak(Dog())      # Output: Woof!
make_it_speak(Cat())      # Output: Meow!
make_it_speak(Person())   # Output: Hello!
```

Notice that `Dog`, `Cat`, and `Person` are not even related by inheritance here. They just all happen to have a method called `speak()`. Python does not care about the relationship — only that the method exists. This is called **duck typing**.

> **Duck typing principle:** "If it walks like a duck and quacks like a duck, then it must be a duck." Python simply tries to call the method — if it exists, great; if not, an error is raised.

---

### Polymorphism With a Loop — Practical Example

```python
class Shape:
    def area(self):
        return 0

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14159 * self.radius ** 2

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

class Triangle(Shape):
    def __init__(self, base, height):
        self.base = base
        self.height = height

    def area(self):
        return 0.5 * self.base * self.height

shapes = [
    Circle(5),
    Rectangle(4, 6),
    Triangle(3, 8),
    Circle(2)
]

print("Areas of all shapes:")
for shape in shapes:
    print(f"  {type(shape).__name__}: {shape.area():.2f}")

# Output:
# Areas of all shapes:
#   Circle: 78.54
#   Rectangle: 24.00
#   Triangle: 12.00
#   Circle: 12.57
```

With polymorphism, adding a new shape (e.g. `Pentagon`) requires zero changes to the loop — you just create the new class with its own `area()` method.

---

### Polymorphism With Built-In Python Features

Python's built-in functions also use polymorphism. The `len()` function works on strings, lists, and dictionaries because they all have their own internal `__len__` method.

```python
print(len("hello"))           # Output: 5     (string's __len__)
print(len([1, 2, 3, 4]))      # Output: 4     (list's __len__)
print(len({"a": 1, "b": 2})) # Output: 2     (dict's __len__)
```

You can add this to your own classes too:

```python
class Bookshelf:
    def __init__(self, books):
        self.books = books

    def __len__(self):
        return len(self.books)

shelf = Bookshelf(["Python Crash Course", "Clean Code", "The Pragmatic Programmer"])
print(len(shelf))    # Output: 3
```

---

### Polymorphism: A Realistic Payment System Example

```python
class Payment:
    def process(self, amount):
        raise NotImplementedError("Subclass must implement process()")

class CreditCard(Payment):
    def __init__(self, card_number):
        self.card_number = card_number

    def process(self, amount):
        print(f"Processing £{amount:.2f} via Credit Card ending in {self.card_number[-4:]}")

class PayPal(Payment):
    def __init__(self, email):
        self.email = email

    def process(self, amount):
        print(f"Processing £{amount:.2f} via PayPal account: {self.email}")

class BankTransfer(Payment):
    def __init__(self, account_number):
        self.account_number = account_number

    def process(self, amount):
        print(f"Processing £{amount:.2f} via Bank Transfer to account: {self.account_number}")

def checkout(payment_method, amount):
    payment_method.process(amount)   # Polymorphic call

card = CreditCard("4111111111111111")
paypal = PayPal("alice@example.com")
bank = BankTransfer("GB12BARC20201530093459")

checkout(card, 49.99)
# Output: Processing £49.99 via Credit Card ending in 1111

checkout(paypal, 129.00)
# Output: Processing £129.00 via PayPal account: alice@example.com

checkout(bank, 500.00)
# Output: Processing £500.00 via Bank Transfer to account: GB12BARC20201530093459
```

> **Professional use:** This is exactly how payment gateways work in real e-commerce systems like Django or Flask web apps. The `checkout()` function never needs to know *which* payment method is being used — it just calls `.process()`.

---

### Common Beginner Mistake 5: Thinking polymorphism requires inheritance

Polymorphism does NOT require inheritance in Python. Any two classes with the same method name work.

```python
class Printer:
    def output(self):
        print("Printing to paper...")

class Screen:
    def output(self):
        print("Displaying on screen...")

class Speaker:
    def output(self):
        print("Playing through speakers...")

devices = [Printer(), Screen(), Speaker()]
for device in devices:
    device.output()

# Output:
# Printing to paper...
# Displaying on screen...
# Playing through speakers...
```

---

### 💡 Thinking Prompt

If you add a new class `Projector` with its own `output()` method and add it to the `devices` list, what changes do you need to make to the loop? (Hint: nothing at all!)

---

## Guided Practice Exercises

---

### Exercise 1: Student Report System (Properties & Methods)

**Objective:** Build a `Student` class that stores data and provides useful behaviours.

**Scenario:** You are building a simple student management system for a school.

**Steps:**

1. Create a `Student` class with properties: `name`, `age`, `grades` (a list of numbers)
2. Add a method `add_grade(grade)` that appends a grade to the list
3. Add a method `average_grade()` that returns the average of all grades
4. Add a method `highest_grade()` that returns the highest grade
5. Add a method `report()` that prints a formatted summary
6. Add `__str__` to give a simple one-line description

**Expected Output:**

```
Student: Aisha | Age: 16
Grades: [78, 92, 85, 90, 88]
Average: 86.6
Highest: 92
```

**Starter Code:**

```python
class Student:
    school = "Riverside High"   # Class property

    def __init__(self, name, age):
        self.name = name
        self.age = age
        self.grades = []

    def add_grade(self, grade):
        self.grades.append(grade)

    def average_grade(self):
        if len(self.grades) == 0:
            return 0
        return sum(self.grades) / len(self.grades)

    def highest_grade(self):
        if len(self.grades) == 0:
            return None
        return max(self.grades)

    def report(self):
        print(f"Student: {self.name} | Age: {self.age}")
        print(f"Grades: {self.grades}")
        print(f"Average: {self.average_grade():.1f}")
        print(f"Highest: {self.highest_grade()}")

    def __str__(self):
        return f"{self.name} (Age {self.age}) at {Student.school}"


student = Student("Aisha", 16)
student.add_grade(78)
student.add_grade(92)
student.add_grade(85)
student.add_grade(90)
student.add_grade(88)
student.report()
print(student)
```

**Self-check Questions:**
- What happens if `grades` is empty and you call `average_grade()`?
- How would you add a method `pass_or_fail()` that returns `"Pass"` if the average is 50+ and `"Fail"` otherwise?

**What-if Challenge:** Add a `lowest_grade()` method and a method `grade_range()` that returns the difference between the highest and lowest grade.

---

### Exercise 2: Animal Kingdom (Inheritance)

**Objective:** Build a small class hierarchy using inheritance.

**Scenario:** A zoo management system needs to track different animals.

**Steps:**

1. Create a base class `Animal` with `name`, `age`, and `diet` properties
2. Add methods `eat()`, `sleep()`, and `describe()`
3. Create `Lion(Animal)` — add a `roar()` method and override `describe()`
4. Create `Eagle(Animal)` — add a `fly()` method and override `describe()`
5. Create `Dolphin(Animal)` — add a `swim()` method and override `describe()`

**Expected Output:**

```
Lion: Simba | Age: 4 | Diet: Carnivore | Habitat: Savanna
Simba roars: ROAAAAR!
Eagle: Sky | Age: 2 | Diet: Carnivore | Habitat: Mountains
Sky soars through the sky!
Simba is eating...
Sky is sleeping...
```

**Solution:**

```python
class Animal:
    def __init__(self, name, age, diet):
        self.name = name
        self.age = age
        self.diet = diet

    def eat(self):
        print(f"{self.name} is eating...")

    def sleep(self):
        print(f"{self.name} is sleeping...")

    def describe(self):
        print(f"Animal: {self.name} | Age: {self.age} | Diet: {self.diet}")

class Lion(Animal):
    def __init__(self, name, age):
        super().__init__(name, age, "Carnivore")
        self.habitat = "Savanna"

    def roar(self):
        print(f"{self.name} roars: ROAAAAR!")

    def describe(self):
        print(f"Lion: {self.name} | Age: {self.age} | Diet: {self.diet} | Habitat: {self.habitat}")

class Eagle(Animal):
    def __init__(self, name, age):
        super().__init__(name, age, "Carnivore")
        self.habitat = "Mountains"

    def fly(self):
        print(f"{self.name} soars through the sky!")

    def describe(self):
        print(f"Eagle: {self.name} | Age: {self.age} | Diet: {self.diet} | Habitat: {self.habitat}")

class Dolphin(Animal):
    def __init__(self, name, age):
        super().__init__(name, age, "Carnivore")
        self.habitat = "Ocean"

    def swim(self):
        print(f"{self.name} leaps through the waves!")

    def describe(self):
        print(f"Dolphin: {self.name} | Age: {self.age} | Diet: {self.diet} | Habitat: {self.habitat}")

lion = Lion("Simba", 4)
eagle = Eagle("Sky", 2)
dolphin = Dolphin("Splash", 6)

lion.describe()
lion.roar()
eagle.describe()
eagle.fly()
lion.eat()
eagle.sleep()
```

---

### Exercise 3: Shape Calculator (Polymorphism)

**Objective:** Use polymorphism to calculate areas and perimeters of different shapes through a single interface.

**Steps:**

1. Create a base `Shape` class with `area()` and `perimeter()` methods that return 0
2. Create `Circle`, `Rectangle`, `Triangle`, and `Square` classes
3. Each overrides `area()` and `perimeter()` with the correct formula
4. Write a function `print_shape_info(shape)` that prints the type, area, and perimeter
5. Test with a list of different shapes

**Expected Output:**

```
Shape: Circle
  Area: 78.54
  Perimeter: 31.42

Shape: Rectangle
  Area: 24.00
  Perimeter: 20.00

Shape: Triangle
  Area: 12.00
  Perimeter: 12.00
```

**Solution:**

```python
import math

class Shape:
    def area(self):
        return 0

    def perimeter(self):
        return 0

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return math.pi * self.radius ** 2

    def perimeter(self):
        return 2 * math.pi * self.radius

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

    def perimeter(self):
        return 2 * (self.width + self.height)

class Triangle(Shape):
    def __init__(self, a, b, c):   # Three sides
        self.a = a
        self.b = b
        self.c = c

    def area(self):
        # Heron's formula
        s = (self.a + self.b + self.c) / 2
        return math.sqrt(s * (s - self.a) * (s - self.b) * (s - self.c))

    def perimeter(self):
        return self.a + self.b + self.c

class Square(Rectangle):
    def __init__(self, side):
        super().__init__(side, side)   # A square is a rectangle where width == height

def print_shape_info(shape):
    print(f"Shape: {type(shape).__name__}")
    print(f"  Area: {shape.area():.2f}")
    print(f"  Perimeter: {shape.perimeter():.2f}")
    print()

shapes = [Circle(5), Rectangle(4, 6), Triangle(3, 4, 5), Square(7)]

for shape in shapes:
    print_shape_info(shape)
```

---

## Mini Project: Library Management System

Let's combine everything you have learned — properties, methods, inheritance, and polymorphism — into one realistic mini-project.

---

### Project Overview

You will build a simplified library system that manages different types of items: books, magazines, and DVDs. Each item type has unique properties and behaviours, but they all share a common base.

---

### Stage 1: The Base Class

```python
class LibraryItem:
    library_name = "Central City Library"

    def __init__(self, title, item_id, available=True):
        self.title = title
        self.item_id = item_id
        self.available = available

    def checkout(self):
        if self.available:
            self.available = False
            print(f'"{self.title}" has been checked out.')
        else:
            print(f'"{self.title}" is already checked out.')

    def return_item(self):
        self.available = True
        print(f'"{self.title}" has been returned.')

    def status(self):
        state = "Available" if self.available else "Checked Out"
        print(f"[{self.item_id}] {self.title} — {state}")

    def __str__(self):
        return f"{type(self).__name__}: {self.title} (ID: {self.item_id})"
```

**Milestone Output (Stage 1):**

```python
item = LibraryItem("Mystery Item", "LIB001")
item.status()       # Output: [LIB001] Mystery Item — Available
item.checkout()     # Output: "Mystery Item" has been checked out.
item.status()       # Output: [LIB001] Mystery Item — Checked Out
item.return_item()  # Output: "Mystery Item" has been returned.
```

---

### Stage 2: Child Classes

```python
class Book(LibraryItem):
    def __init__(self, title, item_id, author, pages):
        super().__init__(title, item_id)
        self.author = author
        self.pages = pages

    def status(self):
        super().status()
        print(f"    Author: {self.author} | Pages: {self.pages}")

class Magazine(LibraryItem):
    def __init__(self, title, item_id, issue_number, month):
        super().__init__(title, item_id)
        self.issue_number = issue_number
        self.month = month

    def status(self):
        super().status()
        print(f"    Issue #{self.issue_number} | {self.month}")

class DVD(LibraryItem):
    def __init__(self, title, item_id, director, duration_mins):
        super().__init__(title, item_id)
        self.director = director
        self.duration_mins = duration_mins

    def status(self):
        super().status()
        print(f"    Director: {self.director} | Duration: {self.duration_mins} mins")

    def play(self):
        if self.available:
            print(f'Now playing: "{self.title}" directed by {self.director}')
        else:
            print(f'"{self.title}" is checked out and cannot be played.')
```

**Milestone Output (Stage 2):**

```python
book = Book("The Pragmatic Programmer", "B001", "Andrew Hunt", 352)
mag  = Magazine("Tech Weekly", "M001", 47, "November 2024")
dvd  = DVD("Inception", "D001", "Christopher Nolan", 148)

book.status()
# Output:
# [B001] The Pragmatic Programmer — Available
#     Author: Andrew Hunt | Pages: 352

dvd.play()
# Output: Now playing: "Inception" directed by Christopher Nolan
```

---

### Stage 3: The Library Class (Bringing It All Together)

```python
class Library:
    def __init__(self):
        self.items = []

    def add_item(self, item):
        self.items.append(item)
        print(f'Added: {item}')

    def show_all(self):
        print(f"\n=== {LibraryItem.library_name} — Catalogue ===")
        for item in self.items:
            item.status()   # Polymorphic call — each item does its own version
            print()

    def find_by_id(self, item_id):
        for item in self.items:
            if item.item_id == item_id:
                return item
        print(f"Item ID {item_id} not found.")
        return None

    def available_items(self):
        print("\n=== Available Items ===")
        available = [item for item in self.items if item.available]
        if not available:
            print("No items currently available.")
        for item in available:
            print(f"  - {item}")
```

---

### Stage 4: Final Full Demo

```python
library = Library()

library.add_item(Book("Python Crash Course", "B001", "Eric Matthes", 544))
library.add_item(Book("Clean Code", "B002", "Robert C. Martin", 464))
library.add_item(Magazine("Nature", "M001", 612, "December 2024"))
library.add_item(DVD("Interstellar", "D001", "Christopher Nolan", 169))
library.add_item(DVD("The Martian", "D002", "Ridley Scott", 141))

library.show_all()

found = library.find_by_id("B001")
if found:
    found.checkout()

found2 = library.find_by_id("D001")
if found2:
    found2.checkout()
    found2.play()

library.available_items()
```

**Final Expected Output:**

```
Added: Book: Python Crash Course (ID: B001)
Added: Book: Clean Code (ID: B002)
Added: Magazine: Nature (ID: M001)
Added: DVD: Interstellar (ID: D001)
Added: DVD: The Martian (ID: D002)

=== Central City Library — Catalogue ===
[B001] Python Crash Course — Available
    Author: Eric Matthes | Pages: 544

[B002] Clean Code — Available
    Author: Robert C. Martin | Pages: 464

[M001] Nature — Available
    Issue #612 | December 2024

[D001] Interstellar — Available
    Director: Christopher Nolan | Duration: 169 mins

[D002] The Martian — Available
    Director: Ridley Scott | Duration: 141 mins

"Python Crash Course" has been checked out.
"Interstellar" has been checked out.
"Interstellar" is checked out and cannot be played.

=== Available Items ===
  - Book: Clean Code (ID: B002)
  - Magazine: Nature (ID: M001)
  - DVD: The Martian (ID: D002)
```

---

### Reflection Questions

1. Why does `show_all()` work correctly for Books, Magazines, and DVDs even though it only calls `item.status()`?
2. What would you need to add to support an `AudioBook` class?
3. Why is it better to have `checkout()` defined in `LibraryItem` rather than in each child class?
4. What would break if you removed the `super().__init__()` call from `Book.__init__`?
5. How does `isinstance(book, LibraryItem)` behave? Why?

**Optional Extension Challenges:**
- Add a due-date system to `checkout(days=14)` that stores when an item is due back
- Add a `late_fee(days_overdue)` method
- Add a search function that finds items by author name
- Track how many times each item has been checked out with a `checkout_count` property

---

## Common Beginner Mistakes — Complete Summary

| Mistake | Problem | Fix |
|---------|---------|-----|
| Missing `self` in `__init__` assignment | `name = name` creates a local variable, not a property | Use `self.name = name` |
| Missing `self` in method definition | `def bark():` instead of `def bark(self):` | Always include `self` as the first parameter |
| Calling internal method without `self` | `area()` instead of `self.area()` | Always use `self.method()` inside the class |
| Forgetting `super().__init__()` in child | Parent's properties never get created | Always call `super().__init__(...)` first |
| Modifying class property on an instance | `dog.species = "Cat"` creates an instance property shadow | Modify class properties via `ClassName.property = value` |
| Thinking polymorphism requires inheritance | Limiting design unnecessarily | Any two classes with the same method name work polymorphically |

---

## Reflection Questions

1. What is the difference between a **class property** and an **instance property**? Give an example of when you would use each.

2. Why does every method inside a class need `self` as its first parameter?

3. What does `super()` do, and when is it essential to use it?

4. Explain method overriding in your own words. Give a real-world scenario where it would be useful.

5. What is polymorphism? Why does it make code more flexible and easier to extend?

6. In what way does a `for` loop that calls `animal.speak()` on many different animal objects demonstrate polymorphism?

7. What is the difference between **overriding** a method and **extending** a method (calling `super()` then adding extra behaviour)?

8. Think of a real-world system (e.g. a school, hospital, restaurant, or game). Identify at least one parent class and two child classes you would create, and list what properties and methods each would have.

---

## Completion Checklist

Before moving to the next lesson, confirm you can do all of the following:

- [ ] Create a class with both instance properties and class properties
- [ ] Write methods that read and modify object properties
- [ ] Use `__str__` to make objects print nicely
- [ ] Create a child class that inherits from a parent class
- [ ] Use `super().__init__()` correctly in a child class
- [ ] Override a parent method in a child class
- [ ] Call a parent's method from inside an overridden version using `super()`
- [ ] Explain what `isinstance()` and `issubclass()` return
- [ ] Write at least two classes with the same method name and demonstrate polymorphism
- [ ] Write a loop that calls the same method on different types of objects
- [ ] Build the Library mini-project (or a similar multi-class system) from scratch
- [ ] Identify and fix all six common beginner mistakes from this lesson

---

## Lesson Summary

In this lesson you covered four of the most important pillars of Object-Oriented Programming in Python:

**Class Properties** store data inside objects. Instance properties (set with `self` in `__init__`) are unique to each object. Class properties are shared across all objects of that class.

**Class Methods** give objects behaviour. Every method takes `self` as its first parameter. Methods can read, modify, and return property values. The `__str__` method controls how an object looks when printed.

**Inheritance** allows child classes to automatically receive all the properties and methods of a parent class. `super()` lets child classes call the parent's `__init__` and other methods without duplicating code. Method overriding lets child classes replace inherited behaviour with their own version.

**Polymorphism** allows different classes to respond to the same method call in their own unique ways. This means you can write one loop or one function that works with many different types of objects — and adding new types later requires zero changes to the existing code.

These four ideas together allow you to write programs that are:
- **Organised** — related data and behaviour live together in classes
- **Reusable** — inheritance eliminates repetition
- **Extensible** — polymorphism means adding new types is safe and easy
- **Maintainable** — changing shared behaviour in one place (the parent) updates all children

You are now writing code the way professional software engineers write it every day.

---

*Next Lesson: Python Iterators and Generators — understanding how Python loops really work under the hood.*
