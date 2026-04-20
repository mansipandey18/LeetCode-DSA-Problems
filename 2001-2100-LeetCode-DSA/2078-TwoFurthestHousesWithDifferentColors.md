# <u>2078. Two Furthest Houses With Different Colors</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/two-furthest-houses-with-different-colors/

---

## 🧠 Intuition:
* 🔹 Goal is to find **maximum distance between two houses having different colors**

* 🔹 We try **all possible pairs (i, j)** where `j > i`

* 🔹 For each pair, check if `colors[i] != colors[j]`

* 🔹 If colors are different, calculate distance = `j - i`

* 🔹 Keep updating the **maximum distance** found so far

* 🔹 This is a **brute-force approach** that checks every valid pair to ensure we don’t miss the farthest one

---

## ⏱ Time Complexity

**O(n^2)**

* Two nested loops over array

---

## 📦 Space Complexity

**O(1)**

* No extra space used

---

## 💻 Java Code

```java
class Solution {
    public int maxDistance(int[] colors) {
        int maxDist = 0;
        int arrayLength = colors.length;
    
        for (int leftIndex = 0; leftIndex < arrayLength; ++leftIndex) {
            for (int rightIndex = leftIndex + 1; rightIndex < arrayLength; ++rightIndex) {
                if (colors[leftIndex] != colors[rightIndex]) {
                    int currentDistance = Math.abs(leftIndex - rightIndex);
                    maxDist = Math.max(maxDist, currentDistance);
                }
            }
        }
      
        return maxDist;
    }
}
```

---