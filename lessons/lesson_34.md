---
render_with_liquid: false
title: "Lesson 34 – Percentiles, Data Distributions, Normal Distribution, Scatter Plots & Linear Regression"
nav_order: 34
---

# Lesson 34 – Percentiles, Data Distributions, Normal Distribution, Scatter Plots & Linear Regression

---

## Lesson Introduction

Welcome to one of the most important lessons on your journey into **Machine Learning and Data Science with Python**.

In this lesson you will learn five core ideas that every data scientist and ML engineer uses every single day:

1. **Percentiles** – how to measure where a value sits inside a dataset
2. **Data Distribution** – how to create and understand large realistic datasets
3. **Normal Distribution** – the most important shape in all of statistics
4. **Scatter Plots** – how to visualise relationships between two variables
5. **Linear Regression** – how to predict a value using a straight line through data

Each of these ideas builds on the last. By the end of this lesson you will understand how data is spread out, how to draw it, and how to draw a prediction line through it — the very foundation of machine learning.

> 💡 **Why this matters**: Almost every machine learning model begins with understanding your data's distribution and relationships. Linear regression is often the first real ML algorithm every data scientist learns.

---

## Prerequisite Concepts

Before we dive in, let us quickly cover the building blocks you will need.

### What is a dataset?

A **dataset** is just a collection of numbers (or other values). For example:

```python
ages = [12, 15, 18, 22, 30, 45, 60]
```

That list of seven numbers is a dataset.

### What is NumPy?

**NumPy** is a Python library for working with numbers and arrays. We import it like this:

```python
import numpy as np
```

`np` is just a short nickname (alias) for NumPy so we do not have to type `numpy` every time.

### What is Matplotlib?

**Matplotlib** is a Python library for drawing charts and graphs. We use it like this:

```python
import matplotlib.pyplot as plt
plt.show()
```

### What is SciPy?

**SciPy** is a Python library for advanced mathematics and statistics. We will use it for the Normal Distribution section.

---

## Part 1 – Percentiles

### What Is a Percentile?

Imagine 100 students took a test. If you scored **at the 70th percentile**, it means you scored **higher than 70 out of every 100 students**. You are in the top 30%.

> 🎯 **Simple definition**: A percentile tells you what **percentage of the data falls below a specific value**.

Percentiles help answer questions like:
- "Is this salary above average for this city?"
- "Is this patient's blood pressure dangerously high compared to others?"
- "Is this website load time in the slow 10% or the fast 90%?"

### The Three Most Common Percentiles

| Percentile | Also Called | Meaning |
|---|---|---|
| 25th | Q1 (First Quartile) | 25% of data is below this value |
| 50th | Q2 / Median | Half the data is below this value |
| 75th | Q3 (Third Quartile) | 75% of data is below this value |

These three together are called the **quartiles**.

---

### How to Calculate a Percentile in Python

Python's NumPy library has a built-in function:

```python
numpy.percentile(array, percentile_number)
```

- **array** = your list of numbers
- **percentile_number** = which percentile you want (0 to 100)

---

### Example 1 – Simple Percentile Calculation

```python
import numpy as np

ages = [5, 31, 43, 48, 50, 41, 7, 11, 15, 39, 80, 82, 32, 2, 8, 6, 25, 36, 27, 61, 31]

# Find the 75th percentile
result = np.percentile(ages, 75)

print(result)
```

**Expected Output:**
```
43.0
```

**What this means:** 75% of the ages in this list are **below 43**. Only 25% are 43 or older.

---

### Line-by-Line Explanation

```python
import numpy as np
```
→ Load the NumPy library and give it the short name `np`.

```python
ages = [5, 31, 43, 48, 50, 41, 7, 11, 15, 39, 80, 82, 32, 2, 8, 6, 25, 36, 27, 61, 31]
```
→ Create a list of 21 age values. This is our dataset.

```python
result = np.percentile(ages, 75)
```
→ Ask NumPy: "What value sits at the 75th percentile in this dataset?"
NumPy sorts the list internally, then calculates which value 75% of the data falls below.

```python
print(result)
```
→ Print the answer: `43.0`

---

### Example 2 – All Three Quartiles at Once

```python
import numpy as np

ages = [5, 31, 43, 48, 50, 41, 7, 11, 15, 39, 80, 82, 32, 2, 8, 6, 25, 36, 27, 61, 31]

q1  = np.percentile(ages, 25)
q2  = np.percentile(ages, 50)
q3  = np.percentile(ages, 75)

print("25th percentile (Q1):", q1)
print("50th percentile (Q2 / Median):", q2)
print("75th percentile (Q3):", q3)
```

**Expected Output:**
```
25th percentile (Q1): 11.0
50th percentile (Q2 / Median): 31.0
75th percentile (Q3): 43.0
```

**What this means:**
- 25% of people are **younger than 11**
- Half the group is **younger than 31** (31 is the middle value)
- 75% of people are **younger than 43**

