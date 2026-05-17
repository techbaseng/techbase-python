---
render_with_liquid: false
title: "Pandas — Analyzing DataFrames and Cleaning Data"
nav_order: 30
---

# Lesson 30 — Pandas: Analyzing DataFrames and Cleaning Data

---

## Lesson Introduction

Imagine you have a spreadsheet full of workout records. Some dates are missing. Some workout durations look like typos. Two rows are exact duplicates. The calorie column has blank entries. If you just calculated the average calories burned from that messy data, your result would be wrong — perhaps badly wrong.

This is the core problem that **data analysis** and **data cleaning** solve.

In this lesson you will learn two connected skills:

1. **Analyzing a DataFrame** — getting a fast overview of your data so you know what you're working with.
2. **Cleaning a DataFrame** — identifying and fixing problems so your data is reliable before you compute anything.

By the end of this lesson you will be able to load a real-world-style dataset, inspect it intelligently, and systematically remove or repair every category of data problem.

---

## Prerequisite Concepts

Before diving in, let's make sure these foundation ideas are clear.

### What is a DataFrame?

A **DataFrame** is like a table in a spreadsheet. It has rows (going across) and columns (going down). Each column has a name (called a **header**), and each cell holds one piece of data.

```
   Name    Age   Score
0  Alice    22    88.5
1  Bob      19    NaN
2  Carol    21    74.0
```

- The numbers on the left (0, 1, 2) are the **row index** — the row's address.
- `Name`, `Age`, `Score` are the **column names**.
- `NaN` means "Not a Number" — it represents a missing value.

### What is Pandas?

**Pandas** is a Python library (a collection of ready-made tools) that makes working with tables of data very easy. You import it at the start of every script:

```python
import pandas as pd
```

The `as pd` part means "give pandas the nickname `pd`" so you can type `pd.something` instead of `pandas.something`.

### What is a CSV file?

A **CSV** (Comma Separated Values) file is a plain text file that stores table data. Each row is a line of text, and the values are separated by commas:

```
Duration,Date,Pulse,Maxpulse,Calories
60,2020/12/01,110,130,409.1
45,2020/12/04,109,175,282.4
```

Pandas can read CSV files directly into a DataFrame with one line of code.

---

## Part 1 — Analyzing DataFrames

### Why analyze before you compute?

Before doing any calculations — averages, totals, comparisons — you must understand your data. Otherwise you might calculate an average that includes missing values, or work with a column that has the wrong data type.

Think of it like checking your ingredients before you start cooking. You want to know: what do I have, how much, and is anything missing?

---

### 1.1 Loading a DataFrame from a CSV

```python
import pandas as pd

df = pd.read_csv('data.csv')
```

- `pd.read_csv('data.csv')` — reads the file called `data.csv` from your current folder and turns it into a DataFrame.
- `df` — we store the DataFrame in a variable called `df` (short for "DataFrame").

> **Real-world use:** In data science jobs, you almost always start by loading data from a CSV, Excel file, or database. This single line is the foundation of every data project.

---

### 1.2 `head()` — See the First Rows

**What is it?** A method that shows the top rows of your DataFrame.

**Why use it?** When a dataset has 10,000 rows, you can't read the whole thing. `head()` gives you a quick preview of the structure and content.

```python
import pandas as pd

df = pd.read_csv('data.csv')

print(df.head(10))   # Show the first 10 rows
```

**Expected Output** (first 10 rows of the dataset):

```
   Duration          Date  Pulse  Maxpulse  Calories
0        60  '2020/12/01'    110       130     409.1
1        60  '2020/12/02'    117       145     479.0
2        60  '2020/12/03'    103       135     340.0
3        45  '2020/12/04'    109       175     282.4
4        45  '2020/12/05'    117       148     406.0
5        60  '2020/12/06'    102       127     300.0
6        60  '2020/12/07'    110       136     374.0
7       450  '2020/12/08'    104       134     253.3
8        30  '2020/12/09'    109       133     195.1
9        60  '2020/12/10'     98       124     269.0
```

**What to notice:** Already in row 7 you can see Duration is `450` — while every other value is between 30 and 60. That looks suspicious!

**Default behaviour (no number given):**

```python
print(df.head())  # Shows first 5 rows by default
```

> 💡 **Tip:** If you call `head()` without a number, it always shows exactly **5 rows**. This is a shortcut for a quick sanity check.

---

### 1.3 `tail()` — See the Last Rows

**What is it?** A method that shows the bottom rows of your DataFrame.

**Why use it?** The last rows of a dataset can reveal problems too — trailing blank rows, or data entered in a different format at the end.

```python
print(df.tail())  # Show the last 5 rows
```

**Expected Output:**

```
    Duration          Date  Pulse  Maxpulse  Calories
27        60  '2020/12/27'     92       118     241.0
28        60  '2020/12/28'    103       132       NaN
29        60  '2020/12/29'    100       132     280.0
30        60  '2020/12/30'    102       129     380.3
31        60  '2020/12/31'     92       115     243.0
```

**What to notice:** Row 28 has `NaN` in Calories — a missing value.

> 🤔 **Think about it:** What would happen if you calculated the average calories without removing the NaN values first? Try to reason through it before reading on.

