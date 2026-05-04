# <u>48. Rotate Image</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/rotate-image/

---

## 🧠 Intuition:
* 🔹 The goal is to rotate the matrix **90° clockwise in-place**

* 🔹 Instead of rotating elements one by one (which is complex), we use a **2-step transformation trick**

* 🔹 Step 1: **Transpose the matrix**
    - Convert rows into columns → swap `matrix[i][j]` with `matrix[j][i]`
    - Only swap for `j > i` to avoid double swapping
    - After transpose, the matrix is flipped across its main diagonal

* 🔹 Step 2: **Reverse each row**
    - For every row, reverse elements from left to right
    - This converts the transposed matrix into a 90° rotated matrix

* 🔹 Why this works:
    - Transpose changes (`i, j`) → (`j, i`)
    - Row reversal shifts elements to their correct rotated positions

* 🔹 This approach avoids extra space and performs rotation directly in the same matrix

---

## ⏱ Time Complexity

**O(n^2)**

* Transpose → **O(n²)**
* Reverse rows → **O(n²)**
    
---

## 📦 Space Complexity

**O(1)**

* No extra space used (in-place operations)

---

## 💻 Java Code

```java
class Solution {
    public void rotate(int[][] matrix) {
        // perform transpose
        for(int i = 0; i < matrix.length; i++){
            for(int j = i+1; j < matrix.length; j++){
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }
        // Reverse each row
        for(int i = 0; i < matrix.length; i++){
            int start = 0, end = matrix.length-1;
            while(start < end){
                int temp = matrix[i][start];
                matrix[i][start] = matrix[i][end];
                matrix[i][end] = temp;

                start++; end--;
            }
        }
    }
}
```

---