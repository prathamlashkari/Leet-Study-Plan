## [422. Valid Word Square](https://leetcode.com/problems/valid-word-square/)

**Difficulty:** Easy  
**Tags:** Array, Matrix  
**Companies:** Google, Apple

---

### 📝 Description

Given an array of strings `words`, return `true` if it forms a **valid word square**.

A sequence of strings forms a valid word square if the `k`th row and column read the same string, where `0 <= k < max(numRows, numColumns)`.

---

### 📘 Examples

**Input:**
words = ["abcd","bnrt","crmy","dtye"]

makefile
Copy
Edit
**Output:**  
true

pgsql
Copy
Edit

**Explanation:**  
The 1st row and 1st column both read `"abcd"`  
The 2nd row and 2nd column both read `"bnrt"`  
The 3rd row and 3rd column both read `"crmy"`  
The 4th row and 4th column both read `"dtye"`  
So, it is a valid word square.

---

**Input:**  
words = ["abcd","bnrt","crm","dt"]
**Output:**  
true

**Explanation:**  
All corresponding rows and columns match.

---

**Input:**  
words = ["ball","area","read","lady"]
**Output:**  
false

**Explanation:**  
The 3rd row reads `"read"` while the 3rd column reads `"lead"`, so it's not a valid word square.

---

### ✅ Constraints

- `1 <= words.length <= 500`
- `1 <= words[i].length <= 500`
- `words[i]` consists of only lowercase English letters.

---

### 💡 Solution (C++)

```cpp
class Solution {
public:
    bool validWordSquare(vector<string>& words) {
        for (int i = 0; i < words.size(); ++i) {
            for (int j = 0; j < words[i].size(); ++j) {
                if (j >= words.size() || words[j].size() <= i || words[j][i] != words[i][j])
                    return false;
            }
        }
        return true;
    }
};
```
