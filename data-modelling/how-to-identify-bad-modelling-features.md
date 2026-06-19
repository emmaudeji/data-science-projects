This question is actually one of the most important concepts in Data Science.

If you truly understand this, you'll stop building "toy models" and start thinking like a real Data Scientist.

---

# Let's Start With A Simple Example

Imagine I'm your manager at Instacart.

I say:

> Emmanuel, before a customer checks out, I want to estimate how much they'll spend.

Notice the phrase:

```text
BEFORE they checkout
```

That's the key.

At prediction time, what information do we have?

Maybe:

```text
Item = Coffee
Location = In-store
Month = June
Weekday = Friday
Payment Method = Card
```

But do we know:

```text
Total Spent ?
```

No.

That's what we're trying to predict.

---

# The Golden Rule

A feature can only be used if it would be available when the prediction is made.

Let's repeat that:

> A feature can only be used if it would exist at the moment you want to make the prediction.

---

# Why Quantity and Price Per Unit Become A Problem

Suppose your dataset contains:

| Item   | Quantity | Price Per Unit | Total Spent |
| ------ | -------- | -------------- | ----------- |
| Coffee | 4        | 1000           | 4000        |

Now imagine we ask:

> Predict Total Spent.

And we give the model:

```python
Quantity = 4
Price Per Unit = 1000
```

The model doesn't need to learn anything.

Because:

```python
Total Spent = Quantity * Price Per Unit
```

Literally:

```python
4000 = 4 * 1000
```

The answer is already hidden inside the features.

---

# Real-Life Analogy

Imagine I ask:

> Predict a student's final score.

Then I give you:

```text
Exam Score = 80
Assignment Score = 10
Final Score = 90
```

And my model uses:

```text
Exam Score
Assignment Score
```

to predict:

```text
Final Score
```

Well...

```python
Final Score = Exam Score + Assignment Score
```

The model is not intelligent.

It's just doing arithmetic.

---

# Data Leakage

This is called:

```text
Data Leakage
```

Definition:

> Information that would not truly be available during prediction is leaking into the model.

Data leakage creates fake accuracy.

---

# What Happens When Beginners Do This

They train:

```python
X = [
    Quantity,
    Price_Per_Unit
]

y = Total_Spent
```

Then they get:

```text
R² = 0.9999
```

And they celebrate.

Meanwhile the model is useless.

Why?

Because:

```python
Quantity * Price_Per_Unit
```

already equals:

```python
Total_Spent
```

---

# The Question Every Data Scientist Asks

Before choosing features:

Ask:

> When this model is deployed, will I know this value?

---

# Scenario 1: Checkout Prediction

Suppose a customer is still shopping.

We know:

```text
Customer Location
Month
Weekday
Past Orders
```

We do NOT know:

```text
Final Spend
```

because checkout hasn't happened.

So we can use:

```text
Location
Month
Weekday
```

but not:

```text
Total Spent
```

---

# Scenario 2: Revenue Forecasting

Manager says:

> Predict tomorrow's revenue.

At prediction time we know:

```text
Today's date
Month
Weekday
Historical sales
Season
```

We don't know:

```text
Tomorrow's revenue
```

because that's the thing we're predicting.

---

# Let's Use An Instacart Example

Suppose management asks:

> Which transactions are likely to be above ₦10,000?

Before checkout, we know:

```text
Item
Month
Weekday
Location
Payment Method
```

We may NOT know:

```text
Total Spent
```

because it hasn't happened yet.

Now the model becomes useful.

---

# Another Way To Think About It

Imagine you're transported into the future system.

A customer is currently placing an order.

You open the prediction page.

What fields can the customer actually fill in?

Maybe:

```text
Item
Location
Payment Method
```

Those are valid features.

Now ask:

Can the customer enter:

```text
Total Spent
```

No.

If they already knew Total Spent, there'd be nothing to predict.

---

# Why Businesses Care

Businesses don't pay Data Scientists to explain the past.

Businesses pay Data Scientists to help make decisions before something happens.

Examples:

### Netflix

Before you watch:

```text
Will Emmanuel like this movie?
```

---

### Bank

Before approval:

```text
Will Emmanuel default on this loan?
```

---

### Instacart

Before inventory runs out:

```text
How many coffee units should we stock tomorrow?
```

---

### Uber

Before surge pricing:

```text
How many rides will be requested in the next hour?
```

---

# Looking At Your Dataset Specifically

If I were mentoring you in a real company, I'd say:

### Bad First Model

```python
Predict Total Spent
using

Quantity
Price Per Unit
```

Reason:

```text
The answer is already hidden in the features.
```

---

### Better Model

```python
Predict Quantity
using

Item
Month
Weekday
Location
```

Business Question:

> How many units of an item will likely be sold?

Now management can use the prediction to stock inventory.

Very realistic.

---

### Even Better Model

Aggregate the data by day.

Create:

| Date   | Revenue |
| ------ | ------- |
| June 1 | 120000  |
| June 2 | 135000  |
| June 3 | 110000  |

Then predict:

```text
Tomorrow's Revenue
```

This is something Instacart executives would actually care about.

---

# The Mental Test I Use

Whenever you're choosing features, ask:

> If I were using this model in production tomorrow morning, would I already know this value?

If YES:

✅ Valid feature

If NO:

❌ Data leakage

That's the easiest way to catch bad models before writing a single line of code.

Now we're ready for modeling, because you've reached the most important realization:

**Machine Learning isn't about getting a high accuracy score. It's about making useful predictions before the outcome happens.**
