Excellent approach.

You’re not asking for **“give me code.”**

You’re asking:

> **"What exactly happens inside EDA, what tools exist, when do I use them, what statistical thinking is happening, and what code patterns should I know before touching the project?"**

That is the right way to learn.

---

# DATA UNDERSTANDING & EDA — Become an Investigator

Goal:

You are **not building models yet.**

You are learning:

```txt
What data do I have?
What does fraud look like?
Which variables matter?
What patterns exist?
What statistical relationships exist?
What anomalies exist?
What preprocessing may be needed?
```

Think:

**Data Detective Mode.**

---

# The EDA Workflow (Structured)

We'll organize EDA into **8 practical categories**.

```txt
1. Dataset Inspection
2. Data Quality Analysis
3. Univariate Analysis
4. Bivariate Analysis
5. Multivariate Analysis
6. Statistical Relationship Analysis
7. Fraud Pattern Discovery
8. EDA Conclusions
```

---

# 1. DATASET INSPECTION

First contact with data.

Goal:

Understand the structure.

---

## Libraries

```python
import pandas as pd
import numpy as np
```

### Why these?

---

### Pandas

Main DS workhorse.

Think:

**Excel on steroids.**

Used for:

```txt
loading
filtering
grouping
cleaning
aggregating
exploring
```

---

### NumPy

Numerical engine.

Handles:

```txt
arrays
matrix math
statistics
numerical operations
```

Pandas is built on top of NumPy.

---

---

## Load Dataset

```python
df = pd.read_csv("creditcard.csv")
```

Meaning:

```txt
CSV file
→ DataFrame object
```

DataFrame = smart spreadsheet.

---

## View Data

### First rows

```python
df.head()
```

Purpose:

Quick preview.

---

### Last rows

```python
df.tail()
```

---

### Random sample

Useful in large datasets.

```python
df.sample(5)
```

---

## Understand Structure

### Shape

```python
df.shape
```

Returns:

```python
(rows, columns)
```

Example:

```txt
(284807,31)
```

---

### Column names

```python
df.columns
```

---

### Datatypes

```python
df.dtypes
```

Check:

```txt
numeric
object
datetime
boolean
```

---

### Full summary

```python
df.info()
```

Shows:

```txt
null values
memory usage
types
row count
```

Very important.

---

---

# 2. DATA QUALITY ANALYSIS

Real data is messy.

Goal:

Find problems.

---

## Missing Values

### Detect missing data

```python
df.isnull().sum()
```

Interpretation:

```txt
Which columns have empty values?
```

---

Visual version.

Libraries:

```python
import seaborn as sns
import matplotlib.pyplot as plt
```

---

### Why Seaborn?

Built for:

```txt
statistics visualization
EDA
beautiful plotting
```

---

### Why Matplotlib?

Core plotting library.

Seaborn uses it internally.

---

Missing value heatmap:

```python
sns.heatmap(df.isnull())
plt.show()
```

Shows missingness patterns.

---

---

## Duplicate Rows

Real financial systems may duplicate events.

Check:

```python
df.duplicated().sum()
```

Remove:

```python
df.drop_duplicates()
```

---

---

## Data Type Problems

Sometimes:

```txt
amount → string
date → object
```

Wrong.

Convert.

```python
pd.to_datetime()
astype()
```

Example:

```python
df["Amount"]=df["Amount"].astype(float)
```

---

---

# 3. UNIVARIATE ANALYSIS

Study **one variable at a time**.

Question:

> "How does this variable behave?"

---

Two categories.

---

## Numerical Variables

Examples:

```txt
Amount
Time
V1
V2
```

---

### Descriptive Statistics

```python
df.describe()
```

Returns:

```txt
mean
median
std
min
max
quartiles
```

---

Concepts.

---

### Mean

Average.

Sensitive to outliers.

---

### Median

Middle value.

Robust.

Fraud datasets often prefer median.

---

### Standard Deviation

Measures spread.

High std:

```txt
values widely dispersed
```

---

---

## Distribution Analysis

### Histogram

Visualize distribution.

```python
sns.histplot(df["Amount"])
plt.show()
```

Question:

```txt
small transactions?
large transactions?
skewed distribution?
```

---

### KDE Plot

Smooth probability curve.

```python
sns.kdeplot(df["Amount"])
```

Used for:

distribution shape.

---

### Boxplot

Outlier detector.

```python
sns.boxplot(x=df["Amount"])
```

Shows:

```txt
median
quartiles
outliers
```

Very useful in fraud.

---

### Skewness

Detect asymmetry.

```python
df["Amount"].skew()
```

---

Interpretation:

```txt
0 = symmetric

positive = long right tail

negative = left tail
```

Fraud data is often **positively skewed**.

---

---

## Categorical Variables

Example:

```txt
Class
MerchantType
Country
```

---

### Frequency counts

```python
df["Class"].value_counts()
```

Critical for fraud.

---

### Percentage distribution

```python
df["Class"].value_counts(normalize=True)
```

Shows imbalance.

---

### Countplot

```python
sns.countplot(x="Class",data=df)
```

Visual class balance.

---

---

# 4. BIVARIATE ANALYSIS

Two variables.

Question:

> "How do these variables interact?"

---

---

## Numerical vs Numerical

---

### Correlation

Core EDA skill.

Library:

