## [487. Max Consecutive Ones II](https://leetcode.com/problems/max-consecutive-ones-ii/)

**Difficulty:** Medium  
**Tags:** Array, Dynamic Programming, Sliding Window  
**Companies:** Meta, Yandex, Google

---

### 📝 Description

Given a binary array `nums`, return the maximum number of consecutive 1's in the array if you can flip **at most one 0**.

---

### 📘 Examples

**Example 1:**  
Input: `nums = [1,0,1,1,0]`  
Output: `4`  
Explanation:

- Flip the first zero: `[1,1,1,1,0]` → 4 consecutive ones
- Flip the second zero: `[1,0,1,1,1]` → 3 consecutive ones  
  Maximum consecutive ones = 4

**Example 2:**  
Input: `nums = [1,0,1,1,0,1]`  
Output: `4`  
Explanation:

- Flip the first zero: `[1,1,1,1,0,1]` → 4 consecutive ones
- Flip the second zero: `[1,0,1,1,1,1]` → 4 consecutive ones  
  Maximum consecutive ones = 4

---

### ✅ Constraints

- `1 <= nums.length <= 10^5`
- `nums[i]` is either 0 or 1.

---

### 💡 Follow-up

If input numbers come one by one as an infinite stream, you can't store all numbers due to memory constraints. You should still solve it efficiently using sliding window techniques.

---

### 💻 Solution (C++)

```cpp
class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums) {
        int n = nums.size();
        int l = 0, z = 0, r = 0, ans = 0;
        while (r < n) {
            if (nums[r] == 0) z++;

            while (z > 1 && l < r) {
                if (nums[l++] == 0) z--;
            }

            ans = max(ans, r - l + 1);
            r++;
        }
        return ans;
    }
};
```