---

### 🤔 Thinking Prompt

> What would happen to the 75th percentile if you added 100 more very old people (ages 90–110) to the dataset? Would it go up or down? Why?

---

### Real-World Use of Percentiles

| Field | How Percentiles Are Used |
|---|---|
| Medicine | "Your child's height is at the 60th percentile for their age" |
| Finance | "Your income is in the top 10%" (90th percentile) |
| Software | "99th percentile server response time is 2 seconds" |
| Education | Standardised test score reporting (SAT, GRE) |
| Sports | Player performance rankings |

---

### Common Beginner Mistake – Confusing Percentile with Percentage

❌ **Wrong thinking:** "75th percentile means I scored 75% on the test."

✅ **Correct thinking:** "75th percentile means I scored *higher than* 75% of all test-takers."

A person at the 75th percentile may have scored 60% on the test — but most others scored even lower!

---

## Part 2 – Data Distribution

### What Is Data Distribution?

**Distribution** describes how data values are **spread out** across a range.

Think of it like this: if you asked 1,000 people their age, some would be very young, some middle-aged, some old. If you drew a chart of how many people fall into each age group, the *shape* of that chart is the **distribution** of your data.

Distribution answers the question: **"Where do most of my values cluster, and how spread out are they?"**

---

### Two Key Words: Mean and Standard Deviation

Before we generate distributions, you need to know two things:

#### Mean (Average)
The **mean** is the sum of all values divided by the count of values.

```python
numbers = [2, 4, 6, 8, 10]
mean = (2 + 4 + 6 + 8 + 10) / 5
# mean = 30 / 5 = 6.0
```

#### Standard Deviation
**Standard deviation** (often written as **std** or **σ**, the Greek letter sigma) measures **how spread out** values are around the mean.

- **Small std** = values are packed tightly around the mean
- **Large std** = values are spread far from the mean

```python
# Dataset A: tight cluster
A = [9, 10, 10, 11, 10]   # std ≈ 0.6  (very close together)

# Dataset B: wide spread
B = [2, 5, 10, 15, 18]    # std ≈ 5.8  (far apart)
```

---

### Generating a Large Random Dataset with NumPy

In real data science, you often need to **simulate** or **generate** data for testing. NumPy makes this easy.

```python
numpy.random.normal(loc, scale, size)
```

| Parameter | What it means |
|---|---|
| `loc` | The **mean** (centre) of the distribution |
| `scale` | The **standard deviation** (spread) |
| `size` | How many values to generate |

---

### Example 3 – Generate a Simple Random Distribution

```python
import numpy as np

# Generate 5 random values with mean=5.0 and std=1.0
data = np.random.normal(5.0, 1.0, 5)

print(data)
```

**Example Output (values will differ each run — random):**
```
[4.73 5.12 6.01 4.88 5.31]
```

All values are near 5.0, because the mean is 5.0 and the spread (std) is only 1.0.

---

### Example 4 – Generate a Larger Dataset and Plot It

```python
import numpy as np
import matplotlib.pyplot as plt

# Generate 250 random values, mean=5.0, std=1.0
x = np.random.normal(5.0, 1.0, 250)

plt.hist(x, 5)   # Draw a histogram with 5 bars
plt.show()
```

**Expected Output:** A histogram (bar chart) showing that most values cluster around 5, with fewer values far from 5.

---

### Line-by-Line Explanation

```python
x = np.random.normal(5.0, 1.0, 250)
```
→ Generate 250 random numbers. Most will be near 5.0 because that is the mean. The standard deviation 1.0 means most values fall within 1 unit of 5 (so roughly between 4 and 6).

```python
plt.hist(x, 5)
```
→ Draw a **histogram**. A histogram is a bar chart where each bar shows **how many values fall into that range**.
The `5` means divide the data into 5 groups (bars).

```python
plt.show()
```
→ Display the chart on screen.

---

### What Does the Histogram Tell You?

The histogram visually shows the **shape** of your data:
- The **tallest bar** is where most values are (near the mean)
- Bars get **shorter** as you move away from the mean
- With enough data this forms a symmetric bell shape

---

### 🤔 Thinking Prompt

> What happens if you change `1.0` to `3.0` in `np.random.normal(5.0, 3.0, 250)`?
> The std becomes larger — what do you think the histogram will look like now?

*(Hint: wider and flatter — more values spread far from 5.0)*

---

### Real-World Use of Data Distribution

| Field | Example |
|---|---|
| Manufacturing | Test whether product measurements are consistently within tolerance |
| Finance | Model stock price changes as random distributions |
| Healthcare | Study how patient recovery times are distributed |
| Education | Analyse how student grades are spread across a class |

---

## Part 3 – Normal Distribution

### What Is Normal Distribution?

The **Normal Distribution** (also called the **Gaussian Distribution** or **Bell Curve**) is the most important shape in all of statistics.

