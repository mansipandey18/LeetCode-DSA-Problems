# <u>206. Reverse Linked List</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/reverse-linked-list/

---

## 🧠 Intuition:
* 🔹 The goal is to reverse a singly linked list so that every node points to its previous node instead of the next

* 🔹 Since each node only has a `next` pointer, we must carefully **reverse links one by one** while traversing

* 🔹 Use three pointers:
    - `prev` → stores the previous node (initially `null`)
    - `curr` → current node being processed (starts from `head`)
    - `next` → temporarily stores the next node so we don’t lose the remaining list


* 🔹 Traverse the list until `curr` becomes `null`

* 🔹 At each step:
    - Save next node → `next = curr.next`
    - Reverse the link → `curr.next = prev`
    - Move `prev` forward → `prev = curr`
    - Move `curr` forward → `curr = next`

* 🔹 This process gradually reverses the direction of all links

* 🔹 At the end, `prev` will point to the new head of the reversed list

* 🔹 Return `prev` as the final answer

* 🔹 This is an **in-place reversal**, so no extra data structures are needed.

---

## ⏱ Time Complexity

**O(n)**

* Where : 
    - `n` = number of nodes in the linked list.

* Each node is visited exactly once
    
---

## 📦 Space Complexity

**O(1)**

* Only a few pointers are used (`prev`, `curr`, `next`).

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
    public ListNode reverseList(ListNode head) {
        ListNode prev = null, curr = head;

        while(curr != null){
            ListNode next = curr.next;

            curr.next = prev;
            prev = curr;
            curr = next;
        }

        return prev;
    }
}   
```

---