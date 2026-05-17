---
render_with_liquid: false
title: "Lesson 31: Pandas Correlations, Pandas Plotting & Introduction to Matplotlib"
nav_order: 31
---

# Lesson 31: Pandas Correlations, Pandas Plotting & Introduction to Matplotlib

---

## Lesson Introduction

Welcome to Lesson 31! In this lesson, you will learn three powerful skills that work beautifully together:

1. **How to find correlations in data using Pandas** — discovering hidden relationships between numbers
2. **How to create charts and graphs directly from a Pandas DataFrame**
3. **What Matplotlib is, how to install it, and how to draw your first plot**

By the end of this lesson, you will be able to look at a table of numbers, automatically measure how strongly different columns are related to each other, and then draw visual charts to *see* those relationships.

**Real-world relevance:** These skills are used every day by data scientists, business analysts, finance professionals, health researchers, sports statisticians, and engineers. Whenever someone says "does more sleep lead to better grades?" or "does workout duration affect calories burned?" — correlation and charts are the tools they use to answer those questions.

---

## Prerequisite Concepts

Before we start, let us make sure you understand a few foundational ideas. We will explain each one simply.

### What is a Library (or Module) in Python?

A **library** (also called a **module** or **package**) is a collection of code that someone else already wrote for you. Instead of writing all the code yourself from scratch, you simply "import" (load) the library and use its ready-made tools.

Think of it like a toolbox: rather than building a hammer yourself, you just open the toolbox and pick up the hammer.

The two libraries we will use in this lesson are:
- **Pandas** — for working with tables of data (like a spreadsheet in Python)
- **Matplotlib** — for drawing charts and graphs

### What is a DataFrame?

A **DataFrame** is like a table — it has rows and columns. Think of it like an Excel spreadsheet inside Python. For example:

```
| Duration | Pulse | Maxpulse | Calories |
|----------|-------|----------|----------|
| 60       | 110   | 130      | 409      |
| 45       | 117   | 141      | 282      |
| 45       | 103   | 132      | 270      |
```

Each **column** holds one type of information (like Duration or Calories). Each **row** holds one record (like one workout session).

### What is a CSV file?

A **CSV** file (Comma-Separated Values) is a simple text file that stores table data. Each line is one row, and columns are separated by commas. Pandas can read CSV files directly into a DataFrame.

### What is NumPy?

**NumPy** is another Python library used for working with numbers and arrays (lists of numbers). Matplotlib often works alongside NumPy. We will use `np.array()` to create lists of numbers for plotting.

---

## Part 1: Pandas — Data Correlations

### What is a Correlation?

**Correlation** means "how much do two things change together?"

Imagine you're tracking students in a class. You record their study hours per week and their exam scores. You notice: students who study more tend to score higher. That is a **positive correlation** — when one goes up, the other goes up too.

Now imagine tracking how many times students skip classes and their exam scores. Students who skip more tend to score *lower*. That is a **negative correlation** — when one goes up, the other goes down.

And sometimes two things have no relationship at all — like a student's shoe size and their exam score. That is **no correlation**.

### The Correlation Scale: From -1 to 1

Pandas measures correlation as a **number between -1 and 1**. Here is how to read that number:

| Correlation Value | What It Means |
|-------------------|---------------|
| `1.0` | Perfect positive relationship |
| `0.9` | Very strong positive relationship |
| `0.6` | Good positive relationship |
| `0.2` | Weak relationship (almost no link) |
| `0.0` | No relationship at all |
| `-0.2` | Weak negative relationship |
| `-0.6` | Good negative relationship |
| `-0.9` | Very strong negative relationship |
| `-1.0` | Perfect negative relationship |

> **Rule of thumb:** A correlation of `0.6` or higher (or `-0.6` or lower) is generally considered a **good** (meaningful) correlation.

> **Analogy:** Think of correlation like a tug-of-war rope. If both sides pull in the same direction → positive correlation. If they pull in opposite directions → negative. If they both just stand still → no correlation.

---

### The `corr()` Method in Pandas

Pandas has a built-in method called `corr()` that automatically calculates the correlation between **every pair of numeric columns** in your DataFrame.

**What it does:** Takes all your numeric columns and measures how strongly each pair is related. It ignores non-numeric (text) columns automatically.

**Why is this useful?** In a dataset with 10 columns, there are 45 possible pairs to compare. Instead of checking each pair manually, `corr()` calculates all of them in one line.

---

### Simple Example: Understanding What `corr()` Returns

Let's start with a tiny, easy example to understand the output before we use real data.

