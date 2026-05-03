# <u>21. Merge Two Sorted Lists</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/merge-two-sorted-lists/

---

## 🧠 Intuition:
* 🔹 We are given two **sorted linked lists**, and we need to merge them into one sorted list

* 🔹 Use a **dummy node** to simplify handling of the head of the new list

* 🔹 Maintain a pointer `curr` to build the merged list step by step

* 🔹 Compare the current nodes of both lists:
    - Attach the smaller node to `curr.next`
    - Move the pointer of that list forward
    - Move `curr` forward

* 🔹 Repeat until one of the lists becomes `null`

* 🔹 After the loop, one list may still have remaining nodes
    - Directly attach the remaining part to curr.next (since it’s already sorted)

* 🔹 Finally, return `dummy.next` as the head of the merged list

* 🔹 This approach efficiently merges without creating new nodes (just re-links existing ones)

---

## ⏱ Time Complexity

**O(n + m)**

* Where:
    - `n` and `m` = length of the two lists

* Each node from both lists is visited exactly once

---

## 📦 Space Complexity

**O(1)**

* No extra space used except pointers

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
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode dummy = new ListNode(0);
        ListNode curr = dummy;

        while(list1 != null && list2 != null){
            if(list1.val <= list2.val){
                curr.next = list1;
                list1 = list1.next;
                curr = curr.next;
            } else{
                curr.next = list2;
                list2 = list2.next;
                curr = curr.next;
            }
        }

        if(list1 == null){
            curr.next = list2;
        }
        if(list2 == null){
            curr.next = list1;
        }
        return dummy.next;
    }
}
```

---