## [624. Maximum Distance in Arrays](https://leetcode.com/problems/maximum-distance-in-arrays/)

**Difficulty:** Medium  
**Tags:** Array, Greedy  
**Companies:** Google, Yahoo, Microsoft, Amazon, Bloomberg

---

### 📝 Description

You are given `m` arrays, where each array is sorted in ascending order.

You can pick up two integers from two different arrays (one from each) and calculate the distance.  
The **distance** between two integers `a` and `b` is `|a - b|`.

Return the **maximum** distance possible.

---

### 📘 Example

**Input:**  
`arrays = [[1,2,3],[4,5],[1,2,3]]`  
**Output:**  
`4`  
**Explanation:** Pick `1` from the first/last array and `5` from the second.

---

### ✅ Constraints

- `2 <= m <= 10⁵`
- `1 <= arrays[i].length <= 500`
- `-10⁴ <= arrays[i][j] <= 10⁴`
- Each `arrays[i]` is sorted in ascending order
- At most `10⁵` integers across all arrays

---

### 💡 Solution (C++)

```cpp
class Solution {
public:
    int maxDistance(vector<vector<int>>& arrays) {
        int maxDif = 0, curMin = 10000, curMax = -10000;
        for (auto& a : arrays) {
            maxDif = max(maxDif, max(a.back()-curMin, curMax-a.front()));
            curMin = min(curMin, a.front());
            curMax = max(curMax, a.back());
        }
        return maxDif;
    }
};
```
