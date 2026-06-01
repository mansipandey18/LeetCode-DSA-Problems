# <u>62. Unique Paths</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/unique-paths/

---

## 🧠 Intuition:
* 🔹 A robot can only move **right** or **down**, so the number of ways to reach a cell equals:
    - Paths from the **top cell +**
    - Paths from the **left cell**.

* 🔹 Use **Dynamic Programming** to store the number of ways to reach each position.

* 🔹 Since the first row and first column can only be reached in one way, initialize all values in the DP array to `1`.

* 🔹 Instead of using a 2D DP table, optimize space by using a **1D array** `pathCounts`.

* 🔹 `pathCounts[col]` represents the number of ways to reach the current cell in that column.

* 🔹 For each cell:
    - `pathCounts[col] += pathCounts[col - 1]`
    - Current paths = paths from above (`pathCounts[col]`) + paths from the left (`pathCounts[col - 1]`).

* 🔹 Continue updating row by row until reaching the bottom-right corner.

* 🔹 The last element of the array contains the total number of unique paths.

---

## ⏱ Time Complexity

**O(m * n)**

* every cell in the grid is processed once.

---

## 📦 Space Complexity

**O(n)**

* only a 1D DP array of size `n` is used.

---

## 💻 Java Code

```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[] pathCounts = new int[n];
      
        Arrays.fill(pathCounts, 1);

        for (int row = 1; row < m; ++row) {
            for (int col = 1; col < n; ++col) {
                pathCounts[col] += pathCounts[col - 1];
            }
        }
      
        return pathCounts[n - 1];
    }
}
```

---