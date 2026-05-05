# <u>61. Rotate List</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/rotate-list/

---

## 🧠 Intuition:
* 🔹 The task is to rotate the linked list to the right by `k` positions

* 🔹 Directly rotating `k` times would be inefficient, so we optimize using list properties

* 🔹 First, handle edge cases:
    - If list is empty, has one node, or `k = 0` → return as is

* 🔹 Traverse the list to:
    - Find the **length** of the list
    - Reach the **tail node**

* 🔹 Connect the tail to the head → this **forms a circular linked list**

* 🔹 Rotation by k steps is equivalent to moving (`length - k % length`) steps from the head
    - This avoids unnecessary full rotations

* 🔹 Move the pointer `t = length - (k % length)` steps from the current tail

* 🔹 The node next to this position becomes the **new head**

* 🔹 Break the circular link by setting `tail.next = null`

* 🔹 Return the new head

* 🔹 This approach efficiently reuses the list structure instead of creating new nodes

---

## ⏱ Time Complexity

**O(n)**

* Traversing list to find length → **O(n)**
* Moving pointer to new position → **O(n)**

---

## 📦 Space Complexity

**O(1)**

* Only pointers are used, no extra data structures

---

## 💻 Java Code

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode rotateRight(ListNode head, int k) {
       if (head == null || head.next == null || k == 0)
       return head;

        int length = 1;
        ListNode tail = head;
        for (; tail.next != null; tail = tail.next)
          ++length;
        tail.next = head; // Circle the list.

        final int t = length - k % length;
        for (int i = 0; i < t; ++i)
          tail = tail.next;
        ListNode newHead = tail.next;
        tail.next = null;

        return newHead; 
    }
}
```

---