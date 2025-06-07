# LeetCode Problem 249: Group Shifted Strings

## Problem Description

You are given an array of strings `strings`. Your task is to group all strings that belong to the same shifting sequence.

### Shifting Rules:

- **Right shift:** Replace every letter with the next letter in the English alphabet. 'z' wraps around to 'a'.  
  Example: `"abc"` → `"bcd"`, `"xyz"` → `"yza"`
- **Left shift:** Replace every letter with the previous letter in the English alphabet. 'a' wraps around to 'z'.  
  Example: `"bcd"` → `"abc"`, `"yza"` → `"xyz"`

Shifting strings repeatedly produces an infinite cyclic sequence, e.g.:  
`... <-> "abc" <-> "bcd" <-> ... <-> "xyz" <-> "yza" <-> ... <-> "zab" <-> "abc" <-> ...`

Group strings that are in the same shifting sequence.

---

## Examples

**Example 1:**  
Input: ["abc","bcd","acef","xyz","az","ba","a","z"]
Output:  
[
["acef"],
["a","z"],
["abc","bcd","xyz"],
["az","ba"]
]

**Example 2:**  
Input: ["a"]
Output: [["a"]]

---

## Constraints

- 1 <= `strings.length` <= 200
- 1 <= `strings[i].length` <= 50
- `strings[i]` contains only lowercase English letters

---

## Approach

1. For each string, calculate a **key** representing its shifting pattern.
2. The key is a sequence of differences between consecutive characters, normalized with modulo 26 to handle wrap-around.
3. Strings with the same key belong to the same shifting sequence group.
4. Use a HashMap to group strings by this key.
5. Return the list of grouped strings.

---

## Code Implementation (Java)

```java
import java.util.*;

public class Solution {
    public List<List<String>> groupStrings(String[] strings) {
        Map<String, List<String>> map = new HashMap<>();

        for (String s : strings) {
            String key = getShiftKey(s);
            map.putIfAbsent(key, new ArrayList<>());
            map.get(key).add(s);
        }

        return new ArrayList<>(map.values());
    }

    private String getShiftKey(String s) {
        if (s.length() == 0) return "";

        StringBuilder sb = new StringBuilder();
        for (int i = 1; i < s.length(); i++) {
            int diff = (s.charAt(i) - s.charAt(i - 1) + 26) % 26;
            sb.append(diff).append(",");
        }
        return sb.toString();
    }
}
```
