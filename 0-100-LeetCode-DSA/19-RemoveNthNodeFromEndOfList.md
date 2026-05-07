# <u>19. Remove Nth Node From End of List</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/remove-nth-node-from-end-of-list/

---

## 🧠 Intuition:
* 🔹 The goal is to remove the **nth node from the end** of the linked list

* 🔹 First, calculate the **total length** of the linked list

* 🔹 If the list length is `len`, then the node to remove from the beginning is:
    - `node = len - n + 1`

* 🔹 Use a **dummy node** before the head to simplify edge cases
    - Especially useful when deleting the first node

* 🔹 Traverse again using two pointers:
    - `prev` → node before the target node
    - `curr` → current node

* 🔹 Move until reaching the target position

* 🔹 Remove the node by changing links:
    - `prev.next = prev.next.next`

* 🔹 This skips the target node and keeps the list connected

* 🔹 Finally, return `dummy.next` as the updated head

---

## ⏱ Time Complexity

**O(n)**

* First traversal to calculate length → **O(n)**
* Second traversal to reach deletion node → **O(n)**
---

## 📦 Space Complexity

**O(1)**

* Only a few pointers are used

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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;

        int len = 0;
        ListNode l = head;

        while(l != null){
            len = len + 1;
            l = l.next;
        }

        int node = len - n + 1;
        ListNode prev = dummy, curr = head;

        int i = 0;

        while(i < (node - 1)){
            curr = curr.next;
            prev = prev.next;
            i++;
        }

        prev.next = prev.next.next;
        return dummy.next;
    }
}
```

---