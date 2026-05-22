---
render_with_liquid: false
title: "Python MySQL — Querying, Filtering, Sorting, Modifying, and Joining Data"
nav_order: 41
---

# Lesson 41 — Python MySQL: Querying, Filtering, Sorting, Modifying, and Joining Data

---

## Lesson Introduction

Welcome! In this lesson you will learn how to **talk to a MySQL database using Python**. By the end of this lesson you will know how to:

- **Read** data from a table (SELECT)
- **Filter** results with conditions (WHERE)
- **Sort** results (ORDER BY)
- **Limit** the number of results (LIMIT / OFFSET)
- **Update** existing rows (UPDATE)
- **Delete** rows (DELETE)
- **Combine two tables** into one result (JOIN)

Think of a database like a giant, organised filing cabinet. Each drawer is a **table**. Inside each drawer are many **rows** (records). This lesson teaches you how to open that cabinet, find exactly the papers you need, change them, throw some away, and even merge two drawers together.

> **Real-world relevance:** Every app you use daily — banking, e-commerce, social media — stores its data in a database and uses exactly these operations to show you information, update your profile, delete old orders, or link your account to your purchases.

---

## Prerequisite Concepts

Before we dive in, let us make sure you understand the building blocks. If any of these words are unfamiliar, read this section carefully.

### What is MySQL?

**MySQL** is a **database management system (DBMS)**. It stores data in organised tables, just like Excel spreadsheets but far more powerful. You can store millions of rows and retrieve exactly the ones you need in milliseconds.

### What is mysql-connector-python?

This is a **Python library** (a pre-built toolbox) that lets your Python code speak to a MySQL server. You install it once with:

```bash
pip install mysql-connector-python
```

### The standard connection block

Every example in this lesson starts with the same connection code. Here is what each line does:

```python
import mysql.connector    # Load the MySQL toolbox

mydb = mysql.connector.connect(   # Open a connection to the MySQL server
    host="localhost",             # Where the server lives (your own machine)
    user="yourusername",          # Your MySQL login name
    password="yourpassword",      # Your MySQL password
    database="mydatabase"         # Which database to use
)

mycursor = mydb.cursor()          # Create a cursor — your "pen" to write queries
```

**Analogy:** Think of `mydb` as opening a phone call to the database. Think of `mycursor` as picking up a pen so you can write your question on paper and send it.

### What is a cursor?

A **cursor** is a special object that:
1. Sends your SQL query to the database
2. Holds the results that come back
3. Lets you loop through those results

### What is SQL?

**SQL** (Structured Query Language) is the language you use to talk to a database. You write SQL commands inside Python strings and send them through the cursor. SQL is not Python — it is its own simple language.

---

## Part 1 — SELECT: Reading Data from a Table

### What is SELECT and why does it exist?

`SELECT` is the SQL command for **reading data**. Without it, you cannot see anything in a database. It is the most-used SQL command in the world.

**Why do we need it?** A table might have thousands of rows. SELECT lets you say: "Give me all rows," or "Give me just the name and address columns," or "Give me just the first row."

### 1.1 — Selecting ALL rows and columns

The `*` symbol means "everything." `SELECT *` means "give me every column."

```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword",
    database="mydatabase"
)

mycursor = mydb.cursor()

mycursor.execute("SELECT * FROM customers")   # Send the SQL query

myresult = mycursor.fetchall()   # fetchall() grabs every single row returned

for x in myresult:       # Loop through each row
    print(x)             # Print the row (it is a tuple)
```

**Line-by-line breakdown:**

| Line | What it does |
|---|---|
| `mycursor.execute(...)` | Sends the SQL query to the database |
| `"SELECT * FROM customers"` | SQL: "Give me every column from the customers table" |
| `mycursor.fetchall()` | Collects ALL the results into a Python list |
| `for x in myresult` | Loops through each row one at a time |
| `print(x)` | Prints one row (shown as a tuple like `(1, 'John', 'Oslo St')`) |

**Expected output** (example with 3 rows):
```
(1, 'John', 'Highway 21')
(2, 'Peter', 'Lowstreet 4')
(3, 'Amy', 'Apple st 652')
```

> **What is a tuple?** A tuple is a group of values in brackets. Each row from the database comes back as a tuple. Position 0 is the first column, position 1 is the second column, and so on.

> **Thinking prompt:** What happens if your `customers` table is empty? What would `myresult` contain?
> Answer: It would be an empty list `[]`, and the `for` loop would simply not print anything.

