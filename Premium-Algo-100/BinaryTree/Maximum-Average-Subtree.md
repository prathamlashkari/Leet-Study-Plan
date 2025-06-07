## [1120. Maximum Average Subtree](https://leetcode.com/problems/maximum-average-subtree/)

**Difficulty:** Medium  
**Tags:** Tree, Depth-First Search, Binary Tree  
**Companies:** Meta, Amazon

---

### 📝 Problem Statement

Given the root of a binary tree, return the maximum average value of a subtree of that tree. Answers within `10^-5` of the actual answer will be accepted.

- A **subtree** of a tree is any node of that tree plus all its descendants.
- The **average value** of a tree is the sum of its values divided by the number of nodes.

---

### 📘 Examples

**Example 1:**  
Input: `root = [5,6,1]`  
Output: `6.00000`  
Explanation:

- For node with value 5, average is (5 + 6 + 1) / 3 = 4.0
- For node with value 6, average is 6 / 1 = 6.0
- For node with value 1, average is 1 / 1 = 1.0  
  Maximum average is 6.

**Example 2:**  
Input: `root = [0,null,1]`  
Output: `1.00000`

---

### ✅ Constraints

- The number of nodes in the tree is in the range `[1, 10^4]`.
- `0 <= Node.val <= 10^5`

---

### 💡 Solution (C++)

```cpp
class Solution {
    double ans = 0.0;

    // Returns pair {sum of subtree values, count of nodes in subtree}
    pair<double, int> avg(TreeNode* node) {
        if (!node) return {0, 0};

        auto left = avg(node->left);
        auto right = avg(node->right);

        double sum = node->val + left.first + right.first;
        int count = 1 + left.second + right.second;

        double currentAvg = sum / count;
        ans = max(ans, currentAvg);

        return {sum, count};
    }

public:
    double maximumAverageSubtree(TreeNode* root) {
        avg(root);
        return ans;
    }
};
```
