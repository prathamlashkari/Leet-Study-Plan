## [708. Insert into a Sorted Circular Linked List](https://leetcode.com/problems/insert-into-a-sorted-circular-linked-list/)

**Difficulty:** Medium  
**Tags:** Linked List  
**Companies:** Meta, Google, Amazon, TikTok

---

### 📝 Description

Given a Circular Linked List node, which is sorted in non-descending order, write a function to insert a value `insertVal` into the list such that it remains a sorted circular list. The given node can be a reference to any single node in the list and may not necessarily be the smallest value in the circular list.

If there are multiple suitable places for insertion, you may choose any place to insert the new value. After the insertion, the circular list should remain sorted.

If the list is empty (i.e., the given node is null), you should create a new single circular list and return the reference to that single node. Otherwise, return the originally given node.

---

### 📘 Examples

**Input:**  
`head = [3,4,1]`, `insertVal = 2`  
**Output:**  
`[3,4,1,2]`  
**Explanation:**  
There is a sorted circular list of three elements. Insert `2` between node `1` and node `3`. Return node `3`.

---

**Input:**  
`head = []`, `insertVal = 1`  
**Output:**  
`[1]`  
**Explanation:**  
List is empty, create a new single circular list and return the node.

---

**Input:**  
`head = [1]`, `insertVal = 0`  
**Output:**  
`[1,0]`

---

### ✅ Constraints

- Number of nodes in the list is in the range `[0, 5 * 10^4]`.
- `-10^6 <= Node.val, insertVal <= 10^6`

---

### 💡 Solution (C++)

```cpp
class Node {
public:
    int val;
    Node* next;
    Node(int _val, Node* _next = nullptr) : val(_val), next(_next) {}
};

class Solution {
public:
    Node* insert(Node* head, int insertVal) {
        if (!head) {
            head = new Node(insertVal, nullptr);
            head->next = head;
            return head;
        }

        Node* prev = head;
        Node* next = head->next;
        bool inserted = false;

        while (true) {
            if ((prev->val <= insertVal && insertVal <= next->val) ||
                (prev->val > next->val && insertVal < next->val) ||
                (prev->val > next->val && insertVal > prev->val)) {
                prev->next = new Node(insertVal, next);
                inserted = true;
                break;
            }

            prev = prev->next;
            next = next->next;
            if (prev == head) break;
        }

        if (!inserted) {
            prev->next = new Node(insertVal, next);
        }

        return head;
    }
};
```
