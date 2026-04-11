# <u>289. Game of Life</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/game-of-life/

---

## 🧠 Intuition:
* 🔹 The problem follows **Conway’s Game of Life rules**, where each cell’s next state depends on its **8 neighbors**.

* 🔹 We must update the board **in-place**, so we cannot directly overwrite values (it would affect neighbor calculations).

* 🔹 To handle this, use state encoding:
    - `1 → 2` → cell was alive, will die
    - `0 → -1` → cell was dead, will become alive

* 🔹 First pass:
    - For every cell, count its **live neighbors** using a helper function.
    - Apply rules:
        * Live cell dies if `< 2` or `> 3` neighbors → mark as `2`
        * Dead cell becomes alive if exactly `3` neighbors → mark as `-1`
        * Otherwise, no change

* 🔹 While counting neighbors:
    - Treat `1` and `2` as **alive** (because 2 was originally alive).

* 🔹 Second pass:
    - Convert encoded states to final values:
        * `2 → 0` (dead)
        * `-1 → 1` (alive)
This ensures all updates happen **simultaneously without extra space**.

---

## ⏱ Time Complexity

**O(m * n)**

* Where :
    - `m` = number of `rows`
    - `n` = number of `columns`

* For each cell, we check up to **8 neighbors** → constant work.

* Total traversal:
    - First pass → `O(m × n)`
    - Second pass → `O(m × n)`
    
---

## 📦 Space Complexity

**O(1)**

* No extra matrix is used.
* Only constant variables.


---

## 💻 Java Code

```java
class Solution {
    public void gameOfLife(int[][] board) {
        int rows = board.length;
        int cols = board[0].length;
      
        // First pass: Mark cells that need to change state
        // Use encoding: 2 = was alive, will die; -1 = was dead, will become alive
        for (int row = 0; row < rows; row++) {
            for (int col = 0; col < cols; col++) {
                // Count live neighbors (excluding current cell)
                int liveNeighbors = countLiveNeighbors(board, row, col, rows, cols);
              
                // Apply Conway's Game of Life rules
                // Rule 1 & 3: Live cell with < 2 or > 3 neighbors dies
                if (board[row][col] == 1 && (liveNeighbors < 2 || liveNeighbors > 3)) {
                    board[row][col] = 2; // Mark as "will die"
                }
                // Rule 4: Dead cell with exactly 3 neighbors becomes alive
                if (board[row][col] == 0 && liveNeighbors == 3) {
                    board[row][col] = -1; // Mark as "will become alive"
                }
                // Rule 2: Live cell with 2-3 neighbors survives (no change needed)
            }
        }
      
        // Second pass: Update all cells to their final states
        for (int row = 0; row < rows; row++) {
            for (int col = 0; col < cols; col++) {
                if (board[row][col] == 2) {
                    board[row][col] = 0; // Cell dies
                } else if (board[row][col] == -1) {
                    board[row][col] = 1; // Cell becomes alive
                }
            }
        }
    }

    private int countLiveNeighbors(int[][] board, int row, int col, int rows, int cols) {
        int liveCount = 0;
      
        // Check all 8 neighboring cells
        for (int neighborRow = row - 1; neighborRow <= row + 1; neighborRow++) {
            for (int neighborCol = col - 1; neighborCol <= col + 1; neighborCol++) {
                // Skip out-of-bounds cells and the current cell itself
                if (neighborRow < 0 || neighborRow >= rows || 
                    neighborCol < 0 || neighborCol >= cols ||
                    (neighborRow == row && neighborCol == col)) {
                    continue;
                }
              
                // Count cell as live if it's currently alive (value > 0)
                // This includes cells marked as 2 (will die) since they're currently alive
                if (board[neighborRow][neighborCol] > 0) {
                    liveCount++;
                }
            }
        }
      
        return liveCount;
    }
}  
```

---