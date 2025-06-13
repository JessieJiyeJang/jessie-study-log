## 🧠 LeetCode – Average Selling Price  
🔗 [Problem Link](https://leetcode.com/problems/average-selling-price)

### 📌 Problem Summary  
You are given:
- A `Prices` table showing the price of a product during a given date range  
- A `UnitsSold` table showing units sold on a particular date

Your goal is to return the **average selling price** per product:

```
average_price = total revenue / total units sold
```

- If no units were sold for a product, its average_price should be `0.00`.
- Result should be rounded to 2 decimal places.

### 💡 SQL Concepts Used  
- `LEFT JOIN`: to include products with 0 sales  
- `FILTER`: to ensure the price matches the purchase date range  
- `COALESCE()`: to replace NULLs with 0  
- `NULLIF(SUM(units), 0)`: to avoid division by 0  
- `ROUND(..., 2)`: to round to 2 decimal places

### ✅ My Solution (PostgreSQL)
```sql
WITH combined_price_table AS (
    SELECT 
        p.product_id,
        u.purchase_date,
        COALESCE(u.units, 0) AS units,
        COALESCE(
            MAX(p.price) FILTER (
                WHERE u.purchase_date BETWEEN p.start_date AND p.end_date
            ), 
            0
        ) AS price
    FROM Prices p
    LEFT JOIN UnitsSold u ON p.product_id = u.product_id 
    GROUP BY p.product_id, u.purchase_date, u.units
)

SELECT 
    product_id, 
    COALESCE(
        ROUND(SUM(units * price) / NULLIF(SUM(units), 0)::NUMERIC, 2),
        0
    ) AS average_price
FROM combined_price_table
GROUP BY product_id;
```

### 💬 What I Learned  
- `NULLIF(x, 0)` is useful to prevent division-by-zero errors.  
- Wrapping that with `COALESCE(..., 0)` ensures a safe fallback value.  
- `FILTER (WHERE ...)` is a powerful tool for conditional aggregation.  
- Even complex logic can be broken down cleanly with a `WITH` clause.
