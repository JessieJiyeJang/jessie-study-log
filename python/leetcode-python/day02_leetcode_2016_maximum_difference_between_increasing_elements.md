## 🧠 LeetCode – Maximum Difference Between Increasing Elements  
🔗 https://leetcode.com/problems/maximum-difference-between-increasing-elements/

### 📌 Problem Summary  
Given a 0-indexed integer array `nums`, return the **maximum difference** `nums[j] - nums[i]` such that `0 <= i < j < n` and `nums[i] < nums[j]`.  
If no such pair exists, return `-1`.

---

### 💡 Algorithm Concepts Used  
- Brute Force comparison of all valid (i, j) pairs  
- Difference tracking using list and `max()`  
- Conditions: i < j and nums[i] < nums[j]

---

### ✅ My Final Solution (Python, Brute Force)
```python
class Solution:
    def maximumDifference(self, nums: List[int]) -> int:
        n = len(nums)
        biggest = [-1]

        for j in range(n):
            for i in range(j):
                if nums[i] < nums[j]: 
                    biggest += [nums[j] - nums[i]]

        return max(biggest)
```

---

### 💬 What I Learned  
- This approach checks all combinations of `i < j` and `nums[i] < nums[j]`, then tracks differences.  
- It is straightforward and easy to understand for small inputs.  
- The return value must be `-1` if no valid (i, j) pair is found.

---

### 🛠️ Room for Improvement  
- The current solution uses **O(n²)** time complexity due to nested loops and checks every pair.  
- It also uses a list `biggest` to store intermediate values, which is not necessary and increases memory usage.  
- We can optimize the solution using a **single pass (O(n))** and a **running minimum**:

  #### 🔧 Optimized Version:
  ```python
  class Solution:
      def maximumDifference(self, nums: List[int]) -> int:
          min_val = nums[0]
          max_diff = -1

          for j in range(1, len(nums)):
              if nums[j] > min_val:
                  max_diff = max(max_diff, nums[j] - min_val)
              else:
                  min_val = nums[j]
                  
          return max_diff
  ```

  #### ✅ Why this is better:
  - Only requires a single scan of the array  
  - Constant space complexity: no list needed  
  - Tracks the lowest value seen so far and computes difference only when `nums[j] > min_val`  
  - Much faster for large arrays (`n` up to 1000)

---

### 📈 Time & Space Complexity
- Brute Force: Time **O(n²)**, Space **O(n)**  
- Optimized: Time **O(n)**, Space **O(1)**
