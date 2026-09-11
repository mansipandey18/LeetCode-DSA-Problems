# <u>3483. Unique 3-Digit Even Numbers</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/unique-3-digit-even-numbers/

---

## 🧠 Intuition:
* 🔹 Use three nested loops to try **every possible selection of 3 different indices** from the `digits` array.

* 🔹 The **ones digit must be even**, so combinations ending in an odd digit are skipped.

* 🔹 The **hundreds digit cannot be `0`**, because then the number would not be a 3-digit number.

* 🔹 Make sure the same array index is not reused for the hundreds, tens, and ones positions.

* 🔹 Construct the 3-digit number using:
    `hundreds × 100 + tens × 10 + ones`

* 🔹 Store every valid number in a `HashSet` so that **duplicate numbers are counted only once**, even when the same digit appears at multiple indices.

* 🔹 Finally, return the size of the set as the number of **unique 3-digit even numbers**.

---

## ⏱ Time Complexity

**O(n³)**

* Three nested loops → `O(n³)`
* `HashSet.add()` takes `O(1)` average time.
    
---

## 📦 Space Complexity

**O(n³)**

* The `HashSet` stores unique 3-digit numbers.
* Since there are only finitely many possible 3-digit numbers, the set can contain at most **900** values.
* Therefore, strictly for this problem's fixed digit range: `O(1)` auxiliary space.
* If expressed in terms of the number of generated candidates, it is `O(n³)` in the worst-case counting model.

---

## 💻 Java Code

```java
class Solution {
    public int totalNumbers(int[] digits) {
        Set<Integer> uniqueNumbers = new HashSet<>();
        int arrayLength = digits.length;
      
        // Iterate through all possible positions for the ones digit (must be even)
        for (int onesIndex = 0; onesIndex < arrayLength; ++onesIndex) {
            // Skip if the digit at this position is odd
            if (digits[onesIndex] % 2 == 1) {
                continue;
            }
          
            // Iterate through all possible positions for the tens digit
            for (int tensIndex = 0; tensIndex < arrayLength; ++tensIndex) {
                // Skip if using the same index as the ones digit
                if (onesIndex == tensIndex) {
                    continue;
                }
              
                // Iterate through all possible positions for the hundreds digit
                for (int hundredsIndex = 0; hundredsIndex < arrayLength; ++hundredsIndex) {
                    // Skip if:
                    // 1. The digit is 0 (cannot be in hundreds place)
                    // 2. The index is already used for ones or tens digit
                    if (digits[hundredsIndex] == 0 || 
                        hundredsIndex == onesIndex || 
                        hundredsIndex == tensIndex) {
                        continue;
                    }
                  
                    // Form the 3-digit number and add to set
                    int threeDigitNumber = digits[hundredsIndex] * 100 + 
                                         digits[tensIndex] * 10 + 
                                         digits[onesIndex];
                    uniqueNumbers.add(threeDigitNumber);
                }
            }
        }
      
        // Return the count of unique 3-digit numbers formed
        return uniqueNumbers.size();
    
    }
}
```

---