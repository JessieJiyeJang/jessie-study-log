## 🧠 LeetCode – Followers Count  
🔗 https://leetcode.com/problems/followers-count/

### 📌 Problem Summary  
Given a table `Followers`, return the number of followers each user has.  
Each row indicates that `follower_id` follows `user_id`.  
Return the result sorted by `user_id` in ascending order.

---

### 💡 SQL Concepts Used  
- `COUNT(DISTINCT ...)` to count unique followers  
- `GROUP BY` to aggregate follower counts per user  
- `ORDER BY` to sort results  
- Primary key note: `(user_id, follower_id)` ensures no duplicate entries

---

### ✅ My Final Solution (MySQL)
```sql
# Write your MySQL query statement below
SELECT 
  user_id, 
  COUNT(DISTINCT follower_id) AS followers_count
FROM Followers
GROUP BY user_id
ORDER BY user_id;
```

---

### 💬 What I Learned  
- Simple `GROUP BY` with aggregate functions can summarize relationships effectively.  
- Using `DISTINCT` inside `COUNT()` ensures that only **unique** followers are counted (important in case of future data changes).  
- Always remember to `ORDER BY` as specified in the problem.

---

### 🛠️ Room for Improvement  
- In a large-scale system, indexing `user_id` or `follower_id` may improve performance.  
- For users with no followers, if needed, an `OUTER JOIN` with a user list would be required — but that is not necessary in this problem.

---

### 📈 Time & Space Complexity
- Time Complexity: **O(n log n)** (due to `GROUP BY` + `ORDER BY` on indexed table)  
- Space Complexity: **O(n)** (to store intermediate grouping and output)
