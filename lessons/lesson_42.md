---
render_with_liquid: false
title: "Python and MongoDB — Getting Started, Databases, Collections, Inserting, and Finding Data"
nav_order: 42
---

# Lesson 42 — Python and MongoDB: Getting Started, Databases, Collections, Inserting, and Finding Data

---

## Lesson Introduction

Welcome to Lesson 42! In this lesson you will learn how to connect Python to **MongoDB**, one of the most popular databases used in modern software development. By the end of this lesson you will be able to:

- Understand what MongoDB is and why it is useful.
- Install the PyMongo driver so Python can talk to MongoDB.
- Create and check databases and collections.
- Delete (drop) a collection you no longer need.
- Insert one or many documents into a collection.
- Retrieve (find) documents from a collection in several different ways.

You will also complete guided practice exercises, build a realistic mini-project, and understand the most common mistakes beginners make.

No database experience is required. If you have never heard the word "database" before, that is perfectly fine — we will start from scratch.

---

## Prerequisite Concepts

Before diving into the lesson, here is a quick overview of background ideas you need to understand. Do not skip this section — it will make everything else click into place.

### What is a Database?

Imagine you run a small online shop and you store every customer's name and address in a notebook. As your shop grows to 10,000 customers, a paper notebook becomes impossible to search and manage. A **database** is a software system that stores large amounts of information in an organised way so that you can quickly search, add, change, and remove records.

### What is a NoSQL Database?

Traditional databases (called **SQL** or **relational** databases) store information in rigid tables — think of a spreadsheet with fixed columns. Every row must match the same columns.

A **NoSQL** database is more flexible. Instead of fixed rows and columns, it stores data in other formats. MongoDB is a NoSQL database that stores data in a format very similar to Python dictionaries. This means each record can have different fields, making it very easy to work with changing or complex data.

### What is JSON and BSON?

**JSON** (JavaScript Object Notation) is a popular way to represent data as text. It looks like a Python dictionary:

```json
{ "name": "Alice", "age": 25, "city": "Lagos" }
```

MongoDB stores data in a format called **BSON** (Binary JSON), which is a compressed, binary version of JSON. As a Python programmer, you never need to think about BSON directly — PyMongo handles the conversion automatically.

### What is a Python Dictionary?

A Python dictionary stores key-value pairs. Example:

```python
person = {"name": "Alice", "age": 25}
print(person["name"])   # Alice
print(person["age"])    # 25
```

**Expected Output:**
```
Alice
25
```

MongoDB documents are essentially Python dictionaries stored in a database. Understanding dictionaries is essential for working with MongoDB.

### What is a Driver?

A **driver** is a piece of software that lets one program communicate with another. When you want Python to talk to a MongoDB database, you need a MongoDB driver for Python. That driver is called **PyMongo**.

---

## Section 1 — Getting Started with MongoDB and PyMongo

### What is MongoDB?

MongoDB is a free, open-source NoSQL database. Instead of storing data in tables (like Excel), it stores data in **documents** that look like JSON/Python dictionaries. These documents are grouped into **collections** (which are like tables), and collections live inside **databases**.

Think of it like this:

```
MongoDB Server
  └── Database ("mydatabase")
        └── Collection ("customers")
              ├── Document { "name": "Alice", "address": "Lagos" }
              ├── Document { "name": "Bob", "address": "Abuja" }
              └── Document { "name": "Chidi", "address": "Port Harcourt" }
```

MongoDB is used by companies like Uber, Forbes, and Bosch to store huge amounts of flexible data because:
- Documents can have different fields — no rigid schema required.
- It scales to millions of records easily.
- It maps naturally to Python dictionaries, making coding fast and intuitive.

### Installing PyMongo

Python needs the **PyMongo** library to communicate with a MongoDB database. You install it using PIP, Python's package manager.

Open your terminal (Command Prompt on Windows, Terminal on Mac/Linux) and type:

```bash
python -m pip install pymongo
```

**What this command does, line by line:**
- `python` — starts the Python interpreter
- `-m pip` — runs the PIP module (the package manager)
- `install pymongo` — downloads and installs the PyMongo library

