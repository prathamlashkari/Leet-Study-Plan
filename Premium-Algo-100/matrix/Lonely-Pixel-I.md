## [531. Lonely Pixel I](https://leetcode.com/problems/lonely-pixel-i/)

**Difficulty:** Easy  
**Tags:** Array, Hash Table, Matrix  
**Companies:** Google

---

### 📝 Description

Given an `m x n` picture consisting of black `'B'` and white `'W'` pixels, return the number of **black lonely pixels**.

A **black lonely pixel** is a character `'B'` located at a specific position such that **no other** black pixels are in the **same row or column**.

---

### 📘 Examples

**Input:**
picture = [["W","W","B"],
["W","B","W"],
["B","W","W"]]

**Output:**  
3

**Explanation:**  
All three `'B'` pixels are isolated in both their rows and columns.

---

**Input:**
picture = [["B","B","B"],
["B","B","W"],
["B","B","B"]]

**Output:**  
0

**Explanation:**  
No `'B'` is isolated in both its row and column.

---

### ✅ Constraints

- `m == picture.length`
- `n == picture[i].length`
- `1 <= m, n <= 500`
- `picture[i][j]` is `'W'` or `'B'`.

---

### 💡 Solution (C++)

```cpp
class Solution {
public:
    int findLonelyPixel(vector<vector<char>>& picture) {
        int m = picture.size(), n = picture[0].size();
        vector<int> rowCount(m, 0), colCount(n, 0);

        for (int i = 0; i < m; ++i)
            for (int j = 0; j < n; ++j)
                if (picture[i][j] == 'B') {
                    rowCount[i]++;
                    colCount[j]++;
                }

        int lonely = 0;
        for (int i = 0; i < m; ++i)
            for (int j = 0; j < n; ++j)
                if (picture[i][j] == 'B' && rowCount[i] == 1 && colCount[j] == 1)
                    lonely++;

        return lonely;
    }
};
```
