## [723. Candy Crush](https://leetcode.com/problems/candy-crush/)

**Difficulty:** Medium  
**Tags:** Array, Two Pointers, Matrix, Simulation  
**Companies:** Meta, Uber, Bloomberg, Rubrik, Capital One

---

### 📝 Description

Given an `m x n` integer array `board` representing a grid of candies, where `board[i][j]` is the type of candy, and `0` means the cell is empty:

Perform **Candy Crush** elimination until the board becomes **stable**, following these rules:

1. Crush candies that form a **line of three or more** (horizontally or vertically).
2. Set crushed cells to 0 (empty).
3. **Drop** candies from above to fill empty spaces.
4. Repeat until **no more candies** can be crushed.

---

### 📘 Examples

**Example 1:**

**Input:**
board = [
[110,5,112,113,114],
[210,211,5,213,214],
[310,311,3,313,314],
[410,411,412,5,414],
[5,1,512,3,3],
[610,4,1,613,614],
[710,1,2,713,714],
[810,1,2,1,1],
[1,1,2,2,2],
[4,1,4,4,1014]
]
**Output:**
[
[0,0,0,0,0],
[0,0,0,0,0],
[0,0,0,0,0],
[110,0,0,0,114],
[210,0,0,0,214],
[310,0,0,113,314],
[410,0,0,213,414],
[610,211,112,313,614],
[710,311,412,613,714],
[810,411,512,713,1014]
]

---

**Example 2:**

**Input:**
board = [
[1,3,5,5,2],
[3,4,3,3,1],
[3,2,4,5,2],
[2,4,4,5,5],
[1,4,4,1,1]
]
**Output:**
[
[1,3,0,0,0],
[3,4,0,5,2],
[3,2,0,3,1],
[2,4,0,5,2],
[1,4,3,1,1]
]

---

### ✅ Constraints

- `3 <= m, n <= 50`
- `1 <= board[i][j] <= 2000`

---

### 💡 Solution (C++)

```cpp
class Solution {
public:
    vector<vector<int>> candyCrush(vector<vector<int>>& b) {
        int n = b.size(), m = b[0].size();
        while (true) {
            vector<pair<int,int>> vp;

            // Step 1: Find positions to crush
            for (int i = 0; i < n; ++i)
                for (int j = 0; j < m; ++j)
                    if (b[i][j]) {
                        int val = b[i][j];
                        // vertical check
                        if (i+2 < n && b[i+1][j] == val && b[i+2][j] == val)
                            for (int k = 0; i + k < n && b[i + k][j] == val; ++k)
                                vp.push_back({i + k, j});
                        // horizontal check
                        if (j+2 < m && b[i][j+1] == val && b[i][j+2] == val)
                            for (int k = 0; j + k < m && b[i][j + k] == val; ++k)
                                vp.push_back({i, j + k});
                    }

            // If no crushable candy, break
            if (vp.empty()) break;

            // Step 2: Crush candies
            for (auto& p : vp)
                b[p.first][p.second] = 0;

            // Step 3: Drop candies
            for (int j = 0; j < m; ++j) {
                int t = n - 1;
                for (int i = n - 1; i >= 0; --i)
                    if (b[i][j]) b[t--][j] = b[i][j];
                while (t >= 0) b[t--][j] = 0;
            }
        }
        return b;
    }
};
```
