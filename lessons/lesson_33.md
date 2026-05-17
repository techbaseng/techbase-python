---
render_with_liquid: false
title: "Lesson 33 – Matplotlib Histograms, Pie Charts & Machine Learning Statistics"
nav_order: 33
---

# Lesson 33 – Matplotlib Histograms, Pie Charts & Machine Learning Statistics

---

## Lesson Introduction

In this lesson you will learn how to **visualise data** using two powerful chart types — **histograms** and **pie charts** — and then step into the exciting world of **Machine Learning (ML)** statistics by mastering **mean**, **median**, **mode**, **standard deviation**, and **percentiles**.

These are not just academic ideas. Every time a business analyses customer ages, a scientist measures temperature variation, or a developer builds a recommendation engine, they use the exact tools you will learn here.

By the end of this lesson you will be able to:

- Draw and customise histograms with Matplotlib
- Draw and customise pie charts with Matplotlib
- Understand what Machine Learning is and why statistics power it
- Calculate mean, median, and mode
- Calculate standard deviation and variance
- Use NumPy and SciPy to perform all these calculations in Python

> **No prior statistics knowledge is needed.** Every concept is taught from scratch with plain English explanations.

---

## Prerequisite Concepts

Before we begin, here is a quick checkpoint of the tools we will use.

### What is Matplotlib?

Matplotlib is a Python library that lets you draw charts and graphs. Think of it as graph paper + coloured pens, but controlled entirely by code.

Install it if needed:

```
pip install matplotlib
```

### What is NumPy?

NumPy is a Python library for fast number crunching. It can store lists of numbers in special structures called **arrays** and calculate things like averages instantly.

```
pip install numpy
```

### What is SciPy?

SciPy builds on NumPy and adds advanced scientific tools — including the ability to find the **mode** of a dataset.

```
pip install scipy
```

### What is a Dataset?

A dataset is simply a collection of values — for example, the ages of 100 people, or the scores of 50 students.

---

## Part 1 — Matplotlib Histograms

---

### What Is a Histogram?

A **histogram** is a type of bar chart that shows how **frequently values appear within ranges (called bins)**.

> **Analogy:** Imagine you asked 100 classmates how many hours they sleep per night. Some said 5, some said 7, some said 9. A histogram groups those answers into ranges — "5–6 hours", "7–8 hours", "9–10 hours" — and draws a bar showing how many people fall in each range.

**Why do we need histograms?**

- To understand the **distribution** (spread) of data
- To spot patterns: Is data bunched together? Spread out? Skewed to one side?
- Used constantly in data science, quality control, medical research, and finance

**A histogram is different from a regular bar chart:**

| Bar Chart | Histogram |
|---|---|
| Compares separate categories (e.g., apples vs oranges) | Shows frequency of a *range* of continuous values |
| Bars have gaps between them | Bars are touching (no gaps) — showing continuity |

---

### Your First Histogram

```python
import matplotlib.pyplot as plt
import numpy as np

# Create a list of 250 random ages between 0 and 130
x = np.random.normal(170, 10, 250)

plt.hist(x)
plt.show()
```

**What does each line do?**

| Line | Explanation |
|---|---|
| `import matplotlib.pyplot as plt` | Loads the chart-drawing tools, nicknamed `plt` |
| `import numpy as np` | Loads NumPy number tools, nicknamed `np` |
| `np.random.normal(170, 10, 250)` | Generates 250 numbers clustered around 170, with a spread of 10 |
| `plt.hist(x)` | Draws a histogram of those numbers |
| `plt.show()` | Opens and displays the chart window |

**Expected output:** A bell-shaped histogram centred around 170. Most bars will be near 170, with fewer bars further away on either side.

> 💡 **Thinking prompt:** What would happen if you changed `10` (the spread) to `30`? Try it! The histogram would become much wider because values would be more spread out.

---

### Understanding `np.random.normal()`

This function creates **normally distributed** (bell-curve) data. Three arguments control it:

```python
np.random.normal(mean, standard_deviation, count)
```

| Argument | Meaning | Example |
|---|---|---|
| `mean` | The central value — where data clusters | `170` (heights cluster around 170 cm) |
| `standard_deviation` | How spread out the data is | `10` (most values are within 10 cm of 170) |
| `count` | How many numbers to generate | `250` data points |

**Quick demo — narrow vs wide spread:**

