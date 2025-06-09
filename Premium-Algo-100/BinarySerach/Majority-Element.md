## [1150. Check If a Number Is Majority Element in a Sorted Array](https://leetcode.com/problems/check-if-a-number-is-majority-element-in-a-sorted-array/)

**Difficulty:** Easy  
**Tags:** Binary Search, Array  
**Companies:** N/A

---

### 📝 Description

Given an integer array `nums` sorted in non-decreasing order and an integer `target`, return `true` if `target` is a majority element, or `false` otherwise.

A majority element in an array `nums` is an element that appears more than `nums.length / 2` times.

---

### 📘 Examples

**Input:**  
`nums = [2,4,5,5,5,5,5,6,6], target = 5`  
**Output:**  
`true`  
**Explanation:** The value 5 appears 5 times and the length of the array is 9.  
Thus, 5 is a majority element because 5 > 9/2 is true.

---

**Input:**  
`nums = [10,100,101,101], target = 101`  
**Output:**  
`false`  
**Explanation:** The value 101 appears 2 times and the length of the array is 4.  
Thus, 101 is not a majority element because 2 > 4/2 is false.

---

### ✅ Constraints

- 1 <= nums.length <= 1000
- 1 <= nums[i], target <= 10⁹
- `nums` is sorted in non-decreasing order.

---

### 💡 Solution (C++)

```cpp
class Solution {
public:
    bool isMajorityElement(vector<int>& nums, int tgt) {
        int N = nums.size();
        int l = 0, r = N - 1, mid;
        while (l < r) {
            mid = (l + r) / 2;
            if (nums[mid] >= tgt)
                r = mid;
            else
                l = mid + 1;
        }
        if ((N % 2 == 0 && l < N/2 && nums[l + N/2] == tgt) ||
            (N % 2 == 1 && l <= N/2 && nums[l + N/2] == tgt))
            return true;
        else
            return false;
    }
};
```
