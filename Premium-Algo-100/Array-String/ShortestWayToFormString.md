## [1055. Shortest Way to Form String](https://leetcode.com/problems/shortest-way-to-form-string/)

**Difficulty:** Medium  
**Tags:** Two Pointers, String, Binary Search, Greedy  
**Companies:** Pinterest, Google, Meta, Amazon

---

### 📝 Description

A subsequence of a string is a new string formed from the original string by deleting some (or none) characters without disturbing the relative positions of the remaining characters.

Given two strings `source` and `target`, return the minimum number of subsequences of `source` such that their concatenation equals `target`. If it is impossible to form `target` from `source`, return `-1`.

---

### 📘 Examples

**Input:**  
`source = "abc"`, `target = "abcbc"`  
**Output:**  
`2`  
**Explanation:** The target `"abcbc"` can be formed by concatenating subsequences `"abc"` and `"bc"` from `source`.

---

**Input:**  
`source = "abc"`, `target = "acdbc"`  
**Output:**  
`-1`  
**Explanation:** The character `"d"` in target cannot be formed from source.

---

**Input:**  
`source = "xyz"`, `target = "xzyxz"`  
**Output:**  
`3`  
**Explanation:** Target can be constructed as `"xz"` + `"y"` + `"xz"`.

---

### ✅ Constraints

- `1 <= source.length, target.length <= 1000`
- `source` and `target` consist of lowercase English letters.

---

### 💡 Solution (C++)

```cpp
class Solution {
public:
    int shortestWay(string s, string tar) {
        int n = s.size(), m = tar.size();
        unordered_set<char> st(s.begin(), s.end());
        int cnt = 0;
        int i = 0;

        while (i < m) {
            // If target character not in source, return -1
            if (st.find(tar[i]) == st.end()) return -1;

            int j = 0;
            // Try to match as many chars of target with source subsequence
            while (j < n && i < m) {
                if (tar[i] == s[j]) i++;
                j++;
            }
            cnt++;
        }
        return cnt;
    }
};
```
