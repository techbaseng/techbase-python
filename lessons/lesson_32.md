---
render_with_liquid: false
title: "Lesson 32 – Matplotlib Visualisation: Markers, Lines, Labels, Grids, Subplots, Scatter Charts, and Bar Charts"
nav_order: 32
---

# Lesson 32 – Matplotlib Visualisation: Markers, Lines, Labels, Grids, Subplots, Scatter Charts, and Bar Charts

---

## Lesson Introduction

Have you ever looked at a news article and seen a line graph showing how temperatures changed over a year, or a bar chart comparing sales across different months?  
Those visuals are **charts** — and in Python, one of the most popular tools for creating them is a library called **Matplotlib**.

In this lesson you will learn how to:

- Add **markers** to highlight data points on a line chart
- Control how the **line** looks — its style, colour, and thickness
- Add **labels** (titles, axis names) so your chart tells a story
- Add a **grid** to make values easier to read
- Place multiple charts side-by-side using **subplots**
- Draw **scatter charts** to spot patterns between two variables
- Draw **bar charts** to compare categories

This lesson is designed for **absolute beginners**. You do not need any prior knowledge of Matplotlib or charting. Every concept is explained from the ground up, with simple examples before more complex ones.

> **Real-world relevance:** Data scientists, engineers, teachers, healthcare analysts, and business managers use charts daily to understand and present information. Learning to create charts in Python is one of the most practical and in-demand skills you can build.

---

## Prerequisite Concepts

Before diving in, here is everything you need to know to follow this lesson comfortably.

### What Is a Library?

Python comes with many built-in tools. A **library** is a collection of extra tools someone has already written that you can add to your project.  
Think of it like a toolbox: Python gives you a basic set of tools, and you can borrow extra specialised tools from a library when you need them.

### Installing and Importing Matplotlib

Matplotlib is not built into Python. You install it once from your terminal:

```bash
pip install matplotlib
```

Then, at the top of every Python file where you want to use it, you **import** it:

```python
import matplotlib.pyplot as plt
```

- `matplotlib` — the full library name
- `pyplot` — the specific module inside the library that handles plotting
- `plt` — a short nickname (alias) we choose so we don't have to type `matplotlib.pyplot` every time

### What Is `plt.show()`?

After you write code to build a chart, you call `plt.show()` to actually **display** it in a window.  
Think of it like writing a letter and then pressing "send" — `plt.show()` is the "send" step.

### What Are Lists?

Charts need data. In Python, data is often stored in a **list** — a collection of values in square brackets:

```python
x = [1, 2, 3, 4, 5]
y = [10, 20, 15, 30, 25]
```

Here `x` might represent days and `y` might represent temperatures recorded on those days.

### What Is a Plot?

A **plot** is just another word for a chart or graph. When we say "plot the data", we mean "draw a chart using this data".

---

## Part 1 – Matplotlib Markers

### What Are Markers?

When you draw a line chart, the line is drawn **between** your data points.  
A **marker** is a small symbol placed exactly **at each data point** so you can clearly see where actual values were recorded.

> **Analogy:** Imagine walking along a path and placing a small flag at every location you stopped to take a note. Those flags are markers.

Without markers, you just see a smooth line. With markers, you can see exactly where each measurement was taken.

### Your First Marker Example

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [3, 7, 2, 9, 5]

plt.plot(x, y, marker='o')
plt.show()
```

**Expected output:** A line chart with a small filled circle (`o`) drawn at each of the five data points.

**Line-by-line explanation:**

| Line | What it does |
|------|--------------|
| `import matplotlib.pyplot as plt` | Loads the plotting tools and gives them the nickname `plt` |
| `x = [1, 2, 3, 4, 5]` | The horizontal (x-axis) values — positions along the bottom |
| `y = [3, 7, 2, 9, 5]` | The vertical (y-axis) values — the heights of each point |
| `plt.plot(x, y, marker='o')` | Draws a line through all points AND places a circle at each point |
| `plt.show()` | Displays the chart |

### All Available Marker Styles

Matplotlib gives you many marker shapes. Here is a complete reference table:

| Marker code | Shape description |
|-------------|------------------|
| `'o'` | Circle |
| `'*'` | Star |
| `'.'` | Small dot |
| `','` | Pixel (tiny single pixel) |
| `'x'` | Cross (×) |
| `'X'` | Filled cross (×) |
| `'+'` | Plus sign (+) |
| `'P'` | Filled plus sign |
| `'s'` | Square |
| `'D'` | Diamond |
| `'d'` | Thin diamond |
| `'p'` | Pentagon |
| `'H'` | Hexagon (flat top) |
| `'h'` | Hexagon (pointy top) |
| `'v'` | Triangle pointing down |
| `'^'` | Triangle pointing up |
| `'<'` | Triangle pointing left |
| `'>'` | Triangle pointing right |
| `'1'` | Tri-down |
| `'2'` | Tri-up |
| `'3'` | Tri-left |
| `'4'` | Tri-right |
| `'|'` | Vertical line |
| `'_'` | Horizontal line |

### Trying Different Markers

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [3, 7, 2, 9, 5]

plt.plot(x, y, marker='*')
plt.show()
```

**Expected output:** Same line chart, but now a star symbol sits at each data point.

> **Thinking prompt:** What would happen if you changed `'*'` to `'s'`? Try it — you should see squares at each point instead of stars.

### Controlling Marker Size

You can change how large the markers are using the `markersize` parameter (shortened as `ms`):

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [3, 7, 2, 9, 5]

plt.plot(x, y, marker='o', ms=15)
plt.show()
```

**Expected output:** The same chart but with noticeably larger circles at each data point.

- `ms=15` means the marker diameter is 15 points (the default is around 6)

### Controlling Marker Colour

Use `mec` (marker edge colour) to change the **outline** colour of the marker, and `mfc` (marker face colour) to change the **fill** colour:

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [3, 7, 2, 9, 5]

plt.plot(x, y, marker='o', ms=15, mec='red', mfc='blue')
plt.show()
```

**Expected output:** Large circles — filled blue with a red outline — at each data point.

