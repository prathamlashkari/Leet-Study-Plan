## [582. Kill Process](https://leetcode.com/problems/kill-process/)

**Difficulty:** Medium  
**Tags:** Array, Hash Table, Tree, BFS, DFS  
**Companies:** Bloomberg, Amazon, Oracle

---

### 📝 Problem Description

You have `n` processes forming a rooted tree. Given two integer arrays:

- `pid`: process IDs
- `ppid`: parent process IDs corresponding to each process in `pid`

Each process has exactly one parent except the root process whose parent ID is 0.

When you kill a process, you also kill all its descendants (children, grandchildren, etc.).

Given a process ID `kill`, return all processes that will be killed.

---

### 📘 Examples

**Example 1:**  
Input: `pid = [1,3,10,5]`, `ppid = [3,0,5,3]`, `kill = 5`  
Output: `[5,10]`  
Explanation: Killing process 5 kills 5 and its child 10.

**Example 2:**  
Input: `pid = [1]`, `ppid = [0]`, `kill = 1`  
Output: `[1]`

---

### ✅ Constraints

- `1 <= n <= 5 * 10^4`
- All `pid` are unique.
- Exactly one root process (ppid = 0).
- `kill` is guaranteed to be in `pid`.

---

### 💡 Approach

- Use a map to record each process's children.
- Perform a BFS (or DFS) starting from `kill`:
  - Add `kill` to queue.
  - Pop from queue, add to result.
  - Push all children of popped node into the queue.
- Return all visited nodes.

---

### 💻 Code (C++)

```cpp
class Solution {
public:
    vector<int> killProcess(vector<int>& pid, vector<int>& ppid, int kill) {
        int n = pid.size();
        unordered_map<int, vector<int>> children;
        vector<int> result;
        queue<int> q;

        // Build map of parent -> children
        for (int i = 0; i < n; i++) {
            children[ppid[i]].push_back(pid[i]);
        }

        // BFS starting from kill
        q.push(kill);
        while (!q.empty()) {
            int cur = q.front();
            q.pop();
            result.push_back(cur);
            for (int child : children[cur]) {
                q.push(child);
            }
        }

        return result;
    }
};
```