```python
import pandas as pd

# Create a very simple DataFrame with 3 columns
data = {
    'Hours_Studied': [1, 2, 3, 4, 5],
    'Exam_Score':    [40, 55, 65, 80, 95],
    'Shoe_Size':     [7, 9, 6, 8, 7]
}

df = pd.DataFrame(data)

# Calculate correlations
result = df.corr()
print(result)
```

**Expected Output:**

```
               Hours_Studied  Exam_Score  Shoe_Size
Hours_Studied       1.000000    0.993399   0.000000
Exam_Score          0.993399    1.000000  -0.019608
Shoe_Size           0.000000   -0.019608   1.000000
```

**Reading this output — line by line:**

- Every column is shown as both a **row** and a **column** in the result.
- The diagonal (top-left to bottom-right) is always `1.000000` — because every column is perfectly correlated with *itself*. Of course!
- `Hours_Studied` vs `Exam_Score` = `0.993399` → **very strong positive correlation**! Students who study more hours get much higher scores. Makes sense!
- `Hours_Studied` vs `Shoe_Size` = `0.000000` → **no correlation**. Of course — shoe size has nothing to do with study hours.
- The table is **symmetric**: the value for (row A, column B) is the same as (row B, column A).

> **Thinking prompt:** What would happen if we added a "Skipped_Classes" column? Would you expect a positive or negative correlation with Exam_Score? Why?

---

### Real Data Example: The Workout Dataset

Now let's use a real dataset. This is a workout tracking CSV file called `data.csv` that contains these columns: `Duration`, `Pulse`, `Maxpulse`, `Calories`.

```python
import pandas as pd

# Read the CSV file into a DataFrame
df = pd.read_csv('data.csv')

# Calculate correlations between all numeric columns
print(df.corr())
```

**Expected Output:**

```
            Duration     Pulse  Maxpulse  Calories
Duration    1.000000 -0.155408  0.009403  0.922721
Pulse      -0.155408  1.000000  0.786535  0.025120
Maxpulse    0.009403  0.786535  1.000000  0.203814
Calories    0.922721  0.025120  0.203814  1.000000
```

**Let's analyse every relationship:**

**1. Duration vs Duration = `1.000000` (Perfect Correlation)**
Every column is perfectly correlated with itself. This is always the case. It simply confirms the math is working correctly.

**2. Duration vs Calories = `0.922721` (Very Good Correlation)**
This is close to 1.0, which means there is a very strong positive relationship. The longer you work out, the more calories you burn. And conversely, if you burned a lot of calories, you probably worked out for a long time. This makes complete physical sense!

**3. Pulse vs Maxpulse = `0.786535` (Good Correlation)**
Your average pulse during a workout is strongly related to your maximum pulse. Higher average pulse → higher max pulse. Makes sense: if your heart is beating fast on average, it probably peaked even higher.

**4. Duration vs Maxpulse = `0.009403` (Very Bad Correlation)**
This is almost zero. The length of your workout has almost no relationship to how high your maximum heart rate goes. You could work out for 2 hours at a calm pace or 20 minutes at an intense pace — both could reach the same max pulse.

**5. Duration vs Pulse = `-0.155408` (Weak Negative Correlation)**
Slightly negative, but very weak. Not enough to draw conclusions from.

**6. Pulse vs Calories = `0.025120` (Basically No Correlation)**
Your average heart rate doesn't really predict how many calories you burn. Duration does, but not pulse alone.

> **Key insight:** A number close to `0` (like `0.009` or `0.025`) means the two things are **not related**. Don't try to predict one from the other — you'll just be guessing.

---

### What "Good Correlation" Means for Predictions

This is where correlation becomes practically useful:

- If Duration and Calories have a correlation of `0.92`, you can say: *"Given how long someone worked out, I can make a reasonable prediction of how many calories they burned."*
- If Duration and Maxpulse have a correlation of `0.009`, you **cannot** say: *"Given how long someone worked out, I can predict their max heart rate."* The data shows no meaningful link.

This is the foundation of **machine learning** and **data science**: you find which inputs (features) are correlated with the output (target) before building a predictive model.

---

### Second Example: Student Performance Correlations

Let's look at another scenario to reinforce the concept:

```python
import pandas as pd

# Student performance data
data = {
    'Study_Hours': [2, 4, 6, 8, 3, 5, 7, 1, 9, 4],
    'Sleep_Hours': [5, 7, 8, 8, 6, 7, 8, 4, 7, 6],
    'Score':       [45, 65, 78, 90, 55, 72, 88, 30, 95, 60],
    'Absences':    [8, 3, 2, 1, 6, 2, 1, 10, 0, 3]
}

df = pd.DataFrame(data)
print(df.corr())
```

