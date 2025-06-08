## [323. Number of Connected Components in an Undirected Graph](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/)

**Difficulty:** Medium  
**Tags:** DFS, BFS, Union Find, Graph  
**Companies:** General Motors, Amazon, LinkedIn, Google, Meta, TikTok

---

### 📝 Problem Description

Given `n` nodes labeled from `0` to `n-1` and an array `edges` where each `edges[i] = [ai, bi]` represents an undirected edge between nodes `ai` and `bi`, return the number of connected components in the graph.

---

### 📘 Examples

**Example 1:**  
Input: `n = 5`, `edges = [[0,1],[1,2],[3,4]]`  
Output: `2`

**Example 2:**  
Input: `n = 5`, `edges = [[0,1],[1,2],[2,3],[3,4]]`  
Output: `1`

---

### ✅ Constraints

- `1 <= n <= 2000`
- `1 <= edges.length <= 5000`
- `edges[i].length == 2`
- `0 <= ai, bi < n`
- `ai != bi`
- No repeated edges.

---

### 💡 Approach

- Construct adjacency list for the graph.
- Maintain a visited array to track visited nodes.
- Iterate over all nodes:
  - If a node is not visited, perform DFS/BFS from that node to visit all nodes in its component.
  - Increment connected components count.
- Return the count of connected components.

---

### 💻 Code (C++)

```cpp
class Solution {
    void dfs(int node, vector<vector<int>>& adj, vector<int>& visit) {
        visit[node] = 1;
        for (int neighbor : adj[node]) {
            if (!visit[neighbor])
                dfs(neighbor, adj, visit);
        }
    }
public:
    int countComponents(int n, vector<vector<int>>& edges) {
        vector<vector<int>> adj(n);
        vector<int> visit(n, 0);

        for (auto& edge : edges) {
            adj[edge[0]].push_back(edge[1]);
            adj[edge[1]].push_back(edge[0]);
        }

        int count = 0;
        for (int i = 0; i < n; i++) {
            if (!visit[i]) {
                count++;
                dfs(i, adj, visit);
            }
        }

        return count;
    }
};
```
