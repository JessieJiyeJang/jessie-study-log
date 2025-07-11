## 🧠 LeetCode – Products With a Valid Serial Number  
🔗 https://leetcode.com/problems/products-with-a-valid-serial-number

### 📌 Problem Summary  
You're given a table `products` with columns `product_id`, `product_name`, and `description`.  
Your task is to find all products whose `description` contains a valid **serial number**, which must:  
- Start with `"SN"` (case-sensitive)  
- Be followed by **exactly 4 digits**  
- Then a hyphen `-`  
- Then **exactly 4 more digits**  
- Appear **anywhere** in the description  

Return results ordered by `product_id` in ascending order.

### 💡 SQL Concepts Used  
- Regular expression matching using `~` in PostgreSQL  
- `\m` and `\M` to ensure word boundaries (start and end of the serial)  
- `{4}` to specify **exact digit count**  
- `ORDER BY` to sort results  

### ✅ My Final Solution (PostgreSQL-compatible)
```sql
    SELECT product_id, product_name, description
    FROM products
    WHERE description ~ '\mSN[0-9]{4}-[0-9]{4}\M'
    ORDER BY product_id;
```
### 💬 What I Learned  
- `\m` and `\M` in PostgreSQL are used for **word boundaries**:  
  - `\m` ensures the match starts at the beginning of a word  
  - `\M` ensures the match ends at the end of a word  
- Using both prevents partial matches like `SN1234-56789` from being incorrectly accepted  
- `{n}` syntax is essential for defining exact repetition in regular expressions  

### 🛠️ Room for Improvement  
- If PostgreSQL is not available, use `SIMILAR TO` or `LIKE` cautiously (they're limited)  
- Lookahead/lookbehind (`(?<!\d)` and `(?!\d)`) could be used as alternatives if needed  
- For performance, consider full-text search or pattern indexing if data size is large
