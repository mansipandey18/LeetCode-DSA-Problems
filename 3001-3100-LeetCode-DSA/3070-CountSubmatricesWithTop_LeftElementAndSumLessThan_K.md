# <u>3070. Count Submatrices with Top-Left Element and Sum Less Than k</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/count-submatrices-with-top-left-element-and-sum-less-than-k/

---

## 🧠 Intuition:
* 🔹 Every valid submatrix must start from the top-left cell (0,0).

* 🔹 So, each cell (i, j) represents one possible submatrix ending at that position.

* 🔹 Instead of calculating submatrix sums again and again, we store cumulative sums using a 2D prefix sum array.

* 🔹 The prefix sum at (i, j) gives the total sum of elements from (0,0) → (i,j).

* 🔹 We build this sum using previously computed top and left values to avoid recomputation.

* 🔹 While constructing the prefix sum matrix, we immediately check:

   - if current submatrix sum ≤ k, then it is valid.

* 🔹 Each valid prefix sum corresponds to one valid submatrix, so we increase the count.

* 🔹 This converts repeated sum calculation into a single traversal of the grid.

---

## ⏱ Time Complexity

**O(m * n)**

Where:
 - m = number of rows  
 - n = number of columns 

---

## 📦 Space Complexity

**O(m * n)**

We create an extra prefix sum matrix of size:
  
 - (rows + 1) × (cols + 1)

---

## 💻 Java Code

```java
class Solution {
    public int countSubmatrices(int[][] grid, int k) {
        int rows = grid.length;
        int cols = grid[0].length;
      
        int[][] prefixSum = new int[rows + 1][cols + 1];
      
        int count = 0;
      
        for (int i = 1; i <= rows; i++) {
            for (int j = 1; j <= cols; j++) {
                prefixSum[i][j] = prefixSum[i - 1][j]           // Sum from top
                                + prefixSum[i][j - 1]           // Sum from left
                                - prefixSum[i - 1][j - 1]       // Remove overlap
                                + grid[i - 1][j - 1];           // Add current element
              
                if (prefixSum[i][j] <= k) {
                    count++;
                }
            }
        }
      
        return count;
    }
}
```

---