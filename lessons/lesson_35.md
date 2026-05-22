---
render_with_liquid: false
title: "Lesson 35: Python Machine Learning — Regression Deep Dive, Scaling, Train/Test & Decision Trees"
nav_order: 35
---

# Lesson 35: Python Machine Learning — Regression Deep Dive, Scaling, Train/Test & Decision Trees

---

## Lesson Introduction

Welcome to Lesson 35! This lesson is one of the most exciting in the whole curriculum — you are about to learn how to build real predictive models, properly prepare your data, rigorously test whether your model actually works, and use one of machine learning's most intuitive and powerful tools: the **Decision Tree**.

By the end of this lesson, you will know how to:

- Use **Polynomial Regression** to model curved, non-linear data
- Use **Multiple Regression** to predict outcomes from more than one input
- **Scale** your data so that different measurement units do not confuse your model
- Use the **Train/Test** method to measure how accurate your model truly is
- Build and read a **Decision Tree** that makes decisions just like a human would

> **Real-world application:** These tools are used every day in Nigerian banks to predict loan defaults, in agricultural research to predict crop yields based on rainfall and temperature, in hospitals to classify patients, and in e-commerce platforms to recommend products.

---

## Prerequisite Concepts

Before we start, let us quickly remind ourselves of what we already know:

**From previous lessons:**
- **Linear Regression** — fitting a straight line through data points to predict future values (e.g., predicting the price of garri based on market trend)
- **R-squared (R²)** — a score from 0 to 1 that tells us how well our regression line fits the data (0 = no relationship, 1 = perfect fit)
- **NumPy** — Python's library for numerical operations and array mathematics
- **Matplotlib** — Python's charting library for drawing scatter plots and graphs
- **Pandas** — Python's library for reading and working with tabular data (like spreadsheets or CSV files)
- **sklearn** — Python's machine learning library (`scikit-learn`) that provides ready-made algorithms

If any of these feel unfamiliar, take a few minutes to review them before continuing. This lesson builds directly on top of them.

---

## Section 1 — Polynomial Regression

### 1.1 What Is It and Why Do We Need It?

In Lesson 34, we learned about **linear regression** — which draws a **straight line** through data. That works perfectly when your data increases (or decreases) at a steady, constant rate.

But what if your data **curves**? What if the pattern bends up and then comes back down?

Think about this real-life example from Lagos: the number of fuel queues (petrol scarcity) throughout the day. In the early morning, there are very few queues. By mid-morning, queues build up. By afternoon, they peak. In the evening, they reduce again. That pattern is **not** a straight line — it **curves**.

For curved data patterns, we need **Polynomial Regression**.

> **Simple analogy:** Linear regression is like drawing a ruler line through your data. Polynomial regression is like bending that ruler into a curve so it follows the ups and downs of the data more closely.

### 1.2 What Is a Polynomial?

Before writing code, let us understand the word "polynomial."

In maths, a **polynomial** is an equation that uses a variable raised to one or more powers. For example:

- `y = 2x + 3` — this is a straight line (degree 1 — linear)
- `y = x² + 2x + 3` — this is a curve (degree 2 — quadratic)
- `y = x³ + x² + 2x + 3` — this is a more complex curve (degree 3 — cubic)

The **degree** tells you how many times the variable `x` is multiplied by itself. A higher degree means more bends in the curve.

> **Thinking prompt:** What would happen if the degree is 1? It would just be linear regression!

### 1.3 The Tollbooth Example

We have data about 18 cars passing a tollbooth. We know each car's speed (km/h) and the time of day (hour). Let us see how speed changes throughout the day.

**Our x values (hours of day):** `[1, 2, 3, 5, 6, 7, 8, 9, 10, 12, 13, 14, 15, 16, 18, 19, 21, 22]`

**Our y values (speed in km/h):** `[100, 90, 80, 60, 60, 55, 60, 65, 70, 70, 75, 76, 78, 79, 90, 99, 99, 100]`

Notice that speeds are high in the early morning, slow down mid-day (perhaps rush hour or road congestion), then pick up again in the evening. That is a **curve**, not a straight line!

#### Step 1 — Draw a Scatter Plot First

Always draw a scatter plot to *see* your data before fitting a model:

```python
import matplotlib.pyplot as plt

x = [1,2,3,5,6,7,8,9,10,12,13,14,15,16,18,19,21,22]
y = [100,90,80,60,60,55,60,65,70,70,75,76,78,79,90,99,99,100]

plt.scatter(x, y)
plt.show()
```

**Expected output in browser:** A scatter plot where the dots form a U-shape (speeds dip in the middle hours and rise at the ends).

#### Step 2 — Fit a Polynomial Regression Line

```python
import numpy
import matplotlib.pyplot as plt

# Our data
x = [1,2,3,5,6,7,8,9,10,12,13,14,15,16,18,19,21,22]
y = [100,90,80,60,60,55,60,65,70,70,75,76,78,79,90,99,99,100]

# Step A: Create the polynomial model
# numpy.polyfit(x, y, 3) — fits a degree-3 (cubic) polynomial
# numpy.poly1d(...) — turns those fit coefficients into a usable model function
mymodel = numpy.poly1d(numpy.polyfit(x, y, 3))

# Step B: Create a smooth line with 100 evenly-spaced points from 1 to 22
myline = numpy.linspace(1, 22, 100)

# Step C: Draw the original scatter points
plt.scatter(x, y)

# Step D: Draw the polynomial regression curve through the data
plt.plot(myline, mymodel(myline))

plt.show()
```

**Expected output in browser:** The scatter plot now has a smooth curved line that follows the U-shape pattern of the dots.

**Line-by-line breakdown:**

| Code | What it does |
|---|---|
| `numpy.polyfit(x, y, 3)` | Calculates the best-fitting polynomial coefficients for degree 3 |
| `numpy.poly1d(...)` | Wraps those coefficients into a function you can call with any x value |
| `numpy.linspace(1, 22, 100)` | Creates 100 evenly spaced numbers from 1 to 22 — used to draw a smooth line |
| `plt.scatter(x, y)` | Draws the original data as dots |
| `plt.plot(myline, mymodel(myline))` | Draws the curve by passing the 100 line points through our model |

