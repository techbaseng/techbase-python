---
render_with_liquid: false
title: "Python MongoDB — Querying, Sorting, Limiting, Updating, and Deleting Documents"
nav_order: 43
---

# Lesson 43: Python MongoDB — Querying, Sorting, Limiting, Updating, and Deleting Documents

---

## Lesson Introduction

Welcome to Lesson 43! In this lesson, you will learn five of the most important and powerful skills for working with a MongoDB database using Python. Together, these skills let you **find exactly the data you want**, **arrange it neatly**, **control how much you get back**, **change existing data**, and **remove data you no longer need**.

Think of a MongoDB collection like a giant filing cabinet full of folders (documents). Right now you know how to open the cabinet and read every folder. This lesson teaches you how to:

- **Query** — Open only the folders that match a rule (e.g. "only folders from 2024")
- **Sort** — Arrange the matching folders alphabetically or numerically
- **Limit** — Say "give me only the first 5 folders, not all 500"
- **Update** — Open a folder and change what is written inside
- **Delete** — Throw a folder (or several) in the bin

These five operations together with what you already know about inserting and finding give you complete control over a MongoDB database. By the end of this lesson you will be able to build a real working customer management system.

> **Why does this matter in the real world?**
> Every app you use every day — Instagram, your banking app, Google — does all five of these operations thousands of times per second on databases exactly like this one.

---

## Prerequisite Concepts

Before we dive in, make sure you understand these ideas. If anything here is new to you, read this section carefully — it will make everything else much easier.

### What is MongoDB and pymongo?

**MongoDB** is a database that stores data as **documents**. A document is just a Python dictionary — it has keys and values. For example:

```python
{"name": "Alice", "address": "Baker Street 1", "age": 30}
```

This is one document. A **collection** is a group of documents (like a table in Excel). A **database** holds multiple collections.

**pymongo** is the Python library that lets your Python code talk to MongoDB.

### The Standard Setup Block

Every example in this lesson starts with the same three lines. Learn this block by heart:

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]
```

Line by line:
- `import pymongo` — loads the pymongo library so we can use it
- `pymongo.MongoClient("mongodb://localhost:27017/")` — connects to MongoDB running on your computer at port 27017 (the default port)
- `myclient["mydatabase"]` — selects the database named "mydatabase"
- `mydb["customers"]` — selects the collection named "customers"

### The Sample Data We Will Use

All examples in this lesson assume the "customers" collection has these 14 documents:

```
{'_id': 1,  'name': 'John',    'address': 'Highway 37'}
{'_id': 2,  'name': 'Peter',   'address': 'Lowstreet 27'}
{'_id': 3,  'name': 'Amy',     'address': 'Apple st 652'}
{'_id': 4,  'name': 'Hannah',  'address': 'Mountain 21'}
{'_id': 5,  'name': 'Michael', 'address': 'Valley 345'}
{'_id': 6,  'name': 'Sandy',   'address': 'Ocean blvd 2'}
{'_id': 7,  'name': 'Betty',   'address': 'Green Grass 1'}
{'_id': 8,  'name': 'Richard', 'address': 'Sky st 331'}
{'_id': 9,  'name': 'Susan',   'address': 'One way 98'}
{'_id': 10, 'name': 'Vicky',   'address': 'Yellow Garden 2'}
{'_id': 11, 'name': 'Ben',     'address': 'Park Lane 38'}
{'_id': 12, 'name': 'William', 'address': 'Central st 954'}
{'_id': 13, 'name': 'Chuck',   'address': 'Main Road 989'}
{'_id': 14, 'name': 'Viola',   'address': 'Sideway 1633'}
```

---

## Part 1 — Querying (Filtering) Documents

### What is a Query?

A **query** is a set of rules you give MongoDB so it only returns documents that match those rules, instead of returning everything.

**Real-life analogy:** Imagine searching your email inbox. Instead of reading all 10,000 emails, you type "subject:invoice" and only the matching emails appear. That search is a query.

Without a query:
```
You ask: "Give me all customers."
MongoDB returns: all 14 customers
```

With a query:
```
You ask: "Give me customers whose address is 'Park Lane 38'."
MongoDB returns: just Ben (document 11)
```

### How to Write a Query in Python

In pymongo, a query is just a **Python dictionary**. You pass it as the first argument to `find()`:

```python
mycol.find( { "field_name": "value_to_match" } )
```

The curly braces `{}` create a dictionary. Inside, you write the field name and the exact value you are looking for.

---

### Simple Exact Match Query

**Example 1 — Find a Customer by Exact Address**

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myquery = { "address": "Park Lane 38" }   # the filter rule

mydoc = mycol.find(myquery)               # run the search

for x in mydoc:
    print(x)                              # print each matching document
```

