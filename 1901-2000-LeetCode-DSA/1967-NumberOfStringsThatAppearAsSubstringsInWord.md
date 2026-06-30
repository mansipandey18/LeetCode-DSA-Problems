# <u>1967. Number of Strings That Appear as Substrings in Word</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/number-of-strings-that-appear-as-substrings-in-word/

---

## 🧠 Intuition:
* 🔹 Iterate through every pattern in the `patterns` array one by one.

* 🔹 For each pattern, check whether it appears as a substring inside the given `word`.

* 🔹 Use the built-in `contains()` method to perform the substring check.

* 🔹 If the pattern exists in the `word`, increase the answer count.

* 🔹 Continue this process until all patterns are checked.

* 🔹 Return the total number of patterns that are found as substrings of `word`.

---

## ⏱ Time Complexity

**O(p * m * n)**

* Where:
    - `p` = number of patterns
    - `n` = length of word
    - `m` = average length of a pattern

---

## 📦 Space Complexity

**O(1)**

* No extra space is needed

---

## 💻 Java Code

```java
class Solution {
    public int numOfStrings(String[] patterns, String word) {
        int matchCount = 0;
      
        // Iterate through each pattern in the patterns array
        for (String pattern : patterns) {
            // Check if the current pattern is a substring of word
            if (word.contains(pattern)) {
                // Increment counter if pattern is found in word
                matchCount++;
            }
        }
      
        // Return the total count of matching patterns
        return matchCount;
    }
}
```

---