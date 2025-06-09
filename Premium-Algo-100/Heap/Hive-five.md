## [1086. High Five](https://leetcode.com/problems/high-five/)

**Difficulty:** Easy  
**Tags:** Sorting, Hash Table, Heap  
**Companies:** (Not specified)

---

### 📝 Description

Given a list of the scores of different students, `items`, where `items[i] = [IDi, scorei]` represents one score from a student with ID `IDi`, calculate each student's top five average.

Return the answer as an array of pairs `result`, where `result[j] = [IDj, topFiveAveragej]` represents the student with ID `IDj` and their top five average. Sort `result` by `IDj` in increasing order.

A student's top five average is calculated by taking the sum of their top five scores and dividing it by 5 using integer division.

---

### 📘 Examples

**Input:**  
`items = [[1,91],[1,92],[2,93],[2,97],[1,60],[2,77],[1,65],[1,87],[1,100],[2,100],[2,76]]`  
**Output:**  
`[[1,87],[2,88]]`  
**Explanation:**  
The student with ID = 1 got scores 91, 92, 60, 65, 87, and 100. Their top five average is `(100 + 92 + 91 + 87 + 65) / 5 = 87`.  
The student with ID = 2 got scores 93, 97, 77, 100, and 76. Their top five average is `(100 + 97 + 93 + 77 + 76) / 5 = 88.6`, but with integer division their average converts to 88.

---

**Input:**  
`items = [[1,100],[7,100],[1,100],[7,100],[1,100],[7,100],[1,100],[7,100],[1,100],[7,100]]`  
**Output:**  
`[[1,100],[7,100]]`

---

### ✅ Constraints

- `1 <= items.length <= 1000`
- `items[i].length == 2`
- `1 <= IDi <= 1000`
- `0 <= scorei <= 100`
- For each `IDi`, there will be at least five scores.

---

### 💡 Solution (C++)

```cpp
class Solution {
public:
    vector<vector<int>> highFive(vector<vector<int>>& items) {
        vector<vector<int>> res;
        map<int, vector<int>> m;
        for (auto& v : items)
            m[v[0]].push_back(v[1]);
        for (auto& [i, v] : m) {
            partial_sort(v.begin(), v.begin() + 5, v.end(), greater<int>());
            res.push_back({ i, (v[0] + v[1] + v[2] + v[3] + v[4]) / 5 });
        }
        return res;
    }
};
```
