# <u>1732. Find the Highest Altitude</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/find-the-highest-altitude/

---

## 🧠 Intuition:
* 🔹 We are given **altitude changes**, not actual altitudes.

* 🔹 Start from **altitude = 0** (initial point).

* 🔹 Traverse the array and keep adding each value to get **current altitude**.

* 🔹 At every step, update the **maximum altitude reached so far**.

* 🔹 This is like keeping a **running sum (prefix sum)** and tracking the highest value.

* 🔹 Finally, return the maximum altitude encountered during the journey.

---

## ⏱ Time Complexity

**O(n)**

* Single traversal of the array

---

## 📦 Space Complexity

**O(1)**

* Only a few variables are used.

---

## 💻 Java Code

```java
class Solution {
    public int largestAltitude(int[] gain) {
        int maxAltitude = 0, currAltitude = 0;

        for(int altitudeChange : gain){
            currAltitude += altitudeChange;

            maxAltitude = Math.max(maxAltitude, currAltitude);
        }

        return maxAltitude;
    }
}
```

---