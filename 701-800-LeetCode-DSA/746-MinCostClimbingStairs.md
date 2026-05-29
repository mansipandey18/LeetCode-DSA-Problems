# <u>746. Min Cost Climbing Stairs</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/min-cost-climbing-stairs/

---

## 🧠 Intuition:
* 🔹 At every stair, we have two choices:
    - Climb `1` step ahead.
    - Climb `2` steps ahead.

* 🔹 Use **DFS + Memoization (Top-Down DP)** to find the minimum cost from each index.

* 🔹 `dfs(i)` represents the minimum cost needed to reach the top starting from stair `i`.

* 🔹 From the current stair:
    - Pay `cost[i]`.
    - Then choose the cheaper option between `dfs(i+1)` and `dfs(i+2)`.

* 🔹 Base Case:
    - If the index goes beyond the last stair, no extra cost is needed, so return `0`.

* 🔹 Memoization stores already computed results in `memo[]` to avoid repeated calculations.

* 🔹 Since we can start from stair 0 or stair 1, take the minimum of:
    - `dfs(0)`
    - `dfs(1)`

* 🔹 This converts the recursive solution into an efficient Dynamic Programming approach.

---

## ⏱ Time Complexity

**O(n)**

* Each stair is computed only once due to memoization.
    
---

## 📦 Space Complexity

**O(n)**

* `O(n)` for memoization array + recursion stack.

---

## 💻 Java Code

```java
class Solution {
    private Integer[] memo;
    private int[] cost;

    public int minCostClimbingStairs(int[] cost) {
        this.cost = cost;
        this.memo = new Integer[cost.length];
      
        return Math.min(dfs(0), dfs(1));
    }

    private int dfs(int currentIndex) {
        if (currentIndex >= cost.length) {
            return 0;
        }
      
        if (memo[currentIndex] == null) {
            int oneStep = dfs(currentIndex + 1);
            int twoSteps = dfs(currentIndex + 2);
            memo[currentIndex] = cost[currentIndex] + Math.min(oneStep, twoSteps);
        }
      
        return memo[currentIndex];
    }
}
```

---