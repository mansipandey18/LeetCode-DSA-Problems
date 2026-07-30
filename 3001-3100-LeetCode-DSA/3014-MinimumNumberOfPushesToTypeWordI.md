# <u>3014. Minimum Number of Pushes to Type Word I</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/minimum-number-of-pushes-to-type-word-i/

---

## 🧠 Intuition:
* 🔹 A phone keypad can assign **up to 8 characters** to require the same number of key presses.

* 🔹 To minimize the total pushes:
    - Assign the **first 8 characters** to require 1 push each.
    - Assign the **next 8 characters** to require 2 pushes each.
    - Continue increasing the required pushes after every group of 8 characters.

* 🔹 Calculate the number of **complete groups of 8** characters in the word.

* 🔹 For each complete group:
    - Add `8 × pushesPerChar` to the total pushes.
    - Increment `pushesPerChar` for the next group.

* 🔹 Finally, process the remaining characters (less than 8) using the current push count.

* 🔹 The accumulated value is the **minimum number of pushes** needed to type the word.

---

## ⏱ Time Complexity

**O(1)**

* Only a few arithmetic operations and a loop with at most 4 iterations (since there are only 26 lowercase letters).

---

## 📦 Space Complexity

**O(1)**

* Only a constant amount of extra space is used.

---

## 💻 Java Code

```java
class Solution {
    public int minimumPushes(String word) {
        int wordLength = word.length();
      
        int totalPushes = 0;
      
        int pushesPerChar = 1;
      
        int completeGroups = wordLength / 8;

        for (int groupIndex = 0; groupIndex < completeGroups; groupIndex++) {
            totalPushes += pushesPerChar * 8;
          
            pushesPerChar++;
        }
      
        int remainingChars = wordLength % 8;
        totalPushes += pushesPerChar * remainingChars;
      
        return totalPushes;
    }
}
```

---