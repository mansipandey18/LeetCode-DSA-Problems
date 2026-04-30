# <u>3742. Maximum Path Score in a Grid</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-path-score-in-a-grid/

---

## 🧠 Intuition:
* 🔹 We need to find the **maximum path score** from `(0,0)` to `(m-1,n-1)` while moving only **up or left (reverse thinking)** and using at most `k` special picks

* 🔹 Instead of starting from `(0,0)`, the solution works **backwards from destination** `(m-1,n-1)`, which simplifies recursion

* 🔹 At every cell `(i, j)`, we decide the best path coming either from:
    - top → `(i-1, j)`
    - left → `(i, j-1)`

* 🔹 Each cell contributes its value to the total score

* 🔹 If the current cell value is **positive**, we must “spend” one of the `k` allowed operations → so reduce `k`

* 🔹 If `k` becomes negative, this path is invalid → return a very small value (`-inf`) to discard it

* 🔹 Base case:
    - When we reach `(0,0)`, return `0` because we don't add it again (already handled in recursion flow)

* 🔹 Use **memoization (3D DP)**:
    - `f[i][j][k]` stores the maximum score reachable at cell `(i,j)` with `k` operations left

* 🔹 For each state:
    - Compute best score from top and left recursively
    - Take the maximum of both and add current cell value

* 🔹 Store result in DP table to avoid recomputation

* 🔹 Finally, if result is negative (invalid path), return `-1`, else return computed score

* 🔹 This transforms an exponential recursion into an efficient DP solution
---

## ⏱ Time Complexity

**O(m * n * k)**

* States = `m × n × k`
* Each state computes constant work (2 recursive calls)
    
---

## 📦 Space Complexity

**O(m * n * k)**

* DP table of size `m × n × k`
* Recursion stack up to `O(m + n)`

---

## 💻 Java Code

```java
class Solution {
    private int[][] grid;
    private Integer[][][] f;
    private final int inf = 1 << 30;

    public int maxPathScore(int[][] grid, int k) {
        this.grid = grid;
        int m = grid.length;
        int n = grid[0].length;
        f = new Integer[m][n][k + 1];
        int ans = dfs(m - 1, n - 1, k);
        return ans < 0 ? -1 : ans;
    }

    private int dfs(int i, int j, int k) {
        if (i < 0 || j < 0 || k < 0) {
            return -inf;
        }
        if (i == 0 && j == 0) {
            return 0;
        }
        if (f[i][j][k] != null) {
            return f[i][j][k];
        }
        int res = grid[i][j];
        int nk = k;
        if (grid[i][j] > 0) {
            --nk;
        }
        int a = dfs(i - 1, j, nk);
        int b = dfs(i, j - 1, nk);
        res += Math.max(a, b);
        f[i][j][k] = res;
        return res;
    }
}
```

---