# <u>2130. Maximum Twin Sum of a Linked List</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-twin-sum-of-a-linked-list/

---

## 🧠 Intuition:
* 🔹 The problem asks to find the **maximum twin sum** in a linked list, where twin nodes are equidistant from the start and end (i.e., `i-th` node from start + `i-th` node from end)

* 🔹 Since linked lists don’t support reverse indexing, we need an efficient way to access nodes from both ends

* 🔹 Use the **slow and fast pointer technique** to find the middle of the linked list
    - `slow` moves 1 step, `fast` moves 2 steps → when fast reaches end, slow is at middle

* 🔹 Split the list into two halves at the middle

* 🔹 Reverse the second half of the linked list using an in-place reversal function

* 🔹 Now we have:
    - First half → forward direction
    - Second half → reversed direction (acts like backward traversal)

* 🔹 Use two pointers:
    - `p1` → start of first half
    - `p2` → start of reversed second half

* 🔹 Traverse both halves simultaneously:
    - For each pair, compute `p1.val + p2.val`
    - Track the maximum sum encountered

* 🔹 This effectively pairs first node with last, second with second-last, and so on

* 🔹 Return the maximum twin sum found

* 🔹 This avoids extra space like arrays and works efficiently in-place

---

## ⏱ Time Complexity

**O(n)**

* Finding middle → **O(n)**
* Reversing second half → **O(n)**
* Traversing both halves → **O(n)**
  
---

## 📦 Space Complexity

**O(1)**

* No extra data structures used (only pointers)

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
    public int pairSum(ListNode head) {
        ListNode slow = head, fast = head;

        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
        }

        ListNode p1 = head, p2 = reverseLL(slow);
        int max = Integer.MIN_VALUE;

        while(p1 != null && p2 != null){
            int candidate = p1.val + p2.val;
            max = Math.max(max, candidate);

            p1 = p1.next;
            p2 = p2.next;
        }
        return max;
    }

    private ListNode reverseLL(ListNode node){
        ListNode prev = null;

        while(node != null){
            ListNode next = node.next;
            node.next = prev;
            prev = node;
            node = next; 
        }
        return prev;
    }
}
```

---