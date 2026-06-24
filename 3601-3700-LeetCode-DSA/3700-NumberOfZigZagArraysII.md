# <u>3700. Number of ZigZag Arrays II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/number-of-zigzag-arrays-ii/

---

## 🧠 Intuition:
* 🔹 We treat each possible value in the range **[l, r]** as a state and build transition matrices to represent valid zigzag moves.

* 🔹 `m1` stores transitions where the next value must be **greater** than the current value, and `m2` stores transitions where the next value must be **smaller** than the current value.

* 🔹 Multiplying `m1` and `m2` gives a matrix representing two consecutive zigzag moves (up followed by down).

* 🔹 Since the array length `n` can be large, we use **matrix exponentiation (binary exponentiation)** to efficiently apply these transitions multiple times.

* 🔹 A vector `arr` keeps track of the number of ways to end at each possible value after applying the required transitions.

* 🔹 We repeatedly square the transition matrix and multiply it with the current state whenever the corresponding bit in the exponent is set.

* 🔹 If the remaining number of moves is odd, we apply one extra increasing transition using `m1`.

* 🔹 Finally, we sum all possible ending states and multiply by 2 to account for both possible starting zigzag directions (increase-first and decrease-first).

---

## ⏱ Time Complexity

**O(len^3 × log n)**

* Where:
    - `len = r - l + 1`

* due to matrix multiplication during binary exponentiation 

---

## 📦 Space Complexity

**O(len^2)**

* storing the transition matrices and intermediate matrix results.

---

## 💻 Java Code

```java
class Solution {
    public int zigZagArrays(int n, int l, int r) {
        int len = r - l + 1;
        long[][] m1 = new long[len][len];
        long[][] m2 = new long[len][len];
        for (int i = 0; i < len; i++) {
            for (int j = i + 1; j < len; j++) {
                m1[i][j] = 1;
            }
            for (int j = 0; j < i; j++) {
                m2[i][j] = 1;
            }
        }
        long[][] m = pro(m1, m2);
        long[] arr = new long[len];
        Arrays.fill(arr, 1);
        n--;
        int count = n / 2;
        while (count > 0) {
            if (count % 2 == 1)
                arr = pro(arr, m);
            m = pro(m);
            count /= 2;
        }
        if (n % 2 == 1)
            arr = pro(arr, m1);
        long res = 0;
        for (long num : arr) {
            res += num;
        }
        return (int) (res * 2 % mod);
    }

    int mod = 1_000_000_007;

    public long[][] pro(long[][] a) {
        long[][] res = new long[a.length][a[0].length];
        for (int i = 0; i < res.length; i++) {
            for (int k = 0; k < res.length; k++) {
                if (a[i][k] == 0)
                    continue;
                for (int j = 0; j < res.length; j++) {
                    res[i][j] = (res[i][j] + a[i][k] * a[k][j]) % mod;
                }
            }
        }
        return res;
    }

    public long[][] pro(long[][] a, long[][] b) {
        long[][] res = new long[a.length][a[0].length];
        for (int i = 0; i < res.length; i++) {
            for (int k = 0; k < res.length; k++) {
                if (a[i][k] == 0)
                    continue;
                for (int j = 0; j < res.length; j++) {
                    res[i][j] = (res[i][j] + a[i][k] * b[k][j]) % mod;
                }
            }
        }
        return res;
    }

    public long[] pro(long[] a, long[][] b) {
        long[] res = new long[a.length];
        for (int j = 0; j < res.length; j++) {
            if (a[j] == 0)
                continue;
            for (int i = 0; i < res.length; i++) {
                res[i] = (res[i] + a[j] * b[j][i]) % mod;
            }
        }
        return res;
    }
}
```

---