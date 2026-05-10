# <u>86. Partition List</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/partition-list/

---

## 🧠 Intuition:
* 🔹 The goal is to rearrange the linked list such that:
    - All nodes with values `< x` come before nodes with values `>= x`
    - Relative order within each group should remain the same

* 🔹 Instead of modifying node values, create two separate linked lists:
    - `less` list → stores nodes with value `< x`
    - `greater` list → stores nodes with value `>= x`

* 🔹 Use dummy nodes (`lessHead` and `greaterHead`) to simplify list construction

* 🔹 Traverse the original list node by node:
    - If `head.val < x`, attach the node to the `less` list
    - Otherwise, attach it to the `greater` list

* 🔹 Move the corresponding tail pointer after adding each node

* 🔹 After traversal:
    - Connect the end of the `less` list to the beginning of the `greater` list

* 🔹 Set `greaterTail.next = null` to avoid accidental cycles

* 🔹 Return `lessHead.next` as the new head of the partitioned list
---

## ⏱ Time Complexity

**O(n)**

* Where :
    - `n` = number of nodes in the linked list

* Each node is visited exactly once during traversal
    
---

## 📦 Space Complexity

**O(1)**

* No extra data structures proportional to n are used
* Only a few pointer variables are maintained

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
    public ListNode partition(ListNode head, int x) {
        ListNode lessHead = new ListNode(0), greaterHead = new ListNode(0), lessTail = lessHead, greaterTail = greaterHead; 

        while (head != null) {
            if (head.val < x) {
                
                lessTail.next = head;
                lessTail = head;
            } else {
                
                greaterTail.next = head;
                greaterTail = head;
            }
            head = head.next; 
        }

        
        lessTail.next = greaterHead.next;
        greaterTail.next = null;
       
        return lessHead.next;
    }
}
```

---