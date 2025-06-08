## [1059. All Paths from Source Lead to Destination](https://leetcode.com/problems/all-paths-from-source-lead-to-destination/)

**Difficulty:** Medium  
**Tags:** Graph, DFS, Topological Sort  
**Companies:** Google

---

### 📝 Problem Description

Given a directed graph with edges `edges[i] = [ai, bi]` and two nodes `source` and `destination`, determine if **all** paths starting from `source` eventually end at `destination`.

Specifically:

- At least one path exists from `source` to `destination`.
- If a path from `source` reaches a node with no outgoing edges, that node **must** be `destination`.
- The number of paths from `source` to `destination` is finite (i.e., no infinite cycles reachable from `source`).

Return `true` if and only if all paths from `source` lead to `destination`.

---

### 📘 Examples

**Example 1:**  
Input: `n = 3`, `edges = [[0,1],[0,2]]`, `source = 0`, `destination = 2`  
Output: `false`  
Explanation: From `0` you can go to `1` or `2`. Node `1` is a dead-end not equal to `destination`.

**Example 2:**  
Input: `n = 4`, `edges = [[0,1],[0,3],[1,2],[2,1]]`, `source = 0`, `destination = 3`  
Output: `false`  
Explanation: There is a cycle between nodes `1` and `2`, so paths do not necessarily lead to `3`.

**Example 3:**  
Input: `n = 4`, `edges = [[0,1],[0,2],[1,3],[2,3]]`, `source = 0`, `destination = 3`  
Output: `true`  
Explanation: All paths from `0` lead to `3`.

---

### ✅ Constraints

- `1 <= n <= 10^4`
- `0 <= edges.length <= 10^4`
- `edges[i].length == 2`
- `0 <= ai, bi <= n-1`
- `0 <= source, destination <= n-1`
- Graph may have self-loops and parallel edges.

---

### 💡 Approach

- Use DFS with memoization (`visited` array) to detect:
  - If current node leads only to `destination` or nodes that do.
  - Avoid infinite loops by marking nodes as visiting (`0`) or visited (`1`).
- If a node has no outgoing edges, it must be `destination`.
- If any path leads to a dead-end or cycle not reaching `destination`, return false.

---

### 💻 Code (C++)

```cpp
class Solution {
public:
    // visited: -1 = unvisited, 0 = visiting, 1 = safe (leads to destination)
    bool dfs(vector<vector<int>>& adj, vector<int>& visited, int node, int destination) {
        if (adj[node].empty())
            return node == destination;

        if (visited[node] != -1)
            return visited[node] == 1;

        visited[node] = 0; // mark as visiting

        for (int next : adj[node]) {
            if (!dfs(adj, visited, next, destination))
                return false;
        }

        visited[node] = 1; // mark as safe
        return true;
    }

    bool leadsToDestination(int n, vector<vector<int>>& edges, int source, int destination) {
        vector<vector<int>> adj(n);
        for (auto& e : edges) {
            adj[e[0]].push_back(e[1]);
        }
        vector<int> visited(n, -1);
        return dfs(adj, visited, source, destination);
    }
};
```
