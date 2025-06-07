## [340. Longest Substring with At Most K Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/)

**Difficulty:** Medium  
**Tags:** Hash Table, String, Sliding Window  
**Companies:** Amazon, Microsoft, Yandex, TikTok, Google, Meta, Coupang, BitGo, Goldman Sachs, AppDynamics

---

### 📝 Description

Given a string `s` and an integer `k`, return the length of the longest substring of `s` that contains **at most k distinct characters**.

---

### 📘 Examples

**Example 1:**  
Input: `s = "eceba"`, `k = 2`  
Output: `3`  
Explanation: The substring is `"ece"` with length 3.

**Example 2:**  
Input: `s = "aa"`, `k = 1`  
Output: `2`  
Explanation: The substring is `"aa"` with length 2.

---

### ✅ Constraints

- `1 <= s.length <= 5 * 10^4`
- `0 <= k <= 50`

---

### 💡 Solution (C++)

```cpp
class Solution {
public:
    int lengthOfLongestSubstringKDistinct(string s, int k) {
        int n = s.size(), i = 0, j = 0, ans = 0;
        unordered_map<char, int> mp;
        while (j < n) {
            mp[s[j]]++;
            while (mp.size() > k && i < j) {
                mp[s[i]]--;
                if (mp[s[i]] == 0) mp.erase(s[i]);
                i++;
            }
            if (mp.size() <= k) ans = max(ans, j - i + 1);
            j++;
        }
        return ans;
    }
};
```
