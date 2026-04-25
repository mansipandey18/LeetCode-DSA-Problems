# <u>452. Minimum Number of Arrows to Burst Balloons</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/

---

## 🧠 Intuition:
* 🔹 Each balloon is represented as an interval `[start, end]`, and one arrow can burst all balloons whose intervals include the arrow’s position

* 🔹 To minimize the number of arrows, we should place each arrow so that it covers the maximum possible overlapping balloons

* 🔹 Sort all balloons based on their **ending coordinate (`end`)** in increasing order

* 🔹 This greedy choice ensures we always shoot the arrow at the earliest possible end position, maximizing future overlap opportunities

* 🔹 Start with no arrows and keep track of the **last arrow position**

* 🔹 Traverse each balloon:
    - If the current balloon’s start position is greater than the last arrow position, it means this balloon cannot be burst by the previous arrow
    - So, fire a new arrow and place it at the current balloon’s end position

* 🔹 If the current balloon overlaps with the previous arrow position, no new arrow is needed

* 🔹 Continue this process until all balloons are covered

* 🔹 The final arrow count gives the minimum number of arrows required

---

## ⏱ Time Complexity

**O(n log n)**

* Sorting all intervals → `O(n log n)`
* Single traversal of all balloons → `O(n)`
    
---

## 📦 Space Complexity

**O(1)**

* Only a few extra variables are used (ignoring sorting space).

---

## 💻 Java Code

```java
class Solution {
    public int findMinArrowShots(int[][] points) {
        Arrays.sort(points, Comparator.comparingInt(point -> point[1]));
      
        int arrowCount = 0;
      
        long lastArrowPosition = -(1L << 60);
      
        for (int[] balloon : points) {
            int startPosition = balloon[0];
            int endPosition = balloon[1];
          
            if (startPosition > lastArrowPosition) {
                arrowCount++;
                lastArrowPosition = endPosition;
            }
        }
      
        return arrowCount;
    }
}   
```

---