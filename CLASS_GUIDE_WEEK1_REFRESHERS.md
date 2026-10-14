# Week 1 Refresher Notebooks: Classroom Guide

This guide explains the first three Jupyter notebooks in a way suitable for students beginning their machine-learning journey.

## How the notebooks fit together

The notebooks introduce three foundational Python libraries:

1. **NumPy** stores and calculates with numerical data.
2. **Pandas** organises data into labelled tables.
3. **Matplotlib** turns data into visual explanations.

A useful analogy is:

> NumPy is the mathematical engine, Pandas is the spreadsheet, and Matplotlib is the drawing board.

Run the notebooks in this order:

1. `1_a_NumpyRefresher.ipynb`
2. `1_b_PandasRefresher.ipynb`
3. `1_c_MatplotlibRefresher.ipynb`

For classroom delivery, run one cell at a time. Ask students to predict the result before executing each cell.

---

# 1. NumPy Refresher

Notebook: [1_a_NumpyRefresher.ipynb](./1_a_NumpyRefresher.ipynb)

## Learning purpose

NumPy introduces arrays: efficient structures for storing and processing numbers.

Machine-learning datasets ultimately become collections of numbers. For example:

- Each row might represent a student.
- Columns might contain study hours, attendance and assessment results.
- The complete rectangular collection is a two-dimensional array.

Many Python data-science libraries, including Pandas, SciPy and scikit-learn, depend on NumPy.

## Step 1: Import NumPy

```python
import numpy as np
```

`np` is the conventional short name for NumPy. It lets us write `np.array()` instead of `numpy.array()`.

### Teaching point

Importing a library makes its additional tools available to the current notebook session.

## Step 2: Compare a Python list with a NumPy array

```python
my_list = [1, 2, 3]
my_array = np.array([1, 2, 3])
```

The two objects look similar, but they serve different purposes:

- A Python list is a general-purpose container.
- A NumPy array is designed for efficient numerical calculation.
- NumPy can perform one operation across an entire array.
- NumPy arrays can represent data in one, two or more dimensions.

The notebook uses `type()` to demonstrate the difference:

```python
type(my_list)   # list
type(my_array)  # numpy.ndarray
```

### Class discussion

Ask students why a machine-learning library might prefer a predictable numerical structure over a general-purpose list.

## Step 3: Understand vectors and matrices

A one-dimensional array can represent a vector:

```python
np.array([1, 2, 3])
```

A two-dimensional array can represent a matrix:

```python
np.array([
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
])
```

Beginner-friendly definitions:

- A **vector** is one line of numbers.
- A **matrix** is a rectangular table of numbers.
- An **array** is NumPy's general structure for this data.

## Step 4: Generate sequences with `arange`

```python
np.arange(10, 20)
np.arange(10, 20, 2)
```

The arguments represent:

1. Starting value.
2. Stopping value.
3. Optional step size.

The start is included, but the stop is excluded. Therefore:

```python
np.arange(10, 20, 2)
```

produces `10, 12, 14, 16, 18`.

## Step 5: Create arrays of zeros and ones

```python
np.zeros(5)
np.zeros((3, 4))
np.ones(5)
np.ones((3, 4))
```

`(3, 4)` means three rows and four columns.

These functions are useful for:

- Initial model parameters.
- Placeholder values.
- Preparing storage for calculated results.
- Creating masks and flags.

## Step 6: Generate evenly spaced values with `linspace`

```python
np.linspace(0, 15, 4)
```

This asks NumPy for four evenly spaced values from 0 through 15.

Important distinction:

- `arange` normally controls the step size.
- `linspace` controls the number of values.

`linspace` includes the endpoint by default.

## Step 7: Create an identity matrix

```python
np.eye(5)
```

An identity matrix has:

- Ones on its main diagonal.
- Zeros everywhere else.

It behaves like the number 1 in matrix multiplication and is important in linear algebra.

## Step 8: Generate random numbers

The notebook demonstrates:

```python
np.random.rand(...)
np.random.randn(...)
np.random.randint(...)
```

Their purposes differ:

