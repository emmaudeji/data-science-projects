Excellent. This stage separates **people who can analyze data** from **people who can build reliable ML systems**.

Think of this stage as:

# Stage 3 — Data Preparation & Feature Engineering

## **Prepare Data for Battle**

Mental model:

```txt
Raw Data
   ↓
Clean Data
   ↓
Model-Ready Data
   ↓
Feature-Enhanced Data
   ↓
Training Pipeline
```

You are no longer just investigating.

You are **engineering inputs for machine learning**.

Goal:

> **Make data understandable, usable, stable, and informative for algorithms.**

---

# The Data Preparation Workflow (Structured)

We'll organize this stage into **8 practical categories**.

```txt
1. Problem Framing & Target Definition
2. Dataset Splitting
3. Data Cleaning & Transformation
4. Scaling & Normalization
5. Encoding Features
6. Feature Engineering
7. Imbalanced Data Handling
8. Pipeline Preparation
```

---

# 1. PROBLEM FRAMING & TARGET DEFINITION

Before touching preprocessing:

Define:

> **What exactly are we predicting?**

---

## Real Fraud Example

Transaction arrives.

Predict:

```txt
Fraud?
YES / NO
```

Target column:

```python
Class
```

---

Target variable.

Convention:

```python
y = target
X = predictors
```

Code:

```python
X = df.drop("Class", axis=1)
y = df["Class"]
```

---

Think.

```txt
X → evidence

y → truth
```

---

### Scientific Thinking

This is **supervised learning**.

Meaning:

We already know historical outcomes.

Example:

| Amount | Time | Class |
| ------ | ---- | ----- |
| 100    | 5    | 0     |
| 9000   | 33   | 1     |

---

### Questions you ask

```txt
What am I predicting?

Which variable is the outcome?

Which columns should be excluded?

Any leakage risk?
```

---

---

## Data Leakage Thinking

One of the most important DS concepts.

---

### Real Example

Imagine adding:

```txt
Fraud_Investigation_Status
```

Column.

Values:

```txt
Investigated Fraud
Cleared
```

Problem?

The future leaked into training.

Model cheats.

---

Bad.

---

Detect leakage:

```txt
post-event information

future knowledge

human investigation outputs
```

---

Rule.

Only use:

> **Information available at prediction time.**

---

---

# 2. DATASET SPLITTING

Critical.

Goal:

Simulate real life.

---

## Why split?

Real life:

Your model predicts **unseen transactions**.

Not training data.

---

Wrong:

```txt
Train + test on same data.
```

Leads to memorization.

---

Correct.

Split.

---

Library.

```python
from sklearn.model_selection import train_test_split
```

---

Code.

```python
X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42
)
```

---

Meaning.

```txt
80% training

20% testing
```

---

### Parameters

---

#### test_size

How much evaluation data?

---

#### random_state

Reproducibility.

Without it:

Different splits every run.

---

### Stratification

VERY important for fraud.

---

Fraud datasets are imbalanced.

Need class preservation.

Use:

```python
stratify=y
```

---

Code.

```python
train_test_split(
    X,
    y,
    stratify=y
)
```

---

Why?

Prevent.

```txt
training: few frauds

testing: zero frauds
```

---

---

## Scientific Thinking

This is:

**generalization testing**.

Question:

> "Can the model perform on unseen reality?"

---

---

# 3. DATA CLEANING & TRANSFORMATION

Now clean inputs.

---

Think:

Data surgery.

---

Goal.

Fix problems discovered in EDA.

---

---

## Missing Values

---

Library.

```python
from sklearn.impute import SimpleImputer
```

---

Why?

Models dislike nulls.

---

Strategies.

---

### Mean Imputation

Replace missing numeric values.

```python
mean
```

---

Code.

```python
imputer = SimpleImputer(
    strategy='mean'
)
```

---

Use cases.

Continuous variables.

---

### Median Imputation

More robust.

Better with outliers.

Common in finance.

---

Code.

```python
strategy='median'
```

---

### Most Frequent

Categorical columns.

```python
strategy='most_frequent'
```

---

---

