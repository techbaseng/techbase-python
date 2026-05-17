---
render_with_liquid: false
title: "Lesson 29: Introduction to Pandas — Data Analysis with Python"
nav_order: 29
---

# Lesson 29: Introduction to Pandas — Data Analysis with Python

---

## Lesson Introduction

Welcome to one of the most powerful lessons in this series! In this lesson, you will learn **Pandas** — a Python library that lets you work with data the way a scientist, analyst, or engineer does every day.

Imagine you have a huge spreadsheet of student grades, weather readings, sales figures, or health records. Instead of clicking through menus in Excel, Pandas lets you write a few lines of Python code to load, explore, clean, filter, and summarise that data instantly.

By the end of this lesson, you will be able to:

- Understand what Pandas is and why it exists
- Install and import Pandas into your Python programs
- Create and work with **Series** (a single column of data)
- Create and work with **DataFrames** (a full table of data)
- Load real data from **CSV files** and **JSON files**
- Access specific rows and columns using labels and index numbers
- Build a simple real-world data mini-project from scratch

No prior data analysis experience is required. We will start from zero and build up together, step by step.

---

## Prerequisite Concepts

Before diving in, let's quickly review two Python concepts this lesson depends on. If you already know these, feel free to skim.

### Python Lists

A list is a collection of values stored in order. Think of it like a numbered shopping list.

```python
fruits = ["apple", "banana", "cherry"]
print(fruits[0])   # Access first item by its index number
```

**Expected Output:**
```
apple
```

Each item has an **index** — a number starting from `0` that tells Python where in the list that item lives.

### Python Dictionaries

A dictionary stores data as **key-value pairs** — like a word and its definition in a real dictionary.

```python
person = {"name": "Amara", "age": 22, "city": "Lagos"}
print(person["name"])
```

**Expected Output:**
```
Amara
```

You use the **key** (the word on the left) to look up its **value** (the data on the right). Pandas uses dictionaries heavily when creating tables of data.

### Python `import` Statement

When you want to use an external tool or library in Python, you bring it in with `import`.

```python
import math
print(math.sqrt(25))
```

**Expected Output:**
```
5.0
```

You will use `import` to bring Pandas into every program you write in this lesson.

---

## Section 1: What Is Pandas?

### The Big Picture — Why Does Pandas Exist?

Imagine you work for a hospital, a bank, or a university. Every day, thousands of records are collected: patient readings, transactions, exam scores. You need to answer questions like:

- What is the average score across all students?
- Which patient has the highest blood pressure?
- On which day did the store earn the most money?

Before Pandas, answering these questions required writing long, complex Python code just to organise the data, let alone analyse it.

**Pandas was created in 2008 by Wes McKinney** to solve exactly this problem. The name stands for **"Panel Data"** and **"Python Data Analysis"** — two hints at what it does.

### What Pandas Actually Does

Pandas is a Python library. A library is simply a collection of pre-written code that someone else (or a team) built and packaged for you to use freely. When you use Pandas, you are borrowing thousands of hours of work to do powerful things in just a few lines.

With Pandas you can:

- **Analyse** big datasets — find averages, maximums, minimums
- **Clean** messy data — fix errors, remove blanks, correct wrong values
- **Explore** data — look at its shape, types, and patterns
- **Manipulate** data — sort, filter, combine, and reshape tables
- **Load data** from external files — CSV, JSON, Excel, and more

> 💡 **Real-world analogy:** Think of Pandas as a supercharged spreadsheet that you control with Python code. Excel can handle perhaps a few hundred thousand rows before slowing down. Pandas can handle **millions** of rows efficiently.

### Where Is Pandas Stored?

