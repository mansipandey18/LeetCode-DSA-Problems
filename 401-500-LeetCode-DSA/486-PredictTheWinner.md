# <u>486. Predict the Winner</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/predict-the-winner/

---

## 🧠 Intuition:
* 🔹 Treat the problem as a **two-player optimal game**, where both players always make the best possible move.

* 🔹 Instead of tracking each player's score separately, calculate the **maximum score difference** the current player can achieve over the opponent.

* 🔹 Define the DP state `dfs(left, right)` as:
    - The maximum score difference the current player can obtain from the subarray `nums[left...right]`.

* 🔹 At every turn, the current player has two choices:
    - **Pick the leftmost number** and let the opponent play on the remaining range.
    - **Pick the rightmost number** and let the opponent play on the remaining range.

* 🔹 Since the opponent also plays optimally, subtract the opponent's best score difference from the chosen value:
    - `chooseLeft = nums[left] - dfs(left + 1, right)`
    - `chooseRight = nums[right] - dfs(left, right - 1)`

* 🔹 Choose the option that gives the **maximum score difference**.

* 🔹 Use **memoization** to store results for each `(left, right)` interval, avoiding repeated calculations.

* 🔹 If the final score difference `dfs(0, n - 1)` is **greater than or equal to 0**, Player 1 can win (or tie), so return `true`.

---

## ⏱ Time Complexity

**O(n²)**

* There are `n²` possible `(left, right)` states, and each state is computed only once.
    
---

## 📦 Space Complexity

**O(n²)**

* For the DP memoization table.

---

## 💻 Java Code

```java
class Solution {
    private int[] nums;
    private int[][] dp;

    public boolean predictTheWinner(int[] nums) {
        this.nums = nums;
        int n = nums.length;
        dp = new int[n][n];
      
        return dfs(0, n - 1) >= 0;
    }

    private int dfs(int left, int right) {
        if (left > right) {
            return 0;
        }
      
        if (dp[left][right] != 0) {
            return dp[left][right];
        }
      
        int chooseLeft = nums[left] - dfs(left + 1, right);
        int chooseRight = nums[right] - dfs(left, right - 1);
      
        dp[left][right] = Math.max(chooseLeft, chooseRight);
        return dp[left][right];
    }

}   
```

---