### Testing the Installation

Once installed, verify it works by running this Python script:

```python
import pymongo
```

**Expected Output:**
```
(No output means success!)
```

If there is no error message, PyMongo is installed correctly and ready to use. If you see `ModuleNotFoundError`, it means the installation did not succeed — run the pip install command again.

> **Tip:** You can download a free local MongoDB server from [https://www.mongodb.com](https://www.mongodb.com), or use a free cloud-based MongoDB database at [https://www.mongodb.com/cloud/atlas](https://www.mongodb.com/cloud/atlas). For this lesson we assume MongoDB is running locally at the default address.

---

## Section 2 — Creating a Database

### What is a MongoDB Database?

A MongoDB **database** is a named container that holds one or more **collections**. You can have many databases on the same MongoDB server. For example, one database for your e-commerce app, another for your school management system.

### How to Create a Database

To create a database in Python, you:
1. Create a `MongoClient` object (this is your connection to the MongoDB server).
2. Access the database by name using square bracket notation.

```python
import pymongo

# Step 1: Connect to the MongoDB server
myclient = pymongo.MongoClient("mongodb://localhost:27017/")

# Step 2: Access (or create) a database called "mydatabase"
mydb = myclient["mydatabase"]
```

**Line-by-line explanation:**

- `import pymongo` — loads the PyMongo library so we can use it
- `pymongo.MongoClient("mongodb://localhost:27017/")` — connects to the MongoDB server running on the local machine (`localhost`) at port `27017` (the default MongoDB port)
- `myclient["mydatabase"]` — accesses the database named `"mydatabase"`. If it doesn't exist yet, MongoDB will create it later when you add data.

> **Very Important:** In MongoDB, a **database is NOT created until it gets content**. Just writing `myclient["mydatabase"]` only reserves the name — MongoDB waits until you actually insert a document before it creates the database on disk.

### Checking if a Database Exists

You can list all existing databases to verify yours was created:

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]

# List all databases on the server
print(myclient.list_database_names())
```

**Expected Output (after you have added data):**
```
['admin', 'config', 'local', 'mydatabase']
```

> Note: `admin`, `config`, and `local` are system databases that MongoDB creates automatically. Your `mydatabase` will only appear after you insert at least one document.

You can also check for a specific database by name:

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")

dblist = myclient.list_database_names()
if "mydatabase" in dblist:
    print("The database exists.")
else:
    print("The database does not exist yet.")
```

**Expected Output (if data has been added):**
```
The database exists.
```

**What's happening here:**
- `myclient.list_database_names()` returns a Python list of all database names
- `if "mydatabase" in dblist:` checks if the string `"mydatabase"` is inside that list
- Python's `in` keyword checks for membership inside a list

> **Thinking Prompt:** What would happen if you ran the database check BEFORE inserting any documents? Try it and see!

---

## Section 3 — Creating a Collection

### What is a Collection?

A **collection** in MongoDB is the same as a **table** in SQL databases. It is a group of related documents stored together. For example:

- A `customers` collection holds all customer records.
- A `products` collection holds all product records.
- An `orders` collection holds all order records.

Unlike SQL tables, MongoDB collections do NOT have a fixed structure (schema). This means one document in the `customers` collection could have a `phone` field and another document might not — MongoDB accepts both.

### Creating a Collection

To create a collection, access it by name through your database object:

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]

# Create (or access) a collection called "customers"
mycol = mydb["customers"]
```

**Line-by-line explanation:**

- `mydb["customers"]` — accesses the collection named `"customers"` inside `mydatabase`. If it doesn't exist yet, MongoDB will create it when you insert the first document.

> **Very Important:** Just like databases, **collections are NOT created until they receive content**. MongoDB waits until you insert a document.

### Checking if a Collection Exists

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]

# List all collections in the database
print(mydb.list_collection_names())
```

**Expected Output (after inserting data):**
```
['customers']
```

Check for a specific collection:

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]

collist = mydb.list_collection_names()
if "customers" in collist:
    print("The collection exists.")
else:
    print("The collection does not exist yet.")
