# <u>1872. Stone Game VIII</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/stone-game-viii/

---

## 🧠 Intuition:
* 🔹 First, convert `stones` into a **prefix-sum array**, where `prefixSum[i]` represents the total value of stones from index `0` to `i`.

* 🔹 The game effectively becomes a choice of taking a prefix sum starting from index `1`.

* 🔹 `dfs(currentIndex)` represents the **maximum score difference/current best result** that can be achieved from the current prefix-sum position.

* 🔹 At every index, there are two choices:
    - **Skip the current prefix:** move to `currentIndex + 1`.
    - **Take the current prefix:** gain `prefixSum[currentIndex]`, while the opponent gets the result of the remaining game, giving `prefixSum[currentIndex] - dfs(currentIndex + 1)`.

* 🔹 Take the maximum of these two choices because both players play optimally.

* 🔹 When `currentIndex >= n - 1`, no further meaningful choice remains, so the current prefix sum becomes the result.

* 🔹 Memoization stores the result for each `currentIndex`, avoiding repeated recursive calculations.

* 🔹 Finally, `dfs(1)` gives the optimal result for the game.

---

## ⏱ Time Complexity

**O(n)**

* The prefix-sum construction takes `O(n)`.
* Each `dfs()` state is calculated only once due to memoization.
* There are at most `n` states, and each state performs constant work.

---

## 📦 Space Complexity

**O(n)**

* `memo` array uses `O(n)` space.
* `prefixSum` references the modified `stones` array, so no additional prefix-sum array is created.
* Recursive call stack can reach `O(n)` depth.

---

## 💻 Java Code

```java
class Solution {
    private Integer[] memo;
    private int[] prefixSum;
    private int n;

    public int stoneGameVIII(int[] stones) {
        n = stones.length;
      
        memo = new Integer[n];
      
        for (int i = 1; i < n; i++) {
            stones[i] += stones[i - 1];
        }
      
        prefixSum = stones;
      
        return dfs(1);
    }

    private int dfs(int currentIndex) {
        if (currentIndex >= n - 1) {
            return prefixSum[currentIndex];
        }
      
        if (memo[currentIndex] == null) {          
            int skipCurrent = dfs(currentIndex + 1);          
            int takeCurrent = prefixSum[currentIndex] - dfs(currentIndex + 1);
          
            memo[currentIndex] = Math.max(skipCurrent, takeCurrent);
        }
      
        return memo[currentIndex];
    }
}
```

---