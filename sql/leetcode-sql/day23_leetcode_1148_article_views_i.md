## 🧠 LeetCode – Article Views I (Self-Viewed Articles)  
🔗 [Problem Link](https://leetcode.com/problems/article-views-i)

### 📌 Problem Summary  
You're given a table `Views` that tracks which users viewed which articles.  
Return all authors who have **viewed at least one of their own articles**, i.e., cases where `author_id = viewer_id`.

The result must be sorted in ascending order by ID.

### 💡 SQL Concepts Used  
- `WHERE`: to filter rows where author and viewer are the same  
- `DISTINCT`: to return each author's ID only once  
- `ORDER BY`: to meet the required output order

### ✅ My Solution (PostgreSQL)
```sql
SELECT DISTINCT author_id AS id
FROM Views
WHERE author_id = viewer_id
ORDER BY id;
```

### 💬 What I Learned  
- Comparing two columns in the same table is a powerful way to find self-references.  
- `DISTINCT` is useful when dealing with data that allows duplicate rows.  
- Always check if the output requires sorting — even if not explicitly mentioned in the query logic.
