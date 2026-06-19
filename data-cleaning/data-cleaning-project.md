Your enterprise-scale practice dataset is ready:

📦 **Download ZIP**
[Enterprise E-commerce Data Cleaning Mastery Dataset](sandbox:/mnt/data/ecommerce_data_cleaning_mastery.zip)

### Included Files

| File                |   Rows |
| ------------------- | -----: |
| customers.csv       | 10,000 |
| products.csv        |  2,000 |
| orders.csv          | 30,000 |
| payments.csv        | 30,000 |
| reviews.csv         | 15,000 |
| support_tickets.csv | 10,000 |

**Total:** ~97,000 records

---

### Data Quality Problems Included

This dataset intentionally contains many real-world issues:

#### Customer Data

* Duplicate IDs
* Missing names
* Invalid ages
* Mixed casing
* Malformed emails
* Inconsistent countries

#### Product Data

* Missing product names
* Negative prices
* Mixed currency formats
* Invalid categories
* Extreme stock values

#### Orders

* Duplicate order IDs
* Invalid foreign keys
* Negative quantities
* Extreme outliers
* Invalid dates
* Delivery dates before order dates

#### Payments

* Negative amounts
* Currency inconsistencies
* Missing statuses
* Invalid order references

#### Reviews

* Invalid ratings
* Missing review text
* Broken customer/product references

#### Support Tickets

* Inconsistent priorities
* Missing statuses
* Invalid dates

---

### Recommended Mastery Project Roadmap

#### Stage 1: Data Audit

Build a complete audit report:

```python
missing_values_report()
duplicate_report()
datatype_report()
foreign_key_report()
outlier_report()
```

#### Stage 2: Cleaning Framework

Create:

```python
clean_customers()
clean_products()
clean_orders()
clean_payments()
clean_reviews()
clean_support_tickets()
```

#### Stage 3: Validation Layer

Using:

```python
pandera
```

or

```python
great_expectations
```

Validate:

* Age > 0
* Price > 0
* Rating between 1–5
* Valid emails
* Order date <= delivery date
* Foreign key integrity

#### Stage 4: EDA

Use:

```python
pandas
numpy
matplotlib
seaborn
```

Find:

* Missing patterns
* Anomalies
* Customer behavior
* Product trends

#### Stage 5: Feature Engineering

Create:

* Customer Lifetime Value
* Average Order Value
* Repeat Purchase Rate
* Customer Retention
* Product Popularity Score

#### Stage 6: Production Pipeline

Build:

```text
project/
│
├── data/
├── audits/
├── cleaners/
├── validators/
├── pipelines/
├── tests/
├── reports/
└── notebooks/
```

This will closely resemble the workflow used by data analysts, data scientists, analytics engineers, and data engineers in production environments.
