## [1100. Find K-Length Substrings With No Repeated Characters](https://leetcode.com/problems/find-k-length-substrings-with-no-repeated-characters/)

**Difficulty:** Easy  
**Tags:** Hash Table, String, Sliding Window  
**Companies:** Amazon

---

### 📝 Description

Given a string `s` and an integer `k`, return the number of substrings in `s` of length `k` with **no repeated characters**.

---

### 📘 Examples

**Example 1:**  
Input: `s = "havefunonleetcode"`, `k = 5`  
Output: `6`  
Explanation: The substrings are `'havef'`, `'avefu'`, `'vefun'`, `'efuno'`, `'etcod'`, `'tcode'`.

**Example 2:**  
Input: `s = "home"`, `k = 5`  
Output: `0`  
Explanation: `k` is larger than the length of `s`, so no substrings possible.

---

### ✅ Constraints

- `1 <= s.length <= 10^4`
- `s` consists of lowercase English letters.
- `1 <= k <= 10^4`

---

### 💻 Solution (C++)

```cpp
class Solution {
public:
    int numKLenSubstrNoRepeats(string S, int K) {
        unordered_set<int> cur;
        int res = 0, i = 0;
        for (int j = 0; j < S.size(); ++j) {
            while (cur.count(S[j]))
                cur.erase(S[i++]);
            cur.insert(S[j]);
            if (j - i + 1 >= K)
                res++;
        }
        return res;
    }
};
```
