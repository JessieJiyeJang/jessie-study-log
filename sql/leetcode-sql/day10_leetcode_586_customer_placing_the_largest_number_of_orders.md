## 🧠 LeetCode – Customer Placing the Largest Number of Orders  
🔗 [Problem Link](https://leetcode.com/problems/customer-placing-the-largest-number-of-orders)

### 📌 Problem Summary  
You're given a table `Orders` with customer and order information.  
Return the `customer_number` of the customer who placed the **most orders**.  
It is guaranteed that exactly one customer placed more orders than anyone else.  

Follow-up: If there are multiple top customers with the same highest number of orders, return **all of them**.

### 💡 SQL Concepts Used  
- `GROUP BY`: to count orders per customer  
- `COUNT()`: to calculate number of orders  
- `ORDER BY` + `LIMIT`: to return the top record  
- `MAX()`: to identify the highest order count  
- CTEs (`WITH`): to break down steps for clarity

### ✅ My Solution (PostgreSQL – Original Constraint)
```sql
WITH order_table AS (
    SELECT customer_number, COUNT(order_number) AS order_count
    FROM Orders
    GROUP BY customer_number
)
SELECT customer_number
FROM order_table
ORDER BY order_count DESC
LIMIT 1;
```

### 💬 What I Learned  
- Aggregation using `GROUP BY` and `COUNT()` helps identify totals per group.  
- `LIMIT` can be used after `ORDER BY` to return only the top result.  
- Meaningful aliases like `order_count` improve readability.  
- I also learned how to handle the follow-up case when multiple customers tie for first.

### 🔄 Follow-Up: Return All Top Customers (if tie)
```sql
WITH order_table AS (
    SELECT customer_number, COUNT(*) AS order_count
    FROM Orders
    GROUP BY customer_number
),
max_count AS (
    SELECT MAX(order_count) AS max_order
    FROM order_table
)
SELECT customer_number
FROM order_table
WHERE order_count = (SELECT max_order FROM max_count);
```
