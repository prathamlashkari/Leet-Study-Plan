## 545. Boundary of Binary Tree

**Difficulty:** Medium  
**Topics:** Tree, Depth-First Search, Binary Tree  
**Companies:** Meta, Amazon, Microsoft, Uber, Nutanix, Snowflake, Apple, Geico, Google, Walmart Labs, BlackRock

---

### Problem Description

Given the root of a binary tree, return the values of its **boundary**.

The boundary of a binary tree is defined as:

- The root node,
- The **left boundary** (excluding leaves),
- All **leaves** ordered from left to right,
- The **right boundary** (excluding leaves) in reverse order.

**Left boundary** rules:

- Start from the root's left child.
- Traverse down preferring the left child. If the left child is missing, take the right child.
- Exclude the leftmost leaf.

**Right boundary** rules:

- Start from the root's right child.
- Traverse down preferring the right child. If the right child is missing, take the left child.
- Exclude the rightmost leaf.
- The right boundary is added in reverse order.

---

### Examples

**Example 1:**  
Input: `root = [1,null,2,3,4]`  
Output: `[1,3,4,2]`  
Explanation:

- Left boundary is empty (no left child of root).
- Leaves: 3,4
- Right boundary: 2 (excluding leaf 4)
- Boundary = [1] + [] + [3,4] + [2] = [1,3,4,2]

**Example 2:**  
Input: `root = [1,2,3,4,5,6,null,null,null,7,8,9,10]`  
Output: `[1,2,4,7,8,9,10,6,3]`  
Explanation:

- Left boundary: 2 (4 is a leaf)
- Leaves: 4,7,8,9,10
- Right boundary (in reverse): 6,3
- Boundary = [1] + [2] + [4,7,8,9,10] + [6,3]

---

### Constraints

- Number of nodes in the tree: `[1, 10^4]`
- `-1000 <= Node.val <= 1000`

---

### Solution (C++)

```cpp
class Solution {
public:
    vector<int> boundaryOfBinaryTree(TreeNode* root) {
        vector<int> res;
        if (!root) return res;

        res.push_back(root->val);
        if (!root->left && !root->right) {
            // Root is a leaf, just return
            return res;
        }

        vector<int> leftBoundary, leaves, rightBoundary;

        getLeftBoundary(root->left, leftBoundary);
        getLeaves(root, leaves);
        getRightBoundary(root->right, rightBoundary);

        reverse(rightBoundary.begin(), rightBoundary.end());

        // Concatenate all parts
        for (int val : leftBoundary) res.push_back(val);
        for (int val : leaves) res.push_back(val);
        for (int val : rightBoundary) res.push_back(val);

        return res;
    }

private:
    void getLeftBoundary(TreeNode* node, vector<int>& leftBoundary) {
        if (!node || (node->left == nullptr && node->right == nullptr)) return;
        leftBoundary.push_back(node->val);
        if (node->left) getLeftBoundary(node->left, leftBoundary);
        else getLeftBoundary(node->right, leftBoundary);
    }

    void getLeaves(TreeNode* node, vector<int>& leaves) {
        if (!node) return;
        if (!node->left && !node->right) {
            leaves.push_back(node->val);
            return;
        }
        getLeaves(node->left, leaves);
        getLeaves(node->right, leaves);
    }

    void getRightBoundary(TreeNode* node, vector<int>& rightBoundary) {
        if (!node || (node->left == nullptr && node->right == nullptr)) return;
        rightBoundary.push_back(node->val);
        if (node->right) getRightBoundary(node->right, rightBoundary);
        else getRightBoundary(node->left, rightBoundary);
    }
};
```