---

### 1.4 `info()` — Get a Full Data Report

**What is it?** A method that prints a structured summary of your entire DataFrame — column names, data types, and how many values are non-null (non-missing).

**Why use it?** It's the fastest way to spot missing values and check whether your columns have the right data type.

```python
print(df.info())
```

**Expected Output:**

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 169 entries, 0 to 168
Data columns (total 4 columns):
 #   Column    Non-Null Count  Dtype  
---  ------    --------------  -----  
 0   Duration  169 non-null    int64  
 1   Pulse     169 non-null    int64  
 2   Maxpulse  169 non-null    int64  
 3   Calories  164 non-null    float64
dtypes: float64(1), int64(3)
memory usage: 5.4 KB
None
```

**Breaking down every part of this output:**

| Part | What it means |
|---|---|
| `RangeIndex: 169 entries, 0 to 168` | There are 169 rows, numbered from 0 to 168 |
| `Data columns (total 4 columns)` | There are 4 columns |
| `#` | The column's position number |
| `Column` | The column's name |
| `Non-Null Count` | How many rows have an actual value (not missing) |
| `Dtype` | The data type of that column |

**What does `164 non-null` mean for Calories?**

There are 169 rows total. Only 164 have a Calories value. So **5 rows are missing their Calories data**. This is a problem you will need to fix before computing statistics.

**What is `int64`?** A whole number (integer). 64 refers to how the computer stores it internally — you don't need to worry about this detail as a beginner.

**What is `float64`?** A decimal number (floating point). Calories uses decimals like `409.1`, so it's stored as float64.

> 💡 **Tip:** Always run `df.info()` immediately after loading a dataset. It tells you everything important at once.

---

### 1.5 What Are Null Values (NaN)?

**NaN** stands for "Not a Number." In data work, it means a cell is completely empty — no value was recorded for that row and column.

Think of it like a form where someone left a question blank. The field exists, but there's nothing in it.

**Why are they a problem?**

Most mathematical operations in Python cannot handle NaN gracefully. For example:

```python
# Simple demonstration of NaN behavior
import math
print(5 + float('nan'))   # Output: nan
print(float('nan') > 10) # Output: False — but this is misleading!
```

When NaN appears in a calculation, the result becomes NaN too — which is wrong. Before doing any analysis, you must either **remove** or **fill** those missing values.

---

## Part 2 — Introduction to Data Cleaning

### What is data cleaning?

**Data cleaning** (also called data wrangling or data munging) is the process of finding and fixing problems in a dataset before you analyze it.

Think of it like washing vegetables before cooking. You wouldn't skip that step — and you shouldn't skip data cleaning either.

### The four main types of data problems

In our workout dataset, we have all four types:

| Problem | Example in Our Data |
|---|---|
| **Empty cells** | Row 18 has no Calories; Row 22 has no Date |
| **Wrong format** | Row 26 has date `20201226` instead of `'2020/12/26'` |
| **Wrong data** | Row 7 has Duration = `450` (should probably be `45`) |
| **Duplicates** | Rows 11 and 12 are identical |

We will handle each type one by one.

---

### Our Dataset

Throughout the cleaning sections, we work with this dataset. Save it mentally — you'll see it again and again:

```
    Duration          Date  Pulse  Maxpulse  Calories
0         60  '2020/12/01'    110       130     409.1
1         60  '2020/12/02'    117       145     479.0
2         60  '2020/12/03'    103       135     340.0
3         45  '2020/12/04'    109       175     282.4
4         45  '2020/12/05'    117       148     406.0
5         60  '2020/12/06'    102       127     300.0
6         60  '2020/12/07'    110       136     374.0
7        450  '2020/12/08'    104       134     253.3   ← Wrong data
8         30  '2020/12/09'    109       133     195.1
9         60  '2020/12/10'     98       124     269.0
10        60  '2020/12/11'    103       147     329.3
11        60  '2020/12/12'    100       120     250.7   ← Duplicate
12        60  '2020/12/12'    100       120     250.7   ← Duplicate
13        60  '2020/12/13'    106       128     345.3
...
18        45  '2020/12/18'     90       112       NaN   ← Empty Calories
...
22        45           NaN    100       119     282.0   ← Empty Date
...
26        60      20201226    100       120     250.0   ← Wrong format
...
28        60  '2020/12/28'    103       132       NaN   ← Empty Calories
```

---

## Part 3 — Cleaning Empty Cells

### Why do empty cells matter?

Empty cells are like blank entries in a survey — they leave gaps in your data. If someone calculates the average calories burned per workout and 5 out of 32 entries are blank, the average will be computed on only 27 entries. This can skew your results or cause errors.

You have two strategies: **remove** the row, or **fill** the empty cell with a sensible value.

---

### 3.1 Strategy 1: Remove Rows with Empty Cells (`dropna()`)

**What is `dropna()`?** A method that drops (removes) any row that has at least one NaN value.

**Analogy:** Imagine a quality inspector on a factory line. Any product with a missing component gets tossed out entirely.

#### Simple Example First

