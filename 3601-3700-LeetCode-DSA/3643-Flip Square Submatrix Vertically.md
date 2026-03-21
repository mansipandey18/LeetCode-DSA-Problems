# <u>3643. Flip Square Submatrix Vertically</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/flip-square-submatrix-vertically/

---

## 🧠 Intuition:
* 🔹 We are given a square submatrix of size k × k starting at position (x, y).
* 🔹 A vertical flip means reversing the order of rows inside this square.
* 🔹 The top row should swap with the bottom row, the second row with the second-last row, and so on.
* 🔹 Only rows inside the selected submatrix are affected; the rest of the grid remains unchanged.
* 🔹 Iterate through only the top half of the square (k / 2 rows).
* 🔹 For each row i in the top half:

    - Find its corresponding mirrored row: i2 = x + k - 1 - (i - x)
* 🔹 Swap every column element between row i and row i2.
* 🔹 Continue swapping until the middle of the square is reached.
* 🔹 This effectively reverses rows vertically within the submatrix.

---

## ⏱ Time Complexity

**O(k^2)**

* We process : 
    - `k/2` rows
    - `k` columns for each row
    
---

## 📦 Space Complexity

**O(1)**

* Swapping is done in-place using one temporary variable.

---

## 💻 Java Code

```java
class Solution {
    public int[][] reverseSubmatrix(int[][] grid, int x, int y, int k) {
        for (int i = x; i < x + k / 2; i++) {
            int i2 = x + k - 1 - (i - x);
            for (int j = y; j < y + k; j++) {
                int t = grid[i][j];
                grid[i][j] = grid[i2][j];
                grid[i2][j] = t;
            }
        }
        return grid;
    }
}
```

---