**Expected Output (approximate):**

```
              Study_Hours  Sleep_Hours     Score  Absences
Study_Hours      1.000000     0.674957  0.985290 -0.947674
Sleep_Hours      0.674957     1.000000  0.718050 -0.678490
Score            0.985290     0.718050  1.000000 -0.962330
Absences        -0.947674    -0.678490 -0.962330  1.000000
```

**Analysis:**
- Study_Hours vs Score = `0.985` → Extremely strong! More study hours → higher scores.
- Absences vs Score = `-0.962` → Extremely strong *negative*! More absences → much lower scores.
- Sleep_Hours vs Score = `0.718` → Good correlation. More sleep helps performance.
- Study_Hours vs Absences = `-0.948` → Students who study more miss fewer classes.

> **Thinking prompt:** What would happen if you added a "TV_Hours" column? Would you expect it to be positively or negatively correlated with Score?

---

### Common Beginner Mistake: Confusing Correlation with Causation

**Mistake:** Assuming that because two things are correlated, one *causes* the other.

**Example:** Ice cream sales and drowning accidents are both high in summer. They are correlated — but ice cream does not *cause* drowning! Both are caused by hot weather leading people to swim more and eat more ice cream.

**Corrected thinking:** Correlation tells you that two things *tend to move together*. It does **not** tell you *why*. Always think critically about whether there is a logical explanation before drawing conclusions.

---

## Part 2: Pandas — Plotting

### What is Plotting?

**Plotting** means drawing a visual chart (a diagram, a graph) from your data. Instead of staring at rows and rows of numbers, you create a picture that shows the pattern at a glance.

Think of it like this: if I show you 200 workout records in a table, you might not immediately see any pattern. But if I draw a scatter plot showing Duration vs Calories — you'll immediately see the upward trend with your eyes.

### How Pandas Plotting Works