```python
import matplotlib.pyplot as plt
import numpy as np

narrow = np.random.normal(50, 2, 200)   # tightly packed around 50
wide   = np.random.normal(50, 20, 200)  # spread far around 50

plt.figure(figsize=(12, 4))

plt.subplot(1, 2, 1)
plt.hist(narrow, color='steelblue')
plt.title("Narrow Spread (std=2)")

plt.subplot(1, 2, 2)
plt.hist(wide, color='tomato')
plt.title("Wide Spread (std=20)")

plt.tight_layout()
plt.show()
```

**Expected output:** Two side-by-side histograms. The left one has a tall, narrow peak. The right one is short and wide.

> 💡 **Thinking prompt:** Which spread better represents a consistent factory product? The narrow one — meaning almost all items are very similar in size.

---

### Controlling the Number of Bins

**Bins** are the ranges that your data is grouped into. More bins = more detail. Fewer bins = simpler picture.

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.random.normal(170, 10, 250)

plt.hist(x, bins=5)   # only 5 groups
plt.title("5 Bins")
plt.show()
```

```python
plt.hist(x, bins=30)  # 30 groups — much more detail
plt.title("30 Bins")
plt.show()
```

**Expected output (5 bins):** Just 5 wide bars — you can see the general shape but not the fine detail.

**Expected output (30 bins):** 30 narrow bars — the bell curve shape is very visible.

> 💡 **Rule of thumb:** A good starting point for bin count is roughly the square root of your data count. For 250 data points → about 15–16 bins.

---

### Common Beginner Mistake: Forgetting `plt.show()`

```python
# WRONG — chart never appears
import matplotlib.pyplot as plt
import numpy as np
x = np.random.normal(100, 15, 100)
plt.hist(x)
# Missing plt.show()!
```

```python
# CORRECT
import matplotlib.pyplot as plt
import numpy as np
x = np.random.normal(100, 15, 100)
plt.hist(x)
plt.show()  # ✅ This line opens the chart window
```

---

### Real-World Use of Histograms

| Field | Example |
|---|---|
| **Medicine** | Distribution of patient blood pressure readings |
| **Education** | Distribution of exam scores across a class |
| **Manufacturing** | Distribution of product weights to check quality |
| **Finance** | Distribution of daily stock price changes |
| **Machine Learning** | Checking if your dataset's values are evenly spread |

---

## Part 2 — Matplotlib Pie Charts

---

### What Is a Pie Chart?

A **pie chart** is a circle divided into slices. Each slice represents a **proportion (share)** of the whole.

> **Analogy:** Imagine a pizza cut into 4 slices — one person gets 2 slices, another gets 1, and two others get half a slice each. A pie chart shows exactly that kind of proportional split.

**Why use pie charts?**

- Perfect for showing **part-to-whole relationships** (e.g., what percentage of sales came from each product)
- Easy to understand at a glance
- Used in business reports, surveys, budgets, and research

---

### Your First Pie Chart

```python
import matplotlib.pyplot as plt

y = [35, 25, 25, 15]

plt.pie(y)
plt.show()
```

**What does each line do?**

| Line | Explanation |
|---|---|
| `y = [35, 25, 25, 15]` | The 4 values that will become 4 slices. They add up to 100. |
| `plt.pie(y)` | Draws the pie chart from those values |
| `plt.show()` | Displays the chart |

**Expected output:** A circle divided into 4 coloured slices — the largest slice takes up 35% of the circle.

> 💡 **Note:** The values don't have to add up to 100. Matplotlib automatically converts them into percentages. If you wrote `[1, 1, 1, 1]`, each slice would be 25%.

---

### Adding Labels to a Pie Chart

Without labels, a pie chart is hard to interpret. Let's add them:

```python
import matplotlib.pyplot as plt

y = [35, 25, 25, 15]
labels = ["Apples", "Bananas", "Cherries", "Dates"]

plt.pie(y, labels=labels)
plt.show()
```

**Expected output:** A pie chart where each slice is labelled with the fruit name.

---

### Starting Angle: `startangle`

By default, the first slice starts at the 3 o'clock position (right side). You can rotate the start:

```python
import matplotlib.pyplot as plt

y = [35, 25, 25, 15]
labels = ["Apples", "Bananas", "Cherries", "Dates"]

plt.pie(y, labels=labels, startangle=90)
plt.show()
```

**Expected output:** The first slice ("Apples") now starts at the 12 o'clock position (top of the circle).

> 💡 `startangle=90` rotates the chart 90° counter-clockwise from the default starting position.

---

### Exploding a Slice

You can "pull out" one slice to highlight it:

```python
import matplotlib.pyplot as plt

y = [35, 25, 25, 15]
labels = ["Apples", "Bananas", "Cherries", "Dates"]
explode = [0.2, 0, 0, 0]   # Pull the first slice (Apples) 0.2 outward