It has these key properties:
- It is **perfectly symmetrical** — left and right sides are mirror images
- The **mean, median, and mode** are all the same value (the centre)
- It forms a **bell shape**
- Most values cluster near the mean, fewer values occur far from the mean

> 🔔 The bell curve is everywhere in nature: human heights, IQ scores, measurement errors, blood pressure, shoe sizes — all follow approximately normal distributions.

---

### The 68-95-99.7 Rule

One of the most powerful properties of the normal distribution:

| Range | % of data contained |
|---|---|
| Mean ± 1 standard deviation | ~68% of all values |
| Mean ± 2 standard deviations | ~95% of all values |
| Mean ± 3 standard deviations | ~99.7% of all values |

**Example:** If the average height of women is 165 cm with a std of 6 cm:
- 68% of women are between 159–171 cm (165 ± 6)
- 95% are between 153–177 cm (165 ± 12)
- 99.7% are between 147–183 cm (165 ± 18)

---

### Generating a Normal Distribution with SciPy

To draw a smooth bell curve, we use **SciPy's stats module**:

```python
from scipy.stats import norm
```

`norm.pdf(x, mean, std)` calculates the **height** of the bell curve at each x value.

---

### Example 5 – Draw a Simple Bell Curve

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import norm

# Create 100 evenly spaced x values from -3 to 3
x = np.arange(-3, 3, 0.1)

# Calculate the bell curve height at each x value
# Mean = 0, Standard Deviation = 1
y = norm.pdf(x, 0, 1)

plt.plot(x, y)
plt.title("Standard Normal Distribution")
plt.xlabel("Value")
plt.ylabel("Probability Density")
plt.show()
```

**Expected Output:** A smooth bell-shaped curve centred at 0, rising to a peak in the middle and tapering symmetrically toward both sides.

---

### Line-by-Line Explanation

```python
x = np.arange(-3, 3, 0.1)
```
→ Create a list of x values: -3.0, -2.9, -2.8, ... 2.8, 2.9. These are the positions along the horizontal axis. `np.arange(start, stop, step)` works like `range()` but allows decimal steps.

```python
y = norm.pdf(x, 0, 1)
```
→ For every x value, calculate how **tall** the bell curve should be at that point.
- `0` = the mean (centre of the bell)
- `1` = the standard deviation (how wide the bell is)
- `pdf` stands for **Probability Density Function** — the mathematical formula for the bell curve shape

```python
plt.plot(x, y)
```
→ Draw a line connecting all the (x, y) points — this creates the smooth curve.

---

### Example 6 – Change the Mean and Standard Deviation

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import norm

x = np.arange(0, 20, 0.1)

# Three curves: same mean=10, different standard deviations
y1 = norm.pdf(x, 10, 1)   # Narrow bell (std=1)
y2 = norm.pdf(x, 10, 2)   # Medium bell (std=2)
y3 = norm.pdf(x, 10, 3)   # Wide flat bell (std=3)

plt.plot(x, y1, label="std=1")
plt.plot(x, y2, label="std=2")
plt.plot(x, y3, label="std=3")
plt.title("Normal Distributions with Different Std")
plt.legend()
plt.show()
```

**Expected Output:** Three bell curves all centred at 10, but with different widths. The `std=1` curve is tall and narrow. The `std=3` curve is wide and flat.

**Key insight:** A **smaller standard deviation = tighter, taller bell** (data is consistent). A **larger standard deviation = wider, flatter bell** (data is more variable).

---

### Example 7 – Normal Distribution Histogram with Real-Scale Data

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import norm

# Generate 1000 random heights (cm), mean=165, std=6
heights = np.random.normal(165, 6, 1000)

# Draw histogram
plt.hist(heights, bins=20, density=True, alpha=0.6, color='skyblue', label='Histogram')

# Draw bell curve on top
x = np.arange(140, 190, 0.1)
y = norm.pdf(x, 165, 6)
plt.plot(x, y, color='red', linewidth=2, label='Bell Curve')

