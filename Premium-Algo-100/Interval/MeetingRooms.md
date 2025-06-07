## [252. Meeting Rooms](https://leetcode.com/problems/meeting-rooms/)

**Difficulty:** Easy  
**Tags:** Array, Sorting  
**Companies:** Amazon, Google, Meta, TikTok, Microsoft, Uber, Apple, Adobe, Oracle

---

### 📝 Description

You are given an array of meeting time intervals `intervals`, where `intervals[i] = [start_i, end_i]`.

**Task:**  
Return `true` if a person **can attend all meetings**, i.e., **no overlapping** intervals exist.  
Otherwise, return `false`.

---

### 📘 Examples

**Example 1:**

**Input:**  
`intervals = [[0,30],[5,10],[15,20]]`  
**Output:**  
`false`  
**Reason:** Meetings overlap, e.g., `[0,30]` overlaps with `[5,10]`.

---

**Example 2:**

**Input:**  
`intervals = [[7,10],[2,4]]`  
**Output:**  
`true`  
**Reason:** No overlaps.

---

### ✅ Constraints

- `0 <= intervals.length <= 10⁴`
- `intervals[i].length == 2`
- `0 <= start_i < end_i <= 10⁶`

---

### 💡 Solution (C++)

```cpp
class Solution {
public:
    bool canAttendMeetings(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end());  // Sort by start time

        int n = intervals.size();
        for (int i = 0; i < n - 1; ++i) {
            if (intervals[i][1] > intervals[i + 1][0]) {
                // If current meeting ends after next meeting starts
                return false;
            }
        }

        return true;
    }
};
```
