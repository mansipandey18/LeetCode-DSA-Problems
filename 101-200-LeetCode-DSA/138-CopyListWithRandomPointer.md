# <u>138. Copy List with Random Pointer</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/copy-list-with-random-pointer/

---

## 🧠 Intuition:
* 🔹 Every child must receive at least one candy.

* 🔹 A child with a higher rating than an adjacent child must get more candies.

* 🔹 While moving through the ratings array, the ratings create three patterns:

    - increasing sequence (uphill)

    - decreasing sequence (downhill)

    - equal ratings (flat).

* 🔹 Instead of using extra arrays, we track the trend of ratings in one pass.

* 🔹 When ratings are increasing:

    - give one more candy than the previous child.

    - keep track of the peak candies given.

* 🔹 When ratings are equal:

    - reset all counters.

    - give exactly one candy.

* 🔹 When ratings are decreasing:

    - candies must decrease step by step.

    - count the length of the decreasing sequence.

* 🔹 If the decreasing sequence becomes longer than the previous increasing peak,

    - we add one extra candy to the peak child to maintain the rule.

* 🔹 By adjusting candies during upward and downward slopes, all constraints are satisfied in a single traversal.

---

## ⏱ Time Complexity

**O(n)**

* Where : 
    - `n` = number of nodes.

---

## 📦 Space Complexity

**O(1)**
  
* No extra space used (excluding output list)

---

## 💻 Java Code

```java
/*
// Definition for a Node.
class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
*/

class Solution {
    public Node copyRandomList(Node head) {
        if (head == null) {
            return null;
        }

        for (Node current = head; current != null; ) {
            Node clone = new Node(current.val); 
            clone.next = current.next; 
            current.next = clone; 
            current = clone.next; 
        }

        for (Node current = head; current != null; current = current.next.next) {
            if (current.random != null) {
                current.next.random = current.random.next;
            }
        }

        Node copyHead = head.next; 
        for (Node current = head; current != null; ) {
            Node clone = current.next; 
            current.next = clone.next;
            clone.next = (clone.next != null) ? clone.next.next : null;
            current = current.next;
        }
      
        return copyHead;
    }
}
```

---