## [1056. Confusing Number](https://leetcode.com/problems/confusing-number/)

**Difficulty:** Easy  
**Tags:** Math  
**Companies:** Google

---

### 📝 Description

A confusing number is a number that when rotated 180 degrees becomes a different number, with each digit valid.

You can rotate digits of a number by 180 degrees to form new digits:

- `0 → 0`, `1 → 1`, `6 → 9`, `8 → 8`, `9 → 6`
- `2, 3, 4, 5, 7` are invalid when rotated

Note: After rotating, leading zeros are ignored.  
For example, rotating `8000` becomes `0008` which is interpreted as `8`.

Given an integer `n`, return `true` if it is a confusing number, otherwise return `false`.

---

### 📘 Examples

**Input:**  
`n = 6`  
**Output:**  
`true`  
**Explanation:** Rotates to `9`, which is valid and different from `6`.

---

**Input:**  
`n = 89`  
**Output:**  
`true`  
**Explanation:** Rotates to `68`, which is valid and different from `89`.

---

**Input:**  
`n = 11`  
**Output:**  
`false`  
**Explanation:** Rotates to `11`, same as original, so not confusing.

---

### ✅ Constraints

- `0 <= n <= 10⁹`

---

### 💡 Solution (C++)

```cpp
class Solution {
public:
    bool confusingNumber(int N) {
        vector<int> vec = {0, 1, -1, -1, -1, -1, 9, -1, 8, 6};
        int n = N;
        int new_number = 0;
        while(n) {
            int r = n % 10;
            if (vec[r] == -1) {
                return false;
            }
            new_number = new_number * 10 + vec[r];
            n /= 10;
        }
        return (new_number != N);
    }
};
```
