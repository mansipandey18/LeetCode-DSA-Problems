# <u>3658. GCD of Odd and Even Sums</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/gcd-of-odd-and-even-sums/

---

## 🧠 Intuition:
* 🔹 Observe the sum of the first `n` odd numbers:
    - `1 + 3 + 5 + ... = n²`

* 🔹 Observe the sum of the first `n` even numbers:
    - `2 + 4 + 6 + ... = n(n + 1)`

* We need to compute:
    - `gcd(n², n(n + 1))`

* 🔹 Factor out the common term `n`:
    - `gcd(n², n(n + 1)) = n × gcd(n, n + 1)`

* 🔹 Since two consecutive numbers are always coprime, `gcd(n, n + 1) = 1`.

* 🔹 Therefore:
    - `gcd(n², n(n + 1)) = n`

* 🔹 Hence, the answer is always `n`, so the function simply returns `n`.

---

## ⏱ Time Complexity

**O(1)**

* The answer is computed directly using the mathematical observation.

---

## 📦 Space Complexity

**O(1)**

* No extra space is used.


---

## 💻 Java Code

```java
class Solution {
    public int gcdOfOddEvenSums(int n) {
        return n;
    }
}
```

---