## 314. Binary Tree Vertical Order Traversal

**Difficulty:** Medium  
**Topics:** Hash Table, Tree, BFS, DFS, Sorting, Binary Tree  
**Companies:** Meta, Google, Bloomberg, Amazon, DoorDash, Microsoft, Apple, TikTok, Oracle, Snap

---

### Problem Description

Given the root of a binary tree, return the vertical order traversal of its nodes' values. The traversal should be done column by column, from leftmost column to rightmost.

- Nodes in the same column should be ordered from top to bottom.
- If two nodes share the same row and column, they should appear in left-to-right order.

---

### Examples

**Example 1:**  
Input: `root = [3,9,20,null,null,15,7]`  
Output: `[[9],[3,15],[20],[7]]`

**Example 2:**  
Input: `root = [3,9,8,4,0,1,7]`  
Output: `[[4],[9],[3,0,1],[8],[7]]`

**Example 3:**  
Input: `root = [1,2,3,4,10,9,11,null,5,null,null,null,null,null,null,null,6]`  
Output: `[[4],[2,5],[1,10,9,6],[3],[11]]`

---

### Constraints

- Number of nodes: `[0, 100]`
- Node values: `[-100, 100]`

---

### Solution (C++)

```cpp
class Solution {
public:
    vector<vector<int>> verticalOrder(TreeNode* root) {
        if (!root) return {};

        // Map: horizontal distance (column) -> nodes in that column in top-down order
        map<int, vector<int>> columnTable;
        // Queue stores pairs of (node, horizontal distance)
        queue<pair<TreeNode*, int>> q;

        q.push({root, 0});

        while (!q.empty()) {
            auto [node, hd] = q.front(); q.pop();
            columnTable[hd].push_back(node->val);

            if (node->left) q.push({node->left, hd - 1});
            if (node->right) q.push({node->right, hd + 1});
        }

        vector<vector<int>> result;
        for (auto& [col, nodes] : columnTable) {
            result.push_back(nodes);
        }

        return result;
    }
};
```