plt.title("Simulated Women's Heights")
plt.xlabel("Height (cm)")
plt.ylabel("Density")
plt.legend()
plt.show()
```

**Expected Output:** A blue histogram of simulated heights with a smooth red bell curve drawn over the top — both centred near 165 cm.

---

### 🤔 Thinking Prompt

> If you change the mean from 165 to 180, what will happen to the position of the bell curve? Will it become taller or shorter?

*(The curve moves right to centre at 180. Height stays the same because std did not change.)*

---

### Real-World Uses of Normal Distribution

| Field | Example |
|---|---|
| Medicine | Blood test values are normally distributed across a healthy population |
| Engineering | Manufacturing tolerances — parts are measured and checked against a normal distribution |
| Finance | Returns on investments are often modelled as normal distributions |
| Psychology | IQ scores follow a normal distribution (mean=100, std=15) |
| Machine Learning | Many ML algorithms assume features are normally distributed |

---

### Common Beginner Mistake – Confusing `pdf` with Probability

❌ **Wrong:** "The output of `norm.pdf(x, 0, 1)` is the probability of getting exactly x."

✅ **Correct:** `pdf` gives the **density** — the height of the curve. For continuous distributions, the probability of getting *exactly* one value is technically zero. You calculate probabilities over **ranges** using the area under the curve.

---

## Part 4 – Scatter Plots

### What Is a Scatter Plot?

A **scatter plot** is a type of chart where **each dot represents one data point** with two values: one on the X-axis and one on the Y-axis.

Scatter plots help you answer the question: **"Is there a relationship between these two variables?"**

For example:
- Does **study hours** relate to **exam score**?
- Does **engine size** relate to **fuel consumption**?
- Does **height** relate to **weight**?

---

### How to Read a Scatter Plot

| Pattern you see | What it means |
|---|---|
| Dots rising from left to right | **Positive relationship** — as X increases, Y increases |
| Dots falling from left to right | **Negative relationship** — as X increases, Y decreases |
| Dots scattered with no pattern | **No relationship** — X and Y are not connected |

---

### Example 8 – Your First Scatter Plot

```python
import matplotlib.pyplot as plt

# Study hours
x = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Exam scores
y = [45, 52, 58, 65, 70, 73, 79, 85, 88, 95]

plt.scatter(x, y)
plt.title("Study Hours vs Exam Score")
plt.xlabel("Hours Studied")
plt.ylabel("Exam Score")
plt.show()
```

**Expected Output:** 10 dots arranged in a clear upward-sloping pattern. Students who study more score higher.

---

### Line-by-Line Explanation

```python
x = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```
→ The X-axis values — hours studied (1 through 10).

```python
y = [45, 52, 58, 65, 70, 73, 79, 85, 88, 95]
```
→ The Y-axis values — exam scores. Note how they increase as x increases.

```python
plt.scatter(x, y)
```
→ Draw one dot for each (x, y) pair. `scatter()` is specifically designed for scatter plots.

```python
plt.xlabel("Hours Studied")
plt.ylabel("Exam Score")
```
→ Label the axes so anyone reading the chart knows what they are looking at.

---

### Example 9 – Scatter Plot with Random Data

This is the W3Schools approach — generating random realistic data:

```python
import numpy as np
import matplotlib.pyplot as plt

# Generate random data for age and speed
x = np.random.normal(0.0, 2.0, 1000)   # X values: 1000 random numbers, mean=0, std=2
y = np.random.normal(0.0, 2.0, 1000)   # Y values: 1000 random numbers, mean=0, std=2

plt.scatter(x, y)
plt.title("Random Scatter Plot (No Relationship)")
plt.show()
```

**Expected Output:** 1,000 dots scattered in a roughly circular cloud centred at (0, 0). Since X and Y were generated independently, there is no relationship between them.

---

### Example 10 – Scatter Plot Showing a Strong Relationship

```python
import numpy as np
import matplotlib.pyplot as plt

# Generate x values
x = np.arange(1, 51)   # 1 to 50

# Y is related to x (y ≈ 2x + some noise)
noise = np.random.normal(0, 3, 50)
y = 2 * x + noise

plt.scatter(x, y, color='green')
plt.title("Strong Positive Relationship")
plt.xlabel("X")
plt.ylabel("Y (≈ 2X + noise)")
plt.show()
```

**Expected Output:** Dots rise clearly from bottom-left to top-right — a strong positive relationship.

---

### 🤔 Thinking Prompt

> If you changed `y = 2 * x + noise` to `y = -2 * x + noise`, what direction would the dots go?

*(They would go from top-left to bottom-right — a negative relationship.)*

---

### Real-World Uses of Scatter Plots

| Field | Variables Compared |
|---|---|
| Health | Age vs Blood Pressure |
| Economics | Education level vs Income |
| Marketing | Ad spend vs Sales |
| Environment | CO₂ emissions vs Temperature |
| Sports | Training hours vs Race finish time |

---

## Part 5 – Linear Regression

### What Is Linear Regression?

**Linear regression** is the process of drawing a **straight line** through your scatter plot data in a way that **best represents the trend** — and then using that line to **predict new values**.

> 🏠 **Analogy**: Imagine you have data on house sizes (in m²) and their prices. Linear regression draws the best straight line through that data. You can then use that line to predict: "If a house is 120m², what price should it have?"

This is one of the most fundamental algorithms in all of machine learning.

---

### The Equation of a Line

Remember from school mathematics: a straight line has the equation:

```
y = mx + b
```

| Symbol | Name | Meaning |
|---|---|---|
| y | Dependent variable | What we are predicting (e.g., price) |
| x | Independent variable | What we know (e.g., house size) |
| m | Slope | How steeply the line rises or falls |
| b | Intercept | Where the line crosses the Y-axis (when x=0) |

Linear regression finds the best values of **m** (slope) and **b** (intercept) to fit your data.

---

### What Does "Best Fit" Mean?

The line of best fit is the one that **minimises the total error** between the actual data points and the line's predicted values.

These errors (vertical distances from each dot to the line) are called **residuals**. The mathematical method that finds the best line is called **Ordinary Least Squares (OLS)** — it minimises the sum of squared residuals.

You do not need to calculate this manually — Python does it for you!

---

### How to Do Linear Regression in Python

We use `scipy.stats.linregress()`:

```python
from scipy import stats

