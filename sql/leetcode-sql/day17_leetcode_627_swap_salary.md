## 🧠 LeetCode – Swap Salary  
🔗 [Problem Link](https://leetcode.com/problems/swap-salary)

### 📌 Problem Summary  
You're given a `Salary` table with a `sex` column having values `'m'` or `'f'`.  
Write a **single `UPDATE` query** (no `SELECT`, no temp tables) that **swaps** all `'m'` values to `'f'` and all `'f'` values to `'m'`.

### 💡 SQL Concepts Used  
- `UPDATE`: to modify values in-place  
- `CASE WHEN`: to apply conditional updates  
- No intermediate table, no subquery, and no SELECT allowed

### ✅ My Solution (PostgreSQL)
```sql
UPDATE Salary
SET sex = CASE 
             WHEN sex = 'm' THEN 'f'
             WHEN sex = 'f' THEN 'm'
          END;
```

### 💬 What I Learned  
- `CASE WHEN` is useful for conditional value replacement directly in an `UPDATE`.  
- You can update multiple rows conditionally without using `SELECT` or temporary structures.  
- SQL logic is often cleaner and more efficient when kept set-based and declarative.

