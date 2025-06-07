## [159. Longest Substring with At Most Two Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/)

**Difficulty:** Medium  
**Tags:** Hash Table, String, Sliding Window  
**Companies:** Meta, Amazon, TikTok, Google, Oracle, eBay

---

### 📝 Description

Given a string `s`, return the length of the longest substring that contains **at most two distinct characters**.

---

### 📘 Examples

**Example 1:**  
Input: `s = "eceba"`  
Output: `3`  
Explanation: The substring is `"ece"` which length is 3.

**Example 2:**  
Input: `s = "ccaabbb"`  
Output: `5`  
Explanation: The substring is `"aabbb"` which length is 5.

---

### ✅ Constraints

- `1 <= s.length <= 10^5`
- `s` consists of English letters.

---

### 💡 Solution (C++)

```cpp
class Solution {
public:
    int lengthOfLongestSubstringTwoDistinct(string s) {
       int n = s.size(), i = 0, j = 0, ans = 0;
       unordered_map<char, int> mp;
       while (j < n) {
            mp[s[j]]++;
            while (mp.size() > 2 && i < j) {
                mp[s[i]]--;
                if (mp[s[i]] == 0) mp.erase(s[i]);
                i++;
            }
            if (mp.size() <= 2) ans = max(ans, j - i + 1);
            j++;
       }
       return ans;
    }
};
```