---

### 1.2 — Selecting SPECIFIC columns

Sometimes you do not want all columns — only certain ones. Instead of `*`, you list the column names separated by commas.

```python
mycursor.execute("SELECT name, address FROM customers")

myresult = mycursor.fetchall()

for x in myresult:
    print(x)
```

**SQL breakdown:**
- `SELECT name, address` — "I only want the name and address columns"
- `FROM customers` — "from the customers table"

**Expected output:**
```
('John', 'Highway 21')
('Peter', 'Lowstreet 4')
('Amy', 'Apple st 652')
```

Notice each tuple now only has 2 values instead of the full row.

> **Thinking prompt:** Why would you want to select only specific columns instead of `*`? Imagine a table with 50 columns — fetching all 50 when you only need 2 wastes memory and makes your program slower.

---

### 1.3 — Using fetchone() to get a single row

`fetchall()` gets every row. `fetchone()` gets just the **first row**. This is useful when you know there is only one result, or you only need to check one record.

```python
mycursor.execute("SELECT * FROM customers")

myresult = mycursor.fetchone()   # Only grab the first row

print(myresult)
```

**Expected output:**
```
(1, 'John', 'Highway 21')
```

**Analogy:** `fetchall()` is like grabbing the entire stack of papers. `fetchone()` is like picking only the top sheet.

> **Common mistake:** Calling `fetchone()` multiple times on the same executed query returns the next row each time. The cursor "moves forward" like a reading finger.

---

## Part 2 — WHERE: Filtering Your Results

### What is WHERE and why does it exist?

Without filtering, you get **every row**. But in real life you almost always want specific rows — "show me the customer named John," or "show me all orders above $100."

`WHERE` is the SQL filter. It says: "Only give me rows that match this condition."

**Analogy:** Imagine searching your email inbox. You don't read all 10,000 emails — you type a name in the search box. `WHERE` is that search box.

---

### 2.1 — Simple WHERE filter

```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword",
    database="mydatabase"
)

mycursor = mydb.cursor()

sql = "SELECT * FROM customers WHERE address = 'Park Lane 38'"

mycursor.execute(sql)

myresult = mycursor.fetchall()

for x in myresult:
    print(x)
```

**SQL breakdown:**
- `SELECT *` — give me all columns
- `FROM customers` — from the customers table
- `WHERE address = 'Park Lane 38'` — BUT only rows where the address is exactly 'Park Lane 38'

**Expected output** (assuming one match):
```
(7, 'Ben', 'Park Lane 38')
```

> **Important:** String values in SQL must be wrapped in **single quotes** `'like this'`. Numbers do not need quotes.

---

### 2.2 — Wildcard search with LIKE and %

Sometimes you want rows that **contain** a word or letter pattern, not an exact match. Use `LIKE` with the `%` symbol.

`%` means "any number of any characters" — like a wildcard in a card game.

```python
sql = "SELECT * FROM customers WHERE address LIKE '%way%'"

mycursor.execute(sql)

myresult = mycursor.fetchall()

for x in myresult:
    print(x)
```

**Breaking down `'%way%'`:**
- First `%` — any characters can come before "way"
- `way` — this exact text must appear somewhere
- Last `%` — any characters can come after "way"

This matches "Highway 21", "Broadway 5", "My way 3", etc.

**Expected output:**
```
(1, 'John', 'Highway 21')
```

**More wildcard examples:**
- `'J%'` — starts with J
- `'%n'` — ends with n
- `'%ohn%'` — contains "ohn" anywhere

---

### 2.3 — Preventing SQL Injection with %s placeholder

**What is SQL Injection?** This is a famous hacking technique. If you build SQL queries by gluing user input directly into a string, a hacker could type something like `'; DROP TABLE customers; --` as their address. This would destroy your table!

**The safe solution:** Use `%s` as a placeholder and pass the actual value separately. The connector will safely handle the escaping for you.

```python
sql = "SELECT * FROM customers WHERE address = %s"
adr = ("Yellow Garden 2", )    # Note the comma — this makes it a tuple

mycursor.execute(sql, adr)     # Pass the query AND the values separately

myresult = mycursor.fetchall()

for x in myresult:
    print(x)
```

**Why `("Yellow Garden 2", )` with a comma?** The `execute()` method expects a **tuple** as the second argument. A single-item tuple in Python requires a trailing comma.

**Expected output:**
```
(8, 'Vicky', 'Yellow Garden 2')
```