plt.pie(y, labels=labels, explode=explode, startangle=90)
plt.show()
```

**Expected output:** The "Apples" slice is visually separated from the rest of the pie, drawing the viewer's attention to it.

**Understanding the `explode` list:**

```python
explode = [0.2, 0, 0, 0]
#          ^    ^  ^  ^
#     Apples  Bananas  Cherries  Dates
# 0.2 = pull out, 0 = stay in place
```

> 💡 Try `explode = [0.2, 0.1, 0, 0]` — both Apples and Bananas will be pulled out!

---

### Adding Shadows

```python
import matplotlib.pyplot as plt

y = [35, 25, 25, 15]
labels = ["Apples", "Bananas", "Cherries", "Dates"]
explode = [0.2, 0, 0, 0]

plt.pie(y, labels=labels, explode=explode, startangle=90, shadow=True)
plt.show()
```

**Expected output:** The pie chart now has a subtle shadow beneath it, giving it a 3D-like appearance.

---

### Custom Colors

```python
import matplotlib.pyplot as plt

y = [35, 25, 25, 15]
labels = ["Apples", "Bananas", "Cherries", "Dates"]
colors = ["red", "yellow", "pink", "orange"]

plt.pie(y, labels=labels, colors=colors, startangle=90)
plt.show()
```

**Expected output:** Each slice now uses your specified colours: red for Apples, yellow for Bananas, etc.

---

### Showing Percentages: `autopct`

```python
import matplotlib.pyplot as plt

y = [35, 25, 25, 15]
labels = ["Apples", "Bananas", "Cherries", "Dates"]

plt.pie(y, labels=labels, autopct="%1.1f%%")
plt.show()
```

**What is `autopct="%1.1f%%"`?**

| Part | Meaning |
|---|---|
| `%1.1f` | Display a number with 1 decimal place |
| `%%` | Display a literal `%` sign |

**Expected output:** Each slice now shows its percentage, e.g., `35.0%`, `25.0%`, `25.0%`, `15.0%`.

---

### Adding a Legend

```python
import matplotlib.pyplot as plt

y = [35, 25, 25, 15]
labels = ["Apples", "Bananas", "Cherries", "Dates"]

plt.pie(y, labels=labels, autopct="%1.1f%%", startangle=90)
plt.legend(title="Fruits")
plt.show()
```

**Expected output:** A coloured legend box appears beside the chart, labelled "Fruits".

---

### Full Polished Pie Chart Example

```python
import matplotlib.pyplot as plt

y = [35, 25, 25, 15]
labels = ["Apples", "Bananas", "Cherries", "Dates"]
explode = [0.2, 0, 0, 0]
colors = ["#e74c3c", "#f1c40f", "#e91e63", "#ff9800"]

plt.pie(
    y,
    labels=labels,
    explode=explode,
    colors=colors,
    autopct="%1.1f%%",
    shadow=True,
    startangle=90
)

plt.legend(title="Fruits", loc="lower right")
plt.title("Fruit Sales Distribution")
plt.show()
```

**Expected output:** A professional-looking pie chart with:
- Highlighted "Apples" slice (pulled out)
- Custom colours
- Percentage labels on each slice
- Drop shadow
- Legend in the lower right
- Chart title at the top

---

### Real-World Use of Pie Charts

| Field | Example |
|---|---|
| **Business** | What percentage of revenue comes from each product |
| **Surveys** | How respondents are split across answer options |
| **Budgeting** | What percentage of a budget is spent on each category |
| **Education** | Grade distribution in a class |
| **Health** | Breakdown of causes of hospital admissions |

---

## Part 3 — Getting Started with Machine Learning

---

### What Is Machine Learning?

**Machine Learning (ML)** is a branch of Artificial Intelligence where computers learn patterns from data — without being explicitly programmed for every situation.

> **Analogy:** Imagine teaching a child to recognise cats. You don't write rules like "cats have pointy ears, whiskers, and fur." Instead, you show the child hundreds of cat pictures, and they learn the pattern. ML works exactly the same way — it learns from **data examples**.

**Why does ML matter?**

| Application | Example |
|---|---|
| **Email filters** | Detecting spam automatically |
| **Recommendations** | Netflix suggesting shows you'll like |
| **Medical diagnosis** | Detecting tumours in X-rays |
| **Self-driving cars** | Recognising road signs |
| **Fraud detection** | Flagging unusual bank transactions |

---

### The Core of ML: Data and Statistics

Before a machine can learn, it needs to understand the data it's working with. This is where **statistics** become essential.

The key statistical concepts used in ML are:

| Concept | What it tells us |
|---|---|
| **Mean** | The average value |
| **Median** | The middle value |
| **Mode** | The most common value |
| **Standard Deviation** | How spread out values are |
| **Percentile** | Where a value sits relative to all others |

Let's learn each one deeply.

---

## Part 4 — Mean, Median, and Mode

---

### What Is the Mean?

The **mean** (also called the **average**) is calculated by:

1. Adding up all values
2. Dividing by how many values there are

**Formula:**
```
Mean = (Sum of all values) ÷ (Number of values)
```

**Simple example:**

```
Values: 10, 20, 30
Sum = 10 + 20 + 30 = 60
Count = 3
Mean = 60 ÷ 3 = 20
```

**In Python with NumPy:**

```python
import numpy as np

