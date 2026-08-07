# <u>3348. Smallest Divisible Digit Product II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/smallest-divisible-digit-product-ii/

---

## 🧠 Intuition:
* 🔹 The product of the digits can only contribute the prime factors **2, 3, 5, and 7**, so first factorize `t` into these primes.

* 🔹 If `t` contains any other prime factor, it is impossible to construct a valid number, so return `"-1"`.

* 🔹 Maintain the remaining prime factor requirements in `primeCount`.

* 🔹 Determine the **minimum number of digits** required to satisfy the remaining prime factors using the most efficient digit combinations (`9`, `8`, `6`, `4`, etc.).

* 🔹 If the current number is shorter than this minimum length, directly construct the smallest valid number using the required digits.

* 🔹 Otherwise, scan the given number from left to right while updating the remaining prime requirements contributed by its digits.

* 🔹 If the original number already satisfies all prime factor requirements (and contains no invalid zero), return it immediately.

* 🔹 If not, try to modify the number from **right to left**:
    - Increase one digit to the next possible value.
    - Check whether the remaining suffix can still satisfy all required prime factors.
    - As soon as a valid modification is found, greedily construct the **smallest possible suffix**.

* 🔹 The suffix is built using the fewest and smallest digits possible by combining prime factors efficiently:
    - Use digits like `9`, `8`, `6`, `4`, etc., to reduce the total number of digits.
    - Fill any remaining positions with `'1'` to keep the overall number lexicographically smallest.

* 🔹 This greedy construction guarantees the **smallest valid number that is greater than or equal to the given number**.

---

## ⏱ Time Complexity

**O(n)**

* Where:
    - `n` = length of `num`
* Factorizing `t` uses only four primes (`2, 3, 5, 7`) → **O(1)**.
* Scanning the number, trying replacements, and building the suffix each take linear time.
* Each digit is processed a constant number of times.

---

## 📦 Space Complexity

**O(n)**

* The result character array stores the constructed answer.
* The prime count array and other helper variables use constant extra space.
* Overall auxiliary space is dominated by the output array.

---

## 💻 Java Code

```java
class Solution {
    int primes[] = new int[] { 2, 3, 5, 7 };
    int maxPrime = primes[primes.length - 1];

    public String smallestNumber(String num, long t) {
        int primeCount[] = new int[maxPrime + 1];
        int numLength = num.length();
        int minLength;
        int firstZeroIndexFromLeft = 0;

        for (int prime : primes) {
            while (t % prime == 0) {
                t /= prime;
                primeCount[prime]++;
            }
        }

        if (t != 1) {
            return "-1";
        }

        minLength = getMinLength(primeCount);

        if (numLength < minLength) {
            return buildSuffix(primeCount, minLength, new char[minLength]);
        }

        char[] result = new char[numLength + 1];

        for (int i = 0; firstZeroIndexFromLeft < numLength
                && (result[++i] = num.charAt(firstZeroIndexFromLeft)) != '0'; firstZeroIndexFromLeft++) {
            logNum(primeCount, result[i], -1);
        }

        if (getMinLength(primeCount) == 0) {
            if (firstZeroIndexFromLeft == numLength) {
                return num;
            }
            Arrays.fill(result, ++firstZeroIndexFromLeft, result.length, '1');
            return new String(result, 1, numLength);
        }

        for (int last = numLength - 1, end = Math.min(firstZeroIndexFromLeft, last); end >= 0; end--) {
            for (logNum(primeCount, result[end + 1], 1); ++result[end + 1] <= '9'; logNum(primeCount, result[end + 1], 1)) {
                logNum(primeCount, result[end + 1], -1);
                if (getMinLength(primeCount) <= last - end) {
                    return buildSuffix(primeCount, last - end, result);
                }
            }
        }

        return buildSuffix(primeCount, result.length, result);
    }

    void logNum(int[] primeCount, int num, int value) {
        if (num < '2') {
            return;
        }

        if (num == '9') {
            primeCount[3] += value << 1;
        } else if (num == '4') {
            primeCount[2] += value << 1;
        } else if (num == '8') {
            primeCount[2] += value * 3;
        } else if (num == '6') {
            primeCount[2] += value;
            primeCount[3] += value;
        } else {
            primeCount[num - '0'] += value;
        }
    }

    String buildSuffix(int[] primeCount, int targetLength, char[] result) {
        int index = result.length;

        while (primeCount[3] > 1) {
            primeCount[3] -= 2;
            result[--index] = '9';
        }

        while (primeCount[2] > 2) {
            primeCount[2] -= 3;
            result[--index] = '8';
        }

        while (primeCount[7]-- > 0) {
            result[--index] = '7';
        }

        if (primeCount[2] > 0 && primeCount[3] > 0) {
            result[--index] = '6';
            primeCount[2]--;
            primeCount[3]--;
        }

        while (primeCount[5]-- > 0) {
            result[--index] = '5';
        }

        while (primeCount[2] > 1) {
            primeCount[2] -= 2;
            result[--index] = '4';
        }

        while (primeCount[3] > 0) {
            primeCount[3]--;
            result[--index] = '3';
        }

        while (primeCount[2] > 0) {
            primeCount[2]--;
            result[--index] = '2';
        }

        while (index + targetLength != result.length) {
            result[--index] = '1';
        }

        return targetLength == result.length ? new String(result) : new String(result, 1, result.length - 1);
    }

    int getMinLength(int[] primeCount) {
        int count2 = Math.max(0, primeCount[2]);
        int count3 = Math.max(0, primeCount[3]);
        int count23 = (count3 & 1) + (count2 % 3);

        return (count3 >> 1) + (count2 / 3) + Math.max(0, primeCount[7]) + Math.max(0, primeCount[5])
                + (count23 == 3 ? 2 : count23 > 0 ? 1 : 0);
    }
}
```

---