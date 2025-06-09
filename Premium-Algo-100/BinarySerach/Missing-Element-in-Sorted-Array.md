## [1060. Missing Element in Sorted Array](https://leetcode.com/problems/missing-element-in-sorted-array/)

**Difficulty:** Medium  
**Tags:** Array, Binary Search  
**Companies:** Meta, Google, Amazon, Arista Networks

---

### 📝 Problem Description

Given an integer array `nums` which is sorted in ascending order and all of its elements are unique, and also given an integer `k`, return the **kth missing number** starting from the leftmost number of the array.

---

### 📘 Examples

**Example 1:**  
Input: `nums = [4,7,9,10], k = 1`  
Output: `5`  
Explanation: The first missing number is 5.

**Example 2:**  
Input: `nums = [4,7,9,10], k = 3`  
Output: `8`  
Explanation: The missing numbers are `[5,6,8,...]`, hence the third missing number is 8.

**Example 3:**  
Input: `nums = [1,2,4], k = 3`  
Output: `6`  
Explanation: The missing numbers are `[3,5,6,7,...]`, hence the third missing number is 6.

---

### ✅ Constraints

- `1 <= nums.length <= 5 * 10^4`
- `1 <= nums[i] <= 10^7`
- `nums` is sorted in ascending order, and all the elements are unique.
- `1 <= k <= 10^8`

---

### 💡 Follow-up

Can you find a logarithmic time complexity solution (O(log n))?

---

### 🔑 Key Insight

The number of missing elements until index `i` is:  
`nums[i] - nums[0] - i`

We can use binary search to find the smallest index `l` where the count of missing elements is at least `k`.

---

### 💻 Code (C++)

```cpp
class Solution {
public:
    int missingElement(vector<int>& nums, int k) {
        int n = nums.size();
        int l = 0, h = n;

        // Binary search to find the first index where
        // missing count >= k
        while (l < h) {
            int m = l + (h - l) / 2;
            // missing elements until index m
            int missing = nums[m] - nums[0] - m;
            if (missing >= k) {
                h = m;
            } else {
                l = m + 1;
            }
        }

        // After binary search:
        // l is the index where missing count >= k,
        // so the kth missing number is between nums[l-1] and nums[l]

        // missing numbers until nums[l-1]
        int missingUntilPrev = nums[l-1] - nums[0] - (l - 1);

        // kth missing number = nums[l-1] + (k - missingUntilPrev)
        return nums[l-1] + (k - missingUntilPrev);
    }
};
```