**Expected Output:**
```
{'_id': 11, 'name': 'Ben', 'address': 'Park Lane 38'}
```

**Line by line explanation:**
- `myquery = { "address": "Park Lane 38" }` — creates a dictionary that says "I only want documents where the 'address' field equals exactly 'Park Lane 38'"
- `mycol.find(myquery)` — sends this filter to MongoDB; it searches every document and returns only the matches
- `for x in mydoc:` — loops through each matching document one at a time
- `print(x)` — prints that document as a dictionary

> **Thinking Prompt:** What would happen if you changed "Park Lane 38" to "park lane 38" (lowercase)? MongoDB queries are **case-sensitive**, so it would find nothing. Exact spelling matters!

---

### Example 2 — Find a Customer by Name

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myquery = { "name": "Amy" }

mydoc = mycol.find(myquery)

for x in mydoc:
    print(x)
```

**Expected Output:**
```
{'_id': 3, 'name': 'Amy', 'address': 'Apple st 652'}
```

---

### Advanced Query: Using Comparison Operators (Modifiers)

Sometimes you don't want an exact match. You want something like:
- "Give me all addresses that come after 'S' alphabetically"
- "Give me all customers whose age is greater than 30"

MongoDB provides special **operators** (also called modifiers) for this. An operator is a keyword that starts with a dollar sign `$`. You put it inside the query dictionary as the value.

#### The `$gt` Operator (Greater Than)

`$gt` means "greater than". For text (strings), MongoDB compares alphabetically. The letter "S" comes after "A", "B", "C"... so anything starting with "S" or later is "greater than" things starting with "R" or earlier.

**Structure:**
```python
myquery = { "field_name": { "$gt": "comparison_value" } }
```

The value is now itself a dictionary containing the operator.

**Example 3 — Find Addresses Starting with "S" or Later (Alphabetically)**

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myquery = { "address": { "$gt": "S" } }   # address must come after "S" alphabetically

mydoc = mycol.find(myquery)

for x in mydoc:
    print(x)
```

**Expected Output:**
```
{'_id': 5,  'name': 'Michael', 'address': 'Valley 345'}
{'_id': 8,  'name': 'Richard', 'address': 'Sky st 331'}
{'_id': 9,  'name': 'Susan',   'address': 'One way 98'}  ← Wait... does "One" come after "S"?
```

> Actually, MongoDB compares the whole string starting from the first character. "Valley" starts with "V" (after "S"), "Sky" starts with "S" (equal, then "k" which is after "S"), "Sideway" starts with "S". "One" starts with "O" which comes before "S", so it would NOT be in the result.

The actual output (addresses that are alphabetically after "S"):
```
{'_id': 5,  'name': 'Michael', 'address': 'Valley 345'}
{'_id': 8,  'name': 'Richard', 'address': 'Sky st 331'}
{'_id': 14, 'name': 'Viola',   'address': 'Sideway 1633'}
{'_id': 10, 'name': 'Vicky',   'address': 'Yellow Garden 2'}
```

> **Thinking Prompt:** What happens if you change `"$gt"` to `"$lt"` (less than)? You would get all addresses that come before "S" alphabetically — the opposite!

---

#### Common Query Operators

| Operator | Meaning | Example |
|---|---|---|
| `$gt` | Greater than | `{"age": {"$gt": 18}}` → age > 18 |
| `$lt` | Less than | `{"age": {"$lt": 65}}` → age < 65 |
| `$gte` | Greater than or equal | `{"age": {"$gte": 18}}` → age >= 18 |
| `$lte` | Less than or equal | `{"age": {"$lte": 65}}` → age <= 65 |
| `$ne` | Not equal | `{"name": {"$ne": "Alice"}}` → name ≠ Alice |

---

### Advanced Query: Using Regular Expressions (`$regex`)

A **regular expression** (regex) is a pattern used to search inside text. Think of it like a wildcard search.

> **Important:** `$regex` only works on text (string) fields, not numbers.

#### The `^` Symbol — Starts With

In regex, `^` means "starts with". So `"^S"` means "starts with the letter S".