```

**Expected Output:**
```
The collection exists.
```

---

## Section 4 — Dropping (Deleting) a Collection

### What Does "Drop" Mean?

In database vocabulary, **dropping** a collection means permanently deleting it — including all documents inside it. This is the equivalent of deleting an entire table in SQL.

> **Warning:** Dropping a collection is irreversible. All data in it is gone. Always double-check before dropping!

### The `drop()` Method

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

# Delete the "customers" collection permanently
mycol.drop()
```

**What each line does:**
- `mycol.drop()` — permanently removes the `customers` collection and all its documents from the database

**Return value:** `drop()` returns `True` if the collection was dropped successfully. It returns `False` if the collection did not exist (nothing to drop).

### Practical Example with Check

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

result = mycol.drop()

if result:
    print("Collection was dropped successfully.")
else:
    print("Collection did not exist, nothing was dropped.")
```

**Expected Output (if collection existed):**
```
Collection was dropped successfully.
```

> **Thinking Prompt:** Why do you think MongoDB returns `False` instead of raising an error when you try to drop a non-existent collection?

---

## Section 5 — Inserting Documents

### What is a Document?

A **document** in MongoDB is the same as a **record** in SQL databases. It is a single unit of data, stored as a dictionary-like structure with key-value pairs.

Example document:

```python
{ "name": "Alice", "address": "12 Market Street, Lagos", "age": 30 }
```

Every document automatically gets a special field called `_id`. Think of this as a unique fingerprint — no two documents in the same collection can have the same `_id`. If you don't provide one, MongoDB generates a unique one automatically.

### Inserting One Document — `insert_one()`

The `insert_one()` method inserts a single document into a collection.

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

# Create a document as a Python dictionary
mydict = { "name": "John", "address": "Highway 37" }

# Insert it into the collection
x = mycol.insert_one(mydict)

print("Insertion complete!")
```

**Expected Output:**
```
Insertion complete!
```

**Line-by-line explanation:**

- `mydict = { "name": "John", "address": "Highway 37" }` — creates a Python dictionary with two fields: `name` and `address`
- `mycol.insert_one(mydict)` — inserts that dictionary as a document into the `customers` collection
- `x =` — captures the result object returned by `insert_one()`

### Getting the Inserted Document's ID

Every document gets a unique `_id`. You can retrieve it from the result:

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

mydict = { "name": "Peter", "address": "Lowstreet 27" }
x = mycol.insert_one(mydict)

# Print the automatically assigned _id
print(x.inserted_id)
```

**Expected Output (your value will differ — it's unique):**
```
ObjectId('64a3b7f9d5e4c2a1b0f12345')
```

**What is `inserted_id`?**

`insert_one()` returns an `InsertOneResult` object. This object has a property called `inserted_id` that stores the `_id` of the document that was just inserted. The `_id` is an `ObjectId` — a 24-character hexadecimal value that MongoDB generates automatically to guarantee uniqueness.

> **Thinking Prompt:** Why does MongoDB automatically generate unique IDs? What problem would arise if two documents had the same ID?

### Inserting Multiple Documents — `insert_many()`

To insert several documents at once, use `insert_many()`. It takes a Python **list** of dictionaries.

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

mylist = [
    { "name": "Amy",     "address": "Apple st 652"   },
    { "name": "Hannah",  "address": "Mountain 21"    },
    { "name": "Michael", "address": "Valley 345"     },
    { "name": "Sandy",   "address": "Ocean blvd 2"   },
    { "name": "Betty",   "address": "Green Grass 1"  },
    { "name": "Richard", "address": "Sky st 331"     },
    { "name": "Susan",   "address": "One way 98"     },
    { "name": "Vicky",   "address": "Yellow Garden 2"},
    { "name": "Ben",     "address": "Park Lane 38"   },
    { "name": "William", "address": "Central st 954" },
    { "name": "Chuck",   "address": "Main Road 989"  },
    { "name": "Viola",   "address": "Sideway 1633"   }
]

x = mycol.insert_many(mylist)

# Print all the inserted IDs
print(x.inserted_ids)
```

