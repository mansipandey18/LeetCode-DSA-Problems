# <u>115. Distinct Subsequences</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/distinct-subsequences/
---

## 🧠 Intuition:
* 🔹 Use **1D DP** where `dp[j]` represents the number of ways to form the first `j` characters of `t` using the characters processed from `s`.

* 🔹 Initialize `dp[0] = 1` because there is exactly **one way to form an empty subsequence**.

* 🔹 Traverse each character of `s` one by one.

* 🔹 For every character, traverse `t` **backward** from `targetLength` to `1`.

* 🔹 If `sourceChar == targetChar`, update:
    - `dp[j] += dp[j - 1]`

* 🔹 Traversing backward is important because it prevents the current character of `s` from being used multiple times in the same iteration.

* 🔹 After processing all characters of `s`, `dp[targetLength]` contains the **total number of distinct subsequences of `s` equal to `t`**.

---

## ⏱ Time Complexity

**O(n * m)**

* Where:
    - `m = s.length()`
    - `n = t.length()`
* Outer loop over `s` → `O(m)`
* Inner loop over `t` → `O(n)`

---

## 📦 Space Complexity

**O(n)**

* Only a 1D `dp` array of size `n + 1` is used.

---

## 💻 Java Code

```java
class Solution {
    public int numDistinct(String s, String t) {
        int targetLength = t.length();
        int[] dp = new int[targetLength + 1];

        dp[0] = 1;

        for (char sourceChar : s.toCharArray()) {
            
            for (int j = targetLength; j > 0; --j) {
                
                char targetChar = t.charAt(j - 1);
              
                if (sourceChar == targetChar) {
                    dp[j] += dp[j - 1];
                }
            }
        }

        return dp[targetLength];
    }
}
```

---