```python
import pandas as pd

# Create a tiny DataFrame with a missing value
data = {'Name': ['Alice', 'Bob', 'Carol'],
        'Score': [88.5, None, 74.0]}

df = pd.DataFrame(data)
print("Before cleaning:")
print(df)

clean_df = df.dropna()
print("\nAfter dropna():")
print(clean_df)
```

**Expected Output:**

```
Before cleaning:
    Name  Score
0  Alice   88.5
1    Bob    NaN
2  Carol   74.0

After dropna():
    Name  Score
0  Alice   88.5
2  Carol   74.0
```

Bob's row was removed because his Score was missing.

#### Applying to the Workout Dataset

```python
import pandas as pd

df = pd.read_csv('data.csv')

new_df = df.dropna()  # Returns a NEW clean DataFrame

print(new_df.to_string())
```

> ⚠️ **Important:** By default, `dropna()` does **not** change your original DataFrame. It creates and returns a brand new one. The original `df` is unchanged.

#### Making the Change Permanent with `inplace=True`

```python
import pandas as pd

df = pd.read_csv('data.csv')

df.dropna(inplace=True)  # Modifies the ORIGINAL df directly

print(df.to_string())
```

**What does `inplace=True` mean?**

Think of it like editing a document:
- Without `inplace=True`: Pandas makes a photocopy and edits the copy. Your original is safe.
- With `inplace=True`: Pandas edits the original document directly.

> 🚫 **Common Beginner Mistake:** Writing `df.dropna()` and expecting `df` to change. It won't! You must either write `df = df.dropna()` or use `inplace=True`.

---

### 3.2 Strategy 2: Fill Empty Cells with a Value (`fillna()`)

**What is `fillna()`?** A method that replaces all NaN values with a value you specify.

**Why use this instead of dropping?** Sometimes losing entire rows wastes too much data. For example, if only the Calories column is missing but Duration, Pulse, and Date are all valid — it might be better to estimate Calories than to throw the whole row away.

#### Simple Example

```python
import pandas as pd

data = {'Name': ['Alice', 'Bob', 'Carol'],
        'Score': [88.5, None, 74.0]}

df = pd.DataFrame(data)

df.fillna(0, inplace=True)  # Fill ALL NaN values with 0

print(df)
```

**Expected Output:**

```
    Name  Score
0  Alice   88.5
1    Bob    0.0
2  Carol   74.0
```

Bob's missing Score is now 0.

> 🤔 **Think about it:** Is filling with 0 always a good idea? What if Score can never be 0 in real life? What would a better fill value be?

#### Fill a Specific Column Only

You almost never want to fill every column with the same value. More often, you target one specific column:

```python
import pandas as pd

df = pd.read_csv('data.csv')

df.fillna({"Calories": 130}, inplace=True)
# Only the Calories column's NaN values become 130
```

**Why 130?** In this example it's just a placeholder. In real analysis, you'd choose a more meaningful value — like the average.

---

### 3.3 Strategy 3: Fill Empty Cells with a Calculated Value (Mean, Median, Mode)

Instead of guessing a fill value, you can calculate the **average** (mean), **middle value** (median), or **most common value** (mode) from the rest of the column and use that.

**Analogy:** If a student missed one exam, the school might substitute their average score from other exams instead of recording a zero. That's fairer.

#### Understanding Mean, Median, and Mode

**Mean (Average):** Add all values together, divide by how many there are.

```
Values: 10, 20, 30, 40, 50
Mean = (10+20+30+40+50) / 5 = 150 / 5 = 30
```

**Median (Middle Value):** Sort the values, then pick the one in the middle.

```
Values sorted: 10, 20, 30, 40, 50
Middle value = 30  (3 values on each side)
```

**Mode (Most Common Value):** The value that appears most often.

```
Values: 10, 20, 20, 20, 50
Mode = 20  (appears 3 times)
```

> 💡 **When to use which:**
> - **Mean** works well when data is spread evenly without extreme outliers.
> - **Median** works better when there are outliers (extreme values). Our duration value of 450 would inflate the mean, making median a safer choice.
> - **Mode** works for categorical data or when one value is clearly the most typical.

#### Fill with Mean

```python
import pandas as pd

df = pd.read_csv('data.csv')

x = df["Calories"].mean()   # Calculate mean of the Calories column
print(f"Mean calories: {x:.2f}")

df.fillna({"Calories": x}, inplace=True)
print(df.to_string())
```

**What `.mean()` does:** Adds up all non-NaN Calories values and divides by how many there are.

**Expected intermediate output:**
```
Mean calories: 304.68
```

All 5 missing Calories cells would be filled with `304.68`.

#### Fill with Median

```python
import pandas as pd

df = pd.read_csv('data.csv')

x = df["Calories"].median()   # The middle value of Calories

df.fillna({"Calories": x}, inplace=True)
```

#### Fill with Mode

```python
import pandas as pd

df = pd.read_csv('data.csv')

x = df["Calories"].mode()[0]   # Most common Calories value
# Note the [0] — mode() returns a list, so we take the first item

df.fillna({"Calories": x}, inplace=True)
```

> ⚠️ **Why `[0]` after `mode()`?** The `mode()` method returns a Series (a list) because there can be more than one most-common value. Adding `[0]` picks the first one.

---

