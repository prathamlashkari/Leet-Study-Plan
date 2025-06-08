## [1506. Find Root of N-Ary Tree](https://leetcode.com/problems/find-root-of-n-ary-tree/)

**Difficulty:** Medium  
**Tags:** Hash Table, Bit Manipulation, Tree, Depth-First Search  
**Companies:** Bloomberg, Google

---

### 📝 Description

You are given all the nodes of an N-ary tree as an array of Node objects, where each node has a unique value.

Return the root of the N-ary tree.

The input array contains all nodes in an arbitrary order.

---

### 📘 Example

**Input:**  
tree = [1,null,3,2,4,null,5,6]

**Output:**  
[1,null,3,2,4,null,5,6]

**Explanation:**  
The root node is Node with value 1. The function receives nodes in any order but must identify the root.

---

### ✅ Constraints

- The total number of nodes is between [1, 5 * 10⁴].
- Each node has a unique value.

---

### 💡 Follow-up

Can you solve this problem in constant space complexity with a linear time algorithm?

---

### 💡 Solution (Java)

```java
class Solution {
    public Node findRoot(List<Node> tree) {
        // Edge Case
        if (tree == null || tree.size() == 0) return null;

        Set<Node> seen = new HashSet<>();

        // Add all children nodes to the set
        for (Node node : tree) {
            for (Node child : node.children) {
                seen.add(child);
            }
        }

        // The root node is the one not in the children set
        for (Node node : tree) {
            if (!seen.contains(node)) {
                return node;
            }
        }

        return null;
    }
}
```
