# <u>125. Valid Palindrome</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/valid-palindrome/

---

## 🧠 Intuition:
* 🔹 A palindrome reads the **same forward and backward**.

* 🔹 We use the two-pointer approach:
    - `left` starts from the beginning.
    - `right` starts from the end.

* 🔹 Move both pointers toward the center while comparing characters.

* 🔹 Ignore characters that are **not letters or digits** (skip spaces, commas, symbols, etc.).

* 🔹 Convert both characters to **lowercase** before comparing to make the check **case-insensitive**.

* 🔹 If valid characters at both pointers are different → string is **not a palindrome**.

* 🔹 If they match → move both pointers inward.

* 🔹 Continue until pointers cross.

* 🔹 If no mismatch is found, the string is a valid palindrome.e.

---

## ⏱ Time Complexity

**O(n)**

* Where :
    - `n` = length of string
    
---

## 📦 Space Complexity

**O(1)**

* No extra data structures are used.
* Only variables (`left`, `right`, chars) are stored.

---

## 💻 Java Code

```java
class Solution {
    public boolean isPalindrome(String s) {
        int left = 0, right = s.length()-1;
        while(left<right)
        {
            char l = s.charAt(left), r = s.charAt(right);
            
            if(!Character.isLetterOrDigit(l)) 
                left++;
            else if(!Character.isLetterOrDigit(r)) 
                right--;
            else if(Character.toLowerCase(l)!=Character.toLowerCase(r)) 
                return false;
            else {
                left++; 
                right--;
            }
        }
        return true;
    }
}
```

---