## Apply Imputation

```python
X_train = imputer.fit_transform(X_train)
```

---

Important distinction.

---

### fit()

Learn pattern.

---

### transform()

Apply learned pattern.

---

### fit_transform()

Both.

---

Mental model.

```txt
fit → learn recipe

transform → cook using recipe
```

---

---

## Outlier Handling

Important in fraud.

Because fraud IS often anomalous.

Careful here.

---

Methods.

---

### IQR Method

Interquartile Range.

Common.

---

Concept.

IQR = Q3 - Q1

Threshold.

Lower = Q1 - 1.5(IQR),\ Upper = Q3 + 1.5(IQR)

---

Code.

```python
Q1 = df['Amount'].quantile(.25)
Q3 = df['Amount'].quantile(.75)

IQR = Q3-Q1
```

---

### Z-score Method

Library.

```python
from scipy.stats import zscore
```

---

Concept.

Measure:

> distance from mean.

---

Code.

```python
zscore(df["Amount"])
```

---

---

### Statistical Thinking

Question.

```txt
Remove?

Cap?

Keep?
```

Fraud projects often **keep some anomalies** because anomalies may contain fraud signal.

---

---

# 4. SCALING & NORMALIZATION

One of the most misunderstood steps.

---

Problem.

Different units.

Example.

```txt
Amount = 500000

Age = 32
```

---

Models see:

```txt
500000 dominates 32
```

---

Need comparable scales.

---

Library.

```python
from sklearn.preprocessing import StandardScaler
```

---

---

## Standardization

Most common.

Concept.

Center around mean.

Scale by std.

genui{"math_block_widget_always_prefetch_v2":{"content":"z = \frac{x-\mu}{\sigma}"}}

---

Code.

```python
scaler = StandardScaler()

X_train_scaled = scaler.fit_transform(
    X_train
)
```

---

Result.

```txt
mean ≈ 0

std ≈ 1
```

---

Use when:

```txt
logistic regression

SVM

KNN

PCA
```

---

---

## MinMax Scaling

Range compression.

Library.

```python
from sklearn.preprocessing import MinMaxScaler
```

---

Concept.

Scale between:

```txt
0 → 1
```

---

Code.

```python
MinMaxScaler()
```

---

Use when:

```txt
neural networks
bounded features
```

---

---

## Robust Scaling

Outlier resistant.

Important for finance.

---

Library.

```python
from sklearn.preprocessing import RobustScaler
```

---

Uses:

```txt
median

IQR
```

instead of mean/std.

---

---

## Scientific Thinking

Scaling affects:

```txt
distance calculations

optimization

gradient convergence
```

---

---

# 5. ENCODING FEATURES

Models speak numbers.

Humans use categories.

---

Example.

```txt
Country:
Nigeria
Ghana
Kenya
```

Need conversion.

---

Library.

```python
from sklearn.preprocessing import OneHotEncoder
```

---

---

## Label Encoding

Simple integer mapping.

```python
Nigeria → 0
Ghana → 1
Kenya → 2
```

---

Library.

```python
LabelEncoder()
```

---

Danger.

Model may assume ordering.

---

---

## One Hot Encoding

Safer.

Creates binary columns.

---

Example.

| Nigeria | Ghana | Kenya |
| ------- | ----- | ----- |
| 1       | 0     | 0     |

---

Code.

```python
pd.get_dummies(df)
```

or

```python
OneHotEncoder()
```

---

Use:

Nominal categories.

---

---

## Statistical Thinking

Encoding changes:

**feature representation geometry**.

Yes.

This matters.

---

---

# 6. FEATURE ENGINEERING

The most creative DS skill.

---

Goal.

Create **better signals**.

---

Raw data:

```txt
transaction_time
```

Useful engineered feature:

```txt
night_transaction
```

---

Real fraud examples.

---

### Time Features

Convert:

```txt
timestamp
```

into:

```txt
hour
weekday
weekend
night
```

---

Code.

```python
df['hour'] = df['date'].dt.hour
```

---

---

### Ratio Features

Example.

```txt
amount / avg_user_amount
```

