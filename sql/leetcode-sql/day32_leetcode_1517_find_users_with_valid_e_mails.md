## 📧 LeetCode – Valid Emails  
🔗 [Problem Link](https://leetcode.com/problems/find-users-with-valid-e-mails)

### 📌 Problem Summary  
Find users whose email is valid according to the following rules:
- Prefix must start with a **letter**
- Prefix may contain: letters, digits, underscore `_`, period `.`, or dash `-`
- Domain must be `@leetcode.com`

### ✅ SQL Concepts Used  
- Regular Expression Matching (`~` in PostgreSQL)  
- Anchors: `^` (start), `$` (end)  
- Escape characters (`\.` to match literal `.`)

### 💡 Solution (PostgreSQL)
```sql
SELECT user_id, name, mail
FROM Users
WHERE mail ~ '^[A-Za-z][A-Za-z0-9_.-]*@leetcode\.com$';
```

### 💬 What I Learned  
- How to validate email with regex in SQL  
- The importance of anchoring (`^`, `$`) for exact match  
- How to escape dot (`.`) in regex  
