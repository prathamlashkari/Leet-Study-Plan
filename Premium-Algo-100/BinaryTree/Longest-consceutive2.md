## [549. Binary Tree Longest Consecutive Sequence II](https://leetcode.com/problems/binary-tree-longest-consecutive-sequence-ii/)

**Difficulty:** Medium  
**Tags:** Tree, Depth-First Search, Binary Tree  
**Companies:** Google

---

### 📝 Description

Given the root of a binary tree, return the length of the longest consecutive path in the tree.

A consecutive path is a path where the values of the consecutive nodes in the path differ by one. This path can be either increasing or decreasing.

For example, `[1,2,3,4]` and `[4,3,2,1]` are both considered valid, but the path `[1,2,4,3]` is not valid.  
On the other hand, the path can be in the child-parent-child order, and not necessarily parent-child order.

---

### 📘 Examples

**Input:**  
`root = [1,2,3]`  
**Output:**  
`2`  
**Explanation:** The longest consecutive path is `[1, 2]` or `[2, 1]`.

---

**Input:**  
`root = [2,1,3]`  
**Output:**  
`3`  
**Explanation:** The longest consecutive path is `[1, 2, 3]` or `[3, 2, 1]`.

---

### ✅ Constraints

- The number of nodes in the tree is in the range `[1, 3 * 10^4]`.
- `-3 * 10^4 <= Node.val <= 3 * 10^4`

---

### 💡 Solution (C++)

```cpp
class Solution {
    int ans = 0;

    pair<int, int> dfs(TreeNode* node) {
        if (!node) return {0, 0};

        int inc = 1, dec = 1;

        if (node->left) {
            auto [l_inc, l_dec] = dfs(node->left);
            if (node->val == node->left->val + 1)
                dec = l_dec + 1;
            else if (node->val == node->left->val - 1)
                inc = l_inc + 1;
        }

        if (node->right) {
            auto [r_inc, r_dec] = dfs(node->right);
            if (node->val == node->right->val + 1)
                dec = max(dec, r_dec + 1);
            else if (node->val == node->right->val - 1)
                inc = max(inc, r_inc + 1);
        }

        ans = max(ans, inc + dec - 1);
        return {inc, dec};
    }

public:
    int longestConsecutive(TreeNode* root) {
        dfs(root);
        return ans;
    }
};
```
