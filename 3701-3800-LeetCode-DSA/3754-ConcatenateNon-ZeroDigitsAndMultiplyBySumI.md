# <u>3754. Concatenate Non-Zero Digits and Multiply by Sum I</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/concatenate-non-zero-digits-and-multiply-by-sum-i/

---

## 🧠 Intuition:
* 🔹 Extract digits one by one using **n % 10**.

* 🔹 Maintain **digitSum** → sum of all digits.

* 🔹 Maintain **compactedNumber** → number formed by only non-zero digits in their original order.

* 🔹 When a digit is non-zero, append it to **compactedNumber** using **placeValue**.

* 🔹 Ignore zeros while building the compacted number.

* 🔹 After processing all digits, return **compactedNumber × digitSum**.

---

## ⏱ Time Complexity

**O(d)**

* Where:
    - `d` = number of digits in `n`

---

## 📦 Space Complexity

**O(1)**

* only a few variables are used

---

## 💻 Java Code

```java
class Solution {
    public long sumAndMultiply(int n) {
        int placeValue = 1;

        int compactedNumber = 0, digitSum = 0;

        for (; n > 0; n /= 10) {
            int digit = n % 10;

            digitSum += digit;

            if (digit != 0) {
                compactedNumber += placeValue * digit;
                placeValue *= 10;
            }
        }

        return 1L * compactedNumber * digitSum;
    }
}
```

---