> **Rule of thumb:** Whenever the WHERE value comes from user input (a form, an API, user typing), ALWAYS use `%s`. Never build SQL by string concatenation.

**Wrong (dangerous):**
```python
# NEVER DO THIS if address comes from user input
sql = "SELECT * FROM customers WHERE address = '" + user_input + "'"
```

**Right (safe):**
```python
sql = "SELECT * FROM customers WHERE address = %s"
mycursor.execute(sql, (user_input,))
```

---

## Part 3 — ORDER BY: Sorting Your Results

### What is ORDER BY and why does it exist?

When MySQL returns rows, the order is not guaranteed. `ORDER BY` sorts the results — alphabetically, numerically, by date, etc.

**Real-world example:** An online shop shows products sorted by price (cheapest first). A leaderboard shows scores sorted highest first.

---

### 3.1 — ORDER BY ascending (default)

`ORDER BY` without anything extra sorts from **smallest to largest** (A to Z for text, 1 to 100 for numbers). This is called **ascending** order.

```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword",
    database="mydatabase"
)

mycursor = mydb.cursor()

sql = "SELECT * FROM customers ORDER BY name"

mycursor.execute(sql)

myresult = mycursor.fetchall()

for x in myresult:
    print(x)
```

**SQL breakdown:**
- `SELECT *` — all columns
- `FROM customers` — from customers table
- `ORDER BY name` — sort the results by the name column, A to Z

**Expected output** (alphabetically sorted by name):
```
(3, 'Amy', 'Apple st 652')
(1, 'John', 'Highway 21')
(2, 'Peter', 'Lowstreet 4')
```

---

### 3.2 — ORDER BY DESC (descending)

Add `DESC` after the column name to sort in **reverse order** — Z to A for text, or largest to smallest for numbers.

```python
sql = "SELECT * FROM customers ORDER BY name DESC"

mycursor.execute(sql)

myresult = mycursor.fetchall()

for x in myresult:
    print(x)
```

**Expected output** (reverse alphabetically):
```
(2, 'Peter', 'Lowstreet 4')
(1, 'John', 'Highway 21')
(3, 'Amy', 'Apple st 652')
```

> **ASC vs DESC summary:**
> - `ASC` (Ascending) — A → Z, 1 → 100 (this is the default)
> - `DESC` (Descending) — Z → A, 100 → 1

---

## Part 4 — LIMIT: Controlling How Many Rows You Get Back

### What is LIMIT and why does it exist?

Imagine a table with 1,000,000 customer rows. If you do `SELECT *`, Python tries to load all one million rows into memory — your program would slow down or crash!

`LIMIT` says: "Only give me the first N rows." This is essential for performance and for building features like **pagination** (showing page 1, page 2, page 3 of results).

---

### 4.1 — Basic LIMIT

```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword",
    database="mydatabase"
)

mycursor = mydb.cursor()

mycursor.execute("SELECT * FROM customers LIMIT 5")

myresult = mycursor.fetchall()

for x in myresult:
    print(x)
```

**SQL breakdown:**
- `SELECT * FROM customers` — all columns from customers
- `LIMIT 5` — but only return the first 5 rows

**Expected output:** The first 5 rows of the table (whatever they are).

---

### 4.2 — LIMIT with OFFSET (pagination)

`OFFSET` tells MySQL **where to start counting from**. Think of it like "skip the first N rows, then give me the next batch."

```python
mycursor.execute("SELECT * FROM customers LIMIT 5 OFFSET 2")

myresult = mycursor.fetchall()

for x in myresult:
    print(x)
```

**SQL breakdown:**
- `LIMIT 5` — give me 5 rows
- `OFFSET 2` — but skip the first 2 rows before starting to count

So if your table has rows 1 through 10, `LIMIT 5 OFFSET 2` returns rows 3, 4, 5, 6, 7.

**Visual illustration:**

```
Row 1  ← skipped (OFFSET 2)
Row 2  ← skipped
Row 3  ← returned ✓
Row 4  ← returned ✓
Row 5  ← returned ✓
Row 6  ← returned ✓
Row 7  ← returned ✓
Row 8  ← not included (past LIMIT 5)
...
```

**Real-world use:** A website showing 10 products per page:
- Page 1: `LIMIT 10 OFFSET 0`
- Page 2: `LIMIT 10 OFFSET 10`
- Page 3: `LIMIT 10 OFFSET 20`

---