```python
corr=df.corr()
```

---

Concept.

Measures relationship strength.

Range:

```txt
-1 to 1
```

---

Interpretation.

```txt
1 → strong positive

-1 → strong negative

0 → no linear relationship
```

---

### Heatmap

Visual correlation matrix.

```python
sns.heatmap(
    df.corr(),
    cmap="coolwarm"
)
```

Purpose:

See feature relationships.

---

---

### Scatter Plot

Relationship visualization.

```python
sns.scatterplot(
x="Time",
y="Amount",
data=df
)
```

Question:

```txt
Do larger amounts occur at specific times?
```

---

---

## Numerical vs Categorical

Very important for fraud.

---

Question:

> "Does Amount differ between Fraud and Non-Fraud?"

---

### GroupBy

Core pandas skill.

```python
df.groupby("Class")["Amount"].mean()
```

Used everywhere.

---

Example thinking.

```txt
average fraud amount

vs

average normal amount
```

---

### Boxplot by category

```python
sns.boxplot(
x="Class",
y="Amount",
data=df
)
```

Excellent fraud visualization.

---

### Violin Plot

Distribution comparison.

```python
sns.violinplot(
x="Class",
y="Amount",
data=df
)
```

Shows:

```txt
shape
density
spread
```

---

---

## Categorical vs Categorical

Example.

```txt
Country vs Fraud
```

---

Cross table.

```python
pd.crosstab()
```

Example:

```python
pd.crosstab(
df["Country"],
df["Class"]
)
```

---

---

# 5. MULTIVARIATE ANALYSIS

Multiple variables.

Real datasets are multidimensional.

---

### Pairplot

Library:

```python
sns.pairplot()
```

---

Purpose:

View many variable relationships.

```python
sns.pairplot(
df[['Amount','Time','Class']]
)
```

---

### Correlation Matrix

Already seen.

Extremely common.

---

### Feature Interaction Analysis

Question:

```txt
Do frauds cluster in certain combinations?
```

---

---

# 6. STATISTICAL RELATIONSHIP ANALYSIS

This is deeper EDA.

Not ML yet.

---

## Covariance

Direction of movement.

```python
df.cov()
```

---

Difference.

---

### Correlation

Standardized.

Easy comparison.

---

### Covariance

Raw movement magnitude.

---

---

## Hypothesis Thinking

Question:

> "Are fraud amounts statistically different?"

---

Simple statistical test.

Library:

```python
from scipy import stats
```

---

### T-Test

```python
stats.ttest_ind()
```

Compare means.

---

Example.

```python
fraud=df[df['Class']==1]['Amount']

normal=df[df['Class']==0]['Amount']

stats.ttest_ind(fraud,normal)
```

---

### P-Value

Interpretation.

```txt
p < 0.05

→ statistically significant
```

---

Important DS thinking.

---

---

# 7. FRAUD PATTERN DISCOVERY

Now domain thinking.

Not generic EDA.

Fraud-specific investigation.

---

Questions.

---

### Class Imbalance

Most important.

```python
df["Class"].value_counts()
```

---

### Fraud Transaction Distribution

```python
sns.histplot(
data=df,
x='Amount',
hue='Class'
)
```

---

Question:

```txt
Are fraud amounts unusually large?
```

---

### Time Patterns

```python
sns.boxplot(
x='Class',
y='Time',
data=df
)
```

---

Question:

```txt
Do frauds happen in bursts?
```

---

### Outlier Discovery

Library.

```python
from scipy.stats import zscore
```

---

Find anomalies.

```python
z=np.abs(zscore(df["Amount"]))
```

---

Threshold.

```python
z>3
```

Potential outliers.

---

---

## Feature Importance Clues

Pre-model intuition.

Correlation to target.

```python
df.corr()['Class']
```

---

Question:

```txt
Which variables relate to fraud?
```

---

---

# 8. EDA CONCLUSIONS

The most overlooked step.

You summarize findings.

---

Example.

```txt
Dataset highly imbalanced.

Amount strongly skewed.

Fraud transactions show abnormal distributions.

Some features correlate with target.

Scaling likely needed.

SMOTE may be required.
```

---

This guides modeling.

EDA is not decoration.

EDA informs:

```txt
feature engineering
cleaning
model choice
evaluation strategy
```

---

# Core Library Cheat Sheet

| Library    | Purpose                   |
| ---------- | ------------------------- |
| pandas     | data manipulation         |
| numpy      | numerical computation     |
| matplotlib | plotting                  |
| seaborn    | statistical visualization |
| scipy      | statistical testing       |

---

# Core Code Patterns You Will Use Constantly

```python
df.head()

df.info()

df.describe()

df.isnull().sum()

df.value_counts()

df.groupby()

df.corr()

sns.histplot()

sns.boxplot()

sns.heatmap()

sns.scatterplot()

pd.crosstab()

stats.ttest_ind()
```

---

# Practical Mental Model

Think of EDA as **4 investigative layers**.

```txt
Layer 1
Understand dataset structure.

Layer 2
Find data quality issues.

Layer 3
Discover statistical patterns.

Layer 4
Extract business/domain insights.
```

After mastering this overview, you will know:

**what tool to reach for, why you are using it, and what question it answers.**

Then we can start the **actual fraud dataset coding walkthrough** step-by-step like a real analyst.
