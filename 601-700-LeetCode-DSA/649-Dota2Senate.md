# <u>649. Dota2 Senate</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/dota2-senate/

---

## 🧠 Intuition:
* 🔹 Each senator can ban one senator of the opposite party, and the process continues in rounds until only one party remains

* 🔹 Since senators act in the order they appear, we need to preserve their turn sequence → **Queue** is the best data structure

* 🔹 Use two separate queues:
    - one for **Radiant (R)** senators
    - one for **Dire (D)** senators

* 🔹 Store the indices of senators instead of characters because the smaller index gets the earlier turn

* 🔹 Traverse the string once and push each senator’s index into the corresponding queue

* 🔹 In each round:
    - Remove the front senator from both queues
    - Compare their indices

* 🔹 The senator with the smaller index gets to act first and bans the opponent senator

* 🔹 The winning senator survives and will participate again in the next round, so push them back with index `currentIndex + n`
    - `(n = senate.length())`, which simulates the circular order of rounds

* 🔹 The banned senator is simply removed and does not return

* 🔹 Continue until one queue becomes empty

* 🔹 If Radiant queue is non-empty → `"Radiant"` wins

* 🔹 Otherwise → `"Dire"` wins

* 🔹 This efficiently simulates the entire banning process while maintaining correct turn order.

---

## ⏱ Time Complexity

**O(n)**

* Where :
    - `n = length of senate string` 

* Initial traversal of senate string → **O(n)**
Each senator is processed and re-added at most once per survival round, overall still linear
    
---

## 📦 Space Complexity

**O(n)**

* Two queues store senator indices → at most **O(n)**

---

## 💻 Java Code

```java
class Solution {
    public String predictPartyVictory(String senate) {
        int senateLength = senate.length();
      
        Deque<Integer> radiantQueue = new ArrayDeque<>();
        Deque<Integer> direQueue = new ArrayDeque<>();
      
        for (int i = 0; i < senateLength; ++i) {
            if (senate.charAt(i) == 'R') {
                radiantQueue.offer(i);
            } else {
                direQueue.offer(i);
            }
        }
      
        while (!radiantQueue.isEmpty() && !direQueue.isEmpty()) {
            int radiantIndex = radiantQueue.poll();
            int direIndex = direQueue.poll();
          
            if (radiantIndex < direIndex) {
                radiantQueue.offer(radiantIndex + senateLength);
            } else {
                direQueue.offer(direIndex + senateLength);
            }
        }
      
        return radiantQueue.isEmpty() ? "Dire" : "Radiant";
    
    }
}
```

---