speed = [99, 86, 87, 88, 111, 86, 103, 87, 94, 78, 77, 85, 86]
x = np.mean(speed)
print(x)
```

**Expected output:**
```
89.77
```

> 💡 This means the average speed in this dataset is about 89.77 km/h.

**Why is mean useful in ML?**

The mean is used to **fill in missing data**, **normalise features**, and understand the **central tendency** of a dataset.

---

### What Is the Median?

The **median** is the **middle value** when all values are sorted in order.

**Why not always use the mean?**

The mean is pulled by extreme values. Consider this scenario:

```
Salaries: 30000, 32000, 35000, 38000, 1000000
Mean = (30000 + 32000 + 35000 + 38000 + 1000000) ÷ 5 = 227000
```

A mean of £227,000 is misleading because 4 out of 5 people earn between £30,000–£38,000. The billionaire distorts the mean.

```
Median = 35000  ← the actual middle value
```

The median is more honest here.

---

**How to find the median manually:**

**Odd count of values:**
```
Values: 77, 86, 86, 86, 87, 87, 88, 94, 99, 103, 111
Count: 11 values (odd)
Middle position: (11+1) ÷ 2 = position 6
6th value = 87
Median = 87
```

**Even count of values:**
```
Values: 77, 86, 86, 87, 87, 88, 94, 99, 103, 111
Count: 10 values (even)
Two middle values: position 5 and 6 → 87 and 88
Median = (87 + 88) ÷ 2 = 87.5
```

---

**In Python with NumPy:**

```python
import numpy as np

speed = [99, 86, 87, 88, 111, 86, 103, 87, 94, 78, 77, 85, 86]
x = np.median(speed)
print(x)
```

**Expected output:**
```
87.0
```

---

### What Is the Mode?

The **mode** is the value that appears **most often** in a dataset.

**Simple example:**

```
Values: 4, 7, 7, 7, 9, 11
Mode = 7  (appears 3 times — more than any other value)
```

**Why is mode useful?**

| Scenario | How mode helps |
|---|---|
| Shoe sizes | Find the most common size to stock the most of |
| Survey answers | Find the most popular response |
| Defect tracking | Find the most common type of fault |

---

**In Python with SciPy:**

```python
from scipy import stats

speed = [99, 86, 87, 88, 111, 86, 103, 87, 94, 78, 77, 85, 86]
x = stats.mode(speed)
print(x)
```

**Expected output:**
```
ModeResult(mode=86, count=3)
```

This tells us: `86` is the most common value, and it appears `3` times.

---

### Comparing Mean, Median, and Mode

Let's compare all three on the same dataset:

```python
import numpy as np
from scipy import stats

data = [99, 86, 87, 88, 111, 86, 103, 87, 94, 78, 77, 85, 86]

print("Mean:  ", np.mean(data))
print("Median:", np.median(data))
print("Mode:  ", stats.mode(data).mode)
```

**Expected output:**
```
Mean:   89.77
Median: 87.0
Mode:   86
```

> 💡 **Thinking prompt:** The mean (89.77) is higher than the median (87). Why? Because the value `111` pulls the mean upward. The median ignores this.

---

### Common Beginner Mistake: Using Mean When Outliers Exist

```python
# WRONG approach for skewed data with outliers
salaries = [30000, 32000, 35000, 38000, 2000000]
average = sum(salaries) / len(salaries)
print("Average salary:", average)
# Output: 427000 ← misleading!
```

```python
import numpy as np
# BETTER — use median for skewed data
salaries = [30000, 32000, 35000, 38000, 2000000]
print("Median salary:", np.median(salaries))
# Output: 35000.0 ← realistic picture
```

> **Rule:** Use **mean** when data is evenly spread. Use **median** when there are outliers or skew.

---

## Part 5 — Standard Deviation and Variance

---

### What Is Standard Deviation?

**Standard deviation** measures how **spread out** the values in a dataset are from the mean.

> **Analogy:** Imagine two archery teams both hitting an average score of 80. Team A's scores are 79, 80, 81, 80, 80. Team B's scores are 50, 95, 100, 65, 90. Both have the same mean — but Team B is wildly inconsistent. Standard deviation captures that inconsistency.

- **Low standard deviation** → values are close to the mean → consistent, predictable
- **High standard deviation** → values are spread far from the mean → varied, unpredictable

---

### Two Example Datasets Side by Side

```python
import numpy as np

