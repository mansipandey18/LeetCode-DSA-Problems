# <u>92. Reverse Linked List II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/reverse-linked-list-ii/

---

## 🧠 Intuition:
* 🔹 The goal is to **reverse a portion of a linked list** from position `left` to `right` (1-based indexing)

* 🔹 Use a **dummy node** to simplify edge cases (especially when `left = 1`)

* 🔹 Traverse the list to reach the node just **before the `left` position**
    - Let `p` → node before the sublist
    - Let `c` → first node of the sublist (position `left`)

* 🔹 Now reverse the sublist from `left` to `right` using standard linked list reversal
    - Maintain `prev`, `curr`, and `next` pointers
    - Reverse exactly `(right - left + 1)` nodes

* 🔹 After reversal:
    - `prev` → new head of reversed sublist
    - `curr` → node right after the reversed sublist
    - `c` → becomes the tail of the reversed sublist

* 🔹 Reconnect the list:
    - `p.next = prev` → connect first part with reversed sublist
    - `c.next = curr` → connect reversed sublist with remaining list

* 🔹 Return `dummy.next` as the new head

* 🔹 This approach reverses only the required portion without affecting the rest of the list

---

## ⏱ Time Complexity

**O(n)**

* Traverse to position left → **O(n)**
* Reverse sublist → **O(n)** (in worst case)

---

## 📦 Space Complexity

**O(1)**

* Only pointers are used

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
    public ListNode reverseBetween(ListNode head, int left, int right) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;

        int count = 0;

        ListNode p = dummy, c = head;

        while(count < left - 1){
            p = c;
            c = c.next;
            count++;
        }

        ListNode prev = null, curr =  c;

        count = 0;
        while(count < (right - left + 1)){
            count++;

            ListNode next = curr.next;

            curr.next = prev;
            prev = curr;
            curr = next;
        }

        p.next = prev;
        c.next = curr;

        return dummy.next;
    }
}
```

---