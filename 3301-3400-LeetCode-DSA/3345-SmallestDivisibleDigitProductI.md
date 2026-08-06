# <u>3345. Smallest Divisible Digit Product I</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/smallest-divisible-digit-product-i/

---

## 🧠 Intuition:
* 🔹 Start checking numbers from `n` and move upward one by one.

* 🔹 For each number:
    - Extract each digit using modulo (`% 10`).
    - Compute the **product of all its digits**.

* 🔹 After calculating the digit product, check whether it is divisible by `t`.

* 🔹 If the product is divisible by `t`, return the current number immediately since we are checking numbers in increasing order.

* 🔹 Otherwise, continue to the next number and repeat the process.

* 🔹 This brute-force approach guarantees that the **first valid number found is the smallest possible answer**.
---

## ⏱ Time Complexity

**O(k * d)**

* Let `k` be the number of integers checked until a valid answer is found.
* Let `d` be the number of digits in each number.
* Computing the digit product takes `O(d)` for each number. 

---

## 📦 Space Complexity

**O(1)**

* Only a few variables are used regardless of the input size.

---

## 💻 Java Code

```java
class Solution {
    public int smallestNumber(int n, int t) {
        for (int currentNumber = n; ; currentNumber++) {
            int digitProduct = 1;
            int tempNumber = currentNumber;
          
            while (tempNumber > 0) {
                int lastDigit = tempNumber % 10;  // Get the last digit
                digitProduct *= lastDigit;         // Multiply to the product
                tempNumber /= 10;                   // Remove the last digit
            }
          
            if (digitProduct % t == 0) {
                return currentNumber;
            }
        }
    }
}
```

---