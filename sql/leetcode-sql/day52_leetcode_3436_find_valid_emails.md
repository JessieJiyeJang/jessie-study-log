## 🧠 LeetCode – Valid Email Addresses  
🔗 https://leetcode.com/problems/valid-email-addresses

### 📌 Problem Summary  
You're given a table `Users` containing user IDs and email addresses.  
Your task is to return all **valid** emails that satisfy the following rules:  
- Must contain **exactly one '@'** symbol  
- Must **end with `.com`**  
- The **local part** (before `@`) must only contain **alphanumeric characters and underscores**  
- The **domain part** (after `@` and before `.com`) must contain **only letters**  

Return the result ordered by `user_id` ascending.

### 💡 SQL Concepts Used  
- Regular expressions with `~` operator in PostgreSQL  
- `^` and `$` anchors to ensure the entire string matches  
- Character classes `[A-Za-z0-9_]` and `[A-Za-z]+` to validate local and domain parts  
- `ORDER BY` for sorted output  

### ✅ My Final Solution (PostgreSQL-compatible)
```sql
    SELECT user_id, email
    FROM Users
    WHERE email ~ '^[A-Za-z0-9_]+@[A-Za-z]+\.com$'
    ORDER BY user_id ASC;
```
### 💬 What I Learned  
- The `~` operator in PostgreSQL is used to apply case-sensitive regular expressions.  
- Anchors `^` and `$` are crucial to ensure that **the entire email** matches the desired format.  
- Carefully crafting character classes ensures strict format enforcement.  

### 🛠️ Room for Improvement  
- If case insensitivity is required, you can use `~*` instead of `~`.  
- For more advanced validation (e.g., subdomains or longer TLDs), you’d need more complex regex.
