# <u>1594. Maximum Non Negative Product in a Matrix</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-non-negative-product-in-a-matrix/

---

## 🧠 Intuition:
* 🔹 Create a DP array:
    - dp[i][j][0] → minimum product reaching (i,j)
    - dp[i][j][1] → maximum product reaching (i,j)

* 🔹 Start from (0,0):
    - Both min and max = starting value.

* 🔹 First row & first column:
    - Only one direction possible (left or up).

* 🔹 For every other cell:
    - We can come from:
        * top (i-1, j)
        * left (i, j-1)

* 🔹 If current number is positive:
    - Minimum stays minimum.
    - Maximum stays maximum.

* 🔹 If current number is negative:
    - Minimum becomes previous maximum.
    - Maximum becomes previous minimum.
    - (sign flips)

* 🔹 Continue filling DP for all cells.

* 🔹 Final answer:
    - Check maximum product at bottom-right.
    - If negative → return -1.
    - Else return modulo 10^9 + 7


---

## ⏱ Time Complexity

**O(m x n)**

* We traverse each cell once.
* For each cell, constant work is done.
    
---

## 📦 Space Complexity

**O(m x n)**

* DP array size = rows × cols × 2.

---

## 💻 Java Code

```java
class Solution {
    private static final int MOD = (int) 1e9 + 7;
    
    public int maxProductPath(int[][] grid) {
        int rows = grid.length;
        int cols = grid[0].length;
      
        // dp[i][j][0] stores the minimum product to reach cell (i, j)
        // dp[i][j][1] stores the maximum product to reach cell (i, j)
        // We track both min and max because negative numbers can flip the relationship
        long[][][] dp = new long[rows][cols][2];
      
        // Initialize starting cell with its value for both min and max
        dp[0][0][0] = grid[0][0];
        dp[0][0][1] = grid[0][0];
      
        // Initialize first column (can only come from above)
        for (int i = 1; i < rows; i++) {
            dp[i][0][0] = dp[i - 1][0][0] * grid[i][0];
            dp[i][0][1] = dp[i - 1][0][1] * grid[i][0];
        }
      
        // Initialize first row (can only come from left)
        for (int j = 1; j < cols; j++) {
            dp[0][j][0] = dp[0][j - 1][0] * grid[0][j];
            dp[0][j][1] = dp[0][j - 1][1] * grid[0][j];
        }
      
        // Fill the dp table for remaining cells
        for (int i = 1; i < rows; i++) {
            for (int j = 1; j < cols; j++) {
                int currentValue = grid[i][j];
              
                if (currentValue >= 0) {
                    // For positive values:
                    // - Minimum stays minimum after multiplication
                    // - Maximum stays maximum after multiplication
                    dp[i][j][0] = Math.min(dp[i - 1][j][0], dp[i][j - 1][0]) * currentValue;
                    dp[i][j][1] = Math.max(dp[i - 1][j][1], dp[i][j - 1][1]) * currentValue;
                } else {
                    // For negative values:
                    // - Previous maximum becomes new minimum after multiplication
                    // - Previous minimum becomes new maximum after multiplication
                    dp[i][j][0] = Math.max(dp[i - 1][j][1], dp[i][j - 1][1]) * currentValue;
                    dp[i][j][1] = Math.min(dp[i - 1][j][0], dp[i][j - 1][0]) * currentValue;
                }
            }
        }
      
        // Get the maximum product at the destination cell
        long maxProduct = dp[rows - 1][cols - 1][1];
      
        // Return -1 if the maximum product is negative, otherwise return modulo result
        return maxProduct < 0 ? -1 : (int) (maxProduct % MOD);
    
    }
}
```

---