**Parameter reference:**

| Parameter | Full name | What it controls |
|-----------|-----------|-----------------|
| `mec` | marker edge color | The colour of the border/outline of the marker |
| `mfc` | marker face color | The colour of the inside/fill of the marker |
| `ms` | markersize | How large the marker is |

### Accepted Colour Values

You can specify colours in several ways:

```python
mec='red'          # by name
mec='#FF0000'      # by hex code (same as red)
mec=(1.0, 0, 0)    # by RGB tuple (red, green, blue each 0–1)
```

> **Common mistake:** Spelling `colour` the British way — Python only accepts `color` (American spelling) in Matplotlib.

### Shorthand Format String for Marker + Line + Colour

Matplotlib allows a very compact "format string" that sets the **colour**, **marker**, and **line style** all at once using a short code:

```
plt.plot(x, y, 'r*--')
```

This means:
- `r` = red colour
- `*` = star marker
- `--` = dashed line

**Full shorthand example:**

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [3, 7, 2, 9, 5]

plt.plot(x, y, 'g^-.')
plt.show()
```

**Expected output:** A green line with triangles at each point, drawn in a dot-dash pattern.

**Format string quick reference:**

| Character | Meaning |
|-----------|---------|
| `r` | Red |
| `g` | Green |
| `b` | Blue |
| `k` | Black |
| `y` | Yellow |
| `m` | Magenta |
| `c` | Cyan |
| `w` | White |
| `o` | Circle marker |
| `*` | Star marker |
| `s` | Square marker |
| `-` | Solid line |
| `--` | Dashed line |
| `-.` | Dash-dot line |
| `:` | Dotted line |

---

## Part 2 – Matplotlib Line Styling

### What Is Line Styling?

A chart line can be customised in three main ways:
1. Its **style** — solid, dashed, dotted, etc.
2. Its **colour** — any named colour or hex code
3. Its **width** — how thick or thin the line is

These are all controlled by parameters inside `plt.plot()`.

### Line Style

Use `linestyle` (or shortened `ls`) to change the style of the line:

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [3, 7, 2, 9, 5]

plt.plot(x, y, linestyle='dashed')
plt.show()
```

**Expected output:** A dashed line connecting the five data points (no markers).

**All linestyle options:**

| Value | What it looks like |
|-------|--------------------|
| `'solid'` or `'-'` | ——————— |
| `'dashed'` or `'--'` | – – – – – |
| `'dotted'` or `':'` | · · · · · |
| `'dashdot'` or `'-.'` | –·–·–·– |

### Line Colour

Use `color` (or `c`) to set the line's colour:

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [3, 7, 2, 9, 5]

plt.plot(x, y, color='hotpink')
plt.show()
```

**Expected output:** A solid hot-pink line connecting the data points.

> Matplotlib recognises over 140 named colours including `'tomato'`, `'steelblue'`, `'goldenrod'`, `'orchid'`, and many more.

### Line Width

Use `linewidth` (or `lw`) to control thickness:

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [3, 7, 2, 9, 5]

plt.plot(x, y, linewidth=8)
plt.show()
```

**Expected output:** A very thick solid line. The default line width is around 1.5.

### Combining All Line Style Options

You can combine marker, line style, colour, and width all in one `plt.plot()` call:

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [3, 7, 2, 9, 5]

plt.plot(
    x, y,
    marker='o',
    ms=10,
    mec='darkblue',
    mfc='skyblue',
    linestyle='dashed',
    color='steelblue',
    linewidth=2
)
plt.show()
```

**Expected output:** A dashed steel-blue line with sky-blue circles (dark-blue outline) at each data point.

> **Thinking prompt:** What would change if you set `linewidth=0`? Try it — the connecting line disappears and you only see the markers!

### Multiple Lines on One Chart

You can draw more than one line simply by calling `plt.plot()` multiple times before `plt.show()`:

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y1 = [3, 7, 2, 9, 5]
y2 = [1, 4, 6, 3, 8]

plt.plot(x, y1, marker='o', color='blue', label='Dataset A')
plt.plot(x, y2, marker='s', color='red', label='Dataset B')
plt.show()
```

**Expected output:** Two lines on the same chart — one blue with circles, one red with squares.

---

## Part 3 – Matplotlib Labels and Titles

### Why Do Labels Matter?

A chart without labels is like a map without place names — you can see the shapes but you don't know what they mean.

Labels include:
- A **title** at the top of the chart
- An **x-axis label** along the bottom
- A **y-axis label** along the left side
- A **legend** (when multiple lines are present) explaining what each line represents

> **Real-world relevance:** In a scientific paper, a business report, or a school project, an unlabelled chart will always be questioned. Labels are what transform raw data into a meaningful story.

### Adding a Title

Use `plt.title()`:

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [3, 7, 2, 9, 5]

plt.plot(x, y)
plt.title("My Daily Measurements")
plt.show()
```

**Expected output:** The same line chart, but now "My Daily Measurements" appears above it as a title.

### Adding Axis Labels

Use `plt.xlabel()` and `plt.ylabel()`:

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [3, 7, 2, 9, 5]

plt.plot(x, y, marker='o')
plt.title("Temperature Over 5 Days")
plt.xlabel("Day")
plt.ylabel("Temperature (°C)")
plt.show()
```

**Expected output:** The chart now has:
- "Temperature Over 5 Days" as the title
- "Day" written below the x-axis
- "Temperature (°C)" written vertically along the y-axis

### Customising Label Font Properties

You can control the font size, colour, and style of any label using the `fontdict` parameter:

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [3, 7, 2, 9, 5]

title_font = {
    'family': 'serif',
    'color': 'darkred',
    'size': 18,
    'weight': 'bold'
}

axis_font = {
    'family': 'serif',
    'color': 'steelblue',
    'size': 12
}

