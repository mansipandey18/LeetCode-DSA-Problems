# <u>788. Rotated Digits</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/rotated-digits/

---

## 🧠 Intuition:
* 🔹 The problem asks to count numbers from `1` to `n` that remain valid after rotation and change to a different number

* 🔹 Rotation rules:
    - Valid rotations → `0→0`, `1→1`, `2→5`, `5→2`, `6→9`, `8→8`, `9→6`
    - Invalid digits → `3, 4, 7` (if present → number is invalid)

* 🔹 A number is considered **good** if:
    - All its digits are valid after rotation
    - The rotated number is **different** from the original number

* 🔹 Approach:
    - Iterate through all numbers from `1` to `n`
    - For each number, check if it is a “good number”

* 🔹 To check a number:
    - Extract digits one by one using modulo (`% 10`)
    - Use `rotationMap` to find the rotated digit
    - If any digit maps to `-1`, return false (invalid number)
    - Build the rotated number using place values

* 🔹 After forming the rotated number:
    - Compare it with the original number
    - If they are different → valid “good number”

* 🔹 Count all such good numbers and return the total

* 🔹 This simulates the rotation process digit by digit efficiently


---

## ⏱ Time Complexity

**O(n log n)**

* For each number from `1` to `n`, we process its digits
* Each number takes **O(d)** time where `d = number of digits ≈ log₁₀(n)`

    
---

## 📦 Space Complexity

**O(1)**

* Only a few variables are used (no extra data structures dependent on `n`)

---

## 💻 Java Code

```java
class Solution {
    private int[] rotationMap = new int[] {0, 1, 5, -1, -1, 2, 9, -1, 8, 6};

    public int rotatedDigits(int n) {
        int goodNumberCount = 0;
      
        for (int number = 1; number <= n; ++number) {
            if (isGoodNumber(number)) {
                ++goodNumberCount;
            }
        }
      
        return goodNumberCount;
    }

    private boolean isGoodNumber(int originalNumber) {
        int rotatedNumber = 0;
        int tempNumber = originalNumber;
        int placeValue = 1;  // Represents the position multiplier (1, 10, 100, ...)
      
        while (tempNumber > 0) {
            int currentDigit = tempNumber % 10;
          
            if (rotationMap[currentDigit] == -1) {
                return false;  // Contains invalid digit (3, 4, or 7)
            }
          
            rotatedNumber = rotationMap[currentDigit] * placeValue + rotatedNumber;
            placeValue *= 10;
            tempNumber /= 10;
        }
      
        return originalNumber != rotatedNumber;
    
    }
}   
```

---