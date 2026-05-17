---
render_with_liquid: false
title: "Lesson 23: Python File Write, Create, and Delete"
nav_order: 23
---

# Lesson 23: Python File Write, Create, and Delete

---

## Lesson Introduction

Welcome to Lesson 23! In the previous lesson (Lesson 22), you learned how to **open and read** files in Python — you could open a file and look at what was already inside it.

Now you are going to learn the **other half** of file handling: how to **write to files**, how to **create brand new files**, and how to **delete files and folders** you no longer need.

This is one of the most important practical skills in Python programming. Almost every real-world application — from mobile apps to hospital systems to banking software — stores data in files at some point. By the end of this lesson, you will be able to write data into files, create new files from scratch, and clean up files you no longer need — all with just a few lines of Python code.

### What You Will Learn in This Lesson

By the end of this lesson, you will be able to:

1. Write new content into an existing file using the `"w"` mode (overwrite).
2. Add content to the end of an existing file using the `"a"` mode (append).
3. Create a brand new file using the `"x"`, `"a"`, or `"w"` modes.
4. Understand the difference between append and overwrite.
5. Delete a file using `os.remove()`.
6. Safely check if a file exists before deleting it using `os.path.exists()`.
7. Delete an empty folder using `os.rmdir()`.
8. Apply all these skills in a real-world mini project.

---

## Prerequisite Concepts (What You Should Already Know)

Before we begin, let us quickly recap a few ideas from earlier lessons that this lesson builds on.

### Quick Recap: What is a File?

A **file** is like a notebook stored on your computer. It has a name, a location (path), and content. Python can open these notebooks, read from them, write into them, and even throw them away.

### Quick Recap: The `open()` Function and `with` Statement

In Lesson 22, you learned that `open()` is Python's way of gaining access to a file:

```python
with open("myfile.txt", "r") as f:
    content = f.read()
    print(content)
```

- `"myfile.txt"` — the name (and path) of the file.
- `"r"` — the **mode**: `"r"` means open for *reading*.
- `with` — ensures the file is automatically closed when Python is done.
- `f` — the variable that represents the open file object.
- `f.read()` — reads all the content of the file as one string.

In this lesson, we will use **different mode letters** — `"a"`, `"w"`, and `"x"` — to write to and create files instead of just reading them.

### Quick Recap: The `os` Module

Python's `os` module is a built-in toolkit for working with your operating system — things like files, folders, and paths. You do not need to install it. You just import it at the top of your script:

```python
import os
```

We will use it later in this lesson to delete files and folders.

---

## Part 1: Writing to an Existing File

### 1.1 — What Does "Writing to a File" Mean?

**Writing to a file** means putting text (or data) into a file from your Python program.

Think of it like this: you have a notebook (the file). Writing to it means picking up a pen and actually putting words on the page. There are two very different ways you can do this:

- **Overwriting** — you flip to page 1, erase everything, and start writing fresh. Whatever was there before is gone.
- **Appending** — you flip to the last page and continue writing from where the content left off. The old content stays untouched.

Python gives you both options through different **mode letters** inside `open()`.

---

### 1.2 — File Opening Modes for Writing

When you call `open("filename.txt", mode)`, the second argument (the mode) tells Python **what you want to do** with the file:

| Mode | Full Name | What It Does |
|------|-----------|--------------|
| `"r"` | Read | Opens the file to read. This is the default. |
| `"a"` | Append | Opens the file to **add** content at the end. Creates the file if it doesn't exist. |
| `"w"` | Write | Opens the file to **overwrite** it completely. Creates the file if it doesn't exist. |
| `"x"` | Create | Creates a **new** file. Raises an error if the file already exists. |

> **Remember:** If you use `"r"` but the file doesn't exist, Python raises a `FileNotFoundError`. But `"a"`, `"w"`, and `"x"` can all create a file if needed.

---

### 1.3 — The `"a"` Mode: Appending Content to a File

#### What Is Appending?

**Appending** means adding new content at the **end** of a file. It does not touch or remove anything that was already there.

