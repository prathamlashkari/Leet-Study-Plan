## [734. Sentence Similarity](https://leetcode.com/problems/sentence-similarity/)

**Difficulty:** Easy  
**Tags:** Array, Hash Table, String  
**Companies:** Google

---

### 📝 Description

We represent a sentence as an array of words. Given two sentences `sentence1` and `sentence2` each represented as a string array, and an array of string pairs `similarPairs` where `similarPairs[i] = [xi, yi]` indicates that the two words `xi` and `yi` are similar.

Return `true` if `sentence1` and `sentence2` are similar, or `false` otherwise.

Two sentences are similar if:

- They have the same length (same number of words).
- For every index `i`, `sentence1[i]` and `sentence2[i]` are similar.

Note:

- A word is always similar to itself.
- Similarity is **not transitive** (e.g., if `a` is similar to `b` and `b` is similar to `c`, `a` is not necessarily similar to `c`).

---

### 📘 Examples

**Example 1:**  
Input:  
sentence1 = ["great","acting","skills"],
sentence2 = ["fine","drama","talent"],
similarPairs = [["great","fine"],["drama","acting"],["skills","talent"]]
Output: `true`  
Explanation: Each corresponding word pair is either equal or marked similar.

**Example 2:**  
Input:  
sentence1 = ["great"],
sentence2 = ["great"],
similarPairs = []
Output: `true`  
Explanation: A word is similar to itself.

**Example 3:**  
Input:  
sentence1 = ["great"],
sentence2 = ["doubleplus","good"],
similarPairs = [["great","doubleplus"]]

arduino
Copy
Edit
Output: `false`  
Explanation: Sentences have different lengths.

---

### ✅ Constraints

- `1 <= sentence1.length, sentence2.length <= 1000`
- `1 <= sentence1[i].length, sentence2[i].length <= 20`
- `sentence1[i]` and `sentence2[i]` consist of English letters.
- `0 <= similarPairs.length <= 1000`
- `similarPairs[i].length == 2`
- `1 <= xi.length, yi.length <= 20`
- `xi` and `yi` consist of lower-case and upper-case English letters.
- All the pairs `(xi, yi)` are distinct.

---

### 💻 Solution (Java)

```java
class Solution {
    public boolean areSentencesSimilar(String[] sentence1, String[] sentence2, List<List<String>> similarPairs) {
        if (sentence1.length != sentence2.length) return false;

        Map<String, Set<String>> map = new HashMap<>();

        for (List<String> pair : similarPairs) {
            String w1 = pair.get(0);
            String w2 = pair.get(1);
            map.putIfAbsent(w1, new HashSet<>());
            map.putIfAbsent(w2, new HashSet<>());
            map.get(w1).add(w2);
            map.get(w2).add(w1);
        }

        for (int i = 0; i < sentence1.length; i++) {
            String w1 = sentence1[i];
            String w2 = sentence2[i];
            if (w1.equals(w2)) continue;
            if (!map.containsKey(w1) || !map.get(w1).contains(w2)) return false;
        }

        return true;
    }
}
```
