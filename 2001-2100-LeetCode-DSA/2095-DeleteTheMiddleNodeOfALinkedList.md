# <u>2095. Delete the Middle Node of a Linked List</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/delete-the-middle-node-of-a-linked-list/

---

## 🧠 Intuition:
* 🔹 We need to delete the middle node of a singly linked list and return the updated head

* 🔹 Since linked lists do not allow direct indexing, using the **slow and fast pointer technique** is the most efficient approach

* 🔹 Create a `dummy` node before `head` so deletion becomes easier, especially when the list has only one node or when deletion affects the head area

* 🔹 Initialize both `slow` and `fast` pointers at the dummy node

* 🔹 Move:
    - `slow` by 1 step
    - `fast` by 2 steps

* 🔹 When `fast` reaches the end of the list, `slow` will be standing just before the middle node

* 🔹 This works because fast travels twice as quickly, so slow reaches the middle-predecessor position exactly when fast finishes

* 🔹 Once `slow` is before the middle node, delete it using:
    - `slow.next = slow.next.next`

* 🔹 This skips the middle node and reconnects the list

* 🔹 Finally, return `dummy.next` as the updated head of the linked list

* 🔹 Using dummy node avoids special edge-case handling and keeps the logic clean

---

## ⏱ Time Complexity

**O(n)**

* Where:
    - `n` = number of nodes in the linked list

* We traverse the linked list only once using slow and fast pointers

---

## 📦 Space Complexity

**O(1)**

* Only a few extra pointers are used (`dummy`, `slow`, `fast`)

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
    public ListNode deleteMiddle(ListNode head) {
        ListNode dummy = new ListNode(0, head);
        ListNode slow = dummy;
        ListNode fast = dummy;

        while (fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        // Delete the middle node
        slow.next = slow.next.next;
        return dummy.next;
    }
}
```

---