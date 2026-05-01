# <u>141. Linked List Cycle</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/linked-list-cycle/

---

## 🧠 Intuition:
* 🔹 The problem is to detect whether a linked list contains a cycle

* 🔹 A naive approach would be to store visited nodes using a hash set, but that uses extra space

* 🔹 Instead, use **Floyd’s Cycle Detection Algorithm (Tortoise and Hare)** for an optimal solution

* 🔹 Initialize two pointers:
    - `slow` → moves one step at a time
    - `fast` → moves two steps at a time

* 🔹 Traverse the list while `fast` and `fast.next` are not null

* 🔹 If there is **no cycle**, `fast` will eventually reach the end (`null`)

* 🔹 If there **is a cycle**, `fast` will eventually meet `slow` inside the loop

* 🔹 Why this works:
    - In a cycle, the fast pointer gains one step over the slow pointer each move
    - This guarantees they will meet at some point inside the cycle

* 🔹 As soon as `slow == fast`, return `true` (cycle detected)

* 🔹 If the loop ends without meeting, return `false` (no cycle)

* 🔹 This approach avoids modifying the list and uses only pointer traversal
---

## ⏱ Time Complexity

**O(n)**

* Where : 
    - n = number of nodes.

* In worst case, both pointers traverse the list once

---

## 📦 Space Complexity

**O(1)**
  
* Only two pointers are used (`slow`, `fast`).

---

## 💻 Java Code

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        ListNode slow = head, fast = head;

        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next; 

            if(slow == fast){
                return true;
            }  
        }
        return false; 
    }
}
```

---