## Part 4 — Cleaning Wrong Format Data

### What is "wrong format"?

A column has wrong format when the same type of information is stored in different ways across different rows. For example, a "Date" column where some dates look like `'2020/12/01'` and one looks like `20201226` — a number instead of a formatted string.

**Why is this a problem?** Computers are very literal. If Python sees `'2020/12/01'` and `20201226` in the same column, it cannot sort them as dates, calculate the number of days between them, or group them by month — because one is a formatted date string and the other is just a plain number.

---

### 4.1 Converting to a Correct Date Format (`pd.to_datetime()`)

Look at row 26 in our dataset — the Date value is `20201226` (a plain number), while every other date looks like `'2020/12/26'`.

We want to convert the **entire Date column** into proper Python date objects.

```python
import pandas as pd

df = pd.read_csv('data.csv')

df['Date'] = pd.to_datetime(df['Date'], format='mixed')

print(df.to_string())
```

**Breaking down the code:**

- `df['Date']` — we are selecting the "Date" column
- `pd.to_datetime(...)` — this is a Pandas function that converts values into proper date objects
- `format='mixed'` — tells Pandas that the dates are in different formats, so it should be flexible and figure each one out

**Expected Result for key rows:**

```
    Duration       Date  Pulse  Maxpulse  Calories
...
22        45        NaT    100       119     282.0   ← Empty date becomes NaT
...
26        60 2020-12-26    100       120     250.0   ← Fixed!
...
```

**What is `NaT`?** It stands for "Not a Time." Just like NaN is the missing value for numbers, NaT is the missing value for dates. Row 22 had no date at all, so after conversion it shows NaT.

---

### 4.2 Removing Rows with Wrong/Missing Dates After Conversion

After converting, any rows that had empty or unreadable dates now have `NaT`. We can remove those rows using `dropna()` targeted at the Date column:

```python
import pandas as pd

df = pd.read_csv('data.csv')

df['Date'] = pd.to_datetime(df['Date'], format='mixed')

df.dropna(subset=['Date'], inplace=True)
# subset=['Date'] means: only drop rows where Date is NaN/NaT
# Rows with NaN in other columns are kept
```

**What `subset=['Date']` means:** Instead of dropping any row with any missing value (which is the default), we only drop rows where the **Date column specifically** is empty. All other missing values are left alone.

> 🤔 **Think about it:** Why might we use `subset` here instead of just `dropna()`? What would happen to row 18 (which has a valid Date but missing Calories) if we called `dropna()` without `subset`?

---

## Part 5 — Cleaning Wrong Data

### What is "wrong data"?

Wrong data is a value that is technically present and in the right format, but is clearly incorrect or impossible given the context.

**Example from our dataset:** Row 7 has `Duration = 450`. All other Duration values are between 30 and 60 minutes. A 450-minute workout session (7.5 hours!) is extremely unlikely. It's almost certainly a typo — someone probably meant `45`.

The tricky part: Pandas can't automatically detect this. The number `450` is perfectly valid as a number. You need domain knowledge (understanding what the data represents) to recognize it's wrong.

---

### 5.1 Replacing a Specific Wrong Value

**Method 1 — Fix one specific cell:**

```python
import pandas as pd

df = pd.read_csv('data.csv')

df.loc[7, 'Duration'] = 45
# loc[7, 'Duration'] = row 7, column 'Duration'
# We set it to 45 (the corrected value)

print(df.loc[7])
```

**Expected Output for row 7:**

```
Duration             45
Date       '2020/12/08'
Pulse               104
Maxpulse            134
Calories          253.3
Name: 7, dtype: object
```

**What is `df.loc[]`?** It's how you access a specific cell or group of cells in a DataFrame.
- `df.loc[7, 'Duration']` means: go to row 7, column 'Duration'.
- Assigning `= 45` changes the value there.

---

### 5.2 Replacing Wrong Values Automatically with a Loop

For a small dataset you can fix values one by one. But imagine you have 10,000 rows — you can't check each one manually. Instead, you write a rule: "any Duration over 120 minutes is unrealistic — change it to 120."

```python
import pandas as pd

df = pd.read_csv('data.csv')

for x in df.index:              # Loop through every row index
    if df.loc[x, "Duration"] > 120:   # Check if Duration is too large
        df.loc[x, "Duration"] = 120   # Cap it at 120

print(df.to_string())
```

**Walking through the code line by line:**

1. `for x in df.index:` — `df.index` is a list of all row numbers (0, 1, 2, ... 31). This loop visits each row one at a time, putting the row number in `x`.
2. `if df.loc[x, "Duration"] > 120:` — checks whether this row's Duration is greater than 120.
3. `df.loc[x, "Duration"] = 120` — if it is too large, set it to exactly 120.

**Expected change:** Only row 7 (Duration = 450) is affected. It becomes 120. All other rows stay the same.

> 💡 **Real-world use:** In financial data, you might cap or flag transactions over a certain amount. In medical data, you might flag heart rates below 30 or above 220 as likely recording errors. This pattern is used everywhere.

---

### 5.3 Removing Rows with Wrong Data

Instead of correcting wrong values, you can simply delete those rows. This is a valid choice when you don't know what the correct value should be.

