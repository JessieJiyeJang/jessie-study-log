## 🧠 LeetCode – Find Low Fat and Recyclable Products  
🔗 https://leetcode.com/problems/find-products-that-are-both-low-fat-and-recyclable/

### 📌 Problem Summary  
You are given a table `Products` with information about food items.  
Return the `product_id` of products that are both **low fat** (`low_fats = 'Y'`) and **recyclable** (`recyclable = 'Y'`).

---

### 💡 SQL Concepts Used  
- `WHERE` clause for conditional filtering  
- Logical operator `AND` to satisfy both conditions simultaneously  
- Simple `SELECT` for specific column

---

### ✅ My Final Solution (MySQL)
```sql
SELECT product_id
FROM Products
WHERE low_fats = 'Y' AND recyclable = 'Y';
```

---

### 💬 What I Learned  
- Basic filtering using `WHERE` is powerful for categorical fields like ENUMs.  
- Chaining conditions with `AND` allows for precise row selection.  
- Clean and readable query for simple filtering logic.

---

### 🛠️ Room for Improvement  
- This solution is already optimal for the problem size and schema.  
- If the table becomes large, indexing `low_fats` and `recyclable` could speed up filtering.  
- `ENUM` columns behave like strings, so character comparison is valid and efficient.

---

### 📈 Time & Space Complexity
- Time Complexity: **O(n)** — linear scan for filtering rows (unless indexed)  
- Space Complexity: **O(1)** — output space only
