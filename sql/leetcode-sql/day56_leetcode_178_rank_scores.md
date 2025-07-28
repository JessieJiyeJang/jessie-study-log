## 🧠 LeetCode – Rank Scores  
🔗 https://leetcode.com/problems/rank-scores

### 📌 Problem Summary  
You're given a table `Scores` where each row contains a player's score (to two decimal places).  
Your task is to assign a **ranking** to each score with the following rules:
- Higher scores should receive a better (lower) rank
- If multiple players have the same score, they share the same rank
- The next rank after a tie should be the next consecutive number (no gaps)

Return the result table ordered by score descending.

### 💡 SQL Concepts Used  
- `DENSE_RANK()` window function to assign consecutive ranks without gaps  
- `OVER (ORDER BY score DESC)` to rank from highest to lowest  
- `ORDER BY` ensures the output is sorted by score descending  

### ✅ My Final Solution (PostgreSQL-compatible)

    SELECT 
        score, 
        DENSE_RANK() OVER (ORDER BY score DESC) AS rank
    FROM scores;

### 💬 What I Learned  
- `DENSE_RANK()` is ideal when handling ties but still needing **continuous** ranking values  
- Contrast this with `RANK()`, which would skip numbers after ties (e.g., ranks: 1, 1, 3, 4...)  
- Window functions allow you to compute rank **without grouping or losing row-level detail**

### 🛠️ Room for Improvement  
- If additional player info were included, you could also partition the ranking by player group using `PARTITION BY`  
- If a fixed limit (like top 3 ranks) was needed, you could wrap this in a CTE and apply a `WHERE` filter
- 