**Example 4 — Find All Customers Whose Address Starts with "S"**

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myquery = { "address": { "$regex": "^S" } }   # address must start with "S"

mydoc = mycol.find(myquery)

for x in mydoc:
    print(x)
```

**Expected Output:**
```
{'_id': 8,  'name': 'Richard', 'address': 'Sky st 331'}
{'_id': 14, 'name': 'Viola',   'address': 'Sideway 1633'}
```

**Explanation:**
- `"$regex": "^S"` — the pattern `^S` means the address field must **start with** the letter "S"
- "Sky st 331" — starts with S ✓
- "Sideway 1633" — starts with S ✓
- "Sandy" was removed in a previous step; "Ocean blvd 2" starts with O — does NOT match

> **Comparing `$gt: "S"` vs `$regex: "^S"`:**
> - `$gt: "S"` finds everything alphabetically after the letter S (not just things starting with S — it includes "Valley", "Yellow" etc.)
> - `$regex: "^S"` finds ONLY things that literally start with the letter S

**Example 5 — Find Names that Start with "B"**

```python
myquery = { "name": { "$regex": "^B" } }
mydoc = mycol.find(myquery)
for x in mydoc:
    print(x)
```

**Expected Output:**
```
{'_id': 7,  'name': 'Betty', 'address': 'Green Grass 1'}
{'_id': 11, 'name': 'Ben',   'address': 'Park Lane 38'}
```

---

## Part 2 — Sorting Results

### What is Sorting?

**Sorting** means arranging the results in a specific order before they come back to you. Without sorting, MongoDB returns documents in the order they were stored, which can feel random.

**Real-life analogy:** Imagine a phone book. If it were not sorted alphabetically, you would have to read every single entry to find someone. Sorting makes data useful.

### The `sort()` Method

You chain `sort()` after `find()`:

```python
mycol.find().sort("field_name")             # ascending (A to Z, 0 to 9)
mycol.find().sort("field_name", 1)          # ascending (same — 1 means ascending)
mycol.find().sort("field_name", -1)         # descending (Z to A, 9 to 0)
```

The second argument is the **direction**:
- `1` = ascending (A → Z, smallest → largest) — this is the **default**
- `-1` = descending (Z → A, largest → smallest)

---

### Example 6 — Sort Customers Alphabetically by Name (A to Z)

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

mydoc = mycol.find().sort("name")   # sort by "name" field, ascending

for x in mydoc:
    print(x)
```

**Expected Output (abbreviated — first few):**
```
{'_id': 3,  'name': 'Amy',     'address': 'Apple st 652'}
{'_id': 11, 'name': 'Ben',     'address': 'Park Lane 38'}
{'_id': 7,  'name': 'Betty',   'address': 'Green Grass 1'}
{'_id': 12, 'name': 'William', 'address': 'Central st 954'}
...
```

The names are now in alphabetical order: Amy, Ben, Betty ... William.

---

### Example 7 — Sort Customers Reverse Alphabetically by Name (Z to A)

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

mydoc = mycol.find().sort("name", -1)   # -1 means descending

for x in mydoc:
    print(x)
```

**Expected Output (abbreviated — first few):**
```
{'_id': 12, 'name': 'William', 'address': 'Central st 954'}
{'_id': 14, 'name': 'Viola',   'address': 'Sideway 1633'}
{'_id': 10, 'name': 'Vicky',   'address': 'Yellow Garden 2'}
...
{'_id': 3,  'name': 'Amy',     'address': 'Apple st 652'}
```

William comes first because W is the last letter alphabetically in our list.

---

### Combining Query and Sort

You can filter AND sort in one go:

**Example 8 — Find addresses starting with "S" and sort them by name**

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myquery = { "address": { "$regex": "^S" } }
mydoc = mycol.find(myquery).sort("name")   # filter THEN sort

for x in mydoc:
    print(x)
```

**Expected Output:**
```
{'_id': 8,  'name': 'Richard', 'address': 'Sky st 331'}
{'_id': 14, 'name': 'Viola',   'address': 'Sideway 1633'}
```

> **Thinking Prompt:** What happens if you sort by `"address"` instead of `"name"`? The order would change — Sky comes before Sideway alphabetically, so Richard appears first.

---

## Part 3 — Limiting Results

### What is Limiting?

**Limiting** means telling MongoDB "I only want the first N documents — stop after that."

