# <u>290. Word Pattern</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/word-pattern/

---

## 🧠 Intuition:
* 🔹 We need to check if **pattern characters map uniquely to words** (one-to-one mapping).

* 🔹 First, split the string `s` into words and check if lengths match → otherwise not possible.

* 🔹 Use **two maps**:
    - `char → word` (to ensure each character maps to same word)
    - `word → char` (to ensure no two characters map to same word)

* 🔹 Traverse both pattern and words together:
    - For each pair `(char, word)`, check:
        * If mapping already exists, it must match the current word
        * If reverse mapping exists, it must match the current char

* 🔹 If any mismatch occurs → return `false`.

* 🔹 Otherwise, store/update mappings and continue.

* 🔹 If all pairs satisfy the condition → return `true`.


---

## ⏱ Time Complexity

**O(n)**

* Where :
    - `n` = length of string / number of words

* Splitting string + single traversal
    
---

## 📦 Space Complexity

**O(n)**

* Two HashMaps storing mappings

---

## 💻 Java Code

```java
class Solution {
    public boolean wordPattern(String pattern, String s) {
        String[] words = s.split(" ");
      
        if (pattern.length() != words.length) {
            return false;
        }
      
        Map<Character, String> charToWordMap = new HashMap<>();
        Map<String, Character> wordToCharMap = new HashMap<>();
      
        for (int i = 0; i < words.length; ++i) {
            char currentChar = pattern.charAt(i);
            String currentWord = words[i];
          
            if (!charToWordMap.getOrDefault(currentChar, currentWord).equals(currentWord) || wordToCharMap.getOrDefault(currentWord, currentChar) != currentChar) {
                return false;
            }
          
            charToWordMap.put(currentChar, currentWord);
            wordToCharMap.put(currentWord, currentChar);
        }
      
        return true;
    }
}
```

---