**Expected Output (your IDs will differ):**
```
[ObjectId('64a3b7f9...1'), ObjectId('64a3b7f9...2'), ObjectId('64a3b7f9...3'), ...]
```

**Line-by-line explanation:**

- `mylist = [...]` — a Python list containing 12 dictionaries, each representing one customer
- `mycol.insert_many(mylist)` — inserts all 12 documents in one operation
- `x.inserted_ids` — returns a Python list of all the `_id` values that were assigned

### Inserting Multiple Documents with Custom IDs

If you want to control the `_id` yourself (instead of letting MongoDB generate one), simply include `"_id"` in each dictionary:

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

mylist = [
    { "_id": 1,  "name": "John",    "address": "Highway 37"    },
    { "_id": 2,  "name": "Peter",   "address": "Lowstreet 27"  },
    { "_id": 3,  "name": "Amy",     "address": "Apple st 652"  },
    { "_id": 4,  "name": "Hannah",  "address": "Mountain 21"   },
    { "_id": 5,  "name": "Michael", "address": "Valley 345"    },
    { "_id": 6,  "name": "Sandy",   "address": "Ocean blvd 2"  },
    { "_id": 7,  "name": "Betty",   "address": "Green Grass 1" },
    { "_id": 8,  "name": "Richard", "address": "Sky st 331"    },
    { "_id": 9,  "name": "Susan",   "address": "One way 98"    },
    { "_id": 10, "name": "Vicky",   "address": "Yellow Garden 2"},
    { "_id": 11, "name": "Ben",     "address": "Park Lane 38"  },
    { "_id": 12, "name": "William", "address": "Central st 954"},
    { "_id": 13, "name": "Chuck",   "address": "Main Road 989" },
    { "_id": 14, "name": "Viola",   "address": "Sideway 1633"  }
]

x = mycol.insert_many(mylist)
print(x.inserted_ids)
```

**Expected Output:**
```
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14]
```

> **Important:** When specifying your own `_id` values, they must be unique across all documents in the collection. Trying to insert a document with a duplicate `_id` will raise an error.

---

## Section 6 — Finding (Reading) Documents

Now that we know how to store data, let's learn how to get it back out. In MongoDB, you use the `find()` and `find_one()` methods to retrieve documents. This is equivalent to the `SELECT` statement in SQL.

### Finding One Document — `find_one()`

`find_one()` returns the **first** document it finds in the collection.

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

# Get the first document in the collection
x = mycol.find_one()
print(x)
```

**Expected Output:**
```
{'_id': 1, 'name': 'John', 'address': 'Highway 37'}
```

**What's happening:**
- `mycol.find_one()` — searches the `customers` collection and returns the very first document as a Python dictionary
- `print(x)` — prints that dictionary

This is useful when you just want a quick peek at what's in the collection, or when you know there is only one matching document.

### Finding All Documents — `find()`

`find()` returns **all** documents in the collection. It returns a special object called a **Cursor** that you can loop through with a `for` loop.

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

# Get ALL documents in the collection
for x in mycol.find():
    print(x)
```

**Expected Output:**
```
{'_id': 1, 'name': 'John', 'address': 'Highway 37'}
{'_id': 2, 'name': 'Peter', 'address': 'Lowstreet 27'}
{'_id': 3, 'name': 'Amy', 'address': 'Apple st 652'}
{'_id': 4, 'name': 'Hannah', 'address': 'Mountain 21'}
{'_id': 5, 'name': 'Michael', 'address': 'Valley 345'}
... (continues for all 14 documents)
```

**Line-by-line explanation:**

- `mycol.find()` — retrieves a cursor pointing to all documents in `customers`
- `for x in mycol.find():` — loops through every document one by one
- `print(x)` — prints each document as a Python dictionary

> **Analogy:** Think of `find()` like asking a librarian to bring you every single book in the library. The cursor is a trolley that carries all the books one by one so you can look at each.

Calling `find()` with no parameters is equivalent to `SELECT *` in SQL — it gets everything.

### Returning Only Some Fields (Projection)

Sometimes a collection has many fields, but you only care about a few of them. The second parameter of `find()` lets you specify which fields to include or exclude. This is called a **projection**.

Use `1` to include a field, `0` to exclude it.

**Example: Show only name and address (exclude `_id`)**

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

# Include only "name" and "address", exclude "_id"
for x in mycol.find({}, { "_id": 0, "name": 1, "address": 1 }):
    print(x)
```

