# <u>940. Distinct Subsequences II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/distinct-subsequences-ii/

---

## 🧠 Intuition:
* 🔹 Use a `dp[26]` array where `dp[i]` stores the number of **distinct subsequences ending with the character** corresponding to index `i`.

* 🔹 Traverse the string character by character.

* 🔹 For the current character:
    - Calculate `sum(dp)` to get the number of all distinct subsequences formed so far.
    - Add `1` to represent the subsequence containing **only the current character**.
    - Store this value in `dp[charIndex]`.

* 🔹 If the same character appears again, its previous value is **replaced**, which removes duplicate subsequences ending with that character.

* 🔹 The `sum(dp)` after processing the entire string gives the total number of **distinct non-empty subsequences**.

* 🔹 Every sum is taken modulo `10^9 + 7` to prevent integer overflow.

---

## ⏱ Time Complexity

**O(n)**

* Where:
    - `n = s.length()`
* For each character, sum(dp) scans 26 elements. Since 26 is constant.
    
---

## 📦 Space Complexity

**O(1)**

* `dp` contains only 26 elements.

---

## 💻 Java Code

```java
class Solution {
    private static final int MOD = (int) 1e9 + 7;

    public int distinctSubseqII(String s) {
        int[] dp = new int[26];
      
        for (int i = 0; i < s.length(); ++i) {
            int charIndex = s.charAt(i) - 'a';
          
            dp[charIndex] = sum(dp) + 1;
        }
      
        return sum(dp);
    }

    private int sum(int[] arr) {
        int total = 0;
      
        for (int value : arr) {
            total = (total + value) % MOD;
        }
      
        return total;
    
    }
}
```

---