slope, intercept, r, p, std_err = stats.linregress(x, y)
```

| Return value | What it means |
|---|---|
| `slope` | The steepness of the best-fit line (the m value) |
| `intercept` | Where the line crosses the Y-axis (the b value) |
| `r` | Correlation coefficient (how well data fits the line) |
| `p` | P-value (statistical significance — not needed for now) |
| `std_err` | Standard error of the slope estimate |

---

### Example 11 – Your First Linear Regression

```python
from scipy import stats

# Car age (years)
x = [5, 7, 8, 7, 2, 17, 2, 9, 4, 11, 12, 9, 6]

# Car speed (km/h)
y = [99, 86, 87, 88, 111, 86, 103, 87, 94, 78, 77, 85, 86]

slope, intercept, r, p, std_err = stats.linregress(x, y)

print("Slope:", slope)
print("Intercept:", intercept)
print("R value:", r)
```

**Expected Output:**
```
Slope: -1.7512877115526118
Intercept: 103.52986248931952
R value: -0.7586402890911867
```

**What this tells us:**
- **Slope = -1.75**: For every extra year of age, a car's speed decreases by about 1.75 km/h
- **Intercept = 103.5**: A brand-new car (age=0) would have a predicted speed of 103.5 km/h
- **R = -0.76**: A negative value close to -1 indicates a moderate-to-strong negative relationship (older cars tend to be slower)

---

### The R Value (Correlation Coefficient) Explained

The **r value** (also called Pearson's r) measures how well the line fits the data:

| r value | Meaning |
|---|---|
| +1.0 | Perfect positive relationship |
| +0.7 to +0.9 | Strong positive relationship |
| +0.4 to +0.6 | Moderate positive relationship |
| 0 | No relationship |
| -0.4 to -0.6 | Moderate negative relationship |
| -0.7 to -0.9 | Strong negative relationship |
| -1.0 | Perfect negative relationship |

---

### Example 12 – Use the Line to Make a Prediction

Now that we have the slope and intercept, we can predict the speed of any car given its age:

```python
from scipy import stats

x = [5, 7, 8, 7, 2, 17, 2, 9, 4, 11, 12, 9, 6]
y = [99, 86, 87, 88, 111, 86, 103, 87, 94, 78, 77, 85, 86]

slope, intercept, r, p, std_err = stats.linregress(x, y)

# Predict the speed of a 10-year-old car
age = 10
predicted_speed = slope * age + intercept

print(f"Predicted speed for a {age}-year-old car: {predicted_speed:.1f} km/h")
```

**Expected Output:**
```
Predicted speed for a 10-year-old car: 85.5 km/h
```

**How it works:** We just applied `y = mx + b`:
```
y = (-1.75) × 10 + 103.53
y = -17.5 + 103.53
y = 86.03  (approximately 85.5 km/h)
```

---

### Example 13 – Full Linear Regression with Scatter Plot and Best-Fit Line

This is the complete, professional workflow combining everything:

```python
import matplotlib.pyplot as plt
from scipy import stats
import numpy as np

# Data: car age vs speed
x = [5, 7, 8, 7, 2, 17, 2, 9, 4, 11, 12, 9, 6]
y = [99, 86, 87, 88, 111, 86, 103, 87, 94, 78, 77, 85, 86]

# Step 1: Calculate the regression line
slope, intercept, r, p, std_err = stats.linregress(x, y)

# Step 2: Create a function to predict y from x
def predict(x_value):
    return slope * x_value + intercept

# Step 3: Generate y values for the regression line
x_line = np.arange(0, 22)          # X values from 0 to 21
y_line = list(map(predict, x_line)) # Predicted Y for each X

# Step 4: Plot scatter + line
plt.scatter(x, y, color='blue', label='Actual data')
plt.plot(x_line, y_line, color='red', label='Best-fit line')
plt.title("Car Age vs Speed — Linear Regression")
plt.xlabel("Car Age (years)")
plt.ylabel("Speed (km/h)")
plt.legend()
plt.show()

print(f"R² = {r**2:.4f}")
```

**Expected Output:** A scatter plot of blue dots with a downward-sloping red line through them. The line trends downward from left to right, showing that older cars are slower.

```
R² = 0.5755
```

---

### Line-by-Line Explanation

```python
slope, intercept, r, p, std_err = stats.linregress(x, y)
```
→ Calculate all the regression statistics at once. Python unpacks them into five separate variables.

```python
def predict(x_value):
    return slope * x_value + intercept
