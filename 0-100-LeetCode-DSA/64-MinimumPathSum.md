# <u>64. Minimum Path Sum</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/minimum-path-sum/

---

## 🧠 Intuition:
* 🔹 Use **Dynamic Programming (DP)** where `dp[i][j]` represents the minimum path sum to reach cell `(i, j)` from the top-left corner.

* 🔹 Initialize the starting cell:
    - `dp[0][0] = grid[0][0]`

* 🔹 Fill the first column since it can only be reached from the cell above.

* 🔹 Fill the first row since it can only be reached from the cell on the left.

* 🔹 For every remaining cell:
    - It can be reached either from the top or the left.
    - Choose the path with the smaller sum:
        * `dp[i][j] = min(dp[i-1][j], dp[i][j-1]) + grid[i][j]`

* 🔹 Continue filling the DP table until the bottom-right cell is reached.

* 🔹 The value at `dp[m-1][n-1]` is the **minimum path sum** from the top-left to the bottom-right.

---

## ⏱ Time Complexity

**O(m * n)**

* Every cell in the grid is processed exactly once.

---

## 📦 Space Complexity

**O(m * n)**

* A DP table of size `m × n` is used to store the minimum path sum for each cell.

---

## 💻 Java Code

```java
class Solution {
    public int minPathSum(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        int[][] dp = new int[m][n];

        dp[0][0] = grid[0][0];

        for (int i = 1; i < m; ++i) {
            dp[i][0] = dp[i - 1][0] + grid[i][0];
        }

        for (int j = 1; j < n; ++j) {
            dp[0][j] = dp[0][j - 1] + grid[0][j];
        }

        for (int i = 1; i < m; ++i) {
            for (int j = 1; j < n; ++j) {
                dp[i][j] = Math.min(dp[i - 1][j], dp[i][j - 1]) + grid[i][j];
            }
        }

        return dp[m - 1][n - 1];
    }
}
```

---