- `rand` generates decimal values uniformly between 0 and 1.
- `randn` generates values from a standard normal distribution centred around zero.
- `randint` generates random integers within a range.

Randomness is used in ML for:

- Initial model weights.
- Data sampling.
- Simulated datasets.
- Train/test splitting.
- Randomised algorithms.

## Step 9: Make randomness reproducible

```python
np.random.seed(15)
```

A seed makes a sequence of random values repeatable.

This is important because:

- Every student can receive the same result.
- Experiments can be repeated.
- Unexpected changes are easier to investigate.

The values are still produced by a random-number algorithm, but the algorithm begins from the same starting state.

## Step 10: Reshape an array

```python
arr = np.arange(20)
arr.reshape(4, 5)
```

The same 20 values are reorganised into four rows and five columns.

Reshaping does not create or remove values. The new dimensions must contain the same total number:

- `4 x 5 = 20` works.
- `2 x 10 = 20` works.
- `3 x 5 = 15` does not work.

Reshaping is common when preparing input for machine-learning models.

## Step 11: Find minimums and maximums

```python
ranarr.max()
ranarr.argmax()
ranarr.min()
ranarr.argmin()
```

The distinction is:

- `max()` returns the largest value.
- `argmax()` returns the position of the largest value.
- `min()` returns the smallest value.
- `argmin()` returns the position of the smallest value.

ML classifiers commonly use `argmax` to select the class with the highest predicted score.

## Step 12: Inspect shape and data type

```python
arr.shape
arr.dtype
```

- `shape` describes the dimensions.
- `dtype` describes the type of values stored in the array.

Examples:

- `(20,)` means a one-dimensional array containing 20 values.
- `(10, 2)` means ten rows and two columns.
- Integer arrays may use a type such as `int64`.
- Decimal arrays normally use a floating-point type.

## NumPy takeaway

> NumPy gives us fast, structured numerical arrays: the basic language in which machine-learning algorithms receive and process data.

---

# 2. Pandas Refresher

Notebook: [1_b_PandasRefresher.ipynb](./1_b_PandasRefresher.ipynb)

Dataset: [data/matildas.csv](./data/matildas.csv)

## Learning purpose

Pandas introduces the DataFrame: a labelled table in which:

- Rows represent observations or records.
- Columns represent variables or features.
- Labels make the data easier to understand.

The notebook first creates a small table and then loads a real dataset describing matches played by the Matildas, Australia's women's national football team.

## Step 1: Import NumPy and Pandas

```python
import numpy as np
import pandas as pd
```

`pd` is the conventional short name for Pandas.

## Step 2: Create repeatable example data

```python
np.random.seed(101)
data = np.random.randint(0, 50, (5, 4))
```

This creates a five-row, four-column NumPy array containing random integers.

The fixed seed ensures everyone receives the same example.

## Step 3: Create meaningful labels

```python
rows = ['SYD', 'MEL', 'CAN', 'BRI', 'PER']
columns = ['JAN', 'FEB', 'MAR', 'APR']
```

The notebook creates DataFrames in stages:

```python
pd.DataFrame(data=data)
pd.DataFrame(data=data, index=rows)
pd.DataFrame(data=data, columns=columns)
pd.DataFrame(data=data, index=rows, columns=columns)
```

This shows the value of labels. Instead of referring to "row 0, column 2", we can reason about "Sydney in March".

### Teaching point

> A NumPy array stores the values; a Pandas DataFrame adds labels and table operations around those values.

## Step 4: Load a CSV dataset

```python
df = pd.read_csv('data/matildas.csv')
```

A CSV file is a text representation of a table. Pandas reads it into a DataFrame named `df`.

The relative path means:

1. Begin in the repository folder.
2. Open the `data` folder.
3. Read `matildas.csv`.

The repository folder must be opened correctly in VS Code for this path to work reliably.

## Step 5: Inspect the dataset

The notebook uses:

```python
df
df.columns
df.index
df.head(5)
df.tail(5)
df.info()
len(df)
```

Each instruction answers a different question:

- `df`: What does the table look like?
- `columns`: Which variables are available?
- `index`: How are rows currently labelled?
- `head()`: What do the first records look like?
- `tail()`: What do the final records look like?
- `info()`: What are the data types, counts and missing-value patterns?
- `len(df)`: How many rows are present?

This is the beginning of **exploratory data analysis**, usually one of the first stages of an ML project.

## Step 6: Generate descriptive statistics

```python
df.describe()
df.describe().transpose()
```

`describe()` summarises numerical columns using values such as:

- Count.
- Mean.
- Standard deviation.
- Minimum.
- Quartiles.
- Maximum.

The transpose changes rows into columns and columns into rows, which can make a wide summary easier to read.

Descriptive statistics can reveal:

- Unexpected ranges.
- Missing values.
- Possible outliers.
- Features measured on very different scales.

## Step 7: Select columns

A single column:

```python
df['attendance']
```

This returns a Pandas `Series`.

Multiple columns:

```python
df[['attendance', 'goals_scored']]
```

This returns another DataFrame.

The inner brackets form a Python list containing the requested column names.

## Step 8: Create new features

```python
df['goal_difference'] = (
    df['goals_scored'] - df['goals_conceded']
)

df['total_goals'] = (
    df['goals_scored'] + df['goals_conceded']
)
```

This is a simple example of **feature engineering**:

- Goal difference describes the winning or losing margin.
- Total goals describes how high-scoring the match was.

Feature engineering creates potentially useful information from existing columns.

## Step 9: Apply NumPy operations to Pandas data

```python
df['attendance_thousands'] = np.round(
    df['attendance'] / 1000,
    2
)
```

This is a vectorised calculation:

1. Divide every attendance value by 1,000.
2. Round every result to two decimal places.
3. Store the results in a new column.

No manual loop is needed.

This demonstrates how Pandas and NumPy work together.

## Step 10: Remove a column

```python
df = df.drop('goal_difference', axis=1)
```

`axis=1` means operate on columns.

The result is assigned back to `df` because `drop()` does not modify the original DataFrame by default.

## Step 11: Work with an index

```python
df.set_index('opponent')
df = df.reset_index()
```

The index provides labels that Pandas uses to identify rows.

When experimenting, discuss the difference between:

```python
df.set_index('opponent')
```

and:

```python
df = df.set_index('opponent')
```

The first displays a changed DataFrame. The second saves that change back into `df`.

## Step 12: Select rows with `iloc` and `loc`

```python
df.iloc[0]
df.loc[2]
df.iloc[0:4]
```

The broad distinction is:

- `iloc` selects by integer position.
- `loc` selects by index label.

They may appear to behave similarly while the DataFrame uses a default integer index, but they are conceptually different.

The slice `df.iloc[0:4]` retrieves positions 0, 1, 2 and 3. As with normal Python slicing, the ending position is excluded.

## Pandas takeaway

> Pandas helps us load, inspect, clean, select and transform labelled datasets before supplying them to a machine-learning model.

---

# 3. Matplotlib Refresher

Notebook: [1_c_MatplotlibRefresher.ipynb](./1_c_MatplotlibRefresher.ipynb)

## Learning purpose

Matplotlib creates charts and scientific figures.

Visualisation helps us:

- Understand a dataset.
- Discover patterns.
- Identify possible outliers.
- Compare variables.
- Explain model results.
- Communicate findings.

## Step 1: Import the plotting interface

```python
import matplotlib.pyplot as plt
```

`pyplot` provides common plotting commands and is conventionally imported as `plt`.

## Step 2: Prepare values to plot

```python
import numpy as np

x = np.arange(2, 12)
y = 1.5 * x
```

Each `x` value has a corresponding `y` value.

Because `y` is always 1.5 times `x`, the plot forms a straight line. This is a simple linear relationship.

## Step 3: Create a basic line plot

```python
plt.plot(x, y)
plt.xlabel('X Axis')
plt.ylabel('Y Axis')
plt.title('My first plot')
plt.show()
```

Each instruction controls one part of the chart:

