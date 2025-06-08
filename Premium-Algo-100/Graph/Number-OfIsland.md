## 305. Number of Islands II

**Difficulty:** Hard  
**Tags:** Union Find, Graph, Dynamic Connectivity  
**Companies:** —

---

### 📝 Problem Description

You start with an empty 2D grid (`m` rows and `n` columns) filled with water (0s). You perform a series of operations turning water cells into land cells (1s) at given positions.

After each operation, return the number of islands in the grid.

An island is formed by connecting adjacent lands horizontally or vertically.

---

### 📘 Example

Input:
m = 3, n = 3,
positions = [[0,0],[0,1],[1,2],[2,1]]

Output: [1,1,2,3]

Explanation:
Initially all water.

Add land at (0,0): islands = 1

Add land at (0,1): still 1 island (connected horizontally)

Add land at (1,2): new island formed, islands = 2

Add land at (2,1): new island formed, islands = 3

---

### ✅ Constraints

- 1 <= m, n, positions.length <= 10^4
- 1 <= m \* n <= 10^4
- positions[i].length == 2
- 0 <= ri < m
- 0 <= ci < n

---

### 💡 Approach

Use **Union-Find (Disjoint Set Union - DSU)** to dynamically manage islands as new land cells are added.

- Represent each cell as a node in DSU.
- Initially, all cells are water (`parent = -1` means water).
- For each addLand operation:
  - Mark the cell as land (`parent[idx] = idx`).
  - Increase island count by 1.
  - Check 4 neighbors; if neighbor is land and belongs to a different island, union them and decrease island count.
- Return island count after each operation.

Time complexity: Amortized near O(k α(mn)) (α is inverse Ackermann function), which is efficient for given constraints.

---

### 💻 Code (C++)

```cpp
class Solution {
    vector<int> parent, rank;

    int find(int x) {
        if (parent[x] != x)
            parent[x] = find(parent[x]); // Path compression
        return parent[x];
    }

    bool unite(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);

        if (rootX == rootY) return false; // Already in same set

        if (rank[rootX] < rank[rootY]) {
            parent[rootX] = rootY;
        } else if (rank[rootX] > rank[rootY]) {
            parent[rootY] = rootX;
        } else {
            parent[rootY] = rootX;
            rank[rootX]++;
        }

        return true;
    }

public:
    vector<int> numIslands2(int m, int n, vector<vector<int>>& positions) {
        parent.resize(m * n, -1);
        rank.resize(m * n, 0);
        vector<int> result;
        int islands = 0;

        vector<vector<int>> dirs = {{0,1},{1,0},{-1,0},{0,-1}};

        for (auto& pos : positions) {
            int r = pos[0], c = pos[1];
            int idx = r * n + c;

            if (parent[idx] != -1) {
                // Already land, no change
                result.push_back(islands);
                continue;
            }

            parent[idx] = idx; // Mark as land
            islands++;

            // Union with neighbors if possible
            for (auto& dir : dirs) {
                int nr = r + dir[0], nc = c + dir[1];
                int nidx = nr * n + nc;

                if (nr < 0 || nc < 0 || nr >= m || nc >= n || parent[nidx] == -1)
                    continue;

                if (unite(idx, nidx))
                    islands--;
            }

            result.push_back(islands);
        }

        return result;
    }
};
```