plt.plot(x, y, marker='o')
plt.title("Temperature Over 5 Days", fontdict=title_font)
plt.xlabel("Day", fontdict=axis_font)
plt.ylabel("Temperature (°C)", fontdict=axis_font)
plt.show()
```

**Expected output:** A styled chart with a large, bold, dark-red title and smaller steel-blue axis labels.

**`fontdict` key reference:**

| Key | What it controls | Example values |
|-----|-----------------|----------------|
| `'family'` | Font family | `'serif'`, `'sans-serif'`, `'monospace'` |
| `'color'` | Text colour | `'red'`, `'#333333'` |
| `'size'` | Font size in points | `10`, `14`, `20` |
| `'weight'` | Bold or normal | `'bold'`, `'normal'` |
| `'style'` | Italic or normal | `'italic'`, `'normal'` |

### Title Positioning

Use the `loc` parameter to align the title:

```python
plt.title("Left-aligned title", loc='left')
plt.title("Right-aligned title", loc='right')
plt.title("Centred title", loc='center')   # This is the default
```

### Adding a Legend

When you have multiple lines, a **legend** is a small box that tells the viewer which line is which. Use `label` in each `plt.plot()` call, then call `plt.legend()`:

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y1 = [3, 7, 2, 9, 5]
y2 = [1, 4, 6, 3, 8]

plt.plot(x, y1, label='City A Temperature')
plt.plot(x, y2, label='City B Temperature')
plt.title("Temperature Comparison")
plt.xlabel("Day")
plt.ylabel("Temperature (°C)")
plt.legend()
plt.show()
```

**Expected output:** A chart with two lines, a legend box showing which colour belongs to "City A Temperature" and "City B Temperature", plus a title and axis labels.

> **Common mistake:** Forgetting to call `plt.legend()`. If you add `label=` to your plots but never call `plt.legend()`, the legend will not appear.

---

## Part 4 – Matplotlib Grid

### What Is a Grid?

A **grid** is a set of light horizontal and/or vertical lines drawn behind the chart data to make it easier to read the value of each data point.

> **Analogy:** Think of graph paper. The faint squares in the background make it much easier to estimate values precisely. Matplotlib's grid does exactly the same thing for your digital charts.

### Adding a Basic Grid

Use `plt.grid()`:

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [3, 7, 2, 9, 5]

plt.plot(x, y, marker='o')
plt.title("Temperature Over 5 Days")
plt.xlabel("Day")
plt.ylabel("Temperature (°C)")
plt.grid()
plt.show()
```

**Expected output:** The same chart as before, but now faint grey gridlines appear horizontally and vertically across the chart area.

### Controlling Which Axis Shows Grid Lines

The `axis` parameter lets you show gridlines only on one axis:

```python
plt.grid(axis='x')    # vertical lines only (one per x value)
plt.grid(axis='y')    # horizontal lines only (one per y value)
plt.grid(axis='both') # both (this is the default)
```

**Example — horizontal gridlines only:**

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [3, 7, 2, 9, 5]

plt.plot(x, y, marker='o')
plt.grid(axis='y')
plt.show()
```

**Expected output:** Only horizontal gridlines appear across the chart (making it easy to read y-values).

### Styling the Grid

You can customise the grid's appearance using standard line parameters:

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [3, 7, 2, 9, 5]

plt.plot(x, y, marker='o', color='steelblue', linewidth=2)
plt.title("Temperature Over 5 Days")
plt.xlabel("Day")
plt.ylabel("Temperature (°C)")
plt.grid(
    color='grey',
    linestyle='--',
    linewidth=0.5
)
plt.show()
```

**Expected output:** A chart with thin dashed grey gridlines behind the data line.

**Grid styling parameters:**

| Parameter | What it does | Example |
|-----------|-------------|---------|
| `color` | Grid line colour | `'grey'`, `'#cccccc'` |
| `linestyle` | Grid line style | `'--'`, `':'`, `'-'` |
| `linewidth` | Grid line thickness | `0.5`, `1`, `2` |

> **Thinking prompt:** What happens if you set `linewidth=3` for the grid? It will overpower the data lines — always keep grid lines subtle (0.3–0.8) so they don't compete with your data.

> **Common mistake:** Placing `plt.grid()` after `plt.show()` — always call `plt.grid()` before `plt.show()`.

---

## Part 5 – Matplotlib Subplots

### What Are Subplots?

So far every example has shown **one chart per figure**. A **subplot** lets you place **multiple charts inside the same figure window**, arranged in rows and columns.

> **Real-world relevance:** A scientist comparing rainfall, temperature, and humidity in one report might display all three charts side-by-side so the reader can see relationships at a glance.

### The `plt.subplot()` Function

```python
plt.subplot(rows, columns, position)
```

- `rows` — how many rows of charts you want
- `columns` — how many columns of charts you want
- `position` — which slot to place the **current** chart in (counted left to right, top to bottom, starting at 1)

### Your First Subplot Example

Two charts side-by-side (1 row, 2 columns):

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y1 = [3, 7, 2, 9, 5]
y2 = [1, 4, 6, 3, 8]

# First chart: position 1 (left slot)
plt.subplot(1, 2, 1)
plt.plot(x, y1, marker='o', color='steelblue')
plt.title("Dataset A")

# Second chart: position 2 (right slot)
plt.subplot(1, 2, 2)
plt.plot(x, y2, marker='s', color='tomato')
plt.title("Dataset B")

plt.show()
```

**Expected output:** Two charts displayed side by side in one figure window.  
- Left chart: blue circles, titled "Dataset A"  
- Right chart: red squares, titled "Dataset B"

**Step-by-step explanation:**

1. `plt.subplot(1, 2, 1)` — create a layout of 1 row and 2 columns, and activate position 1
2. `plt.plot(...)` — draw the first chart into the active position
3. `plt.subplot(1, 2, 2)` — activate position 2 (right slot)
4. `plt.plot(...)` — draw the second chart into position 2
5. `plt.show()` — display the entire figure with both charts

### Two Charts Stacked Vertically

Two charts stacked (2 rows, 1 column):

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y1 = [3, 7, 2, 9, 5]
y2 = [1, 4, 6, 3, 8]

# Top chart
plt.subplot(2, 1, 1)
plt.plot(x, y1, marker='o', color='green')
plt.title("Top Chart")

