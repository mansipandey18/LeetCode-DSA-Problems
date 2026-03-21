# <u>13. Roman to Integer</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/roman-to-integer/

---

## 🧠 Intuition:
* 🔹 Every Roman symbol has a fixed numeric value (I, V, X, L, C, D, M).

* 🔹 Roman numbers are usually formed by adding values from left to right.

* 🔹 Exception: when a smaller value comes before a larger value, it represents subtraction.
    - Example: IV = 5 − 1.

* 🔹 Store the value of each Roman character for quick lookup.
* 🔹 Traverse the string character by character.
* 🔹 For each character:
    - Compare its value with the next character.

* 🔹 If the current value is smaller than the next:
    - subtract it from the total.

* 🔹 Otherwise:
    - add it to the total.

* 🔹 Add the last character separately since it has no next element.

* 🔹 The final accumulated value is the integer representation.

---

## ⏱ Time Complexity

**O(n)**

* Where :
    - `n` = length of the Roman numeral string.

---

## 📦 Space Complexity

**O(1)**

* A fixed-size array of length 128 is used (constant size).

---

## 💻 Java Code

```java
class Solution {
    public int romanToInt(String s) {
        int ans = 0;
        int roman[] = new int[128];

        roman['I'] = 1; 
        roman['V'] = 5; 
        roman['X'] = 10; 
        roman['L'] = 50; 
        roman['C'] = 100;
        roman['D'] = 500;
        roman['M'] = 1000;

        for(int i = 0; i+1 < s.length(); ++i){
            if(roman[s.charAt(i)] < roman[s.charAt(i+1)]){
                ans -= roman[s.charAt(i)];
            }
            else{
                ans += roman[s.charAt(i)];
            }
        } 
        return ans + roman[s.charAt(s.length() - 1)];
    }
}
```

---