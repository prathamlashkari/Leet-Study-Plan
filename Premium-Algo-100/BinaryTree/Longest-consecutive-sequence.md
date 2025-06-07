## [298. Binary Tree Longest Consecutive Sequence](https://leetcode.com/problems/binary-tree-longest-consecutive-sequence/)

**Difficulty:** Medium  
**Tags:** Tree, Depth-First Search, Binary Tree  
**Companies:** Amazon, TikTok, Google, Walmart Labs

---

### 📝 Description

Given the root of a binary tree, return the length of the longest consecutive sequence path.

A consecutive sequence path is a path where the values increase by one along the path.

Note that the path can start at any node in the tree, and you cannot go from a node to its parent in the path.

---

### 📘 Examples

**Input:**  
`root = [1,null,3,2,4,null,null,null,5]`  
**Output:**  
`3`  
**Explanation:** Longest consecutive sequence path is 3-4-5, so return 3.

---

**Input:**  
`root = [2,null,3,2,null,1]`  
**Output:**  
`2`  
**Explanation:** Longest consecutive sequence path is 2-3, not 3-2-1, so return 2.

---

### ✅ Constraints

- The number of nodes in the tree is in the range `[1, 3 * 10^4]`.
- `-3 * 10^4 <= Node.val <= 3 * 10^4`

---

### 💡 Solution (Java)

```java
public class Solution {
    private int max = 0;
    public int longestConsecutive(TreeNode root) {
        if(root == null) return 0;
        helper(root, 0, root.val);
        return max;
    }

    public void helper(TreeNode root, int cur, int target){
        if(root == null) return;
        if(root.val == target) cur++;
        else cur = 1;
        max = Math.max(cur, max);
        helper(root.left, cur, root.val + 1);
        helper(root.right, cur, root.val + 1);
    }
}
```
