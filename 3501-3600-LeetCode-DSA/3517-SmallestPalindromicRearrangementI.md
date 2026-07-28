# <u>3517. Smallest Palindromic Rearrangement I</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/smallest-palindromic-rearrangement-i/

---

## 🧠 Intuition:
* 🔹 Since the given string is already rearrangeable into a palindrome, only the **first half** determines the lexicographical order of the entire palindrome.

* 🔹 Extract the first half of the string because the second half is simply its mirror image.

* 🔹 Sort the characters of the first half in **ascending order** to make the left half as small as possible lexicographically.

* 🔹 If the string has an **odd length**, keep the middle character unchanged since it always stays in the center of the palindrome.

* 🔹 Reverse the sorted first half to create the right half, ensuring the palindrome property is maintained.

* 🔹 Concatenate:
    - **Sorted first half**
    - **Middle character (if any)**
    - **Reversed first half**

* 🔹 The resulting string is the **lexicographically smallest valid palindrome**.

---

## ⏱ Time Complexity

**O(n log n)**

* Sorting the first half of the string (size `n/2`) dominates the running time.

---

## 📦 Space Complexity

**O(n)**

* Extra space is used for the character array, sorted half, reversed half, and the final result string.

---

## 💻 Java Code

```java
class Solution {
    public String smallestPalindrome(String s) {
        int n = s.length();
        
        char[] halfChars = s.substring(0, n / 2).toCharArray();
        
        Arrays.sort(halfChars);
        String sortedHalf = new String(halfChars);
        
        String mid = (n % 2 == 1) ? String.valueOf(s.charAt(n / 2)) : "";
        
        String reversedHalf = new StringBuilder(sortedHalf).reverse().toString();
        
        return sortedHalf + mid + reversedHalf;
    }
}
```

---