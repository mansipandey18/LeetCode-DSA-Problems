# <u>23. Merge k Sorted Lists</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/merge-k-sorted-lists/

---

## 🧠 Intuition:
* 🔹 The idea is to merge the `k` sorted linked lists using a **divide and conquer approach**, similar to merge sort.

* 🔹 First, create a helper function `mergeTwoLists()` that merges two sorted linked lists by comparing their nodes one by one.

* 🔹 In each round, take the lists in pairs and merge them into a single sorted list.

* 🔹 If there is an odd number of lists, carry the last unpaired list directly to the next round.

* 🔹 After one round, the number of lists reduces approximately by half.

* 🔹 Repeat this pairwise merging process until only one final sorted linked list remains.

* 🔹 This approach avoids repeatedly merging one list with all others and provides a more efficient solution.

---

## ⏱ Time Complexity

**O(n log k)**

* Each node is processed in every merging level, and there are `log k` levels of merging, where `N` is the total number of nodes in all lists.

---

## 📦 Space Complexity

**O(log k)**

* For the arrays used across merging rounds; excluding the output linked list.

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

    public ListNode mergeKLists(ListNode[] lists) {
        if(lists.length == 0){
            return null;
        }

        while(lists.length > 1){
            int count = lists.length % 2 == 0 ? lists.length / 2 : (lists.length + 1) / 2;

            ListNode nextRound[] = new ListNode[count];

            for(int p = 0, k = 0; p < lists.length; p = p + 2, k++){
                if(p + 1 < lists.length){
                    nextRound[k] = mergeTwoLists(lists[p], lists[p + 1]);
                } else{
                    nextRound[k] = lists[p];
                }
            }
            lists = nextRound;
        }
        return lists[0];
    }
}
```

---