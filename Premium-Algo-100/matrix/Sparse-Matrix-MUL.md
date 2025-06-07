## [311. Sparse Matrix Multiplication](https://leetcode.com/problems/sparse-matrix-multiplication/)

**Difficulty:** Medium  
**Tags:** Array, Hash Table, Matrix  
**Companies:** Meta, Google, Bloomberg, TikTok, Pinterest, LinkedIn

---

### 📝 Description

Given two **sparse matrices** `mat1` of size `m x k` and `mat2` of size `k x n`, return the result of `mat1 x mat2`.  
You may assume that **multiplication is always possible**.

---

### 📘 Examples

**Input:**
mat1 = [[1,0,0],
[-1,0,3]],

mat2 = [[7,0,0],
[0,0,0],
[0,0,1]]
**Output:**  
[[7,0,0],
[-7,0,3]]

---

**Input:**  
mat1 = [[0]],
mat2 = [[0]]
**Output:**  
[[0]]

---

### ✅ Constraints

- `m == mat1.length`
- `k == mat1[i].length == mat2.length`
- `n == mat2[i].length`
- `1 <= m, n, k <= 100`
- `-100 <= mat1[i][j], mat2[i][j] <= 100`

---

### 💡 Solution (C++)

```cpp
class Solution {
public:
    vector<vector<int>> multiply(vector<vector<int>>& A, vector<vector<int>>& B) {
        int am = A.size();      // Rows in A
        int bm = B.size();      // Rows in B
        int an = A[0].size();   // Columns in A == Rows in B
        int bn = B[0].size();   // Columns in B

        vector<vector<int>> result(am, vector<int>(bn, 0));
        vector<vector<int>> A_non_zero(am);
        vector<vector<int>> B_non_zero(bn);

        // Store non-zero indices for A
        for (int i = 0; i < am; i++)
            for (int j = 0; j < an; j++)
                if (A[i][j]) A_non_zero[i].push_back(j);

        // Store non-zero indices for B (column-wise)
        for (int j = 0; j < bn; j++)
            for (int i = 0; i < bm; i++)
                if (B[i][j]) B_non_zero[j].push_back(i);

        // Multiply only non-zero positions
        for (int i = 0; i < am; i++)
            for (int j = 0; j < bn; j++) {
                int m = 0, n = 0;
                while (m < A_non_zero[i].size() && n < B_non_zero[j].size()) {
                    int idx_A = A_non_zero[i][m];
                    int idx_B = B_non_zero[j][n];
                    if (idx_A == idx_B) {
                        result[i][j] += (A[i][idx_A] * B[idx_B][j]);
                        m++;
                        n++;
                    } else if (idx_A > idx_B)
                        n++;
                    else
                        m++;
                }
            }

        return result;
    }
};
```
