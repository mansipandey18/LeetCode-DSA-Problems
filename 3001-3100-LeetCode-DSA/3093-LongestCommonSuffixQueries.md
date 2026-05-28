# <u>3093. Longest Common Suffix Queries</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/longest-common-suffix-queries/

---

## 🧠 Intuition:
* 🔹 The problem asks for the index of the word in `wordsContainer` having the **longest common suffix** with each query word.

* 🔹 A normal Trie works for prefixes, so to handle suffixes efficiently, insert words in **reverse order**.

* 🔹 Each Trie path now represents a suffix instead of a prefix.

* 🔹 While inserting a word:
    - Traverse characters from the end to the beginning.
    - Create Trie nodes if needed.
    - Store at every node:
        * `minLength` → shortest word length passing through that node.
        * `wordIndex` → index of that shortest word.

* 🔹 Storing the shortest word helps resolve ties automatically according to problem requirements.

* 🔹 During query:
    - Traverse the Trie using the reversed query string.
    - Continue while matching suffix characters exist.
    - Stop when no further match is possible.

* 🔹 The current Trie node then contains the best matching word index for the longest common suffix found.

* 🔹 Root node also stores the globally shortest word, which handles cases where no suffix matches.

---

## ⏱ Time Complexity

**O(totalContainerChars + totalQueryChars)**

* Insertion processes every character once.
* Each query traversal also processes characters once.

---

## 📦 Space Complexity

**O(totalContainerChars × 26)**

* Trie nodes are created for characters of all inserted words.

---

## 💻 Java Code

```java
class Trie {
    private static final int INFINITY = 1 << 30;  
    private Trie[] children = new Trie[26];
    private int minLength = INFINITY;  
    private int wordIndex = INFINITY;

    
    public void insert(String word, int index) {
        Trie currentNode = this;
      
        // Update root node's minimum length if necessary
        if (currentNode.minLength > word.length()) {
            currentNode.minLength = word.length();
            currentNode.wordIndex = index;
        }
      
        // Insert characters in reverse order (from last to first)
        for (int charPos = word.length() - 1; charPos >= 0; charPos--) {
            int charIndex = word.charAt(charPos) - 'a';
          
            // Create new node if path doesn't exist
            if (currentNode.children[charIndex] == null) {
                currentNode.children[charIndex] = new Trie();
            }
          
            // Move to child node
            currentNode = currentNode.children[charIndex];
          
            // Update minimum length at current node if necessary
            if (currentNode.minLength > word.length()) {
                currentNode.minLength = word.length();
                currentNode.wordIndex = index;
            }
        }
    }

    public int query(String word) {
        Trie currentNode = this;
      
        // Traverse the trie following the reverse path of the query word
        for (int charPos = word.length() - 1; charPos >= 0; charPos--) {
            int charIndex = word.charAt(charPos) - 'a';
          
            // Stop if no matching path exists
            if (currentNode.children[charIndex] == null) {
                break;
            }
          
            // Move to child node
            currentNode = currentNode.children[charIndex];
        }
      
        // Return the index of the shortest word found
        return currentNode.wordIndex;
    }
}

class Solution {
    public int[] stringIndices(String[] wordsContainer, String[] wordsQuery) {
        // Build trie from container words
        Trie trie = new Trie();
        for (int i = 0; i < wordsContainer.length; i++) {
            trie.insert(wordsContainer[i], i);
        }
      
        // Process each query word
        int queryCount = wordsQuery.length;
        int[] result = new int[queryCount];
        for (int i = 0; i < queryCount; i++) {
            result[i] = trie.query(wordsQuery[i]);
        }
      
        return result;
    }
}
```

---