**Real-life analogy:** Think of a Google search. There are millions of results, but Google only shows you 10 per page. That is limiting. You are not loading all one million results at once — that would be slow and overwhelming.

**Why use limiting in real apps?**
- Your database has 500,000 customers. You only want to show 20 per page on a website.
- You want to preview the first 5 results before deciding to download all of them.
- You want to get the "Top 10" of something.

### The `limit()` Method

You chain `limit()` after `find()`:

```python
mycol.find().limit(5)    # return only the first 5 documents
```

The number inside is how many documents you want maximum.

---

### Example 9 — Get Only the First 5 Customers

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myresult = mycol.find().limit(5)   # stop after 5 documents

for x in myresult:
    print(x)
```

**Expected Output:**
```
{'_id': 1, 'name': 'John',    'address': 'Highway 37'}
{'_id': 2, 'name': 'Peter',   'address': 'Lowstreet 27'}
{'_id': 3, 'name': 'Amy',     'address': 'Apple st 652'}
{'_id': 4, 'name': 'Hannah',  'address': 'Mountain 21'}
{'_id': 5, 'name': 'Michael', 'address': 'Valley 345'}
```

Only 5 documents come back, even though there are 14 in the collection.

---

### Example 10 — Get the Top 3 Names Alphabetically

You can combine `sort()` and `limit()`:

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myresult = mycol.find().sort("name").limit(3)   # sort A-Z, then take first 3

for x in myresult:
    print(x)
```

**Expected Output:**
```
{'_id': 3,  'name': 'Amy',   'address': 'Apple st 652'}
{'_id': 11, 'name': 'Ben',   'address': 'Park Lane 38'}
{'_id': 7,  'name': 'Betty', 'address': 'Green Grass 1'}
```

> **Thinking Prompt:** What happens if you use `.sort("name", -1).limit(3)` instead? You get the last 3 names alphabetically: William, Viola, Vicky.

---

## Part 4 — Updating Documents

### What is Updating?

**Updating** means changing the value of one or more fields inside an existing document — without deleting and recreating the whole document.

**Real-life analogy:** Imagine you have a contacts app. You don't delete and re-add a contact just to change their phone number. You open the contact, change the number, and save. That is an update.

### Two Update Methods

| Method | What it does |
|---|---|
| `update_one()` | Updates only the **first** document that matches the query |
| `update_many()` | Updates **all** documents that match the query |

### The `$set` Operator

When updating, you must tell MongoDB **what to change**. You do this using the `$set` operator:

```python
newvalues = { "$set": { "field_to_change": "new_value" } }
```

- `$set` tells MongoDB: "Only change these specific fields — leave everything else alone."
- Without `$set`, MongoDB might replace the entire document!

---

### Example 11 — Update One Document (`update_one`)

**Scenario:** Michael moved. His address changed from "Valley 345" to "Canyon 123".

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myquery  = { "address": "Valley 345" }        # find the document with this address
newvalues = { "$set": { "address": "Canyon 123" } }  # change the address to this

mycol.update_one(myquery, newvalues)    # update ONLY the first match

# Verify the change by printing all customers
for x in mycol.find():
    print(x)
```

**Expected Output (Michael's record):**
```
{'_id': 5, 'name': 'Michael', 'address': 'Canyon 123'}
```

Michael's address has been updated. All other documents are untouched.

**How `update_one()` works — input → process → output:**
1. **Input:** Query `{"address": "Valley 345"}` and new values `{"$set": {"address": "Canyon 123"}}`
2. **Process:** MongoDB searches for a document with address "Valley 345". Finds Michael. Changes his address field to "Canyon 123".
3. **Output:** Michael's document is permanently changed in the database.

> **Important Warning:** If the query matches MORE than one document, `update_one()` only changes the **first one it finds**. If you want to change all matches, use `update_many()`.

---

### Example 12 — Update Many Documents (`update_many`)

**Scenario:** All customers whose address starts with "S" have been renamed to "Minnie" in a test database exercise.

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myquery  = { "address": { "$regex": "^S" } }   # all addresses starting with S
newvalues = { "$set": { "name": "Minnie" } }     # change their name to Minnie

x = mycol.update_many(myquery, newvalues)

print(x.modified_count, "documents updated.")
```

**Expected Output:**
```
2 documents updated.
```

