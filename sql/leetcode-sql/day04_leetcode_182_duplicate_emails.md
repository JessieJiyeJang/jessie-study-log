
## 🧠 LeetCode – Duplicate Emails  
🔗 [Problem Link](https://leetcode.com/problems/duplicate-emails)

### 📌 Problem Summary  
You are given a table `Person` with columns `id` and `email`.  
Each row represents a person’s email address, and you are to **return all email addresses that appear more than once** in the table.

### 💡 SQL Concepts Used  
- `GROUP BY`: to group records with the same email address  
- `HAVING COUNT(*) > 1`: to filter only the emails that appear more than once  
- `SELECT`: to return just the duplicate email addresses

### ✅ My Solution  
```sql
SELECT email
FROM person
GROUP BY email
HAVING COUNT(email) > 1;

```
###  💬 What I Learned
- `GROUP BY` combined with `HAVING` is a powerful tool for identifying duplicates.
- `HAVING` is used to filter groups after aggregation, unlike `WHERE` which filters individual rows.
- This approach is efficient and readable, especially when handling duplicate detection in datasets.
