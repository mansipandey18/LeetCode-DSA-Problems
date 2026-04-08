# <u>54. Spiral Matrix</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/spiral-matrix/

---

## 🧠 Intuition:
* 🔹 The problem asks to **traverse the matrix in spiral order** (clockwise).

* 🔹 Instead of changing directions manually, we **shrink boundaries layer by layer**.

* 🔹 Maintain four boundaries:
    - `r1` → top row
    - `r2` → bottom row
    - `c1` → left column
    - `c2` → right column

* 🔹 Each iteration processes **one rectangular layer** of the matrix.

* 🔹 Traverse in 4 steps:
    - **Top row** → move left to right (`c1 → c2`).
    - **Right column** → move top to bottom (`r1+1 → r2-1`).
    - **Bottom row** → move right to left (`c2 → c1`).
    - **Left column** → move bottom to top (`r2-1 → r1+1`).

* 🔹 After completing one layer:
    - Move boundaries inward:
        * `r1++`, `c1++` (shrink from top & left)
        * `r2--`, `c2--` (shrink from bottom & right)

* 🔹 Continue until all elements (`m × n`) are added to the result.

* 🔹 The size check (`ans.size() < m*n`) prevents duplicate traversal when only one row/column remains.

---

## ⏱ Time Complexity

**O(m * n)**

* Where :
    - `m` = length of rows
    - `n` = length of columns
    
---

## 📦 Space Complexity

**O(m * n)**

* Output list stores all matrix elements → **O(m × n)**.
* Only constant extra variables are used besides output.

---


## 💻 Java Code

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        if (matrix.length == 0)
          return new ArrayList<>();

        final int m = matrix.length;
        final int n = matrix[0].length;
        List<Integer> ans = new ArrayList<>();
        int r1 = 0;
        int c1 = 0;
        int r2 = m - 1;
        int c2 = n - 1;

        // Repeatedly add matrix[r1..r2][c1..c2] to `ans`.
        while (ans.size() < m * n) {
          for (int j = c1; j <= c2 && ans.size() < m * n; ++j)
            ans.add(matrix[r1][j]);
          for (int i = r1 + 1; i <= r2 - 1 && ans.size() < m * n; ++i)
            ans.add(matrix[i][c2]);
          for (int j = c2; j >= c1 && ans.size() < m * n; --j)
            ans.add(matrix[r2][j]);
          for (int i = r2 - 1; i >= r1 + 1 && ans.size() < m * n; --i)
            ans.add(matrix[i][c1]);
          ++r1;
          ++c1;
          --r2;
          --c2;
        }

        return ans;
    }
}
```

---