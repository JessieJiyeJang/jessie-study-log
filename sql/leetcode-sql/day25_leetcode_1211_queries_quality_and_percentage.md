## 🧠 LeetCode – Search Queries Quality and Performance  
🔗 [Problem Link](https://leetcode.com/problems/search-queries-quality-and-performance)

### 📌 Problem Summary  
You're given a table `Queries` containing search result rankings and ratings.  
For each `query_name`, return:
- `quality`: the average of `rating / position`, rounded to 2 decimal places  
- `poor_query_percentage`: the percentage of queries with rating < 3, rounded to 2 decimal places

### 💡 SQL Concepts Used  
- `WITH` (CTE): to simplify multi-step aggregations  
- `FILTER`: to count conditionally inside aggregates  
- `SUM()`, `COUNT()`: for computing totals and sub-counts  
- `ROUND()`: to format decimal results  
- Type casting using `::NUMERIC` for accurate division

### ✅ My Solution (PostgreSQL)
```sql
WITH rating_queries AS (
    SELECT 
        query_name,
        COUNT(query_name) AS numbers,
        COUNT(rating) FILTER (WHERE rating < 3) AS poor_query,
        SUM(rating / position::NUMERIC) AS quality_number
    FROM Queries
    GROUP BY query_name
)
SELECT 
    query_name, 
    ROUND(quality_number / numbers::NUMERIC, 2) AS quality, 
    ROUND((poor_query::NUMERIC / numbers) * 100, 2) AS poor_query_percentage
FROM rating_queries
ORDER BY quality DESC;
```

### 💬 What I Learned  
- `FILTER` is a great tool for condition-based aggregations inside `COUNT()` or `SUM()`.  
- Using `::NUMERIC` ensures accurate division when working with integer columns.  
- Common Table Expressions (CTEs) like `WITH` help organize multi-step aggregations cleanly.  
- Rounding values properly is key to matching expected result formats.

