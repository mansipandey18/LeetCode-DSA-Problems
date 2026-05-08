# <u>82. Remove Duplicates from Sorted List II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/

---

## 🧠 Intuition:
* 🔹 The linked list is sorted, so duplicate values always appear consecutively

* 🔹 The goal is to remove **all nodes having duplicate values**, not just extra copies

* 🔹 A **dummy node** is used before the head to handle edge cases easily
    - Especially when duplicates appear at the beginning of the list

* 🔹 Two pointers are maintained:
    - `precedingNode` → last confirmed unique node
    - `currentNode` → used to scan the list

* 🔹 For each node:
    - Move `currentNode` forward while the next node has the same value
    - This helps detect a duplicate block

* 🔹 After traversal of duplicates:
    - If `precedingNode.next == currentNode`
        * No duplicates were found, so move `precedingNode` forward
    - Otherwise
        * Duplicates exist, so skip the entire duplicate sequence using: `precedingNode.next = currentNode.next`

* 🔹 Continue until the whole list is processed

* 🔹 Finally, return `dummyNode.next` as the updated list head

---

## ⏱ Time Complexity

**O(n)**

* Where :
    - `n` = number of nodes in the linked list

* Each node is visited at most once during traversal
    
---

## 📦 Space Complexity

**O(1)**

* Only a few pointers are used, no extra data structures

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
    public ListNode deleteDuplicates(ListNode head) {
        ListNode dummyNode = new ListNode(0, head), precedingNode = dummyNode, currentNode = head;

        while (currentNode != null) {
            while (currentNode.next != null && currentNode.next.val == currentNode.val) {
                currentNode = currentNode.next;
            }
          
            if (precedingNode.next == currentNode) {
                precedingNode = currentNode;
            } else {
                precedingNode.next = currentNode.next;
            }
            currentNode = currentNode.next;
        }
      
        return dummyNode.next;
    }
}
```

---