## Part 5 — UPDATE: Changing Existing Data

### What is UPDATE and why does it exist?

`UPDATE` modifies the value of one or more columns in existing rows. You use it when information changes — a customer moves to a new address, a price changes, a user updates their profile.

> ⚠️ **Critical warning:** Always use a `WHERE` clause with `UPDATE`. Without it, **every single row** in the table gets changed!

---

### 5.1 — Basic UPDATE

```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword",
    database="mydatabase"
)

mycursor = mydb.cursor()

sql = "UPDATE customers SET address = 'Canyon 123' WHERE address = 'Valley 345'"

mycursor.execute(sql)

mydb.commit()   # IMPORTANT: saves the changes permanently

print(mycursor.rowcount, "record(s) affected")
```

**SQL breakdown:**
- `UPDATE customers` — I want to update the customers table
- `SET address = 'Canyon 123'` — change the address column to this new value
- `WHERE address = 'Valley 345'` — but ONLY for rows where address is currently 'Valley 345'

**Expected output:**
```
1 record(s) affected
```

**What is `mydb.commit()`?**
`commit()` is like pressing **Save** on a document. Without it, your changes exist temporarily but are NOT written to the database permanently. This is a very common beginner mistake — forgetting `commit()` and wondering why nothing changed!

> **Analogy:** Imagine you're editing a Word document. `execute()` makes your edits on screen. `commit()` is pressing Ctrl+S to actually save to disk.

**What is `mycursor.rowcount`?**
This tells you how many rows were actually changed. It is very useful to confirm your update worked.

---

### 5.2 — UPDATE with SQL Injection protection

```python
sql = "UPDATE customers SET address = %s WHERE address = %s"
val = ("Valley 345", "Canyon 123")    # (new value, condition to match)

mycursor.execute(sql, val)

mydb.commit()

print(mycursor.rowcount, "record(s) affected")
```

Here two `%s` placeholders are used. The first is for the new address (`SET address = %s`), and the second is for the WHERE condition. They are filled in order from the tuple `val`.

---

## Part 6 — DELETE: Removing Rows

### What is DELETE and why does it exist?

`DELETE FROM` permanently removes rows from a table. You use it to clean up old data — expired sessions, cancelled orders, deleted accounts.

> ⚠️ **Critical warning:** Always use a `WHERE` clause with `DELETE`. Without it, **every row in the entire table is deleted** — and this action cannot be undone (unless you have a backup)!

---

### 6.1 — Basic DELETE

```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword",
    database="mydatabase"
)

mycursor = mydb.cursor()

sql = "DELETE FROM customers WHERE address = 'Mountain 21'"

mycursor.execute(sql)

mydb.commit()   # Required to make the deletion permanent

print(mycursor.rowcount, "record(s) deleted")
```

**SQL breakdown:**
- `DELETE FROM customers` — remove rows from the customers table
- `WHERE address = 'Mountain 21'` — but only rows where address matches

**Expected output:**
```
1 record(s) deleted
```

---

### 6.2 — DELETE with SQL Injection protection

```python
sql = "DELETE FROM customers WHERE address = %s"
adr = ("Yellow Garden 2", )    # Tuple with one value

mycursor.execute(sql, adr)

mydb.commit()

print(mycursor.rowcount, "record(s) deleted")
```

> **Rule:** Use `%s` placeholders whenever the value comes from outside your code — user input, API data, config files, etc.

---

### 6.3 — The danger of DELETE without WHERE

```python
# ⚠️ THIS DELETES EVERY SINGLE ROW IN THE TABLE
sql = "DELETE FROM customers"
mycursor.execute(sql)
mydb.commit()
# The customers table is now completely empty!
```

This is one of the most dangerous mistakes in database programming. **Always double-check your DELETE statements have a WHERE clause.**

---

## Part 7 — JOIN: Combining Two Tables

### What is JOIN and why does it exist?

In real-world databases, information is split across **multiple tables** to avoid repetition. For example:
- A `users` table stores user names and IDs
- A `products` table stores product names and IDs
- Users can "favourite" a product — but you don't copy the product name into the users table

Instead, you store the product's ID in the users table, and use `JOIN` to link them when needed.

**Analogy:** Imagine two lists. List A is your class roster (student name + favourite subject code). List B is the subject list (subject code + subject name). JOIN combines them so you can see "John → Mathematics" instead of just "John → 101".

---

### The sample tables for this section

