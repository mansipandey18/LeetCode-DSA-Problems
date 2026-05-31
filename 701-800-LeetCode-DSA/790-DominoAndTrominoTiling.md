# <u>790. Domino and Tromino Tiling</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/domino-and-tromino-tiling/

---

## 🧠 Intuition:
* 🔹 Use **Dynamic Programming with state compression** to track how the current column of the 2×n board is filled.

* 🔹 Represent each column's filling status using **4 states (0 to 3)**:
    - `0` → both cells filled.
    - `1` → top cell empty.
    - `2` → bottom cell empty.
    - `3` → both cells empty.

* 🔹 `dp[state]` stores the number of ways to tile the board up to the current column with that state.

* 🔹 For each new column, compute the next states (`newDp`) based on all possible placements of **dominoes** and **trominoes**.

* 🔹 Transition formulas combine ways from previous states to generate valid configurations for the next column.

* 🔹 Use modulo `10^9 + 7` to avoid integer overflow.

* 🔹 Since only the previous column's states are needed, keep just a **4-element DP array** instead of a full DP table.

* 🔹 After processing all `n` columns, `dp[0]` (fully filled state) contains the total number of valid tilings.

---

## ⏱ Time Complexity

**O(n)**

* iterate through all `n` columns, performing constant-time state transitions.

    
---

## 📦 Space Complexity

**O(1)**

* only two arrays of size 4 are used regardless of `n`.

---

## 💻 Java Code

```java
class Solution {
    public int numTilings(int n) {
        long[] dp = {1, 0, 0, 0};
      
        int mod = (int) 1e9 + 7;
      
        for (int i = 1; i <= n; ++i) {
            long[] newDp = new long[4];
          
            newDp[0] = (dp[0] + dp[1] + dp[2] + dp[3]) % mod;       
            newDp[1] = (dp[2] + dp[3]) % mod;
            newDp[2] = (dp[1] + dp[3]) % mod;          
            newDp[3] = dp[0];
          
            dp = newDp;
        }
      
        return (int) dp[0];
    }
}
```

---