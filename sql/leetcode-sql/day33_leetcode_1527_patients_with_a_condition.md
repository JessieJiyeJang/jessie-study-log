## 🩺 LeetCode SQL – Patients With Type I Diabetes  
🔗 [Problem Link](https://leetcode.com/problems/patients-with-a-condition/)

### 📌 Problem Summary  
Find patients whose `conditions` include **Type I Diabetes**, which always starts with the prefix `'DIAB1'`.  
The `conditions` column is a space-separated string of medical codes.

---

### ✅ PostgreSQL Solution
```sql
SELECT patient_id, patient_name, conditions
FROM Patients
WHERE conditions ~ '(^| )DIAB1';
```

- The regular expression `'(^| )DIAB1'` matches:
  - `DIAB1` at the **start of the string** (`^`)
  - or **immediately following a space** (` `)

---

### 💡 What I Learned

I learned how to:

- Use regular expression operators in **PostgreSQL** (e.g., `~` for case-sensitive matching)
- Apply anchors like `^` to match the start of a string
- Simulate word boundary detection using patterns like `(^| )`

---

### 🔤 Basic Regex Anchors and Boundaries

| Symbol | Meaning                          |
|--------|----------------------------------|
| `^`    | Start of string                  |
| `$`    | End of string                    |
| `.`    | Any single character (except newline) |
| `(...)`| Grouping (used to group parts of the pattern) |

---

### 🔡 Character Classes

| Pattern       | Meaning                             |
|---------------|-------------------------------------|
| `[abc]`       | Match one of: a, b, or c            |
| `[^abc]`      | Match any character except a, b, or c |
| `[a-z]`       | Match any lowercase letter          |
| `[A-Za-z0-9_]`| Match any letter, digit, or underscore |
| `\d`          | Digit (same as `[0-9]`)             |
| `\w`          | Word character (same as `[A-Za-z0-9_]`) |
| `\s`          | Whitespace (space, tab, newline)    |

---

### 🔁 Quantifiers

| Symbol   | Meaning                        |
|----------|--------------------------------|
| `*`      | 0 or more times                |
| `+`      | 1 or more times                |
| `?`      | 0 or 1 time                    |
| `{n}`    | Exactly n times                |
| `{n,}`   | n or more times                |
| `{n,m}`  | Between n and m times          |

---

### 📏 Word Boundaries and Special Anchors (PostgreSQL Specific)

| Symbol  | Meaning                         |
|---------|---------------------------------|
| `\y`    | Word boundary (PostgreSQL only) |
| `\m`    | Start of word                   |
| `\M`    | End of word                     |
| `(^| )` | Start of string or after space (used to simulate word boundary) |

---

### 🧠 Key Takeaway  
Regex is incredibly powerful for **pattern matching** within strings.  
In SQL, it's especially useful when dealing with **non-normalized data**, like space-separated condition codes.
