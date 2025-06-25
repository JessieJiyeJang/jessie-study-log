# 📘 38 SQL Interview Queries (FAANG + Tech Companies)

---

## ✅ 1. Find duplicate records in a table (Amazon)
```sql
SELECT column1, column2, COUNT(*)
FROM your_table
GROUP BY column1, column2
HAVING COUNT(*) > 1;
```

## ✅ 2. Retrieve the second highest salary (Microsoft)
```sql
SELECT MAX(salary) AS SecondHighestSalary
FROM Employee
WHERE salary < (SELECT MAX(salary) FROM Employee);
```

## ✅ 3. Find employees without department (Uber)
```sql
SELECT e.*
FROM Employee e
LEFT JOIN Department d ON e.department_id = d.department_id
WHERE d.department_id IS NULL;
```

## ✅ 4. Calculate total revenue per product (PayPal)
```sql
SELECT product_id,
       SUM(quantity * price) AS total_revenue
FROM Sales
GROUP BY product_id;
```

## ✅ 5. Get top 3 highest-paid employees (Google)
```sql
SELECT TOP 3 *
FROM Employee
ORDER BY salary DESC;
```

## ✅ 6. Customers who made purchases but never returned products (Walmart)
```sql
SELECT DISTINCT c.customer_id
FROM Customers c
JOIN Orders o ON c.customer_id = o.customer_id
WHERE c.customer_id NOT IN (
    SELECT customer_id FROM Returns
);
```

## ✅ 9. Average order value per customer (Microsoft)
```sql
SELECT customer_id,
       AVG(total_amount) AS avg_order_value
FROM Orders
GROUP BY customer_id;
```

## ✅ 10. Latest order placed by each customer (Uber)
```sql
SELECT customer_id,
       MAX(order_date) AS latest_order_date
FROM Orders
GROUP BY customer_id;
```

## ✅ 11. Products that were never sold (Adobe)
```sql
SELECT p.product_id
FROM Products p
LEFT JOIN Sales s ON p.product_id = s.product_id
WHERE s.product_id IS NULL;
```

## ✅ 12. Most selling product (Walmart)
```sql
SELECT TOP 1 product_id,
       SUM(quantity) AS total_qty
FROM Sales
GROUP BY product_id
ORDER BY total_qty DESC;
```

## ✅ 13. Total revenue and number of orders per region (Meta)
```sql
SELECT region,
       SUM(total_amount) AS total_revenue,
       COUNT(*) AS order_count
FROM Orders
GROUP BY region;
```

## ✅ 14. Customers with more than 5 orders (Amazon)
```sql
SELECT COUNT(*) AS customer_count
FROM (
    SELECT customer_id
    FROM Orders
    GROUP BY customer_id
    HAVING COUNT(*) > 5
) AS subquery;
```

## ✅ 15. Customers with orders above average value (PayPal)
```sql
SELECT *
FROM Orders
WHERE total_amount > (
    SELECT AVG(total_amount) FROM Orders
);
```

## ✅ 16. Employees hired on weekends (Google)
```sql
SELECT *
FROM Employee
WHERE DATENAME(WEEKDAY, hire_date) IN ('Saturday', 'Sunday');
```

## ✅ 19. Rank employees by salary within each department (Amazon)
```sql
SELECT employee_id, department_id, salary,
       RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS salary_rk
FROM Employee;
```

## ✅ 20. Customers who placed orders every month in 2023 (Meta)
```sql
SELECT customer_id
FROM Orders
WHERE YEAR(order_date) = 2023
GROUP BY customer_id
HAVING COUNT(DISTINCT FORMAT(order_date, 'yyyy-MM')) = 12;
```

## ✅ 21. Moving average of sales over the last 3 days (Microsoft)
```sql
SELECT order_date,
       AVG(total_amount) OVER (
           ORDER BY order_date
           ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
       ) AS moving_avg
FROM Orders;
```

## ✅ 22. First and last order date per customer (Uber)
```sql
SELECT customer_id,
       MIN(order_date) AS first_order,
       MAX(order_date) AS last_order
FROM Orders
GROUP BY customer_id;
```



## ✅ 23. Product sales distribution (% of total revenue) (PayPal)
```sql
WITH TotalRevenue AS (
  SELECT SUM(quantity * price) AS total FROM Sales
)
SELECT s.product_id,
       SUM(s.quantity * s.price) AS revenue,
       SUM(s.quantity * s.price) * 100.0 / t.total AS revenue_pct
FROM Sales s
CROSS JOIN TotalRevenue t
GROUP BY s.product_id, t.total;
```

## ✅ 24. Customers with 2-day consecutive purchases (Walmart)
```sql
WITH cte AS (
  SELECT id, order_date,
         LAG(order_date) OVER (PARTITION BY id ORDER BY order_date) AS prev_order_date
  FROM Orders
)
SELECT id, order_date, prev_order_date
FROM cte
WHERE DATEDIFF(DAY, prev_order_date, order_date) = 1;
```

