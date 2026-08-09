# <u>1140. Stone Game II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/stone-game-ii/

---

## 🧠 Intuition:
* 🔹 Tribonacci sequence follows:
    - `T0 = 0`
    - `T1 = 1`
    - `T2 = 1`
    - `Tn = T(n-1) + T(n-2) + T(n-3)`

* 🔹 Instead of using recursion or DP array, keep track of only the last three numbers.

* 🔹 Initialize:
    - `first = 0`
    - `second = 1`
    - `third = 1`

* 🔹 In each iteration:
    - Compute the next Tribonacci number using the sum of previous three values.
    - Shift the variables forward:
        * `first = second`
        * `second = third`
        * `third = next`

* 🔹 Repeat this process `n` times.

* 🔹 After all updates, `first` holds the required `n-th` Tribonacci number.

* 🔹 This approach avoids recursion overhead and optimizes space usage.

---

## ⏱ Time Complexity

**O(n³)**

* There are **O(n²)** possible `(index, M)` states.
* For each state, we may try up to **O(n)** choices of `X`.
* Each transition uses prefix sums in **O(1)**.
    
---

## 📦 Space Complexity

**O(n²)**

* **O(n²)** for the `dp` memoization table.
* **O(n) **for the `prefixSum` array.
* Recursion stack can use **O(n)** space.

---

## 💻 Java Code

```java
class Solution {
    private int[] prefixSum;
    private Integer[][] dp;
    private int n; 

    public int stoneGameII(int[] piles) {
        n = piles.length;
      
        prefixSum = new int[n + 1];
        for (int i = 0; i < n; i++) {
            prefixSum[i + 1] = prefixSum[i] + piles[i];
        }
      
        dp = new Integer[n][n + 1];
      
        return dfs(0, 1);
    }

    
    private int dfs(int index, int M) {
        if (2 * M >= n - index) {
            return prefixSum[n] - prefixSum[index];
        }
      
        if (dp[index][M] != null) {
            return dp[index][M];
        }
      
        int maxStones = 0;
      
        for (int X = 1; X <= 2 * M; X++) {
           int currentPlayerStones = prefixSum[n] - prefixSum[index] - dfs(index + X, Math.max(M, X));
            maxStones = Math.max(maxStones, currentPlayerStones);
        }
      
        dp[index][M] = maxStones;
        return maxStones;
    
    }
}
```

---