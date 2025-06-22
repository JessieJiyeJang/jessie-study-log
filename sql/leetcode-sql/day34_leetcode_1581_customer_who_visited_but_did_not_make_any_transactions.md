## 🧠 LeetCode – Customer Who Visited but Did Not Make Any Transactions  
🔗 [Problem Link](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions)

### 📌 Problem Summary  
You're given two tables: `Visits` and `Transactions`.  
Return the `customer_id` and the number of times (`count_no_trans`) they visited **without** making a transaction.

### 💡 SQL Concepts Used  
- `LEFT JOIN`: to include all visits even if there's no matching transaction  
- `IS NULL`: to filter out rows where a transaction didn’t exist  
- `GROUP BY`: to count how many non-transaction visits each customer made  
- `COUNT(*)`: counts rows when conditionally filtered using `IS NULL`

### ✅ My Final Solution (PostgreSQL)

```sql
SELECT v.customer_id, COUNT(*) AS count_no_trans
FROM Visits v
LEFT JOIN Transactions t ON v.visit_id = t.visit_id
WHERE t.transaction_id IS NULL
GROUP BY v.customer_id;
```

### 💬 What I Learned  
- `NOT IN` is **not NULL-safe**. If any value inside the subquery is NULL, the whole filter can fail silently.  
- `LEFT JOIN ... IS NULL` is the preferred way to find unmatched records between two tables.  
- `COUNT(*)` is used here because `customer_id` is always present in `Visits`.  

### ⚠️ My Initial (Buggy) Attempt  

```sql
SELECT customer_id, COUNT(customer_id) AS count_no_trans
FROM Visits
WHERE visit_id NOT IN (
SELECT visit_id
FROM transactions
)
GROUP BY customer_id;
```

### ❌ Problem with This Approach  
- If **any** `visit_id` in `Transactions` is `NULL`, `NOT IN` fails due to three-valued logic in SQL.  
- It's safer to avoid `NOT IN` when the subquery might include `NULL`.
