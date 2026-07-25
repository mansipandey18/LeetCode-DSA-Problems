# <u>3536. Maximum Product of Two Digits</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-product-of-two-digits/

---

## 🧠 Intuition:
* 🔹 Traverse the digits of the number one by one using the modulo (`% 10`) operation.

* 🔹 Maintain two variables:
    - `largestDigit` → stores the largest digit seen so far.
    - `secondLargestDigit` → stores the second largest digit.

* 🔹 For each extracted digit:
    - If it is greater than the current largest digit:
        * Move the current largest digit to `secondLargestDigit`.
        * Update `largestDigit` with the current digit.
    * Otherwise, if it is greater than the current second largest digit:
        * Update `secondLargestDigit`.

* 🔹 Remove the last digit by dividing the number by `10` and continue until all digits are processed.

* 🔹 After processing all digits, multiply the two largest digits to get the maximum possible product.

---

## ⏱ Time Complexity

**O(d)**

* Where:
    - `d` = number of digits.
* Each digit of the number is processed exactly once   
---

## 📦 Space Complexity

**O(1)**

* Only two variables are used to track the largest and second largest digits.

---

## 💻 Java Code

```java
class Solution {
    public int maxProduct(int n) {
        int largestDigit = 0;
        int secondLargestDigit = 0;
      
        while (n > 0) {
            int currentDigit = n % 10;
          
            if (currentDigit > largestDigit) {
                secondLargestDigit = largestDigit;
                largestDigit = currentDigit;
            } else if (currentDigit > secondLargestDigit) {
                secondLargestDigit = currentDigit;
            }
          
            n /= 10;
        }
      
        return largestDigit * secondLargestDigit;
    }
}
```

---