# <u>3756. Concatenate Non-Zero Digits and Multiply by Sum II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/concatenate-non-zero-digits-and-multiply-by-sum-ii/

---

## 🧠 Intuition:
* 🔹 Since there are **multiple range queries**, recomputing the answer for each substring would be too slow, so preprocess useful information using **prefix arrays**.

* 🔹 Build a **prefix sum array** to quickly calculate the sum of digits for any query range.

* 🔹 Build a **prefix count array** to track how many **non-zero digits** have appeared up to each position.

* 🔹 Build a **prefix concatenation value array**, where each non-zero digit extends the previously formed number using the relation: `newValue = previousValue × 10 + digit`.

* 🔹 Precompute **powers of 10 modulo MOD** so that the concatenated value of any substring can be extracted efficiently.

* 🔹 For each query:
    - Find the **sum of digits** using the prefix sum array.
    - Find the **number of non-zero digits** in the range.
    - If there are no non-zero digits, the answer is `0`.
    - Otherwise, use the prefix concatenation values and powers of 10 to isolate the concatenated non-zero number of the current substring.
    - Multiply the extracted concatenated value with the digit sum and take the result modulo `10^9 + 7`.

* 🔹 This preprocessing allows every query to be answered in **constant time** after the initial setup.

---

## ⏱ Time Complexity

**O(n + q)**

* `O(n)` for preprocessing

* `O(1)` for each of the q queries.

---

## 📦 Space Complexity

**O(n)**

* Prefix arrays and powers of 10 require linear extra space.

---

## 💻 Java Code

```java
class Solution {
    private static final int MOD = 1000000007;

    public int[] sumAndMultiply(String s, int[][] queries) {
        int m = s.length();
        int q = queries.length;

        long[] pow10 = new long[m + 1];
        pow10[0] = 1;
        for (int i = 1; i <= m; i++) {
            pow10[i] = (pow10[i - 1] * 10) % MOD;
        }

        int[] sumD = new int[m + 1];  // sum of digits
        int[] cntN0 = new int[m + 1]; // count of non-zero digits
        long[] p = new long[m + 1];   // value of concatenated non-zero digits

        for (int i = 0; i < m; i++) {
            int digit = s.charAt(i) - '0';
            
            sumD[i + 1] = sumD[i] + digit;
            cntN0[i + 1] = cntN0[i];
            p[i + 1] = p[i];

            if (digit > 0) {
                cntN0[i + 1]++;
                p[i + 1] = (p[i] * 10 + digit) % MOD;
            }
        }

        int[] answer = new int[q];
        for (int i = 0; i < q; i++) {
            int l = queries[i][0];
            int r = queries[i][1];

            int n0 = cntN0[r + 1] - cntN0[l];
            
            if (n0 == 0) {
                answer[i] = 0;
                continue;
            }

            long sum = sumD[r + 1] - sumD[l];

            long x = (p[r + 1] - (p[l] * pow10[n0]) % MOD + MOD) % MOD;

            answer[i] = (int) ((x * sum) % MOD);
        }

        return answer;
    }
}
```

---