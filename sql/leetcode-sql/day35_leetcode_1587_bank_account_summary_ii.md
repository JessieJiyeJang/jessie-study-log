## 🧠 LeetCode – Bank Account Summary II  
🔗 https://leetcode.com/problems/bank-account-summary-ii

### 📌 Problem Summary  
You're given two tables: `Users` and `Transactions`.  
Return the `name` and total `balance` for users whose account balance exceeds **10,000**.  
Balance is the sum of all `amount`s (positive for deposits, negative for withdrawals).

### 💡 SQL Concepts Used  
- `JOIN`: to combine user info with their transactions  
- `GROUP BY`: to calculate total balance per user  
- `HAVING`: to filter groups after aggregation  
- `SUM()`: to calculate total account balance

### ✅ My Final Solution (PostgreSQL-compatible)
```sql
SELECT 
  u.name, 
  SUM(t.amount) AS balance
FROM Users u
JOIN Transactions t 
  ON u.account = t.account
GROUP BY u.name
HAVING SUM(t.amount) > 10000;
```

### 💬 What I Learned  
- You **must** use `HAVING` (not `WHERE`) when filtering by aggregate results like `SUM()`.  
- It's better to `GROUP BY u.name` instead of `u.account, u.name` when `name` is unique (as per problem statement).  
- Always check for **uniqueness guarantees** in the problem description to simplify your query.

### ⚠️ My Initial Query (Still Correct but Slightly Verbose)
SELECT u.name, SUM(t.amount) AS balance
FROM Users u
JOIN Transactions t ON u.account = t.account
GROUP BY u.account, u.name
HAVING SUM(t.amount) > 10000;

### 🛠️ Why I Improved It  
- Since `name` is unique, grouping by both `account` and `name` is redundant.  
- Simpler `GROUP BY u.name` is equally correct and easier to read.
