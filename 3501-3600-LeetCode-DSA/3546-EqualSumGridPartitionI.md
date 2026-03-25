# <u>3546. Equal Sum Grid Partition I</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/equal-sum-grid-partition-i/

---

## 🧠 Intuition:
* 🔹 Calculate the total sum of all elements in the grid.

* 🔹 If the total sum is odd, equal partition is impossible → return false.

* 🔹 Try to divide the grid using a horizontal cut (between rows).

* 🔹 Keep adding row values to a running prefix sum from top to bottom.

* 🔹 If the prefix sum becomes half of the total sum and at least one row remains below, a valid partition exists.

* 🔹 If no horizontal split works, try a vertical cut (between columns).

* 🔹 Add column values from left to right while maintaining a prefix sum.

* 🔹 If the prefix sum equals half of the total sum and at least one column remains on the right, partition is possible.

* 🔹 If neither horizontal nor vertical cut satisfies the condition, return false.

---

## ⏱ Time Complexity

**O(m * n)**

* Let : 
    - `r` = number of rows
    - `c` = number of columns
    
* **1️⃣ Calculate total sum**
    - Traverse entire grid → O(m × n)

* **2️⃣ Horizontal partition check**
    - Each element visited once again → O(m × n)

* **3️⃣ Vertical partition check**
    - Again traverse all elements → O(m × n)
---

## 📦 Space Complexity

**O(1)**

* Only variables used (totalSum, prefixSum, counters).
* No extra data structures.

---

## 💻 Java Code

```java
class Solution {
    public boolean canPartitionGrid(int[][] grid) {
        long totalSum = 0;
        for (int[] row : grid) {
            for (int value : row) {
                totalSum += value;
            }
        }
      
        // If total sum is odd, we cannot partition into two equal halves
        if (totalSum % 2 != 0) {
            return false;
        }
      
        int rows = grid.length;
        int cols = grid[0].length;
      
        // Check if we can partition horizontally (between rows)
        long prefixSum = 0;
        for (int i = 0; i < rows; i++) {
            // Add current row sum to prefix sum
            for (int value : grid[i]) {
                prefixSum += value;
            }
            // Check if prefix sum equals half of total sum
            // Also ensure we're not at the last row (need at least one row on each side)
            if (prefixSum * 2 == totalSum && i < rows - 1) {
                return true;
            }
        }
      
        // Check if we can partition vertically (between columns)
        prefixSum = 0;
        for (int j = 0; j < cols; j++) {
            // Add current column sum to prefix sum
            for (int i = 0; i < rows; i++) {
                prefixSum += grid[i][j];
            }
            // Check if prefix sum equals half of total sum
            // Also ensure we're not at the last column (need at least one column on each side)
            if (prefixSum * 2 == totalSum && j < cols - 1) {
                return true;
            }
        }
      
        // No valid partition found
        return false;
    
    }
}
```

---