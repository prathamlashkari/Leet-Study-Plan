## 366. Find Leaves of Binary Tree

**Difficulty:** Medium  
**Topics:** Tree, Depth-First Search, Binary Tree  
**Companies:** LinkedIn, Amazon, Google, Salesforce, Yahoo

---

### Problem Description

Given the root of a binary tree, collect its nodes in the following way:

- Collect all the leaf nodes.
- Remove all those leaf nodes from the tree.
- Repeat the process until the tree is empty.

Return a list of lists, where each inner list contains the values of the leaves collected at that iteration.

---

### Examples

**Example 1:**  
Input: `root = [1,2,3,4,5]`  
Output: `[[4,5,3],[2],[1]]`  
Explanation:

- First leaves are 4,5,3
- Remove them → next leaves: 2
- Remove it → last leaf: 1

**Example 2:**  
Input: `root = [1]`  
Output: `[[1]]`

---

### Constraints

- Number of nodes in the tree: `[1, 100]`
- Node values: `[-100, 100]`

---

### Solution (C++)

```cpp
class Solution {
private:
    int dfs(TreeNode* root, vector<vector<int>>& res) {
        if (!root) return 0;
        int leftHeight = dfs(root->left, res);
        int rightHeight = dfs(root->right, res);
        int currLevel = max(leftHeight, rightHeight) + 1;

        if (currLevel > (int)res.size())
            res.push_back(vector<int>());

        res[currLevel - 1].push_back(root->val);
        return currLevel;
    }
public:
    vector<vector<int>> findLeaves(TreeNode* root) {
        vector<vector<int>> res;
        dfs(root, res);
        return res;
    }
};
```
