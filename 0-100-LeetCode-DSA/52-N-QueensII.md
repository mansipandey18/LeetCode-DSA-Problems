# <u>52. N-Queens II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/n-queens-ii/

---

## 🧠 Intuition:
* 🔹 We need to place `n` queens on an `n × n` chessboard such that no two queens attack each other.

* 🔹 Use **Backtracking** to place queens row by row, trying every possible column in the current row.

* 🔹 Maintain three boolean arrays to quickly check whether a position is safe:
    - `columnsInUse` → tracks which columns already contain a queen.
    - `positiveDiagonalsInUse` → tracks diagonals with the same `row + col` value.
    - `negativeDiagonalsInUse` → tracks diagonals with the same `row - col` value (shifted by `n` to avoid negative indices).

* 🔹 For each cell `(row, col)`:
    - If its column or diagonals already have a queen, skip that position.
    - Otherwise, place the queen and mark the corresponding column and diagonals as occupied.

* 🔹 Recursively move to the next row to place the remaining queens.

* 🔹 When all rows are processed (`row == n`), a valid arrangement is found, so increase the solution count.

* 🔹 After exploring a placement, remove the queen and unmark the column and diagonals (**backtracking**) to try other possible arrangements.

* 🔹 Using boolean arrays allows checking whether a position is valid in **O(1)** time, making the backtracking more efficient.

---

## ⏱ Time Complexity

**O(n!)**

* In the worst case, we try different column arrangements for each row, leading to factorial combinations.
    
---

## 📦 Space Complexity

**O(n)**

* For the recursion stack and the column/diagonal tracking arrays.

---

## 💻 Java Code

```java
class Solution {
    private int boardSize;
    private int solutionsCount;
    private boolean[] columnsInUse; 
    private boolean[] positiveDiagonalsInUse; 
    private boolean[] negativeDiagonalsInUse; 
    public int totalNQueens(int n) {
        this.boardSize = n;
        this.columnsInUse = new boolean[n]; 
        this.positiveDiagonalsInUse = new boolean[2 * n]; 
        this.negativeDiagonalsInUse = new boolean[2 * n]; 
        this.solutionsCount = 0;
        placeQueens(0);
        return solutionsCount;
    }

    private void placeQueens(int row) {
        if (row == boardSize) {
            ++solutionsCount;
            return;
        }

        for (int col = 0; col < boardSize; ++col) {
            int positiveDiagonalIndex = row + col;
            int negativeDiagonalIndex = row - col + boardSize;
            if (columnsInUse[col] || positiveDiagonalsInUse[positiveDiagonalIndex] || 
                negativeDiagonalsInUse[negativeDiagonalIndex]) {
                continue; 
            }

            columnsInUse[col] = true;
            positiveDiagonalsInUse[positiveDiagonalIndex] = true;
            negativeDiagonalsInUse[negativeDiagonalIndex] = true;
            placeQueens(row + 1); 

            columnsInUse[col] = false;
            positiveDiagonalsInUse[positiveDiagonalIndex] = false;
            negativeDiagonalsInUse[negativeDiagonalIndex] = false;
        }
    }
}
```

---