# Bottom chart
plt.subplot(2, 1, 2)
plt.plot(x, y2, marker='^', color='purple')
plt.title("Bottom Chart")

plt.show()
```

**Expected output:** Two charts stacked vertically — green circles on top, purple triangles below.

### A 2×2 Grid of Four Charts

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]

plt.subplot(2, 2, 1)
plt.plot(x, [1, 4, 9, 16, 25], color='blue')
plt.title("Squares")

plt.subplot(2, 2, 2)
plt.plot(x, [1, 8, 27, 64, 125], color='orange')
plt.title("Cubes")

plt.subplot(2, 2, 3)
plt.plot(x, [2, 4, 8, 16, 32], color='green')
plt.title("Powers of 2")

plt.subplot(2, 2, 4)
plt.plot(x, [1, 3, 6, 10, 15], color='red')
plt.title("Triangular Numbers")

plt.suptitle("Number Sequences")
plt.show()
```

**Expected output:** Four charts in a 2×2 grid, each showing a different mathematical sequence. A super-title "Number Sequences" appears above all four.

**`plt.suptitle()`** adds a title to the **whole figure**, sitting above all individual chart titles.

### Subplot Position Numbering Explained

For a 2×2 grid:

```
┌──────────┬──────────┐
│ pos 1    │ pos 2    │
├──────────┼──────────┤
│ pos 3    │ pos 4    │
└──────────┴──────────┘
```

Positions are numbered **left to right, then top to bottom**.

> **Common mistake:** Using `plt.subplot(2, 2, 0)` — positions start at **1**, not 0. Using 0 raises an error.

> **Thinking prompt:** If you call `plt.subplot(3, 2, 5)`, which slot does that activate? Answer: Row 3, Column 1 (bottom-left).

---

## Part 6 – Matplotlib Scatter Charts

### What Is a Scatter Chart?

A **scatter chart** (also called a scatter plot) places individual dots on a chart — one dot per data point. There are **no connecting lines** between the dots.

Scatter charts are used to:
- Reveal whether two variables are **related** (correlated)
- Spot **clusters** — groups of similar data points
- Identify **outliers** — unusual values far from the rest

> **Real-world example:** A biologist measuring the relationship between rainfall (x) and plant height (y) would use a scatter chart to see if taller plants grow where there is more rain.

> **Line chart vs scatter chart:**  
> Use a **line chart** when data is ordered over time (days, months, steps).  
> Use a **scatter chart** when two independent measurements are compared with no time ordering.

### Your First Scatter Chart

```python
import matplotlib.pyplot as plt

x = [5, 7, 8, 7, 2, 17, 2, 9, 4, 11, 12, 9, 6]
y = [99, 86, 87, 88, 111, 86, 103, 87, 94, 78, 77, 85, 86]

plt.scatter(x, y)
plt.title("Car Age vs Average Speed")
plt.xlabel("Age of Car (years)")
plt.ylabel("Average Speed (km/h)")
plt.show()
```

**Expected output:** A scatter chart with 13 individual dots, showing the age of cars on the x-axis and their average speed on the y-axis.

**Line-by-line explanation:**

| Line | What it does |
|------|-------------|
| `x = [...]` | Car ages in years |
| `y = [...]` | Average speeds in km/h |
| `plt.scatter(x, y)` | Draws one dot for each (x, y) pair |
| `plt.title(...)` | Adds a title |
| `plt.xlabel(...)` | Labels the x-axis |
| `plt.ylabel(...)` | Labels the y-axis |

### Customising Scatter Chart Colour and Size

Use `color` to change dot colour and `s` to change dot **size**:

```python
import matplotlib.pyplot as plt

x = [5, 7, 8, 7, 2, 17, 2, 9, 4, 11, 12, 9, 6]
y = [99, 86, 87, 88, 111, 86, 103, 87, 94, 78, 77, 85, 86]

plt.scatter(x, y, color='hotpink', s=100)
plt.title("Car Age vs Average Speed")
plt.xlabel("Age of Car (years)")
plt.ylabel("Average Speed (km/h)")
plt.show()
```

**Expected output:** Same scatter chart but with larger pink dots.

### Using Different Colours Per Dot

Pass a **list of colours** (one per data point) to colour each dot differently:

```python
import matplotlib.pyplot as plt

x = [5, 7, 8, 7, 2, 17]
y = [99, 86, 87, 88, 111, 86]

colours = ['red', 'green', 'blue', 'orange', 'purple', 'brown']

plt.scatter(x, y, c=colours, s=100)
plt.title("Individual Car Speeds")
plt.show()
```

**Expected output:** Six differently coloured dots — one red, one green, one blue, etc.

> Notice that for scatter charts, the colour parameter shorthand is `c=` rather than `color=` when passing a list.

### Using a Colour Map

A **colour map** (or cmap) automatically assigns colours from a gradient based on the value of another variable. This is useful for encoding a third dimension of data visually:

```python
import matplotlib.pyplot as plt

x = [5, 7, 8, 7, 2, 17, 2, 9, 4, 11, 12, 9, 6]
y = [99, 86, 87, 88, 111, 86, 103, 87, 94, 78, 77, 85, 86]
# Use the y-values to colour the dots
colors = y

plt.scatter(x, y, c=colors, cmap='viridis', s=100)
plt.colorbar()
plt.title("Car Age vs Speed (colour = speed)")
plt.xlabel("Age (years)")
plt.ylabel("Speed (km/h)")
plt.show()
```

**Expected output:** Dots coloured along a purple-yellow gradient — lower speeds in purple, higher speeds in yellow — plus a colour bar on the right showing the scale.

**Popular colour maps:**

| Name | Gradient description |
|------|---------------------|
| `'viridis'` | Purple → blue → green → yellow |
| `'plasma'` | Purple → pink → yellow |
| `'inferno'` | Black → red → yellow |
| `'coolwarm'` | Blue → white → red |
| `'Greens'` | Light green → dark green |

### Controlling Dot Transparency with Alpha

