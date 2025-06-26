
## 🧠 LeetCode – Unique Leads and Partners  
🔗 https://leetcode.com/problems/unique-leads-and-partners

### 📌 Problem Summary  
You're given a `DailySales` table that logs each sale by `date_id`, `make_name`, `lead_id`, and `partner_id`.  
Your task is to **group by `date_id` and `make_name`**, and return:  
- `unique_leads`: the number of **distinct lead_id** values  
- `unique_partners`: the number of **distinct partner_id** values  

### 💡 SQL Concepts Used  
- `GROUP BY`: to group data by `date_id` and `make_name`  
- `COUNT(DISTINCT ...)`: to count unique values within each group  
- No `ORDER BY` required as result can be in any order

### ✅ My Final Solution (PostgreSQL-compatible)
```sql
SELECT  
  date_id,  
  make_name,  
  COUNT(DISTINCT lead_id) AS unique_leads,  
  COUNT(DISTINCT partner_id) AS unique_partners  
FROM DailySales  
GROUP BY date_id, make_name;
```

### 💬 What I Learned  
- `COUNT(DISTINCT column)` is useful when tracking **unique interactions** within grouped data.  
- Even if the table contains duplicates, `DISTINCT` ensures accuracy.  
- Always verify the **grouping keys** match the aggregation goal — here, `date_id` and `make_name`.