> **Thinking prompt:** What if we used degree 1 instead of degree 3? Try changing the `3` to `1` — you would get a straight line (just like linear regression).

### 1.4 Checking the Fit — The R-Squared Score

How do we know if our polynomial curve is a good fit? We check the **R-squared** score.

```python
import numpy
from sklearn.metrics import r2_score

x = [1,2,3,5,6,7,8,9,10,12,13,14,15,16,18,19,21,22]
y = [100,90,80,60,60,55,60,65,70,70,75,76,78,79,90,99,99,100]

mymodel = numpy.poly1d(numpy.polyfit(x, y, 3))

# r2_score compares the actual y values against what the model predicts
print(r2_score(y, mymodel(x)))
```

**Expected output:**
```
0.94
```

**What does 0.94 mean?** It means our polynomial curve explains **94% of the variation** in the speed data. That is an excellent fit! An R² of 0.94 is very close to 1, meaning we can trust this model to make predictions.

> **Rule of thumb:** R² above 0.75 is generally considered a good fit. Below 0.3 means poor fit.

### 1.5 Predicting a Future Value

Once we have a good model (R² is high), we can use it to predict values that are NOT in our original data.

**Question:** What would the speed of a car be at hour 17 (5 PM)?

```python
import numpy
from sklearn.metrics import r2_score

x = [1,2,3,5,6,7,8,9,10,12,13,14,15,16,18,19,21,22]
y = [100,90,80,60,60,55,60,65,70,70,75,76,78,79,90,99,99,100]

mymodel = numpy.poly1d(numpy.polyfit(x, y, 3))

# Predict speed at hour 17
speed = mymodel(17)
print(speed)
```

**Expected output:**
```
88.87
```

So our model predicts a car would be travelling at approximately **88.87 km/h** at 5 PM. We can verify this by looking at where hour 17 falls on our curve — it falls right around that value.

### 1.6 When Polynomial Regression Fails (Bad Fit)

Not all data is suitable for polynomial regression. Let us see what a **bad fit** looks like:

```python
import numpy
import matplotlib.pyplot as plt

# Random, unrelated data
x = [89,43,36,36,95,10,66,34,38,20,26,29,48,64,6,5,36,66,72,40]
y = [21,46,3,35,67,95,53,72,58,10,26,34,90,33,38,20,56,2,47,15]

mymodel = numpy.poly1d(numpy.polyfit(x, y, 3))
myline = numpy.linspace(2, 95, 100)

plt.scatter(x, y)
plt.plot(myline, mymodel(myline))
plt.show()
```

**Expected output in browser:** A scatter plot where the dots are scattered randomly with no clear pattern. The curve barely follows them.

Now check the R² score:

```python
from sklearn.metrics import r2_score

print(r2_score(y, mymodel(x)))
```

**Expected output:**
```
0.00995
```

An R² of **0.01** means the model explains almost **nothing** about the data. This data has no useful pattern — polynomial regression is not appropriate here.

> **Key lesson:** Always check R² before using a model for predictions. A low R² means "do not trust this model."

---

## Section 2 — Multiple Regression

### 2.1 What Is It and Why Do We Need It?

In linear and polynomial regression, we predict `y` from a **single** input value `x`. For example: predicting a car's speed from only the hour of day.

But in real life, outcomes are often influenced by **multiple factors at the same time**.

**Everyday example from Nigeria:** The price of tomatoes in Mile 12 Market, Lagos, depends on:
- The season (rainy or dry)
- Transport cost from the farm
- The quantity available
- How many days since the tomatoes were harvested

If we use only **one** of those factors to predict the price, we would miss a lot of the picture. **Multiple regression** lets us use ALL of them together to make a better prediction.

> **Simple analogy:** Linear regression is like judging a student's final grade only by their test scores. Multiple regression considers test scores, attendance, assignment completion, and class participation — giving a much more accurate prediction.

### 2.2 The Data Set — Car CO2 Emissions

We have a dataset of 36 cars with these columns:
- **Volume** — engine size in cm³ (how big the engine is)
- **Weight** — car weight in kg
- **CO2** — how many grams of CO2 the car emits per km driven

We want to predict **CO2** based on both **Volume** AND **Weight**.

Here is a sample of the data:

| Car | Volume (cm³) | Weight (kg) | CO2 (g/km) |
|---|---|---|---|
| Toyota Aygo | 1000 | 790 | 99 |
| Mitsubishi Space Star | 1200 | 1160 | 95 |
| Skoda Citigo | 1000 | 929 | 95 |
| Mini Cooper | 1500 | 1140 | 105 |
| Audi A6 | 2000 | 1725 | 114 |
| Mercedes SLK | 2500 | 1395 | 120 |

The pattern: heavier cars with bigger engines generally emit more CO2. But we need both pieces of information together.

### 2.3 Installing Prerequisite Libraries

Make sure you have these installed:

```bash
pip install pandas scikit-learn
```

You also need to download `data.csv` — the car dataset. (In a real project, you would have this file in your working directory.)

### 2.4 Building the Multiple Regression Model

```python
import pandas                       # For reading CSV files and handling data tables
from sklearn import linear_model    # For building regression models

# Step 1: Read the data from a CSV file into a DataFrame
df = pandas.read_csv("data.csv")

# Step 2: Define the independent variables (inputs)
# We use BOTH Weight and Volume to predict CO2
# Note: Capital X is convention for the input matrix
X = df[['Weight', 'Volume']]

# Step 3: Define the dependent variable (what we want to predict)
# Note: Lowercase y is convention for the output/target
y = df['CO2']

# Step 4: Create a linear regression object
regr = linear_model.LinearRegression()

# Step 5: Train (fit) the model — it learns the relationship between X and y
regr.fit(X, y)

# Step 6: Predict CO2 for a car with Weight=2300 kg and Volume=1300 cm³
predictedCO2 = regr.predict([[2300, 1300]])
print(predictedCO2)
```

**Expected output:**
```
[107.2087328]
```

Our model predicts that a car weighing **2300 kg** with a **1300 cm³** engine emits approximately **107.2 grams** of CO2 per kilometre.

