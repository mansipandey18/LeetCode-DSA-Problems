# <u>322. Coin Change</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/coin-change/

---

## 🧠 Intuition:
* 🔹 Use **Dynamic Programming (Bottom-Up)** where `dp[i]` represents the **minimum number of coins** needed to make amount `i`.

* 🔹 Initialize the `dp` array with a large value (`amount + 1`) to represent an unreachable state.

* 🔹 Set `dp[0] = 0` because **0 coins are needed to make amount 0**.

* 🔹 Process every amount from `1` to `amount`.

* 🔹 For each amount, try using every available coin:
    - If the coin can contribute to the current amount `(i - coin >= 0)`, update:
        * `dp[i] = min(dp[i], dp[i - coin] + 1)`

* 🔹 This transition means:
    - If we already know the minimum coins needed for `i - coin`, then adding the current coin gives a possible solution for `i`.

* 🔹 Continue filling the DP table until all amounts are processed.

* 🔹 If `dp[amount]` is still greater than `amount`, it means the target amount cannot be formed, so return -1; otherwise, return `dp[amount]`.

---

## ⏱ Time Complexity

**O(amount × number_of_coins)**

* For every amount, we iterate through all the coins.

---

## 📦 Space Complexity

**O(amount)**

* A one-dimensional DP array of size `amount + 1` is used.

---

## 💻 Java Code

```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        int[] dp = new int[amount + 1];
        java.util.Arrays.fill(dp, amount + 1);
        dp[0] = 0; // Base case

        for (int i = 1; i <= amount; i++) {
            for (int coin : coins) {
                if (i - coin >= 0) {
                    dp[i] = Math.min(dp[i], dp[i - coin] + 1);
                }
            }
        }
        return dp[amount] > amount ? -1 : dp[amount];
    }
}
```

---