**Real-life analogy:** Imagine a school attendance register. Every day, the teacher adds a new day's record at the bottom of the page. They never erase the old records. That is exactly what `"a"` mode does.

#### How Does It Work?

```python
with open("demofile.txt", "a") as f:
    f.write("Now the file has more content!")
```

Line by line:
- `open("demofile.txt", "a")` — Open `demofile.txt` for appending. If the file doesn't exist yet, Python will create it.
- `as f` — Name the open file `f` so we can use it inside the `with` block.
- `f.write("Now the file has more content!")` — Write (add) this text to the end of the file.
- The `with` block closes the file automatically when done.

#### Full Example: Append, Then Read Back

```python
# Step 1: Append new text to the file
with open("demofile.txt", "a") as f:
    f.write("Now the file has more content!")

# Step 2: Open and read the file to confirm
with open("demofile.txt") as f:
    print(f.read())
```

**Expected output in the terminal (assuming the file already contained "Hello, Lagos!"):**

```
Hello, Lagos!Now the file has more content!
```

> **Notice:** The new text was added right after the last character of the old content, with no automatic space or new line. If you want the new text to appear on a new line, add `\n` (newline character) at the start of your text:
>
> ```python
> f.write("\nNow the file has more content!")
> ```
>
> This would produce:
> ```
> Hello, Lagos!
> Now the file has more content!
> ```

---

### 1.4 — The `"w"` Mode: Overwriting a File

#### What Is Overwriting?

**Overwriting** means erasing everything currently in the file and replacing it with entirely new content. Think of it like using correction fluid on a form — the old text is gone, and you write fresh content on top.

> ⚠️ **Warning:** The `"w"` mode is powerful and dangerous if misused. Everything in the file is permanently deleted the moment you open it in `"w"` mode — even before you call `f.write()`. Always double-check before using `"w"` on an important file.

#### Simple Overwrite Example

```python
# This will ERASE all existing content in demofile.txt
with open("demofile.txt", "w") as f:
    f.write("Woops! I have deleted the content!")

# Now read back to confirm
with open("demofile.txt") as f:
    print(f.read())
```

**Expected output:**

```
Woops! I have deleted the content!
```

Everything that was in the file before is gone. Only the new text remains.

---

### 1.5 — Append vs. Overwrite: Side-by-Side Comparison

This is an important distinction that confuses many beginners. Study this table carefully:

