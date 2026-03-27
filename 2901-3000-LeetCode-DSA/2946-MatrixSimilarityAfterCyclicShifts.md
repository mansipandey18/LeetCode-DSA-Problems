# <u>2946. Matrix Similarity After Cyclic Shifts</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/matrix-similarity-after-cyclic-shifts/

---

## 🧠 Intuition:
* 🔹 First, take `k % columnCount`
    - Because shifting `columnCount` times brings row back to original position.

* 🔹 Traverse every cell `(row, col)` of the matrix.

* 🔹 For odd rows:
    - Right cyclic shift happens.
    - New index becomes:
        * `(col + k) % columnCount`

* 🔹 For even rows:
    - Left cyclic shift happens.
    - New index becomes:
        * `(col - k + columnCount) % columnCount`
    - Adding `columnCount` avoids negative index.

* 🔹 Compare:
    - Current element
    - Element at its shifted position

* 🔹 If any mismatch occurs → return `false`.

* 🔹 If all positions match → return `true`.

---

## ⏱ Time Complexity

**O(m * n)**

* The algorithm checks every element of the matrix once.
* Where:
    - `m` = number of rows
    - `n` = number of columns
* Each check takes O(1) time.
    
---

## 📦 Space Complexity

**O(1)**

* No extra array or matrix is created.
* Only a few variables (row, col, shiftedPosition, etc.) are used.

---

## 💻 Java Code

```java
class Solution {
    public boolean areSimilar(int[][] mat, int k) {
        int rowCount = mat.length;
        int columnCount = mat[0].length;
      
        // Optimize k to avoid unnecessary full rotations
        k = k % columnCount;
      
        // Check each element in the matrix
        for (int row = 0; row < rowCount; row++) {
            for (int col = 0; col < columnCount; col++) {
              
                // For odd rows (1, 3, 5...), check right shift
                if (row % 2 == 1) {
                    int shiftedPosition = (col + k) % columnCount;
                    if (mat[row][col] != mat[row][shiftedPosition]) {
                        return false;
                    }
                }
              
                // For even rows (0, 2, 4...), check left shift
                if (row % 2 == 0) {
                    // Add columnCount to handle negative modulo correctly
                    int shiftedPosition = (col - k + columnCount) % columnCount;
                    if (mat[row][col] != mat[row][shiftedPosition]) {
                        return false;
                    }
                }
            }
        }
      
        // All elements match their shifted positions
        return true;
    }
}
```

---