```python
import pandas as pd

df = pd.read_csv('data.csv')

for x in df.index:
    if df.loc[x, "Duration"] > 120:
        df.drop(x, inplace=True)  # Delete the entire row

print(df.to_string())
```

**What `df.drop(x, inplace=True)` does:** Removes the row with index number `x` from the DataFrame permanently (because of `inplace=True`).

**After this code:** Row 7 is completely gone. The DataFrame goes from 32 rows to 31 rows.

> ⚠️ **Correction vs Deletion — which should you choose?**
> - **Correct** if you're confident what the right value should be (e.g., `450` is clearly a typo for `45`).
> - **Delete** if the error is too severe to fix, or if you don't know what the right value should be.

---

## Part 6 — Removing Duplicate Rows

### What are duplicate rows?

A **duplicate row** is a row that has been entered more than once — all values in that row are identical to another row.

**Analogy:** Imagine a school roll call system accidentally recorded the same student twice. Any report generated from that data would count that student twice — doubling their influence on every statistic.

In our workout dataset, look at rows 11 and 12:

```
    Duration          Date  Pulse  Maxpulse  Calories
11        60  '2020/12/12'    100       120     250.7
12        60  '2020/12/12'    100       120     250.7
```

Every single value is identical. This workout session was accidentally recorded twice.

---

### 6.1 Discovering Duplicates with `duplicated()`

Before removing duplicates, it's good practice to first find them and see which rows they are.

```python
import pandas as pd

df = pd.read_csv('data.csv')

print(df.duplicated())
```

**Expected Output (abbreviated):**

```
0     False
1     False
2     False
...
11    False
12     True   ← Row 12 is a duplicate of row 11
...
31    False
dtype: bool
```

**What `duplicated()` returns:** A Series (a column) of `True` or `False` values.

- `False` means "this row is unique — it hasn't appeared before."
- `True` means "this row is a duplicate — an identical row appeared earlier."

Notice that row 11 shows `False` (it's the first occurrence) and row 12 shows `True` (it's the repeat).

#### Second Simple Example

```python
import pandas as pd

data = {'Name': ['Alice', 'Bob', 'Alice'],
        'Score': [88, 72, 88]}

df = pd.DataFrame(data)

print(df.duplicated())
```

**Expected Output:**

```
0    False
1    False
2     True    ← Second "Alice" with Score 88 is a duplicate
dtype: bool
```

---

### 6.2 Removing Duplicates with `drop_duplicates()`

Once you've confirmed duplicates exist, remove them:

```python
import pandas as pd

df = pd.read_csv('data.csv')

df.drop_duplicates(inplace=True)

print(df.to_string())
```

**What happens:** Pandas scans all rows. When it finds two identical rows, it keeps the first one and removes the second. Our dataset drops from 32 rows to 31 rows (row 12 is removed, row 11 is kept).

**The `inplace=True` rule applies here too:** Without `inplace=True`, the result is returned as a new DataFrame. With `inplace=True`, the original DataFrame is modified.

> 💡 **Real-world use:** Duplicates are extremely common in datasets that come from form submissions, database merges, or automated logging systems. Always check for them!

---

## Part 7 — Guided Practice Exercises

### Exercise 1 — Warm-Up: Inspecting a Student Dataset

**Objective:** Practice using `head()`, `tail()`, and `info()` on a new dataset.

**Scenario:** You are a teaching assistant at a university. You receive student exam scores as a CSV file. Before calculating any grades, you must understand the data.

**Steps:**

1. Create the following DataFrame in Python (paste this code):

```python
import pandas as pd

data = {
    'StudentID': [101, 102, 103, 104, 105, 106, 107],
    'Name': ['Ada', 'Ben', 'Cara', 'Dan', 'Eva', 'Frank', 'Grace'],
    'Exam1': [85, 92, None, 78, 88, 95, 71],
    'Exam2': [90, 88, 76, None, 82, 91, 69],
    'Grade': ['B', 'A', 'C', 'B', 'B', 'A', 'C']
}

df = pd.DataFrame(data)
```

2. Print the first 3 rows using `head()`.
3. Print the last 2 rows using `tail()`.
4. Print the full info report using `info()`.

**Expected output from `info()`:**

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 7 entries, 0 to 6
Data columns (total 5 columns):
 #   Column     Non-Null Count  Dtype  
---  ---------  --------------  -----  
 0   StudentID  7 non-null      int64  
 1   Name       7 non-null      object 
 2   Exam1      6 non-null      float64
 3   Exam2      6 non-null      float64
 4   Grade      7 non-null      object 
dtypes: float64(2), int64(1), object(2)
memory usage: 412.0+ bytes
```

**Self-check Questions:**

- How many students are missing Exam1 scores?
- How many students are missing Exam2 scores?
- Which columns have no missing values?
- What data type is the Grade column? (Hint: `object` means string/text)

---

### Exercise 2 — Handling Missing Values in a Sales Dataset

**Objective:** Practice `dropna()` and `fillna()` with mean.

**Scenario:** You work at a retail company. You have monthly sales data, but some months are missing their revenue figures. You need to clean the data before reporting.

**Steps:**

1. Create this DataFrame:

```python
import pandas as pd