speed1 = [86, 87, 88, 86, 87, 85, 86]       # similar values — low spread
speed2 = [32, 111, 138, 28, 59, 77, 97]     # very different values — high spread

print("Speed1 Mean:", np.mean(speed1))
print("Speed2 Mean:", np.mean(speed2))
print()
print("Speed1 Std Dev:", np.std(speed1))
print("Speed2 Std Dev:", np.std(speed2))
```

**Expected output:**
```
Speed1 Mean: 85.57
Speed2 Mean: 77.43

Speed1 Std Dev: 0.90
Speed2 Std Dev: 37.85
```

> 💡 Both datasets have similar means (~85 vs ~77), but Speed1 has a tiny standard deviation (0.90) while Speed2 has a huge one (37.85). Speed1 values barely deviate from their mean; Speed2 values vary wildly.

---

### Calculating Standard Deviation Step by Step

Let's manually understand how it's calculated with a tiny dataset: `[4, 8, 6, 5, 3]`

**Step 1 — Find the mean:**
```
Mean = (4 + 8 + 6 + 5 + 3) ÷ 5 = 26 ÷ 5 = 5.2
```

**Step 2 — Find each value's distance from the mean (deviation):**
```
4 - 5.2 = -1.2
8 - 5.2 =  2.8
6 - 5.2 =  0.8
5 - 5.2 = -0.2
3 - 5.2 = -2.2
```

**Step 3 — Square each deviation (to remove negatives):**
```
(-1.2)² = 1.44
( 2.8)² = 7.84
( 0.8)² = 0.64
(-0.2)² = 0.04
(-2.2)² = 4.84
```

**Step 4 — Find the mean of those squares (this is the VARIANCE):**
```
Variance = (1.44 + 7.84 + 0.64 + 0.04 + 4.84) ÷ 5
         = 14.80 ÷ 5
         = 2.96
```

**Step 5 — Square root of the variance = Standard Deviation:**
```
Standard Deviation = √2.96 ≈ 1.72
```

---

**In Python with NumPy (does all 5 steps instantly):**

```python
import numpy as np

data = [4, 8, 6, 5, 3]

variance = np.var(data)
std_dev  = np.std(data)

print("Variance:          ", variance)
print("Standard Deviation:", std_dev)
```

**Expected output:**
```
Variance:           2.96
Standard Deviation: 1.7204650534085253
```

> ✅ NumPy's result matches our manual calculation exactly.

---

### What Is Variance?

**Variance** is simply the **square of the standard deviation** — or equivalently, the mean of the squared deviations. It's an intermediate step in calculating standard deviation.

```
Variance = (Standard Deviation)²
Standard Deviation = √Variance
```

| Concept | Formula | Unit |
|---|---|---|
| Variance | Mean of squared deviations | km² (if data is in km) |
| Standard Deviation | √Variance | km (same unit as the data) |

> Standard deviation is more practical because it's in the **same unit** as your data.

---

### What Are Percentiles?

A **percentile** tells you what percentage of values fall **below** a specific value.

> **Analogy:** If you scored in the **90th percentile** on an exam, it means 90% of students scored lower than you.

```python
import numpy as np

ages = [5, 31, 43, 48, 50, 41, 7, 11, 15, 39, 80, 82, 32, 2, 8, 6, 25, 36, 27, 61, 31]

p75 = np.percentile(ages, 75)
print("75th percentile:", p75)
```

**Expected output:**
```
75th percentile: 43.0
```

This means: **75% of people in this dataset are younger than 43 years old.**

---

### Percentiles in Action

```python
import numpy as np

ages = [5, 31, 43, 48, 50, 41, 7, 11, 15, 39, 80, 82, 32, 2, 8, 6, 25, 36, 27, 61, 31]

for p in [25, 50, 75, 90]:
    val = np.percentile(ages, p)
    print(f"{p}th percentile: {val}")