**Line-by-line breakdown:**

| Code | What it does |
|---|---|
| `df[['Weight', 'Volume']]` | Selects two columns — double brackets `[[...]]` create a 2D table of inputs |
| `df['CO2']` | Selects one column — the thing we want to predict |
| `linear_model.LinearRegression()` | Creates the regression algorithm object |
| `regr.fit(X, y)` | Trains the model — it figures out the mathematical relationship |
| `regr.predict([[2300, 1300]])` | Feeds two input values and asks "what is the predicted CO2?" |

> **Thinking prompt:** Why do we use `[[2300, 1300]]` with double brackets? Because the model expects a 2D input (a table with rows and columns), even if we are predicting just one car.

### 2.5 Coefficients — Understanding What the Model Learned

The word **coefficient** in machine learning means: "how much does this input affect the output?"

```python
import pandas
from sklearn import linear_model

df = pandas.read_csv("data.csv")
X = df[['Weight', 'Volume']]
y = df['CO2']

regr = linear_model.LinearRegression()
regr.fit(X, y)

# Print the coefficients — one for each input variable
print(regr.coef_)
```

**Expected output:**
```
[0.00755095 0.00780526]
```

**Interpretation:**
- **Weight coefficient = 0.00755095** — Every time the car weight increases by **1 kg**, the CO2 emission increases by **0.00755 grams/km**
- **Volume coefficient = 0.00780526** — Every time the engine volume increases by **1 cm³**, the CO2 emission increases by **0.00781 grams/km**

**Let us verify this with a test:** If we increase the weight from 2300 kg to 3300 kg (an increase of 1000 kg), what happens?

```python
predictedCO2 = regr.predict([[3300, 1300]])
print(predictedCO2)
```

**Expected output:**
```
[114.75968007]
```

Let us verify mathematically:

```
107.2087328 + (1000 × 0.00755095) = 107.2087328 + 7.55095 = 114.75968
```

The maths checks out perfectly! The coefficient is correct.

> **Real-world connection:** These coefficients are exactly the kind of numbers that Nigerian environmental agencies use when calculating carbon tax on vehicles — the heavier and bigger the engine, the more CO2, and the higher the levy.

---

## Section 3 — Scale (Feature Scaling)

### 3.1 The Problem with Different Units

Here is a serious problem that beginners often miss.

Look at our car dataset again:
- **Weight** values: 790, 1160, 929, 1725... (values in the hundreds and thousands)
- **Volume** values: 1.0, 1.2, 0.9, 2.5... (values between 0 and 3)

These two columns use **completely different scales**. Weight is in kilograms (large numbers). Volume is in litres (small decimals).

When a machine learning algorithm looks at these numbers, it might accidentally think that Weight is more important just because its numbers are bigger! That is a measurement bias, not a real pattern.

**Think about it this way:** Imagine you are comparing a student's score out of 100 (say, 78) and their height in metres (say, 1.75). The height number (1.75) is much smaller than the score (78), but that does not mean height is less important! They are just on different scales.

**Solution: Scaling!** We transform all our numbers into a common comparable scale.

### 3.2 The Standardization Method

The most common scaling method in machine learning is **standardization** (also called **z-score normalization**). The formula is:

```
z = (x - mean) / standard_deviation
```

Where:
- `x` = the original value
- `mean` = the average of all values in that column
- `standard_deviation` = how spread out the values are
- `z` = the new scaled value

**Let us work through an example manually:**

Weight column mean ≈ 1292.23 kg, Standard deviation ≈ 238.74 kg

For the first car (weight = 790 kg):
```
z = (790 - 1292.23) / 238.74 = -2.1
```

Volume column mean ≈ 1.61 litres, Standard deviation ≈ 0.38 litres

For the first car (volume = 1.0 litres):
```
z = (1.0 - 1.61) / 0.38 = -1.59
```

Now we can compare **-2.1 with -1.59** — both are on the same scale! Much easier for the model to work with.

> **What do negative values mean?** A negative z-score means the value is *below the average*. The first car (Toyota Aygo) is lighter than average (-2.1) and has a smaller engine than average (-1.59). Both make sense for a small city car!

### 3.3 Scaling with Python (The Easy Way)

We do not need to calculate this manually. Python's `sklearn` provides `StandardScaler()`:

```python
import pandas
from sklearn import linear_model
from sklearn.preprocessing import StandardScaler  # The scaling tool

# Create a scaler object
scale = StandardScaler()

# Read the data (this version has Volume in litres, not cm³)
df = pandas.read_csv("data.csv")

# Select our input columns
X = df[['Weight', 'Volume']]

# fit_transform() does two things at once:
# 1. "fit" — learns the mean and std deviation of each column
# 2. "transform" — applies the z-score formula to every value
scaledX = scale.fit_transform(X)

print(scaledX)
```

**Expected output (first few rows):**
```
[[-2.10389253 -1.59336644]
 [-0.55407235 -1.07190106]
 [-1.52166278 -1.59336644]
 ...
```

Notice the very first row is `[-2.1, -1.59]` — exactly what we calculated manually!

### 3.4 Predicting with Scaled Data

When we use scaled data to train our model, we **must also scale** any new data before predicting. Here is the full workflow:

```python
import pandas
from sklearn import linear_model
from sklearn.preprocessing import StandardScaler

scale = StandardScaler()

df = pandas.read_csv("data.csv")

X = df[['Weight', 'Volume']]
y = df['CO2']

# Step 1: Scale the training data
scaledX = scale.fit_transform(X)

# Step 2: Train the model on the SCALED data
regr = linear_model.LinearRegression()
regr.fit(scaledX, y)

# Step 3: To predict, we MUST scale the new input using the SAME scaler
# (scale.transform, NOT scale.fit_transform — we do not re-learn the scale!)
scaled_new = scale.transform([[2300, 1.3]])

# Step 4: Predict using the scaled new values
predictedCO2 = regr.predict([scaled_new[0]])
print(predictedCO2)
```

**Expected output:**
```
[107.2087328]
```

The result is the same as before — but now the model learned from properly scaled data, making it more reliable and fair.

**Critical distinction:**

