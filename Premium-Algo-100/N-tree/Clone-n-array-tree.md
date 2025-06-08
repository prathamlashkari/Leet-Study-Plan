## [1490. Clone N-ary Tree](https://leetcode.com/problems/clone-n-ary-tree/)

**Difficulty:** Medium  
**Tags:** Hash Table, Tree, Depth-First Search, Breadth-First Search  
**Companies:** Amazon

---

### 📝 Description

Given a root of an N-ary tree, return a deep copy (clone) of the tree.

Each node in the N-ary tree contains a `val` (int) and a list (`List[Node]`) of its children.

N-ary tree input serialization is represented in their level order traversal, each group of children is separated by the null value (see examples).

📘 Examples
Input:
root = [1,null,3,2,4,null,5,6]
Output:
[1,null,3,2,4,null,5,6]

Input:
root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
Output:
[1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]

✅ Constraints
The depth of the N-ary tree is less than or equal to 1000.

The total number of nodes is between [0, 10⁴].

💡 Follow up
Can your solution work for the graph problem?

```cpp
💡 Solution (C++)
class Solution {
public:
Node* cloneTree(Node* r) {
if (r == nullptr)
return nullptr;
auto new_r = new Node(r->val);
for (auto child : r->children)
new_r->children.push_back(cloneTree(child));
return new_r;
}
};

```

```

```
