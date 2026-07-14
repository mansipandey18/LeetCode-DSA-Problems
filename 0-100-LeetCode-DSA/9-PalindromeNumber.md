# <u>9. Palindrome Number</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/palindrome-number/

---

## 🧠 Intuition:
* 🔹 A palindrome number reads the same from **left to right and right to left**.

* 🔹 Negative numbers can never be palindromes because they contain a `-` sign, so return `false` immediately.

* 🔹 Store the original number in a separate variable to compare later.

* 🔹 Reverse the digits of the number by:
    - Taking the last digit using `% 10`.
    - Appending it to the reversed number.
    - Removing the last digit from the original number using `/ 10`.

* 🔹 After the entire number is reversed, compare the reversed number with the original stored value.

* 🔹 If both are equal, the number is a palindrome; otherwise, it is not.

---

## ⏱ Time Complexity

**O(og₁₀ n)**

* Each digit is processed exactly once.
    
---

## 📦 Space Complexity

**O(1)**

* Only a few integer variables are used.

---

## 💻 Java Code

```java
class Solution {
    public boolean isPalindrome(int x) {
        int rem , rev = 0;
        int checkNum = x;

        if(x < 0){
            return false;
        }

        while (x != 0) {
            rem = x % 10;
            rev = rev*10 + rem;
            x /= 10;
        }
        
        if (checkNum == rev) {
            return true;
        } else{
            return false;
        }
        
    }
}
```

---