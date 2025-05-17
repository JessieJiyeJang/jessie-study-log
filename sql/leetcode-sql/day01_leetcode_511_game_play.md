# 🧠 LeetCode 511 – Game Play Analysis I

🔗 [Problem link](https://leetcode.com/problems/game-play-analysis-i/)

## 📌 Problem Summary
You are given an `Activity` table that logs player sessions.  
Your task is to find the **first login date for each player**.

---

## 💡 SQL Concepts Used
- `GROUP BY`: to group records by `player_id`
- `MIN()`: to get the earliest login date
- `AS`: to rename the output column (`first_login`)

---

## ✅ My Solution

```sql
SELECT 
    player_id, 
    MIN(event_date) AS first_login
FROM 
    Activity
GROUP BY 
    player_id;

```

## 💬 What I Learned
- You can use `MIN()` with date columns just like numbers.
- `GROUP BY` with aggregate functions is essential for summarizing grouped data.
- Renaming columns using `AS` makes results clearer and readable.
