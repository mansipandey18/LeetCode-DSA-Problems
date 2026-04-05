# <u>30. Substring with Concatenation of All Words</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/substring-with-concatenation-of-all-words/

---

## 🧠 Intuition:
* 🔹 We are given a string `s` and an array `words`, and we must find **all starting indices where all words appear exactly once and continuously** (order does not matter).

* 🔹 Since all words have the same length, treat the string as blocks of fixed size `(wordLength)`.

* 🔹 First, create a `wordCount` map to store how many times each word should appear.

* 🔹 Instead of checking every index character-by-character, slide a window in steps of `wordLength` to align with word boundaries.

* 🔹 Start checking from every possible offset (`0` to `wordLength - 1`) to cover all alignments.

* 🔹 Maintain:
    - `currentCount` → counts of words inside the current window.
    - `left` and `right` pointers → represent the sliding window.
    - `totalWords` → number of valid words currently matched.

* 🔹 Move `right` forward and extract substrings of length `wordLength`.

* 🔹 If the word is **not in the given list**, reset the window because the sequence is invalid.

* 🔹 If the word exists, add it to `currentCount`.

* 🔹 If any word appears more times than allowed, shrink the window from the left until counts become valid.

* 🔹 When `totalWords == number of words`, we found a valid concatenation → store `left` index.

* 🔹 Continue sliding to find all valid starting positions.
---

## ⏱ Time Complexity

**O(n)**

* Where :
    - `n` = length of string
    
---

## 📦 Space Complexity

**O(n)**

* Let :
    - `n` = length of string `s`
    - Each character is processed at most once per offset using sliding window.

---

## 💻 Java Code

```java
class Solution {
    public List<Integer> findSubstring(String s, String[] words) {
        Map<String, Integer> wordCount = new HashMap<>();
      
        // Create and populate a map with the count of each unique word
        for (String word : words) {
            wordCount.merge(word, 1, Integer::sum);
        }
      
        int strLength = s.length(), numOfWords = words.length;
        int wordLength = words[0].length(); // Assume all words are the same length
        List<Integer> indices = new ArrayList<>();
      
        // Iterate over all possible word start indices to check for valid substrings
        for (int i = 0; i < wordLength; ++i) {
            Map<String, Integer> currentCount = new HashMap<>();
            int left = i, right = i;
            int totalWords = 0;
          
            // Expand the window to the right, adding words into current window count
            while (right + wordLength <= strLength) {
                String sub = s.substring(right, right + wordLength);
                right += wordLength;
              
                // If the word is not in the original word list, reset the window
                if (!wordCount.containsKey(sub)) {
                    currentCount.clear();
                    left = right;
                    totalWords = 0;
                    continue;
                }
              
                // Increase the count for the current word in the window
                currentCount.merge(sub, 1, Integer::sum);
                ++totalWords;
              
                // If a word count exceeds its count in wordCount, reduce from left side
                while (currentCount.get(sub) > wordCount.get(sub)) {
                    String removed = s.substring(left, left + wordLength);
                    left += wordLength;
                    currentCount.merge(removed, -1, Integer::sum);
                    --totalWords;
                }
              
                // If the total words reached the number of words, a valid substring is found
                if (totalWords == numOfWords) {
                    indices.add(left);
                }
            }
        }
        return indices;
    }
}
```

---