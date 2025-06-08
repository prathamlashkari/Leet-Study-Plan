## [277. Find the Celebrity](https://leetcode.com/problems/find-the-celebrity/)

**Difficulty:** Medium  
**Tags:** Two Pointers, Graph, Interactive  
**Companies:** LinkedIn, Amazon, Meta, Google, Microsoft, DoorDash, TikTok

---

### 📝 Problem Description

You are at a party with `n` people labeled from `0` to `n-1`. There may exist one celebrity in the party.

**Celebrity Definition:**

- Everyone else knows the celebrity.
- The celebrity knows no one else.

You can only ask questions like: "Does person A know person B?" (via `knows(a, b)` function).  
Find the celebrity (if any) by minimizing calls to `knows`.

---

### 📘 Examples

**Example 1:**  
Input: graph = [[1,1,0],[0,1,0],[1,1,1]]  
Output: 1  
Explanation: Person 1 is known by everyone else, but knows no one.

**Example 2:**  
Input: graph = [[1,0,1],[1,1,0],[0,1,1]]  
Output: -1  
Explanation: No celebrity exists.

---

### ✅ Constraints

- `2 <= n <= 100`
- `graph[i][j]` is 0 or 1.
- `graph[i][i] == 1`
- The API `knows(a, b)` is provided.

---

### 💡 Approach

- Start by assuming `candidate = 0`.
- For each person `i` from 1 to n-1:
  - If `i` does not know the current candidate, then `i` becomes the new candidate.
- After this, verify if the candidate is actually the celebrity:
  - Check if everyone knows the candidate.
  - Check if candidate knows no one else.
- Return candidate if valid, else -1.

This approach uses **O(n)** calls to `knows` in the worst case, meeting the 3\*n limit.

---

### 💻 Code (C++)

```cpp
/* The knows API is defined for you.
      bool knows(int a, int b); */

class Solution {
public:
    int findCelebrity(int n) {
        if (n <= 1) return n;

        int candidate = 0;

        // Find candidate
        for (int i = 1; i < n; i++) {
            if (!knows(i, candidate)) {
                candidate = i;
            }
        }

        // Verify candidate
        for (int j = 0; j < n; j++) {
            if (j == candidate) continue;

            // Candidate should be known by everyone, and candidate knows no one
            if (!knows(j, candidate) || knows(candidate, j)) {
                return -1;
            }
        }

        return candidate;
    }
};
```
