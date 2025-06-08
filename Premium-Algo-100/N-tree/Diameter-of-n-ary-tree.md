## [1522. Diameter of N-Ary Tree](https://leetcode.com/problems/diameter-of-n-ary-tree/)

**Difficulty:** Medium  
**Tags:** Tree, Depth-First Search  
**Companies:** Meta, DoorDash

---

### 📝 Problem Description

Given the root of an N-ary tree, compute the **diameter** of the tree.

- The **diameter** is defined as the length of the longest path between any two nodes.
- The path may or may not pass through the root.
- The tree is represented by N-ary nodes where each node has a list of children.

---

### 📘 Examples

**Example 1:**  
Input: root = [1,null,3,2,4,null,5,6]  
Output: 3  
Explanation: The longest path (diameter) is shown with length 3.

**Example 2:**  
Input: root = [1,null,2,null,3,4,null,5,null,6]  
Output: 4

**Example 3:**  
Input: root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]  
Output: 7

---

### ✅ Constraints

- The depth of the tree ≤ 1000
- Number of nodes between [1, 10⁴]

---

### 💡 Intuition

The diameter can be found by tracking the two longest depths of subtrees for each node, updating the maximum diameter as we traverse.

---

### 💻 Solution (C++)

```cpp
class Solution {
public:
    int max_dia = 0;

    int diameter(Node* root, bool isRoot = true) {
        int max_depth = 0;
        int second_max_depth = 0;

        for (auto child : root->children) {
            int depth = 1 + diameter(child, false);

            if (depth > max_depth) {
                second_max_depth = max_depth;
                max_depth = depth;
            } else if (depth > second_max_depth) {
                second_max_depth = depth;
            }
        }

        max_dia = max(max_dia, max_depth + second_max_depth);

        return isRoot ? max_dia : max_depth;
    }
};
```