**Expected Output:**
```
{'name': 'John', 'address': 'Highway 37'}
{'name': 'Peter', 'address': 'Lowstreet 27'}
{'name': 'Amy', 'address': 'Apple st 652'}
...
```

**What each part does:**

- `{}` — the first parameter is the filter (empty `{}` means "match all documents")
- `{ "_id": 0, "name": 1, "address": 1 }` — the second parameter is the projection:
  - `"_id": 0` — exclude the `_id` field
  - `"name": 1` — include the `name` field
  - `"address": 1` — include the `address` field

**Example: Exclude one field (show everything except address)**

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

# Show all fields EXCEPT "address"
for x in mycol.find({}, { "address": 0 }):
    print(x)
```

**Expected Output:**
```
{'_id': 1, 'name': 'John'}
{'_id': 2, 'name': 'Peter'}
{'_id': 3, 'name': 'Amy'}
...
```

> **Important Rule:** You cannot mix `0` and `1` in the same projection **except** for the `_id` field. This is because including some fields (1) automatically excludes all others, and excluding some fields (0) automatically includes all others. Mixing them creates an ambiguous instruction. The `_id` is the only exception to this rule.

**Example of what NOT to do:**

```python
# This will cause an error!
for x in mycol.find({}, { "name": 1, "address": 0 }):
    print(x)
```

**Expected Error:**
```
pymongo.errors.OperationFailure: Projection cannot have a mix of inclusion and exclusion.
```

> **Thinking Prompt:** When would you want to use a projection in a real application? Think about a situation where you have a document with 20 fields but only need 2 of them.

---

## Guided Practice Exercises

### Exercise 1 — Setting Up a Book Database

**Objective:** Create a database, collection, and insert your first document.

**Scenario:** You are building a library management system. You need to store book records in MongoDB.

**Steps:**

1. Connect to MongoDB at `localhost:27017`.
2. Create a database called `"library"`.
3. Create a collection called `"books"`.
4. Insert ONE book with these fields: `"title"`, `"author"`, `"year"`, `"genre"`.
5. Print the `inserted_id`.

**Starter code:**

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["library"]
mycol = mydb["books"]

book = {
    "title":  "Things Fall Apart",
    "author": "Chinua Achebe",
    "year":   1958,
    "genre":  "Fiction"
}

result = mycol.insert_one(book)
print("Inserted ID:", result.inserted_id)
```

**Expected Output:**
```
Inserted ID: ObjectId('64a3c...')
```

**Self-check Questions:**
- Did you see an `ObjectId` in the output?
- What would happen if you ran this code twice? (Hint: Would you get two documents or one?)

---

### Exercise 2 — Inserting a Full Library Catalogue

**Objective:** Use `insert_many()` to add multiple books at once.

**Scenario:** The library has 5 books to add to the database.

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["library"]
mycol = mydb["books"]

books = [
    { "_id": 1, "title": "Things Fall Apart",     "author": "Chinua Achebe",   "year": 1958 },
    { "_id": 2, "title": "Half of a Yellow Sun",  "author": "Chimamanda Adichie","year": 2006 },
    { "_id": 3, "title": "Purple Hibiscus",       "author": "Chimamanda Adichie","year": 2003 },
    { "_id": 4, "title": "Season of Migration",   "author": "Tayeb Salih",     "year": 1966 },
    { "_id": 5, "title": "So Long a Letter",      "author": "Mariama Bâ",      "year": 1979 }
]