- `plot` draws the data.
- `xlabel` describes the horizontal axis.
- `ylabel` describes the vertical axis.
- `title` explains the chart.
- `show` renders the figure.

### Teaching point

A chart should not merely look attractive. Its labels should allow another person to understand what is being shown.

## Step 4: Control the visible range

```python
plt.xlim(2, 6)
plt.ylim(2, 12)
```

These commands limit the visible range of each axis.

This can focus attention on an important region, but students should understand that inappropriate limits can also make a chart misleading.

## Step 5: Save a plot

```python
plt.savefig('plot1.png')
```

This saves the chart as an image in the repository folder.

The notebook later uses:

```python
fig.savefig('figure.png', bbox_inches='tight')
```

`bbox_inches='tight'` reduces unwanted whitespace and helps prevent labels from being clipped.

## Step 6: Understand figures and axes

```python
fig = plt.figure()
axes = fig.add_axes([0, 0, 1, 1])
axes.plot(x, y)
```

The distinction is:

- A **Figure** is the complete canvas.
- An **Axes** object is an individual plotting area on the canvas.

Although a chart has x and y axes, Matplotlib uses the object name `Axes` for the complete plotting region.

The four `add_axes` values represent:

1. Distance from the left.
2. Distance from the bottom.
3. Width.
4. Height.

They use proportions of the complete figure.

## Step 7: Plot a nonlinear relationship

```python
a = np.linspace(0, 10, 11)
b = a ** 2
```

`b` is the square of `a`, so the plotted relationship is curved rather than straight.

This demonstrates how visualisation can quickly reveal the shape of a relationship.

## Step 8: Add multiple axes to one figure

```python
axes1 = fig.add_axes([0, 0, 1, 1])
axes2 = fig.add_axes([0.2, 0.2, 0.5, 0.5])
```

The second plotting area is placed inside the first figure, creating an inset chart.

Each axes object can have its own:

- Data.
- Labels.
- Title.
- Colours.
- Limits.

## Step 9: Create subplots

```python
fig, axes = plt.subplots()
```

This creates a figure and axes together.

The notebook then creates several plotting areas:

```python
fig, axes = plt.subplots(nrows=1, ncols=2)
fig, axes = plt.subplots(nrows=2, ncols=2)
```

For a one-row, two-column layout:

```python
axes[0]
axes[1]
```

For a two-row, two-column layout:

```python
axes[0][0]
axes[0][1]
axes[1][0]
axes[1][1]
```

This connects back to NumPy because the collection of axes behaves like an array with a shape.

## Step 10: Customise plots

The notebook introduces:

- Axis labels.
- Titles.
- Colours.
- Plot positioning.
- Figure saving.

Useful classroom extensions include:

- Different line colours.
- Dashed and dotted line styles.
- Markers at each data point.
- Legends.
- Grid lines.
- Different figure sizes.

## Matplotlib takeaway

> Matplotlib converts numerical results into visual evidence, making patterns and relationships easier to discover and explain.

---

# Suggested classroom delivery

## Lesson 1: NumPy

Focus on:

- Arrays.
- Shapes.
- Data types.
- Random values.
- Seeds.
- Reshaping.
- Vectorised calculations.

Suggested question:

> Why would a model need to know the shape of its input?

## Lesson 2: Pandas

Connect it explicitly to NumPy:

- Arrays become labelled tables.
- A real CSV becomes a DataFrame.
- Rows and columns can be selected.
- New features can be calculated.
- Data can be inspected before modelling.

Suggested question:

> What problems could occur if we train a model without first inspecting the data?

## Lesson 3: Matplotlib

Use data from the earlier lessons:

- Plot numerical arrays.
- Compare straight and curved relationships.
- Label charts correctly.
- Create multiple plots.
- Save figures.

Suggested question:

> What can a graph reveal that a table of numbers might hide?

## Final learning message

The normal workflow is:

1. Use **NumPy** to represent numerical values.
2. Use **Pandas** to load, label, inspect and transform a dataset.
3. Use **Matplotlib** to explore and communicate what the data shows.
4. Later notebooks will use these foundations to train and evaluate machine-learning models.

