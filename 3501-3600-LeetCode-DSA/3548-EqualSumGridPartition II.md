# <u>3548. Equal Sum Grid Partition II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/equal-sum-grid-partition-ii/

---

## 🧠 Intuition:
* 🔹 The goal is to check whether the grid can be divided into two parts having equal sum.

* 🔹 Partition can be:
    - Horizontal cut (between rows), or
    - Vertical cut (between columns).

* 🔹 Instead of writing separate logic for both directions:
    - First check normally (horizontal cuts).
    - Then rotate the grid and reuse the same logic to simulate vertical cuts.

* 🔹 Compute total sum of the grid and store frequencies of all elements in `cnt2` (right/bottom part).

* 🔹 Maintain two running sums:
    - `s1` → sum of first partition (top part).
    - `s2` → sum of remaining partition (bottom part).

* 🔹 Move row by row:
    - Transfer elements from bottom part → top part.
    - Update sums and frequency maps.

* 🔹 After each possible cut:
    - If `s1 == s2`, partition is valid ✅.

* 🔹 If sums are unequal:
    - Calculate difference diff = |s1 − s2|.
    - Check if removing one element from the larger side can balance sums.

* 🔹 Use hash maps (cnt1, cnt2) to quickly check if such an element exists.

* 🔹 Extra boundary checks ensure both partitions remain valid grids.

* 🔹 If horizontal check fails, rotate matrix and repeat for vertical partition.

* 🔹 If any case works → return true, otherwise false.

---

## ⏱ Time Complexity

**O(m * n)**

* Let:
    - `m` = number of rows
    - `n` = number of columns

* **1️⃣ Building sums & frequency map**
    - Traverse entire grid once → O(m × n)

* **2️⃣ Checking partitions**
    - Each element processed once while moving rows → O(m × n)

* **3️⃣ Rotation of grid**
    - Matrix transpose → O(m × n)

* **4️⃣ Second check after rotation**
    - Again → O(m × n)
    
---

## 📦 Space Complexity

**O(m * n)**

* Extra structures used:
    - Two HashMaps storing frequencies → O(m × n)
    - Rotated grid → O(m × n)

---

## 💻 Java Code

```java
class Solution {
    public boolean canPartitionGrid(int[][] grid) {
        return check(grid) || check(rotate(grid));
    }

     private boolean check(int[][] g) {
        int m = g.length, n = g[0].length;
        long s1 = 0, s2 = 0;

        Map<Long, Integer> cnt1 = new HashMap<>();
        Map<Long, Integer> cnt2 = new HashMap<>();

        for (int[] row : g) {
            for (int x : row) {
                s2 += x;
                cnt2.merge((long) x, 1, Integer::sum);
            }
        }

        for (int i = 0; i < m - 1; i++) {
            for (int x : g[i]) {
                s1 += x;
                s2 -= x;

                cnt1.merge((long) x, 1, Integer::sum);
                cnt2.merge((long) x, -1, Integer::sum);
            }

            if (s1 == s2) {
                return true;
            }

            if (s1 < s2) {
                long diff = s2 - s1;
                if (cnt2.getOrDefault(diff, 0) > 0) {
                    if ((m - i - 1 > 1 && n > 1)
                        || (i == m - 2 && (g[i + 1][0] == diff || g[i + 1][n - 1] == diff))
                        || (n == 1 && (g[i + 1][0] == diff || g[m - 1][0] == diff))) {
                        return true;
                    }
                }
            } else {
                long diff = s1 - s2;
                if (cnt1.getOrDefault(diff, 0) > 0) {
                    if ((i + 1 > 1 && n > 1) || (i == 0 && (g[0][0] == diff || g[0][n - 1] == diff))
                        || (n == 1 && (g[0][0] == diff || g[i][0] == diff))) {
                        return true;
                    }
                }
            }
        }

        return false;
    }

    private int[][] rotate(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        int[][] t = new int[n][m];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                t[j][i] = grid[i][j];
            }
        }
        return t;
    }
}
```

---