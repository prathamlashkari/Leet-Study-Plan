# 1133. Largest Unique Number

## Problem Statement

Given an integer array `nums`, return the largest integer that **only occurs once**. If no integer occurs once, return `-1`.

---

## Examples

### Example 1

**Input:**  
nums = [5,7,3,9,4,9,8,3,1]
**Output:**  
8
**Explanation:**  
The maximum integer in the array is 9 but it is repeated. The number 8 occurs only once, so it is the answer.

---

### Example 2

**Input:**
nums = [9,9,8,8]

**Output:**  
-1

**Explanation:**  
There is no number that occurs only once.

---

## Constraints

- 1 <= nums.length <= 2000
- 0 <= nums[i] <= 1000

---

## Acceptance Rate

- Accepted: 92,501 / 130.7K
- Acceptance Rate: 70.8%

---

## Topics

- Array
- Hash Table
- Sorting

---

## Companies

- Amazon (6 months ago)

---

## Solution (C++)

```cpp
class Solution {
public:
    int largestUniqueNumber(vector<int>& A) {
        short a[1001] = {};
        for (auto n : A)
            ++a[n];
        int i = 1000;
        while (i >= 0 && a[i] != 1)
            --i;
        return i;
    }
};
```
