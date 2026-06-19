Since you already have a programming background and are learning Python for Data Science, I'd approach **Data Cleaning** as a specialized skill that sits between raw data collection and analysis/modeling.

A data scientist may spend **60-80% of their time cleaning data**, so mastering this area gives you a major advantage.

# Phase 1: Python Foundations for Data Cleaning (1 Week)

### Core Python

* Variables and Data Types
* Strings
* Lists
* Tuples
* Dictionaries
* Sets
* Functions
* Lambda Functions
* List Comprehensions
* Error Handling (`try/except`)
* Modules and Packages

### File Handling

* CSV
* JSON
* TXT
* Excel

### Useful Libraries

* `os`
* `pathlib`
* `datetime`
* `re` (Regular Expressions)

**Project**

* Read and clean customer data from CSV files.

---

# Phase 2: NumPy Fundamentals (3–5 Days)

### Arrays

* Creating arrays
* Indexing
* Slicing
* Filtering

### Data Manipulation

* Reshaping
* Broadcasting
* Vectorization

### Missing Values

* `np.nan`
* Detecting nulls

### Statistics

* Mean
* Median
* Std
* Percentiles

**Project**

* Clean sensor data containing missing values.

---

# Phase 3: Pandas Fundamentals (2 Weeks)

### Data Structures

* Series
* DataFrame

### Reading Data

```python
pd.read_csv()
pd.read_excel()
pd.read_json()
```

### Inspection

```python
.head()
.tail()
.info()
.describe()
.shape
.columns
.dtypes
```

### Selection

```python
.loc[]
.iloc[]
.query()
```

### Filtering

* Boolean masks
* Multiple conditions

### Sorting

```python
.sort_values()
.sort_index()
```

**Project**

* Analyze retail sales data.

---

# Phase 4: Data Quality Assessment (1 Week)

Learn to identify:

### Missing Data

```python
.isnull()
.notnull()
```

### Duplicate Data

```python
.duplicated()
.drop_duplicates()
```

### Inconsistent Values

Examples:

```
Male
male
M
m
```

### Invalid Formats

Examples:

```
Phone numbers
Emails
Dates
```

### Outliers

Examples:

```
Age = 250
Salary = -5000
```

**Project**

* Audit a messy HR dataset.

---

# Phase 5: Missing Data Mastery (1 Week)

### Detect Missing Values

```python
df.isnull().sum()
```

### Remove Missing Data

```python
dropna()
```

### Imputation

#### Numeric

* Mean
* Median
* Mode

#### Categorical

* Most Frequent
* Custom Value

#### Advanced

* KNN Imputation
* Iterative Imputation

Libraries:

```python
sklearn.impute
```

**Project**

* Clean healthcare records with missing information.

---

# Phase 6: String Cleaning & Text Processing (1 Week)

### String Operations

```python
.str.lower()
.str.upper()
.str.strip()
.str.replace()
```

### Regular Expressions

```python
import re
```

Topics:

* Pattern Matching
* Email Validation
* Phone Validation
* Extracting IDs

### Text Normalization

* Remove extra spaces
* Remove punctuation
* Standardize naming conventions

**Project**

* Clean customer contact information.

---

# Phase 7: Date & Time Cleaning (3 Days)

### Datetime

```python
pd.to_datetime()
```

### Time Operations

* Extract year
* Month
* Day
* Weekday

### Time Zones

### Invalid Dates

Examples:

```
32/12/2025
```

**Project**

* Clean event booking records.

---

# Phase 8: Categorical Data Cleaning (4 Days)

### Standardization

Convert:

```
Male
male
M
```

into

```
Male
```

### Category Management

```python
astype("category")
```

### Encoding

* Label Encoding
* One-Hot Encoding

**Project**

* Clean survey data.

---

# Phase 9: Outlier Detection & Treatment (1 Week)

### Statistical Methods

#### Z-Score

#### IQR

### Visualization

* Boxplots
* Histograms

### Treatment

* Remove
* Cap
* Transform

**Project**

* Clean financial transaction data.

---

# Phase 10: Data Validation & Integrity (1 Week)

### Rules

Examples:

```
Age > 0
Salary >= 0
```

### Cross-field Validation

Examples:

```
Start Date < End Date
```

### Unique Constraints

### Referential Integrity

**Project**

* Validate employee database.

---

# Phase 11: Advanced Pandas (2 Weeks)

### Merge Data

```python
merge()
join()
concat()
```

### Group Operations

```python
groupby()
pivot_table()
```

### MultiIndex

### Window Functions

### Method Chaining

### Performance Optimization

```python
categorical dtypes
vectorization
```

**Project**

* Clean and combine multiple business datasets.

---

# Phase 12: Exploratory Data Analysis for Cleaning (1 Week)

Libraries:

```python
matplotlib
seaborn
```

### Visual Checks

* Histograms
* Boxplots
* Scatterplots
* Correlation matrices

### Detect

* Missing patterns
* Outliers
* Data entry issues

**Project**

* Perform EDA on retail sales data.

---

# Phase 13: Automation & Production Cleaning (2 Weeks)

### Build Reusable Cleaning Functions

```python
clean_names()
clean_dates()
clean_phone_numbers()
```

### Pipelines

```python
sklearn.pipeline
```

### Logging

### Exception Handling

### Data Cleaning Frameworks

* Great Expectations
* Pandera

**Project**

* Build a reusable cleaning package.

---

# Phase 14: SQL for Data Cleaning (1 Week)

### Data Cleaning in SQL

* NULL handling
* CASE statements
* Window functions
* Deduplication

### SQL + Pandas Workflow

**Project**

* Clean data directly from a database.

---

# Phase 15: Real-World Data Cleaning Portfolio (3–4 Weeks)

Complete at least 10 datasets from:

* Kaggle
* Government datasets
* Retail datasets
* Healthcare datasets
* Finance datasets
* HR datasets

For each project:

1. Data Audit
2. Cleaning Plan
3. Cleaning Execution
4. Validation
5. EDA
6. Documentation

---

# Advanced Topics (Master Level)

### Data Quality Frameworks

* Great Expectations
* Pandera

### Big Data Cleaning

* Dask
* PySpark

### Data Warehousing

* ETL Pipelines
* ELT Pipelines

### Data Governance

* Data Lineage
* Data Catalogs

### Data Quality Metrics

### Feature Engineering

### Data Observability

Tools:

* Great Expectations
* Soda
* Monte Carlo

---

# Libraries You Should Master

### Essential

```python
pandas
numpy
matplotlib
seaborn
re
datetime
```

### Intermediate

```python
scikit-learn
openpyxl
sqlalchemy
```

### Advanced

```python
great_expectations
pandera
dask
pyspark
```

# Final Mastery Checklist

You can call yourself highly proficient in data cleaning when you can:

✅ Audit any dataset in under 30 minutes

✅ Detect all major data quality issues

✅ Handle missing values correctly

✅ Clean text, dates, and categorical data

✅ Detect and treat outliers

✅ Validate business rules

✅ Merge datasets safely

✅ Build reusable cleaning pipelines

✅ Automate cleaning workflows

✅ Clean datasets with millions of rows

✅ Document and test cleaning processes

✅ Explain every cleaning decision with business justification

If completed consistently, this roadmap is roughly **10–14 weeks full-time** or **4–6 months part-time**, and will take you from Python fundamentals to professional-level data cleaning expertise.
