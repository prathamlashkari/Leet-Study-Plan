## [Print Immutable Linked List in Reverse](https://leetcode.com/problems/print-immutable-linked-list-in-reverse/)

**Difficulty:** Easy  
**Tags:** Linked List, Two Pointers, Stack, Recursion  
**Companies:** Amazon

---

### 📝 Description

You are given an immutable linked list, print out all values of each node in reverse order using the following interface:

- `ImmutableListNode.printValue()`: Print value of the current node.
- `ImmutableListNode.getNext()`: Return the next node.

You cannot modify the linked list and can only access it via the provided API.

---

### 📘 Examples

**Input:**  
`head = [1,2,3,4]`  
**Output:**  
`[4,3,2,1]`

---

**Input:**  
`head = [0,-4,-1,3,-5]`  
**Output:**  
`[-5,3,-1,-4,0]`

---

**Input:**  
`head = [-2,0,6,4,4,-6]`  
**Output:**  
`[-6,4,4,6,0,-2]`

---

### ✅ Constraints

- Length of linked list: `[1, 1000]`
- Node values: `[-1000, 1000]`

---

### 💡 Solution (C++)

```cpp
class Solution {
public:
    void printLinkedListInReverse(ImmutableListNode* head) {
        if (!head) return;
        printLinkedListInReverse(head->getNext());
        head->printValue();
    }
};
```
