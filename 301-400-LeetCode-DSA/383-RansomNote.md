# <u>383. Ransom Note</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/ransom-note/

---

## 🧠 Intuition:
* 🔹 The problem is to check if we can construct `ransomNote` using characters from `magazine`.

* 🔹 Idea: Count how many times each character appears in `magazine`.

* 🔹 Create an array `letterCounts[26]` to store frequency of each lowercase letter.

* 🔹 First loop:
    - Traverse `magazine` and **increment count** for each character.

* 🔹 Second loop:
    - Traverse `ransomNote` and **decrement count** for each character.
    - If any count becomes **negative**, it means:
        * That character is required more times than available → return `false`.

* 🔹 If all characters are successfully matched, return `true`.

* 🔹 This works because we ensure **availability of each character before using it**.

---

## ⏱ Time Complexity

**O(m + n)**

* Where :
    - `m` = length of `magazine`
    - `n` = length of `ransomNote`

* Counting characters in `magazine` → **O(m)**

* Checking ransomNote → **O(n)**
    
---

## 📦 Space Complexity

**O(1)**

* Fixed array of size 26 (for lowercase letters).

---

## 💻 Java Code

```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        int[] letterCounts = new int[26];
      
        for (int i = 0; i < magazine.length(); i++) {
            letterCounts[magazine.charAt(i) - 'a']++;
        }
      
        for (int i = 0; i < ransomNote.length(); i++) {
            if (--letterCounts[ransomNote.charAt(i) - 'a'] < 0) {
                return false;
            }
        }
      
        return true;
    }
}   
```

---