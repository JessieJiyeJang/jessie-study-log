## 🧠 LeetCode – Two Sum  
🔗 https://leetcode.com/problems/two-sum/

### 📌 Problem Summary  
Given an array of integers `nums` and an integer `target`, return **indices** of the two numbers such that they add up to `target`.  
Each input has **exactly one solution**, and you **may not use the same element twice**.  
You can return the answer in any order.

---

### 💡 Algorithm Concepts Used  
- Brute Force (O(n²))  
- Nested loops to check all pairs  
- Early return upon match

---

### ✅ My Final Solution (Python, Brute Force)
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            for j in range(i + 1, len(nums)):
                if nums[i] + nums[j] == target:
                    return [i, j]
```

---

### 💬 What I Learned  
- This brute-force solution checks all possible pairs, which is intuitive and easy to implement.  
- However, its **time complexity is O(n²)**, which becomes inefficient as input size grows.  
- After solving it this way, I learned that the problem can be solved in **O(n) time** using a **hash map (dictionary)**.  
  That approach tracks seen numbers and checks for complements in a single pass, making it much faster.

---

### 🛠️ Room for Improvement  
- Current solution is readable but inefficient for large inputs.  
- By using a hash map to store previously seen numbers and their indices, we can reduce time complexity to **O(n)**:  
  ```python
  class Solution:
      def twoSum(self, nums: List[int], target: int) -> List[int]:
          num_map = {}
          for i, num in enumerate(nums):
              complement = target - num
              if complement in num_map:
                  return [num_map[complement], i]
              num_map[num] = i
  ```
- This was a great example of learning how to optimize brute-force code with a smarter data structure.

### 📈 Time & Space Complexity
- Brute Force: Time O(n²), Space O(1)
- Optimized (Hash Map): Time O(n), Space O(n)
