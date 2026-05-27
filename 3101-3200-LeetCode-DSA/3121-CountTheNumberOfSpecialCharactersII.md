# <u>3121. Count the Number of Special Characters II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/count-the-number-of-special-characters-ii/

---

## 🧠 Intuition:
* 🔹 A character is considered special if:
    - Its lowercase version appears in the string.
    - Its uppercase version also appears.
    - Every lowercase occurrence comes before the first uppercase occurrence.

* 🔹 Use two arrays:
    - `firstOccurrence` → stores the first position of each character.
    - `lastOccurrence` → stores the last position of each character.

* 🔹 Traverse the string once:
    - Record the first occurrence if not already set.
    - Continuously update the last occurrence.

* 🔹 After preprocessing, check all 26 English letters:
    - Let lowercase = `'a' + i`
    - Let uppercase = `'A' + i`

* 🔹 A letter is special if:
    - Lowercase exists.
    - Uppercase exists.
    - `lastOccurrence[lowercase] < firstOccurrence[uppercase]`

* 🔹 Count all such valid characters and return the result.

* 🔹 This approach efficiently validates ordering without extra nested traversals.

---

## ⏱ Time Complexity

**O(n)**

* One traversal of the string and one loop over 26 letters.

---

## 📦 Space Complexity

**O(1)**

* Fixed-size arrays are used for character tracking.

---

## 💻 Java Code

```java
class Solution {
    public int numberOfSpecialChars(String word) {
        int[] firstOccurrence = new int['z' + 1];
        int[] lastOccurrence = new int['z' + 1];
      
        for (int i = 1; i <= word.length(); i++) {
            char currentChar = word.charAt(i - 1);
          
            if (firstOccurrence[currentChar] == 0) {
                firstOccurrence[currentChar] = i;
            }
          
            lastOccurrence[currentChar] = i;
        }
      
        int specialCharCount = 0;
      
        for (int i = 0; i < 26; i++) {
            char lowercaseLetter = (char) ('a' + i);
            char uppercaseLetter = (char) ('A' + i);
          
            if (lastOccurrence[lowercaseLetter] > 0 && 
                firstOccurrence[uppercaseLetter] > 0 && 
                lastOccurrence[lowercaseLetter] < firstOccurrence[uppercaseLetter]) {
                specialCharCount++;
            }
        }
      
        return specialCharCount;
    }
}
```

---