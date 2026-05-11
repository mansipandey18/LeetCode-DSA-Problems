# <u>2553. Separate the Digits in an Array</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/separate-the-digits-in-an-array/

---

## 🧠 Intuition:
* 🔹 The goal is to separate every digit from each number in the array while preserving the original order

* 🔹 Traverse each number in `nums` one by one

* 🔹 For each number:
    - Extract digits using `% 10` (rightmost digit)
    - Remove the extracted digit using `/= 10`

* 🔹 Since digits are extracted from right to left, they get stored in reverse order

* 🔹 Use `Collections.reverse()` to restore the original digit order

* 🔹 Add all digits of the current number into the final result list

* 🔹 After processing all numbers:
    - Convert the `List<Integer>` into an integer array

* 🔹 Return the final array containing all separated digits in sequence

---

## ⏱ Time Complexity

**O(d)**

* Let : 
    - `d` = total number of digits across all numbers.

* Each digit is processed once during extraction and once during reversal

---

## 📦 Space Complexity

**O(d)**

* Extra list is used to store all separated digits
* Temporary list is also used for digits of each number

---

## 💻 Java Code

```java
class Solution {
    public int[] separateDigits(int[] nums) {
        List<Integer> resultList = new ArrayList<>();
      
        for (int number : nums) {
            List<Integer> digitsOfCurrentNumber = new ArrayList<>();
          
            while (number > 0) {
                digitsOfCurrentNumber.add(number % 10);  // Get the rightmost digit
                number /= 10;  // Remove the rightmost digit
            }
          
            Collections.reverse(digitsOfCurrentNumber);
          
            resultList.addAll(digitsOfCurrentNumber);
        }
      
        int[] resultArray = new int[resultList.size()];
        for (int i = 0; i < resultArray.length; i++) {
            resultArray[i] = resultList.get(i);
        }
      
        return resultArray;
    }
}
```

---