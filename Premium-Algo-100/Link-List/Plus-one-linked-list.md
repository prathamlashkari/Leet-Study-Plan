## [369. Plus One Linked List](https://leetcode.com/problems/plus-one-linked-list/)

**Difficulty:** Medium  
**Tags:** Linked List, Math  
**Companies:** Amazon, Google

---

### 📝 Description

Given a non-negative integer represented as a linked list of digits, plus one to the integer.

The digits are stored such that the most significant digit is at the head of the list.

---

### 📘 Examples

**Input:**  
`head = [1,2,3]`  
**Output:**  
`[1,2,4]`

---

**Input:**  
`head = [0]`  
**Output:**  
`[1]`

---

### ✅ Constraints

- The number of nodes in the linked list is in the range `[1, 100]`.
- `0 <= Node.val <= 9`
- The number represented by the linked list does not contain leading zeros except for the zero itself.

---

### 💡 Solution (Java)

```java
public class Solution {
    public ListNode plusOne(ListNode head) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode i = dummy;
        ListNode j = dummy;

        while (j.next != null) {
            j = j.next;
            if (j.val != 9) {
                i = j;
            }
        }
        i.val++;
        i = i.next;
        while (i != null) {
            i.val = 0;
            i = i.next;
        }

        if (dummy.val == 0) return dummy.next;
        return dummy;
    }
}
```
