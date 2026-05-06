# <u>25. Reverse Nodes in k-Group</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/reverse-nodes-in-k-group/

---

## 🧠 Intuition:
* 🔹 The goal is to **reverse nodes of a linked list in groups** of size `k`

* 🔹 First, compute the **length of the list** to know how many full groups can be formed
    - Only complete groups of size `k` should be reversed

* 🔹 Calculate `times = len / k` → number of groups to reverse

* 🔹 Use a **dummy node** to simplify connections, especially for the head

* 🔹 Maintain pointers:
    - `curr` → current node being processed
    - `p1` → tail of the already processed part

* 🔹 For each group:
    - Reverse exactly `k` nodes using standard linked list reversal
        * Use `prev`, `curr`, `next` pointers

    - After reversal:
        * `prev` → new head of the group
        * `p2` (original start of group) → becomes tail

* 🔹 Reconnect:
    - `p1.next = prev` → connect previous part with reversed group
    - `p2.next = curr` → connect reversed group with next part

* 🔹 Move `p1` to `p2` (new tail) and continue

* 🔹 Remaining nodes (less than `k`) are left unchanged

* 🔹 Finally, return `dummy.next`

---

## ⏱ Time Complexity

**O(n)**

* Traverse to calculate length → **O(n)**
* Reverse nodes → **O(n)**

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
    public ListNode reverseKGroup(ListNode head, int k) {
        int len = 0; 
        ListNode curr = head;

        while(curr != null){
            len++;
            curr = curr.next;
        }

        int times = len / k;

        curr = head;

        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode p1 = dummy;

        for(int i = 0; i < times; i++){
            int count = 0;
            ListNode prev = null, p2 = curr;

            while(count < k && curr != null){
                count++;

                ListNode next = curr.next;

                curr.next = prev;
                prev = curr;
                curr = next;

            }

            p1.next = prev;
            p2.next = curr;

            p1 = p2;
        }

        return dummy.next;
    }
}
```

---