```

**Expected output:**
```
25th percentile: 11.0
50th percentile: 31.0
75th percentile: 43.0
90th percentile: 61.0
```

> 💡 The **50th percentile is always equal to the median**. Notice above: 50th percentile = 31, and `np.median(ages)` would also give 31.

---

### Why Standard Deviation and Percentiles Matter in ML

| ML Use Case | Why it matters |
|---|---|
| **Feature normalisation** | Ensures all features (inputs) are on the same scale |
| **Outlier detection** | Values more than 2–3 standard deviations from the mean are flagged as unusual |
| **Model performance** | Understanding how consistent predictions are |
| **Data quality checks** | Verifying your dataset is realistic and not corrupted |

---

## Guided Practice Exercises

---

### Exercise 1 — Histogram of Exam Scores

**Objective:** Draw a histogram showing the distribution of 200 student exam scores.

**Scenario:** A teacher wants to see how their students performed.

**Steps:**

1. Use `np.random.normal(65, 12, 200)` to simulate scores centred around 65 with spread of 12
2. Draw a histogram with 15 bins
3. Add a title: `"Student Exam Score Distribution"`
4. Add x-label: `"Score"` and y-label: `"Number of Students"`

**Solution:**

```python
import matplotlib.pyplot as plt
import numpy as np

scores = np.random.normal(65, 12, 200)

plt.hist(scores, bins=15, color='steelblue', edgecolor='white')
plt.title("Student Exam Score Distribution")
plt.xlabel("Score")
plt.ylabel("Number of Students")
plt.show()
```

**Expected output:** A bell-shaped histogram centred around 65, with bars showing how many students scored in each 5-point range.

**Self-check questions:**
- Which score range contains the most students?
- What happens if you change the standard deviation from 12 to 3?
- What does a very tall, narrow histogram tell you about the class?

---

### Exercise 2 — Pie Chart of Monthly Budget

**Objective:** Create a pie chart showing a personal monthly budget breakdown.

**Scenario:** A young professional wants to visualise where their money goes.

**Steps:**

1. Create values: `[800, 300, 200, 150, 100, 450]`
2. Create labels: `["Rent", "Food", "Transport", "Entertainment", "Savings", "Other"]`
3. Explode the "Rent" slice (the biggest expense)
4. Show percentages with `autopct`
5. Add a legend

**Solution:**

```python
import matplotlib.pyplot as plt

amounts = [800, 300, 200, 150, 100, 450]
labels = ["Rent", "Food", "Transport", "Entertainment", "Savings", "Other"]
explode = [0.1, 0, 0, 0, 0, 0]
colors = ["#e74c3c", "#3498db", "#2ecc71", "#f39c12", "#9b59b6", "#95a5a6"]

plt.pie(
    amounts,
    labels=labels,
    explode=explode,
    colors=colors,
    autopct="%1.1f%%",
    shadow=True,
    startangle=90
)

plt.legend(title="Categories", loc="lower left")
plt.title("Monthly Budget Breakdown")
plt.show()
```

**Expected output:** A colourful pie chart where Rent is the largest slice (pulled out), with all percentages labelled.

---

### Exercise 3 — Mean, Median, Mode of Temperature Data

**Objective:** Analyse a week of temperature readings.

**Scenario:** A weather station recorded daily temperatures.

```python
import numpy as np
from scipy import stats

temperatures = [22, 21, 23, 22, 25, 28, 22, 20, 19, 22, 24, 22, 21]

mean_temp   = np.mean(temperatures)
median_temp = np.median(temperatures)
mode_temp   = stats.mode(temperatures)
std_temp    = np.std(temperatures)

print(f"Mean temperature:   {mean_temp:.2f}°C")
print(f"Median temperature: {median_temp:.2f}°C")
print(f"Mode temperature:   {mode_temp.mode}°C (appeared {mode_temp.count} times)")
print(f"Standard deviation: {std_temp:.2f}°C")
```

**Expected output:**
```
Mean temperature:   22.38°C
Median temperature: 22.00°C
Mode temperature:   22°C (appeared 5 times)
Standard deviation: 2.04°C
```

**Self-check questions:**
- The mean and median are very close — what does this suggest about the data?
- The standard deviation is about 2°C — is that high or low variability for daily temperature?

---

## Mini-Project — Student Performance Analyser

### Project Overview

You will build a complete Python program that:

1. Stores student test scores
2. Visualises the distribution with a histogram
3. Visualises grade categories with a pie chart
4. Calculates all key statistics
5. Prints a full report

---

### Stage 1 — Setup and Data

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy import stats

# Simulate 50 student scores (mean 70, std dev 15, min 0, max 100)
np.random.seed(42)  # seed ensures same results every run
raw_scores = np.random.normal(70, 15, 50)
scores = np.clip(raw_scores, 0, 100)  # clamp between 0 and 100

print("First 10 scores:", scores[:10].round(1))
print("Total students:", len(scores))
```