result = mycol.insert_many(books)
print("Inserted IDs:", result.inserted_ids)
```

**Expected Output:**
```
Inserted IDs: [1, 2, 3, 4, 5]
```

**Self-check Questions:**
- How many documents are now in the `books` collection?
- What would happen if you tried to insert `_id: 1` again?

---

### Exercise 3 — Finding Books

**Objective:** Use `find_one()` and `find()` to retrieve books from the library.

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["library"]
mycol = mydb["books"]

# Get the first book
print("--- First Book ---")
first = mycol.find_one()
print(first)

# Get all books (title and author only, no _id)
print("\n--- All Books (Title and Author) ---")
for book in mycol.find({}, { "_id": 0, "title": 1, "author": 1 }):
    print(book)
```

**Expected Output:**
```
--- First Book ---
{'_id': 1, 'title': 'Things Fall Apart', 'author': 'Chinua Achebe', 'year': 1958}

--- All Books (Title and Author) ---
{'title': 'Things Fall Apart', 'author': 'Chinua Achebe'}
{'title': 'Half of a Yellow Sun', 'author': 'Chimamanda Adichie'}
{'title': 'Purple Hibiscus', 'author': 'Chimamanda Adichie'}
{'title': 'Season of Migration', 'author': 'Tayeb Salih'}
{'title': "So Long a Letter", 'author': 'Mariama Bâ'}
```

**What-if Challenge:** What would change in the output if you used `{ "year": 0 }` as the projection instead?

---

### Exercise 4 — Dropping a Collection

**Objective:** Practice safely checking for and dropping a collection.

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["library"]
mycol = mydb["books"]

# Check before dropping
collist = mydb.list_collection_names()
if "books" in collist:
    mycol.drop()
    print("books collection dropped.")
else:
    print("books collection did not exist.")
```

**Expected Output (if collection existed):**
```
books collection dropped.
```

---

## Mini-Project — Customer Records Manager

In this mini-project, you will build a small Python program that manages customer records in MongoDB. You will use everything learned in this lesson.

### Stage 1: Setup and Connection

```python
import pymongo

# Connect to MongoDB
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["shopdb"]
mycol = mydb["customers"]

print("Connected to MongoDB!")
print("Database: shopdb")
print("Collection: customers")
```

**Expected Output:**
```
Connected to MongoDB!
Database: shopdb
Collection: customers
```

### Stage 2: Insert Customer Records

```python
# Insert 6 customers with custom IDs
customers = [
    { "_id": 1, "name": "Amara Okafor",   "city": "Lagos",       "purchases": 5  },
    { "_id": 2, "name": "Emeka Nwosu",    "city": "Enugu",       "purchases": 12 },
    { "_id": 3, "name": "Fatima Bello",   "city": "Kano",        "purchases": 3  },
    { "_id": 4, "name": "Kwame Mensah",   "city": "Accra",       "purchases": 8  },
    { "_id": 5, "name": "Ngozi Adeyemi",  "city": "Ibadan",      "purchases": 15 },
    { "_id": 6, "name": "Seun Ogundimu",  "city": "Abeokuta",    "purchases": 2  }
]

result = mycol.insert_many(customers)
print(f"\nInserted {len(result.inserted_ids)} customer records.")
print("IDs:", result.inserted_ids)
```

**Expected Output:**
```
Inserted 6 customer records.
IDs: [1, 2, 3, 4, 5, 6]
```

### Stage 3: Display All Customer Names and Cities

```python
print("\n--- Customer Directory ---")
for customer in mycol.find({}, { "_id": 0, "name": 1, "city": 1 }):
    print(f"  {customer['name']} — {customer['city']}")
```

**Expected Output:**
```
--- Customer Directory ---
  Amara Okafor — Lagos
  Emeka Nwosu — Enugu
  Fatima Bello — Kano
  Kwame Mensah — Accra
  Ngozi Adeyemi — Ibadan
  Seun Ogundimu — Abeokuta
```

### Stage 4: Show First Customer's Full Record

```python
print("\n--- First Customer (Full Record) ---")
first = mycol.find_one()
for key, value in first.items():
    print(f"  {key}: {value}")
```

**Expected Output:**
```
--- First Customer (Full Record) ---
  _id: 1
  name: Amara Okafor
  city: Lagos
  purchases: 5
