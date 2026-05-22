---
render_with_liquid: false
title: "Python and MySQL — Getting Started, Databases, Tables, Drop Table, and Inserting Data"
nav_order: 40
---

# Lesson 40: Python and MySQL — Getting Started, Creating Databases, Tables, Dropping Tables, and Inserting Data

---

## Lesson Introduction

Welcome to one of the most powerful and practical topics in all of Python programming! In this lesson, you are going to learn how to connect Python to a **real database** called **MySQL** and store, organise, and manage data inside it.

Think about every app you use daily — a student record system at school, an online shop, a hospital system, or even a bank. All of them store data in a database. After this lesson, you will understand exactly how that works and how to build it yourself using Python.

By the end of this lesson, you will be able to:

- Understand what MySQL is and why it is used
- Install the MySQL driver for Python
- Connect Python to a MySQL database server
- Create a new database
- Check if a database exists
- Create tables with columns (including Primary Keys)
- Check if a table exists
- Drop (delete) a table safely
- Insert one record into a table
- Insert many records at once
- Retrieve the ID of the last inserted record

This lesson is fully beginner-friendly. We will assume you know nothing about databases and teach everything from scratch.

---

## Prerequisite Concepts

Before diving in, let us briefly explain a few key ideas you need to understand. Don't worry — we will explain each one in simple everyday language.

### What is a Database?

A **database** is an organised collection of data stored on a computer. Think of it like a filing cabinet. Instead of paper files, a database stores information in a structured way so it can be found, updated, or deleted very quickly.

**Real-world example:** A school database stores student names, grades, subjects, and attendance. Instead of searching through hundreds of paper folders, the computer finds any student's record in a fraction of a second.

### What is MySQL?

**MySQL** is one of the most popular databases in the world. It stores data in **tables** — which look like spreadsheets with rows and columns. MySQL is free, reliable, fast, and used by companies like Facebook, YouTube, Twitter, and NASA.

**Analogy:** If your data is like a library, MySQL is the building that organises all the books (data) and gives you a way to find any book instantly.

### What is SQL?

**SQL** stands for **Structured Query Language**. It is the language you use to talk to a database. SQL commands let you create tables, add data, read data, update data, and delete data.

Some common SQL commands (we will use these in this lesson):
- `CREATE DATABASE` — make a new database
- `CREATE TABLE` — make a new table inside a database
- `INSERT INTO` — add data into a table
- `DROP TABLE` — delete a table
- `SHOW DATABASES` — list all databases
- `SHOW TABLES` — list all tables

### What is a Driver / Connector?

A **driver** (also called a connector) is a small piece of software that lets one program talk to another. To let Python talk to MySQL, we need a special driver called **mysql-connector-python**. Think of it as a translator — it translates Python instructions into something MySQL understands.

### What is a Cursor?

A **cursor** is an object in Python that lets you execute (run) SQL commands and retrieve results. Think of it like a remote control for your database — you press a button (run a command) and the database does what you asked.

### What is a Module / Import?

When you write `import mysql.connector` in Python, you are loading the MySQL driver into your program so you can use its features. This is just like picking up a tool from your toolbox before starting a job.

---

## Part 1: Getting Started with Python MySQL

### Step 1 — Install MySQL on Your Computer

Before writing any Python code, you need MySQL installed on your computer. MySQL is free to download.

