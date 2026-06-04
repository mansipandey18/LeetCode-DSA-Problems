# <u>130. Surrounded Regions</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/surrounded-regions/

---

## 🧠 Intuition:
* 🔹 The goal is to **capture all ‘O’ regions that are fully surrounded by ‘X’**.

* 🔹 Any `‘O’` connected to the **boundary cannot be flipped**, because it is not fully enclosed.

* 🔹 Step 1: Start DFS from all **border cells (first/last row and column)**.

* 🔹 During DFS, mark all reachable `‘O’` cells from the boundary as **safe (temporary marker '.')**.

* 🔹 Step 2: After marking, traverse the entire board:
    - Convert remaining **unmarked ‘O’ → ‘X’** (these are fully surrounded).
    - Convert **'.' back → 'O'** (restore safe regions).

* 🔹 This works because:
    - Boundary-connected regions are protected.
    - Only fully enclosed regions remain unchanged until final conversion.

* 🔹 DFS ensures we explore and mark all connected components efficiently.

---

## ⏱ Time Complexity

**O(rows * cols)**

* Each cell is visited at most once during DFS and final traversal.
    
---

## 📦 Space Complexity

**O(rows * cols)**

* DFS recursion stack in worst case: `O(R × C)` (entire board filled with 'O').
* No extra data structures besides recursion.

---

## 💻 Java Code

```java
class Solution {
    private final int[] DIRECTIONS = {-1, 0, 1, 0, -1};
    private char[][] board;
    private int rows;
    private int cols;

    public void solve(char[][] board) {
        rows = board.length;
        cols = board[0].length;
        this.board = board;
      
        for (int row = 0; row < rows; row++) {
            dfs(row, 0);              // Left border
            dfs(row, cols - 1);       // Right border
        }
      
        for (int col = 0; col < cols; col++) {
            dfs(0, col);              // Top border
            dfs(rows - 1, col);       // Bottom border
        }
      
        for (int row = 0; row < rows; row++) {
            for (int col = 0; col < cols; col++) {
                if (board[row][col] == '.') {
                    board[row][col] = 'O';
                } else if (board[row][col] == 'O') {
                    board[row][col] = 'X';
                }
            }
        }
    }

    private void dfs(int row, int col) {
        if (row < 0 || row >= rows || col < 0 || col >= cols || board[row][col] != 'O') {
            return;
        }
      
        board[row][col] = '.';
      
        for (int k = 0; k < 4; k++) {
            int newRow = row + DIRECTIONS[k];
            int newCol = col + DIRECTIONS[k + 1];
            dfs(newRow, newCol);
        }
    }
}
```

---