```
users table:
{ id: 1, name: 'John',    fav: 154 }
{ id: 2, name: 'Peter',   fav: 154 }
{ id: 3, name: 'Amy',     fav: 155 }
{ id: 4, name: 'Hannah',  fav: NULL }
{ id: 5, name: 'Michael', fav: NULL }

products table:
{ id: 154, name: 'Chocolate Heaven' }
{ id: 155, name: 'Tasty Lemons'     }
{ id: 156, name: 'Vanilla Dreams'   }
```

The `fav` column in users matches the `id` column in products. Hannah and Michael have no favourite (NULL/empty).

---

### 7.1 — INNER JOIN (only matching rows)

`INNER JOIN` returns rows where there is a **match in both tables**. Rows without a match are excluded.

```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword",
    database="mydatabase"
)

mycursor = mydb.cursor()

sql = """SELECT
  users.name AS user,
  products.name AS favorite
FROM users
INNER JOIN products ON users.fav = products.id"""

mycursor.execute(sql)

myresult = mycursor.fetchall()

for x in myresult:
    print(x)
```

**SQL breakdown line by line:**

```sql
SELECT
  users.name AS user,       -- Get name from users table, label it "user"
  products.name AS favorite -- Get name from products table, label it "favorite"
FROM users                  -- Start with the users table
INNER JOIN products         -- Connect it to the products table
ON users.fav = products.id  -- Match where users.fav equals products.id
```

- `table.column` syntax — when two tables have a column with the same name (like `name`), you must specify which table's column you want using `tablename.columnname`
- `AS user` — renames the column in the output (called an alias)
- `ON` — specifies how the two tables are linked

**Expected output:**
```
('John', 'Chocolate Heaven')
('Peter', 'Chocolate Heaven')
('Amy', 'Tasty Lemons')
```

Notice Hannah and Michael are **not included** because their `fav` is NULL — no matching product.

> **Note:** `JOIN` and `INNER JOIN` are identical. You can use either.

---

### 7.2 — LEFT JOIN (all from left table, matched from right)

`LEFT JOIN` returns **all rows from the first (left) table**, plus matching data from the second table where available. If there is no match, the right side shows `None`.

```python
sql = """SELECT
  users.name AS user,
  products.name AS favorite
FROM users
LEFT JOIN products ON users.fav = products.id"""

mycursor.execute(sql)

myresult = mycursor.fetchall()

for x in myresult:
    print(x)
```

**Expected output:**
```
('John', 'Chocolate Heaven')
('Peter', 'Chocolate Heaven')
('Amy', 'Tasty Lemons')
('Hannah', None)
('Michael', None)
```

Now Hannah and Michael appear — but their favourite shows as `None` because they have no matching product.

**Use case:** Show ALL customers and their orders, including customers who haven't ordered anything yet.

---

### 7.3 — RIGHT JOIN (all from right table, matched from left)

`RIGHT JOIN` is the opposite — it returns **all rows from the second (right) table**, plus matching data from the left table.

```python
sql = """SELECT
  users.name AS user,
  products.name AS favorite
FROM users
RIGHT JOIN products ON users.fav = products.id"""

mycursor.execute(sql)

myresult = mycursor.fetchall()

for x in myresult:
    print(x)
```

**Expected output:**
```
('John', 'Chocolate Heaven')
('Peter', 'Chocolate Heaven')
('Amy', 'Tasty Lemons')
(None, 'Vanilla Dreams')
```

Now all products appear, including Vanilla Dreams which nobody has as a favourite — but Hannah and Michael are excluded.

**Use case:** Show ALL products and who likes them, including products nobody likes yet.

---

### JOIN summary table

| Join Type | Left table rows | Right table rows |
|---|---|---|
| `INNER JOIN` | Only matched | Only matched |
| `LEFT JOIN` | All rows | Only matched (None for unmatched) |
| `RIGHT JOIN` | Only matched (None for unmatched) | All rows |

---

## Guided Practice Exercises

### Exercise 1 — Reading and Filtering Data

**Objective:** Practice SELECT and WHERE together.

**Scenario:** You manage a school database. The `students` table has columns: `id`, `name`, `grade`, `city`.

**Steps:**
1. Connect to your database.
2. Select all students.
3. Select only `name` and `grade` columns.
4. Select students whose city is 'Lagos'.
5. Select students whose name contains the letter 'a'.

