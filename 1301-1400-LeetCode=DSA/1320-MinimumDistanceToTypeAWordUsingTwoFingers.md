# <u>1320. Minimum Distance to Type a Word Using Two Fingers
</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/minimum-distance-to-type-a-word-using-two-fingers/
---

## 🧠 Intuition:
* 🔹 The problem is about typing a word using **two fingers** on a keyboard while minimizing total movement distance.

* 🔹 Each character is mapped to a position on a **6-column grid**, and distance is **Manhattan distance**.

* 🔹 Use **Dynamic Programming (DP)** to track the optimal cost:
    - `dp[i][j][k]` = minimum distance to type first `i+1` characters with **left finger at** `j` and **right finger at** `k`.

* 🔹 Initialization:
    - For the first character, either finger can type it with **0 cost**.
    - The other finger can be assumed at any position.

* 🔹 For each next character:
    - Let `prevChar` = previous character, `currChar` = current character.

* 🔹 Two choices at each step:
    - **1. Move the same finger** that typed the previous character:
        * Add distance from `prevChar → currChar`.
    - **2. Use the other finger**:
        * Move the idle finger from its current position to `currChar`.
        * The previous finger stays in place.

* 🔹 Take the **minimum cost** among all possibilities.

* 🔹 After processing all characters:
        - The answer is the **minimum cost where one finger is on the last character**.

* 🔹 This ensures we always pick the most optimal finger movement combination.


---

## ⏱ Time Complexity

**O(n)**

* Let : 
    - `n` = length of the word.

* DP states: `n × 26 × 26`

* For each state, transitions may involve looping over 26 characters.
    
---

## 📦 Space Complexity

**O(n)**

* DP array size: `n × 26 × 26`

---

## 💻 Java Code

```java
class Solution {
    public int minimumDistance(String word) {
        int n = word.length();
        final int INF = 1 << 30;
      
        int[][][] dp = new int[n][26][26];
      
        for (int[][] row : dp) {
            for (int[] cell : row) {
                Arrays.fill(cell, INF);
            }
        }
      
        int firstChar = word.charAt(0) - 'A';
        for (int j = 0; j < 26; ++j) {
            dp[0][firstChar][j] = 0;  // Left finger types first char, right at position j
            dp[0][j][firstChar] = 0;  // Right finger types first char, left at position j
        }
      
        for (int i = 1; i < n; ++i) {
            int prevChar = word.charAt(i - 1) - 'A';
            int currChar = word.charAt(i) - 'A';
            int distance = dist(prevChar, currChar);
          
            for (int j = 0; j < 26; ++j) {
                dp[i][currChar][j] = Math.min(dp[i][currChar][j], dp[i - 1][prevChar][j] + distance);

                dp[i][j][currChar] = Math.min(dp[i][j][currChar], dp[i - 1][j][prevChar] + distance);
              
                if (j == prevChar) {
                    for (int k = 0; k < 26; ++k) {
                        int moveDistance = dist(k, currChar);

                        dp[i][currChar][j] = Math.min(dp[i][currChar][j], dp[i - 1][k][prevChar] + moveDistance);
                        
                        dp[i][j][currChar] = Math.min(dp[i][j][currChar], dp[i - 1][prevChar][k] + moveDistance);
                    }
                }
            }
        }
      
        int result = INF;
        int lastChar = word.charAt(n - 1) - 'A';
        for (int j = 0; j < 26; ++j) {
            result = Math.min(result, dp[n - 1][j][lastChar]);  // Right finger on last char
            result = Math.min(result, dp[n - 1][lastChar][j]);  // Left finger on last char
        }
      
        return result;
    }

    private int dist(int a, int b) {
        int row1 = a / 6, col1 = a % 6;
        int row2 = b / 6, col2 = b % 6;
        return Math.abs(row1 - row2) + Math.abs(col1 - col2);
    }
}
```

---