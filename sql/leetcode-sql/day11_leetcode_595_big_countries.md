## 🧠 LeetCode – Big Countries  
🔗 [Problem Link](https://leetcode.com/problems/big-countries)

### 📌 Problem Summary  
You are given a table `World` with information about countries, including their area, population, and GDP.  
A country is considered **big** if it has:  
- an area of at least 3,000,000 km² **OR**  
- a population of at least 25,000,000.  

Return the **name**, **population**, and **area** of all big countries.

### 💡 SQL Concepts Used  
- `WHERE`: to filter rows based on area or population  
- Logical operator `OR`: to satisfy either of two conditions  
- Optional: Parentheses to improve readability of combined conditions

### ✅ My Solution (PostgreSQL)
```sql
SELECT name, population, area
FROM World
WHERE (area >= 3000000 OR population >= 25000000);
```

### 💬 What I Learned  
- `OR` allows you to define multiple conditions where at least one must be true.  
- Adding parentheses improves readability in complex `WHERE` clauses.  
- Simple conditional filters can be powerful when paired with well-structured data.