| Method | When to use |
|---|---|
| `scale.fit_transform(X)` | ONLY on training data — learns the scale parameters AND transforms |
| `scale.transform(new_data)` | On new prediction data — uses already-learned parameters to transform |

> **Common beginner mistake:** Using `fit_transform()` on new prediction data. This would learn NEW mean and std from the tiny new data, giving wrong results. Always use `transform()` for new data after training.

---

## Section 4 — Train/Test

### 4.1 Why Testing Your Model Matters

Imagine you are a WAEC examiner. You give students practice questions, they memorise the answers, and then you test them using those **exact same questions**. Of course they score 100%! But that tells you nothing about whether they actually *understand* the material.

Machine learning models have the same problem. If you test a model on the same data it was trained on, it might score very well — but that does not mean it will work on **new, unseen data** in the real world.

**The solution is Train/Test splitting:**
- Take your data
- Use **80%** to *train* (teach) the model
- Use the remaining **20%** to *test* (evaluate) the model
- The model never sees the test data during training, so the test is fair

> **Nigerian school analogy:** The 80% training data is like the textbook and class notes. The 20% test data is like the WAEC exam questions — unseen, fair, and revealing of actual competence.

### 4.2 Setting Up the Data

We will use a randomly generated dataset of 100 shoppers. For each customer:
- **x** = how many minutes they spent in the shop before buying
- **y** = how much money they spent (in dollars)

```python
import numpy
import matplotlib.pyplot as plt

# Set a random seed so results are reproducible
# (Without this, the random data would change every run)
numpy.random.seed(2)

# Generate 100 random values for "minutes spent in shop"
# numpy.random.normal(mean, std_deviation, num_samples)
x = numpy.random.normal(3, 1, 100)    # Average 3 minutes, std dev 1

# Generate 100 random values for "money spent"
y = numpy.random.normal(150, 40, 100) / x  # Amount divided by time spent

# Visualise the data
plt.scatter(x, y)
plt.show()
```

**Expected output in browser:** A scatter plot showing a downward curve — customers who spend fewer minutes tend to spend more money (perhaps impulsive buyers), while those who take longer spend less per minute.

### 4.3 Splitting into Training and Testing Sets

```python
# The first 80 data points become training data
train_x = x[:80]   # Elements 0 to 79 (80 items)
train_y = y[:80]

# The remaining 20 data points become test data
test_x = x[80:]    # Elements 80 to 99 (20 items)
test_y = y[80:]
```

**Understanding the slice notation:**
- `x[:80]` means "give me elements from the start up to (but not including) index 80"
- `x[80:]` means "give me elements from index 80 all the way to the end"

Let us visualise each set to make sure they look representative:

```python
# Visualise training set
plt.scatter(train_x, train_y)
plt.title("Training Set (80%)")
plt.show()

# Visualise test set
plt.scatter(test_x, test_y)
plt.title("Test Set (20%)")
plt.show()
```

**Expected output:** Both scatter plots should look similar to the full dataset — confirming that neither set is biased or unrepresentative.

### 4.4 Fitting and Evaluating the Model

The data looks like a curve, so we will use polynomial regression (degree 4):

```python
import numpy
from sklearn.metrics import r2_score

numpy.random.seed(2)

x = numpy.random.normal(3, 1, 100)
y = numpy.random.normal(150, 40, 100) / x

train_x = x[:80]
train_y = y[:80]
test_x = x[80:]
test_y = y[80:]

# Train the model on TRAINING data only
mymodel = numpy.poly1d(numpy.polyfit(train_x, train_y, 4))

# Evaluate how well it fits the TRAINING data
r2_train = r2_score(train_y, mymodel(train_x))
print("Training R²:", r2_train)
```

**Expected output:**
```
Training R²: 0.799
```

An R² of 0.80 on training data is acceptable. But this alone tells us very little — the model was trained on this data, so of course it fits it somewhat well.

**The real test — how does it do on UNSEEN test data?**

```python
# Evaluate how well it fits the TEST data (data the model has NEVER seen)
r2_test = r2_score(test_y, mymodel(test_x))
print("Test R²:", r2_test)
```

**Expected output:**
```
Test R²: 0.809
```

The model scores **0.809 on test data** — nearly the same as the training score of 0.799! This is very good news. It means the model is **not memorising** the training data — it has genuinely learned the underlying pattern and can apply it to new, unseen data.

> **What if test R² was much lower than training R²?** That would be a warning sign called **overfitting** — the model memorised the training data but cannot generalise. Imagine a student who memorises specific answers but cannot apply the concept to new questions.

### 4.5 Making a Prediction with the Validated Model

Now that we have confirmed the model works on both training and test data, we can confidently use it:

```python
# Predict: how much will a customer spend if they stay 5 minutes?
predicted_amount = mymodel(5)
print(predicted_amount)
```

**Expected output:**
```
22.88
```

Our model predicts that a customer who stays **5 minutes** in the shop will spend approximately **$22.88**.

**Summary of the Train/Test workflow:**

```
Full Data (100 rows)
        │
        ├── Training Set (80%) ──► Train the model ──► Get R² on training data
        │
        └── Testing Set (20%) ──► Test the model ──► Get R² on test data
                                                               │
                                               If training R² ≈ test R²: Model is GOOD ✓
                                               If test R² << training R²: Model is OVERFITTING ✗
```

---

## Section 5 — Decision Tree

### 5.1 What Is a Decision Tree?

A **Decision Tree** is a machine learning algorithm that makes predictions by asking a series of YES/NO questions — exactly the way a human makes decisions.

Think about how you decide whether to buy jollof rice or fried rice at a bukka:

```
Is it Friday? 
    YES → Is the jollof available?
              YES → Get jollof rice
              NO  → Get fried rice
    NO  → Is it your cheat day?
              YES → Get anything
              NO  → Get the vegetable soup
```

That mental process IS a decision tree! Python can build this same kind of tree automatically from your data.

> **Key difference from regression:** Regression predicts a **number** (like CO2 in grams). A Decision Tree predicts a **category** (like YES or NO, or which class of loan risk, or which product category).

### 5.2 The Comedy Show Dataset

