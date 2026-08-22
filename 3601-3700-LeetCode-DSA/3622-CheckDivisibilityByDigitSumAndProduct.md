# <u>3620. Network Recovery Pathways</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/check-divisibility-by-digit-sum-and-product/

---

## 🧠 Intuition:
* 🔹 Make a copy of `n` so the original number remains unchanged for the final divisibility check.

* 🔹 Extract each digit using `number % 10`.

* 🔹 Remove the last digit using `number /= 10`.

* 🔹 Maintain two values while processing the digits:
    - `digitSum` → sum of all digits.
    - `digitProduct` → product of all digits.

* 🔹 After processing all digits, calculate `digitSum + digitProduct`.

* 🔹 Check whether `n` is exactly divisible by this value using `n % (digitSum + digitProduct) == 0`.

* 🔹 Return `true` if divisible; otherwise, return `false`.

---

## ⏱ Time Complexity

**O(d)**

* Where:
    - `d` = number of digits in `n`
* The loop processes each digit exactly once.

---

## 📦 Space Complexity

**O(1)**

* Only a few integer variables are used.

---

## 💻 Java Code

```java
class Solution {
    public boolean checkDivisibility(int n) {
        int digitSum = 0;      // Sum of all digits
        int digitProduct = 1;  // Product of all digits
        int number = n;        // Copy of n for digit extraction
      
        while (number != 0) {
            int currentDigit = number % 10;  // Get the last digit
            number /= 10;                     // Remove the last digit
          
            digitSum += currentDigit;        // Add digit to sum
            digitProduct *= currentDigit;    // Multiply digit to product
        }
      
        return n % (digitSum + digitProduct) == 0;
    }
}
```

---