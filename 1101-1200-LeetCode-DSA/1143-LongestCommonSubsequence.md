# <u>1143. Longest Common Subsequence</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/longest-common-subsequence/

---

## 🧠 Intuition:
* 🔹 We need to find the **longest subsequence** that appears in both strings while maintaining the relative order of characters.

* 🔹 Use **Dynamic Programming (DP)** where `dp[i][j]` represents the length of the LCS between:
    - First `i` characters of `text1`
    - First `j` characters of `text2`

* 🔹 If the current characters match:
    - `text1.charAt(i-1) == text2.charAt(j-1)`
    - Include this character in the LCS.
    - `dp[i][j] = dp[i-1][j-1] + 1`

* 🔹 If the characters do not match:
    - Skip one character from either string.
    - Take the better result:
    - `dp[i][j] = max(dp[i-1][j], dp[i][j-1])`

* 🔹 Fill the DP table row by row until all character pairs are processed.

* 🔹 The value at `dp[length1][length2]` gives the length of the **Longest Common Subsequence**.

---

## ⏱ Time Complexity

**O(m * n)**

* every pair of characters from both strings is processed once.
    
---

## 📦 Space Complexity

**O(m * n)**

* DP table of size `(length1 + 1) × (length2 + 1)` is used.

---

## 💻 Java Code

```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        int length1 = text1.length();
        int length2 = text2.length();
      
        int[][] dp = new int[length1 + 1][length2 + 1];
      
        for (int i = 1; i <= length1; i++) {
            for (int j = 1; j <= length2; j++) {
                if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }
      
        return dp[length1][length2];
    }
}
```

---