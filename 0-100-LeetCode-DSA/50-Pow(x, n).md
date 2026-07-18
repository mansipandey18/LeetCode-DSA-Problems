# <u>50. Pow(x, n)</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/powx-n/

---

## 🧠 Intuition:
* 🔹 Instead of multiplying `x` by itself `n` times, use **Binary Exponentiation (Fast Power)** to reduce the number of operations.

* 🔹 If the exponent is **negative**, compute the power using its positive value and return its reciprocal `(1 / result)`.

* 🔹 Start with `result = 1`.

* 🔹 While the exponent is greater than `0`:
    - If the current exponent is **odd**, multiply the current  `base` with the `result`.
    - Square the `base (base = base × base)` to represent powers of `2`.
    - Divide the exponent by `2` using a right shift (`exponent >>= 1`).

* 🔹 Repeat until the exponent becomes `0`.

* 🔹 Using `long` for the exponent prevents overflow when handling `Integer.MIN_VALUE`.

* 🔹 This approach computes the answer efficiently by processing the exponent bit by bit.
---

## ⏱ Time Complexity

**O(log n)**

* The exponent is halved in every iteration.
    
---

## 📦 Space Complexity

**O(1)**

* Only a few variables are used; no extra data structures are required.

---

## 💻 Java Code

```java
class Solution {
    public double myPow(double x, int n) {
        return n >= 0 ? quickPower(x, n) : 1.0 / quickPower(x, -(long) n);
    }

    private double quickPower(double base, long exponent) {
        double result = 1.0;

        while (exponent > 0) {
            if ((exponent & 1) == 1) {
                result *= base;
            }

            base *= base;
            exponent >>= 1;
        }

        return result;
    }
}
```

---