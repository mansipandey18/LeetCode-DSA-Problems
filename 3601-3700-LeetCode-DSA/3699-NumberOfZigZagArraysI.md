# <u>3699. Number of ZigZag Arrays I</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/number-of-zigzag-arrays-i/

---

## 🧠 Intuition:
* 🔹 A ZigZag array alternates between increasing and decreasing relationships between adjacent elements.

* 🔹 Since only the relative difference between values matters, shift the range by making `l = 0` and work with values from `0` to `r - l`.

* 🔹 Use Dynamic Programming where `dp[v]` stores the number of valid ZigZag sequences ending with value `v` for the current length.

* 🔹 Initialize all values with `1` because an array of length `1` can end at any value in the range.

* 🔹 For each next position:
    - If the position requires an increasing relation, use prefix sums from left to right to count all smaller previous values.
    - If the position requires a decreasing relation, use prefix sums from right to left to count all larger previous values.

* 🔹 The `pre` variable maintains the running prefix/suffix sum, allowing transitions to be calculated efficiently without using an extra nested loop.

* 🔹 After building sequences of length `n`, sum all possible ending values to get the total count.

* 🔹 Multiply the final result by `2` because the ZigZag pattern can start with either an increasing step or a decreasing step.

* 🔹 Apply modulo `10^9 + 7` at each step to avoid integer overflow.

---

## ⏱ Time Complexity

**O(n × (r - l + 1))**

* We iterate through all possible values for each of the `n` positions.
    
---

## 📦 Space Complexity

**O(r - l + 1)**

* A single DP array is used to store counts for all possible values.

---

## 💻 Java Code

```java
class Solution {
    public int zigZagArrays(int n, int l, int r) {
        int MOD = 1_000_000_007;
        r -= l;
        int[] dp = new int[r + 1];
        Arrays.fill(dp, 1);
        for (int i = 1; i < n; i++) {
            int pre = 0, pre2;
            if ((i & 1) == 1) {
                for (int v = 0; v <= r; v++) {
                    pre2 = pre + dp[v];
                    dp[v] = pre;
                    pre = pre2 % MOD;
                }
            } else {
                for (int v = r; v >= 0; v--) {
                    pre2 = pre + dp[v];
                    dp[v] = pre;
                    pre = pre2 % MOD;
                }
            }
        }
        int res = 0;
        for (int v : dp)
            res = (res + v) % MOD;
        return res * 2 % MOD;
    }
}
```

---