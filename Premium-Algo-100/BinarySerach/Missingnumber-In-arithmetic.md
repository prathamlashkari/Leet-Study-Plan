## [1228. Missing Number In Arithmetic Progression](https://leetcode.com/problems/missing-number-in-arithmetic-progression/)

**Difficulty:** Easy  
**Tags:** Math, Array  
**Companies:** (Not specified)

---

### 📝 Description

In some array `arr`, the values were in arithmetic progression: the values `arr[i + 1] - arr[i]` are all equal for every `0 <= i < arr.length - 1`.

A value from `arr` was removed that was not the first or last value in the array.

Given `arr`, return the removed value.

---

### 📘 Examples

**Input:**  
`arr = [5,7,11,13]`  
**Output:**  
`9`  
**Explanation:** The previous array was `[5,7,9,11,13]`.

---

**Input:**  
`arr = [15,13,12]`  
**Output:**  
`14`  
**Explanation:** The previous array was `[15,14,13,12]`.

---

### ✅ Constraints

- `3 <= arr.length <= 1000`
- `0 <= arr[i] <= 10^5`
- The given array is guaranteed to be a valid array.

---

### 💡 Solution (C++)

```cpp
class Solution {
public:
    int missingNumber(vector<int>& A) {
        int first = A[0], last = A[0], sum = 0, n = A.size();
        for (int a : A) {
            first = min(first, a);
            last = max(last, a);
            sum += a;
        }
        return (first + last) * (n + 1) / 2 - sum;
    }
};
```