**Starter code:**
```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="root",
    password="yourpassword",
    database="school"
)
mycursor = mydb.cursor()

# Step 2 - All students
mycursor.execute("SELECT * FROM students")
print("All students:")
for row in mycursor.fetchall():
    print(row)

# Step 3 - Only name and grade
mycursor.execute("SELECT name, grade FROM students")
print("\nNames and grades:")
for row in mycursor.fetchall():
    print(row)

# Step 4 - Students from Lagos (use %s for safety)
mycursor.execute("SELECT * FROM students WHERE city = %s", ("Lagos",))
print("\nStudents from Lagos:")
for row in mycursor.fetchall():
    print(row)

# Step 5 - Names containing 'a'
mycursor.execute("SELECT * FROM students WHERE name LIKE %s", ("%a%",))
print("\nNames containing 'a':")
for row in mycursor.fetchall():
    print(row)
```

**Expected output** (example):
```
All students:
(1, 'Amara', 'A', 'Lagos')
(2, 'John', 'B', 'Abuja')
(3, 'Fatima', 'A', 'Lagos')

Names and grades:
('Amara', 'A')
('John', 'B')
('Fatima', 'A')

Students from Lagos:
(1, 'Amara', 'A', 'Lagos')
(3, 'Fatima', 'A', 'Lagos')

Names containing 'a':
(1, 'Amara', 'A', 'Lagos')
(3, 'Fatima', 'A', 'Lagos')
```

**Self-check questions:**
- What changes if you use `LIKE '%A%'` instead of `LIKE '%a%'`?
- What does `fetchone()` return instead of `fetchall()`?

---

### Exercise 2 — Sorting and Limiting

**Objective:** Practice ORDER BY and LIMIT.

**Scenario:** You run an online store. The `products` table has: `id`, `name`, `price`, `stock`.

**Steps:**
1. Get all products sorted by price (cheapest first).
2. Get all products sorted by name Z to A.
3. Get only the 3 most expensive products. (Hint: sort DESC then LIMIT 3)
4. Get products 4 through 6 by price. (Hint: LIMIT 3 OFFSET 3)

**Code:**
```python
# Step 1 - Cheapest first
mycursor.execute("SELECT * FROM products ORDER BY price")
print("Products by price (cheap first):")
for row in mycursor.fetchall():
    print(row)

# Step 2 - Name Z to A
mycursor.execute("SELECT * FROM products ORDER BY name DESC")
print("\nProducts by name (Z to A):")
for row in mycursor.fetchall():
    print(row)

# Step 3 - Top 3 most expensive
mycursor.execute("SELECT * FROM products ORDER BY price DESC LIMIT 3")
print("\nTop 3 most expensive:")
for row in mycursor.fetchall():
    print(row)

# Step 4 - Products 4 to 6 by price
mycursor.execute("SELECT * FROM products ORDER BY price LIMIT 3 OFFSET 3")
print("\nProducts 4 to 6 by price:")
for row in mycursor.fetchall():
    print(row)
```

**What-if challenge:** Change OFFSET to 0. What changes? Change LIMIT to 1. What do you get?

---

### Exercise 3 — Updating and Deleting Safely

**Objective:** Practice UPDATE and DELETE with WHERE and %s.

**Scenario:** You manage an employee database. Table `employees` has: `id`, `name`, `department`, `salary`.

**Code:**
```python
# Update salary for employees in 'Sales' department
sql = "UPDATE employees SET salary = %s WHERE department = %s"
val = (75000, "Sales")
mycursor.execute(sql, val)
mydb.commit()
print(mycursor.rowcount, "employee(s) salary updated")

# Delete employees in department 'Temp'
sql = "DELETE FROM employees WHERE department = %s"
mycursor.execute(sql, ("Temp",))
mydb.commit()
print(mycursor.rowcount, "temp employee(s) removed")

# Verify the changes
mycursor.execute("SELECT * FROM employees")
for row in mycursor.fetchall():
    print(row)
```

**Self-check questions:**
- What would happen if you forgot `mydb.commit()` after UPDATE?
- What would happen if you forgot the WHERE clause in DELETE?

---

## Mini Project: Customer Order Management System

Build a simple system that queries and manages a shop's data.

### Setup — Assumed Tables

```
customers table: id, name, city
orders table:    id, customer_id, product, amount
```

### Stage 1 — Display all customers sorted alphabetically

```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="root",
    password="yourpassword",
    database="shop"
)
mycursor = mydb.cursor()

print("=== CUSTOMER LIST ===")
mycursor.execute("SELECT * FROM customers ORDER BY name")
for row in mycursor.fetchall():
    print(f"ID: {row[0]} | Name: {row[1]} | City: {row[2]}")
```

