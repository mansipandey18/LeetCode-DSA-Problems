# <u>3116. Kth Smallest Amount With Single Denomination Combination</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/kth-smallest-amount-with-single-denomination-combination/

---

## 🧠 Intuition:
* 🔹 The goal is to find the **k-th smallest positive amount** that is divisible by at least one denomination in `coins`.

* 🔹 Use **Binary Search on the answer**:
    - Search for the smallest value `x` such that there are at least `k` valid amounts `≤ x`.

* 🔹 For a given `maxValue`, `countMultiples()` calculates how many numbers up to `maxValue` are divisible by **at least one coin**.

* 🔹 To avoid double-counting numbers divisible by multiple coins, use the **Inclusion-Exclusion Principle**:
    - Add multiples of individual coins.
    - Subtract multiples common to every pair.
    - Add back intersections of three coins, and so on.

* 🔹 For every subset of coins, calculate its **LCM**:
    - Numbers divisible by all coins in that subset are exactly the multiples of their LCM.
    - The number of such multiples up to `maxValue` is `maxValue / LCM`.

* 🔹 If the subset contains an odd number of coins, add its count; if even, subtract it.

* 🔹 `feasible(mid)` checks whether the number of valid amounts up to `mid` is at least `k`.

* 🔹 Binary search then narrows the range until the **smallest feasible value** is found.

* 🔹 The final `firstTrueIndex` is the k-th smallest valid amount.

---

## ⏱ Time Complexity

**O(2ⁿ · n · log V)**

* Let:
    - `n = coins.length`
    - `V = 10¹¹` (binary-search upper bound)
    - Binary search takes **O(log V)** iterations.
    - For every midpoint, `countMultiples()` examines all `2ⁿ - 1` subsets.
    - Calculating the LCM of a subset can take **O(n)** in the worst case.
* For this problem, `n` is small, so the exponential subset enumeration is feasible.

---

## 📦 Space Complexity

**O(n)**

* Only a constant number of variables and recursion stack for `gcd()` are used.
* No DP/table proportional to `n` is maintained.

---

## 💻 Java Code

```java
class Solution {
    private int[] coins;
    private int k;

    public long findKthSmallest(int[] coins, int k) {
        this.coins = coins;
        this.k = k;

        long left = 1;
        long right = (long) 1e11;
        long firstTrueIndex = -1;

        while (left <= right) {
            long mid = left + (right - left) / 2;
            if (feasible(mid)) {
                firstTrueIndex = mid;
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }

        return firstTrueIndex;
    }

    private boolean feasible(long maxValue) {
        return countMultiples(maxValue) >= k;
    }

    private long countMultiples(long maxValue) {
        long count = 0;
        int n = coins.length;

        for (int bitmask = 1; bitmask < (1 << n); ++bitmask) {
            long lcmValue = 1;

            for (int j = 0; j < n; ++j) {
                if ((bitmask >> j & 1) == 1) {
                    lcmValue = lcm(lcmValue, coins[j]);
                    if (lcmValue > maxValue) {
                        break;
                    }
                }
            }

            int subsetSize = Integer.bitCount(bitmask);
            if (subsetSize % 2 == 1) {
                count += maxValue / lcmValue;
            } else {
                count -= maxValue / lcmValue;
            }
        }

        return count;
    }

    private long lcm(long a, long b) {
        return a * b / gcd(a, b);
    }

    private long gcd(long a, long b) {
        return b == 0 ? a : gcd(b, a % b);
    }
}
```

---