```

### Stage 5: Check Database and Collection Existence

```python
# Verify everything was created
print("\n--- System Check ---")
dbs = myclient.list_database_names()
cols = mydb.list_collection_names()

print(f"Databases available: {dbs}")
print(f"Collections in shopdb: {cols}")

if "shopdb" in dbs:
    print("shopdb database: EXISTS")
if "customers" in cols:
    print("customers collection: EXISTS")
```

**Expected Output:**
```
--- System Check ---
Databases available: ['admin', 'config', 'local', 'shopdb']
Collections in shopdb: ['customers']
shopdb database: EXISTS
customers collection: EXISTS
```

### Milestone Output — Full Combined Program

When you run all 5 stages together, the complete output looks like:

```
Connected to MongoDB!
Database: shopdb
Collection: customers

Inserted 6 customer records.
IDs: [1, 2, 3, 4, 5, 6]

--- Customer Directory ---
  Amara Okafor — Lagos
  Emeka Nwosu — Enugu
  Fatima Bello — Kano
  Kwame Mensah — Accra
  Ngozi Adeyemi — Ibadan
  Seun Ogundimu — Abeokuta

--- First Customer (Full Record) ---
  _id: 1
  name: Amara Okafor
  city: Lagos
  purchases: 5

--- System Check ---
Databases available: ['admin', 'config', 'local', 'shopdb']
Collections in shopdb: ['customers']
shopdb database: EXISTS
customers collection: EXISTS
```

### Optional Extension Challenges

- Add a `"email"` field to each customer.
- Print only customers who have more than 10 purchases (hint: you'll need a filter in `find()`).
- Drop the collection at the end and verify it no longer exists.

---

## Common Beginner Mistakes

### Mistake 1 — Forgetting That Databases and Collections Are "Lazy"

**Wrong thinking:** "I created the database, so it exists now."

**Reality:** In MongoDB, databases and collections are not created on disk until you insert at least one document. Simply writing `myclient["mydb"]` or `mydb["mycol"]` does nothing by itself.

**Fix:** Always insert at least one document before checking if a database or collection exists.

---

### Mistake 2 — Using the Wrong Case in Names

```python
# These are THREE different collections!
mydb["Customers"]   # Capital C
mydb["customers"]   # Lowercase c
mydb["CUSTOMERS"]   # All uppercase
```

MongoDB collection and database names are **case-sensitive**. Always be consistent with your naming.

---

### Mistake 3 — Mixing `0` and `1` in Projections

```python
# This WILL raise an error:
mycol.find({}, { "name": 1, "address": 0 })
```

You cannot tell MongoDB to both include some fields and exclude others in the same projection. The only exception is `_id`, which you can explicitly set to `0` even when including other fields.

**Correct:**

```python
# Include name and address, exclude _id:
mycol.find({}, { "_id": 0, "name": 1, "address": 1 })

# Exclude only address, keep everything else:
mycol.find({}, { "address": 0 })
```

---

### Mistake 4 — Inserting Duplicate Custom `_id` Values

```python
mycol.insert_one({ "_id": 1, "name": "Alice" })
mycol.insert_one({ "_id": 1, "name": "Bob" })  # ERROR! _id 1 already exists
```

**Fix:** Make sure all custom `_id` values are unique, or let MongoDB generate them automatically by omitting the `_id` field.

---

### Mistake 5 — Forgetting to Loop Through `find()` Results

```python
# WRONG — this prints the cursor object, not the documents
result = mycol.find()
print(result)  # <pymongo.cursor.Cursor object at 0x...>

# CORRECT — loop through the cursor
for doc in mycol.find():
    print(doc)
```

`find()` returns a Cursor object, not a list. You must iterate over it with a `for` loop (or convert it to a list with `list(mycol.find())`).

---

### Mistake 6 — Not Importing PyMongo

```python
# This will raise: NameError: name 'pymongo' is not defined
myclient = pymongo.MongoClient("mongodb://localhost:27017/")