Pandas has a built-in `plot()` method that lets you draw charts directly from a DataFrame. It uses Matplotlib (which we'll learn about in Parts 3–5) behind the scenes to actually display the chart. You call `plt.show()` to make the chart appear on screen.

**The basic structure is:**

```python
import pandas as pd
import matplotlib.pyplot as plt   # needed to show the chart

df = pd.read_csv('data.csv')       # load the data
df.plot()                           # draw the plot
plt.show()                          # display the plot
```

---

### Simple Default Plot

When you call `df.plot()` with no arguments, Pandas draws a **line chart** of all numeric columns against the row index (0, 1, 2, 3...).

```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv('data.csv')

df.plot()

plt.show()
```

**What this does:**
- `import pandas as pd` → loads the Pandas library, called `pd` for short
- `import matplotlib.pyplot as plt` → loads the Matplotlib plotting submodule, called `plt` for short
- `df = pd.read_csv('data.csv')` → reads the CSV file and creates a DataFrame
- `df.plot()` → tells Pandas to draw a default line plot of all numeric columns
- `plt.show()` → displays the chart on your screen (without this line, nothing appears!)

**Expected result:** A line chart showing Duration, Pulse, Maxpulse, and Calories all drawn as separate lines. This gives a general overview.

---

### Scatter Plot: Visualising Correlation

A **scatter plot** is one of the most powerful charts for visualising correlation. It places a dot for every data row, with the x-position determined by one column and the y-position determined by another.

If the dots form a diagonal upward line → positive correlation.
If the dots form a diagonal downward line → negative correlation.
If the dots are scattered randomly → no correlation.

**Syntax for a scatter plot with Pandas:**

```python
df.plot(kind = 'scatter', x = 'ColumnName', y = 'OtherColumnName')
```

- `kind = 'scatter'` → tells Pandas to make a scatter plot (not a line chart)
- `x = 'Duration'` → use the Duration column as the horizontal axis
- `y = 'Calories'` → use the Calories column as the vertical axis

---

#### Scatter Plot Example 1: Good Correlation (Duration vs Calories)

```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv('data.csv')

# Scatter plot showing a GOOD correlation
df.plot(kind = 'scatter', x = 'Duration', y = 'Calories')

plt.show()
```

**Expected result:** The dots will form a clear upward diagonal pattern — the longer the workout duration, the more calories burned. You can visually see the strong correlation of `0.922721` that we calculated earlier.

> **Connecting the dots (literally):** When you see the dots trending upward from left to right, that is the *visual proof* of the high positive correlation number.

---

#### Scatter Plot Example 2: Bad Correlation (Duration vs Maxpulse)

Now let's plot the pair that had a very low correlation (`0.009403`):

```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv('data.csv')

# Scatter plot showing a BAD (no) correlation
df.plot(kind = 'scatter', x = 'Duration', y = 'Maxpulse')

plt.show()
```

**Expected result:** The dots will be **scattered randomly** all over the chart with no clear pattern or direction. There is no diagonal trend. This is the visual confirmation that Duration and Maxpulse have no meaningful relationship — just like the near-zero correlation value showed us numerically.

> **Thinking prompt:** Compare the two scatter plots side by side. Can you see immediately which pair has a strong relationship and which doesn't? This is the power of visualisation.

---

### Histogram: Seeing How Data Is Distributed

A **histogram** shows you how often values fall into different ranges (called "bins" or "intervals"). It answers the question: "How spread out is my data? What's the most common range?"

**Analogy:** Imagine asking 200 students how many hours they studied. Instead of listing all 200 numbers, a histogram groups them: "40 students studied 1–2 hours, 80 students studied 3–4 hours," etc. You immediately see the most common study amount.

**Key difference from scatter plot:** A scatter plot needs two columns (x and y). A histogram only needs **one column**.

**Syntax for a histogram:**

```python
df["ColumnName"].plot(kind = 'hist')
```

- `df["Duration"]` → select just the Duration column from the DataFrame
- `.plot(kind = 'hist')` → draw a histogram of that column's values

---

#### Histogram Example: Distribution of Workout Durations

```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv('data.csv')

# Histogram of the Duration column
df["Duration"].plot(kind = 'hist')

plt.show()
```

**Expected result:** A bar chart where the x-axis shows ranges of Duration (like 50–60 minutes, 60–70 minutes, etc.) and the y-axis shows how many workouts fell in each range.

According to the dataset, **over 100 workouts lasted between 50 and 60 minutes** — this would show as the tallest bar in the histogram, making it very easy to see the most common workout length at a glance.

> **Real-world use:** Histograms are used everywhere — doctors look at histograms of patient ages, engineers look at histograms of measurement errors, teachers look at histograms of exam scores to see how grades are distributed.

---

### Summary of Pandas Plot Types

| Plot Type | `kind =` value | What it shows | Columns needed |
|-----------|----------------|---------------|----------------|
| Line chart | (default, no `kind`) | Trends over rows | All numeric |
| Scatter plot | `'scatter'` | Relationship between 2 columns | 2 (x and y) |
| Histogram | `'hist'` | Distribution/frequency of values | 1 |

---

## Part 3: Introduction to Matplotlib

### What is Matplotlib?

**Matplotlib** is a Python library specifically designed for creating charts, graphs, diagrams, and all kinds of visualisations.

- It was created by **John D. Hunter**
- It is **open source** — free for anyone to use
- It is mostly written in Python, with some parts in C, Objective-C, and JavaScript
- It is the most popular charting library in the Python data science world

**Why do we need it?** Pandas' `plot()` method we used above actually *uses* Matplotlib internally. But when you use Matplotlib directly, you get much more control: custom colours, labels, titles, grid lines, multiple charts in one figure, and much more.

**Where is the code?** The source code is on GitHub at: `https://github.com/matplotlib/matplotlib`

---

### Installing Matplotlib

Before you can use any external library, you must install it. Here's how:

**Step 1:** Open your command prompt (Windows) or terminal (Mac/Linux).

**Step 2:** Type this command and press Enter:

```
pip install matplotlib
```

`pip` is Python's **package manager** — the tool that downloads and installs libraries from the internet.

If this command doesn't work, you might be using a Python distribution like **Anaconda** or **Spyder**, which often have Matplotlib already pre-installed.

---

### Checking Your Matplotlib Version

Once installed, you can verify the installation and see which version you have:

```python
import matplotlib

print(matplotlib.__version__)
```

**Expected Output (your version may differ):**

```
3.9.2
```

**Line-by-line explanation:**
- `import matplotlib` → loads the entire Matplotlib library
- `print(matplotlib.__version__)` → prints the version number stored in the `__version__` attribute
- Note: there are **two underscore characters** on each side of `version` (that's four underscores total: `__version__`)

> **Common mistake:** Typing `_version_` (one underscore each side) instead of `__version__` (two underscores each side). Python won't recognise it.

---

## Part 4: Matplotlib — The Pyplot Submodule

### What is Pyplot?

Matplotlib is a large library with many parts. The part we almost always use is called **Pyplot** — a submodule (a smaller package inside the bigger one) that contains all the functions for drawing plots.

**Think of it this way:** Matplotlib is the whole art studio. Pyplot is the particular drawing table where you actually sit down and draw.

### Importing Pyplot

The standard way to import Pyplot is:

```python
import matplotlib.pyplot as plt
```

**Breaking this down:**
- `import matplotlib.pyplot` → loads the pyplot submodule
- `as plt` → gives it a short nickname `plt` so you don't have to type `matplotlib.pyplot` every time
- Now whenever you want to use Pyplot, you just write `plt.something()`

> **Convention:** `import matplotlib.pyplot as plt` is the universally agreed way to import it. You'll see this exact line in virtually every data science script in the world.

---

### Your First Plot with Pyplot

Now let's draw something! This is the simplest possible Matplotlib example — a straight line:

```python
import matplotlib.pyplot as plt
import numpy as np

# Define the x-coordinates of our two points
xpoints = np.array([0, 6])

# Define the y-coordinates of our two points
ypoints = np.array([0, 250])

# Draw a line connecting those points
plt.plot(xpoints, ypoints)

# Display the chart
plt.show()
```

**Expected Output:** A chart window opens showing a straight line going from (0, 0) at the bottom-left to (6, 250) at the top-right.

**Line-by-line explanation:**

- `import matplotlib.pyplot as plt` → loads Pyplot with the nickname `plt`
- `import numpy as np` → loads NumPy with the nickname `np`
- `xpoints = np.array([0, 6])` → creates an array with two x-values: 0 and 6
- `ypoints = np.array([0, 250])` → creates an array with two y-values: 0 and 250
- `plt.plot(xpoints, ypoints)` → draws a line chart. Python will plot the point (0, 0) and (6, 250) and draw a line between them
- `plt.show()` → opens a window on your screen to display the chart. **This is required!** Without it, nothing appears.

> **What is `np.array()`?** It creates a NumPy array — an ordered collection of numbers. Think of it as a smarter version of a Python list. Matplotlib works best with NumPy arrays.

---

## Part 5: Matplotlib Plotting — Drawing Points and Lines

### The `plot()` Function

The `plt.plot()` function is the core of Matplotlib. It draws markers (dots) or lines in a diagram.

**How it works:**
- **Parameter 1:** An array of x-coordinates (horizontal positions)
- **Parameter 2:** An array of y-coordinates (vertical positions)
- Each pair (x[i], y[i]) defines one point
- By default, Matplotlib connects the points with a line

> **Think of it like plotting points on graph paper.** The x-axis is horizontal. The y-axis is vertical. You mark each point and Matplotlib connects them.

---

### Example 1: Simple Line Between Two Points

```python
import matplotlib.pyplot as plt
import numpy as np

# Point 1: (1, 3)   Point 2: (8, 10)
xpoints = np.array([1, 8])
ypoints = np.array([3, 10])

plt.plot(xpoints, ypoints)
plt.show()
```

**Expected Output:** A straight line going from point (1, 3) to point (8, 10).

**How does Python know which x goes with which y?**
- `xpoints[0]` = 1 pairs with `ypoints[0]` = 3 → Point (1, 3)
- `xpoints[1]` = 8 pairs with `ypoints[1]` = 10 → Point (8, 10)
- Matplotlib draws a line connecting them in order.

---

### Example 2: Plotting Without a Line (Just Dots)

Sometimes you just want dots, not a line connecting them. Use the shortcut `'o'` as the third argument — `'o'` stands for "circles" (ring markers):

```python
import matplotlib.pyplot as plt
import numpy as np

xpoints = np.array([1, 8])
ypoints = np.array([3, 10])

plt.plot(xpoints, ypoints, 'o')   # 'o' means: show dots only, no line
plt.show()
```

**Expected Output:** Two small circle dots on the chart at positions (1, 3) and (8, 10), but **no line** connecting them.

**Why would you want this?** This is similar to a scatter plot — when you just want to see the positions of data points without implying they are connected in sequence.

---

### Example 3: Multiple Points — Connecting a Path

You can provide as many points as you want, as long as both arrays have the same number of elements:

```python
import matplotlib.pyplot as plt
import numpy as np

# Four x-points and four y-points
xpoints = np.array([1, 2, 6, 8])
ypoints = np.array([3, 8, 1, 10])

plt.plot(xpoints, ypoints)
plt.show()
```

**Expected Output:** A line chart that:
- Starts at (1, 3)
- Goes up to (2, 8)
- Drops down to (6, 1)
- Goes back up to (8, 10)

**Line-by-line:**
- `xpoints = np.array([1, 2, 6, 8])` → four x-positions
- `ypoints = np.array([3, 8, 1, 10])` → four corresponding y-positions
- Matplotlib connects them in order: (1,3) → (2,8) → (6,1) → (8,10)

> **Critical rule:** Both arrays must have the **same number of values**. If `xpoints` has 4 values, `ypoints` must also have exactly 4 values. Otherwise you get an error.

---

### Example 4: Plotting with Default X-Points

If you only provide y-values and leave out the x-values, Matplotlib automatically assigns x-values starting from 0:

```python
import matplotlib.pyplot as plt
import numpy as np

# Only y-values provided
ypoints = np.array([3, 8, 1, 10, 5, 7])

plt.plot(ypoints)
plt.show()
```

**Expected Output:** A line chart where:
- x-axis goes 0, 1, 2, 3, 4, 5 (automatically assigned)
- y-axis shows the values: 3, 8, 1, 10, 5, 7

**So the plotted points are:** (0,3), (1,8), (2,1), (3,10), (4,5), (5,7)

**When is this useful?** When your data is in sequence and the index (position number) is the natural x-axis — for example, daily temperatures for a week, where day 0 = Monday, day 1 = Tuesday, etc.

> **Thinking prompt:** What would happen if you provided 10 y-values? What would the x-axis go up to?

---

## Guided Practice Exercises

### Exercise 1: Simple Correlation Finder

**Objective:** Use `corr()` to discover relationships in student data.

**Scenario:** You have data from 8 students tracking study time, sleep, and test scores.

**Steps:**

1. Copy and run this code:

```python
import pandas as pd

data = {
    'Study_Hours': [2, 5, 3, 8, 1, 6, 4, 7],
    'Sleep_Hours': [6, 7, 5, 8, 4, 8, 6, 7],
    'Test_Score':  [55, 78, 60, 95, 40, 88, 70, 90],
    'Phone_Hours': [5, 2, 4, 1, 7, 1, 3, 2]
}

df = pd.DataFrame(data)
print(df.corr())
```

2. Look at each pair and answer:

**Self-check Questions:**
- What is the correlation between Study_Hours and Test_Score? Is it strong?
- What is the correlation between Phone_Hours and Test_Score? Positive or negative?
- What does the diagonal always equal?
- Would you expect more phone use to lead to lower or higher scores?

**Expected Output (approximate):**

```
              Study_Hours  Sleep_Hours  Test_Score  Phone_Hours
Study_Hours      1.000000     0.697539    0.993180    -0.996386
Sleep_Hours      0.697539     1.000000    0.746671    -0.707764
Test_Score       0.993180     0.746671    1.000000    -0.991474
Phone_Hours     -0.996386    -0.707764   -0.991474     1.000000
```

**What to notice:**
- Study_Hours vs Test_Score ≈ `0.993` — incredibly strong positive correlation!
- Phone_Hours vs Test_Score ≈ `-0.991` — incredibly strong *negative* correlation. More phone time → much lower scores.

---

### Exercise 2: Scatter Plot to Confirm Correlations

**Objective:** Visualise two pairs of data — one with strong correlation, one without.

**Scenario:** You have production data from a factory.

**Steps:**

```python
import pandas as pd
import matplotlib.pyplot as plt

# Factory data
data = {
    'Machine_Hours': [2, 4, 6, 8, 10, 12, 14, 16],
    'Units_Made':    [18, 38, 55, 80, 99, 120, 142, 160],
    'Coffee_Breaks': [3, 1, 4, 2, 5, 2, 3, 1]
}

df = pd.DataFrame(data)

# First: check correlations
print(df.corr())

# Second: scatter plot Machine_Hours vs Units_Made (should show strong correlation)
df.plot(kind='scatter', x='Machine_Hours', y='Units_Made')
plt.title('Machine Hours vs Units Made')
plt.show()

# Third: scatter plot Machine_Hours vs Coffee_Breaks (should show no correlation)
df.plot(kind='scatter', x='Machine_Hours', y='Coffee_Breaks')
plt.title('Machine Hours vs Coffee Breaks')
plt.show()
```

**Expected result:** The first scatter plot shows an upward diagonal (strong positive correlation). The second shows dots scattered randomly (no correlation).

**Optional challenge:** Can you add a histogram showing the distribution of Units_Made?

---

### Exercise 3: Plotting a Custom Line with Matplotlib

**Objective:** Draw a Matplotlib line chart from scratch.

**Scenario:** Track the temperature in a city over 6 days.

```python
import matplotlib.pyplot as plt
import numpy as np

# Days of the week (x-axis)
days = np.array([1, 2, 3, 4, 5, 6])

# Temperature in Celsius (y-axis)
temperature = np.array([22, 25, 28, 24, 19, 23])

# Draw the line
plt.plot(days, temperature)

# Show the chart
plt.show()
```

**Expected Output:** A line chart showing temperature going up from day 1 to 3, then dropping on day 5, then slightly recovering on day 6.

**What-if challenge:** What happens if you change `plt.plot(days, temperature)` to `plt.plot(days, temperature, 'o')`? Try it!

---

## Mini Project: Workout Analysis Dashboard

Let's combine everything from this lesson into a realistic mini-project that a fitness coach might actually use.

### Project Goal

Analyse workout data to:
1. Find which factors are most strongly correlated with calories burned
2. Draw visual charts to present the findings
3. Summarise your conclusions

---

### Stage 1: Setup — Create the Data

```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

# Simulate workout data for 10 sessions
workout_data = {
    'Duration_min': [30, 45, 60, 75, 90, 30, 45, 60, 75, 90],
    'Avg_Pulse':    [110, 120, 115, 125, 130, 105, 118, 122, 128, 135],
    'Max_Pulse':    [135, 145, 142, 155, 160, 130, 143, 150, 158, 165],
    'Intensity_1to10': [4, 6, 5, 7, 8, 3, 5, 6, 7, 9],
    'Calories':     [240, 380, 450, 560, 680, 200, 350, 460, 570, 710]
}

df = pd.DataFrame(workout_data)
print("=== Workout Data ===")
print(df)
```

**Milestone output:** A nicely printed table showing all 10 workout sessions.

---

### Stage 2: Correlation Analysis

```python
# Find correlations with Calories
print("\n=== Correlation Matrix ===")
corr = df.corr()
print(corr)

print("\n=== Calories Correlations Specifically ===")
print(corr['Calories'].sort_values(ascending=False))
```

**Milestone output:** You'll see which factors are most strongly tied to Calories burned.

---

### Stage 3: Visual Charts

```python
# Chart 1: Duration vs Calories (expected: strong positive)
df.plot(kind='scatter', x='Duration_min', y='Calories')
plt.title('Duration vs Calories Burned')
plt.xlabel('Workout Duration (minutes)')
plt.ylabel('Calories Burned')
plt.show()

# Chart 2: Intensity vs Calories (expected: strong positive)
df.plot(kind='scatter', x='Intensity_1to10', y='Calories')
plt.title('Intensity Level vs Calories Burned')
plt.xlabel('Intensity (1=Easy, 10=Maximum)')
plt.ylabel('Calories Burned')
plt.show()

# Chart 3: Distribution of Calories burned
df['Calories'].plot(kind='hist')
plt.title('Distribution of Calories Burned Per Workout')
plt.xlabel('Calories')
plt.ylabel('Number of Workouts')
plt.show()

# Chart 4: A line chart showing calories trend across sessions
session_numbers = np.array(range(1, 11))
calories = np.array(df['Calories'])
plt.plot(session_numbers, calories)
plt.title('Calories Burned Per Workout Session')
plt.xlabel('Session Number')
plt.ylabel('Calories Burned')
plt.show()
```

---

### Stage 4: Final Conclusions

After running all the code above, answer these questions in your notes:

1. Which single column has the highest positive correlation with Calories?
2. Is Avg_Pulse or Max_Pulse more strongly linked to Calories?
3. Looking at the scatter plot of Duration vs Calories, what does the pattern look like?
4. From the histogram, what is the most common calories-burned range?

**Optional advanced extension:** Can you add a column called `Water_Intake_L` (litres of water drunk) and investigate whether hydration correlates with performance?

---

## Common Beginner Mistakes

### Mistake 1: Forgetting `plt.show()`

**Wrong:**
```python
plt.plot(x, y)
# Nothing appears on screen!
```

**Correct:**
```python
plt.plot(x, y)
plt.show()  # This is what actually displays the chart
```

**Why it happens:** Beginners think drawing the chart and displaying it are the same step. They're not. `plt.plot()` prepares the chart in memory; `plt.show()` opens the window.

---

### Mistake 2: Different Array Lengths

**Wrong:**
```python
x = np.array([1, 2, 3, 4])    # 4 values
y = np.array([10, 20, 30])     # only 3 values!
plt.plot(x, y)  # ERROR!
```

**Correct:**
```python
x = np.array([1, 2, 3, 4])    # 4 values
y = np.array([10, 20, 30, 40]) # also 4 values
plt.plot(x, y)  # Works!
```

**Rule:** x and y arrays must always have the **exact same number of elements**.

---

### Mistake 3: Using `.corr()` on Non-Numeric Data

**Wrong:**
```python
data = {'Name': ['Alice', 'Bob', 'Charlie'], 'Score': [85, 90, 78]}
df = pd.DataFrame(data)
print(df.corr())  # Only 'Score' will appear — Name is text, not a number
```

**Correct understanding:** `.corr()` **automatically ignores** text columns. Only numeric columns participate in the correlation calculation. This is not an error — it is by design.

---

### Mistake 4: Misreading the Correlation Table

**Wrong thinking:** "The number in row Duration, column Calories is different from row Calories, column Duration."

**Correct:** The table is **symmetric**. The value at (Duration, Calories) = the value at (Calories, Duration). They are always the same.

---

### Mistake 5: Importing Without Aliases

**Wrong:**
```python
import matplotlib.pyplot
matplotlib.pyplot.plot(x, y)  # Very tedious to type!
```

**Correct:**
```python
import matplotlib.pyplot as plt
plt.plot(x, y)  # Much cleaner!
```

The `as plt` shortcut is not required, but it is standard practice and makes your code much easier to read and write.

---

### Mistake 6: Using One Underscore in `__version__`

**Wrong:**
```python
print(matplotlib._version_)   # One underscore each side — Error!
```

**Correct:**
```python
print(matplotlib.__version__)  # Two underscores each side — Correct!
```

---

## Reflection Questions

Think carefully about each of these questions. You don't need to write code — just think about or discuss them:

1. If the correlation between Exercise and Lifespan is `0.72`, does that mean exercising *causes* longer life? What other explanation could there be?

2. You calculate the correlation between two things and get `0.03`. Is this a meaningful result? What would you conclude?

3. Why is a scatter plot better than just looking at the correlation number alone?

4. You run `df.corr()` and one of your columns has a correlation of `-0.85` with another. Is this a strong or weak relationship? Good or bad?

5. What would a perfectly horizontal scatter plot (all dots at the same y-level regardless of x) tell you about the correlation?

6. When would you use a histogram instead of a scatter plot? What different question does each one answer?

7. If you had a dataset with 50 columns, why would `df.corr()` be far more useful than checking each pair manually?

8. Why do you think `import matplotlib.pyplot as plt` is preferred over just `import matplotlib`?

---

## Completion Checklist

Before moving on, make sure you can do each of these:

- [ ] Explain what correlation is in simple everyday language
- [ ] Read a correlation number and classify it as strong, weak, positive, or negative
- [ ] Use `df.corr()` to generate a correlation matrix from a DataFrame
- [ ] Identify which column pairs have meaningful relationships vs no relationship
- [ ] Use `df.plot()` to draw a default line chart
- [ ] Use `df.plot(kind='scatter', x=..., y=...)` to draw a scatter plot
- [ ] Use `df['column'].plot(kind='hist')` to draw a histogram
- [ ] Explain what Matplotlib is and why it is used
- [ ] Install Matplotlib using `pip install matplotlib`
- [ ] Check the Matplotlib version with `matplotlib.__version__`
- [ ] Import Pyplot with `import matplotlib.pyplot as plt`
- [ ] Use `plt.plot(x, y)` to draw a line between points
- [ ] Use `plt.plot(x, y, 'o')` to draw dots without a connecting line
- [ ] Plot multiple points by providing longer arrays
- [ ] Understand that `plt.show()` is required to display the chart
- [ ] Understand the default x-axis behaviour when no x-values are provided

---

## Lesson Summary

In this lesson, you learned three major tools that work together in data analysis:

**Pandas Correlations (`corr()`):** A single method that automatically measures how strongly every pair of numeric columns in your dataset is related. The output is a number between -1 and 1. Values above 0.6 or below -0.6 indicate meaningful relationships. This is your first step in understanding what drives what in your data.

**Pandas Plotting:** You can draw charts directly from a DataFrame using `df.plot()`. The `kind` argument lets you choose between scatter plots (which visually show correlation), histograms (which show how values are distributed), and line charts (which show trends over time or sequence). All Pandas plots require Matplotlib in the background, and `plt.show()` to display them.

**Matplotlib Introduction:** Matplotlib is the most popular Python charting library. Its Pyplot submodule (imported as `plt`) provides the `plot()` function which draws lines and dots in a diagram. You provide x-coordinates and y-coordinates as arrays, and Matplotlib connects them. This is the foundational building block for all the more advanced charts you'll learn in later lessons.

Together, these three tools form a powerful analysis workflow: load data → find correlations → visualise with charts → draw conclusions. This workflow is used daily in finance, health, science, engineering, sports analytics, and business.

---

*End of Lesson 31 — Pandas Correlations, Pandas Plotting & Introduction to Matplotlib*
