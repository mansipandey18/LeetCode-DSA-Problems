# <u>63. Unique Paths II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/unique-paths-ii/

---

## 🧠 Intuition:
* 🔹 Use **Dynamic Programming (DP)** where `dp[row][col]` represents the **number of unique paths** to reach cell `(row, col)` from the top-left corner.

* 🔹 If a cell contains an obstacle (1), it cannot be reached, so its DP value remains `0`.

* 🔹 Initialize the **first column**:
    - Keep assigning `1` until an obstacle is encountered, because there is only one way to move downward.

* 🔹 Initialize the **first row**:
    - Keep assigning `1` until an obstacle is encountered, because there is only one way to move right.

* 🔹 For every remaining cell:
    - If it is **not an obstacle**, the number of ways to reach it is the sum of:
        * Paths from the **top** `(dp[row - 1][col])`
        * Paths from the **left** `(dp[row][col - 1])`
    - Update:
        * `dp[row][col] = dp[row - 1][col] + dp[row][col - 1]`

* 🔹 Continue filling the DP table until the bottom-right cell.

* 🔹 The value at `dp[numRows - 1][numCols - 1]` gives the total number of unique paths while avoiding obstacles.

---

## ⏱ Time Complexity

**O(m * n)**

* Every cell in the grid is processed exactly once.

---

## 📦 Space Complexity

**O(m * n)**

* A DP table of size `m × n` is used to store the number of unique paths to each cell.

---

## 💻 Java Code

```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int numRows = obstacleGrid.length, numCols = obstacleGrid[0].length, dp[][] = new int[numRows][numCols];
      
        for (int row = 0; row < numRows && obstacleGrid[row][0] == 0; ++row) {
            dp[row][0] = 1;
        }
      
        for (int col = 0; col < numCols && obstacleGrid[0][col] == 0; ++col) {
            dp[0][col] = 1;
        }

        for (int row = 1; row < numRows; ++row) {
            for (int col = 1; col < numCols; ++col) {
                if (obstacleGrid[row][col] == 0) {
                    dp[row][col] = dp[row - 1][col] + dp[row][col - 1];
                }
            }
        }
      
        return dp[numRows - 1][numCols - 1];
   
    }
}
```

---