data = {
    'Month': ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun'],
    'Revenue': [15000, None, 18500, 14200, None, 21000],
    'Units': [120, 95, 145, 110, 98, 160]
}

df = pd.DataFrame(data)
print("Original data:")
print(df)
```

2. Find the mean revenue (only from the non-missing months).
3. Fill the missing Revenue values with that mean.
4. Print the cleaned DataFrame.

**Hint:**

```python
mean_rev = df['Revenue'].mean()
df.fillna({'Revenue': mean_rev}, inplace=True)
```

**Expected Output (cleaned):**

```
  Month     Revenue  Units
0   Jan  15000.000    120
1   Feb  17175.000    95    ← Was None, now filled with mean
2   Mar  18500.000    145
3   Apr  14200.000    110
4   May  17175.000    98    ← Was None, now filled with mean
5   Jun  21000.000    160
```

**What-if challenge:** What would the mean revenue be if you used median instead of mean? Try it and compare.

---

### Exercise 3 — Fixing Date Formats and Wrong Data

**Objective:** Practice `pd.to_datetime()` and conditional value correction.

**Scenario:** A fitness app exported workout records. Some dates are in the wrong format, and one duration looks like a data entry error.

**Steps:**

1. Create this DataFrame:

```python
import pandas as pd

data = {
    'Date': ['2024/01/15', '2024/01/16', '20240117', '2024/01/18'],
    'Duration_min': [45, 350, 60, 30],
    'Calories': [320, 280, 410, 190]
}

df = pd.DataFrame(data)
print("Original:")
print(df)
```

2. Convert the `Date` column to proper dates using `pd.to_datetime()` with `format='mixed'`.
3. Find the row where Duration is unrealistically high (over 180 minutes) and fix it to 45.
4. Print the corrected DataFrame.

**Expected output after cleaning:**

```
        Date  Duration_min  Calories
0 2024-01-15            45       320
1 2024-01-16            45       280   ← 350 corrected to 45
2 2024-01-17            60       410   ← Date format fixed
3 2024-01-18            30       190
```

---

### Exercise 4 — Detecting and Removing Duplicates

**Objective:** Practice `duplicated()` and `drop_duplicates()`.

**Scenario:** Your company's order management system accidentally recorded some orders twice. You need to remove the duplicate entries.

**Steps:**

1. Create this DataFrame:

```python
import pandas as pd

data = {
    'OrderID': [1001, 1002, 1003, 1002, 1004, 1003],
    'Product': ['Laptop', 'Mouse', 'Keyboard', 'Mouse', 'Monitor', 'Keyboard'],
    'Price': [999.99, 29.99, 79.99, 29.99, 349.99, 79.99]
}

df = pd.DataFrame(data)
```

2. Print `df.duplicated()` to see which rows are duplicates.
3. Remove the duplicates using `drop_duplicates()`.
4. Print the cleaned DataFrame and count how many rows remain.

**Expected output after cleaning:**

```
   OrderID   Product    Price
0     1001    Laptop   999.99
1     1002     Mouse    29.99
2     1003  Keyboard    79.99
4     1004   Monitor   349.99
```

**Self-check:** Which rows were removed? Why did the index go from 0,1,2,3,4,5 to 0,1,2,4?

---

## Part 8 — Mini Project: Clean a Full Workout Dataset

In this project, you will apply all five cleaning techniques to the complete workout dataset — in the correct order.

**Project Goal:** Start with a messy, uncleaned dataset and produce a fully clean, analysis-ready version.

---

### Stage 1 — Setup and Initial Inspection

```python
import pandas as pd

# We simulate the dataset described in the lesson
data = {
    'Duration': [60, 60, 60, 45, 45, 60, 60, 450, 30, 60,
                 60, 60, 60, 60, 60, 60, 60, 60, 45, 60,
                 45, 60, 45, 60, 45, 60, 60, 60, 60, 60, 60, 60],
    'Date': ['2020/12/01','2020/12/02','2020/12/03','2020/12/04',
             '2020/12/05','2020/12/06','2020/12/07','2020/12/08',
             '2020/12/09','2020/12/10','2020/12/11','2020/12/12',
             '2020/12/12','2020/12/13','2020/12/14','2020/12/15',
             '2020/12/16','2020/12/17','2020/12/18','2020/12/19',
             '2020/12/20','2020/12/21', None,       '2020/12/23',
             '2020/12/24','2020/12/25','20201226',  '2020/12/27',
             '2020/12/28','2020/12/29','2020/12/30','2020/12/31'],
    'Pulse': [110,117,103,109,117,102,110,104,109,98,
              103,100,100,106,104,98,98,100,90,103,
              97,108,100,130,105,102,100,92,103,100,102,92],
    'Maxpulse': [130,145,135,175,148,127,136,134,133,124,
                 147,120,120,128,132,123,120,120,112,123,
                 125,131,119,101,132,126,120,118,132,132,129,115],
    'Calories': [409.1,479.0,340.0,282.4,406.0,300.0,374.0,253.3,
                 195.1,269.0,329.3,250.7,250.7,345.3,379.3,275.0,
                 215.2,300.0, None, 323.0,243.0,364.2,282.0,300.0,
                 246.0,334.5,250.0,241.0, None, 280.0,380.3,243.0]
}

