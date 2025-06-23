## 🧠 LeetCode – Percentage of Users Attended a Contest  
🔗 https://leetcode.com/problems/percentage-of-users-attended-a-contest

### 📌 Problem Summary  
You're given two tables: `Users` and `Register`.  
Return the `contest_id` and percentage of users registered in each contest, rounded to **two decimal places**.  
Sort the result by `percentage` in **descending** order, and by `contest_id` in **ascending** order in case of ties.

### 💡 SQL Concepts Used  
- `COUNT()` to get the number of users per contest  
- Subquery to get the **total user count**  
- `ROUND()` to round percentages  
- Arithmetic with `* 100.0` to avoid integer division  
- `GROUP BY` and `ORDER BY` for grouping and sorting

### ✅ My Final Solution (PostgreSQL-compatible)
```sql
SELECT  
  contest_id,  
  ROUND((COUNT(user_id) * 100.0) / (SELECT COUNT(*) FROM Users), 2) AS percentage  
FROM Register  
GROUP BY contest_id  
ORDER BY percentage DESC, contest_id ASC;
```

### 💬 What I Learned  
- In PostgreSQL, multiplying by `100.0` instead of using `::numeric` is a simpler way to ensure **floating-point division**.  
- `ROUND(number, 2)` helps cleanly display results to 2 decimal places.  
- A scalar subquery can be used directly in a SELECT clause to provide a global constant (like total users).  
- When calculating percentages, be mindful of **integer division pitfalls** — use floats or decimal values explicitly.

### ⚠️ My Initial Query (Still Works but Can Be Improved)
SELECT  
  contest_id,  
  ROUND((COUNT(user_id) / (SELECT COUNT(user_id) FROM Users)::NUMERIC), 4) * 100 AS percentage  
FROM Register  
GROUP BY contest_id  
ORDER BY percentage DESC, contest_id ASC;

### 🛠️ Why I Improved It  
- Using `* 100.0` instead of casting is **cleaner** and avoids an extra `::NUMERIC` cast.  
- Reducing `ROUND(..., 4) * 100` to `ROUND(..., 2)` simplifies the rounding logic and is more accurate for percentages.  
- Small tweaks can make a query **easier to read and maintain** without changing correctness.
