# Bitcoin Study Case - Code Overview

This document provides an overview of the code I used to create the visualizations, perform the analysis, and clean the data for the **Bitcoin Study Case** project.

---

## 1. Bitcoin Halving Events

### Data on Bitcoin Halving Events
The table below summarizes the Bitcoin halving events and the corresponding mining rewards:

| Year | Mining Reward (BTC) |
|------|---------------------|
| 2012 | 25                  |
| 2016 | 12.5                |
| 2020 | 6.25                |
| 2024 | 3.125               |
| 2028 | 1.5625              |
| 2032 | 0.78125             |
| 2036 | 0.390625            |

### Visualization of Bitcoin Halving Events
Below is the Python code used to visualize Bitcoin halving events:

```python
import matplotlib.pyplot as plt

# Data for halving events
years = [2012, 2016, 2020, 2024, 2028, 2032, 2036]
rewards = [25, 12.5, 6.25, 3.125, 1.5625, 0.78125, 0.390625]

# Plot the data
plt.figure(figsize=(10, 6))
plt.plot(years, rewards, marker='o', color='orange')
plt.title('Bitcoin Halving Events and Mining Rewards')
plt.xlabel('Year')
plt.ylabel('Mining Reward (BTC)')
plt.grid(True)
plt.show()
```

---

## 2. Bitcoin vs. Fiat Currency Comparison

### Data on Bitcoin vs. Fiat Currency
The table below compares Bitcoin with fiat currencies based on key criteria:

| Criteria         | Bitcoin          | Fiat Currency           |
|------------------|------------------|-------------------------|
| Control          | Decentralized    | Centralized (government/banks) |
| Supply           | Limited (21 million) | Unlimited (can be printed) |
| Transparency     | Public, blockchain-based | Private, bank records |
| Transaction Fees | Generally lower  | Higher (3rd party involved) |
| Inflation        | Resistant due to limited supply | Prone to inflation |

### Visualization of Bitcoin vs. Fiat Currency
Below is the Python code used to create a bar chart comparing Bitcoin and fiat currency:

```python
import matplotlib.pyplot as plt

# Data for comparison
criteria = ['Control', 'Supply', 'Transparency', 'Transaction Fees', 'Inflation']
bitcoin = [10, 10, 10, 9, 10]  # Scores for Bitcoin (0-10)
fiat = [2, 1, 3, 4, 2]         # Scores for Fiat (0-10)

# Plot the data
plt.figure(figsize=(12, 6))
bar_width = 0.35
index = range(len(criteria))

plt.bar(index, bitcoin, width=bar_width, label='Bitcoin', color='blue')
plt.bar([i + bar_width for i in index], fiat, width=bar_width, label='Fiat Currency', color='grey')

plt.title('Bitcoin vs. Fiat Currency Comparison')
plt.xlabel('Criteria')
plt.ylabel('Score (0-10)')
plt.xticks([i + bar_width / 2 for i in index], criteria)
plt.legend()
plt.show()
```

---

## 3. Return on Investment (ROI) Comparison

### ROI Calculation
The following Python code calculates and visualizes the ROI for Bitcoin, Gold, and the S&P 500 over a specified period:

```python
import matplotlib.pyplot as plt

# ROI data (in percentage)
assets = ['Bitcoin', 'Gold', 'S&P 500']
roi = [450, 50, 30]  # Example ROI values

# Plot the data
plt.figure(figsize=(8, 6))
plt.bar(assets, roi, color=['orange', 'gold', 'green'])
plt.title('ROI Comparison: Bitcoin vs. Gold vs. S&P 500')
plt.xlabel('Asset')
plt.ylabel('ROI (%)')
plt.show()
```

---

## 4. Real-Life Use Cases of Bitcoin

### Visualization of Bitcoin Adoption Growth
The following Python code illustrates the increasing adoption of Bitcoin by companies and institutions:

```python
import matplotlib.pyplot as plt

# Data for adoption
years = [2015, 2018, 2021, 2024]
adoption_rate = [10, 30, 60, 90]  # Example adoption rates in percentage

# Plot the data
plt.figure(figsize=(10, 6))
plt.plot(years, adoption_rate, marker='o', color='green')
plt.title('Bitcoin Adoption Growth (2015-2024)')
plt.xlabel('Year')
plt.ylabel('Adoption Rate (%)')
plt.grid(True)
plt.show()
```

## 5. SQL Queries for Data Cleaning
Below are some SQL queries I used for cleaning and preparing the data:

### Removing Duplicates
This query removes duplicate rows from the Bitcoin transactions table:

```sql
DELETE FROM bitcoin_transactions
WHERE id NOT IN (
    SELECT MIN(id)
    FROM bitcoin_transactions
    GROUP BY transaction_hash
);
```

### Handling Missing Values
This query fills in missing values in the `transaction_fee` column with the average fee:

```sql
UPDATE bitcoin_transactions
SET transaction_fee = (
    SELECT AVG(transaction_fee)
    FROM bitcoin_transactions
)
WHERE transaction_fee IS NULL;
```

### Filtering Relevant Data
This query filters transactions with a value greater than 0.01 BTC:

```sql
SELECT *
FROM bitcoin_transactions
WHERE transaction_value > 0.01;
```

---
