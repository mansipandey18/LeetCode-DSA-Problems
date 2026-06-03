# <u>200. Number of Islands</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/number-of-islands/

---

## 🧠 Intuition:
* 🔹 Treat the grid as a graph where each land cell +(`'1'`) is connected to its neighboring land cells (up, down, left, right).

* 🔹 Traverse every cell in the grid.

* 🔹 Whenever an unvisited land cell (`'1'`) is found, it means a new island has been discovered.

* 🔹 Start a DFS from that cell to visit and mark all connected land cells as water (`'0'`).

* 🔹 This ensures the same island is not counted multiple times.

* 🔹 After the DFS completes, increment the island count by 1.

* 🔹 Repeat the process until all cells have been processed.

* 🔹 The final island count represents the total number of disconnected groups of land.


---

## ⏱ Time Complexity

**O(rows * cols)**

* each cell is visited at most once.
    
---

## 📦 Space Complexity

**O(rows * cols)**

* **O(rows * cols)** in the worst case due to the recursive DFS call stack (when the entire grid is one large island).

---

## 💻 Java Code

```java
class Solution {
    private char[][] grid;
    private int rows;
    private int cols;

    public int numIslands(char[][] grid) {
        this.rows = grid.length;
        this.cols = grid[0].length;
        this.grid = grid;
      
        int islandCount = 0;
      
        for (int row = 0; row < rows; row++) {
            for (int col = 0; col < cols; col++) {
                if (grid[row][col] == '1') {
                    dfs(row, col);
                    islandCount++;
                }
            }
        }
      
        return islandCount;
    }

    private void dfs(int row, int col) {
        grid[row][col] = '0';
      
        int[] directions = {-1, 0, 1, 0, -1};
      
        for (int i = 0; i < 4; i++) {
            int newRow = row + directions[i];
            int newCol = col + directions[i + 1];
          
            if (newRow >= 0 && newRow < rows && 
                newCol >= 0 && newCol < cols && 
                grid[newRow][newCol] == '1') {
                dfs(newRow, newCol);
            }
        }
    }
}
```

---