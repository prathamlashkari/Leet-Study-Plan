## [266. Palindrome Permutation](https://leetcode.com/problems/palindrome-permutation/)

**Difficulty:** Easy  
**Tags:** Hash Table, String, Bit Manipulation  
**Companies:** Meta, Microsoft, Nordstrom, Google, Bloomberg, Apple, Uber, Docusign

---

### 📝 Description

Given a string `s`, return `true` if a permutation of the string could form a palindrome and `false` otherwise.

---

### 📘 Examples

**Example 1:**  
Input: `s = "code"`  
Output: `false`

**Example 2:**  
Input: `s = "aab"`  
Output: `true`

**Example 3:**  
Input: `s = "carerac"`  
Output: `true`

---

### ✅ Constraints

- `1 <= s.length <= 5000`
- `s` consists of only lowercase English letters.

---

### 💻 Solution (Java)

```java
class Solution {
    public boolean canPermutePalindrome(String s) {
        int []chars = new int[26];
        int n = s.length();
        for (int i = 0 ; i < n ; i++) {
           chars[s.charAt(i) - 'a']++;
        }
        int oddCount = 0;
        for (int count : chars) {
            if (count % 2 == 1) {
                oddCount++;
            }
        }
        return oddCount <= 1;
    }
}
```
