# <u>328. Odd Even Linked List</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/odd-even-linked-list/

---

## 🧠 Intuition:
* 🔹 We need to rearrange the linked list such that all nodes at **odd indices** come first, followed by all nodes at **even indices**

* 🔹 The relative order among odd nodes and among even nodes must remain the same

* 🔹 Instead of creating new lists, we can rearrange pointers in-place for better efficiency

* 🔹 If the list has 0 or 1 node, it is already arranged, so return it directly

* 🔹 Use two pointers:
    - `curr1` → tracks the odd-position nodes
    - `curr2` → tracks the even-position nodes

* 🔹 Store the head of even-position nodes (`head.next`) in `temp1` because we need to attach the even list after the odd list at the end

* 🔹 Traverse the list while even pointer and its next exist

* 🔹 In each step:
    - Connect current odd node to the next odd node → `curr1.next = curr2.next`
    - Move odd pointer forward
    - Connect current even node to the next even node → `curr2.next = curr1.next`
    - Move even pointer forward

* 🔹 This separates odd-indexed nodes and even-indexed nodes into two linked chains

* 🔹 After traversal, connect the last odd node to the head of the even list (`temp1`)

* 🔹 Return the original head since odd nodes start from the original head

* 🔹 This keeps the order stable and uses only pointer manipulation without extra space

---

## ⏱ Time Complexity

**O(n)**

* Where :
    - `n` = number of nodes in the linked list

* Each node is visited only once during traversal

---

## 📦 Space Complexity

**O(1)**

* Only a few pointers are used (`curr1`, `curr2`, `temp1`)

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
    public ListNode oddEvenList(ListNode head) {
        if(head == null || head.next == null){
            return head;
        }

        ListNode curr1 = head, curr2 = head.next;
        ListNode temp1 = curr2;

        while(curr2 != null && curr2.next != null){
            curr1.next = curr2.next;
            curr1 = curr1.next;

            curr2.next = curr1.next;
            curr2 = curr2.next;
        }

        curr1.next = temp1;
        return head;
    }
}
```

---