- `x.modified_count` — this is a property that tells you how many documents were actually changed
- In our dataset, "Sky st 331" (Richard) and "Sideway 1633" (Viola) both start with S, so 2 documents are updated

**After running this, the database would show:**
```
{'_id': 8,  'name': 'Minnie', 'address': 'Sky st 331'}
{'_id': 14, 'name': 'Minnie', 'address': 'Sideway 1633'}
```

> **Thinking Prompt:** Why is it safer to use `update_one()` when you only mean to change one record? If you accidentally write a query that is too broad (matches too many documents), `update_many()` could change hundreds of records at once!

---

### The `$set` Operator in Detail

`$set` is a MongoDB **update operator**. It tells MongoDB to update only specific fields, leaving the rest of the document unchanged.

**Without `$set` (DANGEROUS — don't do this):**
```python
# This would REPLACE the entire document with just the new address!
mycol.update_one({"name": "John"}, {"address": "New Road 1"})
# John's name field would DISAPPEAR!
```

**With `$set` (SAFE — always do this):**
```python
# This changes ONLY the address; name and all other fields remain intact
mycol.update_one({"name": "John"}, {"$set": {"address": "New Road 1"}})
```

> Always use `$set` when updating specific fields.

---

## Part 5 — Deleting Documents

### What is Deleting?

**Deleting** means permanently removing one or more documents from a collection.

**Real-life analogy:** When you delete a contact from your phone, or cancel an account on a website, the system is running a delete operation to remove your record from the database.

> **Warning:** Deleting in MongoDB is **permanent**. There is no "undo" button. Always be careful with delete operations, especially `delete_many()`.

### Three Delete Approaches

| Method | What it does |
|---|---|
| `delete_one()` | Deletes the **first** document that matches the query |
| `delete_many()` | Deletes **all** documents that match the query |
| `delete_many({})` | Deletes **ALL** documents (empty query = match everything) |

---

### Example 13 — Delete One Document (`delete_one`)

**Scenario:** Hannah has cancelled her account. Delete her record.

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myquery = { "address": "Mountain 21" }   # Hannah's address — find her document

mycol.delete_one(myquery)                # delete the first match
```

After running this, Hannah's document is gone. The collection now has 13 documents instead of 14.

> **Note:** `delete_one()` returns a result object, but you don't have to use it. If you want to confirm the deletion, you can call `mycol.find()` afterwards to check.

---

### Example 14 — Delete Many Documents (`delete_many`)

**Scenario:** All customers with an address starting with "S" are being removed from the system.

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myquery = { "address": { "$regex": "^S" } }   # all addresses starting with "S"

x = mycol.delete_many(myquery)

print(x.deleted_count, " documents deleted.")
```

**Expected Output:**
```
2  documents deleted.
```

- `x.deleted_count` — tells you exactly how many documents were removed
- This is useful for logging or confirming the operation worked

---

### Example 15 — Delete ALL Documents in a Collection

**Warning: This removes every single document. Use with extreme caution.**

To delete everything, pass an **empty dictionary** `{}` as the query. An empty query means "match every document":

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

x = mycol.delete_many({})    # empty query = match ALL documents

print(x.deleted_count, " documents deleted.")
```

**Expected Output (if all 14 documents are still present):**
```
14  documents deleted.
```

The collection now exists but is completely empty. This is different from dropping the collection entirely — the collection structure still exists, it just has no documents inside.

> **When would you use this in real life?**
> - Clearing a test/staging database before running a fresh test
> - Resetting a session or cache collection
> - Wiping temporary data that should not persist overnight

---

## Guided Practice Exercises

### Exercise 1 — Query Practice

**Objective:** Find specific customers using different query techniques.

**Scenario:** You work at a delivery company. You need to look up customers by address.

**Step 1:** Find the customer at "Green Grass 1":
```python
myquery = { "address": "Green Grass 1" }
mydoc = mycol.find(myquery)
for x in mydoc:
    print(x)
```

**Expected Output:**
```
{'_id': 7, 'name': 'Betty', 'address': 'Green Grass 1'}
```

**Step 2:** Find all customers whose name starts with "V":
```python
myquery = { "name": { "$regex": "^V" } }
mydoc = mycol.find(myquery)
for x in mydoc:
    print(x)
```

**Expected Output:**
```
{'_id': 10, 'name': 'Vicky', 'address': 'Yellow Garden 2'}
{'_id': 14, 'name': 'Viola', 'address': 'Sideway 1633'}
```

**Self-check Questions:**
- Why do we use `$regex` instead of just `{ "name": "V" }`?
- What would `{ "name": { "$regex": "^Vi" } }` return?

---

### Exercise 2 — Sort Practice

**Objective:** Sort the customer list in different ways.

**Step 1:** Sort all customers by address, A to Z:
```python
mydoc = mycol.find().sort("address")
for x in mydoc:
    print(x)
```

**Expected Output (first few):**
```
{'_id': 3,  'name': 'Amy',    'address': 'Apple st 652'}
{'_id': 12, 'name': 'William','address': 'Central st 954'}
{'_id': 7,  'name': 'Betty',  'address': 'Green Grass 1'}
...
```

**Step 2:** Sort by name, Z to A, and take only the first 3:
```python
mydoc = mycol.find().sort("name", -1).limit(3)
for x in mydoc:
    print(x)
```

**Expected Output:**
```
{'_id': 12, 'name': 'William', 'address': 'Central st 954'}
{'_id': 14, 'name': 'Viola',   'address': 'Sideway 1633'}
{'_id': 10, 'name': 'Vicky',   'address': 'Yellow Garden 2'}
```

---

### Exercise 3 — Update Practice

**Objective:** Update a customer record safely.

**Scenario:** Ben has moved to "Main Street 99". Update his address.

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myquery  = { "name": "Ben" }
newvalues = { "$set": { "address": "Main Street 99" } }

mycol.update_one(myquery, newvalues)

# Verify the change
result = mycol.find_one({ "name": "Ben" })
print(result)
```

**Expected Output:**
```
{'_id': 11, 'name': 'Ben', 'address': 'Main Street 99'}
```

**Optional Challenge:** After updating Ben, try updating all customers whose name starts with "S" and change their address to "Secret Location". How many are updated?

---

### Exercise 4 — Delete Practice

**Objective:** Safely delete a document and confirm the deletion.

**Scenario:** Peter has requested account deletion. Remove his record.

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

# Count documents before deletion
before = mycol.count_documents({})
print(f"Before deletion: {before} documents")

# Delete Peter
mycol.delete_one({ "name": "Peter" })

# Count after deletion
after = mycol.count_documents({})
print(f"After deletion: {after} documents")

# Verify Peter is gone
result = mycol.find_one({ "name": "Peter" })
print(f"Peter found? {result}")
```

**Expected Output:**
```
Before deletion: 14 documents
After deletion: 13 documents
Peter found? None
```

---

## Mini Project — Customer Management System

Let's put everything together in a realistic project. You will build a command-driven customer management system.

### Project Overview

**Goal:** A Python script that can query, sort, update, and delete from the customer database in a structured way.

### Stage 1 — Setup the Database

```python
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

# Insert the sample customers (run once to populate)
customers = [
    {"_id": 1,  "name": "John",    "address": "Highway 37"},
    {"_id": 2,  "name": "Peter",   "address": "Lowstreet 27"},
    {"_id": 3,  "name": "Amy",     "address": "Apple st 652"},
    {"_id": 4,  "name": "Hannah",  "address": "Mountain 21"},
    {"_id": 5,  "name": "Michael", "address": "Valley 345"},
    {"_id": 6,  "name": "Sandy",   "address": "Ocean blvd 2"},
    {"_id": 7,  "name": "Betty",   "address": "Green Grass 1"},
    {"_id": 8,  "name": "Richard", "address": "Sky st 331"},
    {"_id": 9,  "name": "Susan",   "address": "One way 98"},
    {"_id": 10, "name": "Vicky",   "address": "Yellow Garden 2"},
    {"_id": 11, "name": "Ben",     "address": "Park Lane 38"},
    {"_id": 12, "name": "William", "address": "Central st 954"},
    {"_id": 13, "name": "Chuck",   "address": "Main Road 989"},
    {"_id": 14, "name": "Viola",   "address": "Sideway 1633"},
]

mycol.insert_many(customers)
print("Database ready!")
```

**Milestone Output:**
```
Database ready!
```

---

### Stage 2 — Search Functions

```python
def find_by_address(collection, address):
    """Find a customer by their exact address."""
    query = { "address": address }
    results = collection.find(query)
    found = list(results)
    if found:
        for doc in found:
            print(doc)
    else:
        print(f"No customer found at '{address}'")

def find_names_starting_with(collection, letter):
    """Find all customers whose name starts with a given letter."""
    query = { "name": { "$regex": f"^{letter}" } }
    results = collection.find(query)
    for doc in results:
        print(doc)

# Test the search functions
find_by_address(mycol, "Park Lane 38")
find_names_starting_with(mycol, "B")
```

**Milestone Output:**
```
{'_id': 11, 'name': 'Ben', 'address': 'Park Lane 38'}

{'_id': 7,  'name': 'Betty', 'address': 'Green Grass 1'}
{'_id': 11, 'name': 'Ben',   'address': 'Park Lane 38'}
```

---

### Stage 3 — Display Functions (Sort and Limit)

```python
def show_top_customers(collection, n, sort_field="name", direction=1):
    """Show the top N customers sorted by a field."""
    results = collection.find().sort(sort_field, direction).limit(n)
    print(f"\nTop {n} customers sorted by '{sort_field}':")
    for doc in results:
        print(f"  {doc['name']} — {doc['address']}")

# Show top 5 by name A-Z
show_top_customers(mycol, 5, "name", 1)

# Show top 3 by name Z-A
show_top_customers(mycol, 3, "name", -1)
```

**Milestone Output:**
```
Top 5 customers sorted by 'name':
  Amy — Apple st 652
  Ben — Park Lane 38
  Betty — Green Grass 1
  Chuck — Main Road 989
  Hannah — Mountain 21

Top 3 customers sorted by 'name':
  William — Central st 954
  Viola — Sideway 1633
  Vicky — Yellow Garden 2
```

---

### Stage 4 — Modify and Remove Functions

```python
def update_address(collection, name, new_address):
    """Update a customer's address by their name."""
    query  = { "name": name }
    update = { "$set": { "address": new_address } }
    result = collection.update_one(query, update)
    if result.modified_count > 0:
        print(f"✓ {name}'s address updated to '{new_address}'")
    else:
        print(f"✗ No customer named '{name}' was found")

def remove_customer(collection, name):
    """Delete a customer by name."""
    query  = { "name": name }
    result = collection.delete_one(query)
    if result.deleted_count > 0:
        print(f"✓ Customer '{name}' has been removed")
    else:
        print(f"✗ No customer named '{name}' was found")

# Test update and delete
update_address(mycol, "Ben", "New Avenue 5")
remove_customer(mycol, "Hannah")
remove_customer(mycol, "Nobody")   # testing a non-existent customer
```

**Milestone Output:**
```
✓ Ben's address updated to 'New Avenue 5'
✓ Customer 'Hannah' has been removed
✗ No customer named 'Nobody' was found
```

---

### Stage 5 — Final Summary Report

```python
def print_summary(collection):
    """Print a summary of the current database state."""
    total = collection.count_documents({})
    print(f"\n=== Customer Database Summary ===")
    print(f"Total customers: {total}")
    print("\nAll customers (sorted A-Z):")
    for doc in collection.find().sort("name"):
        print(f"  [{doc['_id']}] {doc['name']} — {doc['address']}")

print_summary(mycol)
```

**Milestone Output:**
```
=== Customer Database Summary ===
Total customers: 13

All customers (sorted A-Z):
  [3]  Amy — Apple st 652
  [11] Ben — New Avenue 5
  [7]  Betty — Green Grass 1
  ...
```

---

## Common Beginner Mistakes

### Mistake 1 — Forgetting `$set` in Update

```python
# WRONG — replaces the ENTIRE document with just the new address
mycol.update_one({"name": "John"}, {"address": "New Road 1"})
# John now only has _id and address — name is gone!

# CORRECT — only changes the address field
mycol.update_one({"name": "John"}, {"$set": {"address": "New Road 1"}})
```

---

### Mistake 2 — Case Sensitivity in Queries

```python
# WRONG — will find NOTHING if the actual value is "Park Lane 38"
myquery = { "address": "park lane 38" }

# CORRECT — match exactly as stored
myquery = { "address": "Park Lane 38" }
```

Use `$regex` with the `(?i)` flag for case-insensitive matching:
```python
myquery = { "address": { "$regex": "park lane 38", "$options": "i" } }
```

---

### Mistake 3 — Using `update_one` When You Mean `update_many`

```python
# If 5 customers all have address "Valley 345", this only fixes ONE of them
mycol.update_one({"address": "Valley 345"}, {"$set": {"address": "Canyon 123"}})

# Use update_many to fix all of them
mycol.update_many({"address": "Valley 345"}, {"$set": {"address": "Canyon 123"}})
```

---

### Mistake 4 — Accidentally Deleting Everything

```python
# This deletes EVERY document — there is no undo!
mycol.delete_many({})

# Always add a specific query to be safe
mycol.delete_many({"address": {"$regex": "^S"}})
```

Before any `delete_many()` call, it is good practice to first run `find()` with the same query to see what you are about to delete.

---

### Mistake 5 — Confusing `$gt` (Greater Than) with `$regex` (Pattern Match)

```python
# $gt: "S" → all addresses that come AFTER "S" alphabetically (includes "Valley", "Yellow")
myquery = { "address": { "$gt": "S" } }

# "$regex": "^S" → only addresses that LITERALLY START WITH the letter S
myquery = { "address": { "$regex": "^S" } }
```

They are NOT the same. Use `$regex` when you want pattern matching.

---

### Mistake 6 — Forgetting to Loop Over `find()` Results

```python
# WRONG — this prints a cursor object, not the documents
result = mycol.find({"name": "Amy"})
print(result)
# Output: <pymongo.cursor.Cursor object at 0x...>

# CORRECT — loop through the cursor
result = mycol.find({"name": "Amy"})
for x in result:
    print(x)
# Output: {'_id': 3, 'name': 'Amy', 'address': 'Apple st 652'}
```

---

## Reflection Questions

1. What is the difference between `delete_one()` and `delete_many()`? When would you use each?

2. Why must you always use `$set` when updating a document? What would happen if you forgot it?

3. How is `$gt: "S"` different from `$regex: "^S"`? Can you think of a case where using `$gt` accidentally returns more results than expected?

4. If you want to show only 10 results per page in a web app, which method would you use and why?

5. A colleague runs `mycol.update_many({}, {"$set": {"status": "active"}})`. What does this do? Is this safe or dangerous?

6. You need to find all customers whose name contains the letters "an" anywhere in the name (not just at the start). What regex pattern would you use?

---

## Completion Checklist

Before moving to the next lesson, confirm you can do all of the following:

- [ ] Write a basic exact-match query using a Python dictionary
- [ ] Use the `$gt` operator to do comparison-based queries
- [ ] Use `$regex` with `^` to find documents where a field starts with a specific letter
- [ ] Sort results ascending (A–Z) using `.sort("field")`
- [ ] Sort results descending (Z–A) using `.sort("field", -1)`
- [ ] Limit results to a specific number using `.limit(n)`
- [ ] Chain `.sort()` and `.limit()` together
- [ ] Update a single document using `update_one()` with `$set`
- [ ] Update multiple documents using `update_many()` with `$set`
- [ ] Check how many documents were modified using `.modified_count`
- [ ] Delete one document using `delete_one()`
- [ ] Delete multiple documents using `delete_many()` with a query
- [ ] Delete all documents using `delete_many({})` with an empty query
- [ ] Check how many documents were deleted using `.deleted_count`
- [ ] Explain why `$set` is important when updating

---

## Lesson Summary

In this lesson, you mastered five core MongoDB operations using Python and the pymongo library:

**1. Querying** — You learned how to filter documents using a query dictionary. Exact matches use simple key-value pairs. Advanced filtering uses operators like `$gt` (greater than), `$lt` (less than), and `$regex` (pattern matching with `^` meaning "starts with").

**2. Sorting** — You learned to use `.sort("field_name")` for ascending order (A→Z) and `.sort("field_name", -1)` for descending order (Z→A). Sorting can be chained with `.find()` and `.limit()`.

**3. Limiting** — You learned that `.limit(n)` restricts results to the first n documents. This is essential for building paginated results in real applications.

**4. Updating** — You learned `update_one()` (changes the first match only) and `update_many()` (changes all matches). You must always use the `$set` operator to safely change only specific fields without destroying the rest of the document.

**5. Deleting** — You learned `delete_one()` (removes first match), `delete_many(query)` (removes all matches), and `delete_many({})` (removes everything — use with extreme caution). The `.deleted_count` property tells you how many documents were removed.

Together, these operations — combined with the insertion and retrieval skills from earlier lessons — give you complete CRUD (Create, Read, Update, Delete) power over a MongoDB database. This is the foundation of virtually every modern web application and data system.

---

*Sources: W3Schools Python MongoDB Tutorial — Query, Sort, Limit, Update, Delete*
