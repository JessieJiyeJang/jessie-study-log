## 🧠 LeetCode – Combine Two Tables  
🔗 [Problem Link](https://leetcode.com/problems/combine-two-tables)

### 📌 Problem Summary  
You are given two tables: `Person` and `Address`.  
Return each person’s `firstName`, `lastName`, `city`, and `state`.  
If the person has no address, return `null` for `city` and `state`.

### 💡 SQL Concepts Used  
- `LEFT JOIN`: to return all rows from the `Person` table even if there is no matching address  
- `ON`: to specify the join condition using `personId`  
- `NULL`: used when no match is found in the `Address` table

### ✅ My Solution  
```sql
SELECT 
    person.firstName, 
    person.lastName, 
    address.city, 
    address.state
FROM 
    Person
LEFT JOIN 
    Address 
ON 
    person.personId = address.personId;
```

### 💬 What I Learned
- `LEFT JOIN` is perfect when you want to include all records from one table regardless of matches in the other.
-  It's important to join on the correct key (`personId` here).
-  Using table aliases or formatting helps keep queries cleaner and more readable.
