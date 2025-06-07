# Remove Interval

## 🧩 Problem Statement

A set of real numbers can be represented as the union of several disjoint intervals, where each interval is in the form `[a, b)` — including `a` but excluding `b`. A real number `x` is in the set if it lies within any of these intervals.

You are given:

- A sorted list of disjoint intervals `intervals`, where `intervals[i] = [a_i, b_i)` represents the interval `[a_i, b_i)`.
- Another interval `toBeRemoved = [start, end)`.

Return the set of real numbers after **removing** the interval `toBeRemoved` from the union of the `intervals`. In other words, return a sorted list of disjoint intervals representing the set of numbers in `intervals` but **not** in `toBeRemoved`.

---

## 🧪 Examples

### Example 1:

Input: intervals = [[0,2],[3,4],[5,7]], toBeRemoved = [1,6]
Output: [[0,1],[6,7]]

### Example 2:

Input: intervals = [[0,5]], toBeRemoved = [2,3]
Output: [[0,2],[3,5]]

### Example 3:

Input: intervals = [[-5,-4],[-3,-2],[1,2],[3,5],[8,9]], toBeRemoved = [-1,4]
Output: [[-5,-4],[-3,-2],[4,5],[8,9]]

---

## ✅ Constraints

- `1 <= intervals.length <= 10^4`
- `-10^9 <= a_i < b_i <= 10^9`
- Intervals are sorted and disjoint.

---

## 💡 Approach

- Iterate through each interval in `intervals`.
- If the current interval lies **completely outside** `toBeRemoved`, add it as is.
- Otherwise, if there's an intersection:
  - Add the left portion if any (`[interval_start, toBeRemoved_start)`).
  - Add the right portion if any (`[toBeRemoved_end, interval_end)`).
- Return the list of intervals after removal.

---

## 📝 Code (C++)

```cpp
class Solution {
public:
    vector<vector<int>> removeInterval(vector<vector<int>>& intervals, vector<int>& toBeRemoved) {
        vector<vector<int>> res;
        int start = toBeRemoved[0], end = toBeRemoved[1];

        for (auto &v : intervals) {
            // Interval completely before or after toBeRemoved
            if (v[1] <= start || v[0] >= end) {
                res.push_back(v);
            } else {
                // Left part outside toBeRemoved
                if (v[0] < start)
                    res.push_back({v[0], start});

                // Right part outside toBeRemoved
                if (v[1] > end)
                    res.push_back({end, v[1]});
            }
        }
        return res;
    }
};

```
