Good. We’ll do this like a **real apprenticeship**, not tutorial hopping.

# PROJECT 1 — Tech Job Market Intelligence Platform

Goal:

Build a **real analyst → scientist portfolio project**.

Something a recruiter can say:

> *“This person can work with labor market data, analytics, dashboards, and predictive modeling.”*

---

# Outcome (What you will ship)

You will produce **4 deliverables**:

1. **SQL Analysis**
2. **Python Analytics Notebook**
3. **Power BI Dashboard**
4. **Salary Prediction Model**

Portfolio ready.

---

# Stack

Only use:

```txt
SQL (Postgres)

Python
- pandas
- matplotlib
- seaborn
- scikit-learn

Jupyter Notebook

Power BI

GitHub
```

No FastAPI. No Docker. No complexity.

---

# Dataset (REAL + RELATABLE)

Start with **real job market data**.

## Data Source

Use **Adzuna Jobs API**.

Why?

Because it is actual live-ish labor market data.

Useful fields:

* job title
* salary_min
* salary_max
* company
* location
* description
* category

Website:

Search:

**"Adzuna API developer access"**

Free starter access exists.

---

### Backup Dataset

If API setup slows you down:

Use Kaggle:

**Data Science Job Salaries Dataset**

Start moving. Don't stall.

---

# Week 1 — SQL + Business Understanding

## Business Question

You are hired by:

**Career Intelligence Company**

They want to know:

> Which tech skills command higher salaries?

---

## Task 1 — Create Database

Create table.

Example structure:

```sql
CREATE TABLE jobs (
    id SERIAL PRIMARY KEY,
    title TEXT,
    company TEXT,
    location TEXT,
    salary_min NUMERIC,
    salary_max NUMERIC,
    category TEXT,
    description TEXT
);
```

---

## Task 2 — Import Data

Learn:

* CSV import
* pgAdmin import

or

Python insert.

---

## Task 3 — SQL Analysis

Answer these questions.

### Q1.

Top hiring roles.

```sql
COUNT(*)
GROUP BY title
```

---

### Q2.

Highest paying locations.

---

### Q3.

Average salary by role.

---

### Q4.

Remote vs onsite comparison.

---

### Q5.

Top companies hiring.

---

### Q6.

Salary distribution.

---

## SQL Skills To Learn

Learn only:

```txt
SELECT

WHERE

GROUP BY

ORDER BY

CASE WHEN

CTE

Window Functions
```

Ignore advanced SQL for now.

---

## Resource

**Alex The Analyst — Complete SQL Course**

Do not binge.

Learn → immediately use in project.

---

# Week 2 — Python Data Cleaning + EDA

Now become a real analyst.

---

## Notebook Structure

Create:

```txt
01_data_cleaning.ipynb
```

---

## Step 1 — Load Data

```python
import pandas as pd

df = pd.read_csv("jobs.csv")
```

---

## Step 2 — Cleaning

Handle:

* null salaries
* duplicates
* messy titles
* inconsistent locations

Learn:

```python
dropna()

fillna()

str.contains()

str.extract()

apply()
```

---

## Step 3 — Feature Engineering

Create:

### average_salary

```python
df["avg_salary"]=(df.salary_min+df.salary_max)/2
```

---

### seniority_level

Extract:

* Junior
* Mid
* Senior

from title.

---

### remote_flag

Extract from descriptions.

---

## Step 4 — EDA

Questions:

### Highest paying skills?

Search descriptions for:

```txt
Python
SQL
AWS
React
Docker
Power BI
Machine Learning
```

Create skill columns.

---

### Questions to answer

Which skills:

* pay more?
* appear most?
* dominate roles?

---

## Visualizations

Build:

* bar charts
* histograms
* salary boxplots
* heatmaps

---

## Resources

**Keith Galli Pandas Tutorial**

**freeCodeCamp Pandas**

Enough.

---

# Week 3 — Dashboard (Analyst Portfolio Piece)

Now think like a stakeholder.

---

## Build Power BI Dashboard

Pages:

### Executive Overview

KPIs:

* total jobs
* avg salary
* top location
* top role

---

### Salary Analytics

Charts:

* salary by role
* salary by city
* salary distribution

---

### Skills Intelligence

Charts:

* most demanded skills
* salary vs skill
* role skill map

---

### Filters

Add:

* location
* role
* company

---

Goal:

Interactive business dashboard.

---

## Resource

**Maven Analytics Power BI YouTube**

---

# Week 4 — Data Science Layer

Now become a beginner data scientist.

---

## Problem

Predict:

> expected salary from job features.

---

## Notebook

Create:

```txt
02_salary_prediction.ipynb
```

---

## Features

Use:

```txt
title

location

skills

remote_flag

category
```

---

## Learn

### Train/Test Split

### Encoding

### Pipelines

### Regression

---

## Models

Start simple.

Use:

### Linear Regression

then

### Random Forest Regressor.

---

## Evaluation

Learn:

```txt
MAE

RMSE

R²
```

---

Don't chase perfect accuracy.

Explain results.

---

## Resource

**StatQuest Regression Playlist**

---

# Week 5 — Make It Portfolio Ready

Create GitHub repo.

---

## Repository Structure

```txt
tech-job-intelligence/

│── data/
│── notebooks/
│   ├── 01_cleaning.ipynb
│   ├── 02_model.ipynb
│
│── sql/
│   ├── analysis.sql
│
│── dashboard/
│   └── powerbi.pbix
│
│── README.md
```

---

## README Template

### Problem

Tech workers struggle understanding salary trends.

---

### Dataset

Adzuna Jobs API.

---

### Analysis Questions

* top skills
* salaries
* location trends

---

### Methods

SQL

EDA

Regression modeling.

---

### Findings

Summarize results.

---

### Recommendations

Example:

> SQL + Cloud skills correlate with higher salaries.

---

### Dashboard Screenshot

Include visuals.

---

# Real Learning Checklist

By end you should know:

## SQL

✅ aggregation

✅ joins

✅ filtering

✅ window functions

---

## Python

✅ cleaning

✅ EDA

✅ feature engineering

---

## BI

✅ stakeholder dashboards

---

## ML

✅ regression workflow

---

## Portfolio

✅ business storytelling

 
