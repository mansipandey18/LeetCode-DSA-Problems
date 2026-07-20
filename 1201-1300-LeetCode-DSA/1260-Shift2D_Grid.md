# <u>1260. Shift 2D Grid</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/shift-2d-grid/

---

## 🧠 Intuition:
* 🔹 A single shift moves every element **one position forward** in row-major order.

* 🔹 The last element of the grid wraps around and becomes the /**first element**.

* 🔹 Store the last element before shifting because it would otherwise be overwritten.

* 🔹 Traverse the grid from **top-left to bottom-right**:
    - Save the current cell value.
    - Replace it with the value carried from the previous cell (`newVal`).
    - Update `newVal` with the saved value for the next position.

* 🔹 After one complete traversal, the grid has been shifted by **one position**.

* 🔹 Repeat this process `k` times to achieve the required number of shifts.

* 🔹 Finally, convert the shifted 2D array into the required `List<List<Integer>>` format and return it.

---

## ⏱ Time Complexity

**O(k × m × n)**

* Each shift traverses all `m × n` cells, and the process is repeated `k` times.
    
---

## 📦 Space Complexity

**O(1)**

* The shifting is done in-place, using only a few temporary variables (excluding the output).

---

## 💻 Java Code

```java
class Solution {
    public int[][] oneShift(int[][] grid, int m, int n) 
    {           
        int newVal= grid[m-1][n-1];
        
        for(int i=0; i<m; i++) {
            for(int j=0; j<n; j++) {
                int temp= grid[i][j];
                grid[i][j]= newVal;
                newVal= temp;
            }
        }
        
        return grid;
    }
    
    public List<List<Integer>> shiftGrid(int[][] grid, int k) 
    {
        while(k-->0) {
            grid= oneShift(grid, grid.length, grid[0].length);
        }

        return (List)Arrays.asList(grid);
    }

}
```

---