Use `alpha` (a value between 0.0 and 1.0) to make dots semi-transparent. This is very useful when many dots overlap:

```python
import matplotlib.pyplot as plt

x = [5, 7, 8, 7, 2, 17, 2, 9, 4, 11, 12, 9, 6]
y = [99, 86, 87, 88, 111, 86, 103, 87, 94, 78, 77, 85, 86]

plt.scatter(x, y, color='steelblue', s=200, alpha=0.5)
plt.show()
```

**Expected output:** Large semi-transparent dots where overlapping areas appear darker.

- `alpha=1.0` — fully opaque (default)
- `alpha=0.5` — 50% transparent
- `alpha=0.0` — fully invisible

### Two Datasets on One Scatter Chart

```python
import matplotlib.pyplot as plt

# Dataset 1: Cars from 2010–2015
x1 = [5, 7, 8, 7, 2, 17, 2, 9, 4]
y1 = [99, 86, 87, 88, 111, 86, 103, 87, 94]

# Dataset 2: Cars from 2016–2021
x2 = [2, 3, 6, 12, 8, 5]
y2 = [105, 100, 98, 90, 103, 110]

plt.scatter(x1, y1, color='blue', label='2010–2015', alpha=0.7)
plt.scatter(x2, y2, color='red', label='2016–2021', alpha=0.7)
plt.title("Car Age vs Speed by Era")
plt.xlabel("Age (years)")
plt.ylabel("Speed (km/h)")
plt.legend()
plt.show()
```

**Expected output:** A scatter chart with blue dots for older cars and red dots for newer cars, with a legend identifying each group.

---

## Part 7 – Matplotlib Bar Charts

### What Is a Bar Chart?

A **bar chart** uses rectangular bars to compare values across different **categories**.  
The length (or height) of each bar represents the value for that category.

> **Real-world examples:**
> - Comparing monthly sales figures across 12 months
> - Comparing the number of students enrolled in different university courses
> - Comparing rainfall amounts in different cities

> **Bar chart vs line chart:**  
> Use a **line chart** when showing change **over time** with a continuous connection.  
> Use a **bar chart** when comparing **discrete categories** that don't have a natural connection.

### Your First Bar Chart

```python
import matplotlib.pyplot as plt

categories = ["Apples", "Bananas", "Cherries", "Dates"]
values     = [450,      380,       210,         310]

plt.bar(categories, values)
plt.title("Fruit Sales This Month")
plt.xlabel("Fruit")
plt.ylabel("Units Sold")
plt.show()
```

**Expected output:** Four vertical bars — one for each fruit — with heights proportional to the sales values.

**Line-by-line explanation:**

| Line | What it does |
|------|-------------|
| `categories` | The x-axis labels for each bar |
| `values` | The height of each bar |
| `plt.bar(categories, values)` | Draws the bar chart |
| `plt.title(...)` | Adds a title |
| `plt.xlabel(...)` | Labels the x-axis (category axis) |
| `plt.ylabel(...)` | Labels the y-axis (value axis) |

### Customising Bar Colour

Pass a single colour for all bars, or a list of colours:

```python
import matplotlib.pyplot as plt

categories = ["Apples", "Bananas", "Cherries", "Dates"]
values     = [450, 380, 210, 310]

# All bars the same colour
plt.bar(categories, values, color='steelblue')
plt.title("Fruit Sales")
plt.show()
```

**Expected output:** All four bars in steel blue.

```python
import matplotlib.pyplot as plt

categories = ["Apples", "Bananas", "Cherries", "Dates"]
values     = [450, 380, 210, 310]

# Each bar a different colour
colours = ['red', 'yellow', 'crimson', 'saddlebrown']
plt.bar(categories, values, color=colours)
plt.title("Fruit Sales")
plt.show()
```

**Expected output:** Red bar for Apples, yellow for Bananas, crimson for Cherries, brown for Dates.

### Controlling Bar Width

The default bar width is `0.8`. Use `width` to change it:

```python
import matplotlib.pyplot as plt

categories = ["Apples", "Bananas", "Cherries", "Dates"]
values     = [450, 380, 210, 310]

plt.bar(categories, values, width=0.4)
plt.title("Narrower Bars")
plt.show()
```

**Expected output:** Narrower bars with more space between them.

- `width=1.0` — bars touch each other
- `width=0.8` — default (small gap between bars)
- `width=0.4` — narrow bars with larger gaps

### Horizontal Bar Charts

Swap `plt.bar()` for `plt.barh()` to draw horizontal bars:

```python
import matplotlib.pyplot as plt

categories = ["Apples", "Bananas", "Cherries", "Dates"]
values     = [450, 380, 210, 310]

plt.barh(categories, values, color='darkorange')
plt.title("Fruit Sales — Horizontal")
plt.xlabel("Units Sold")
plt.ylabel("Fruit")
plt.show()
```

**Expected output:** Four horizontal bars extending from left to right, one per fruit.

> **When to use horizontal bars:**  
> Horizontal bars are especially useful when you have many categories or long category names — they fit much better along the y-axis without overlapping.

### Adding a Grid to a Bar Chart

```python
import matplotlib.pyplot as plt

categories = ["Apples", "Bananas", "Cherries", "Dates"]
values     = [450, 380, 210, 310]

plt.bar(categories, values, color='steelblue')
plt.title("Fruit Sales")
plt.xlabel("Fruit")
plt.ylabel("Units Sold")
plt.grid(axis='y', linestyle='--', linewidth=0.7, color='grey')
plt.show()
```

**Expected output:** A bar chart with horizontal dashed grey gridlines, making it easy to read the exact height of each bar.

> **Best practice:** For bar charts, add `axis='y'` to the grid so only horizontal lines appear. Vertical gridlines on a bar chart are usually distracting.

---

## Guided Practice Exercises

### Exercise 1 – Weather Line Chart with Markers and Labels

**Scenario:** You are a meteorologist tracking the daily maximum temperature (°C) in a city for one week.

**Data:**

| Day | Temperature (°C) |
|-----|-----------------|
| Mon | 18 |
| Tue | 21 |
| Wed | 19 |
| Thu | 25 |
| Fri | 27 |
| Sat | 24 |
| Sun | 22 |

