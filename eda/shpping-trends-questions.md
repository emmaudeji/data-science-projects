This is exactly the mindset of a Data Analyst:

> **Don't start with charts. Start with business questions.**
>
> Every dataset = stakeholders asking:
>
> * What's happening?
> * Why is it happening?
> * What should we do next?

For your Shopping Trends dataset, here are **20 high-value business questions**, the **business expectation**, and the **Pandas code** to answer them.

---

# 1. Which products generate the most revenue?

**Business Decision:** Stock more of them.

```python
# Top revenue generating products
df.groupby("Item Purchased")["Purchase Amount (USD)"] \
  .sum() \
  .sort_values(ascending=False) \
  .head(10)
```

---

# 2. Which categories generate the most revenue?

**Business Decision:** Invest more in winning categories.

```python
# Revenue by category
df.groupby("Category")["Purchase Amount (USD)"] \
  .sum() \
  .sort_values(ascending=False)
```

---

# 3. Which products sell most frequently?

**Business Decision:** Know customer favorites.

```python
# Most purchased items
df["Item Purchased"].value_counts().head(10)
```

---

# 4. Which locations generate the highest sales?

**Business Decision:** Focus marketing in top regions.

```python
# Revenue by location
df.groupby("Location")["Purchase Amount (USD)"] \
  .sum() \
  .sort_values(ascending=False)
```

---

# 5. Which customer gender spends more?

**Business Decision:** Better targeting.

```python
# Average spend by gender
df.groupby("Gender")["Purchase Amount (USD)"] \
  .mean()
```

---

# 6. Which age group spends the most?

**Business Decision:** Identify core customers.

```python
# Age segmentation
df["Age Group"] = pd.cut(
    df["Age"],
    bins=[0,25,35,45,55,100],
    labels=["18-25","26-35","36-45","46-55","56+"]
)

df.groupby("Age Group")["Purchase Amount (USD)"] \
  .mean()
```

---

# 7. Which season generates the most revenue?

**Business Decision:** Plan inventory and campaigns.

```python
# Revenue by season
df.groupby("Season")["Purchase Amount (USD)"] \
  .sum()
```

---

# 8. Which payment method is most used?

**Business Decision:** Improve checkout experience.

```python
# Popular payment methods
df["Payment Method"].value_counts()
```

---

# 9. Which payment method brings the highest spend?

**Business Decision:** Promote profitable payment channels.

```python
# Revenue by payment method
df.groupby("Payment Method")["Purchase Amount (USD)"] \
  .mean() \
  .sort_values(ascending=False)
```

---

# 10. Do discounts increase spending?

**Business Decision:** Evaluate discount strategy.

```python
# Discount impact
df.groupby("Discount Applied")["Purchase Amount (USD)"] \
  .mean()
```

---

# 11. Do promo codes increase spending?

**Business Decision:** Measure campaign effectiveness.

```python
# Promo code impact
df.groupby("Promo Code Used")["Purchase Amount (USD)"] \
  .mean()
```

---

# 12. Which shipping option is most preferred?

**Business Decision:** Optimize logistics.

```python
# Shipping preference
df["Shipping Type"].value_counts()
```

---

# 13. Which shipping option attracts higher spending?

**Business Decision:** Offer premium shipping strategically.

```python
# Spend by shipping type
df.groupby("Shipping Type")["Purchase Amount (USD)"] \
  .mean() \
  .sort_values(ascending=False)
```

---

# 14. Are subscribers spending more?

**Business Decision:** Should we push subscriptions?

```python
# Subscriber value
df.groupby("Subscription Status")["Purchase Amount (USD)"] \
  .mean()
```

---

# 15. Which customers are most loyal?

**Business Decision:** Reward loyal customers.

```python
# Highest repeat purchasers
df.nlargest(10, "Previous Purchases")[
    ["Customer ID","Previous Purchases"]
]
```

---

# 16. Does loyalty lead to higher spending?

**Business Decision:** Build retention programs.

```python
# Correlation
df[["Previous Purchases",
    "Purchase Amount (USD)"]].corr()
```

---

# 17. Which colors are most popular?

**Business Decision:** Inventory planning.

```python
# Popular colors
df["Color"].value_counts().head(10)
```

---

# 18. Which sizes are most purchased?

**Business Decision:** Stock the right sizes.

```python
# Size demand
df["Size"].value_counts()
```

---

# 19. Which categories receive the highest ratings?

**Business Decision:** Learn what customers love.

```python
# Category satisfaction
df.groupby("Category")["Review Rating"] \
  .mean() \
  .sort_values(ascending=False)
```

---

# 20. Which customer segment is most valuable?

**Business Decision:** Focus marketing budget.

```python
# Revenue by gender and category
pd.pivot_table(
    df,
    values="Purchase Amount (USD)",
    index="Gender",
    columns="Category",
    aggfunc="sum"
)
```

---

# The Analyst Mental Model (Memorize This)

Whenever you receive a business dataset, ask:

### Revenue

```text
Who makes us money?
What makes us money?
Where does the money come from?
```

### Customers

```text
Who buys?
Who spends most?
Who is loyal?
Who is at risk of leaving?
```

### Products

```text
What sells most?
What sells least?
What brings most revenue?
```

### Marketing

```text
Do discounts work?
Do promo codes work?
Which campaigns perform best?
```

### Operations

```text
Which shipping method is preferred?
Which locations perform best?
What inventory should we stock?
```

### Customer Satisfaction

```text
Are customers happy?
Which products have better ratings?
What should be improved?
```

If you can answer these 6 areas during EDA, you'll already be thinking like a business analyst rather than someone who only produces charts.