## ✅ 25. Churned customers (no orders in 6 months) (Amazon)
```sql
SELECT customer_id
FROM Orders
GROUP BY customer_id
HAVING MAX(order_date) < DATEADD(MONTH, -6, GETDATE());
```

## ✅ 26. Cumulative revenue by day (Adobe)
```sql
SELECT order_date,
       SUM(total_amount) OVER (ORDER BY order_date) AS cumulative_revenue
FROM Orders;
```

## ✅ 27. Top departments by avg salary (Google)
```sql
SELECT department_id,
       AVG(salary) AS avg_salary
FROM Employee
GROUP BY department_id
ORDER BY avg_salary DESC;
```

## ✅ 28. Customers who ordered more than average (Meta)
```sql
WITH customer_orders AS (
  SELECT customer_id, COUNT(*) AS order_count
  FROM Orders
  GROUP BY customer_id
)
SELECT * 
FROM customer_orders
WHERE order_count > (
  SELECT AVG(order_count) FROM customer_orders
);
```

## ✅ 29. Revenue from first-time customers (Microsoft)
```sql
WITH first_orders AS (
  SELECT customer_id, MIN(order_date) AS first_order_date
  FROM Orders
  GROUP BY customer_id
)
SELECT SUM(o.total_amount) AS new_revenue
FROM Orders o
JOIN first_orders f ON o.customer_id = f.customer_id
WHERE o.order_date = f.first_order_date;
```

## ✅ 30. Percentage of employees per department (Uber)
```sql
SELECT department_id,
       COUNT(*) AS emp_count,
       COUNT(*) * 100.0 / (SELECT COUNT(*) FROM Employee) AS pct
FROM Employee
GROUP BY department_id;
```

## ✅ 31. Max salary difference per department (PayPal)
```sql
SELECT department_id,
       MAX(salary) - MIN(salary) AS salary_diff
FROM Employee
GROUP BY department_id;
```

## ✅ 32. Products that contribute to 80% revenue (Walmart)
```sql
WITH sales_cte AS (
  SELECT product_id, SUM(qty * price) AS revenue
  FROM Sales GROUP BY product_id
),
total_revenue AS (
  SELECT SUM(revenue) AS total FROM sales_cte
)
SELECT s.product_id, s.revenue,
       SUM(s.revenue) OVER (
         ORDER BY s.revenue DESC
         ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
       ) AS running_total
FROM sales_cte s, total_revenue t
WHERE SUM(s.revenue) OVER (
         ORDER BY s.revenue DESC
         ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
       ) <= t.total * 0.8;
```

## ✅ 33. Avg time between purchases per customer (Meta)
```sql
WITH cte AS (
  SELECT customer_id, order_date,
         LAG(order_date) OVER (PARTITION BY customer_id ORDER BY order_date) AS prev_date
  FROM Orders
)
SELECT customer_id,
       AVG(DATEDIFF(DAY, prev_date, order_date)) AS avg_gap_days
FROM cte
WHERE prev_date IS NOT NULL
GROUP BY customer_id;
```

## ✅ 34. Last purchase per customer (Google)
```sql
WITH ranked_orders AS (
  SELECT customer_id, order_id, total_amount,
         ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY order_date DESC) AS rn
  FROM Orders
)
SELECT customer_id, order_id, total_amount
FROM ranked_orders
WHERE rn = 1;
```

## ✅ 35. YoY growth in revenue (Microsoft)
```sql
SELECT FORMAT(order_date, 'yyyy') AS year,
       SUM(total_amount) AS revenue,
       SUM(total_amount) - LAG(SUM(total_amount)) OVER (
         ORDER BY FORMAT(order_date, 'yyyy')
       ) AS yoy_growth
FROM Orders
GROUP BY FORMAT(order_date, 'yyyy');
```

## ✅ 36. Customers with purchase above 90th percentile (Amazon)
```sql
WITH ranked_orders AS (
  SELECT customer_id, order_id, total_amount,
         NTILE(10) OVER (PARTITION BY customer_id ORDER BY total_amount) AS decile
  FROM Orders
)
SELECT customer_id, order_id, total_amount
FROM ranked_orders
WHERE decile = 10;
```

## ✅ 37. Longest gap between orders (Amazon)
```sql
WITH cte AS (
  SELECT customer_id, order_date,
         LAG(order_date) OVER (PARTITION BY customer_id ORDER BY order_date) AS prev_order_date
  FROM Orders
)
SELECT customer_id,
       MAX(DATEDIFF(DAY, prev_order_date, order_date)) AS max_gap
FROM cte
WHERE prev_order_date IS NOT NULL
GROUP BY customer_id;
```

## ✅ 38. Customers with revenue below 10th percentile (Google)
```sql
WITH cte AS (
  SELECT customer_id, SUM(total_amount) AS total_revenue
  FROM Orders
  GROUP BY customer_id
)
SELECT customer_id, total_revenue
FROM cte
WHERE total_revenue < (
  SELECT PERCENTILE_CONT(0.1) WITHIN GROUP (ORDER BY total_revenue)
  FROM cte
);
```
