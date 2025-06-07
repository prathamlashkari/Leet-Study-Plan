## [163. Missing Ranges](https://leetcode.com/problems/missing-ranges/)

**Difficulty:** Easy  
**Tags:** Array  
**Companies:** Meta, Google, Amazon, TikTok

---

### 📝 Description

Given:

- An inclusive range `[lower, upper]`.
- A **sorted**, **unique** integer array `nums` where all elements are within that range.

A number `x` is **missing** if `x ∈ [lower, upper]` and `x ∉ nums`.

**Task:**  
Return the **shortest sorted list of ranges** that **exactly cover all the missing numbers**.  
Each range is represented as a list: `[start, end]`.

---

### 📘 Examples

**Example 1:**

**Input:**  
`nums = [0,1,3,50,75]`, `lower = 0`, `upper = 99`

**Output:**  
`[[2,2],[4,49],[51,74],[76,99]]`

**Explanation:**

- 2 is missing → [2,2]
- 4 to 49 → [4,49]
- 51 to 74 → [51,74]
- 76 to 99 → [76,99]

---

**Example 2:**

**Input:**  
`nums = [-1]`, `lower = -1`, `upper = -1`

**Output:**  
`[]`

**Explanation:** No numbers are missing.

---

### ✅ Constraints

- `-10^9 <= lower <= upper <= 10^9`
- `0 <= nums.length <= 100`
- `lower <= nums[i] <= upper`
- All values of `nums` are **unique** and **sorted**

---

### 💡 Solution (C++)

```cpp
class Solution {
public:
    vector<vector<int>> findMissingRanges(vector<int>& nums, int lower, int upper) {
        vector<vector<int>> ans;
        int n = nums.size();

        if (n == 0) {
            ans.push_back({lower, upper});
            return ans;
        }

        // Range before first element
        if (nums[0] > lower)
            ans.push_back({lower, nums[0] - 1});

        // Ranges between elements
        for (int i = 0; i < n - 1; i++) {
            if (nums[i+1] - nums[i] > 1)
                ans.push_back({nums[i] + 1, nums[i+1] - 1});
        }

        // Range after last element
        if (nums[n-1] < upper)
            ans.push_back({nums[n-1] + 1, upper});

        return ans;
    }
};
```
