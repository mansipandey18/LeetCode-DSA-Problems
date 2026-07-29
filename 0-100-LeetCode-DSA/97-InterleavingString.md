# <u>97. Interleaving String</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/interleaving-string/

---

## 🧠 Intuition:
* 🔹 Maintain two variables:
    - `first` → the smallest element seen so far.
    - `second` → the smallest element greater than `first`.

* 🔹 Traverse the array from left to right.

* 🔹 If the current number is smaller than or equal to `first`, update `first`.

* 🔹 Otherwise, if the current number is smaller than or equal to `second`, update `second`.

* 🔹 If the current number is greater than both `first` and `second`, then an increasing triplet (`first < second < current`) exists.

* 🔹 Return `true` immediately when such a triplet is found.

* 🔹 If the traversal ends without finding a valid third element, return `false`.


---

## ⏱ Time Complexity

**O(n)**

* The array is traversed only once.

---

## 📦 Space Complexity

**O(1)**

* Only two variables (`first` and `second`) are used regardless of the input size.

---

## 💻 Java Code

```java
class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        int m = s1.length(), n = s2.length();

        if (m + n != s3.length()) {
            return false;
        }

        boolean[] dp = new boolean[n + 1];
        dp[0] = true;

        for (int i = 0; i <= m; ++i) {
            for (int j = 0; j <= n; ++j) {

                int k = i + j - 1;

                if (i > 0) {
                    dp[j] &= s1.charAt(i - 1) == s3.charAt(k);
                }

                if (j > 0) {
                    dp[j] |= (dp[j - 1] & (s2.charAt(j - 1) == s3.charAt(k)));
                }
            }
        }

        return dp[n];

    }
}
```

---