**Where to download MySQL:**
Visit [https://www.mysql.com/downloads/](https://www.mysql.com/downloads/) and follow the installation instructions for your operating system (Windows, Mac, or Linux).

During installation, MySQL will ask you to set a **username** and **password**. These are important — you will use them in your Python code to connect to the database. The default username is usually `root`.

### Step 2 — Install the MySQL Connector for Python

After MySQL is installed, you need to install the Python connector (driver). This is done using **PIP**, which is Python's package manager (a tool for downloading and installing Python add-ons).

Open your **command prompt** (Windows) or **terminal** (Mac/Linux) and type this command:

```bash
python -m pip install mysql-connector-python
```

**What each part means:**
- `python` — runs Python
- `-m pip` — tells Python to use the pip tool
- `install` — the action (install something new)
- `mysql-connector-python` — the name of the package to install

After you run this, pip will download and install the connector automatically. You will see some output ending with something like `Successfully installed mysql-connector-python`.

> **Tip:** If PIP is not recognised, make sure Python is added to your system PATH. You can check by typing `python --version` in the terminal.

### Step 3 — Test if the Installation Worked

Create a new Python file (e.g., `test_mysql.py`) and write just one line inside it:

```python
import mysql.connector
```

**What this does:**
- `import` — loads the mysql.connector module into your Python program
- `mysql.connector` — the name of the installed driver package

Now run the file. If no error appears, the installation was successful!

**Expected output:** *(No output — which means success! If there was an error, the connector isn't installed correctly.)*

> **Common Beginner Mistake:** Forgetting to install the connector before trying to import it. If you see `ModuleNotFoundError: No module named 'mysql'`, it means you need to run the pip install command first.

**Corrected approach:**
```bash
# First install, then import
python -m pip install mysql-connector-python
```

### Step 4 — Create Your First Connection

Now let's actually connect Python to the MySQL database server. This is like dialling a phone number to call someone.

```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword"
)

print(mydb)
```

**Line by line explanation:**

- `import mysql.connector` — loads the MySQL driver tool
- `mydb = mysql.connector.connect(...)` — creates a connection to MySQL and stores it in the variable `mydb`
  - `host="localhost"` — where MySQL is running. `"localhost"` means it is running on your own computer (not a remote server)
  - `user="yourusername"` — the username you set during MySQL installation (often `"root"`)
  - `password="yourpassword"` — the password you set during MySQL installation
- `print(mydb)` — prints the connection object to confirm it worked

**Expected Output:**

```
<mysql.connector.connection_cext.CMySQLConnection object at 0x000001A2B3C4D5E6>
```

*(The exact numbers will differ. What matters is that it says `CMySQLConnection object` — this confirms the connection is live.)*

> **What does `host="localhost"` mean?**
> `localhost` is a special name that always refers to *your own computer*. When you install MySQL on your PC or laptop, the server runs right there on your machine. If MySQL were running on a different computer or a cloud server, you would replace `"localhost"` with that server's IP address or domain name.

> **Thinking Prompt:** What would happen if you typed the wrong password? Try it and see! You would get an error like `Access denied for user 'root'@'localhost'`.

---

## Part 2: Creating a Database

Now that Python can talk to MySQL, let's create our first database!

### What is "Creating a Database"?

Think of creating a database as building a new folder for a project. Inside that folder (database), you will later create files (tables) that hold your actual data.

### How to Create a Database

To create a database, we use the SQL command `CREATE DATABASE` followed by the name we want to give it.

**Step-by-step example:**

```python
import mysql.connector

# Step 1: Connect to MySQL (without specifying a database yet)
mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword"
)

# Step 2: Create a cursor (our "remote control" for MySQL)
mycursor = mydb.cursor()

# Step 3: Run the SQL command to create a database
mycursor.execute("CREATE DATABASE mydatabase")
```

**Line by line explanation:**

- `mydb = mysql.connector.connect(...)` — establishes the connection (same as before)
- `mycursor = mydb.cursor()` — creates a cursor object. The cursor is what you use to send SQL commands to MySQL. You MUST create a cursor before you can run any SQL.
- `mycursor.execute("CREATE DATABASE mydatabase")` — sends the SQL command to MySQL
  - `execute()` — the method that runs a SQL command
  - `"CREATE DATABASE mydatabase"` — the SQL instruction: create a new database and name it `mydatabase`

**Expected output:** *(No output means success! If the database already exists, you will get an error.)*

> **What is `mycursor.execute()`?**
> The `.execute()` method is how you send SQL commands to MySQL through Python. Whatever SQL text you put inside the brackets gets run in the MySQL database. This is the most important method you will use.

### Check if the Database Already Exists

It is good practice to check if a database exists before creating it. You can do this by listing all databases using the SQL command `SHOW DATABASES`.

**Example — List all databases:**

```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword"
)

mycursor = mydb.cursor()

# Run SHOW DATABASES to list all databases
mycursor.execute("SHOW DATABASES")

# Loop through the results and print each one
for x in mycursor:
    print(x)
```

**What the `for x in mycursor` loop does:**
After running `SHOW DATABASES`, the cursor holds a list of all database names. The `for` loop goes through each one and prints it. Each `x` is a tuple (a small group of values) containing one database name.

**Expected Output:**

```
('information_schema',)
('mydatabase',)
('mysql',)
('performance_schema',)
('sys',)
```

*(You will see `('mydatabase',)` in the list if the creation worked. The other entries are built-in MySQL system databases.)*

> **Thinking Prompt:** Why does each name appear inside parentheses and with a comma, like `('mydatabase',)`? This is because MySQL returns each row as a **tuple** in Python. A tuple with one item looks like `('item',)`.

### Alternative: Connect Directly to an Existing Database

Another way to check if a database exists is to try connecting to it directly. If it doesn't exist, MySQL will throw an error.

```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword",
    database="mydatabase"      # <-- specify which database to use
)
```

**What `database="mydatabase"` does:**
This tells Python which database inside MySQL you want to work with. From this point on, all your tables and data commands will happen inside `mydatabase`.

> **Common Beginner Mistake:** Forgetting to specify `database=` when connecting. If you run table commands without this, MySQL won't know which database to use and will give an error like `No database selected`.

---

## Part 3: Creating a Table

A **table** is where actual data lives in a database. Think of a table like a spreadsheet — it has **columns** (which define what type of data you store) and **rows** (which are the individual records or entries).

**Example of what a table looks like:**

| id | name    | address       |
|----|---------|---------------|
| 1  | John    | Highway 21    |
| 2  | Maria   | Park Lane 38  |
| 3  | Sandra  | Mountain View |

Each column has a **name** and a **data type** that defines what kind of data can go in it.

### Common MySQL Data Types (Beginner-Friendly)

| Data Type       | What it stores                        | Example               |
|-----------------|---------------------------------------|-----------------------|
| `INT`           | Whole numbers                         | 1, 42, 1000           |
| `VARCHAR(255)`  | Text up to 255 characters             | "John", "Highway 21"  |
| `TEXT`          | Long text (no character limit)        | A full article or note|
| `FLOAT`         | Decimal numbers                       | 3.14, 99.99           |
| `DATE`          | A date (year-month-day)               | 2024-01-15            |

### Step 1 — Create a Simple Table

Let's create a table called `customers` with two columns: `name` and `address`.

```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword",
    database="mydatabase"   # Important: specify the database!
)

mycursor = mydb.cursor()

# Create a table called 'customers' with 2 columns
mycursor.execute("CREATE TABLE customers (name VARCHAR(255), address VARCHAR(255))")
```

**Line by line explanation:**

- `database="mydatabase"` — we are now working inside the `mydatabase` database
- `mycursor.execute(...)` — sends the SQL command to MySQL
- `"CREATE TABLE customers (name VARCHAR(255), address VARCHAR(255))"` — the SQL command:
  - `CREATE TABLE customers` — create a new table named `customers`
  - `(name VARCHAR(255), ...)` — define the columns inside parentheses
  - `name VARCHAR(255)` — a column called `name` that holds text up to 255 characters
  - `address VARCHAR(255)` — a column called `address` that holds text up to 255 characters

**Expected output:** *(No output means success!)*

> **Why `VARCHAR(255)` and not just `TEXT`?** `VARCHAR(255)` is more efficient for shorter text. It only uses as much space as needed, while `TEXT` reserves more space. For names and addresses, `VARCHAR(255)` is perfect.

### Step 2 — Check if a Table Exists

Just like with databases, you can check which tables exist using `SHOW TABLES`.

```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword",
    database="mydatabase"
)

mycursor = mydb.cursor()

# List all tables in the current database
mycursor.execute("SHOW TABLES")

for x in mycursor:
    print(x)
```

**Expected Output:**

```
('customers',)
```

This confirms the `customers` table was created successfully.

### Step 3 — Create a Table with a Primary Key

A **Primary Key** is a special column that gives every row in a table a **unique ID number**. It is extremely important because it lets you identify and find any specific row.

**Why do we need a Primary Key?**

Imagine you have 500 customers all named "John Smith". Without a unique ID, you can't tell them apart! A primary key automatically assigns each customer their own unique number.

**Real-world analogy:** Your national ID number or passport number is your "primary key" — it is a unique number that identifies only you among millions of people.

```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword",
    database="mydatabase"
)

mycursor = mydb.cursor()

# Create a table with id, name, and address. The id is the PRIMARY KEY.
mycursor.execute(
    "CREATE TABLE customers (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(255), address VARCHAR(255))"
)
```

**Breaking down the SQL:**

- `id INT AUTO_INCREMENT PRIMARY KEY`
  - `id` — the name of the column
  - `INT` — the data type (whole number)
  - `AUTO_INCREMENT` — MySQL will automatically give this column the next available number each time you add a new row. You start at 1, then 2, 3, 4... forever.
  - `PRIMARY KEY` — tells MySQL this column is the unique identifier for each row. No two rows can have the same `id`.
- `name VARCHAR(255)` — stores the customer's name
- `address VARCHAR(255)` — stores the customer's address

**What the table looks like after adding data:**

| id | name  | address    |
|----|-------|------------|
| 1  | John  | Highway 21 |
| 2  | Maria | Park Lane  |
| 3  | Sandy | Oak Street |

The `id` column is filled automatically by MySQL — you don't have to type it yourself!

### Step 4 — Add a Primary Key to an Existing Table

What if you already created the table without a primary key and now want to add one? Use the `ALTER TABLE` command.

```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword",
    database="mydatabase"
)

mycursor = mydb.cursor()

# Add a primary key column to an existing table
mycursor.execute("ALTER TABLE customers ADD COLUMN id INT AUTO_INCREMENT PRIMARY KEY")
```

**What `ALTER TABLE` does:**
`ALTER TABLE` is used to modify an existing table's structure. In this case, we are adding a new column (`id`) to the `customers` table that already exists.

> **Common Beginner Mistake:** Trying to create a table that already exists. MySQL will give an error: `Table 'customers' already exists`. Always check first using `SHOW TABLES`, or use `DROP TABLE IF EXISTS` before recreating.

---

## Part 4: Dropping (Deleting) a Table

Sometimes you need to delete a table entirely — maybe the design was wrong, or you want to start fresh. Deleting a table in MySQL is called **dropping** it.

> **WARNING:** Dropping a table permanently deletes the table AND all the data inside it. There is no "undo" button! Always be sure before you drop a table.

### Drop a Table

```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword",
    database="mydatabase"
)

mycursor = mydb.cursor()

# Delete the table named 'customers'
sql = "DROP TABLE customers"
mycursor.execute(sql)
```

**Line by line explanation:**

- `sql = "DROP TABLE customers"` — stores the SQL command in a variable called `sql`. This is good practice for keeping long SQL commands readable.
- `mycursor.execute(sql)` — sends the DROP TABLE command to MySQL

**Expected output:** *(No output means the table was deleted successfully.)*

> **Real-world parallel:** Dropping a table is like shredding a document. Once it is gone, it is gone. In a professional environment, you would always back up (save a copy of) your data before dropping anything.

### Drop a Table Only if it Exists (Safe Method)

What if the table you are trying to drop has already been deleted? MySQL would give you an error. To avoid this, use the `IF EXISTS` keyword:

```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword",
    database="mydatabase"
)

mycursor = mydb.cursor()

# Safe drop: only delete if the table exists
sql = "DROP TABLE IF EXISTS customers"
mycursor.execute(sql)
```

**What `IF EXISTS` does:**
Before attempting to drop the table, MySQL first checks if it exists. If it does exist, it is dropped. If it does NOT exist, MySQL simply does nothing and no error is raised. This makes your code much safer and more robust.

**Analogy:** This is like saying "if there is a glass on the table, pick it up" — if there is no glass, you don't crash or panic; you just move on.

**Example comparison:**

```python
# Risky — causes an error if table doesn't exist:
mycursor.execute("DROP TABLE customers")

# Safe — silently does nothing if table doesn't exist:
mycursor.execute("DROP TABLE IF EXISTS customers")
```

> **Best Practice:** Always use `IF EXISTS` when dropping tables in production code. It prevents your program from crashing due to an error that can easily be anticipated.

> **Thinking Prompt:** Why would a table NOT exist when you try to drop it? Maybe another part of your program already dropped it, or maybe the table was never created because an earlier step failed. `IF EXISTS` guards against all these scenarios.

---

## Part 5: Inserting Data Into a Table

Now comes one of the most exciting parts — actually putting data into your table! This is called **inserting** records.

### What is "Inserting"?

Inserting means adding a new **row** (also called a **record**) into a table. Every time you add a new customer, student, product, or any piece of information, you are inserting a record.

**Real-world example:** When you register on a website, your name, email, and password are inserted as a new row in the site's users table.

### The INSERT INTO Statement

The SQL command for inserting data is `INSERT INTO`. Here is the structure:

```sql
INSERT INTO table_name (column1, column2) VALUES (value1, value2)
```

- `INSERT INTO` — tells MySQL you want to add a new row
- `table_name` — the name of the table you want to add to
- `(column1, column2)` — the columns you want to fill with data
- `VALUES (value1, value2)` — the actual data values to store

### Insert One Record

Let's insert a single customer into the `customers` table:

```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword",
    database="mydatabase"
)

mycursor = mydb.cursor()

# The SQL command with %s as placeholders
sql = "INSERT INTO customers (name, address) VALUES (%s, %s)"

# The actual values to fill in the placeholders
val = ("John", "Highway 21")

# Execute the command with the values
mycursor.execute(sql, val)

# IMPORTANT: Save the changes to the database
mydb.commit()

print(mycursor.rowcount, "record inserted.")
```

**Line by line explanation:**

- `sql = "INSERT INTO customers (name, address) VALUES (%s, %s)"` — the SQL template. The `%s` symbols are **placeholders** — they mark the spots where actual values will be put. This technique is called **parameterised queries**.
- `val = ("John", "Highway 21")` — a **tuple** holding the actual values. `"John"` goes where the first `%s` is, and `"Highway 21"` goes where the second `%s` is.
- `mycursor.execute(sql, val)` — runs the SQL command. The cursor takes the `sql` template and replaces the `%s` placeholders with the values from `val`.
- `mydb.commit()` — **THIS IS CRITICAL!** This saves the changes permanently to the database. Without `commit()`, your data is held temporarily and discarded when the program ends. Think of `commit()` as pressing the "Save" button in a word processor.
- `print(mycursor.rowcount, "record inserted.")` — prints how many rows were affected. `rowcount` is a property that tells you how many rows were changed by the last operation.

**Expected Output:**

```
1 record inserted.
```

> **Why use `%s` instead of writing the values directly?**
> You could write: `"INSERT INTO customers (name, address) VALUES ('John', 'Highway 21')"` but this is DANGEROUS. It opens your program to a security attack called **SQL injection**, where a bad actor could type specially crafted input that changes your SQL command and damages or steals your data.
>
> Using `%s` placeholders and passing values separately is the **safe and professional** way. MySQL handles the values securely.

### A Second Simple Example — Insert Another Customer

```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword",
    database="mydatabase"
)

mycursor = mydb.cursor()

sql = "INSERT INTO customers (name, address) VALUES (%s, %s)"
val = ("Sarah", "Green Street 10")
mycursor.execute(sql, val)

mydb.commit()

print(mycursor.rowcount, "record inserted.")
```

**Expected Output:**

```
1 record inserted.
```

> **Thinking Prompt:** What happens if you forget `mydb.commit()`? The record appears to be inserted (no error), but when you close the program or check the database with another tool, the data is gone. The change was never saved.

### Insert Multiple Rows at Once

What if you want to add many records at the same time — like loading 500 student records? Doing one `execute()` per record would be very slow. Instead, use `executemany()`.

```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword",
    database="mydatabase"
)

mycursor = mydb.cursor()

sql = "INSERT INTO customers (name, address) VALUES (%s, %s)"

# A list of tuples — each tuple is one customer record
val = [
    ('Peter',   'Lowstreet 4'),
    ('Amy',     'Apple st 652'),
    ('Hannah',  'Mountain 21'),
    ('Michael', 'Valley 345'),
    ('Sandy',   'Ocean blvd 2'),
    ('Betty',   'Green Grass 1'),
    ('Richard', 'Sky st 331'),
    ('Susan',   'One way 98'),
    ('Vicky',   'Yellow Garden 2'),
    ('Ben',     'Park Lane 38'),
    ('William', 'Central st 954'),
    ('Chuck',   'Main Road 989'),
    ('Viola',   'Sideway 1633')
]

# executemany() runs the INSERT once for each tuple in val
mycursor.executemany(sql, val)

mydb.commit()

print(mycursor.rowcount, "records were inserted.")
```

**What is `executemany()`?**
The `executemany()` method works exactly like `execute()`, except it takes a **list of tuples** as the second argument. It automatically loops through the list and runs the SQL insert for each tuple. This is far more efficient than calling `execute()` 13 times.

**What is a list of tuples?**
- A **tuple** is a group of values wrapped in round brackets: `('Peter', 'Lowstreet 4')`
- A **list** is a collection of items in square brackets: `[item1, item2, item3]`
- A **list of tuples** is a list where each item is itself a tuple: `[('Peter', 'Lowstreet 4'), ('Amy', 'Apple st 652'), ...]`

**Expected Output:**

```
13 records were inserted.
```

> **When would you use `executemany()` in real life?**
> - Uploading data from a spreadsheet into a database
> - Importing thousands of products into an online store
> - Adding a large batch of student enrolments at the start of a term
> - Populating a database from an API response

### Get the ID of the Last Inserted Record

After inserting a row, you can find out what ID was automatically assigned to it using `mycursor.lastrowid`.

```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword",
    database="mydatabase"
)

mycursor = mydb.cursor()

sql = "INSERT INTO customers (name, address) VALUES (%s, %s)"
val = ("Michelle", "Blue Village")

mycursor.execute(sql, val)
mydb.commit()

# Print the ID of the row we just inserted
print("1 record inserted, ID:", mycursor.lastrowid)
```

**What is `mycursor.lastrowid`?**
After any INSERT operation, `lastrowid` is a property on the cursor that holds the auto-generated `id` of the last row that was inserted. This is useful when you need to know the ID so you can use it in the next step of your program (for example, linking an order to a customer).

**Expected Output:**

```
1 record inserted, ID: 15
```

*(The actual number depends on how many records were already in the table.)*

> **Note:** If you insert multiple rows using `executemany()`, `lastrowid` gives you the ID of the **last** row inserted (not all of them).

---

## Guided Practice Exercises

### Exercise 1 — Build Your Own School Database (Beginner)

**Objective:** Practice connecting to MySQL, creating a database, creating a table, and inserting records.

**Scenario:** You are building a database for a small school called "GreenLeaf Academy" to store student information.

**Steps:**

1. Connect to MySQL (use your credentials)
2. Create a database called `greenleaf_academy`
3. Connect to that database
4. Create a table called `students` with columns:
   - `id` — INT, AUTO_INCREMENT, PRIMARY KEY
   - `name` — VARCHAR(255)
   - `grade` — INT (stores a whole number like 85 or 91)
5. Insert the following 3 students:
   - ("Alice", 88)
   - ("Bob", 72)
   - ("Chidi", 95)
6. Print how many records were inserted

**Hints:**
- After creating the connection without a database, create the database, then disconnect and reconnect with `database="greenleaf_academy"`
- Use `executemany()` to insert all 3 students at once
- Remember `mydb.commit()` after inserting!

**Expected Output:**

```
3 records were inserted.
```

**Self-check Questions:**
- Did you remember `mydb.commit()`?
- Did you include the `id` column in your table? (You should not insert values for it — MySQL fills it automatically!)
- Did you connect to the right database before creating the table?

---

### Exercise 2 — Safe Table Management (Intermediate)

**Objective:** Practice using `DROP TABLE IF EXISTS` safely before recreating a table.

**Scenario:** You made a mistake in your `students` table design — you forgot to add a `subject` column. You need to drop the table and recreate it correctly.

**Steps:**

1. Connect to `greenleaf_academy`
2. Drop the `students` table safely using `IF EXISTS`
3. Recreate the table with an extra column: `subject VARCHAR(100)`
4. Insert 2 new students:
   - ("Fatima", 91, "Mathematics")
   - ("James",  78, "English")
5. Print the number of records inserted

**Expected Output:**

```
2 records were inserted.
```

**What-if challenge:** What happens if you try to drop the table a second time without `IF EXISTS`? Try it and observe the error, then fix it.

---

### Exercise 3 — Get the Last Inserted ID (Intermediate)

**Objective:** Practice inserting a single record and retrieving its auto-generated ID.

**Scenario:** A new student joins GreenLeaf Academy. After adding them to the database, you need to display their student ID so you can print them an ID card.

**Steps:**

1. Connect to `greenleaf_academy`
2. Insert a single student: `("Ngozi", 84, "Biology")`
3. Call `mydb.commit()`
4. Print the message: `"New student added. Student ID: X"` where X is the `lastrowid`

**Expected Output:**

```
New student added. Student ID: 3
```

*(The exact number depends on your table data.)*

---

## Mini Project: Simple Customer Registry System

Now let us combine everything you have learned into one complete, realistic project. You will build a **Customer Registry System** for a small shop.

### Project Goal

Build a Python program that:
1. Creates a database called `shop_db`
2. Creates a `customers` table with id, name, address, and phone
3. Inserts a batch of 6 customers
4. Prints how many customers were added
5. Prints the ID of the last customer added

---

### Stage 1 — Setup: Connect and Create Database

```python
import mysql.connector

# Connect to MySQL server (no database yet)
mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword"
)

mycursor = mydb.cursor()

# Create the shop database
mycursor.execute("CREATE DATABASE IF NOT EXISTS shop_db")
print("Database created or already exists.")
```

**Expected Output:**

```
Database created or already exists.
```

> **Note:** `CREATE DATABASE IF NOT EXISTS` is a safer version — it creates the database only if it doesn't already exist, preventing an error if you run the script twice.

---

### Stage 2 — Core Logic: Create the Customers Table

```python
import mysql.connector

# Connect to the shop_db database
mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword",
    database="shop_db"
)

mycursor = mydb.cursor()

# Drop old table if it exists (safe reset)
mycursor.execute("DROP TABLE IF EXISTS customers")

# Create fresh customers table
mycursor.execute("""
    CREATE TABLE customers (
        id      INT AUTO_INCREMENT PRIMARY KEY,
        name    VARCHAR(255),
        address VARCHAR(255),
        phone   VARCHAR(20)
    )
""")
print("Customers table created.")
```

**Expected Output:**

```
Customers table created.
```

**What is the triple-quote `"""..."""` syntax?**
In Python, you can write a string across multiple lines using triple quotes `"""`. This is very useful for long SQL commands because it keeps them readable and organised.

---

### Stage 3 — Enhancements: Insert All Customers

```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword",
    database="shop_db"
)

mycursor = mydb.cursor()

sql = "INSERT INTO customers (name, address, phone) VALUES (%s, %s, %s)"

customers = [
    ("Amara Osei",    "12 Lagos Road",      "08012345678"),
    ("Ben Carter",    "45 Oxford Street",   "07098765432"),
    ("Chioma Eze",    "7 Freedom Avenue",   "08123456789"),
    ("David Mensah",  "3 Nkrumah Circle",   "05511223344"),
    ("Emeka Adeyemi", "22 Victoria Island", "08033445566"),
    ("Fatou Diallo",  "9 Rue de Paris",     "07711234567"),
]

mycursor.executemany(sql, customers)
mydb.commit()

print(mycursor.rowcount, "customers were added.")
print("Last customer ID:", mycursor.lastrowid)
```

**Expected Output:**

```
6 customers were added.
Last customer ID: 6
```

---

### Stage 4 — Final Output: Full Programme Together

Here is the complete programme all in one place:

```python
import mysql.connector

# ─── STEP 1: Create the database ───────────────────────────────
setup = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword"
)
cursor_setup = setup.cursor()
cursor_setup.execute("CREATE DATABASE IF NOT EXISTS shop_db")
setup.close()

# ─── STEP 2: Connect to shop_db ────────────────────────────────
mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword",
    database="shop_db"
)
mycursor = mydb.cursor()

# ─── STEP 3: Reset and create the customers table ──────────────
mycursor.execute("DROP TABLE IF EXISTS customers")
mycursor.execute("""
    CREATE TABLE customers (
        id      INT AUTO_INCREMENT PRIMARY KEY,
        name    VARCHAR(255),
        address VARCHAR(255),
        phone   VARCHAR(20)
    )
""")

# ─── STEP 4: Insert all customers ──────────────────────────────
sql = "INSERT INTO customers (name, address, phone) VALUES (%s, %s, %s)"
customers = [
    ("Amara Osei",    "12 Lagos Road",      "08012345678"),
    ("Ben Carter",    "45 Oxford Street",   "07098765432"),
    ("Chioma Eze",    "7 Freedom Avenue",   "08123456789"),
    ("David Mensah",  "3 Nkrumah Circle",   "05511223344"),
    ("Emeka Adeyemi", "22 Victoria Island", "08033445566"),
    ("Fatou Diallo",  "9 Rue de Paris",     "07711234567"),
]
mycursor.executemany(sql, customers)
mydb.commit()

# ─── STEP 5: Report results ────────────────────────────────────
print("=== Shop Customer Registry ===")
print(mycursor.rowcount, "customers successfully registered.")
print("Last customer assigned ID:", mycursor.lastrowid)
```

**Expected Final Output:**

```
=== Shop Customer Registry ===
6 customers successfully registered.
Last customer assigned ID: 6
```

**Reflection questions:**
1. Why did we need two separate connections? (Hint: the first one created the database, then we reconnected with `database="shop_db"`)
2. What would happen if we removed `mydb.commit()`?
3. What would happen if we tried to run this programme twice without the `DROP TABLE IF EXISTS` line?

**Optional extension challenges:**
- Add a `signup_date DATE` column to the customers table
- Add a `city VARCHAR(100)` column
- Try inserting 20 customers using a loop that generates fake data

---

## Common Beginner Mistakes and How to Fix Them

### Mistake 1: Forgetting `mydb.commit()`

```python
# WRONG — data is lost when programme ends
mycursor.execute(sql, val)
print("Done")   # appears to work but data is NOT saved!

# CORRECT — always commit after INSERT, UPDATE, or DELETE
mycursor.execute(sql, val)
mydb.commit()
print("Done")   # data is now permanently saved
```

### Mistake 2: Not Specifying the Database in the Connection

```python
# WRONG — MySQL doesn't know which database you mean
mydb = mysql.connector.connect(
    host="localhost",
    user="root",
    password="pass"
)
mycursor.execute("CREATE TABLE students ...")  # ERROR: No database selected

# CORRECT — always specify the database
mydb = mysql.connector.connect(
    host="localhost",
    user="root",
    password="pass",
    database="mydatabase"   # ← add this
)
```

### Mistake 3: Dropping a Non-Existent Table Without IF EXISTS

```python
# WRONG — crashes if table doesn't exist
mycursor.execute("DROP TABLE customers")    # ERROR if table is already gone

# CORRECT — safe to run even if table doesn't exist
mycursor.execute("DROP TABLE IF EXISTS customers")
```

### Mistake 4: Putting Values Directly in the SQL String (SQL Injection Risk)

```python
name = "O'Brien"   # Note the apostrophe — this would break unparameterised SQL

# WRONG — dangerous and breaks with special characters
sql = "INSERT INTO customers (name) VALUES ('" + name + "')"
# This becomes: INSERT INTO customers (name) VALUES ('O'Brien')  ← SYNTAX ERROR

# CORRECT — use %s placeholders and pass values separately
sql = "INSERT INTO customers (name) VALUES (%s)"
val = (name,)
mycursor.execute(sql, val)   # MySQL handles the apostrophe safely
```

### Mistake 5: Trying to Insert into the `id` Column

```python
# WRONG — MySQL manages id automatically, don't insert it yourself
sql = "INSERT INTO customers (id, name, address) VALUES (%s, %s, %s)"
val = (1, "John", "Main St")   # Will ERROR if id already exists!

# CORRECT — skip the id column entirely
sql = "INSERT INTO customers (name, address) VALUES (%s, %s)"
val = ("John", "Main St")   # MySQL sets id automatically
```

### Mistake 6: Forgetting to Create the Cursor

```python
# WRONG — you can't execute SQL without a cursor
mydb = mysql.connector.connect(...)
mydb.execute("CREATE TABLE ...")   # ERROR: connection object has no .execute()

# CORRECT — always create a cursor first
mydb = mysql.connector.connect(...)
mycursor = mydb.cursor()           # ← create cursor
mycursor.execute("CREATE TABLE ...")   # now this works
```

---

## Reflection Questions

Think through these questions after completing the lesson. They will deepen your understanding significantly.

1. What is the difference between `execute()` and `executemany()`? When would you use each one?

2. Why is `mydb.commit()` required after an INSERT operation but NOT after a SELECT (read) operation?

3. What would happen to your data if the Python programme crashed right after `execute()` but before `commit()`? Would the data be in the database?

4. If `AUTO_INCREMENT` starts at 1 and you insert 5 records, then delete records 3 and 4, what will the next `id` be when you insert a new record? (Answer: 6 — MySQL does not reuse deleted IDs!)

5. Why is using `%s` placeholders safer than string concatenation when building SQL commands?

6. What is the purpose of a `cursor` in MySQL Python programming?

7. If you drop a table that has 10,000 rows of customer data, can you get that data back? What does this tell you about being careful with `DROP TABLE`?

8. What is the difference between `CREATE DATABASE` and `CREATE DATABASE IF NOT EXISTS`? Which one is safer to use in code that might run multiple times?

---

## Completion Checklist

Before you move on to the next lesson, make sure you can do all of the following:

- [ ] I can install the `mysql-connector-python` driver using pip
- [ ] I can import `mysql.connector` in Python
- [ ] I can create a connection to a MySQL server
- [ ] I understand what `host`, `user`, `password`, and `database` mean in the connection
- [ ] I can create a cursor using `mydb.cursor()`
- [ ] I can create a new database using `CREATE DATABASE`
- [ ] I can list all databases using `SHOW DATABASES` and loop through results
- [ ] I can connect directly to a specific database
- [ ] I can create a table using `CREATE TABLE`
- [ ] I understand what `VARCHAR(255)` and `INT` data types mean
- [ ] I can add a `PRIMARY KEY` with `AUTO_INCREMENT` to a table
- [ ] I can add a primary key to an existing table using `ALTER TABLE`
- [ ] I can list all tables using `SHOW TABLES`
- [ ] I can drop a table using `DROP TABLE`
- [ ] I can safely drop a table using `DROP TABLE IF EXISTS`
- [ ] I can insert a single record using `execute()` and `%s` placeholders
- [ ] I know why `mydb.commit()` is essential after data changes
- [ ] I can insert multiple records at once using `executemany()`
- [ ] I can retrieve the last inserted row's ID using `mycursor.lastrowid`
- [ ] I understand the danger of SQL injection and how `%s` prevents it

---

## Lesson Summary

In this lesson, you went from zero knowledge about databases to being able to build a complete database system using Python and MySQL. Here is a quick recap of everything you covered:

**Setting Up:** You installed MySQL on your computer and installed the `mysql-connector-python` driver using pip. You learned that `import mysql.connector` loads the database tool into Python.

**Connecting:** You used `mysql.connector.connect()` with `host`, `user`, `password`, and optionally `database` to establish a connection to the MySQL server. You always need a `cursor` — created by `mydb.cursor()` — to send SQL commands.

**Databases:** You created databases with `CREATE DATABASE`, listed them with `SHOW DATABASES`, and connected to a specific one by adding `database="name"` to your connection.

**Tables:** You created tables with `CREATE TABLE`, defining columns with data types like `VARCHAR(255)` and `INT`. You added a `PRIMARY KEY` with `AUTO_INCREMENT` to give each row a unique ID. You listed tables with `SHOW TABLES` and modified existing ones with `ALTER TABLE`.

**Dropping Tables:** You deleted tables with `DROP TABLE` and used the safer `DROP TABLE IF EXISTS` to avoid errors when a table might not exist.

**Inserting Data:** You used `INSERT INTO` with `%s` placeholders to safely insert data. You always called `mydb.commit()` to permanently save changes. You inserted multiple rows efficiently using `executemany()` with a list of tuples. You retrieved the auto-generated ID of the last inserted row using `mycursor.lastrowid`.

**Real-world connection:** Every website, app, and system that stores user data, orders, records, or any persistent information uses database operations exactly like the ones you practised in this lesson. You now have the foundation to build real, data-driven applications.
