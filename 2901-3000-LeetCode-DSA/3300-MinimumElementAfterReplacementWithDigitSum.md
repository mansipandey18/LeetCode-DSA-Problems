# <u>3300. Minimum Element After Replacement With Digit Sum</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/minimum-element-after-replacement-with-digit-sum/

---

## 🧠 Intuition:
* 🔹 For each number in the array, replace it with the sum of its digits.

* 🔹 To calculate the digit sum:
    - Repeatedly take the last digit using `number % 10`.
    - Add it to `digitSum`.
    - Remove the last digit using `number /= 10`.

* 🔹 After computing the digit sum of a number, compare it with the current minimum digit sum.

* 🔹 Keep updating `minDigitSum` whenever a smaller digit sum is found.

* 🔹 After processing all elements, return the minimum digit sum obtained.

* 🔹 This approach directly simulates the required replacement operation efficiently.

---

## ⏱ Time Complexity

**O(n * d)**

* Where:
    - `n` = number of elements
    - `d` = number of digits in each number
    
---

## 📦 Space Complexity

**O(1)**

* Only constant extra variables are used.

---

## 💻 Java Code

```java
class Solution {
    public int minElement(int[] nums) {
        int minDigitSum = 100;
      
        // Iterate through each number in the array
        for (int number : nums) {
            // Calculate the sum of digits for the current number
            int digitSum = 0;
          
            // Extract and sum each digit by repeatedly dividing by 10
            while (number > 0) {
                digitSum += number % 10;  // Add the last digit to the sum
                number /= 10;              // Remove the last digit
            }
          
            // Update the minimum digit sum if current sum is smaller
            minDigitSum = Math.min(minDigitSum, digitSum);
        }
      
        return minDigitSum;
    }
}
```

---