| Question | `"a"` (Append) | `"w"` (Write/Overwrite) |
|---|---|---|
| What happens to old content? | Preserved — new text is added after it | **Deleted permanently** |
| Where does new text go? | At the very end of the file | At the very beginning (and it's the only thing there) |
| Does it create the file if missing? | Yes | Yes |
| Best used for... | Log files, adding records, diaries | Replacing a report, resetting a config file |

**Quick mental test:**

Imagine `notes.txt` currently contains: `Chidi scored 80 in Maths.`

After running:
```python
with open("notes.txt", "a") as f:
    f.write(" Amaka scored 95 in English.")
```

The file now contains:
```
Chidi scored 80 in Maths. Amaka scored 95 in English.
```

But after running:
```python
with open("notes.txt", "w") as f:
    f.write("Tunde scored 70 in Science.")
```

The file now contains **only**:
```
Tunde scored 70 in Science.
```

The earlier content about Chidi and Amaka is gone forever.

> **Thinking prompt:** What would happen if you opened a file with `"w"` and then never called `f.write()` at all? The file would become completely empty. This is a common accidental mistake!

---

## Part 2: Creating a New File

### 2.1 — Why Would You Create a New File?

Sometimes you need to create a file that did not exist before — for example:
- Creating a new log file for a fresh day's records.
- Starting a new configuration file for your application.
- Saving a report generated by your program.

Python provides three modes that can all create a new file:

| Mode | Creates New File? | What Happens if File Already Exists? |
|---|---|---|
| `"x"` | Yes | Raises a `FileExistsError` — stops and alerts you |
| `"a"` | Yes, if missing | Opens the existing file and appends to it (no error) |
| `"w"` | Yes, if missing | Opens the existing file and **overwrites** it (no error) |

---

### 2.2 — The `"x"` Mode: Safe File Creation

The `"x"` mode is the **safest** way to create a brand new file. It is specifically designed for creation:

- If the file **does not exist** → Python creates it as an empty file.
- If the file **already exists** → Python raises a `FileExistsError` and stops. This protects you from accidentally overwriting an important existing file.

#### Example

```python
f = open("myfile.txt", "x")
```

**Expected result:** A new, empty file called `myfile.txt` is created in the current working directory.

If you run this exact same line again, Python will raise:

```
FileExistsError: [Errno 17] File exists: 'myfile.txt'
```

This is a safety net — it is telling you: "Hey! This file already exists. Are you sure you want to do this?"

---

### 2.3 — Creating a File Using `"a"` Mode

If you open a file with `"a"` and the file does not exist yet, Python quietly creates it for you without complaining:

```python
with open("newlogfile.txt", "a") as f:
    f.write("System started at 08:00.\n")
```

**Expected result:** A file called `newlogfile.txt` is created with this content:
```
System started at 08:00.
```

If the file already existed, this line would simply be added to the end.

---

### 2.4 — Creating a File Using `"w"` Mode

Similarly, `"w"` mode will create the file if it doesn't exist:

```python
with open("report.txt", "w") as f:
    f.write("Monthly Sales Report\n")
    f.write("Total: ₦4,500,000\n")
```

**Expected result:** A file called `report.txt` is created with this content:
```
Monthly Sales Report
Total: ₦4,500,000
```

> **Key reminder:** If `report.txt` already existed with important data inside it, **that data would be completely erased**.

---

### 2.5 — Writing Multiple Lines to a File

You can call `f.write()` multiple times, and each call adds text right after the previous one. Use `\n` (the newline character) to move to a new line:

```python
with open("students.txt", "w") as f:
    f.write("Adaeze - 92\n")
    f.write("Emeka - 87\n")
    f.write("Funmi - 95\n")
    f.write("Babatunde - 88\n")

# Verify by reading back
with open("students.txt") as f:
    print(f.read())
```

**Expected output:**

```
Adaeze - 92
Emeka - 87
Funmi - 95
Babatunde - 88
```

> **What is `\n`?** It is the **escape character** for a new line. When Python writes `\n` into a file, the next character appears on the line below. It's invisible in the file output but moves the cursor down one row. Think of it as pressing the Enter key on your keyboard.

---

## Part 3: Deleting Files and Folders

### 3.1 — Why Would You Delete a File?

Deleting files is just as important as creating them. In real-world software, you might need to:
- Remove a temporary file after it has been processed.
- Clean up log files that are old and no longer needed.
- Delete a user's data when they close their account.
- Remove test files after testing is complete.

Python handles deletion through the `os` module — a built-in module that lets Python interact with your computer's operating system.

---

### 3.2 — The `os` Module: A Quick Introduction

**What is a module?** A module is a file containing Python code that you can import and use in your own scripts. Python comes with many built-in modules. You do not install them — you just import them.

**What is the `os` module?** The `os` module gives Python the ability to interact with the operating system — things like creating folders, deleting files, checking if paths exist, and navigating the file system.

To use it, always write this at the very top of your script:

```python
import os
```

This one line loads the module into memory and makes all its functions available to you.

---

### 3.3 — Deleting a File with `os.remove()`

#### What Does `os.remove()` Do?

`os.remove()` permanently deletes a file from your computer.

> ⚠️ **Critical Warning:** This deletion is **permanent**. Unlike moving something to the Recycle Bin, `os.remove()` bypasses it completely. The file is gone immediately. There is no "undo." Always be 100% certain before using this.

#### Syntax

```python
os.remove("filename.txt")
```

- `os` — the module you imported.
- `.remove()` — the function inside the module that deletes a file.
- `"filename.txt"` — the name (and path if needed) of the file to delete.

#### Simple Example

```python
import os

os.remove("demofile.txt")
```

**Expected result:** The file `demofile.txt` is permanently deleted. There is no output printed — it just disappears from your file system.

---

### 3.4 — The Problem: What If the File Doesn't Exist?

If you try to delete a file that does not exist, Python raises a `FileNotFoundError`:

```python
import os

os.remove("ghost_file.txt")  # This file doesn't exist!
```

**Error output:**

```
FileNotFoundError: [Errno 2] No such file or directory: 'ghost_file.txt'
```

Your entire program would crash at that point. In a real application, this could be catastrophic.

---

### 3.5 — The Safe Approach: Check Before You Delete

Python gives you a way to check if a file exists before trying to delete it: `os.path.exists()`.

#### What Does `os.path.exists()` Return?

- `True` — if the file (or folder) at that path exists.
- `False` — if it does not exist.

#### Safe Delete Pattern

```python
import os

if os.path.exists("demofile.txt"):
    os.remove("demofile.txt")
else:
    print("The file does not exist")
```

Line by line:
- `import os` — loads the `os` module.
- `if os.path.exists("demofile.txt"):` — checks whether the file exists. Returns `True` or `False`.
- `os.remove("demofile.txt")` — only runs if the file actually exists (condition was `True`).
- `else:` — if the condition was `False` (file not found).
- `print("The file does not exist")` — gives a friendly message instead of crashing.

**Expected output (if the file exists):** No output. The file is silently deleted.

**Expected output (if the file does NOT exist):**

```
The file does not exist
```

> **This is the pattern you should always use in real projects.** Never call `os.remove()` without first checking that the file exists. It takes two extra lines and can save you from program-breaking crashes.

---

### 3.6 — Deleting a Folder with `os.rmdir()`

What if you want to delete an entire folder instead of just a file?

Use `os.rmdir()`:

```python
import os

os.rmdir("myfolder")
```

**Expected result:** The folder named `myfolder` is permanently deleted.

#### Very Important Rule: The Folder Must Be Empty

`os.rmdir()` only works on **empty** folders. If the folder contains any files or subfolders, Python will raise an `OSError`:

```
OSError: [Errno 39] Directory not empty: 'myfolder'
```

**Why this restriction?** It is a safety measure. Python does not want you to accidentally delete a folder that has important files inside it. If you want to delete a folder and everything in it, you would need to first delete all files inside it (covered in more advanced lessons using `shutil.rmtree()`).

#### Safe Folder Deletion Pattern

Just like with files, you should check before deleting a folder:

```python
import os

if os.path.exists("myfolder"):
    os.rmdir("myfolder")
else:
    print("The folder does not exist")
```

---

### 3.7 — Summary: `os.remove()` vs `os.rmdir()`

| Feature | `os.remove()` | `os.rmdir()` |
|---|---|---|
| What it deletes | A **file** | A **folder** |
| Works on non-empty? | N/A (files have no contents restriction) | No — folder must be empty |
| Raises error if target missing? | Yes — `FileNotFoundError` | Yes — `FileNotFoundError` |
| Best practice | Check with `os.path.exists()` first | Check with `os.path.exists()` first |

---

## Part 4: Guided Practice Exercises

### Exercise 1: Write a Student Report to a File

**Objective:** Use the `"w"` mode to create a new file and write a student results report into it.

**Scenario:** The end-of-term results for JSS 2A at Sunshine Academy, Lagos, are ready. Your task is to write the results to a file called `results_jss2a.txt`.

**Steps:**

1. Open a file called `results_jss2a.txt` in `"w"` mode.
2. Write a header line: `"JSS 2A End-of-Term Results\n"`.
3. Write results for 5 students, each on a new line.
4. Close the file (handled automatically by `with`).
5. Open the same file in `"r"` mode and print its contents to verify.

**Hint:** Each line should end with `\n` so the results appear on separate lines.

**Solution:**

```python
# Step 1-4: Write the results
with open("results_jss2a.txt", "w") as f:
    f.write("JSS 2A End-of-Term Results\n")
    f.write("===========================\n")
    f.write("Adaeze Okafor   - 91\n")
    f.write("Emeka Nwosu     - 85\n")
    f.write("Funmi Adeleke   - 78\n")
    f.write("Ibrahim Musa    - 88\n")
    f.write("Chioma Eze      - 94\n")

# Step 5: Verify by reading back
with open("results_jss2a.txt") as f:
    print(f.read())
```

**Expected output:**

```
JSS 2A End-of-Term Results
===========================
Adaeze Okafor   - 91
Emeka Nwosu     - 85
Funmi Adeleke   - 78
Ibrahim Musa    - 88
Chioma Eze      - 94
```

**Self-check questions:**
- What mode did we use to write? (`"w"`)
- What would happen if `results_jss2a.txt` already existed with different data inside? (It would be completely erased and replaced.)
- What does `\n` do in our written text? (Moves to a new line.)

---

### Exercise 2: Append a Daily Market Entry to a Log File

**Objective:** Use the `"a"` mode to add new entries to an existing file without disturbing its old content.

**Scenario:** Mama Ngozi runs a provisions store at Balogun Market, Lagos. Each day, she logs her total sales in a file called `sales_log.txt`. Today is a new day, and she wants to add today's entry to the log.

**Steps:**

1. First, create the initial log file with Monday's entry (use `"w"` mode for this one-time setup).
2. Then, append Tuesday's entry using `"a"` mode.
3. Then, append Wednesday's entry using `"a"` mode.
4. Read the full log file to see all three entries.

**Solution:**

```python
# One-time setup: Create the log with Monday's entry
with open("sales_log.txt", "w") as f:
    f.write("Monday: ₦38,500\n")

# Tuesday: Append a new entry
with open("sales_log.txt", "a") as f:
    f.write("Tuesday: ₦41,200\n")

# Wednesday: Append another entry
with open("sales_log.txt", "a") as f:
    f.write("Wednesday: ₦29,700\n")

# Read back the full log
with open("sales_log.txt") as f:
    print(f.read())
```

**Expected output:**

```
Monday: ₦38,500
Tuesday: ₦41,200
Wednesday: ₦29,700
```

**Self-check questions:**
- What would the log look like if we had used `"w"` for Tuesday's entry instead of `"a"`? (Only Tuesday's entry would remain — Monday's would be erased.)
- How does `"a"` mode know where to start adding text? (It goes to the end of the file automatically.)

---

### Exercise 3: Safe File Deletion with Existence Check

**Objective:** Use `os.path.exists()` and `os.remove()` together to safely handle file deletion.

**Scenario:** Kemi is cleaning up temporary files from a data processing script. She has a temp file called `temp_data.txt`. She wants to delete it safely, with a message printed in either case.

**Steps:**

1. Create the file `temp_data.txt` with some dummy content.
2. Use the safe delete pattern to delete it.
3. Try the safe delete pattern again — this time the file won't exist.
4. Observe the printed messages in both scenarios.

**Solution:**

```python
import os

# Step 1: Create the temp file
with open("temp_data.txt", "w") as f:
    f.write("Temporary processing data - do not keep.")

# Step 2: Safe delete (file exists)
if os.path.exists("temp_data.txt"):
    os.remove("temp_data.txt")
    print("temp_data.txt has been deleted.")
else:
    print("The file does not exist.")

# Step 3: Safe delete attempt (file already gone)
if os.path.exists("temp_data.txt"):
    os.remove("temp_data.txt")
    print("temp_data.txt has been deleted.")
else:
    print("The file does not exist.")
```

**Expected output:**

```
temp_data.txt has been deleted.
The file does not exist.
```

**Self-check question:**
- What would happen if we removed the `if os.path.exists()` check and just ran `os.remove("temp_data.txt")` the second time? (Python would raise a `FileNotFoundError` and the program would crash.)

---

## Part 5: Mini Project — Student Record Manager

In this mini project, you will build a simple student record manager for a fictional school in Abuja. The program will create a record file, add students to it, and clean up a temp file when done.

### Project Goal

Build a Python script that:
1. Creates a fresh student record file.
2. Writes the initial set of students into it.
3. Appends a late-registered student to the file.
4. Creates a temporary backup file.
5. Reads and displays the final record.
6. Safely deletes the temporary backup file.

---

### Stage 1 — Setup: Create the Student Record File

```python
# Stage 1: Create fresh student record
with open("student_records.txt", "w") as f:
    f.write("UNITY SECONDARY SCHOOL, ABUJA\n")
    f.write("SS1 Student Register\n")
    f.write("==============================\n")
    f.write("1. Aisha Bello       - F - Kano State\n")
    f.write("2. Danladi Yusuf     - M - Plateau State\n")
    f.write("3. Ngozi Okonkwo     - F - Anambra State\n")
    f.write("4. Seun Adeyemi      - M - Ogun State\n")

print("Stage 1 complete: student_records.txt created.")
```

**Milestone output:**

```
Stage 1 complete: student_records.txt created.
```

---

### Stage 2 — Enhancement: Append a Late-Registered Student

```python
# Stage 2: Late registration — append new student
with open("student_records.txt", "a") as f:
    f.write("5. Fatima Abdullahi  - F - Sokoto State\n")

print("Stage 2 complete: Late student added.")
```

**Milestone output:**

```
Stage 2 complete: Late student added.
```

---

### Stage 3 — Backup: Create a Temporary Backup File

```python
import os

# Stage 3: Create a temp backup
with open("temp_backup.txt", "x") as backup:
    backup.write("Backup created for this session only.\n")

print("Stage 3 complete: temp_backup.txt created.")
```

**Milestone output:**

```
Stage 3 complete: temp_backup.txt created.
```

---

### Stage 4 — Output: Display the Full Record

```python
# Stage 4: Read and display the final student record
print("\n--- FINAL STUDENT RECORD ---\n")
with open("student_records.txt") as f:
    print(f.read())
```

**Milestone output:**

```
--- FINAL STUDENT RECORD ---

UNITY SECONDARY SCHOOL, ABUJA
SS1 Student Register
==============================
1. Aisha Bello       - F - Kano State
2. Danladi Yusuf     - M - Plateau State
3. Ngozi Okonkwo     - F - Anambra State
4. Seun Adeyemi      - M - Ogun State
5. Fatima Abdullahi  - F - Sokoto State
```

---

### Stage 5 — Cleanup: Delete the Temporary Backup File

```python
# Stage 5: Safe cleanup of temp file
if os.path.exists("temp_backup.txt"):
    os.remove("temp_backup.txt")
    print("Stage 5 complete: temp_backup.txt deleted.")
else:
    print("Temp file not found — nothing to delete.")
```

**Milestone output:**

```
Stage 5 complete: temp_backup.txt deleted.
```

---

### Full Project Script (All Stages Combined)

```python
import os

# --- STAGE 1: Create student record ---
with open("student_records.txt", "w") as f:
    f.write("UNITY SECONDARY SCHOOL, ABUJA\n")
    f.write("SS1 Student Register\n")
    f.write("==============================\n")
    f.write("1. Aisha Bello       - F - Kano State\n")
    f.write("2. Danladi Yusuf     - M - Plateau State\n")
    f.write("3. Ngozi Okonkwo     - F - Anambra State\n")
    f.write("4. Seun Adeyemi      - M - Ogun State\n")

print("Stage 1 complete: student_records.txt created.")

# --- STAGE 2: Append late student ---
with open("student_records.txt", "a") as f:
    f.write("5. Fatima Abdullahi  - F - Sokoto State\n")

print("Stage 2 complete: Late student added.")

# --- STAGE 3: Create temp backup ---
with open("temp_backup.txt", "x") as backup:
    backup.write("Backup created for this session only.\n")

print("Stage 3 complete: temp_backup.txt created.")

# --- STAGE 4: Display the record ---
print("\n--- FINAL STUDENT RECORD ---\n")
with open("student_records.txt") as f:
    print(f.read())

# --- STAGE 5: Safe delete temp file ---
if os.path.exists("temp_backup.txt"):
    os.remove("temp_backup.txt")
    print("Stage 5 complete: temp_backup.txt deleted.")
else:
    print("Temp file not found — nothing to delete.")
```

**Full Expected Output:**

```
Stage 1 complete: student_records.txt created.
Stage 2 complete: Late student added.
Stage 3 complete: temp_backup.txt created.

--- FINAL STUDENT RECORD ---

UNITY SECONDARY SCHOOL, ABUJA
SS1 Student Register
==============================
1. Aisha Bello       - F - Kano State
2. Danladi Yusuf     - M - Plateau State
3. Ngozi Okonkwo     - F - Anambra State
4. Seun Adeyemi      - M - Ogun State
5. Fatima Abdullahi  - F - Sokoto State

Stage 5 complete: temp_backup.txt deleted.
```

**Mini Project Reflection Questions:**
- Why did we use `"w"` mode in Stage 1 instead of `"a"` mode?
- What would happen in Stage 3 if we ran the script a second time? (It would raise a `FileExistsError` because `"x"` fails if the file already exists.)
- How could you fix that Stage 3 issue for repeated runs? (Use `"w"` instead of `"x"`, or add an `if not os.path.exists()` check first.)
- What would go wrong in Stage 5 if we removed the `os.path.exists()` check?

**Optional Extension Challenges:**
- Modify Stage 2 to prompt the user to enter a student name and state using `input()` before appending.
- Add a line counter so each new student gets the correct number automatically.
- Change Stage 5 to also print how many lines the student record file contains before deleting the backup.

---

## Part 6: Common Beginner Mistakes

### Mistake 1: Using `"w"` When You Meant `"a"`

**The error:**
```python
# You want to ADD a new entry to your log
with open("daily_log.txt", "w") as f:   # WRONG mode!
    f.write("New entry for today.\n")
```

**What happens:** All previous log entries are erased forever. Only the new entry remains.

**The fix:**
```python
with open("daily_log.txt", "a") as f:   # Correct mode
    f.write("New entry for today.\n")
```

**Rule of thumb:** If you want to keep old content, always use `"a"`. Only use `"w"` when you intentionally want to start fresh.

---

### Mistake 2: Forgetting `\n` — All Text Runs Together

**The error:**
```python
with open("names.txt", "w") as f:
    f.write("Chidi")
    f.write("Amaka")
    f.write("Tobi")
```

**Resulting file content:**
```
ChidiAmakaTobi
```

All names are squashed together on one line with no separating spaces or line breaks.

**The fix:**
```python
with open("names.txt", "w") as f:
    f.write("Chidi\n")
    f.write("Amaka\n")
    f.write("Tobi\n")
```

**Resulting file content:**
```
Chidi
Amaka
Tobi
```

---

### Mistake 3: Calling `os.remove()` Without Checking if the File Exists

**The error:**
```python
import os
os.remove("report.txt")   # What if the file isn't there?
```

**What happens:** If `report.txt` doesn't exist, Python raises `FileNotFoundError` and your program crashes.

**The fix:**
```python
import os
if os.path.exists("report.txt"):
    os.remove("report.txt")
else:
    print("Nothing to delete.")
```

---

### Mistake 4: Forgetting to Import `os` Before Using It

**The error:**
```python
os.remove("myfile.txt")   # Forgot to import os!
```

**What happens:** Python raises `NameError: name 'os' is not defined`.

**The fix:**
```python
import os   # Always at the top of the script
os.remove("myfile.txt")
```

---

### Mistake 5: Trying to Delete a Non-Empty Folder with `os.rmdir()`

**The error:**
```python
import os
os.rmdir("myproject")   # The folder has files inside it!
```

**What happens:** Python raises `OSError: [Errno 39] Directory not empty`.

**The fix (delete files first, then the folder):**
```python
import os

# Delete files inside first
os.remove("myproject/notes.txt")
os.remove("myproject/data.csv")

# Now the folder is empty — safe to remove
os.rmdir("myproject")
```

---

### Mistake 6: Using `"x"` Mode on a File That Already Exists

**The error:**
```python
f = open("myfile.txt", "x")   # myfile.txt already exists!
```

**What happens:** Python raises `FileExistsError: [Errno 17] File exists: 'myfile.txt'`.

**The fix:** Check first, then create:
```python
import os

if not os.path.exists("myfile.txt"):
    f = open("myfile.txt", "x")
    f.close()
    print("File created.")
else:
    print("File already exists — skipping creation.")
```

---

## Reflection Questions

Pause and think through these questions. Writing your answers down will help cement your understanding:

1. What is the difference between `"a"` mode and `"w"` mode? When would you choose one over the other?
2. Why does `"x"` mode raise an error when the file already exists, and why is this actually a useful safety feature?
3. You have a program that runs every night and writes a daily sales summary. Should you use `"w"` or `"a"` mode? Why?
4. What does `os.path.exists()` return, and why is it important to use it before calling `os.remove()`?
5. Why can't `os.rmdir()` delete a folder that has files inside it? Can you think of why this restriction exists?
6. What is the `os` module and how do you load it into your script?
7. What happens to an open file when the `with` block finishes?
8. You accidentally used `"w"` mode and erased an important file. What can you learn from this for future projects?

---

## Completion Checklist

Before moving on to Lesson 24, make sure you can confidently tick every item:

- [ ] I understand the difference between `"a"` (append) and `"w"` (write/overwrite) modes.
- [ ] I know that `"x"` mode creates a new file and raises an error if it already exists.
- [ ] I know that `"a"` and `"w"` modes will also create a new file if one doesn't exist.
- [ ] I can write multiple lines to a file using `f.write()` and `\n`.
- [ ] I can import the `os` module and explain what it does.
- [ ] I can delete a file using `os.remove()`.
- [ ] I always check `os.path.exists()` before calling `os.remove()`.
- [ ] I know that `os.rmdir()` only removes **empty** folders.
- [ ] I completed all three guided exercises.
- [ ] I completed the student record mini project.
- [ ] I can explain all six common mistakes and how to avoid them.

---

## Lesson Summary

In this lesson, you moved from simply **reading** files to **controlling** them — writing, creating, and deleting with confidence.

**Writing to Existing Files:**
- `"a"` (Append) mode adds new content to the **end** of a file. Old content is preserved.
- `"w"` (Write) mode **erases everything** in the file and writes fresh content from scratch.

**Creating New Files:**
- `"x"` mode creates a new file and **fails** if the file already exists (safest for creation).
- `"a"` mode creates the file silently if it doesn't exist, then appends.
- `"w"` mode creates the file silently if it doesn't exist, then writes.

**Deleting Files and Folders:**
- `import os` loads Python's operating system module.
- `os.remove("file.txt")` permanently deletes a file.
- `os.path.exists("file.txt")` returns `True` or `False` — always use this before deleting.
- `os.rmdir("folder")` deletes an **empty** folder only.

**The Golden Rules:**
1. Always use `"a"` when you want to preserve existing content.
2. Only use `"w"` when you are certain you want to start fresh.
3. Always check `os.path.exists()` before calling `os.remove()` or `os.rmdir()`.
4. Remember that file deletion via `os.remove()` is **permanent** — there is no undo.

---

## Quick-Reference Card

```
FILE WRITING & CREATION
─────────────────────────────────────────────────────────
open("file.txt", "a")   → Append to end  (creates if missing)
open("file.txt", "w")   → Overwrite all  (creates if missing)
open("file.txt", "x")   → Create new     (error if exists)
f.write("text\n")       → Write a line (use \n for newlines)
─────────────────────────────────────────────────────────

FILE DELETION
─────────────────────────────────────────────────────────
import os                        → Load the os module
os.remove("file.txt")            → Delete a file (permanent!)
os.path.exists("file.txt")       → True/False — does it exist?
os.rmdir("folder")               → Delete an EMPTY folder
─────────────────────────────────────────────────────────

SAFE DELETE PATTERN
─────────────────────────────────────────────────────────
import os
if os.path.exists("file.txt"):
    os.remove("file.txt")
else:
    print("File does not exist")
─────────────────────────────────────────────────────────

MODE COMPARISON TABLE
─────────────────────────────────────────────────────────
Mode │ Preserves old content? │ Creates if missing? │ Error if exists?
"a"  │ YES                    │ YES                 │ NO
"w"  │ NO (overwrites)        │ YES                 │ NO
"x"  │ N/A                    │ YES                 │ YES
─────────────────────────────────────────────────────────
```
