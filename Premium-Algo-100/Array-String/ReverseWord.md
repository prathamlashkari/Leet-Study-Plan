## [186. Reverse Words in a String II](https://leetcode.com/problems/reverse-words-in-a-string-ii/)

**Difficulty:** Medium  
**Tags:** Two Pointers, String  
**Companies:** Microsoft, Amazon, Apple, ServiceNow, Uber

---

### 📝 Description

Given a character array `s`, reverse the order of the words **in-place**.

A word is defined as a sequence of non-space characters. The words in `s` are separated by a single space.

---

### 📘 Examples

**Input:**  
`s = ["t","h","e"," ","s","k","y"," ","i","s"," ","b","l","u","e"]`  
**Output:**  
`["b","l","u","e"," ","i","s"," ","s","k","y"," ","t","h","e"]`

---

**Input:**  
`s = ["a"]`  
**Output:**  
`["a"]`

---

### ✅ Constraints

- `1 <= s.length <= 10^5`
- `s[i]` is an English letter (uppercase or lowercase), digit, or space `' '`.
- There is at least one word in `s`.
- `s` does not contain leading or trailing spaces.
- Words are separated by a single space.

---

### 💡 Solution (C++)

```cpp
class Solution {
public:
    void reverse(vector<char>& s, int l, int r) {
        while (l < r) swap(s[l++], s[r--]);
    }

    void reverseWords(vector<char>& s) {
        int n = s.size();
        // Reverse the entire string
        reverse(s, 0, n - 1);

        int start = 0;
        for (int end = 0; end <= n; ++end) {
            // When space or end of string found, reverse the word
            if (end == n || s[end] == ' ') {
                reverse(s, start, end - 1);
                start = end + 1;
            }
        }
    }
};
```
