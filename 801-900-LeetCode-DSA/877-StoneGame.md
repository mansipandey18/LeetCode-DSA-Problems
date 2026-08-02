# <u>877. Stone Game</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/stone-game/

---

## 🧠 Intuition:
* 🔹 Treat the game as a **two-player optimal strategy problem**, where both players always make the best possible move.

* 🔹 Instead of tracking the scores of Alice and Bob separately, calculate the **maximum score difference** the current player can achieve over the opponent.

* 🔹 Define `solve(left, right)` as:
    - The maximum score difference the current player can obtain from the subarray `piles[left...right]`.

* 🔹 At every turn, the current player has two choices:
    - **Pick the left pile** and let the opponent play on the remaining range.
    - **Pick the right pile** and let the opponent play on the remaining range.

* 🔹 Since the opponent also plays optimally, subtract the opponent's best score difference:
    - `leftAns = piles[left] - solve(left + 1, right)`
    - `rightAns = piles[right] - solve(left, right - 1)`

* 🔹 Choose the option that gives the **maximum score difference**.

* 🔹 Use **memoization (DP)** to store results for every `(left, right)` interval, avoiding repeated calculations.

* 🔹 If the final score difference is **positive**, the first player wins.

* 🔹 In this problem, however, the answer is **always** `true` because with an even number of piles and an odd total number of stones, Alice can always guarantee a win using an optimal strategy.

---

## ⏱ Time Complexity

**O(n²)**

* There are `n²` possible `(left, right)` states, and each state is computed only once.

    
---

## 📦 Space Complexity

**O(n²)**

* **O(n²)** – DP memoization table.
* **O(n)** – Recursion stack depth.

---

## 💻 Java Code

```java
class Solution {
    public boolean stoneGame(int[] piles) {
        Integer dp[][] = new Integer[piles.length][piles.length];

        // return solve(piles, 0, piles.length-1,dp) >0;
        return true;
    }

    public int solve(int[] nums, int left,int right, Integer[][] dp){

        if(left==right){
            return nums[left];
        }

        if(dp[left][right]!=null){
            return dp[left][right];
        }

        int leftAns = nums[left] - solve(nums, left+1,right, dp );
        int rightAns = nums[right] - solve(nums, left, right-1, dp);

        dp[left][right] = Math.max(leftAns, rightAns);

        return dp[left][right];
    }
}
```

---