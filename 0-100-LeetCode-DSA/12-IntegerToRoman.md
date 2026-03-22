# <u>12. Integer to Roman</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/integer-to-roman/

---

## 🧠 Intuition:
* 🔹 We have a big matrix, and we focus on a small k × k square inside it.
* 🔹 This small square acts like a window.
* 🔹 First, we place the window at the top-left corner of the matrix.
* 🔹 We collect all k² numbers inside this window.
* 🔹 To easily analyze these numbers, we sort them.
* 🔹 Sorting helps us quickly find the required value (like smallest, median, etc.).
* 🔹 After finishing one window, we move the window one step to the right.
* 🔹 When we reach the end of the row, we move the window down to the next row.
* 🔹 We repeat the same process for every possible window position.
* 🔹 Since each window is processed separately, we repeat sorting for every k × k block.

---

## ⏱ Time Complexity

**O(1)**

* The loop runs over a fixed list of 13 Roman symbols.
* The number of operations is bounded (Roman numerals limit ≤ 3999).

---

## 📦 Space Complexity

**O(1)**

* Only a `StringBuilder` is used to store the result.

---

## 💻 Java Code

```java
class Solution {
    public String intToRoman(int num) {
        // Define arrays for Roman numeral characters and their corresponding values.
        String[] romanNumerals = {"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"};
        int[] values = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};
      
        // Initialize a StringBuilder to build the Roman numeral string.
        StringBuilder romanString = new StringBuilder();
      
        // Iterate over the Roman numerals and values to construct the Roman numeral.
        for (int i = 0; i < romanNumerals.length; i++) {
            while (num >= values[i]) { // While the number is greater than the current value
                num -= values[i]; // Subtract the value from the number
                romanString.append(romanNumerals[i]); // Append the corresponding Roman numeral to the string
            }
        }

        // Return the constructed Roman numeral string.
        return romanString.toString();
    }
}
```

---