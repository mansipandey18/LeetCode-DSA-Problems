# <u>3499. Maximize Active Section with Trade I</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximize-active-section-with-trade-i/

---

## 🧠 Intuition:
* 🔹 Traverse the string and divide it into **continuous segments** of the same character (`0`s or `1`s).

* 🔹 Count the total number of active sections (`1`s) by adding the length of every `1` segment.

* 🔹 While processing `0` segments, keep track of:
    - The length of the previous `0` segment.
    - The **maximum sum of two adjacent `0` segments** separated by a single 1 segment.

* 🔹 Whenever a new `0` segment is found, compute the sum of its length and the previous `0` segment's length.

* 🔹 Update the maximum combined `0` length if this sum is larger.

* 🔹 After scanning the entire string, the best trade is to merge the two largest adjacent `0` segments.

* 🔹 Add this maximum gain to the original count of `1`s to obtain the maximum possible active sections after one trade.

---

## ⏱ Time Complexity

**O(n)**

* The string is traversed once, and each character is processed exactly once.
    
---

## 📦 Space Complexity

**O(1)**

* Only a few integer variables are used to track counts and segment lengths.

---

## 💻 Java Code

```java
class Solution {
    public int maxActiveSectionsAfterTrade(String s) {
        int n = s.length();
        int totalOnes = 0;  
        int currentIndex = 0;
        int previousZeroSegmentLength = Integer.MIN_VALUE;  // Length of previous segment of '0's
        int maxZeroSegmentSum = 0;  // Maximum sum of two adjacent zero segments

        while (currentIndex < n) {
            int segmentEnd = currentIndex + 1;
            while (segmentEnd < n && s.charAt(segmentEnd) == s.charAt(currentIndex)) {
                segmentEnd++;
            }
          
            int currentSegmentLength = segmentEnd - currentIndex;
          
            if (s.charAt(currentIndex) == '1') {
                totalOnes += currentSegmentLength;
            } else {
                maxZeroSegmentSum = Math.max(maxZeroSegmentSum, 
                                            previousZeroSegmentLength + currentSegmentLength);

                previousZeroSegmentLength = currentSegmentLength;
            }
          
            currentIndex = segmentEnd;
        }

        totalOnes += maxZeroSegmentSum;
        
        return totalOnes;
    
    }
}
```

---