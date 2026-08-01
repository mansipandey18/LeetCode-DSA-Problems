# <u>188. Best Time to Buy and Sell Stock IV</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/

---

## 🧠 Intuition:
* 🔹 At every day, we have three pieces of information that define our state:
    - Current day.
    - Number of transactions remaining.
    - Whether we are currently holding a stock or not.

* 🔹 Use **DFS + Memoization (Top-Down Dynamic Programming)** to avoid solving the same state multiple times.

* 🔹 For each state, there are two possible choices:
    - **Skip the current day** and move to the next day without changing the current state.
    - **Take an action** based on the current holding status:
        * If **not holding** a stock and transactions are available, buy the stock (spend money and reduce the remaining transaction count).
        * If **holding** a stock, sell it (earn money and switch back to the non-holding state).

* 🔹 Compute the maximum profit between skipping and taking the valid action.

* 🔹 Store the result for each `(day, transactionsLeft, holdingState)` in the DP table so that repeated states are reused instead of recomputed.

* 🔹 The answer is the maximum profit starting from **day 0**, with **k transactions available**, and **not holding any stock**.


---

## ⏱ Time Complexity

**O(nk)**

* There are `n` days, `k + 1` transaction states, and `2` holding states.
* Each state is computed only once.
---

## 📦 Space Complexity

**O(nk)**

* DP memoization table stores `n × (k + 1) × 2` states.
* The recursion stack can take up to **O(n)** in the worst case.
* Overall auxiliary space: **O(nk)**.

---

## 💻 Java Code

```java
class Solution {
    private Integer[][][] dp;
    private int[] prices;
    private int n;

    public int maxProfit(int k, int[] prices) {
        n = prices.length;
        this.prices = prices;
        
        dp = new Integer[n][k + 1][2];
      
        return dfs(0, k, 0);
    }

    private int dfs(int day, int transactionsLeft, int isHolding) {
        if (day >= n) {
            return 0;
        }
      
        if (dp[day][transactionsLeft][isHolding] != null) {
            return dp[day][transactionsLeft][isHolding];
        }
      
        int maxProfit = dfs(day + 1, transactionsLeft, isHolding);
      
        if (isHolding == 1) {
            maxProfit = Math.max(maxProfit, 
                                prices[day] + dfs(day + 1, transactionsLeft, 0));
        } else if (transactionsLeft > 0) {
            maxProfit = Math.max(maxProfit, 
                                -prices[day] + dfs(day + 1, transactionsLeft - 1, 1));
        }
      
        return dp[day][transactionsLeft][isHolding] = maxProfit;
    }
}
```

---