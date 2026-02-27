# 2. Add Two Numbers

## 🔗 Problem Link
https://leetcode.com/problems/add-two-numbers/

## 🧠 Intuition:
* Create a **dummy node** to build result list.
* Use a pointer `curr` to construct new list.
* Maintain a variable `carry`.
* Traverse both lists:
   - Add values from `l1` and `l2` (if present).
   - Add previous carry.
   - Create new node with `sum % 10`.
   - Update carry = `sum / 10`.
* Move forward.
* Return `dummy.next`.

## ⏱ Time Complexity

O(max(n, m))

Where:
- n = length of l1  
- m = length of l2  

---

## 📦 Space Complexity

O(max(n, m))  
(New linked list is created)

## 💻 Java Code

```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode curr = dummy;
        int carry = 0;

        while (l1 != null || l2 != null || carry > 0) {

            if (l1 != null) {
                carry += l1.val;
                l1 = l1.next;
            }

            if (l2 != null) {
                carry += l2.val;
                l2 = l2.next;
            }

            curr.next = new ListNode(carry % 10);
            carry /= 10;
            curr = curr.next;
        }

        return dummy.next;
    }
}
```

---