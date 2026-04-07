# <u>36. Valid Sudoku</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/valid-sudoku/

---

## 🧠 Intuition:
* 🔹 The goal is to check whether a Sudoku board configuration is valid according to Sudoku rules.

* 🔹 A valid Sudoku means:
    - Each number **1–9 appears only once** in every **row**.
    - Each number **1–9 appears only once** in every **column**.
    - Each number **1–9 appears only once** in every **3×3 subgrid**.

* 🔹 Use three boolean matrices to track used numbers:
    - `rows[9][9]` → tracks numbers seen in each row.
    - `cols[9][9]` → tracks numbers seen in each column.
    - `subgrids[9][9]` → tracks numbers seen in each 3×3 box.

* 🔹 Traverse the board cell by cell.

* 🔹 Skip empty cells (`'.'`) because they don’t affect validity.

* 🔹 Convert character `'1'–'9'` into index `0–8` using:
    - number = currentChar - '0' - 1

* 🔹 Compute subgrid index using:
    - subgridIndex = (row / 3) * 3 + (col / 3)

    - → maps every cell to one of the 9 subgrids.

* 🔹 Before marking a number:
    - Check if it already exists in the same row, column, or subgrid.
    - If yes → Sudoku is invalid → return `false`.

* 🔹 Otherwise mark the number as seen in all three trackers.

* 🔹 If entire board is processed without conflicts → return `true`.

---

## ⏱ Time Complexity

**O(1)**

* Sudoku board size is fixed 9 × 9 = 81 cells.
* Each cell is visited once.

✅ O(9 × 9) = O(1)

---

## 📦 Space Complexity

**O(1)**

* Three boolean arrays:
    - `rows[9][9]`
    - `cols[9][9]`
    - `subgrids[9][9]`
    - 
    - Total storage is constant.

---

## 💻 Java Code

```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        boolean rows[][] = new boolean[9][9], cols[][] = new boolean[9][9], subgrids[][] = new boolean[9][9];

        for(int i = 0; i < 9; i++){
            for(int j = 0; j < 9; j++){
                char currentChar = board[i][j];

                if(currentChar == '.'){
                    continue;
                }

                int number = currentChar - '0' - 1;

                int subgridsIdx = (i / 3)* 3 + j / 3;

                if(rows[i][number] || cols[j][number] || subgrids[subgridsIdx][number]){
                    return false;
                }

                rows[i][number] = true;
                cols[j][number] = true;
                subgrids[subgridsIdx][number] = true;
            }
        }
        return true;
    }
}
```

---