Our example: a person has attended many comedy shows and recorded information about each comedian and whether they went (YES) or didn't go (NO):

| Age | Experience (yrs) | Rank (1–10) | Nationality | Went? |
|---|---|---|---|---|
| 36 | 10 | 9 | UK | NO |
| 42 | 12 | 4 | USA | NO |
| 23 | 4 | 6 | Nigeria | NO |
| 43 | 21 | 8 | USA | YES |
| 66 | 3 | 7 | Nigeria | YES |
| 35 | 14 | 9 | UK | YES |
| 52 | 13 | 7 | Nigeria | YES |
| 18 | 3 | 7 | UK | YES |
| 45 | 9 | 9 | UK | YES |

Given this historical data, we want to build a model that can tell us: "Given a new comedian's details, should I go to their show?"

### 5.3 The Full Code — Building the Decision Tree

```python
import pandas
from sklearn import tree
from sklearn.tree import DecisionTreeClassifier
import matplotlib.pyplot as plt

# Step 1: Read the data
df = pandas.read_csv("data.csv")

# Step 2: Convert text columns to numbers
# Machine learning ONLY works with numbers, not text strings!
# We create a mapping (dictionary) of text → number

# Nationality: UK=0, USA=1, N(Norway)=2
d = {'UK': 0, 'USA': 1, 'N': 2}
df['Nationality'] = df['Nationality'].map(d)

# Target column: YES=1, NO=0
d = {'YES': 1, 'NO': 0}
df['Go'] = df['Go'].map(d)

# Step 3: Separate features (inputs) from target (output)
features = ['Age', 'Experience', 'Rank', 'Nationality']
X = df[features]   # Input: what we know about the comedian
y = df['Go']       # Output: did we go? (1=YES, 0=NO)

# Step 4: Create and train the Decision Tree
dtree = DecisionTreeClassifier()  # Creates the algorithm
dtree = dtree.fit(X, y)           # Trains it on our data

# Step 5: Visualise the tree
tree.plot_tree(dtree, feature_names=features)
plt.show()
```

**Expected output in browser:** A tree diagram with boxes and arrows showing the questions the algorithm asks.

### 5.4 Reading the Decision Tree — Box by Box

The decision tree produces a diagram that looks like a flowchart. Let us read each box carefully.

#### Box 1 — The Root (Top of the Tree): "Rank <= 6.5"

```
Rank <= 6.5
gini = 0.497
samples = 13
value = [6, 7]
```

- **Rank <= 6.5** — The first question: "Does this comedian have a rank of 6.5 or lower?"
  - If YES → go LEFT (these are lower-ranked comedians)
  - If NO → go RIGHT (higher-ranked comedians)
