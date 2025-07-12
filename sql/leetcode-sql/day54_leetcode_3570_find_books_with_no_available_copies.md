## 🧠 LeetCode – Fully Borrowed Books  
🔗 https://leetcode.com/problems/books-currently-borrowed-and-unavailable

### 📌 Problem Summary  
You are given two tables:
- `library_books`: contains all books and how many total copies exist
- `borrowing_records`: contains borrowing history, including whether the book has been returned (via `return_date`)  

Your task is to:
- Find all books that are currently borrowed (`return_date IS NULL`)  
- And have **zero available copies** in the library  
- Return the result ordered by number of current borrowers in descending order, and book title in ascending order

### 💡 SQL Concepts Used  
- `JOIN` to combine book and borrow data  
- `FILTER` inside `COUNT()` to count only currently borrowed books  
- `CTE (WITH)` to simplify and organize logic  
- `ORDER BY` with multiple conditions  

### ✅ My Final Solution (PostgreSQL-compatible)
```sql
    WITH borrowers AS (
        SELECT 
            l.*, 
            COUNT(b.book_id) FILTER (WHERE b.return_date IS NULL)
        FROM library_books l
        JOIN borrowing_records b ON l.book_id = b.book_id
        GROUP BY 
            b.book_id, l.book_id, l.title, l.author, 
            l.genre, l.publication_year, l.total_copies
    )
    
    SELECT 
        book_id, 
        title, 
        author, 
        genre, 
        publication_year, 
        count AS current_borrowers
    FROM borrowers
    WHERE total_copies - count = 0
    ORDER BY count DESC, title ASC;
```
### 💬 What I Learned  
- `COUNT(column)` only counts non-null values in that column  
- In this specific problem, since `book_id` is always present, it works correctly  
- The `FILTER` clause allows conditional aggregation within `COUNT()`  

### 🛠️ Room for Improvement  
- A more reliable alternative in real-world scenarios is to use:  
  
      COUNT(*) FILTER (WHERE return_date IS NULL)
  
- This counts the total number of **rows**, regardless of whether any particular column contains a `NULL`  
- It’s a safer and more robust approach in case any fields (like `book_id` or `borrower_name`) might be `NULL`
