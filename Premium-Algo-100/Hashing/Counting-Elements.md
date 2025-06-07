## [1426. Counting Elements](https://leetcode.com/problems/counting-elements/)

**Difficulty:** Easy  
**Tags:** Array, Hash Table  
**Companies:** DRW

---

### 📝 Description

Given an integer array `arr`, count how many elements `x` there are such that `x + 1` is also in `arr`. If there are duplicates in `arr`, count them separately.

---

### 📘 Examples

**Input:**  
`arr = [1,2,3]`  
**Output:**  
`2`  
**Explanation:**  
1 and 2 are counted because 2 and 3 are in `arr`.

---

**Input:**  
`arr = [1,1,3,3,5,5,7,7]`  
**Output:**  
`0`  
**Explanation:**  
No numbers are counted because there is no 2, 4, 6, or 8 in `arr`.

---

### ✅ Constraints

- `1 <= arr.length <= 1000`
- `0 <= arr[i] <= 1000`

---

### 💡 Solution (C++)

```cpp
class Solution {
public:
    int countElements(vector<int>& arr) {
        unordered_set<int> s(arr.begin(), arr.end());
        return count_if(arr.begin(), arr.end(), [&](int x) { return s.count(x + 1); });
    }
};
```
