## [250. Count Univalue Subtrees](https://leetcode.com/problems/count-univalue-subtrees/)

**Difficulty:** Medium  
**Tags:** Tree, Depth-First Search, Binary Tree  
**Companies:** Amazon, Google, Zeta, Bloomberg

---

### 📝 Problem Statement

Given the root of a binary tree, return the number of uni-value subtrees.

A **uni-value subtree** means all nodes of the subtree have the same value.

---

### 📘 Examples

**Example 1:**  
Input: `root = [5,1,5,5,5,null,5]`  
Output: `4`

**Example 2:**  
Input: `root = []`  
Output: `0`

**Example 3:**  
Input: `root = [5,5,5,5,5,null,5]`  
Output: `6`

---

### ✅ Constraints

- The number of nodes in the tree is in the range `[0, 1000]`.
- `-1000 <= Node.val <= 1000`

---

### 💡 Solution (C++)

```cpp
class Solution {
public:
    int countUnivalSubtrees(TreeNode* root) {
        int count = 0;
        countUnivalSubtreesRecursive(root, count);
        return count;
    }

    bool countUnivalSubtreesRecursive(TreeNode* root, int& count) {
        if (root == nullptr) return true;

        bool isLeftUnival = countUnivalSubtreesRecursive(root->left, count);
        bool isRightUnival = countUnivalSubtreesRecursive(root->right, count);

        if (isLeftUnival && isRightUnival &&
            (root->left == nullptr || root->left->val == root->val) &&
            (root->right == nullptr || root->right->val == root->val)) {
            ++count;
            return true;
        }

        return false;
    }
};
```
