## [161. One Edit Distance](https://leetcode.com/problems/one-edit-distance/)

**Difficulty:** Medium  
**Tags:** Two Pointers, String  
**Companies:** Yandex, Meta, Amazon, Snap, Google, Uber

---

### 📝 Description

Given two strings `s` and `t`, return `true` if they are **one edit distance apart**, otherwise return `false`.

A string `s` is one edit distance apart from string `t` if you can:

- Insert exactly one character into `s` to get `t`.
- Delete exactly one character from `s` to get `t`.
- Replace exactly one character of `s` with a different character to get `t`.

---

### 📘 Examples

**Input:**  
`s = "ab", t = "acb"`  
**Output:**  
`true`  
**Explanation:** You can insert `'c'` into `s` to get `t`.

---

**Input:**  
`s = "", t = ""`  
**Output:**  
`false`  
**Explanation:** Cannot get `t` from `s` by exactly one edit.

---

### ✅ Constraints

- `0 <= s.length, t.length <= 10⁴`
- `s` and `t` consist of lowercase letters, uppercase letters, and digits.

---

### 💡 Solution (C++)

```cpp
class Solution {
    int solve(int i, int j, int n, int m, string& s, string& t, vector<vector<int>>& dp) {
        if (i == n && j == m) return 0;
        if (i == n) return m - j;
        if (j == m) return n - i;

        if (dp[i][j] != -1) return dp[i][j];

        if (s[i] == t[j]) {
            return dp[i][j] = solve(i + 1, j + 1, n, m, s, t, dp);
        } else {
            int insertOp = 1 + solve(i, j + 1, n, m, s, t, dp);
            int deleteOp = 1 + solve(i + 1, j, n, m, s, t, dp);
            int replaceOp = 1 + solve(i + 1, j + 1, n, m, s, t, dp);
            return dp[i][j] = min({insertOp, deleteOp, replaceOp});
        }
    }

public:
    bool isOneEditDistance(string s, string t) {
        int n = s.size(), m = t.size();
        vector<vector<int>> dp(n + 1, vector<int>(m + 1, -1));
        int ops = solve(0, 0, n, m, s, t, dp);
        return ops == 1;
    }
};
```
