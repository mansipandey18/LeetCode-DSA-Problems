# <u>1301. Number of Paths with Max Score</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/number-of-paths-with-max-score/

---

## 🧠 Intuition:
* 🔹 Traverse the board **from the bottom-right (`S`) to the top-left (`E`)**, since every move in the original problem (down, right, diagonal) becomes a transition from already computed cells.

* 🔹 Use two DP tables:
    - `maxScore[i][j]` → the **maximum score** that can be collected from cell `(i, j)` to the destination.
    - `pathCount[i][j]` → the **number of paths** that achieve this maximum score.

* 🔹 Initialize the destination (`S`) with score `0` and path count `1`.

* 🔹 For every cell, check the three possible next cells (down, right, and diagonal).

* 🔹 Ignore cells that are **out of bounds, blocked (`X`), or unreachable**.

* 🔹 If a neighboring cell provides a **higher score**, update the current cell's maximum score and copy its path count.

* 🔹 If another neighboring cell provides the **same maximum score**, add its path count (modulo 10^9 + 7).

* 🔹 After determining the best score for a cell, add the numeric value of the current cell (if it contains a digit).

* 🔹 At the end, `maxScore[0][0]` gives the maximum obtainable score, and `pathCount[0][0]` gives the number of optimal paths.

---

## ⏱ Time Complexity

**O(n^2)**

* Every cell is processed once, and each checks at most 3 neighboring cells.
    
---

## 📦 Space Complexity

**O(n^2)**

* For the `maxScore` and `pathCount` DP tables.

---

## 💻 Java Code

```java
class Solution {
    private List<String> board;
    private int boardSize;
  
    private int[][] maxScore;    // maxScore[i][j]: maximum score from (i,j) to end
    private int[][] pathCount;   // pathCount[i][j]: number of paths achieving max score
  
    private final int MOD = (int) 1e9 + 7;

    public int[] pathsWithMaxScore(List<String> board) {
        this.boardSize = board.size();
        this.board = board;
      
        maxScore = new int[boardSize][boardSize];
        pathCount = new int[boardSize][boardSize];
      
        for (int[] row : maxScore) {
            Arrays.fill(row, -1);
        }
      
        maxScore[boardSize - 1][boardSize - 1] = 0;
        pathCount[boardSize - 1][boardSize - 1] = 1;
      
        for (int row = boardSize - 1; row >= 0; row--) {
            for (int col = boardSize - 1; col >= 0; col--) {
                updateFromNextCell(row, col, row + 1, col);      // Move down
                updateFromNextCell(row, col, row, col + 1);      // Move right
                updateFromNextCell(row, col, row + 1, col + 1);  // Move diagonal
              
                if (maxScore[row][col] != -1) {
                    char currentChar = board.get(row).charAt(col);
                    if (currentChar >= '0' && currentChar <= '9') {
                        maxScore[row][col] += (currentChar - '0');
                    }
                }
            }
        }
      
        int[] result = new int[2];
      
        if (maxScore[0][0] != -1) {
            result[0] = maxScore[0][0];
            result[1] = pathCount[0][0];
        }
      
        return result;
    }

    
    private void updateFromNextCell(int currentRow, int currentCol, int nextRow, int nextCol) {
        if (nextRow >= boardSize || nextCol >= boardSize) {
            return;  // Out of bounds
        }
      
        if (maxScore[nextRow][nextCol] == -1) {
            return;  // Next cell is unreachable
        }
      
        char currentChar = board.get(currentRow).charAt(currentCol);
        if (currentChar == 'X' || currentChar == 'S') {
            return;  // Current cell is obstacle or end position
        }
      
        if (maxScore[nextRow][nextCol] > maxScore[currentRow][currentCol]) {
            maxScore[currentRow][currentCol] = maxScore[nextRow][nextCol];
            pathCount[currentRow][currentCol] = pathCount[nextRow][nextCol];
        } else if (maxScore[nextRow][nextCol] == maxScore[currentRow][currentCol]) {
            pathCount[currentRow][currentCol] = 
                (pathCount[currentRow][currentCol] + pathCount[nextRow][nextCol]) % MOD;
        }
    }
}
```

---