# <u>3225. Maximum Score From Grid Operations</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-score-from-grid-operations/

---

## 🧠 Intuition:
* 🔹 The goal is to maximize the score by selecting cells column by column while maintaining the valid operation rules between adjacent columns

* 🔹 Instead of thinking about every individual cell, we focus on the **bottommost selected row** in each column because that completely determines the chosen prefix of that column

* 🔹 If the bottommost selected row is `k`, it means rows `0 to k-1` are selected in that column

* 🔹 To quickly calculate the sum of selected cells in any column range, we precompute **prefix sums** for every column

* 🔹 `prefix[j][i]` stores the sum of the first `i` cells in column `j`, allowing range sum calculation in **O(1)**

* 🔹 Use Dynamic Programming with two states:
    - `prevPick[i]` → maximum score up to previous column when previous column contributes directly to current transitions
    - `prevSkip[i]` → maximum score when we rely on the column before previous for transition handling

* 🔹 For every new column, try all possible values of:
    - `prev` = bottommost selected row in previous column
    - `curr` = bottommost selected row in current column

* 🔹 **Two cases arise:**

* ### Case 1: `curr > prev`
    - Current column goes deeper than previous column
    - Extra contribution comes from the previous column
    - Add score of rows `[prev ... curr-1]` from previous column using prefix sums

* ### Case 2: `prev >= curr`
    - Previous column goes deeper than current column
    - Extra contribution comes from the current column
    - Add score of rows `[curr ... prev-1]` from current column
    - For both cases, update the best possible DP values using maximum transitions
    - After processing all columns, the maximum value in the final DP array is the answer
    - This avoids brute force over all subsets and reduces the problem to manageable DP over column boundaries.

---

## ⏱ Time Complexity

**O(n^3)**

* Prefix sum computation → **O(n^2)**
* For each column (`n` columns), we try all (`curr, prev`) pairs → **O(n^2)** per column

---

## 📦 Space Complexity

**O(n^2)**

* Prefix sum array → **O(n^2)**
* DP arrays (`prevPick`, `prevSkip`, `currPick`, `currSkip`) → **O(n)**

---

## 💻 Java Code

```java
class Solution {
    public long maximumScore(int[][] grid) {
        final int n = grid.length;
        // prefix[j][i] := the sum of the first i elements in the j-th column
        long[][] prefix = new long[n][n + 1];
        // prevPick[i] := the maximum achievable score up to the previous column,
        // where the bottommost selected element in that column is in row (i - 1)
        long[] prevPick = new long[n + 1];
        // prevSkip[i] := the maximum achievable score up to the previous column,
        // where the bottommost selected element in the column before the previous
        // one is in row (i - 1)
        long[] prevSkip = new long[n + 1];

        for (int j = 0; j < n; ++j)
            for (int i = 0; i < n; ++i)
                prefix[j][i + 1] = prefix[j][i] + grid[i][j];

        for (int j = 1; j < n; ++j) {
            long[] currPick = new long[n + 1];
            long[] currSkip = new long[n + 1];
            // Consider all possible combinations of the number of current and
            // previous selected elements.
            for (int curr = 0; curr <= n; ++curr)
                for (int prev = 0; prev <= n; ++prev)
                    if (curr > prev) {
                        // 1. The current bottom is deeper than the previous bottom.
                        // Get the score of grid[prev..curr)[j - 1] for pick and skip.
                        final long score = prefix[j - 1][curr] - prefix[j - 1][prev];
                        currPick[curr] = Math.max(currPick[curr], prevSkip[prev] + score);
                        currSkip[curr] = Math.max(currSkip[curr], prevSkip[prev] + score);
                    } else {
                        // 2. The previous bottom is deeper than the current bottom.
                        // Get the score of grid[curr..prev)[j] for pick only.
                        final long score = prefix[j][prev] - prefix[j][curr];
                        currPick[curr] = Math.max(currPick[curr], prevPick[prev] + score);
                        currSkip[curr] = Math.max(currSkip[curr], prevPick[prev]);
                    }
            prevPick = currPick;
            prevSkip = currSkip;
        }

        return Arrays.stream(prevPick).max().getAsLong();

    }
}
```

---