## [358. Rearrange String k Distance Apart](https://leetcode.com/problems/rearrange-string-k-distance-apart/)

**Difficulty:** Medium  
**Tags:** Heap, Greedy, String  
**Companies:** (Not specified)

---

### 📝 Description

Given a string `s` and an integer `k`, rearrange `s` such that the same characters are at least distance `k` from each other. If it is not possible to rearrange the string, return an empty string `""`.

---

### 📘 Examples

**Input:**  
`s = "aabbcc", k = 3`  
**Output:**  
`"abcabc"`  
**Explanation:** The same letters are at least a distance of 3 from each other.

---

**Input:**  
`s = "aaabc", k = 3`  
**Output:**  
`""`  
**Explanation:** It is not possible to rearrange the string.

---

**Input:**  
`s = "aaadbbcc", k = 2`  
**Output:**  
`"abacabcd"`  
**Explanation:** The same letters are at least a distance of 2 from each other.

---

### ✅ Constraints

- `1 <= s.length <= 3 * 10^5`
- `s` consists of only lowercase English letters.
- `0 <= k <= s.length`

---

### 💡 Solution (C++)

```cpp
class Solution {
public:
    string rearrangeString(string str, int k) {
        if(k == 0) return str;
        int length = (int)str.size();

        string res;
        unordered_map<char, int> dict;
        priority_queue<pair<int, char>> pq;

        for(char ch : str) dict[ch]++;
        for(auto it = dict.begin(); it != dict.end(); it++){
            pq.push(make_pair(it->second, it->first));
        }

        while(!pq.empty()){
            vector<pair<int, char>> cache; // store used chars during one while loop
            int count = min(k, length);    // how many steps in one while loop
            for(int i = 0; i < count; i++){
                if(pq.empty()) return "";
                auto tmp = pq.top();
                pq.pop();
                res.push_back(tmp.second);
                if(--tmp.first > 0) cache.push_back(tmp);
                length--;
            }
            for(auto p : cache) pq.push(p);
        }
        return res;
    }
};
```
