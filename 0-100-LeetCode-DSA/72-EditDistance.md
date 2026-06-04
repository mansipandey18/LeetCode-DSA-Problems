# <u>72. Edit Distance</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/edit-distance/

---

## 🧠 Intuition:
* 🔹 We solve the problem using **recursion + memoization (top-down DP)**.

* 🔹 Define `helper(ind1, ind2)` as the **minimum operations needed to convert** `word1[0..ind1]` into `word2[0..ind2]`.

* 🔹 If either string is exhausted:
    - If `ind1 < 0`, we need to **insert remaining characters of word2** → `ind2 + 1`.
    - If `ind2 < 0`, we need to **delete remaining characters of word1** → `ind1 + 1`.

* 🔹 If characters match (`s1[ind1] == s2[ind2]`):
    - No operation needed → move diagonally (`ind1-1, ind2-1`).

* 🔹 If characters do not match, we consider 3 operations:
    - **Insert** → move `ind2 - 1`
    - **Delete** → move `ind1 - 1`
    - **Replace** → move both `ind1 - 1, ind2 - 1`

* 🔹 Take the **minimum of all three operations + 1** (for the current operation).

* 🔹 Memoization (`dp[ind1][ind2]`) ensures each subproblem is solved only once.

* 🔹 Final answer is `helper(n-1, m-1)` which gives minimum edits for full strings.

---

## ⏱ Time Complexity

**O(n * m)**

* There are `n × m` unique states in DP.
* Each state is computed once with `O(1)` work.

---

## 📦 Space Complexity

**O(n * m)**

* DP table of size `n × m` → `O(n × m)`
* Recursion stack in worst case → `O(n + m)`

---

## 💻 Java Code

```java
class Solution {
    public int minDistance(String word1, String word2) {
        int n =  word1.length();
        int m = word2.length();
        int [][]dp = new int [n][m];
        for(int row[] : dp){
           Arrays.fill(row,-1);
        }
        return helper(n-1,m-1,word1,word2,dp);

    }

    int helper(int ind1,int ind2,String s1, String s2,int [][]dp){
        if(ind1<0) return ind2+1;
        if(ind2<0) return ind1+1;

        if(dp[ind1][ind2] != -1 ) return dp[ind1][ind2];

        if(s1.charAt(ind1) == s2.charAt(ind2))
            return dp[ind1][ind2] = 0+helper(ind1-1,ind2-1,s1,s2,dp);

        int insertOp = helper(ind1, ind2 - 1, s1, s2, dp);
        int deleteOp = helper(ind1 - 1, ind2, s1, s2, dp);
        int replaceOp = helper(ind1 - 1, ind2 - 1, s1, s2, dp);
        return dp[ind1][ind2] = 1 + Math.min(insertOp, Math.min(deleteOp, replaceOp));
    }
}
```

---
