# <u>221. Maximal Square</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/count-complete-tree-nodes/

---

## 🧠 Intuition:
* 🔹 Use **Dynamic Programming** to find the largest square ending at each cell.

* 🔹 Let `dp[i][j]` represent the **side length of the largest square** whose bottom-right corner is at `matrix[i-1][j-1]`.

* 🔹 If the current cell contains `'0'`, no square can end here, so its DP value remains `0`.

* 🔹 If the current cell contains `'1'`, a larger square can be formed only if the top, left, and top-left neighboring cells also support a square.

* 🔹 The side length of the current square is:
    - `1 + min(top, left, top-left)`

* 🔹 This works because the smallest neighboring square limits how large the current square can become.

* 🔹 Keep updating the maximum side length while filling the DP table.

* 🔹 At the end, return the area of the largest square by calculating:
    - `maxSideLength × maxSideLength`.

---

## ⏱ Time Complexity

**O(m * n)**

* Every cell is processed exactly once.

---

## 📦 Space Complexity

**O(m * n)**

* A DP table of size `(rows + 1) × (cols + 1)` is used to store the largest square side ending at each cell.

---

## 💻 Java Code

```java
class Solution {
    public int maximalSquare(char[][] matrix) {
        int rows = matrix.length;
        int cols = matrix[0].length;
      
        int[][] dp = new int[rows + 1][cols + 1];
      
        int maxSideLength = 0;
      
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (matrix[i][j] == '1') {
                    dp[i + 1][j + 1] = Math.min(
                        Math.min(dp[i][j + 1], dp[i + 1][j]),  // min of top and left
                        dp[i][j]                                 
                    ) + 1;
                  
                    maxSideLength = Math.max(maxSideLength, dp[i + 1][j + 1]);
                }
            }
        }
      
        return maxSideLength * maxSideLength;    
    }
}
```

---