df = pd.DataFrame(data)

print("=== STAGE 1: Initial Inspection ===")
print(f"Shape: {df.shape}")   # (rows, columns)
print(df.info())
```

**Milestone Output:**

```
Shape: (32, 5)
...
Calories  30 non-null    float64   ← Only 30 out of 32!
```

---

### Stage 2 — Fix the Date Format

```python
print("\n=== STAGE 2: Fix Date Format ===")
df['Date'] = pd.to_datetime(df['Date'], format='mixed')
print("Date column converted successfully.")
print(df[['Date']].head(5))
```

**Milestone Output:**

```
        Date
0 2020-12-01
1 2020-12-02
2 2020-12-03
3 2020-12-04
4 2020-12-05
```

---

### Stage 3 — Fix Wrong Duration Data

```python
print("\n=== STAGE 3: Fix Wrong Duration Values ===")
for x in df.index:
    if df.loc[x, 'Duration'] > 120:
        df.loc[x, 'Duration'] = 120

print(f"Max Duration is now: {df['Duration'].max()}")   # Should be 120
```

**Milestone Output:**

```
Max Duration is now: 120
```

---

### Stage 4 — Remove Duplicates

```python
print("\n=== STAGE 4: Remove Duplicates ===")
print(f"Rows before: {len(df)}")
df.drop_duplicates(inplace=True)
print(f"Rows after: {len(df)}")
```

**Milestone Output:**

```
Rows before: 32
Rows after: 31
```

---

### Stage 5 — Handle Missing Values

```python
print("\n=== STAGE 5: Handle Missing Values ===")

# Drop rows where Date is missing (NaT)
df.dropna(subset=['Date'], inplace=True)
print(f"Rows after dropping missing dates: {len(df)}")

# Fill missing Calories with the median
median_cal = df['Calories'].median()
df.fillna({'Calories': median_cal}, inplace=True)
print(f"Missing Calories filled with median: {median_cal:.1f}")
```

**Milestone Output:**

```
Rows after dropping missing dates: 30
Missing Calories filled with median: 300.0
```

---

### Stage 6 — Final Verification

```python
print("\n=== STAGE 6: Final Dataset Check ===")
print(df.info())
print(f"\nTotal rows in clean dataset: {len(df)}")
print(f"\nFirst 5 rows of clean data:")
print(df.head())
```

**Final Milestone Output:**

```
<class 'pandas.core.frame.DataFrame'>
...
 0   Duration  30 non-null    int64  
 1   Date      30 non-null    datetime64[ns]
 2   Pulse     30 non-null    int64  
 3   Maxpulse  30 non-null    int64  
 4   Calories  30 non-null    float64
...

