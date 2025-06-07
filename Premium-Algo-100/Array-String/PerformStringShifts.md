## [1427. Perform String Shifts](https://leetcode.com/problems/perform-string-shifts/)

**Difficulty:** Easy  
**Tags:** Array, Math, String  
**Companies:** Goldman Sachs

---

### 📝 Description

You are given a string `s` containing lowercase English letters, and a matrix `shift`, where `shift[i] = [directionᵢ, amountᵢ]`:

- `directionᵢ` can be `0` (for left shift) or `1` (for right shift).
- `amountᵢ` is the number of characters to shift.

- A **left shift by 1** means: remove the first character and append it to the end.
- A **right shift by 1** means: remove the last character and add it to the beginning.

Return the final string after **all shift operations**.

---

### 📘 Examples

**Input:**  
`s = "abc", shift = [[0,1],[1,2]]`  
**Output:**  
`"cab"`  
**Explanation:**

- `[0,1]`: left shift `"abc"` → `"bca"`
- `[1,2]`: right shift `"bca"` → `"cab"`

---

**Input:**  
`s = "abcdefg", shift = [[1,1],[1,1],[0,2],[1,3]]`  
**Output:**  
`"efgabcd"`  
**Explanation:**

- `[1,1]`: `"abcdefg"` → `"gabcdef"`
- `[1,1]`: `"gabcdef"` → `"fgabcde"`
- `[0,2]`: `"fgabcde"` → `"abcdefg"`
- `[1,3]`: `"abcdefg"` → `"efgabcd"`

---

### ✅ Constraints

- `1 <= s.length <= 100`
- `s` only contains lowercase English letters
- `1 <= shift.length <= 100`
- `shift[i].length == 2`
- `directionᵢ` is either `0` or `1`
- `0 <= amountᵢ <= 100`

---

### 💡 Solution (C++)

```cpp
class Solution {
public:
    string stringShift(string s, vector<vector<int>>& shift) {
        for (int i = 0; i != shift.size(); ++i) {
            int t = shift[i][1] % s.size();
            if (shift[i][0] == 0) {
                rotate(s.begin(), s.begin() + t, s.end());
            } else {
                rotate(s.rbegin(), s.rbegin() + t, s.rend());
            }
        }
        return s;
    }
};
```