Pandas is an open-source project. Its code lives at [https://github.com/pandas-dev/pandas](https://github.com/pandas-dev/pandas) where developers from all over the world contribute improvements. **GitHub** is a platform where many people can work on the same codebase at once — think of it as Google Docs for code.

### What Fields Use Pandas?

Pandas is used in virtually every field that works with data:

- **Data Science and Machine Learning** — preparing datasets for AI models
- **Finance and Banking** — analysing stock prices, transactions, risk
- **Healthcare** — processing patient records and clinical trial data
- **Engineering** — analysing sensor readings and measurements
- **Education** — processing exam results and student performance
- **Business** — sales analysis, customer behaviour, inventory tracking

---

## Section 2: Getting Started — Installing and Importing Pandas

### Step 1: Install Pandas

Before you can use Pandas, you must install it. Pandas is not built into Python by default, so you need to add it using **PIP** — Python's package manager.

Open your terminal (also called the command prompt or shell) and type:

```bash
pip install pandas
```

**What this command does:**
- `pip` — this is Python's install helper tool
- `install` — tells pip to download and install a package
- `pandas` — the name of the package to install

If the installation is successful, you will see output ending with something like:

```
Successfully installed pandas-2.x.x
```

> 💡 **Tip:** If you are using an environment like Anaconda, Spyder, or Google Colab, Pandas is usually already pre-installed. You can skip the installation step and go straight to importing.

### Step 2: Import Pandas

Once Pandas is installed, you bring it into your Python script using the `import` keyword. You do this at the very top of every file where you want to use Pandas.

**The full import (less common):**

```python
import pandas

print(pandas.__version__)
```

**Expected Output:**
```
2.x.x
```

**The standard import with an alias (used everywhere):**

```python
import pandas as pd

print(pd.__version__)
```

**Expected Output:**
```
2.x.x
```

### Understanding the `as pd` Alias

An **alias** is a shorter nickname for something. Instead of typing `pandas` every time you want to use the library, you give it the short name `pd`. This is a universal convention — every Pandas programmer in the world uses `import pandas as pd`. You will see `pd` used in all examples from this point forward.

Think of it like this: instead of saying "please pass me the television remote control", you just say "remote". Same object, shorter name.

**Verifying the version:**

```python
import pandas as pd

print(pd.__version__)
```

The `__version__` attribute (the double underscores mean it is a special built-in attribute) stores the version string of the installed library. Checking this is a simple way to confirm Pandas loaded correctly.

---

## Section 3: Pandas Series — A Single Column of Data

### What Is a Series?

A **Pandas Series** is a one-dimensional array — meaning it is a **single column** of data. You can think of it as a list, but smarter.

> 💡 **Analogy:** If a DataFrame is a full spreadsheet, a Series is one single column of that spreadsheet. For example, the "Temperature" column in a weather table, or the "Score" column in a student grade table.

A Series can hold any type of data: numbers, text, dates, True/False values.

### Creating a Simple Series from a List

```python
import pandas as pd

a = [1, 7, 2]

myvar = pd.Series(a)

print(myvar)
```

**Expected Output:**
```
0    1
1    7
2    2
dtype: int64
```

**Breaking down this output line by line:**

- The left column (`0`, `1`, `2`) shows the **index** — the label for each position, automatically assigned starting from `0`
- The right column (`1`, `7`, `2`) shows the **values** — the actual data you provided
- `dtype: int64` — this tells you the data type. `int64` means 64-bit integer (whole numbers). Pandas automatically detects what type your data is.

> 🤔 **Thinking prompt:** What happens if you change `a = [1, 7, 2]` to `a = [10, 20, 30]`? Try it — does the index change? Why or why not?

### Accessing Values by Index

Once a Series is created, you can retrieve any value using its index number inside square brackets `[]`.

```python
import pandas as pd

a = [1, 7, 2]
myvar = pd.Series(a)

print(myvar[0])   # First value (index 0)
print(myvar[1])   # Second value (index 1)
print(myvar[2])   # Third value (index 2)
```

**Expected Output:**
```
1
7
2
```

The index always starts at `0`, not `1`. This is called **zero-based indexing** and is standard in Python.

### Creating a Series with Custom Labels

By default, Pandas numbers the index 0, 1, 2, and so on. But you can give your own meaningful names to the index positions using the `index` argument.

```python
import pandas as pd

a = [1, 7, 2]

myvar = pd.Series(a, index = ["x", "y", "z"])

print(myvar)
```

**Expected Output:**
```
x    1
y    7
z    2
dtype: int64
```

Now the index labels are `"x"`, `"y"`, and `"z"` instead of numbers. This makes it easier to understand what each value represents.

**Accessing by custom label:**

```python
print(myvar["y"])
```

**Expected Output:**
```
7
```

You can use either the label (`"y"`) or the numeric position (`[1]`) to access the value — they both work!

### Creating a Series from a Dictionary

A very common way to create a Series is from a Python dictionary, because dictionaries already have the key-value structure that maps perfectly to index-value pairs.

```python
import pandas as pd

calories = {"day1": 420, "day2": 380, "day3": 390}

myvar = pd.Series(calories)

print(myvar)
```

**Expected Output:**
```
day1    420
day2    380
day3    390
dtype: int64
```

**What happened here?**
- The dictionary **keys** (`"day1"`, `"day2"`, `"day3"`) automatically became the **index labels**
- The dictionary **values** (`420`, `380`, `390`) became the **Series values**

This is extremely useful when you have labelled data — like calorie counts per day, or temperatures per city.

### Selecting Only Some Items from a Dictionary

Sometimes you have a dictionary with many entries but only want to include some of them in your Series. Use the `index` argument to specify which keys to include:

```python
import pandas as pd

calories = {"day1": 420, "day2": 380, "day3": 390}

myvar = pd.Series(calories, index = ["day1", "day2"])

print(myvar)
```

**Expected Output:**
```
day1    420
day2    380
dtype: int64
```

Only `day1` and `day2` were included. `day3` was ignored because it was not listed in the `index` argument.

> 🤔 **Thinking prompt:** What do you think would happen if you listed a key in `index` that does NOT exist in the dictionary? Try `index = ["day1", "day5"]`. What does Pandas return for `day5`?

---

## Section 4: Pandas DataFrames — The Full Data Table

### What Is a DataFrame?

If a Series is a single column, a **DataFrame** is the entire table — rows AND columns.

A **Pandas DataFrame** is a two-dimensional (2D) data structure, similar to a spreadsheet or a SQL table. It has:
- **Rows** — each row represents one record (e.g., one student, one day's workout, one product)
- **Columns** — each column represents one attribute or measurement (e.g., name, score, price)
- **Index** — labels for each row (automatically numbered 0, 1, 2... unless you name them)

> 💡 **Analogy:** Think of a DataFrame as an Excel sheet. Each column is a Series. Multiple Series stacked side by side form a DataFrame.

### Creating a Simple DataFrame

You create a DataFrame by passing a Python dictionary to `pd.DataFrame()`. Each key in the dictionary becomes a **column name**, and each list of values becomes that column's data.

```python
import pandas as pd

data = {
  "calories": [420, 380, 390],
  "duration": [50, 40, 45]
}

df = pd.DataFrame(data)

print(df)
```

**Expected Output:**
```
   calories  duration
0       420        50
1       380        40
2       390        45
```

**Explaining every part of this output:**
- The top row (`calories  duration`) shows the **column headers** — one for each key in the dictionary
- The leftmost column (`0`, `1`, `2`) shows the **row index** — automatically assigned, starting at `0`
- Each row of numbers represents one record. Row `0` says "this workout burned 420 calories and lasted 50 minutes"

By convention, the variable holding a DataFrame is often called `df`. This is just a short, recognisable name — like how we use `x` for unknowns in maths.

### Locating a Specific Row Using `.loc`

Once you have a DataFrame, you often need to look at one specific row. Pandas provides the `.loc` attribute (short for "locate") for this purpose.

**Access a single row by index number:**

```python
import pandas as pd

data = {
  "calories": [420, 380, 390],
  "duration": [50, 40, 45]
}

df = pd.DataFrame(data)

print(df.loc[0])
```

**Expected Output:**
```
calories    420
duration     50
Name: 0, dtype: int64
```

Notice: when you locate a single row, the result is displayed vertically and is actually a **Pandas Series**! The column names become the index labels, and the values in that row become the values.

**Access multiple rows by passing a list of indexes:**

```python
print(df.loc[[0, 1]])
```

**Expected Output:**
```
   calories  duration
0       420        50
1       380        40
```

When you pass a list `[0, 1]` to `.loc`, the result is a **DataFrame** (a table with multiple rows). Notice the double square brackets — `[[0, 1]]` not `[0, 1]`.

> 💡 **Key rule:** `.loc[0]` → returns a **Series** (one row). `.loc[[0, 1]]` → returns a **DataFrame** (multiple rows).

### Creating a DataFrame with Named Row Indexes

By default, row indexes are numbers (0, 1, 2...). You can give rows meaningful names using the `index` parameter:

```python
import pandas as pd

data = {
  "calories": [420, 380, 390],
  "duration": [50, 40, 45]
}

df = pd.DataFrame(data, index = ["day1", "day2", "day3"])

print(df)
```

**Expected Output:**
```
      calories  duration
day1       420        50
day2       380        40
day3       390        45
```

Now each row is labelled with a meaningful name. This is very useful for time-series data (data measured over days, months, years).

**Accessing a named row:**

```python
print(df.loc["day2"])
```

**Expected Output:**
```
calories    380
duration     40
Name: day2, dtype: int64
```

You used the string `"day2"` as the row label, and `.loc` found it instantly.

> 🤔 **Thinking prompt:** Can you add a third column called `"heartrate"` with values `[120, 110, 115]` to the dictionary and recreate the DataFrame? What does the output look like?

### Loading Data from Files into a DataFrame

In real work, you will rarely type all your data manually. You will load it from external files. The most common types are CSV and JSON.

```python
import pandas as pd

df = pd.read_csv('data.csv')

print(df)
```

This loads an entire file of data into a DataFrame with one line of code. You will learn the full details of this in the next sections.

---

## Section 5: Reading CSV Files

### What Is a CSV File?

A **CSV file** (Comma-Separated Values) is a plain text file that stores tabular data. Each row in the file is one record, and the values within each row are separated by commas.

Here is what a simple CSV file looks like when you open it in a text editor:

```
Duration,Pulse,Maxpulse,Calories
60,110,130,409
60,117,145,479
60,103,135,340
45,109,175,282
45,117,148,406
60,102,127,300
```

The first line is the **header row** — it contains the column names. Every line after that is one row of data. CSV files are extremely common because they are simple, human-readable, and supported by almost every tool including Excel, Python, and databases.

> 💡 **Real-world use:** CSV files are how many banks export transaction histories, how hospitals share patient records between systems, and how weather services distribute climate data.

### Reading a CSV File with Pandas

Pandas has a built-in function called `pd.read_csv()` that reads a CSV file and converts it into a DataFrame automatically.

```python
import pandas as pd

df = pd.read_csv('data.csv')

print(df.to_string())
```

**What each line does:**
- `import pandas as pd` — loads the Pandas library with the short name `pd`
- `pd.read_csv('data.csv')` — reads the file named `data.csv` and builds a DataFrame from it, stored in `df`
- `df.to_string()` — converts the entire DataFrame to a string for printing, so you see every row

**Expected Output (abbreviated):**
```
   Duration  Pulse  Maxpulse  Calories
0        60    110       130     409.1
1        60    117       145     479.0
2        60    103       135     340.0
3        45    109       175     282.4
4        45    117       148     406.0
...
```

> 💡 **Tip:** Without `.to_string()`, if the DataFrame has many rows, Pandas only prints the first 5 and the last 5 rows by default, with `...` in between. Using `to_string()` forces it to display everything.

### Printing Without `.to_string()`

If you just do `print(df)` on a large dataset:

```python
import pandas as pd

df = pd.read_csv('data.csv')

print(df)
```

**Expected Output (for a large file):**
```
     Duration  Pulse  Maxpulse  Calories
0          60    110       130     409.1
1          60    117       145     479.0
2          60    103       135     340.0
3          45    109       175     282.4
4          45    117       148     406.0
..        ...    ...       ...       ...
164        60    105       140     290.8
165        60    110       145     300.0
...
[169 rows x 5 columns]
```

Pandas truncates the output to be readable. It shows 5 rows from the top and 5 from the bottom, then shows you the total number of rows and columns at the bottom.

### Checking and Changing the Maximum Display Rows

Pandas has a setting that controls how many rows are shown when you print a DataFrame. You can check it like this:

```python
import pandas as pd

print(pd.options.display.max_rows)
```

**Expected Output:**
```
60
```

This means: if your DataFrame has more than 60 rows, Pandas will only show the first and last 5 when you `print(df)`.

**Changing the maximum rows:**

```python
import pandas as pd

pd.options.display.max_rows = 9999

df = pd.read_csv('data.csv')

print(df)
```

By setting `max_rows` to `9999`, you are telling Pandas to show up to 9,999 rows without truncating. This is useful when you want to inspect the full dataset.

**Why does this setting exist?** Because some real-world datasets have millions of rows. Printing all of them to the terminal would be both slow and useless. Pandas defaults to showing a manageable summary.

---

## Section 6: Reading JSON Files

### What Is JSON?

**JSON** stands for **JavaScript Object Notation**. Despite the name mentioning JavaScript, JSON is a universal data format used everywhere — web APIs, databases, configuration files, and data science pipelines.

JSON uses a structure that looks very similar to a Python dictionary:

```json
{
  "Duration": {"0": 60, "1": 60, "2": 60},
  "Pulse":    {"0": 110, "1": 117, "2": 103},
  "Calories": {"0": 409, "1": 479, "2": 340}
}
```

The outer keys (`"Duration"`, `"Pulse"`, `"Calories"`) are column names. The inner keys (`"0"`, `"1"`, `"2"`) are row indexes. The inner values are the data.

> 💡 **Key insight:** JSON = Python Dictionary (in terms of structure). This is why Pandas can load both with ease.

### Reading a JSON File

Just like CSV, Pandas has a dedicated function: `pd.read_json()`.

```python
import pandas as pd

df = pd.read_json('data.json')

print(df.to_string())
```

**Expected Output:**
```
   Duration  Pulse  Maxpulse  Calories
0        60    110       130     409.1
1        60    117       145     479.0
2        60    103       135     340.0
...
```

The result is identical to reading the CSV — a proper DataFrame with column headers and row indexes. Pandas handles the conversion for you.

### Loading a Python Dictionary Directly as JSON

Since JSON and Python dictionaries share the same structure, you can also pass a Python dictionary directly to `pd.DataFrame()` to simulate reading JSON data without needing a file:

```python
import pandas as pd

data = {
  "Duration": {
    "0": 60,
    "1": 60,
    "2": 60,
    "3": 45,
    "4": 45,
    "5": 60
  },
  "Pulse": {
    "0": 110,
    "1": 117,
    "2": 103,
    "3": 109,
    "4": 117,
    "5": 102
  },
  "Maxpulse": {
    "0": 130,
    "1": 145,
    "2": 135,
    "3": 175,
    "4": 148,
    "5": 127
  },
  "Calories": {
    "0": 409,
    "1": 479,
    "2": 340,
    "3": 282,
    "4": 406,
    "5": 300
  }
}

df = pd.DataFrame(data)

print(df)
```

**Expected Output:**
```
   Duration  Pulse  Maxpulse  Calories
0        60    110       130       409
1        60    117       145       479
2        60    103       135       340
3        45    109       175       282
4        45    117       148       406
5        60    102       127       300
```

**What happened here, step by step:**

1. We defined a nested dictionary where outer keys are column names and inner keys are row index labels
2. `pd.DataFrame(data)` read that dictionary and converted it into a DataFrame
3. Pandas automatically aligned all the values by their matching index keys

This approach is useful when your data comes from an API (a web service that returns JSON) and you want to quickly turn it into a DataFrame for analysis.

### CSV vs JSON — A Quick Comparison

| Feature | CSV | JSON |
|---|---|---|
| Format | Plain text, comma-separated | Structured key-value pairs |
| Readability | Very simple, human-readable | More structured, slightly more complex |
| Use case | Flat tables, spreadsheet exports | Web APIs, nested or hierarchical data |
| Pandas function | `pd.read_csv()` | `pd.read_json()` |

Both formats are extremely common. A data analyst needs to be comfortable with both.

---

## Section 7: Guided Practice Exercises

### Exercise 1: Creating Your First Series

**Objective:** Create and explore a Pandas Series using a list.

**Scenario:** You are tracking the daily temperatures (in °C) in Lagos for 5 days.

**Steps:**

1. Create a list: `[32, 34, 30, 35, 31]`
2. Create a Pandas Series from that list
3. Print the full Series
4. Print only the temperature for day 3 (index `2`)
5. Create the same Series again but with custom labels: `["Mon", "Tue", "Wed", "Thu", "Fri"]`
6. Access Wednesday's temperature using its label

**Solution:**

```python
import pandas as pd

# Step 1-3: Create and print
temperatures = [32, 34, 30, 35, 31]
temp_series = pd.Series(temperatures)
print(temp_series)
```

**Expected Output:**
```
0    32
1    34
2    30
3    35
4    31
dtype: int64
```

```python
# Step 4: Access by index
print(temp_series[2])
```

**Expected Output:**
```
30
```

```python
# Step 5-6: Custom labels
temp_series_labelled = pd.Series(temperatures, index=["Mon", "Tue", "Wed", "Thu", "Fri"])
print(temp_series_labelled)
print(temp_series_labelled["Wed"])
```

**Expected Output:**
```
Mon    32
Tue    34
Wed    30
Thu    35
Fri    31
dtype: int64
30
```

**Self-check questions:**
- What is the difference between `temp_series[2]` and `temp_series_labelled["Wed"]`?
- Why do both return `30`?
- What happens if you try `temp_series["Wed"]`?

---

### Exercise 2: Building a Student Grade DataFrame

**Objective:** Create a DataFrame from a dictionary and use `.loc` to access specific rows.

**Scenario:** You are an assistant at a university building a grade sheet for five students.

**Steps:**

1. Create a dictionary with keys `"student"`, `"maths"`, `"english"`, `"science"`
2. Fill each key with a list of five values
3. Create a DataFrame from the dictionary
4. Print the full DataFrame
5. Use `.loc` to print the data for student at index `0`
6. Use `.loc` to print data for students at indexes `1` and `3`

**Solution:**

```python
import pandas as pd

# Step 1-4
data = {
  "student": ["Amara", "Bola", "Chidi", "Dami", "Emeka"],
  "maths":   [85, 72, 90, 65, 78],
  "english": [88, 80, 76, 91, 70],
  "science": [79, 85, 92, 60, 83]
}

df = pd.DataFrame(data)
print(df)
```

**Expected Output:**
```
  student  maths  english  science
0   Amara     85       88       79
1    Bola     72       80       85
2   Chidi     90       76       92
3    Dami     65       91       60
4   Emeka     78       70       83
```

```python
# Step 5: Single row
print(df.loc[0])
```

**Expected Output:**
```
student    Amara
maths         85
english       88
science       79
Name: 0, dtype: object
```

```python
# Step 6: Multiple rows
print(df.loc[[1, 3]])
```

**Expected Output:**
```
  student  maths  english  science
1    Bola     72       80       85
3    Dami     65       91       60
```

**Optional What-If Challenge:** Add an `index` parameter to give each student their student ID as the row label (e.g., `"S001"`, `"S002"`, ...). Then use `.loc["S003"]` to access Chidi's grades.

---

### Exercise 3: Reading and Exploring CSV Data

**Objective:** Practice loading a CSV file and controlling how it displays.

**Scenario:** You download a dataset of workout sessions. Create a small sample CSV in your mind (or actually create the file) and load it.

**Steps:**

1. Create a file called `workouts.csv` with the following content (save it in the same folder as your Python file):

```
day,duration_minutes,calories_burned,heartrate
Monday,45,350,130
Tuesday,60,450,145
Wednesday,30,220,115
Thursday,50,400,138
Friday,40,310,125
Saturday,75,600,155
Sunday,20,160,105
```

2. Load it using `pd.read_csv()`
3. Print it using `to_string()` to see everything
4. Print it without `to_string()` to see the default behaviour
5. Check the current `max_rows` setting

**Solution:**

```python
import pandas as pd

# Step 2-3
df = pd.read_csv('workouts.csv')
print(df.to_string())
```

**Expected Output:**
```
        day  duration_minutes  calories_burned  heartrate
0    Monday                45              350        130
1   Tuesday                60              450        145
2 Wednesday                30              220        115
3  Thursday                50              400        138
4    Friday                40              310        125
5  Saturday                75              600        155
6    Sunday                20              160        105
```

```python
# Step 5
print(pd.options.display.max_rows)
```

**Expected Output:**
```
60
```

---

### Exercise 4: Loading JSON Data from a Dictionary

**Objective:** Create a DataFrame from a nested dictionary (simulating JSON data).

**Scenario:** You receive a JSON-style data payload from a weather API with temperature data for three cities over three days.

```python
import pandas as pd

weather_data = {
  "Lagos": {"Mon": 32, "Tue": 34, "Wed": 30},
  "Abuja": {"Mon": 28, "Tue": 29, "Wed": 27},
  "Kano":  {"Mon": 35, "Tue": 37, "Wed": 33}
}

df = pd.DataFrame(weather_data)
print(df)
```

**Expected Output:**
```
     Lagos  Abuja  Kano
Mon     32     28    35
Tue     34     29    37
Wed     30     27    33
```

Notice: here the **outer keys** became the **column names** (cities), and the **inner keys** became the **row index labels** (days). This is the natural structure when the dictionary is organised by column.

**Self-check questions:**
- How would you access the temperature in Abuja on Tuesday?
- What happens if you use `df.loc["Tue"]`?

---

## Section 8: Mini Project — Weekly Fitness Tracker

This mini-project pulls together everything you have learned: creating Series, building DataFrames, naming indexes, and loading data.

**Project Goal:** Build a weekly fitness tracker that stores, displays, and accesses a person's daily workout data using Pandas.

---

### Stage 1: Setup — Create the Data

**Scenario:** Adaeze is tracking her fitness for one week. She records: how many minutes she exercised, how many calories she burned, and her average heart rate.

```python
import pandas as pd

# Stage 1: Create the workout data as a dictionary
workout_data = {
  "duration_min": [45, 60, 30, 55, 40, 75, 20],
  "calories":     [350, 450, 220, 420, 310, 600, 160],
  "heartrate":    [130, 145, 115, 140, 125, 155, 105]
}

days = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"]

df = pd.DataFrame(workout_data, index=days)

print("=== Adaeze's Weekly Fitness Log ===")
print(df)
```

**Expected Output:**
```
=== Adaeze's Weekly Fitness Log ===
           duration_min  calories  heartrate
Monday               45       350        130
Tuesday              60       450        145
Wednesday            30       220        115
Thursday             55       420        140
Friday               40       310        125
Saturday             75       600        155
Sunday               20       160        105
```

**Milestone achieved:** A full, labelled DataFrame created from scratch.

---

### Stage 2: Access Specific Days

```python
# Stage 2: Access individual days using .loc

# Look at Saturday's full workout
print("\n=== Saturday's Workout ===")
print(df.loc["Saturday"])

# Compare Monday and Wednesday
print("\n=== Monday vs Wednesday ===")
print(df.loc[["Monday", "Wednesday"]])
```

**Expected Output:**
```
=== Saturday's Workout ===
duration_min     75
calories        600
heartrate       155
Name: Saturday, dtype: int64

=== Monday vs Wednesday ===
           duration_min  calories  heartrate
Monday               45       350        130
Wednesday            30       220        115
```

**Milestone achieved:** Targeted row access using named labels.

---

### Stage 3: Extract Individual Series (Columns)

Each column in a DataFrame is itself a Series. You can extract any column like this:

```python
# Stage 3: Extract columns as Series

# Get all daily calorie values
calories_series = df["calories"]
print("\n=== Daily Calories ===")
print(calories_series)
```

**Expected Output:**
```
=== Daily Calories ===
Monday       350
Tuesday      450
Wednesday    220
Thursday     420
Friday       310
Saturday     600
Sunday       160
Name: calories, dtype: int64
```

**Milestone achieved:** Extracting a single column as a Series.

---

### Stage 4: Simple Analysis

```python
# Stage 4: Basic statistics on the data

print("\n=== Fitness Summary ===")
print("Total calories burned this week:", df["calories"].sum())
print("Average workout duration:", df["duration_min"].mean(), "minutes")
print("Highest heart rate recorded:", df["heartrate"].max())
print("Lowest calorie day value:", df["calories"].min())
print("Best workout day (most calories):", df["calories"].idxmax())
```

**Expected Output:**
```
=== Fitness Summary ===
Total calories burned this week: 2510
Average workout duration: 46.43 minutes
Highest heart rate recorded: 155
Lowest calorie day value: 160
Best workout day (most calories): Saturday
```

**Milestone achieved:** Using built-in Pandas methods (`.sum()`, `.mean()`, `.max()`, `.min()`, `.idxmax()`) to extract useful insights.

---

### Stage 5: Save the Data as CSV (Optional Extension)

```python
# Stage 5: Export to CSV for future use
df.to_csv("adaeze_fitness_log.csv")
print("\nFitness log saved to adaeze_fitness_log.csv!")
```

You can then reload it with:

```python
df_loaded = pd.read_csv("adaeze_fitness_log.csv", index_col=0)
print(df_loaded)
```

**Reflection questions:**
1. What do you notice about the `index_col=0` argument in `read_csv()`?
2. What would happen if you left that argument out?
3. Can you add an 8th day ("Monday Week 2") to the DataFrame and recalculate the total calories?

**Optional advanced extension:** Add a column `"intensity"` where you classify each workout as `"Low"`, `"Medium"`, or `"High"` based on the calorie count, then display the updated DataFrame.

---

## Section 9: Common Beginner Mistakes

### Mistake 1: Forgetting `import pandas as pd`

```python
# WRONG — Pandas not imported
df = pd.DataFrame({"a": [1, 2, 3]})
```

**Error:**
```
NameError: name 'pd' is not defined
```

**Fix:** Always start your file with `import pandas as pd`.

```python
# CORRECT
import pandas as pd
df = pd.DataFrame({"a": [1, 2, 3]})
```

---

### Mistake 2: Single Brackets vs Double Brackets with `.loc`

```python
import pandas as pd
data = {"calories": [420, 380, 390], "duration": [50, 40, 45]}
df = pd.DataFrame(data)

# This returns a Series (one row)
print(df.loc[0])

# This returns a DataFrame (still one row but in table format)
print(df.loc[[0]])
```

**Output comparison:**

`df.loc[0]` → **Series** (vertical display)
`df.loc[[0]]` → **DataFrame** (horizontal table display)

Use double brackets when you want to keep the table structure intact.

---

### Mistake 3: Mixing Up List and Dictionary Formats

```python
# WRONG — passing a flat list to pd.DataFrame creates an error
import pandas as pd
df = pd.DataFrame([1, 2, 3])   # This actually works but creates something unexpected
print(df)
```

**Output:**
```
   0
0  1
1  2
2  3
```

This creates a DataFrame with one column (named `0`) and the numbers as rows. This is rarely what you intend. The proper way to create a meaningful DataFrame is using a **dictionary**:

```python
# CORRECT
import pandas as pd
df = pd.DataFrame({"values": [1, 2, 3]})
print(df)
```

**Output:**
```
   values
0       1
1       2
2       3
```

---

### Mistake 4: Wrong File Path for CSV/JSON

```python
import pandas as pd
df = pd.read_csv('myfile.csv')
```

**Error:**
```
FileNotFoundError: [Errno 2] No such file or directory: 'myfile.csv'
```

**Causes and fixes:**
- The file doesn't exist → create or download the file
- The file is in a different folder → provide the full path, e.g., `pd.read_csv('/home/user/data/myfile.csv')`
- Wrong file extension → check you're not accidentally trying to read a `.txt` file as `.csv`

---

### Mistake 5: Accessing an Index That Doesn't Exist

```python
import pandas as pd
a = [10, 20, 30]
s = pd.Series(a)
print(s[5])   # There is no index 5 — only 0, 1, 2 exist
```

**Error:**
```
KeyError: 5
```

**Fix:** Always check the length of your Series first with `len(s)` or print the Series to see its valid indexes before accessing.

---

### Mistake 6: Confusing `.loc` Label Access with `.iloc` Position Access

Pandas has two ways to access rows:
- `.loc["label"]` — access by **label** (the name you gave the index)
- `.iloc[2]` — access by **position** (the numeric position, always starting from 0)

If you have named indexes and you try to use a number with `.loc`, you might get unexpected results or errors.

```python
import pandas as pd
data = {"value": [100, 200, 300]}
df = pd.DataFrame(data, index=["a", "b", "c"])

# Using .loc with label
print(df.loc["b"])     # Correct — uses label "b"

# Using .iloc with position
print(df.iloc[1])      # Correct — uses position 1 (which is "b")
```

Both give the same result here, but always know which one you need.

---

## Section 10: Reflection Questions

Think carefully about each of these before moving on. These questions will test whether you truly understood the concepts — not just memorised the code.

1. You have a Python list `scores = [88, 72, 95, 60, 83]`. If you create `pd.Series(scores)`, what will be the index labels? How would you change the labels to `["Alice", "Bob", "Carol", "David", "Eve"]`?

2. A friend creates a DataFrame and complains: "I accessed row 1 with `.loc[1]` but I got a Series, not a table!" What would you tell them to do if they want a DataFrame back?

3. You are working at a company and a colleague shares a file called `sales_data.csv`. You have never seen the file. Write the two lines of Python code you would use to load it and print the full contents.

4. What is the difference between a **Series** and a **DataFrame**? Use a real-world example to explain.

5. You read a JSON file and get the following output:
```
   Duration  Pulse  Calories
0        60    110       409
1        60    117       479
```
How many rows does this DataFrame have? How many columns? What is the index of the last row?

6. You want to check Tuesday's workout data from a DataFrame with days as row labels. What code would you write?

7. Why do we write `import pandas as pd` instead of just `import pandas`? What benefit does the alias `pd` provide?

8. What happens to your CSV's header row when Pandas loads the file? Where does it go?

---

## Section 11: Completion Checklist

Before moving to the next lesson, confirm that you can do each of the following confidently. Tick each item mentally as you review it:

- [ ] I can explain what Pandas is and name at least three real-world fields where it is used
- [ ] I can install Pandas using `pip install pandas`
- [ ] I can write `import pandas as pd` and explain why we use the `as pd` alias
- [ ] I can check the version of Pandas with `pd.__version__`
- [ ] I can create a Pandas Series from a list, with and without custom index labels
- [ ] I can access a value in a Series by its index number AND by its label
- [ ] I can create a Pandas Series from a Python dictionary
- [ ] I can create a Pandas DataFrame from a dictionary
- [ ] I understand the difference between a Series (one column) and a DataFrame (full table)
- [ ] I can use `.loc[index]` to access a single row and return a Series
- [ ] I can use `.loc[[index1, index2]]` to access multiple rows and return a DataFrame
- [ ] I can create a DataFrame with custom row index labels using the `index` parameter
- [ ] I can load a CSV file into a DataFrame using `pd.read_csv('filename.csv')`
- [ ] I can print the full DataFrame using `df.to_string()`
- [ ] I understand why Pandas truncates large DataFrames and how to change this with `pd.options.display.max_rows`
- [ ] I can load a JSON file into a DataFrame using `pd.read_json('filename.json')`
- [ ] I can build a Python dictionary and convert it directly to a DataFrame (simulating JSON loading)
- [ ] I completed the weekly fitness tracker mini-project

---

## Lesson Summary

In this lesson, you took your first major steps into the world of **data analysis with Python using Pandas**.

Here is everything you covered:

**What is Pandas?** A Python library created in 2008 for analysing, cleaning, exploring, and manipulating data. It is used in data science, finance, healthcare, engineering, and beyond.

**Getting Started:** Install with `pip install pandas`. Always import with `import pandas as pd`. Check your version with `pd.__version__`.

**Pandas Series:** A one-dimensional array of data — like a single column in a spreadsheet. Created from lists or dictionaries. Supports numeric and custom index labels. Accessed by position or label using `series[index]`.

**Pandas DataFrame:** A two-dimensional table with rows and columns. Created from a Python dictionary where keys become column headers. Rows can have numbered or named index labels. Use `df.loc[label]` for a single row (returns Series) and `df.loc[[label1, label2]]` for multiple rows (returns DataFrame).

**Reading CSV Files:** Use `pd.read_csv('file.csv')` to load any CSV file into a DataFrame instantly. Use `.to_string()` to display the full table. Control display rows with `pd.options.display.max_rows`.

**Reading JSON Files:** Use `pd.read_json('file.json')` to load JSON data. Since JSON and Python dictionaries share the same structure, you can also pass a nested dictionary directly to `pd.DataFrame()`.

**Mini-Project:** You built a complete weekly fitness tracker that stores, accesses, and analyses real data using everything from this lesson.

You now have the foundation to work with real data in Python. In the next lesson, you will go deeper — learning how to analyse, clean, and draw conclusions from data using Pandas.

> 💡 **Final thought:** Every data scientist, machine learning engineer, and analyst uses Pandas daily. What you learned in this lesson is not just a beginner concept — it is production-level knowledge used by professionals worldwide. Well done!