Total rows in clean dataset: 30
```

No more NaN values! No more wrong formats! No more duplicates! The data is ready for analysis.

**Reflection Questions:**

- We went from 32 rows to 30 rows. Which specific rows were removed and why?
- Why did we fix the date format BEFORE dropping missing dates?
- Would the result have been different if we removed duplicates before or after fixing Duration? Why?

**Optional Extension:** Calculate the average calories per workout on the cleaned data. How would this average differ from calculating it on the original uncleaned data?

---

## Part 9 — Common Beginner Mistakes

### Mistake 1: Forgetting `inplace=True` and wondering why nothing changed

**Wrong:**
```python
df.dropna()         # Does nothing to df!
df.fillna(0)        # Does nothing to df!
df.drop_duplicates() # Does nothing to df!
```

**Right (Option A — use inplace):**
```python
df.dropna(inplace=True)
df.fillna(0, inplace=True)
df.drop_duplicates(inplace=True)
```

**Right (Option B — reassign):**
```python
df = df.dropna()
df = df.fillna(0)
df = df.drop_duplicates()
```

---

### Mistake 2: Filling ALL columns with the same value

**Wrong:**
```python
df.fillna(0, inplace=True)
# This fills missing dates with 0, missing names with 0 — nonsense!
```

**Right:**
```python
df.fillna({'Calories': df['Calories'].mean()}, inplace=True)
# Only fill the specific column that makes sense
```

---

### Mistake 3: Using `dropna()` without `subset` and accidentally removing too many rows

**Wrong:**
```python
df.dropna(inplace=True)
# This removes a row if ANY column is missing
# A row with valid Date but missing Calories gets deleted too
```

**Right:**
```python
df.dropna(subset=['Date'], inplace=True)
# Only remove rows where the Date is missing
```

---

### Mistake 4: Not checking for wrong data — assuming numbers are always correct

Just because a cell has a number doesn't mean it's the right number. Always inspect your data domain and use `describe()` or `info()` to spot suspiciously large or small values:

```python
print(df['Duration'].describe())
# Shows min, max, mean, etc. — helps you spot outliers
```

---

### Mistake 5: Modifying a DataFrame inside a loop without resetting the index

After dropping rows, the index numbers may have gaps (e.g., 0, 1, 2, 4, 5 — missing 3). If you then loop using the old index, you might hit a `KeyError`. Reset after major operations if needed:

```python
df.reset_index(drop=True, inplace=True)
```

---

### Mistake 6: Forgetting `[0]` when using mode

**Wrong:**
```python
df.fillna({'Calories': df['Calories'].mode()}, inplace=True)
# Tries to fill with an entire Series — will raise an error!
```

**Right:**
```python
df.fillna({'Calories': df['Calories'].mode()[0]}, inplace=True)
# [0] selects the first (most common) value from the result
```

---

## Part 10 — Reflection Questions

Think carefully about each of these questions. Try to answer from memory before reviewing the lesson.

1. What is the difference between `df.head()` and `df.tail()`? When would you use each one?

2. If `df.info()` shows `Non-Null Count: 160` for a column in a DataFrame with 200 rows, how many values are missing?

3. What is the difference between dropping a row and filling a missing value? Give one situation where each approach is better.

4. Why is it important to check for wrong data even if all cells have values and none are blank?

5. You have a column called `Temperature` with values like `22.5, 23.1, 95.0, 21.8, 22.9`. The value `95.0` is likely in Fahrenheit while all others are in Celsius. What is the best strategy to handle this?

6. After calling `df.drop_duplicates()` (without `inplace=True`), you print `df` and the duplicates are still there. What went wrong and how do you fix it?

7. You have a dataset with 10,000 rows and 20 columns. 3 rows have a missing value in one column. Is it better to drop those 3 rows or fill the missing values? Explain your reasoning.

8. Why does `mode()` return a list instead of a single value? Give an example where there would be more than one mode.

---

## Completion Checklist

Go through each item. Once you can confidently check it off, you've mastered this lesson.

- [ ] I can load a CSV into a Pandas DataFrame using `pd.read_csv()`
- [ ] I can use `head()` to preview the first rows of a DataFrame
- [ ] I can use `tail()` to preview the last rows of a DataFrame
- [ ] I can use `info()` to get a structured report about a DataFrame's columns, types, and missing values
- [ ] I understand what `NaN` and `NaT` mean and why they cause problems
- [ ] I can identify the four types of data problems (empty cells, wrong format, wrong data, duplicates)
- [ ] I can remove rows with missing values using `dropna()`
- [ ] I understand the difference between using `inplace=True` and reassigning the result
- [ ] I can fill missing values with a constant using `fillna()`
- [ ] I can fill missing values with the mean, median, or mode of a column
- [ ] I know when to use mean vs median vs mode
- [ ] I can convert a date column to proper date format using `pd.to_datetime()`
- [ ] I can use `subset` with `dropna()` to target a specific column
- [ ] I can fix wrong data by assigning a new value with `df.loc[]`
- [ ] I can fix wrong data automatically using a for loop with a condition
- [ ] I can find duplicate rows using `duplicated()`
- [ ] I can remove duplicate rows using `drop_duplicates()`
- [ ] I can apply all cleaning steps in the correct logical order on a full dataset

---

## Lesson Summary

In this lesson, you learned how to work with Pandas DataFrames from inspection all the way through to full data cleaning.

**Analyzing DataFrames:**

| Method | Purpose |
|---|---|
| `df.head(n)` | Show first `n` rows (default 5) |
| `df.tail(n)` | Show last `n` rows (default 5) |
| `df.info()` | Print column types, counts, and missing value summary |

**Cleaning Empty Cells:**

| Approach | Code | When to use |
|---|---|---|
| Remove rows | `df.dropna(inplace=True)` | Dataset is large; missing rows don't significantly reduce your data |
| Remove targeted rows | `df.dropna(subset=['Col'], inplace=True)` | Only drop rows where one specific column is empty |
| Fill with constant | `df.fillna({'Col': 0}, inplace=True)` | You have a known default value |
| Fill with mean | `df.fillna({'Col': df['Col'].mean()}, inplace=True)` | Numeric column, data is fairly evenly distributed |
| Fill with median | `df.fillna({'Col': df['Col'].median()}, inplace=True)` | Numeric column with outliers |
| Fill with mode | `df.fillna({'Col': df['Col'].mode()[0]}, inplace=True)` | Most common value is the best estimate |

**Cleaning Wrong Format:**

| Approach | Code | When to use |
|---|---|---|
| Convert dates | `df['Col'] = pd.to_datetime(df['Col'], format='mixed')` | Date column has inconsistent formats |

**Cleaning Wrong Data:**

| Approach | Code | When to use |
|---|---|---|
| Fix one cell | `df.loc[row, 'Col'] = new_value` | Small dataset, single known error |
| Fix with loop | Loop + `if condition: df.loc[x, 'Col'] = cap_value` | Apply a rule across all rows |
| Delete wrong rows | Loop + `df.drop(x, inplace=True)` | Error is too severe to fix |

**Removing Duplicates:**

| Method | Purpose |
|---|---|
| `df.duplicated()` | Returns True/False for each row — identifies duplicates |
| `df.drop_duplicates(inplace=True)` | Removes all duplicate rows (keeps first occurrence) |

> 🎯 **Golden Rule of Data Cleaning:** Always inspect first (`info()`, `head()`, `tail()`), then clean step by step — format → wrong data → duplicates → missing values. Never compute statistics on uncleaned data.