- **gini = 0.497** — This measures how mixed the current data is. Close to 0.5 means very mixed (almost half say YES, half say NO). Close to 0.0 means one side is clearly dominant.
- **samples = 13** — At this point, all 13 comedians are still being evaluated (we haven't split yet)
- **value = [6, 7]** — Of these 13 comedians, 6 got "NO" (don't go) and 7 got "YES" (go)

**Understanding the Gini formula:**
```
Gini = 1 - (x/n)² - (y/n)²

Where:
  x = number of YES answers = 7
  n = total samples = 13
  y = number of NO answers = 6

Gini = 1 - (7/13)² - (6/13)²
     = 1 - 0.2899 - 0.2130
     = 0.497
```

A Gini of 0.497 means this node is nearly 50/50 — very uncertain. Good splits reduce uncertainty.

#### Box 2 (Left branch) — "Low Rank Comedians"

```
gini = 0.0
samples = 5
value = [5, 0]
```

- 5 comedians had Rank <= 6.5
- All 5 got "NO" (value = [5, 0] means 5 NOs, 0 YESs)
- Gini = 0.0 means perfect — no uncertainty. The answer is always NO.
- **Decision: If the comedian's rank is 6.5 or lower → Don't go!**

#### Box 2 (Right branch) — "High Rank Comedians": "Nationality <= 0.5"

```
Nationality <= 0.5
gini = 0.219
samples = 8
value = [1, 7]
```

- 8 comedians had Rank > 6.5
- Of these 8, only 1 got "NO" and 7 got "YES"
- Gini = 0.219 — much lower than before, so we are getting clearer
- Next question: Nationality <= 0.5 — since UK=0, this asks "Is the comedian from the UK?" (0 <= 0.5 is TRUE)

#### Further Branches — Age and Experience

The tree continues splitting, eventually asking about:
- **Age** — younger UK comedians (≤ 35.5) are more likely to go see
- **Experience** — among older UK comedians, those with ≤ 9.5 years experience get a NO

The tree keeps splitting until every branch has a clear, unambiguous answer (gini = 0.0).

### 5.5 Predicting with the Decision Tree

Now we can use the trained tree to predict whether to attend a new show:

```python
# Predict: Should we go see a comedian with these details?
# [Age=40, Experience=10, Rank=7, Nationality=USA(1)]
print(dtree.predict([[40, 10, 7, 1]]))
```

**Expected output:**
```
[1]
```

The tree predicts **1** (YES — go to the show!).

Let us try another comedian:

```python
# [Age=25, Experience=2, Rank=5, Nationality=UK(0)]
print(dtree.predict([[25, 2, 5, 0]]))
```

**Expected output:**
```
[0]
```

Rank of 5 is below 6.5 — the tree says **0** (NO — don't go).

---

## Guided Practice Exercises

### Exercise 1 — Polynomial Regression with Market Data

**Scenario:** Chinwe runs a provision store in Onitsha. She records weekly sales (in units) against average outdoor temperature (°C) for 10 weeks. Hot and cold weeks tend to have different sales patterns for soft drinks.

**Data:**
```python
temp = [18, 20, 22, 24, 26, 28, 30, 32, 34, 36]
sales = [80, 95, 110, 130, 145, 150, 142, 128, 100, 85]
```

**Objective:** Find out if sales follow a polynomial curve with temperature.

**Steps:**

1. Draw a scatter plot of temperature vs. sales
2. Fit a degree-2 polynomial regression (quadratic)
3. Draw the fitted curve on top of the scatter plot
4. Check the R² score

**Expected solution:**

```python
import numpy
import matplotlib.pyplot as plt
from sklearn.metrics import r2_score

temp = [18, 20, 22, 24, 26, 28, 30, 32, 34, 36]
sales = [80, 95, 110, 130, 145, 150, 142, 128, 100, 85]

# Fit a degree-2 polynomial
mymodel = numpy.poly1d(numpy.polyfit(temp, sales, 2))

# Create a smooth line
myline = numpy.linspace(18, 36, 100)

# Plot
plt.scatter(temp, sales, label="Actual Sales")
plt.plot(myline, mymodel(myline), color='red', label="Poly Fit")
plt.xlabel("Temperature (°C)")
plt.ylabel("Sales (units)")
plt.title("Chinwe's Store - Sales vs Temperature")
plt.legend()
plt.show()

# Check R² score
print("R² score:", r2_score(sales, mymodel(temp)))
```

**Expected output:**
```
R² score: ~0.98
```

An R² of ~0.98 is excellent. The quadratic curve closely matches the real sales data.

**Self-check questions:**
- At what temperature are sales highest? (Around 28°C — look at the peak of the curve)
- What would sales be predicted at 25°C? Try `mymodel(25)`
- What does the R² tell us about the relationship between temperature and sales?

---

### Exercise 2 — Multiple Regression for House Prices

**Scenario:** Emeka is a property agent in Abuja. He collects data on houses sold recently. He wants to predict house prices based on size (m²) and number of rooms.

```python
import pandas
from sklearn import linear_model

# Sample data — 8 houses
data = {
    'Size_m2':   [60,  80,  100, 120, 75,  90,  110, 65],
    'Rooms':     [2,   3,   4,   5,   3,   3,   4,   2],
    'Price_M':   [18,  25,  34,  45,  22,  29,  38,  20]  # Price in millions of Naira
}

df = pandas.DataFrame(data)

X = df[['Size_m2', 'Rooms']]
y = df['Price_M']

regr = linear_model.LinearRegression()
regr.fit(X, y)

# Predict price of a 95m² house with 3 rooms
predicted = regr.predict([[95, 3]])
print(f"Predicted price: ₦{predicted[0]:.2f} million")

# Show coefficients
print("Coefficients:", regr.coef_)
```

**Expected output:**
```
Predicted price: ₦28.xx million
Coefficients: [approximately 0.28, 2.5]
```

**Self-check questions:**
- What does the coefficient for `Rooms` tell you? (Each additional room adds approximately ₦2.5 million to the price)
- What does the coefficient for `Size_m2` tell you? (Each additional square metre adds approximately ₦280,000 to the price)
- What would happen to the predicted price if we added one more room?

---

### Exercise 3 — Train/Test on Student Exam Data

**Scenario:** A WAEC data analyst wants to build a model predicting exam scores from hours of study. She has data from 50 students. She wants to test whether the model actually generalises.

```python
import numpy
from sklearn.metrics import r2_score

numpy.random.seed(10)

# Simulate: hours studied (between 1 and 10 hours)
hours = numpy.random.uniform(1, 10, 50)

# Simulate: exam scores (roughly: more hours = higher score, with some randomness)
scores = 40 + (hours * 6) + numpy.random.normal(0, 5, 50)

# Split: 80% train, 20% test
train_hours = hours[:40]
train_scores = scores[:40]
test_hours = hours[40:]
test_scores = scores[40:]

# Fit polynomial regression on training data
mymodel = numpy.poly1d(numpy.polyfit(train_hours, train_scores, 2))

# Evaluate
r2_train = r2_score(train_scores, mymodel(train_hours))
r2_test = r2_score(test_scores, mymodel(test_hours))

print(f"Training R²: {r2_train:.3f}")
print(f"Test R²:     {r2_test:.3f}")

# Predict score for a student who studies 7 hours
print(f"Predicted score for 7 hours: {mymodel(7):.1f}")
```

**Expected output (approximate — varies slightly due to randomness):**
```
Training R²: 0.85x
Test R²:     0.80x
Predicted score for 7 hours: ~82.0
```

**Self-check questions:**
- Are the training R² and test R² close to each other? (Yes — good sign, no overfitting)
- What would it mean if test R² were 0.20 while training R² were 0.85?
- What does the model predict for a student who studies only 1 hour?

---

## Mini Project — Abuja Farmers Market Predictive Intelligence System

In this mini-project, you will build a complete data analysis and prediction system for a farmers market in Abuja. You will use polynomial regression, feature scaling, train/test validation, and a decision tree — all in one project.

**Scenario:** Alhaji Musa manages a weekly farmers market. He wants to use past data to:
1. Predict how many customers will attend based on temperature
2. Predict how much revenue per stall based on customer count and day of week
3. Decide whether to order extra supplies based on weather and forecast

---

### Stage 1 — Polynomial Regression: Temperature vs. Attendance

```python
import numpy
import matplotlib.pyplot as plt
from sklearn.metrics import r2_score

# Historical data: temperature (°C) and customer attendance
temperature = [20, 22, 24, 25, 27, 28, 30, 32, 33, 35, 37, 38]
attendance  = [200, 250, 310, 340, 400, 420, 410, 380, 340, 280, 210, 180]

# Milestone 1: Visualise the data
plt.scatter(temperature, attendance, color='green')
plt.xlabel("Temperature (°C)")
plt.ylabel("Customer Attendance")
plt.title("Abuja Farmers Market — Temperature vs Attendance")
plt.show()
```

**Milestone 1 output:** A scatter plot showing an inverted U-shape — attendance peaks at moderate temperatures and drops in extreme heat.

```python
# Milestone 2: Fit polynomial regression (degree 2)
mymodel = numpy.poly1d(numpy.polyfit(temperature, attendance, 2))
myline = numpy.linspace(20, 38, 100)

plt.scatter(temperature, attendance, color='green', label='Actual')
plt.plot(myline, mymodel(myline), color='blue', label='Polynomial Fit')
plt.legend()
plt.title("Attendance Prediction Model")
plt.show()

r2 = r2_score(attendance, mymodel(temperature))
print(f"Model R²: {r2:.3f}")

# Predict attendance at 29°C
print(f"Predicted attendance at 29°C: {int(mymodel(29))} customers")
```

**Milestone 2 expected output:**
```
Model R²: 0.97x
Predicted attendance at 29°C: ~415 customers
```

---

### Stage 2 — Multiple Regression with Scaling: Predicting Revenue per Stall

```python
import pandas
from sklearn import linear_model
from sklearn.preprocessing import StandardScaler

# Simulated data: 10 market days
data = {
    'Customers':   [200, 320, 415, 380, 250, 440, 300, 360, 410, 270],
    'Day_of_Week': [6,   7,   6,   7,   3,   7,   4,   5,   6,   2],    # 1=Mon, 7=Sun
    'Revenue_k':   [85,  140, 175, 160, 100, 185, 120, 150, 170, 108]    # in thousands of Naira
}

df = pandas.DataFrame(data)

X = df[['Customers', 'Day_of_Week']]
y = df['Revenue_k']

# Scale the features
scale = StandardScaler()
scaledX = scale.fit_transform(X)

# Train multiple regression on scaled data
regr = linear_model.LinearRegression()
regr.fit(scaledX, y)

# Predict revenue: Saturday (Day=7) with 390 customers
new_data = scale.transform([[390, 7]])
predicted_revenue = regr.predict([new_data[0]])
print(f"Predicted revenue: ₦{predicted_revenue[0]:.0f},000 per stall")
```

**Milestone 3 expected output:**
```
Predicted revenue: ₦16x,000 per stall
```

---

### Stage 3 — Decision Tree: Should Musa Order Extra Supplies?

```python
import pandas
from sklearn.tree import DecisionTreeClassifier

# Historical supply decisions
supply_data = {
    'Forecast_Temp':  [28, 35, 25, 30, 32, 22, 29, 38, 26, 31],
    'Is_Weekend':     [1,  0,  1,  1,  0,  1,  0,  1,  0,  1],
    'Rainy_Season':   [0,  1,  0,  0,  1,  1,  0,  1,  0,  0],
    'Order_Extra':    [1,  0,  1,  1,  0,  0,  1,  0,  1,  1]   # 1=YES, 0=NO
}

df_supply = pandas.DataFrame(supply_data)

features = ['Forecast_Temp', 'Is_Weekend', 'Rainy_Season']
X = df_supply[features]
y = df_supply['Order_Extra']

dtree = DecisionTreeClassifier()
dtree.fit(X, y)

# Next Saturday forecast: 30°C, weekend, not rainy season
prediction = dtree.predict([[30, 1, 0]])
decision = "ORDER EXTRA SUPPLIES" if prediction[0] == 1 else "NORMAL ORDER"
print(f"Market Intelligence Decision: {decision}")
```

**Milestone 4 expected output:**
```
Market Intelligence Decision: ORDER EXTRA SUPPLIES
```

**Reflection questions:**
- Which factor (temperature, weekend, or rain season) do you think the tree gives most importance to? (Try looking at the tree diagram)
- What would change if we added more data from 50 market days instead of 10?
- How could Alhaji Musa use this system every week to plan better?

---

## Common Beginner Mistakes

### Mistake 1 — Using fit_transform() on new prediction data

**Wrong:**
```python
# WRONG — learns new mean/std from just 1 data point
new_scaled = scale.fit_transform([[2300, 1.3]])
```

**Correct:**
```python
# CORRECT — uses the mean/std already learned from training data
new_scaled = scale.transform([[2300, 1.3]])
```

**Why it matters:** `fit_transform()` calculates a new mean and standard deviation. With only one data point, it would produce completely wrong scaled values, and your prediction would be garbage.

---

### Mistake 2 — Choosing a polynomial degree that is too high

**Wrong:**
```python
# Degree 10 polynomial — way too complex, will memorise noise
mymodel = numpy.poly1d(numpy.polyfit(x, y, 10))
```

**Correct:**
```python
# Start with degree 2 or 3 — usually enough
mymodel = numpy.poly1d(numpy.polyfit(x, y, 3))
```

**Why it matters:** A very high degree polynomial will perfectly fit the training data but fail completely on new data. This is called **overfitting** — the model memorises noise instead of learning the real pattern.

---

### Mistake 3 — Testing the model on training data (not on unseen data)

**Wrong:**
```python
# WRONG — testing on the same data we trained on
r2 = r2_score(train_y, mymodel(train_x))
print("Model accuracy:", r2)  # This score is misleading!
```

**Correct:**
```python
# CORRECT — train on training data, test on SEPARATE test data
r2_train = r2_score(train_y, mymodel(train_x))
r2_test  = r2_score(test_y,  mymodel(test_x))
print("Training R²:", r2_train)
print("Test R²:", r2_test)
```

**Why it matters:** A model that scores 0.99 on training data but 0.3 on test data is useless in real life. Only the test score tells you how the model will perform on new data.

---

### Mistake 4 — Forgetting to convert text to numbers for Decision Trees

**Wrong:**
```python
# WRONG — decision trees cannot handle text strings
df['Nationality'] = ['UK', 'USA', 'Nigeria', ...]   # still text!
dtree.fit(X, y)   # This will crash with an error
```

**Correct:**
```python
# CORRECT — convert text to numbers first
d = {'UK': 0, 'USA': 1, 'Nigeria': 2}
df['Nationality'] = df['Nationality'].map(d)
dtree.fit(X, y)   # Now it works!
```

**Why it matters:** All machine learning algorithms in sklearn only work with numerical data. Text must always be converted to numbers before fitting.

---

### Mistake 5 — Ignoring R² when checking fit quality

**Wrong:**
```python
# Building a model and jumping straight to predictions
mymodel = numpy.poly1d(numpy.polyfit(x, y, 3))
print(mymodel(50))  # Predicting without knowing if the model is reliable!
```

**Correct:**
```python
# Always check R² BEFORE making predictions
mymodel = numpy.poly1d(numpy.polyfit(x, y, 3))
r2 = r2_score(y, mymodel(x))
print("R²:", r2)
if r2 > 0.75:
    print(mymodel(50))  # Only predict if the model is trustworthy
else:
    print("Model fit is too weak — do not use for predictions!")
```

---

### Mistake 6 — Using X (capital) and y (lowercase) inconsistently

A widely used convention in machine learning:
- `X` (capital) = the **input matrix** (multiple columns, 2D)
- `y` (lowercase) = the **target/output** (single column, 1D)

Mixing them up can cause confusing errors. Stick to this convention always.

---

## Reflection Questions

1. **Polynomial vs. Linear:** You are studying how electricity bills in Lagos change as household size grows from 1 to 10 people. Would you expect the relationship to be linear or curved? Which regression type would you choose first, and why?

2. **Multiple Regression:** Imagine you are predicting the number of patients visiting a Kano hospital per day. List at least three input variables you would include in a multiple regression model. Why is using all three together better than using any one alone?

3. **Feature Scaling:** A dataset has two columns: age (range 20–70) and income in Naira (range 100,000–10,000,000). Without scaling, which column would dominate the model, and why? What would scaling do to fix this?

4. **Train/Test:** You build a model that gets R² = 0.95 on training data but only R² = 0.35 on test data. What does this tell you about the model? What would you do to fix it?

5. **Decision Trees:** Think about how a bank in Nigeria decides whether to approve a loan. What four questions (features) would a bank decision tree likely ask? What would the outcome nodes (leaf nodes) say?

6. **R-Squared interpretation:** Your polynomial regression gets an R² of 0.47. A colleague says "That's almost 50%, it's fine." Do you agree? What R² range would you consider acceptable for a real-world prediction model?

---

## Completion Checklist

Use this checklist to confirm you have mastered the lesson:

- [ ] I can explain what polynomial regression is and when to use it instead of linear regression
- [ ] I can use `numpy.polyfit()` and `numpy.poly1d()` to build a polynomial model
- [ ] I can interpret R-squared values and know what a good score looks like
- [ ] I can use R-squared to judge whether a dataset is suitable for polynomial regression
- [ ] I can explain what multiple regression is and name at least three real-world examples
- [ ] I can build a multiple regression model with pandas and sklearn's `LinearRegression()`
- [ ] I can read and interpret regression coefficients
- [ ] I can explain the problem that feature scaling solves
- [ ] I can use `StandardScaler()` to scale training data and new prediction data correctly
- [ ] I know the difference between `fit_transform()` and `transform()` and when to use each
- [ ] I can explain the train/test split and why it is necessary
- [ ] I can split data into 80% training and 20% testing and evaluate both with R²
- [ ] I understand what overfitting looks like and how train/test helps detect it
- [ ] I can explain what a Decision Tree is and how it makes predictions
- [ ] I can convert text columns to numbers before feeding data to a Decision Tree
- [ ] I can read a decision tree diagram and explain what gini, samples, and value mean
- [ ] I can use `dtree.predict()` to classify new data
- [ ] I have completed all three guided exercises with correct outputs
- [ ] I have attempted all four stages of the mini-project

---

## Lesson Summary

This lesson covered five powerful machine learning concepts that build naturally on each other:

**Polynomial Regression** extends linear regression by fitting curves instead of straight lines. It is used when data has a non-linear pattern (like sales peaking at moderate temperatures). You use `numpy.polyfit()` with a degree > 1, and always check R² to confirm the fit quality before predicting.

**Multiple Regression** allows prediction from more than one input variable simultaneously. Instead of one column X, you pass a table with multiple columns. The model learns a coefficient for each variable, telling you how much each input affects the output.

**Feature Scaling** solves the problem of variables measured in different units or on very different scales. `StandardScaler()` converts each feature to z-scores (mean 0, std 1), making them directly comparable. Always use `fit_transform()` on training data and `transform()` on new prediction data — never the other way around.

**Train/Test splitting** is the standard method for evaluating model quality honestly. By holding out 20% of your data as unseen test data, you get a realistic estimate of how well your model will perform on real-world data. If training R² and test R² are both high and close together, your model is reliable.

**Decision Trees** are intuitive, interpretable models for classification problems (predicting categories, not numbers). They work by learning a series of threshold questions (like "Is rank ≤ 6.5?") from labelled training data. Each node shows the question, the gini impurity, sample count, and class distribution. All input columns must be numeric.

---

## Quick Reference Card

| Concept | Key Function(s) | Purpose |
|---|---|---|
| Polynomial Regression | `numpy.polyfit(x, y, degree)` `numpy.poly1d(...)` | Fit a curved line through data |
| R-squared | `r2_score(y_actual, y_predicted)` | Measure fit quality (0 = bad, 1 = perfect) |
| Multiple Regression | `LinearRegression()` `.fit(X, y)` `.predict([[...]])` | Predict from multiple inputs |
| Regression Coefficients | `regr.coef_` | Shows impact of each input variable |
| Feature Scaling | `StandardScaler()` `.fit_transform(X)` `.transform(new_data)` | Normalize different-scale features |
| Train/Test Split | `x[:80]` / `x[80:]` | Honest model evaluation on unseen data |
| Decision Tree | `DecisionTreeClassifier()` `.fit(X, y)` `.predict([[...]])` | Classify data into categories |
| Gini Impurity | Displayed in tree nodes | Measures node purity (0 = pure, 0.5 = mixed) |
| Convert text to numbers | `df['col'].map({'A': 0, 'B': 1})` | Prepare text data for ML algorithms |

**R² Interpretation Guide:**

| R² Value | Meaning |
|---|---|
| 0.90 – 1.00 | Excellent fit — model is very reliable |
| 0.75 – 0.90 | Good fit — model is usable for predictions |
| 0.50 – 0.75 | Moderate fit — use with caution |
| 0.00 – 0.50 | Poor fit — model not suitable for this data |

**Decision Tree Node Key:**

```
Feature <= threshold       ← The question being asked
gini = X.XXX               ← How mixed the data is at this node
samples = N                ← How many data points reached this node
value = [NO_count, YES_count]  ← Breakdown of outcomes at this node
```

---

*End of Lesson 35. In Lesson 36, we continue with more advanced machine learning tools: the Confusion Matrix, Hierarchical Clustering, and Logistic Regression.*