---

---

### Behavioral Features

Real fintech feature engineering.

---

Examples.

```txt
transactions_last_1hr

failed_logins

device_count

new_location
```

---

---

### Binning

Turn continuous into groups.

---

Example.

```txt
low amount

medium amount

high amount
```

---

Library.

```python
pd.cut()
```

---

Code.

```python
pd.cut(
    df["Amount"],
    bins=5
)
```

---

---

### Log Transformation

Fix skewed distributions.

Common in finance.

---

Concept.

Compress extreme values.

---

Code.

```python
np.log1p(df["Amount"])
```

---

---

### Statistical Thinking

Feature engineering improves:

```txt
signal extraction

nonlinear patterns

separability
```

---

---

# 7. IMBALANCED DATA HANDLING

THIS is the heart of fraud ML.

---

Reality.

```txt
99.8% normal

0.2% fraud
```

---

Without handling.

Model predicts:

```txt
everything normal
```

---

Looks:

```txt
99% accurate
```

Actually terrible.

---

Library.

```python
from imblearn.over_sampling import SMOTE
```

---

---

## Oversampling

Increase minority class.

---

### SMOTE

Synthetic data generation.

Creates artificial fraud examples.

---

Code.

```python
smote = SMOTE()

X_res,y_res = smote.fit_resample(
    X_train,
    y_train
)
```

---

---

## Undersampling

Reduce majority class.

---

Library.

```python
RandomUnderSampler()
```

---

Tradeoff.

Lose data.

---

---

## Class Weights

Very important.

---

Tell model:

> fraud mistakes cost more.

---

Code.

```python
class_weight='balanced'
```

---

Common in:

```txt
logistic regression

random forest
```

---

---

## Scientific Thinking

This is:

**cost-sensitive learning**.

Question:

> "How do we make rare events visible to algorithms?"

---

---

# 8. PIPELINE PREPARATION

Production mindset begins here.

---

Problem.

Too many preprocessing steps.

---

Need automation.

---

Library.

```python
from sklearn.pipeline import Pipeline
```

---

Example.

```python
pipeline = Pipeline([
    ('scaler',StandardScaler()),
    ('model',LogisticRegression())
])
```

---

Benefits.

---

### Reproducibility

Same process every run.

---

### Leakage prevention

Safer workflow.

---

### Cleaner code

Production ready.

---

---

## ColumnTransformer

Handle different column types.

---

Library.

```python
from sklearn.compose import ColumnTransformer
```

---

Example.

```python
numeric → scaling

categorical → encoding
```

---

---

# Core Library Cheat Sheet

| Library                 | Purpose             |
| ----------------------- | ------------------- |
| sklearn.model_selection | splitting           |
| sklearn.impute          | missing values      |
| sklearn.preprocessing   | scaling / encoding  |
| sklearn.pipeline        | workflow automation |
| imblearn                | imbalance handling  |
| scipy                   | statistics          |

---

# Core Code Patterns You'll Use Constantly

```python
train_test_split()

SimpleImputer()

StandardScaler()

MinMaxScaler()

OneHotEncoder()

pd.get_dummies()

SMOTE()

Pipeline()

ColumnTransformer()

fit()

transform()

fit_transform()
```

---

# Mental Model — Data Preparation Hierarchy

Think in **5 engineering layers**.

```txt
Layer 1
Define target & prevent leakage.

Layer 2
Split reality into train/test.

Layer 3
Clean & standardize data.

Layer 4
Create stronger features.

Layer 5
Build reusable preprocessing pipelines.
```

---

# Final Project Mental Model So Far

```txt
STAGE 1
Business Understanding
"Why does fraud matter?"

STAGE 2
EDA
"What patterns exist?"

STAGE 3
Preparation & Feature Engineering
"How do we make data ML-ready?"
```

After this stage, the data becomes:

```txt
Reliable
Clean
Scaled
Balanced
Feature-rich
Pipeline-ready
```

Then we enter **Stage 4 — Machine Learning Modeling**:

> **Teach algorithms to detect fraud.**

This is where all the preparation work starts paying off.
