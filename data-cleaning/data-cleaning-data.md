I've generated a dirty dataset for data-cleaning practice:

📁 **Download CSV:**
[Data Cleaning Mastery Dataset](sandbox:/mnt/data/data_cleaning_mastery_dirty_dataset.csv)

### What's intentionally wrong in this dataset?

* Missing values (`NULL`, blank fields)
* Duplicate customer IDs
* Invalid ages (`-5`, `250`, `"Twenty Eight"`)
* Inconsistent gender values (`Male`, `male`, `M`, etc.)
* Inconsistent country names (`USA`, `U.S.A`, `United States`, `US`)
* Invalid email formats
* Missing products
* Negative and extreme quantities
* Mixed price formats (`99.99`, `$200`, `150 USD`)
* Invalid payment methods
* Mixed date formats
* Invalid dates (`yesterday`, `invalid-date`)
* Cross-field inconsistencies

### Suggested Learning Workflow

1. Load the dataset
2. Perform a data audit report
3. Identify all quality issues
4. Clean column by column
5. Create validation rules
6. Build reusable cleaning functions
7. Generate a final cleaned dataset
8. Write unit tests for your cleaning pipeline

After you finish this dataset, I can generate a much larger **10,000–100,000 row enterprise e-commerce dataset with 50+ real-world data quality problems across multiple CSV files (customers, orders, payments, products, reviews, support tickets)** that is closer to what data engineers and senior data scientists encounter in production.
