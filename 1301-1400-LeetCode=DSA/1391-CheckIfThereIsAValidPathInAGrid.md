# <u>1391. Check if There is a Valid Path in a Grid</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/check-if-there-is-a-valid-path-in-a-grid/
---

## 🧠 Intuition:
* 🔹 Each cell in the grid represents a street type, and every type connects only in specific directions

* 🔹 Directly checking valid connections between neighboring cells can become complex because each street type has different movement rules

* 🔹 To simplify this, each original cell is expanded into a **3 × 3 mini-grid**, where the valid street path is drawn using `true` values

* 🔹 This converts the problem into a simple path-finding problem on a larger boolean grid

* 🔹 For example:
    - Horizontal street → mark the middle row
    - Vertical street → mark the middle column
    - Corner streets → mark only the connected turning path

* 🔹 After building this upscaled grid, if a continuous path exists from the start cell to the destination cell, then the original grid also has a valid path

* 🔹 Start DFS from the top-left valid center point `(1,1)` of the expanded grid

* 🔹 During DFS:
    - Stop if out of bounds
    - Stop if current cell is `false` (no road exists)
    - Return true if destination center `(last-2, last-2)` is reached

* 🔹 Mark visited cells as `false` to avoid revisiting and infinite loops

* 🔹 If DFS reaches the destination, return `true`, otherwise `false`

* 🔹 This approach avoids manual street compatibility checks and turns the problem into standard graph traversal

---

## ⏱ Time Complexity

**O(m * n)**

* Creating the expanded grid takes **O(m × n)**
* DFS visits each cell of the expanded grid once
* Expanded grid size = `(3m × 3n)` = still proportional to **O(m × n)**
    
---

## 📦 Space Complexity

**O(m * n)**

* Upscaled boolean grid uses **O(m × n)** space
* DFS recursion stack can also take up to **O(m × n)** in worst case

---

## 💻 Java Code

```java
class Solution {
    public boolean hasValidPath(int[][] grid) {
        final int m = grid.length;
        final int n = grid[0].length;
        // g := upscaled grid
        boolean[][] g = new boolean[m * 3][n * 3];

        for (int i = 0; i < m; ++i)
            for (int j = 0; j < n; ++j)
                switch (grid[i][j]) {
                  case 1:
                        g[i * 3 + 1][j * 3 + 0] = true;
                        g[i * 3 + 1][j * 3 + 1] = true;
                        g[i * 3 + 1][j * 3 + 2] = true;
                        break;
                  case 2:
                        g[i * 3 + 0][j * 3 + 1] = true;
                        g[i * 3 + 1][j * 3 + 1] = true;
                        g[i * 3 + 2][j * 3 + 1] = true;
                        break;
                  case 3:
                        g[i * 3 + 1][j * 3 + 0] = true;
                        g[i * 3 + 1][j * 3 + 1] = true;
                        g[i * 3 + 2][j * 3 + 1] = true;
                        break;
                  case 4:
                        g[i * 3 + 1][j * 3 + 1] = true;
                        g[i * 3 + 1][j * 3 + 2] = true;
                        g[i * 3 + 2][j * 3 + 1] = true;
                        break;
                  case 5:
                        g[i * 3 + 0][j * 3 + 1] = true;
                        g[i * 3 + 1][j * 3 + 0] = true;
                        g[i * 3 + 1][j * 3 + 1] = true;
                        break;
                  case 6:
                        g[i * 3 + 0][j * 3 + 1] = true;
                        g[i * 3 + 1][j * 3 + 1] = true;
                        g[i * 3 + 1][j * 3 + 2] = true;
                        break;
                }

        return dfs(g, 1, 1);
    }

    private boolean dfs(boolean[][] g, int i, int j) {
        if (i < 0 || i == g.length || j < 0 || j == g[0].length)
            return false;
        if (!g[i][j]) // There's no path here.
            return false;
        if (i == g.length - 2 && j == g[0].length - 2)
             return true;

        g[i][j] = false; // Mark as visited.
        
        return dfs(g, i + 1, j) || dfs(g, i - 1, j) || dfs(g, i, j + 1) || dfs(g, i, j - 1);
    
    }
}
```

---