## [1198. Find Smallest Common Element in All Rows](https://leetcode.com/problems/find-smallest-common-element-in-all-rows/)

**Difficulty:** Easy  
**Tags:** Array, Hash Table, Binary Search, Matrix, Counting  
**Companies:** Microsoft

---

### 📝 Description

Given an `m x n` matrix `mat` where every row is sorted in strictly increasing order, return the smallest common element in all rows.

If there is no common element, return `-1`.

---

### 📘 Examples

**Input:**  
mat = [[1,2,3,4,5],
[2,4,5,8,10],
[3,5,7,9,11],
[1,3,5,7,9]]
**Output:**  
5

---

**Input:**  
mat = [[1,2,3],
[2,3,4],
[2,3,5]]
**Output:**  
2

---

### ✅ Constraints

- `m == mat.length`
- `n == mat[i].length`
- `1 <= m, n <= 500`
- `1 <= mat[i][j] <= 10^4`
- `mat[i]` is sorted in strictly increasing order.

---

### 💡 Solution (C++)

```cpp
class Solution {
public:
    int smallestCommonElement(vector<vector<int>>& mat) {
        int n = mat.size(), m = mat[0].size();
        unordered_map<int, int> mp;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                mp[mat[i][j]]++;
            }
        }
        int ans = INT_MAX;
        for (auto it : mp) {
            if (it.second == n) {
                ans = min(ans, it.first);
            }
        }
        return ans == INT_MAX ? -1 : ans;
    }
};

```