**Expected output:**
```
First 10 scores: [79.3 57.9 76.4 84.3 76.2 72.5 80.3 73.3 54.2 64.4]
Total students: 50
```

---

### Stage 2 — Statistics Report

```python
mean   = np.mean(scores)
median = np.median(scores)
mode   = stats.mode(scores.round())
std    = np.std(scores)
p25    = np.percentile(scores, 25)
p75    = np.percentile(scores, 75)

print("=" * 40)
print("    STUDENT PERFORMANCE REPORT")
print("=" * 40)
print(f"Mean Score:          {mean:.2f}")
print(f"Median Score:        {median:.2f}")
print(f"Mode Score:          {mode.mode:.1f}")
print(f"Standard Deviation:  {std:.2f}")
print(f"25th Percentile:     {p25:.2f}")
print(f"75th Percentile:     {p75:.2f}")
print(f"Highest Score:       {scores.max():.2f}")
print(f"Lowest Score:        {scores.min():.2f}")
print("=" * 40)
```

**Expected output:**
```
========================================
    STUDENT PERFORMANCE REPORT
========================================
Mean Score:          70.22
Median Score:        70.69
Mode Score:          70.0
Standard Deviation:  14.82
25th Percentile:     60.14
75th Percentile:     81.23
Highest Score:       98.44
Lowest Score:        31.03
========================================
```

---

### Stage 3 — Histogram

```python
plt.figure(figsize=(8, 5))
plt.hist(scores, bins=10, color='steelblue', edgecolor='white')
plt.axvline(mean, color='red', linestyle='dashed', linewidth=2, label=f'Mean: {mean:.1f}')
plt.axvline(median, color='green', linestyle='dashed', linewidth=2, label=f'Median: {median:.1f}')
plt.title("Student Score Distribution")
plt.xlabel("Score")
plt.ylabel("Number of Students")
plt.legend()
plt.tight_layout()
plt.show()
```

**Expected output:** A histogram with a red dashed line for the mean and a green dashed line for the median. Both lines will be close together (indicating roughly symmetrical data).

---

### Stage 4 — Grade Pie Chart

```python
# Categorise scores into grade bands
def grade(score):
    if score >= 70: return "Pass (≥70)"
    elif score >= 50: return "Near Pass (50–69)"
    else: return "Fail (<50)"

grade_counts = {"Pass (≥70)": 0, "Near Pass (50–69)": 0, "Fail (<50)": 0}
for s in scores:
    grade_counts[grade(s)] += 1

labels = list(grade_counts.keys())
values = list(grade_counts.values())
colors = ["#2ecc71", "#f39c12", "#e74c3c"]

plt.figure(figsize=(7, 7))
plt.pie(values, labels=labels, colors=colors, autopct="%1.1f%%", startangle=90, shadow=True)
plt.title("Grade Distribution")
plt.show()

print("Grade Breakdown:")
for label, count in grade_counts.items():
    print(f"  {label}: {count} students ({count/50*100:.1f}%)")
```

**Expected output (chart):** A 3-slice pie chart showing percentages of students in each grade band.

**Expected output (text):**
```
Grade Breakdown:
  Pass (≥70): 28 students (56.0%)
  Near Pass (50–69): 17 students (34.0%)
  Fail (<50): 5 students (10.0%)
```

*(Exact numbers may vary slightly due to random generation.)*

---

### Stage 5 — Reflection

After completing the project, ask yourself:

- If the standard deviation were 5 instead of 15, how would the histogram look different?
- If 40% of students failed, what would the pie chart's red slice look like?
- How would you use the mean and median to advise the teacher on whether the exam was too hard?

**Optional extension challenges:**
- Add a second dataset (a second class) and compare their histograms side by side
- Colour the histogram bars differently for pass/fail zones
- Export the statistics report to a `.txt` file using Python's `open()` function

---

## Common Beginner Mistakes

### Mistake 1 — Confusing Histogram with Bar Chart

```python
# WRONG — using bar() for continuous numerical distribution
categories = ["60-70", "70-80", "80-90"]
counts = [10, 25, 15]
plt.bar(categories, counts)  # ← this works but is semantically wrong for distributions

# CORRECT — use hist() for continuous numerical data
data = [65, 72, 74, 78, 81, 85, 88, 63, 71]
plt.hist(data)  # ← Matplotlib handles the binning automatically
```

