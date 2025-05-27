## 🧠 LeetCode – Find Customer Referee  
🔗 [Problem Link](https://leetcode.com/problems/find-customer-referee)

### 📌 Problem Summary  
You are given a table `Customer` where each customer may or may not have a referee.  
The task is to **find all customer names whose referee is not the customer with id = 2**, including customers who were not referred by anyone (`referee_id IS NULL`).

### 💡 SQL Concepts Used  
- `WHERE`: to filter rows based on conditions  
- `COALESCE`: to handle `NULL` values by substituting them with a default for comparison

### ✅ My Solution (PostgreSQL)
```sql
SELECT name
FROM customer
WHERE COALESCE(referee_id, 0) != 2;
```

### 🛠 Improvement Suggestion  
- In PostgreSQL, you can use the `IS DISTINCT FROM` operator, which is a NULL-safe alternative to `!=`.
- Unlike `!=`, it treats `NULL` values as valid and allows safe comparison.
- Using this operator, the same logic can be expressed more clearly without needing `COALESCE()`:

```sql
SELECT name
FROM customer
WHERE referee_id IS DISTINCT FROM 2;
```
- This improves readability and ensures correct results when dealing with `NULL` values.

### 💬 What I Learned
- `COALESCE()` is useful when comparing values that may be `NULL`, by replacing them with a default (e.g. `0`).
- In PostgreSQL, `IS DISTINCT FROM` provides a cleaner way to perform `NULL`-safe comparisons.
- In SQL, expressions like `referee_id != 2` will ignore `NULL` rows unless handled explicitly with `COALESCE` or `IS NULL`
