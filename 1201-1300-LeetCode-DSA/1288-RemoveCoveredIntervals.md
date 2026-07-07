# <u>1288. Remove Covered Intervals</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/remove-covered-intervals/

---

## 🧠 Intuition:
* 🔹 Sort the intervals by their **starting point in ascending order**.

* 🔹 If two intervals have the same starting point, sort them by their **ending point in descending order** so that the larger interval comes first.

* 🔹 This sorting ensures that if an interval is covered by another, it will appear after the interval that covers it.

* 🔹 Traverse the sorted intervals while keeping track of the **maximum ending point** (`maxEnd`) seen so far.

* 🔹 If the current interval's end is **greater than** `maxEnd`, it is not covered, so count it and update maxEnd.

* 🔹 If the current interval's end is **less than or equal to** `maxEnd`, it is completely covered by a previous interval, so skip it.

* 🔹 The final count represents the number of intervals remaining after removing all covered intervals.

---

## ⏱ Time Complexity

**O(n log n)**

* Due to sorting the intervals, followed by a single linear scan.
    
---

## 📦 Space Complexity

**O(1)**

* excluding the sorting space used by Java's sorting algorithm.

---

## 💻 Java Code

```java
class Solution {
    public int removeCoveredIntervals(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> {
            int val = Integer.compare(a[0], b[0]);

            return val == 0 ? Integer.compare(b[1], a[1]) : val;
        });

        int count = 1;
        int maxEnd = intervals[0][1];

        for(int i = 1; i < intervals.length; i++){
            if(intervals[i][1] > maxEnd){
                count++;
                maxEnd = intervals[i][1];
            }
        }

        return count;
    }
}


```

---