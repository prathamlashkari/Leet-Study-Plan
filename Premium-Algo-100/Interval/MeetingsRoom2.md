## [253. Meeting Rooms II](https://leetcode.com/problems/meeting-rooms-ii/)

**Difficulty:** Medium  
**Tags:** Array, Two Pointers, Greedy, Sorting, Heap (Priority Queue)  
**Companies:** Amazon, Google, Meta, IBM, Microsoft, Apple, Uber, TikTok

---

### 📝 Description

Given an array of meeting time intervals `intervals` where `intervals[i] = [start_i, end_i]`, return the **minimum number of conference rooms required**.

---

### 📘 Examples

**Example 1:**

**Input:**  
`intervals = [[0,30],[5,10],[15,20]]`  
**Output:** `2`  
**Explanation:**

- Room 1: [0,30]
- Room 2: [5,10] and then [15,20]

---

**Example 2:**

**Input:**  
`intervals = [[7,10],[2,4]]`  
**Output:** `1`  
**Explanation:**  
No overlaps, can be done in one room.

---

### ✅ Constraints

- `1 <= intervals.length <= 10⁴`
- `0 <= start_i < end_i <= 10⁶`

---

### 💡 Solution (Java - Two Pointers)

```java
import java.util.*;

class Solution {
    public int minMeetingRooms(int[][] intervals) {
        if (intervals.length == 0) return 0;

        int n = intervals.length;
        int[] start = new int[n];
        int[] end = new int[n];

        // Extract start and end times
        for (int i = 0; i < n; i++) {
            start[i] = intervals[i][0];
            end[i] = intervals[i][1];
        }

        // Sort start and end times separately
        Arrays.sort(start);
        Arrays.sort(end);

        int rooms = 0, endPtr = 0;
        for (int i = 0; i < n; i++) {
            if (start[i] < end[endPtr]) {
                // New room needed
                rooms++;
            } else {
                // One meeting ended, move pointer
                endPtr++;
            }
        }

        return rooms;
    }
}
```
