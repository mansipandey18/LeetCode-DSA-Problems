# <u>1833. Maximum Ice Cream Bars</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-ice-cream-bars/

---

## 🧠 Intuition:
* 🔹 To buy the maximum number of ice cream bars, always purchase the **cheapest bars first** (Greedy approach).

* 🔹 Sort the `costs` array in increasing order so that lower-cost ice creams are considered before expensive ones.

* 🔹 Traverse the sorted array and keep buying ice creams as long as enough coins are available.

* 🔹 For each ice cream:
    - If the remaining coins are less than its cost, we cannot buy any more ice creams, so return the number purchased so far.
    - Otherwise, subtract its cost from the available coins and continue.

* 🔹 If all ice creams are purchased, return the total number of ice cream bars.

* 🔹 This greedy strategy works because spending coins on cheaper ice creams first leaves the maximum possible budget to buy more bars.

---

## ⏱ Time Complexity

**O(n log n)**

* Sorting the costs array takes `O(n log n)` time
* The single traversal takes `O(n)`

---

## 📦 Space Complexity

**O(log n)**

* Due to the recursion stack used

---

## 💻 Java Code

```java
class Solution {
    public int maxIceCream(int[] costs, int coins) {
        Arrays.sort(costs);
      
        int numberOfIceCreams = costs.length;
      
        for (int i = 0; i < numberOfIceCreams; ++i) {
            if (coins < costs[i]) {
                return i;
            }
          
            coins -= costs[i];
        }
      
        return numberOfIceCreams;
    }
}
```

---