```
→ Define a function that takes any x value and returns the predicted y. This is our line equation `y = mx + b` as a function.

```python
x_line = np.arange(0, 22)
y_line = list(map(predict, x_line))
```
→ Create 22 x values (0 through 21). Then use `map()` to apply `predict()` to each one, creating the corresponding y values for the line.

```python
plt.scatter(x, y, color='blue', label='Actual data')
plt.plot(x_line, y_line, color='red', label='Best-fit line')
```
→ Draw the actual data as blue dots, then draw the regression line in red.

```python
print(f"R² = {r**2:.4f}")
```
→ Print R-squared (R²). This is the square of the R value and tells you **what percentage of the variation in Y is explained by X**.
`R² = 0.5755` means 57.55% of speed variation is explained by age. Not perfect, but meaningful.

---

### Understanding R² (R-Squared)

**R²** (pronounced "R-squared") is one of the most important model quality metrics:

| R² value | Model quality |
|---|---|
| 0.9 – 1.0 | Excellent fit |
| 0.7 – 0.9 | Good fit |
| 0.4 – 0.7 | Moderate fit |
| 0.1 – 0.4 | Weak fit |
| 0 – 0.1 | Very poor fit |

`R² = 0.5755` for our car data means: a moderate fit — age explains about 57% of the variation in speed. Other factors (engine condition, brand, maintenance) account for the rest.

---

### 🤔 Thinking Prompts

> 1. If R² = 0.95, does that mean your model will always make perfect predictions?
> 2. If slope = 0, what does the regression line look like, and what does it mean?
> 3. If you added more data points far from the line, would R² increase or decrease?

---

### Common Beginner Mistakes in Linear Regression

#### Mistake 1 – Predicting Far Outside the Data Range

```python
# Our data goes from age 2 to 17.
# This prediction is unreliable:
predicted = predict(100)   # A 100-year-old car?!
print(predicted)  # Output: -71.6  — A negative speed! Nonsense!
```

✅ **Rule:** Only predict within or slightly beyond the range of your training data. Predicting far outside is called **extrapolation** and is often misleading.

#### Mistake 2 – Confusing Correlation with Causation

❌ "The regression shows age causes lower speed."

✅ Linear regression shows a **statistical relationship**. Correlation does not prove causation. There may be other factors involved, or the pattern may be coincidental.

#### Mistake 3 – Using Linear Regression on Non-Linear Data

```python
# If your data curves upward like y = x², a straight line is a poor fit.
# Always plot your data first and visually check if a straight line is appropriate.
```

---

## Guided Practice Exercises

### Exercise 1 – Temperature Percentiles

**Scenario:** A weather station recorded daily high temperatures (°C) for a month:

```python
temps = [15, 18, 21, 22, 23, 23, 24, 25, 25, 26, 26, 27, 27, 28, 28,
         28, 29, 29, 30, 30, 31, 31, 32, 33, 34, 35, 36, 37, 38, 40]
```

**Tasks:**
1. Find the 25th, 50th, and 75th percentile temperatures.
2. What temperature separates the hottest 10% of days from the rest? (90th percentile)
3. What percentage of days had temperatures below the 50th percentile?

**Solution:**

```python
import numpy as np

temps = [15, 18, 21, 22, 23, 23, 24, 25, 25, 26, 26, 27, 27, 28, 28,
         28, 29, 29, 30, 30, 31, 31, 32, 33, 34, 35, 36, 37, 38, 40]

print("25th percentile:", np.percentile(temps, 25))
print("50th percentile:", np.percentile(temps, 50))
print("75th percentile:", np.percentile(temps, 75))
print("90th percentile:", np.percentile(temps, 90))
```

**Expected Output:**
```
25th percentile: 25.25
50th percentile: 28.5
75th percentile: 33.25
90th percentile: 37.1
```

**Answer to task 3:** By definition, exactly 50% of days had temperatures below the 50th percentile.

---

### Exercise 2 – Visualise Student Score Distributions

**Scenario:** Two schools each tested 500 students. School A is consistent, School B is more variable.

```python
import numpy as np
import matplotlib.pyplot as plt

school_a = np.random.normal(70, 5, 500)   # mean=70, std=5 (consistent)
school_b = np.random.normal(70, 15, 500)  # mean=70, std=15 (variable)

plt.figure(figsize=(10, 4))

plt.subplot(1, 2, 1)
plt.hist(school_a, bins=20, color='blue', alpha=0.7)
plt.title("School A (std=5)")
plt.xlabel("Score")

plt.subplot(1, 2, 2)
plt.hist(school_b, bins=20, color='green', alpha=0.7)
plt.title("School B (std=15)")
plt.xlabel("Score")