**Objective:** Create a fully labelled line chart with markers, a styled line, a grid, and appropriate labels.

**Steps:**

1. Create a list for days and a list for temperatures
2. Call `plt.plot()` with circle markers and a blue dashed line
3. Add a title: `"Weekly Maximum Temperatures"`
4. Add x-axis label: `"Day of Week"`
5. Add y-axis label: `"Temperature (°C)"`
6. Add a grid with only horizontal lines
7. Display the chart

**Expected solution:**

```python
import matplotlib.pyplot as plt

days = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
temps = [18, 21, 19, 25, 27, 24, 22]

plt.plot(days, temps, marker='o', linestyle='dashed', color='steelblue', linewidth=2)
plt.title("Weekly Maximum Temperatures", fontsize=14)
plt.xlabel("Day of Week")
plt.ylabel("Temperature (°C)")
plt.grid(axis='y', linestyle='--', linewidth=0.6, color='grey')
plt.show()
```

**Expected output:** A styled blue dashed line with circles at each day's temperature, horizontal gridlines, and full labels.

**Self-check questions:**
- Can you identify the hottest day from the chart?
- What would the chart look like if you added `mfc='red'` to highlight the data points?
- What if you changed `axis='y'` to `axis='both'`?

**What-if challenge:** Add a second line showing the minimum temperatures for the same week: `[10, 12, 11, 15, 16, 14, 13]`

---

### Exercise 2 – Student Score Scatter Chart

**Scenario:** A teacher wants to see if the number of hours studied relates to exam scores.

**Data:**

| Hours studied | Score (%) |
|--------------|-----------|
| 1 | 55 |
| 2 | 60 |
| 3 | 65 |
| 2.5 | 58 |
| 5 | 80 |
| 4 | 75 |
| 6 | 85 |
| 7 | 90 |
| 5.5 | 82 |
| 3.5 | 70 |

**Objective:** Create a scatter chart with colour-mapped dots showing the score, and a colour bar.

**Steps:**

1. Create `hours` and `scores` lists
2. Use `plt.scatter()` with `c=scores`, `cmap='YlOrRd'`, `s=150`, `alpha=0.8`
3. Add a colour bar
4. Add title, x-label, y-label
5. Add a horizontal grid

**Expected solution:**

```python
import matplotlib.pyplot as plt

hours  = [1, 2, 3, 2.5, 5, 4, 6, 7, 5.5, 3.5]
scores = [55, 60, 65, 58, 80, 75, 85, 90, 82, 70]

plt.scatter(hours, scores, c=scores, cmap='YlOrRd', s=150, alpha=0.8)
plt.colorbar(label='Score (%)')
plt.title("Study Hours vs Exam Score")
plt.xlabel("Hours Studied")
plt.ylabel("Exam Score (%)")
plt.grid(axis='y', linestyle='--', linewidth=0.5, color='grey')
plt.show()
```

**Expected output:** A scatter chart where dots go from yellow (lower scores) to dark red (higher scores), with a colour bar on the right.

**Self-check questions:**
- Does the chart suggest a positive relationship (more hours → higher score)?
- What would `cmap='Blues'` look like compared to `'YlOrRd'`?

---

### Exercise 3 – Department Budget Bar Chart

**Scenario:** A company wants to compare its annual budget allocation across five departments.

**Data:**

| Department | Budget (£ thousands) |
|-----------|---------------------|
| Engineering | 850 |
| Marketing | 420 |
| Operations | 630 |
| HR | 200 |
| R&D | 710 |

**Objective:** Create a horizontal bar chart with distinct colours for each department, a grid on the value axis, and full labels.

**Expected solution:**

```python
import matplotlib.pyplot as plt

departments = ["Engineering", "Marketing", "Operations", "HR", "R&D"]
budgets = [850, 420, 630, 200, 710]
colours = ['steelblue', 'tomato', 'mediumseagreen', 'gold', 'mediumpurple']

plt.barh(departments, budgets, color=colours)
plt.title("Annual Budget by Department", fontsize=14)
plt.xlabel("Budget (£ thousands)")
plt.ylabel("Department")
plt.grid(axis='x', linestyle='--', linewidth=0.6, color='grey')
plt.show()
```

**Expected output:** Five horizontal bars of different colours, with dashed vertical gridlines behind them, making budget values easy to read.

---

### Exercise 4 – Subplot Comparison Dashboard

**Scenario:** You want a single figure showing three related charts — daily sales as a line chart, product category sales as a bar chart, and customer age vs purchase value as a scatter chart.

**Objective:** Build a 1×3 subplot layout with three different chart types.

**Expected solution:**

```python
import matplotlib.pyplot as plt

# Data
days   = [1, 2, 3, 4, 5, 6, 7]
sales  = [120, 145, 132, 178, 155, 190, 168]

categories = ["Electronics", "Clothing", "Food", "Books"]
cat_sales  = [450, 320, 210, 140]

ages    = [22, 35, 41, 28, 55, 48, 33, 29, 62, 44]
amounts = [150, 320, 280, 190, 450, 370, 220, 175, 500, 310]

# Create figure
plt.figure(figsize=(15, 4))

# Chart 1: Line chart
plt.subplot(1, 3, 1)
plt.plot(days, sales, marker='o', color='steelblue', linewidth=2)
plt.title("Daily Sales")
plt.xlabel("Day")
plt.ylabel("Sales (£)")
plt.grid(axis='y', linestyle='--', linewidth=0.5)

# Chart 2: Bar chart
plt.subplot(1, 3, 2)
plt.bar(categories, cat_sales, color=['steelblue', 'tomato', 'mediumseagreen', 'gold'])
plt.title("Sales by Category")
plt.xlabel("Category")
plt.ylabel("Sales (£)")
plt.grid(axis='y', linestyle='--', linewidth=0.5)

# Chart 3: Scatter chart
plt.subplot(1, 3, 3)
plt.scatter(ages, amounts, c=amounts, cmap='viridis', s=80, alpha=0.8)
plt.title("Age vs Purchase Value")
plt.xlabel("Customer Age")
plt.ylabel("Purchase (£)")
plt.grid(linestyle='--', linewidth=0.4)

plt.suptitle("Sales Dashboard — Week 1", fontsize=16, fontweight='bold')
plt.tight_layout()
plt.show()
```

