# <u>3120. Count the Number of Special Characters I</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/count-the-number-of-special-characters-i/

---

## 🧠 Intuition:
* 🔹 A character is called special if both its lowercase and uppercase forms exist in the string.

* 🔹 Use a boolean array to mark which characters are present in the word.

* 🔹 Traverse the string once and mark each character as present using its ASCII value.

* 🔹 After storing all characters, check all 26 English letters:
    - If both `'a' + i` and `'A' + i` are present, then that character is special.

* 🔹 Count all such valid characters and return the total count.

* 🔹 This approach avoids extra nested loops and allows constant-time presence checking.

---

## ⏱ Time Complexity

**O(n)**

* One traversal of the string and one loop over 26 letters.

---

## 📦 Space Complexity

**O(1)**

* Fixed-size boolean array is used.

---

## 💻 Java Code

```java
class Solution {
    public int numberOfSpecialChars(String word) {
        boolean[] characterPresence = new boolean['z' + 1];
      
        for (int i = 0; i < word.length(); i++) {
            characterPresence[word.charAt(i)] = true;
        }
      
        int specialCharCount = 0;
      
        for (int i = 0; i < 26; i++) {
            if (characterPresence['a' + i] && characterPresence['A' + i]) {
                specialCharCount++;
            }
        }
      
        return specialCharCount;
    }
}
```

---