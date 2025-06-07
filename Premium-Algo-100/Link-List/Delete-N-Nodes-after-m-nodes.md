## [1474. Delete N Nodes After M Nodes of a Linked List](https://leetcode.com/problems/delete-n-nodes-after-m-nodes-of-a-linked-list/)

**Difficulty:** Medium  
**Tags:** Linked List  
**Companies:** Microsoft

---

### 📝 Description

You are given the head of a linked list and two integers `m` and `n`.

Traverse the linked list and remove some nodes in the following way:

1. Start with the head as the current node.
2. Keep the first `m` nodes starting with the current node.
3. Remove the next `n` nodes.
4. Keep repeating steps 2 and 3 until you reach the end of the list.

Return the head of the modified list after removing the mentioned nodes.

---

### 📘 Examples

**Input:**  
`head = [1,2,3,4,5,6,7,8,9,10,11,12,13], m = 2, n = 3`  
**Output:**  
`[1,2,6,7,11,12]`  
**Explanation:**  
Keep the first `m = 2` nodes starting from the head (1 → 2). Delete the next `n = 3` nodes (3 → 4 → 5). Repeat until the end.

---

**Input:**  
`head = [1,2,3,4,5,6,7,8,9,10,11], m = 1, n = 3`  
**Output:**  
`[1,5,9]`  
**Explanation:**  
Return the head of the linked list after removing nodes as described.

---

### ✅ Constraints

- The number of nodes in the list is in the range `[1, 10^4]`.
- `1 <= Node.val <= 10^6`
- `1 <= m, n <= 1000`

---

### 💡 Follow up

Could you solve this problem by modifying the list in-place?

---

### 💡 Solution (C++)

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
   ListNode* deleteNodes(ListNode* head, int m, int n) {
    ListNode temp(0, head);
    for (auto p = &temp; p != nullptr; )
        for (int i = 0; i < n + m && p != nullptr; ++i)
            if (i < m)
                p = p->next;
            else if (p->next != nullptr)
                p->next = p->next->next;
    return head;
}
};
```