**Expected output:** A single figure containing three charts side-by-side forming a mini dashboard, with an overall title.

> `plt.tight_layout()` — automatically adjusts spacing between subplots so labels and titles don't overlap. Always use it when building subplots.

---

## Mini Project — Climate Data Visualisation Dashboard

### Project Overview

You are a data analyst at a weather research institute. Your manager has asked you to produce a visual dashboard from one month of climate data, showing:

1. Daily temperatures as a line chart (with markers)
2. Daily rainfall as a bar chart
3. Temperature vs humidity as a scatter chart
4. All three in one figure using subplots

### Stage 1 – Setup and Data

```python
import matplotlib.pyplot as plt

# 30 days of simulated climate data
days = list(range(1, 31))

temperature = [
    15, 17, 16, 18, 20, 22, 21, 19, 18, 23,
    25, 24, 26, 28, 27, 25, 22, 20, 19, 21,
    23, 24, 26, 28, 29, 27, 25, 23, 21, 20
]

rainfall_mm = [
    5, 0, 2, 8, 1, 0, 0, 3, 10, 0,
    0, 1, 0, 0, 2, 5, 7, 3, 0, 0,
    1, 0, 0, 0, 2, 4, 6, 2, 0, 1
]

humidity = [
    70, 65, 68, 75, 60, 55, 58, 72, 80, 54,
    50, 52, 48, 45, 58, 68, 75, 72, 65, 60,
    62, 55, 50, 48, 60, 70, 78, 72, 63, 58
]
```

**Milestone output:** Data is ready. No errors when you run this block.

### Stage 2 – Temperature Line Chart

```python
plt.figure(figsize=(16, 12))

# --- Chart 1: Temperature ---
plt.subplot(2, 2, 1)
plt.plot(
    days, temperature,
    marker='o', ms=5,
    color='tomato', linewidth=1.8
)
plt.title("Daily Temperature — July", fontsize=12)
plt.xlabel("Day of Month")
plt.ylabel("Temperature (°C)")
plt.grid(axis='y', linestyle='--', linewidth=0.5, color='grey')
```

**Milestone output:** Top-left chart shows a red temperature line with circles.

### Stage 3 – Rainfall Bar Chart

```python
# --- Chart 2: Rainfall ---
plt.subplot(2, 2, 2)
bar_colours = ['steelblue' if r > 0 else 'lightgrey' for r in rainfall_mm]
plt.bar(days, rainfall_mm, color=bar_colours)
plt.title("Daily Rainfall — July", fontsize=12)
plt.xlabel("Day of Month")
plt.ylabel("Rainfall (mm)")
plt.grid(axis='y', linestyle='--', linewidth=0.5, color='grey')
```

> **New concept:** `['steelblue' if r > 0 else 'lightgrey' for r in rainfall_mm]`  
> This is a **list comprehension** — a compact way to build a list. For each rainfall value `r`, if it is greater than 0 the colour is `'steelblue'`, otherwise `'lightgrey'`. Rainy days appear blue; dry days appear grey.

**Milestone output:** Top-right chart shows blue bars on rainy days and grey bars on dry days.

### Stage 4 – Temperature vs Humidity Scatter Chart

```python
# --- Chart 3: Temperature vs Humidity ---
plt.subplot(2, 2, 3)
plt.scatter(
    temperature, humidity,
    c=temperature, cmap='RdYlGn_r',
    s=80, alpha=0.8
)
plt.colorbar(label='Temperature (°C)')
plt.title("Temperature vs Humidity — July", fontsize=12)
plt.xlabel("Temperature (°C)")
plt.ylabel("Humidity (%)")
plt.grid(linestyle='--', linewidth=0.4, color='grey')
```

**Milestone output:** Bottom-left scatter chart with dots coloured from green (cool) to red (warm), plus a colour bar.

### Stage 5 – Final Assembly and Display

```python
# --- Overall title and layout ---
plt.suptitle(
    "Climate Dashboard — July 2024",
    fontsize=16,
    fontweight='bold',
    y=1.01
)
plt.tight_layout()
plt.show()
```

**Final output:** A professional-looking 2×2 figure with:
- Temperature line chart (top-left)
- Rainfall bar chart (top-right)
- Temperature vs humidity scatter chart (bottom-left)
- An overall dashboard title

### Stage 6 – Reflection

Answer these questions after completing the project:

1. On which days was rainfall highest? Does high rainfall seem to coincide with lower or higher temperatures?
2. Does the scatter chart suggest that hotter days tend to be drier (lower humidity)?
3. What would you change to make the dashboard suitable for a formal weather report?
4. How would you add a fourth chart (e.g., a line chart of humidity over time) to complete the 2×2 grid?

### Optional Extensions

- Add data labels (text showing the exact value) above each bar in the rainfall chart
- Use `plt.axhline(y=25, color='red', linestyle='--')` to add a horizontal "heatwave threshold" line to the temperature chart
- Try `plt.style.use('seaborn-v0_8')` at the top to apply a professional chart style automatically

---

## Common Beginner Mistakes

### Mistake 1 — Calling `plt.show()` Too Early

```python
# WRONG
plt.plot(x, y)
plt.show()          # Chart displays here with nothing else
plt.title("My Chart")  # This line has no effect — chart already shown

# CORRECT
plt.plot(x, y)
plt.title("My Chart")  # Add everything first
plt.show()             # Then display
```

### Mistake 2 — Mismatched List Lengths

```python
# WRONG — x has 5 values, y has 4 values
x = [1, 2, 3, 4, 5]
y = [10, 20, 30, 40]
plt.plot(x, y)  # Raises ValueError

# CORRECT
x = [1, 2, 3, 4, 5]
y = [10, 20, 30, 40, 50]
plt.plot(x, y)
```