**Milestone output:**
```
=== CUSTOMER LIST ===
ID: 3  | Name: Amy    | City: London
ID: 1  | Name: John   | City: Oslo
ID: 2  | Name: Peter  | City: Berlin
```

---

### Stage 2 — Show only customers from a specific city

```python
target_city = "Oslo"   # In a real app this could come from user input

print(f"\n=== CUSTOMERS IN {target_city} ===")
mycursor.execute("SELECT * FROM customers WHERE city = %s", (target_city,))
for row in mycursor.fetchall():
    print(f"  {row[1]}")
```

**Milestone output:**
```
=== CUSTOMERS IN Oslo ===
  John
```

---

### Stage 3 — Show the top 3 orders by amount

```python
print("\n=== TOP 3 ORDERS ===")
mycursor.execute("SELECT * FROM orders ORDER BY amount DESC LIMIT 3")
for row in mycursor.fetchall():
    print(f"Order #{row[0]} | Product: {row[2]} | Amount: ${row[3]}")
```

**Milestone output:**
```
=== TOP 3 ORDERS ===
Order #5 | Product: Laptop    | Amount: $1200
Order #2 | Product: Monitor   | Amount: $450
Order #8 | Product: Keyboard  | Amount: $80
```

---

### Stage 4 — Join customers and orders to show full info

```python
print("\n=== CUSTOMERS AND THEIR ORDERS ===")
sql = """SELECT
    customers.name AS customer,
    orders.product AS product,
    orders.amount AS amount
FROM customers
INNER JOIN orders ON customers.id = orders.customer_id
ORDER BY customers.name"""

mycursor.execute(sql)
for row in mycursor.fetchall():
    print(f"  {row[0]} ordered {row[1]} for ${row[2]}")
```

**Milestone output:**
```
=== CUSTOMERS AND THEIR ORDERS ===
  Amy ordered Keyboard for $80
  John ordered Laptop for $1200
  John ordered Monitor for $450
```

---

### Stage 5 — Update a customer's city

```python
# Update John's city from Oslo to Stockholm
sql = "UPDATE customers SET city = %s WHERE name = %s"
val = ("Stockholm", "John")
mycursor.execute(sql, val)
mydb.commit()
print(f"\nUpdated {mycursor.rowcount} record(s)")

# Verify
mycursor.execute("SELECT * FROM customers WHERE name = %s", ("John",))
print("John's new record:", mycursor.fetchone())
```

**Milestone output:**
```
Updated 1 record(s)
John's new record: (1, 'John', 'Stockholm')
```

---

### Stage 6 — Delete test/expired orders

```python
# Delete orders with amount below $10 (perhaps test entries)
sql = "DELETE FROM orders WHERE amount < %s"
mycursor.execute(sql, (10,))
mydb.commit()
print(f"\nRemoved {mycursor.rowcount} low-value order(s)")
```

---

### Optional Extensions

- Add a `LEFT JOIN` to show customers who have NO orders yet
- Show a paginated list: first 5 orders, then next 5
- Sort the joined result by amount DESC to show most expensive orders first

---

## Common Beginner Mistakes

**Mistake 1: Forgetting `mydb.commit()` after UPDATE or DELETE**
```python
# Wrong — the change never gets saved!
mycursor.execute("UPDATE customers SET city = 'Lagos' WHERE id = 1")
# Forgot commit — nothing changes in the database

# Correct
mycursor.execute("UPDATE customers SET city = 'Lagos' WHERE id = 1")
mydb.commit()  # This saves the change
```

**Mistake 2: Using DELETE or UPDATE without WHERE**
```python
# Deletes EVERY row — catastrophic!
mycursor.execute("DELETE FROM customers")

# Updates EVERY row — also catastrophic!
mycursor.execute("UPDATE customers SET city = 'Lagos'")
```

**Mistake 3: Building SQL by string concatenation with user input**
```python
# DANGEROUS — SQL injection vulnerability
user_city = input("Enter city: ")
sql = "SELECT * FROM customers WHERE city = '" + user_city + "'"

# SAFE
sql = "SELECT * FROM customers WHERE city = %s"
mycursor.execute(sql, (user_city,))
```

**Mistake 4: Forgetting the trailing comma in a single-value tuple**
```python
# Wrong — this is just a string in brackets, not a tuple
val = ("Lagos")         # This is just "Lagos"

# Correct — the comma makes it a tuple
val = ("Lagos",)        # This is a tuple with one item
```

