## [1165. Single-Row Keyboard](https://leetcode.com/problems/single-row-keyboard/)

**Difficulty:** Easy  
**Tags:** Hash Table, String  
**Companies:** Google

---

### 📝 Description

There is a special keyboard with all keys in a single row.

Given a string `keyboard` of length 26 indicating the layout of the keyboard (indexed from 0 to 25). Initially, your finger is at index 0. To type a character, you must move your finger to the index of that character. The time taken to move your finger from index `i` to index `j` is `|i - j|`.

Given a string `word`, calculate how much time it takes to type it with one finger.

---

### 📘 Examples

**Example 1:**  
Input: keyboard = "abcdefghijklmnopqrstuvwxyz" word = "cba"
Output: `4`  
**Explanation:**  
Move from 0 to 2 for 'c' (2), then to 1 for 'b' (1), then to 0 for 'a' (1). Total = 4.

**Example 2:**  
Input:keyboard = "pqrstuvwxyzabcdefghijklmno"
word = "leetcode"

Output: `73`

---

### ✅ Constraints

- `keyboard.length == 26`
- `keyboard` contains each lowercase letter exactly once
- `1 <= word.length <= 10^4`
- `word[i]` is a lowercase letter

---

### 💻 Solution (Java)

```java
class Solution {
    public int calculateTime(String keyboard, String word) {
        int[] pos = new int[26];
        for (int i = 0; i < 26; i++) {
            pos[keyboard.charAt(i) - 'a'] = i;
        }
        int ans = 0, curr = 0;
        for (char c : word.toCharArray()) {
            int next = pos[c - 'a'];
            ans += Math.abs(curr - next);
            curr = next;
        }
        return ans;
    }
}

```