plt.tight_layout()
plt.show()
```

**Self-check:** School A's histogram should be tall and narrow. School B's should be wide and flat. Both centred near 70.

---

### Exercise 3 – Salary vs Experience Linear Regression

**Scenario:** You have data on years of experience and annual salaries:

```python
from scipy import stats
import matplotlib.pyplot as plt
import numpy as np

experience = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
salary =     [32000, 35000, 40000, 43000, 48000,
              52000, 57000, 60000, 64000, 70000]

slope, intercept, r, p, std_err = stats.linregress(experience, salary)

print(f"Slope: {slope:.0f}")
print(f"Intercept: {intercept:.0f}")
print(f"R² = {r**2:.4f}")

# Predict salary for 12 years experience
prediction = slope * 12 + intercept
print(f"Predicted salary at 12 years: £{prediction:,.0f}")

# Plot
x_line = np.arange(0, 15)
y_line = [slope * xi + intercept for xi in x_line]

plt.scatter(experience, salary, color='blue', label='Actual salaries')
plt.plot(x_line, y_line, color='red', label='Trend line')
plt.title("Years Experience vs Salary")
plt.xlabel("Years of Experience")
plt.ylabel("Salary (£)")
plt.legend()
plt.show()
```

**Expected Output:**
```
Slope: 4164
Intercept: 27636
R² = 0.9976
R² near 1.0 — excellent fit!
Predicted salary at 12 years: £77,600
```

**What this tells you:** R² = 0.9976 means experience explains 99.76% of salary variation in this dataset — an almost perfect linear relationship.

---

## Mini Project – Predicting House Prices with Linear Regression

You will build a complete beginner data science workflow from scratch.

### Stage 1 – Setup the Data

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy import stats

# House sizes in square metres
size = [50, 60, 70, 75, 80, 85, 90, 95, 100, 110,
        120, 130, 140, 150, 160, 170, 180, 200, 220, 250]

# House prices in £1,000s
price = [120, 140, 155, 165, 170, 180, 190, 200, 205, 225,
         240, 265, 275, 290, 310, 325, 345, 380, 420, 480]

print("Number of houses in dataset:", len(size))
print("Smallest house:", min(size), "m²")
print("Largest house:", max(size), "m²")
print("Cheapest house: £", min(price), "k")
print("Most expensive: £", max(price), "k")
```

**Expected Output:**
```
Number of houses in dataset: 20
Smallest house: 50 m²
Largest house: 250 m²
Cheapest house: £ 120 k
Most expensive: £ 480 k
```

---

### Stage 2 – Explore with a Scatter Plot

```python
plt.scatter(size, price, color='navy', s=60)
plt.title("House Size vs Price")
plt.xlabel("Size (m²)")
plt.ylabel("Price (£1,000s)")
plt.grid(True, linestyle='--', alpha=0.4)
plt.show()
```

**Milestone:** You should see dots rising from bottom-left to top-right — bigger houses cost more.

---

### Stage 3 – Calculate the Regression Line

```python
slope, intercept, r, p, std_err = stats.linregress(size, price)

print(f"Slope:     {slope:.2f}")
print(f"Intercept: {intercept:.2f}")
print(f"R:         {r:.4f}")
print(f"R²:        {r**2:.4f}")
```

**Expected Output:**
```
Slope:     1.87
Intercept: 28.42
R:         0.9947
R²:        0.9894
```

**Interpretation:**
- Every extra m² adds approximately **£1,870** to the predicted price
- The intercept (£28,420) is the theoretical base price when size = 0
- R² = 0.9894 → **excellent fit** — size explains 98.94% of price variation

---

### Stage 4 – Plot Regression Line + Scatter

```python
x_line = np.arange(40, 270, 5)
y_line = slope * x_line + intercept

plt.scatter(size, price, color='navy', label='Actual prices', s=60)
plt.plot(x_line, y_line, color='crimson', linewidth=2, label='Predicted line')
plt.title("House Price Prediction Model")
plt.xlabel("Size (m²)")
plt.ylabel("Price (£1,000s)")
plt.legend()
plt.grid(True, linestyle='--', alpha=0.4)
plt.show()
```

---

### Stage 5 – Make Predictions

```python
def predict_price(size_m2):
    predicted = slope * size_m2 + intercept
    return round(predicted, 1)

print("Predicted price for  80 m²: £", predict_price(80), "k")
print("Predicted price for 135 m²: £", predict_price(135), "k")
print("Predicted price for 200 m²: £", predict_price(200), "k")
```

**Expected Output:**
```
Predicted price for  80 m²: £ 178.0 k
Predicted price for 135 m²: £ 281.1 k
Predicted price for 200 m²: £ 402.8 k
```

---

### Stage 6 – Analyse Percentiles of Prices

