# <u>149. Max Points on a Line</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/max-points-on-a-line/

---

## 🧠 Intuition:
* 🔹 Every pair of points uniquely defines a line, so treat each pair as a candidate line.

* 🔹 For every pair of points `(i, j)`, assume they are already on the same line, so the initial count is `2`.

* 🔹 Check every remaining point `k` to see if it lies on this line.

* 🔹 To avoid floating-point precision issues, use the **cross-product** instead of comparing slopes.

* 🔹 If `(y2 - y1) × (x3 - x1) == (y3 - y1) × (x2 - x1)`, then the three points are collinear.

* 🔹 Increase the count whenever another point lies on the same line.

* 🔹 Keep track of the maximum number of points found on any line during the process.

* 🔹 After checking all possible pairs, return the maximum count.

---

## ⏱ Time Complexity

**O(n³)**

* Three nested loops are used to check every pair of points and every remaining point.

---

## 📦 Space Complexity

**O(1)**
  
* Only a few variables are used; no extra data structures are required.

---

## 💻 Java Code

```java
class Solution {
    public int maxPoints(int[][] points) {
        int n = points.length;
        int maxPointsOnLine = 1; // At least one point exists
      
        for (int i = 0; i < n; ++i) {
            int x1 = points[i][0];
            int y1 = points[i][1];
          
            for (int j = i + 1; j < n; ++j) {
                int x2 = points[j][0];
                int y2 = points[j][1];
                int pointsOnCurrentLine = 2; 
              
                for (int k = j + 1; k < n; ++k) {
                    int x3 = points[k][0];
                    int y3 = points[k][1];
                  
                    int crossProduct1 = (y2 - y1) * (x3 - x1);
                    int crossProduct2 = (y3 - y1) * (x2 - x1);
                  
                    if (crossProduct1 == crossProduct2) {
                        ++pointsOnCurrentLine;
                    }
                }
              
                maxPointsOnLine = Math.max(maxPointsOnLine, pointsOnCurrentLine);
            }
        }
      
        return maxPointsOnLine;
    }
}
```

---