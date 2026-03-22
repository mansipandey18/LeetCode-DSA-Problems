# <u>1886. Determine Whether Matrix Can Be Obtained By Rotation</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/determine-whether-matrix-can-be-obtained-by-rotation/

---

## 🧠 Intuition:
* 🔹 We want to check if matrix mat can become target after rotating it.

* 🔹 A square matrix can only have 4 possible rotations:
    - 0° (original)
    - 90°
    - 180°
    - 270°

* 🔹 So instead of thinking of many cases, we just try all 4 rotations.

* 🔹 First, check if the current matrix already matches the target.

* 🔹 If not, rotate the matrix 90° clockwise.

* 🔹 After rotating, compare again with the target matrix.

* 🔹 Repeat this process up to 4 times.

* 🔹 If at any rotation both matrices become the same → return true.

* 🔹 If none of the rotations match → return false.
---

## ⏱ Time Complexity

**O(n^2)**

* Let `n` be the size of the matrix `(n × n)`.
* Per rotation : 
    - Matrix comparison → O(n^2)
    - Matrix rotation → O(n^2)
    
---

## 📦 Space Complexity

**O(1)**

* Rotation is done in-place.
* No extra matrix is created.

---

## 💻 Java Code

```java
class Solution {
    public boolean findRotation(int[][] mat, int[][] target) {
        int rotationAttempts = 4;
      
        while (rotationAttempts-- > 0) {
            // Check if current rotation matches target
            if (equals(mat, target)) {
                return true;
            }
            // Rotate matrix 90 degrees clockwise for next check
            rotate(mat);
        }
      
        return false;
    }

    private void rotate(int[][] matrix) {
        int n = matrix.length;
      
        // Process each layer from outer to inner
        for (int layer = 0; layer < n / 2; ++layer) {
            // Define the boundaries of current layer
            int first = layer;
            int last = n - 1 - layer;
          
            // Rotate elements in current layer
            for (int offset = first; offset < last; ++offset) {
                // Save top element
                int temp = matrix[first][offset];
              
                // Move left to top
                matrix[first][offset] = matrix[n - offset - 1][first];
              
                // Move bottom to left
                matrix[n - offset - 1][first] = matrix[last][n - offset - 1];
              
                // Move right to bottom
                matrix[last][n - offset - 1] = matrix[offset][last];
              
                // Move saved top to right
                matrix[offset][last] = temp;
            }
        }
    }

    
    private boolean equals(int[][] matrix1, int[][] matrix2) {
        int n = matrix1.length;
      
        // Compare each element
        for (int row = 0; row < n; ++row) {
            for (int col = 0; col < n; ++col) {
                if (matrix1[row][col] != matrix2[row][col]) {
                    return false;
                }
            }
        }
      
        return true;
    }
}
```

---