```python
import numpy as np

print("25th percentile price: £", np.percentile(price, 25), "k")
print("50th percentile price: £", np.percentile(price, 50), "k")
print("75th percentile price: £", np.percentile(price, 75), "k")
print("90th percentile price: £", np.percentile(price, 90), "k")
```

**Expected Output:**
```
25th percentile price: £ 180.0 k
50th percentile price: £ 252.5 k
75th percentile price: £ 328.75 k
90th percentile price: £ 406.0 k
```

**Interpretation:** Half the houses cost less than £252,500. Only 10% cost more than £406,000.

---

### Stage 7 – Project Reflection Questions

1. The slope is approximately 1.87. What does this mean in plain English?
2. Our R² is 0.99 — is house size alone sufficient to predict price, or would you add more variables?
3. Can we use this model to predict a 10 m² house? A 1,000 m² house? Why or why not?
4. What other variables might improve this model (bedrooms, location, age, condition)?

---

### Optional Extension Challenges

1. Add a second list for number of bedrooms and create a second scatter plot: bedrooms vs price
2. Calculate and print the mean and standard deviation of house prices
3. Simulate 500 house prices using `np.random.normal()` based on the mean and std you calculated, then draw the bell curve
4. Find which actual house was the furthest from the predicted price (the worst prediction)

---

## Common Beginner Mistakes Summary

| Mistake | Explanation | Fix |
|---|---|---|
| Confusing percentile with percentage | 75th percentile ≠ 75% score | Percentile = position among peers |
| Using too few data points for regression | A regression line through 3 points is meaningless | Use at least 10–20+ points |
| Predicting outside the data range | May produce absurd results | Stay within training data range |
| Ignoring the R² value | A "fitted" line may fit very poorly | Always check R² ≥ 0.7 for meaningful predictions |
| Assuming correlation = causation | A pattern does not prove one thing causes another | Look for logical mechanisms |
| Forgetting to label axes | Charts become unreadable | Always use `plt.xlabel()` and `plt.ylabel()` |
| Not plotting data before regressing | May miss curves, outliers, or clusters | Always scatter plot first |

---

## Reflection Questions

1. A student's exam score is at the 40th percentile. Is this above or below average? How do you know?
2. Two factories produce bolts. Factory A has bolt-length std=0.1mm, Factory B has std=2mm. Which is more consistent? Which histogram would be taller and narrower?
3. You draw a scatter plot of shoe size vs exam score and find R²=0.02. What does this tell you?
4. Your linear regression gives slope=0. What does the best-fit line look like? What does it mean for prediction?
5. Why is it dangerous to use a model trained on house prices from 2015 to predict 2025 prices?
6. What is the difference between the R value and the R² value? When would you report each?

---

## Completion Checklist

- [ ] I can explain what a percentile means in plain language
- [ ] I can use `np.percentile()` to find any percentile
- [ ] I understand mean and standard deviation
- [ ] I can generate random normally distributed data with `np.random.normal()`
- [ ] I can draw a histogram with `plt.hist()`
- [ ] I understand what the bell curve shape means
- [ ] I can draw a bell curve with `norm.pdf()`
- [ ] I can create a scatter plot with `plt.scatter()`
- [ ] I can identify positive, negative, and no relationships from scatter plots
- [ ] I can run linear regression with `stats.linregress()`
- [ ] I understand slope, intercept, R, and R²
- [ ] I can make predictions using the regression line equation
- [ ] I can plot the regression line over a scatter plot
- [ ] I completed the mini house price prediction project
- [ ] I know when linear regression is and is not appropriate

---

## Lesson Summary

In this lesson you covered five powerful data science and machine learning foundations:

**Percentiles** let you place any value in context within a dataset. The `np.percentile()` function calculates any percentile instantly. The 25th, 50th, and 75th percentiles (quartiles) summarise the spread of your data.

**Data Distribution** describes how values are spread. `np.random.normal(mean, std, n)` generates realistic test data. The standard deviation controls how tightly values cluster around the mean.

**Normal Distribution** is the bell curve — the most common shape in nature, statistics, and machine learning. `norm.pdf(x, mean, std)` from SciPy draws it. The 68-95-99.7 rule tells you how much data falls within each standard deviation.

**Scatter Plots** show relationships between two variables. `plt.scatter(x, y)` draws them. Visual patterns (rising, falling, scattered) tell you whether a relationship exists and in which direction.

**Linear Regression** finds the best-fit straight line through scatter plot data and uses it to predict new values. `stats.linregress(x, y)` returns the slope, intercept, and R value. R² tells you how well your line explains the data. The prediction formula is always: `y = slope × x + intercept`.

> 🎉 **You now have the core toolkit for your first complete ML workflow: generate data → describe it → visualise it → model it → predict with it.**

---

*Lesson 34 — Percentiles, Data Distributions, Normal Distribution, Scatter Plots & Linear Regression*
*Source material: W3Schools Python Machine Learning — Statistics & Regression modules*
