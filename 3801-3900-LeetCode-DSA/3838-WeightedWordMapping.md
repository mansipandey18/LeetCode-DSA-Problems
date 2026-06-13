# <u>3838. Weighted Word Mapping</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/weighted-word-mapping/

---

## 🧠 Intuition:
* 🔹 Process each word one by one from the given `words` array.

* 🔹 For every character in a word, use the `weights` array to find its assigned weight.

* 🔹 Sum up the weights of all characters to get the **total weight of the word**.

* 🔹 Take the total weight modulo `26` to keep the value within the alphabet range.

* 🔹 Convert the remainder into a character using **reverse alphabetical mapping**:
    - `0 → 'z'`
    - `1 → 'y'`
    - ...
    - `25 → 'a'`

* 🔹 Append the mapped character to the result string.

* 🔹 Repeat this process for all words and return the final constructed string.

---

## ⏱ Time Complexity

**O(N * L)**

* Let : 
    - `N` = number of words.
    - `L` = average length of a word.

* For each word, we traverse all its characters once.
    
---

## 📦 Space Complexity

**O(N)**

* The `StringBuilder` stores one character per word.
* No extra data structures proportional to the input size are used.

---

## 💻 Java Code

```java
class Solution {
    public String mapWordWeights(String[] words, int[] weights) {
        StringBuilder result = new StringBuilder();
        
        for (String word : words) {
            int wordWeight = 0;
            
            // Calculate total weight of the current word
            for (int i = 0; i < word.length(); i++) {
                wordWeight += weights[word.charAt(i) - 'a'];
            }
            
            // Get remainder modulo 26
            int remainder = wordWeight % 26;
            
            // Map to reverse alphabetical order: 0 -> 'z', 1 -> 'y', ..., 25 -> 'a'
            char mappedChar = (char) ('z' - remainder);
            result.append(mappedChar);
        }
        
        return result.toString();
    }
}
```

---