# <u>242. Valid Anagram</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/valid-anagram/

---

## 🧠 Intuition:
* 🔹 First check: if lengths of both strings are different → they can’t be anagrams.

* 🔹 Use a **frequency array** to count characters.

* 🔹 Traverse string `s` and **increase count** for each character.

* 🔹 Traverse string `t` and **decrease count** for each character:
    - If at any point count becomes 0 before decrement → means extra character in `t` → return `false`.

* 🔹 If all counts match perfectly, every character cancels out → strings are anagrams.

* 🔹 Final result → return true if no mismatch found.

---

## ⏱ Time Complexity

**O(n)**

* Traverse both strings once
    
---

## 📦 Space Complexity

**O(1)**

* Fixed size array (only 26 lowercase letters)

---

## 💻 Java Code

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if(s.length() != t.length()) {
            return false;
        }

        int[] charsCount = new int[28];

        for(char c: s.toCharArray()) {
            charsCount[c-'a']++;
        }
        for(char c: t.toCharArray()) {
            if(charsCount[c-'a']==0){
                return false;
            }
            charsCount[c-'a']--;
        }

        return true;
    }
}   
```

---