# Fix — always import at the top:
import pymongo
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
```

---

### Mistake 7 — Dropping a Collection Accidentally

```python
mycol.drop()  # No warning, no confirmation — it's gone immediately!
```

Always add a safety check before dropping:

```python
collist = mydb.list_collection_names()
if "customers" in collist:
    confirm = input("Are you sure you want to drop 'customers'? (yes/no): ")
    if confirm == "yes":
        mycol.drop()
        print("Dropped.")
```

---

## Reflection Questions

Think carefully about each question before reading ahead:

1. Why does MongoDB not create a database immediately when you reference it?
2. What is the difference between `insert_one()` and `insert_many()`? When would you use each?
3. What is the difference between `find_one()` and `find()`?
4. In real life, when would you need a projection — where you only return some fields?
5. What would happen to all the data if you called `drop()` on a collection containing 10,000 documents?
6. If two documents can have different fields, how is MongoDB different from a spreadsheet?
7. Why is it important that `_id` values are always unique?
8. What does the `in` keyword do in `if "customers" in collist`?

---

## Completion Checklist

Before moving on to the next lesson, make sure you can check every item below:

- [ ] I understand what MongoDB is and why it is useful
- [ ] I can install PyMongo using PIP and verify the installation
- [ ] I understand the relationship between databases, collections, and documents
- [ ] I can create a database and check if it exists
- [ ] I can create a collection and check if it exists
- [ ] I can drop (delete) a collection using `drop()`
- [ ] I can insert a single document using `insert_one()`
- [ ] I can retrieve the `_id` of an inserted document using `inserted_id`
- [ ] I can insert multiple documents using `insert_many()`
- [ ] I can insert documents with custom `_id` values
- [ ] I can retrieve the first document using `find_one()`
- [ ] I can retrieve all documents using `find()` with a `for` loop
- [ ] I can use projections to include or exclude specific fields
- [ ] I understand why you cannot mix `1` and `0` in projections (except for `_id`)
- [ ] I completed all 4 practice exercises
- [ ] I built the mini-project Customer Records Manager

---

## Lesson Summary

In this lesson you learned the fundamentals of connecting Python to MongoDB using the PyMongo driver.

**Key Vocabulary Recap:**

| Term | Meaning |
|---|---|
| MongoDB | A NoSQL database that stores documents (JSON-like dictionaries) |
| PyMongo | The Python driver (library) that connects Python to MongoDB |
| Database | A named container for collections (like a folder) |
| Collection | A group of documents (like a table in SQL) |
| Document | A single record stored as a dictionary (like a row in SQL) |
| `_id` | A unique identifier automatically assigned to every document |
| `MongoClient` | The PyMongo object that creates a connection to the MongoDB server |
| Cursor | The object returned by `find()` — you iterate through it with a `for` loop |
| Projection | The second parameter of `find()` that controls which fields to show |
| `drop()` | Permanently deletes a collection and all its data |

**Key Methods Summary:**

| Method | Purpose |
|---|---|
| `pymongo.MongoClient(url)` | Connect to MongoDB server |
| `myclient["dbname"]` | Access/create a database |
| `mydb["colname"]` | Access/create a collection |
| `myclient.list_database_names()` | List all databases |
| `mydb.list_collection_names()` | List all collections in a database |
| `mycol.drop()` | Delete a collection permanently |
| `mycol.insert_one(dict)` | Insert one document |
| `mycol.insert_many(list)` | Insert multiple documents |
| `mycol.find_one()` | Get the first document |
| `mycol.find()` | Get all documents (returns a cursor) |
| `mycol.find({}, {field: 1})` | Get documents with specific fields only |

**Real-World Applications:**

MongoDB with Python is used in countless real-world systems, including e-commerce platforms (storing product catalogues and customer orders), social media apps (storing user profiles and posts), IoT systems (storing sensor readings with varying fields), content management systems (storing articles with different metadata), and data analytics pipelines (storing raw data with flexible structures).

You are now ready to advance to the next lesson where you will learn how to **query** MongoDB — filtering documents based on specific field values, using comparison operators, and combining conditions to find exactly the data you need.

---

*Lesson 42 — Python and MongoDB: Getting Started through Finding Data. Sources: W3Schools Python MongoDB Tutorial Series.*
