# <u>73. Set Matrix Zeroes</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/set-matrix-zeroes/

---

## 🧠 Intuition:
* 🔹 The problem requires setting entire **row and column to 0** if any cell is 0, but doing it **in-place** (without extra space).

* 🔹 Instead of using extra arrays, use the first row and first column as markers.

* 🔹 Traverse the matrix:
    - If `matrix[i][j] == 0`:
        * Mark its row → set `matrix[i][0] = 0`
        * Mark its column → set `matrix[0][j] = 0`

    - Special case for first column → use a variable c0 to track if it needs to be zero.

* 🔹 After marking, traverse the matrix again (excluding first row & column):
    - If the corresponding row or column is marked (`matrix[i][0] == 0` or `matrix[0][j] == 0`), set the cell to 0.

* 🔹 Finally:
    - If `matrix[0][0] == 0`, zero out the entire first row.
    - If `c0 == 0`, zero out the entire first column.

* 🔹 This approach avoids overwriting important information too early and achieves constant space optimization.

---

## ⏱ Time Complexity

**O(m * n)**

* Where :
    - `n` = number of rows
    - `m` = number of columns

* First pass (marking) → **O(n × m)**
* Second pass (filling zeros) → **O(n × m)**
* Final row & column updates → **O(n + m)**
    
---

## 📦 Space Complexity

**O(1)**

* No extra data structures used.
* Only one variable `c0`.

---

## 💻 Java Code

```java
class Solution {
    public void setZeroes(int[][] matrix) {
        int n = matrix.length, m = matrix[0].length, c0 = 1;

        // traverse the matrix and mark first cell of each row and column
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(matrix[i][j] == 0){
                    // mark i-th row
                    matrix[i][0] = 0;

                    // mark j-th row
                    if(j == 0){
                        c0 = 0;
                    } else{
                        matrix[0][j] = 0;
                    }
                }
            }
        }
        // Traverse and mark the matrix from (1, 1) to (n - 1, m - 1)
        for(int i = 1; i < n; i++){
            for(int j = 1; j < m; j++){
                // check for col & row
                if(matrix[i][0] == 0 || matrix[0][j] == 0){
                    matrix[i][j] = 0;
                }
            }
        }
        // Mark the first row
        if(matrix[0][0] == 0){
            for(int j = 0; j < m; j++){
                matrix[0][j] = 0;
            }
        }
        // Mark the first col
        if(c0 == 0){
            for(int i = 0; i < n; i++){
                matrix[i][0] = 0;
            }
        }

    }
}
```

---