**Rule:** `x` and `y` lists must always have exactly the same number of values.

### Mistake 3 — Subplot Position Starting at 0

```python
# WRONG — positions start at 1, not 0
plt.subplot(1, 2, 0)  # Raises ValueError

# CORRECT
plt.subplot(1, 2, 1)
```

### Mistake 4 — Forgetting `plt.legend()` After Adding Labels

```python
# WRONG — labels added but legend never shown
plt.plot(x, y1, label='Dataset A')
plt.plot(x, y2, label='Dataset B')
plt.show()  # No legend visible

# CORRECT
plt.plot(x, y1, label='Dataset A')
plt.plot(x, y2, label='Dataset B')
plt.legend()  # This line makes the legend appear
plt.show()
```

### Mistake 5 — Using `color` Instead of `c` in Scatter for Lists

```python
# WRONG — passing a list to color= in scatter
plt.scatter(x, y, color=['red', 'blue', 'green'])  # May raise an error

# CORRECT — use c= when passing a list
plt.scatter(x, y, c=['red', 'blue', 'green'])
```

### Mistake 6 — Grid Lines Obscuring Data

```python
# Poor practice — thick dark grid lines overpower the data
plt.grid(color='black', linewidth=3)

# Better practice — thin, light, subtle grid lines
plt.grid(color='grey', linestyle='--', linewidth=0.5)
```

### Mistake 7 — Overlapping Subplot Labels

```python
# WRONG — labels from adjacent subplots overlap
plt.subplot(1, 2, 1)
plt.plot(...)
plt.subplot(1, 2, 2)
plt.plot(...)
plt.show()  # Labels may overlap

# CORRECT — add tight_layout before show
plt.tight_layout()
plt.show()
```

### Mistake 8 — Using Bar Width Greater Than 1

```python
# WRONG — bars overflow into adjacent positions
plt.bar(categories, values, width=1.5)

# CORRECT — keep width at or below 1.0
plt.bar(categories, values, width=0.8)
```

---

## Reflection Questions

1. What is the difference between a **marker** and a **line** in a Matplotlib chart? When would you want to show markers without a line?

2. A classmate says "I always use line charts for everything — it's simpler." What would you tell them about when a **scatter chart** or **bar chart** is a better choice?

3. You are making a chart for a printed black-and-white report. Which of the line style options (`solid`, `dashed`, `dotted`, `dashdot`) would be most useful, and why?

4. Why is `plt.tight_layout()` especially important when using subplots?

5. In the climate dashboard project, the rainfall bar colours were set conditionally: blue for rainy days, grey for dry days. How does this design choice improve the reader's experience compared to all bars being the same colour?

6. What are three things a chart must have to be considered properly labelled for a professional audience?

7. If your scatter chart shows dots clustered in a diagonal line going from bottom-left to top-right, what does that suggest about the relationship between x and y?

---

## Completion Checklist

Before moving to the next lesson, make sure you can confidently tick every item below:

- [ ] I understand what a **marker** is and can add one to a line chart using `marker=`
- [ ] I can change a marker's **size**, **face colour**, and **edge colour** using `ms=`, `mfc=`, and `mec=`
- [ ] I can use the **format string shorthand** (e.g. `'r*--'`) to set colour, marker, and line style at once
- [ ] I can change the **line style** using `linestyle=` or its shorthand `ls=`
- [ ] I can change the **line colour** using `color=` or `c=`
- [ ] I can change the **line width** using `linewidth=` or `lw=`
- [ ] I can add a **title** using `plt.title()` and customise it with `fontdict=`
- [ ] I can add **x and y axis labels** using `plt.xlabel()` and `plt.ylabel()`
- [ ] I can add a **legend** using `label=` in plots and `plt.legend()`
- [ ] I can add a **grid** using `plt.grid()` and control which axis shows gridlines
- [ ] I can control **grid line style, colour, and width**
- [ ] I understand the **subplot position numbering system** and can place charts in a grid layout
- [ ] I can use `plt.suptitle()` for a whole-figure title and `plt.tight_layout()` to fix spacing
- [ ] I can create a **scatter chart** using `plt.scatter()`
- [ ] I can use a **colour map** with scatter charts and add a `plt.colorbar()`
- [ ] I can control scatter dot **size** (`s=`) and **transparency** (`alpha=`)
- [ ] I can create a **vertical bar chart** using `plt.bar()`
- [ ] I can create a **horizontal bar chart** using `plt.barh()`
- [ ] I can control **bar width** and **bar colour** (single colour or per-bar list)
- [ ] I have completed at least two guided exercises
- [ ] I have completed the climate dashboard mini project

---

## Lesson Summary

In this lesson you covered seven key Matplotlib topics, progressing from styling individual chart elements all the way to building multi-chart dashboards.

**Markers** let you mark the exact location of each data point on a line chart. You can choose from dozens of shapes and fully customise their size, fill colour, and edge colour.

**Line styling** gives you control over how connecting lines look — their style (solid, dashed, dotted, dash-dot), their colour (named, hex, or RGB), and their width.

**Labels** transform a raw chart into a communication tool. Every chart should have a descriptive title, labelled x and y axes, and a legend when multiple data series are present.

**Grids** add faint reference lines behind your data, making values easier to read. Always keep grid lines thin and subtle so they support rather than compete with your data.

**Subplots** allow you to place multiple charts inside a single figure using the `plt.subplot(rows, columns, position)` system. Use `plt.suptitle()` for a shared title and `plt.tight_layout()` to prevent label overlaps.

**Scatter charts** (`plt.scatter()`) plot individual dots with no connecting lines, making them ideal for revealing correlations, clusters, and outliers between two variables. Colour maps and transparency add a third dimension to the story.

**Bar charts** (`plt.bar()` and `plt.barh()`) compare values across discrete categories. Vertical bars are standard; horizontal bars work better with many categories or long labels.

Together these tools form a complete beginner toolkit for data visualisation in Python — skills directly applicable to data science, scientific research, business analytics, engineering, education, and beyond.

---

*End of Lesson 32*
