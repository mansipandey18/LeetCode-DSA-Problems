# <u>58. Length of Last Word</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/length-of-last-word/

---

## 🧠 Intuition:
* 🔹 **Step 1:** Start from the last character of the string.
    - `endIndex = s.length() - 1`

* 🔹 **Step 2:** Skip all trailing spaces.
    - Move left until we find a non-space character.
    - Now we are at the last character of the last word.

* 🔹 **Step 3:** Mark this position as `startIndex`.

* 🔹 **Step 4:** Keep moving left while characters are not spaces.
    - This finds where the last word starts.

* 🔹 **Step 5:** Calculate length:
    - Length = `endIndex - startIndex`

---

## ⏱ Time Complexity

**O(n)**

* Where : 
    - `n` = length of string.

---

## 📦 Space Complexity

**O(1)**

* No extra data structures used.
* Only variables are used.


---

## 💻 Java Code

```java
class Solution {
    public int lengthOfLastWord(String s) {
        int endIndex = s.length() - 1;
        while (endIndex >= 0 && s.charAt(endIndex) == ' '){
            endIndex--;
        }
        int startIndex = endIndex;
      
        while (startIndex >= 0 && s.charAt(startIndex) != ' ') {
            startIndex--;
        }    
        return endIndex - startIndex;
    }
}
```

---