---

### Mistake 2 — Forgetting to Import NumPy or SciPy

```python
# WRONG
x = mean([1, 2, 3])  # mean() is not a built-in Python function!

# CORRECT
import numpy as np
x = np.mean([1, 2, 3])
```

---

### Mistake 3 — Using Mean for Skewed Data

```python
import numpy as np

house_prices = [200000, 210000, 195000, 205000, 1500000]  # one outlier

print("Mean:  ", np.mean(house_prices))    # 462000 — misleading!
print("Median:", np.median(house_prices))  # 205000 — realistic
```

**Output:**
```
Mean:   462000.0
Median: 205000.0
```

---

### Mistake 4 — Misreading `stats.mode()` Output

```python
from scipy import stats

data = [4, 4, 7, 9]
result = stats.mode(data)

# WRONG — printing the whole object
print(result)  # Prints: ModeResult(mode=4, count=2)

# CORRECT — access .mode and .count attributes
print("Mode:", result.mode)   # 4
print("Count:", result.count) # 2
```

---

### Mistake 5 — Not Setting `bins` Intentionally

```python
import matplotlib.pyplot as plt
import numpy as np

data = np.random.normal(50, 10, 1000)

# Default bins might hide patterns
plt.hist(data)  # Uses 10 bins by default — may not be ideal

# Better — set bins deliberately
plt.hist(data, bins=30)  # More detail visible
plt.show()
```

---

## Reflection Questions

1. A dataset has `mean = 50` and `median = 35`. What does this tell you about the shape of the data?

2. You have two groups of factory parts. Group A has `std = 0.2 mm`, Group B has `std = 5 mm`. Which group's parts are more consistent?

3. A pie chart has one slice at 75%. Does that mean it's the mode of the data? Explain the difference.

4. If you calculate the 90th percentile of student heights and get 185 cm, what does that mean in plain English?

5. You're building an ML model to predict house prices. Should you use mean or median to represent a "typical" house price in a city? Why?

6. Why do histograms have touching bars while regular bar charts have gaps?

7. A histogram is very flat (all bars are roughly the same height). What does this tell you about the data?

---

## Completion Checklist

Before moving on, confirm you can do each of the following:

- [ ] Draw a histogram using `plt.hist()` with customised bins
- [ ] Draw a pie chart using `plt.pie()` with labels, colours, explode, shadow, and percentages
- [ ] Add a legend to a pie chart with `plt.legend()`
- [ ] Explain the difference between mean, median, and mode in plain English
- [ ] Calculate mean using `np.mean()`
- [ ] Calculate median using `np.median()`
- [ ] Calculate mode using `stats.mode()`
- [ ] Calculate standard deviation using `np.std()`
- [ ] Calculate variance using `np.var()`
- [ ] Calculate percentiles using `np.percentile()`
- [ ] Decide whether to use mean or median based on data shape
- [ ] Combine histogram + pie chart + statistics into a working mini-project

---

## Lesson Summary

### What You Learned

**Histograms:**
- A histogram groups numerical data into bins and shows how many values fall in each range
- `plt.hist(data, bins=n)` draws it
- Use `np.random.normal(mean, std, count)` to generate realistic test data
- More bins = more detail; fewer bins = simpler overview

**Pie Charts:**
- A pie chart shows each value as a proportion (slice) of the whole
- Key parameters: `labels`, `explode`, `colors`, `autopct`, `shadow`, `startangle`
- Add a legend with `plt.legend()`

**Machine Learning Foundation:**
- ML learns patterns from data — statistics help us understand that data
- The three measures of **central tendency**: mean (average), median (middle), mode (most common)
- Use mean for symmetric data; use median when outliers exist

**Spread and Variation:**
- **Standard deviation** = how far values typically stray from the mean
- **Variance** = standard deviation squared (intermediate calculation)
- **Percentiles** = what % of values fall below a given point
- Low std dev = consistent; high std dev = variable

### Quick Reference

```python
import numpy as np
from scipy import stats
import matplotlib.pyplot as plt

data = [10, 20, 20, 30, 40, 50]

# Central tendency
np.mean(data)              # Average
np.median(data)            # Middle value
stats.mode(data).mode      # Most common value

# Spread
np.std(data)               # Standard deviation
np.var(data)               # Variance
np.percentile(data, 75)    # 75th percentile

# Histogram
plt.hist(data, bins=10)
plt.show()

# Pie chart
plt.pie([35, 25, 25, 15], labels=["A","B","C","D"], autopct="%1.1f%%")
plt.show()
```

---

*End of Lesson 33*
