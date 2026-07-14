# <u>3336. Find the Number of Subsequences With Equal GCD</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/find-the-number-of-subsequences-with-equal-gcd/

---

## 🧠 Intuition:
* 🔹 The goal is to count pairs of subsequences whose **GCD values are equal**.

* 🔹 Use **Dynamic Programming (DP)** where each state represents the current GCD of the two subsequences.

* 🔹 Define `dp[g1][g2]` as the number of ways to build two subsequences whose current GCDs are `g1` and `g2`.

* 🔹 Initially, both subsequences are empty, so start with `dp[0][0] = 1`.

* 🔹 For every element x in the array, consider **three possible choices:**
    - Skip `x`.
    - Add `x` to the first subsequence and update its GCD.
    - Add `x` to the second subsequence and update its GCD.

* 🔹 Whenever an element is added, compute the new GCD using:
    - `x` itself if the subsequence is empty (`g = 0`).
    - `gcd(currentGCD, x)` otherwise.

* 🔹 After processing all elements, look at all states where **both subsequences are non-empty and have the same GCD** `(g1 == g2 > 0)`.

* 🔹 Sum these valid states to get the final answer, taking modulo **10⁹ + 7**.

---

## ⏱ Time Complexity

**O(n × M² × log M)**

* Where:
    - `n` = number of elements
    - `M` = maximum value in nums
* each DP transition may compute a GCD in `O(log M)`  

---

## 📦 Space Complexity

**O(M²)**

---

## 💻 Java Code

```java
class Solution {
    public int subsequencePairCount(int[] nums) {
        int maxNum = Arrays.stream(nums).max().getAsInt();
        Integer[][][] mem = new Integer[nums.length][maxNum + 1][maxNum + 1];
        return subsequencePairCount(nums, 0, 0, 0, mem);
    }

    private static final int MOD = 1_000_000_007;

    private int subsequencePairCount(int[] nums, int i, int x, int y, Integer[][][] mem) {
        if (i == nums.length)
            return (x > 0 && x == y) ? 1 : 0;
        if (mem[i][x][y] != null)
            return mem[i][x][y];
        
        int skip = subsequencePairCount(nums, i + 1, x, y, mem);
        int take1 = subsequencePairCount(nums, i + 1, gcd(x, nums[i]), y, mem);
        int take2 = subsequencePairCount(nums, i + 1, x, gcd(y, nums[i]), mem);
        
        return mem[i][x][y] = (int) (((long) skip + take1 + take2) % MOD);
    }

    private int gcd(int a, int b) {
        return b == 0 ? a : gcd(b, a % b);
    }
}
```

---