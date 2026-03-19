# <u>3212. Count Submatrices With Equal Frequency of X and Y
</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/count-submatrices-with-equal-frequency-of-x-and-y/

---

## 🧠 Intuition:
* 🔹 Every valid submatrix must start from the top-left corner (0,0).

* 🔹 So each cell (i, j) represents one submatrix ending at that position.

* 🔹 We need to check two conditions for every such submatrix:

    - contains at least one 'X'

    - number of 'X' = number of 'Y'.

* 🔹 Instead of counting characters repeatedly for every submatrix, we use a prefix sum technique.

* 🔹 We maintain a 3D prefix sum array:

    - prefixSum[i][j][0] → count of 'X'

    - prefixSum[i][j][1] → count of 'Y'
from (0,0) to (i-1,j-1).

* 🔹 Using inclusion–exclusion, we efficiently build cumulative counts from previously computed cells.

* 🔹 For each cell:

    - we instantly know total 'X' and 'Y' in the submatrix (0,0) → (i,j).

* 🔹 If:

    - count of 'X' > 0, and

    - count of 'X' equals count of 'Y', then this submatrix is valid.

* 🔹 Increment the result while building the prefix sums (single traversal).

---

## ⏱ Time Complexity

**O(m * n)**

 - We traverse the grid once using nested loops.
 - Each prefix calculation takes O(1) time.

---

## 📦 Space Complexity

**O(m * n)**

* A 3D prefix sum array of size: 
  
   - (rows+1)×(cols+1)×2

---

## 💻 Java Code

```java
class Solution {
    public int numberOfSubmatrices(char[][] grid) {
        int rows = grid.length;
        int cols = grid[0].length;
      
        // Create a 3D prefix sum array
        // prefixSum[i][j][0] stores count of 'X' from (0,0) to (i-1,j-1)
        // prefixSum[i][j][1] stores count of 'Y' from (0,0) to (i-1,j-1)
        int[][][] prefixSum = new int[rows + 1][cols + 1][2];
      
        int result = 0;
      
        // Build prefix sum array and count valid submatrices
        for (int i = 1; i <= rows; i++) {
            for (int j = 1; j <= cols; j++) {
                // Calculate prefix sum for 'X' count using inclusion-exclusion principle
                prefixSum[i][j][0] = prefixSum[i - 1][j][0] 
                                    + prefixSum[i][j - 1][0] 
                                    - prefixSum[i - 1][j - 1][0]
                                    + (grid[i - 1][j - 1] == 'X' ? 1 : 0);
              
                // Calculate prefix sum for 'Y' count using inclusion-exclusion principle
                prefixSum[i][j][1] = prefixSum[i - 1][j][1] 
                                    + prefixSum[i][j - 1][1] 
                                    - prefixSum[i - 1][j - 1][1]
                                    + (grid[i - 1][j - 1] == 'Y' ? 1 : 0);
              
                // Check if submatrix from (0,0) to (i-1,j-1) is valid
                // Valid means: contains at least one 'X' and equal number of 'X' and 'Y'
                if (prefixSum[i][j][0] > 0 && prefixSum[i][j][0] == prefixSum[i][j][1]) {
                    result++;
                }
            }
        }
      
        return result;
    }
}
```

---