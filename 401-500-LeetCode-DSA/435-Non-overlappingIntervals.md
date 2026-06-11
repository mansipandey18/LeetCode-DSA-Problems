# <u>435. Non-overlapping Intervals</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/non-overlapping-intervals/

---

## 🧠 Intuition:
* 🔹 The goal is to keep the **maximum number of non-overlapping intervals** and remove the rest.

* 🔹 First, find the minimum and maximum interval end points to create a compact index range.

* 🔹 Use a `rightEnds` array where `rightEnds[r]` stores the **largest starting point** among intervals ending at `r`.

* 🔹 Shift interval coordinates to handle negative values easily.

* 🔹 For each interval, update the corresponding ending position with the maximum start value.

* 🔹 Traverse the ending points from left to right.

* 🔹 If the stored start point is greater than or equal to the end point of the last selected interval, we can safely include this interval without overlap.

* 🔹 Count how many non-overlapping intervals can be selected.

* 🔹 The answer is:
    - **Total intervals − Maximum non-overlapping intervals selected**

---

## ⏱ Time Complexity

**O(n + R)**

* Finding min/max endpoints: `O(n)`
* Filling the rightEnds array: `O(n)`
* Traversing the endpoint range: `O(R)` 
* Where:
    - `R = maxEnd - minEnd + 2`
    
---

## 📦 Space Complexity

**O(R)**

* `rightEnds` array of size `R`

* Where:
    - `R = maxEnd - minEnd + 2`(the range of interval and values)

---

## 💻 Java Code

```java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        int max = intervals[0][1];
        int min = max;
        for (int i = 1; i < intervals.length; i++) {
            max = Math.max(max, intervals[i][1]);
            min = Math.min(min, intervals[i][1]);
        }
        int shift = 1 - min;
        int maxIntervalRange = 2 + max - min;
        int[] rightEnds = new int[maxIntervalRange];

        for (int[] interval : intervals) {
            int left = interval[0] + shift;
            int right = interval[1] + shift;
            if (left > rightEnds[right]) {
                rightEnds[right] = left;
            }
        }
        int start = 1;
        int count = 1;
        for (int i = 2; i < maxIntervalRange; i++) {
            if (start <= rightEnds[i]) {
                count++;
                start = i;
            }
        }
        return intervals.length - count;
    }
}   
```

---