**Mistake 5: Confusing `fetchall()` and `fetchone()`**
```python
mycursor.execute("SELECT * FROM customers")
row = mycursor.fetchone()   # Gets first row only
print(row)                  # (1, 'John', 'Oslo')

# If you call fetchone() again...
row2 = mycursor.fetchone()  # Gets the SECOND row (cursor moved forward)
print(row2)                 # (2, 'Peter', 'Berlin')
```

**Mistake 6: Using `*` in JOINs when both tables have a column called `name`**
```python
# This could confuse which "name" column is which
sql = "SELECT * FROM users INNER JOIN products ON users.fav = products.id"

# Better — explicitly select what you need with aliases
sql = "SELECT users.name AS user, products.name AS product FROM users INNER JOIN products ON users.fav = products.id"
```

---

## Reflection Questions

1. What is the difference between `fetchall()` and `fetchone()`? When would you use each?
2. Why is `mydb.commit()` required for UPDATE and DELETE but not for SELECT?
3. What is SQL injection? How does using `%s` placeholders prevent it?
4. You have a table with 50,000 rows. You only need to display 10 at a time on a webpage. Which SQL keywords would you use?
5. What is the difference between INNER JOIN, LEFT JOIN, and RIGHT JOIN? Give a real-world example for each.
6. Why is it dangerous to run `DELETE FROM tablename` without a `WHERE` clause?
7. How would you find all customers whose names start with the letter 'S'?
8. You need to show the top 10 best-selling products. Which SQL keywords would you combine?

---

## Completion Checklist

Use this checklist to confirm you have mastered this lesson:

- [ ] I can connect Python to a MySQL database using `mysql.connector`
- [ ] I can use `SELECT *` to retrieve all rows and columns from a table
- [ ] I can use `SELECT column1, column2` to retrieve specific columns
- [ ] I understand the difference between `fetchall()` and `fetchone()`
- [ ] I can use `WHERE` to filter rows by an exact match
- [ ] I can use `WHERE column LIKE '%pattern%'` for partial matches
- [ ] I always use `%s` placeholders to prevent SQL injection
- [ ] I can sort results with `ORDER BY column ASC` and `ORDER BY column DESC`
- [ ] I can limit results with `LIMIT N`
- [ ] I can skip rows using `OFFSET N` for pagination
- [ ] I can update existing rows with `UPDATE ... SET ... WHERE`
- [ ] I always call `mydb.commit()` after UPDATE and DELETE
- [ ] I can delete rows with `DELETE FROM ... WHERE`
- [ ] I understand the danger of UPDATE/DELETE without WHERE
- [ ] I can use `INNER JOIN` to combine two tables showing only matched rows
- [ ] I can use `LEFT JOIN` to include all rows from the left table
- [ ] I can use `RIGHT JOIN` to include all rows from the right table
- [ ] I completed the Customer Order Management mini-project

---

## Lesson Summary

In this lesson you mastered the **core operations** for working with MySQL data in Python:

**Reading data:** `SELECT * FROM table` gets all data. `SELECT col1, col2` gets specific columns. `fetchall()` retrieves all rows; `fetchone()` retrieves just the first.

**Filtering:** `WHERE column = value` narrows results to matching rows. `LIKE '%pattern%'` enables partial matching. Always use `%s` placeholders to prevent SQL injection.

**Sorting:** `ORDER BY column` sorts ascending (A→Z). `ORDER BY column DESC` sorts descending (Z→A).

**Limiting:** `LIMIT N` caps results at N rows. `LIMIT N OFFSET M` skips the first M rows — perfect for pagination.

**Modifying:** `UPDATE table SET column = value WHERE condition` changes existing data. Always use `mydb.commit()` to save. Always include `WHERE` to avoid changing every row.

**Deleting:** `DELETE FROM table WHERE condition` removes matching rows. Always use `mydb.commit()`. Always include `WHERE` to avoid deleting everything.

**Joining:** `INNER JOIN` returns only rows with matches in both tables. `LEFT JOIN` returns all left rows plus matches. `RIGHT JOIN` returns all right rows plus matches.

These seven operations — SELECT, WHERE, ORDER BY, LIMIT, UPDATE, DELETE, JOIN — are the foundation of virtually every database-powered application in the world. Master them and you can build anything from a student gradebook to a complete e-commerce system.
