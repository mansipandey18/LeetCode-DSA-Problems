# <u>208. Implement Trie (Prefix Tree)</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/implement-trie-prefix-tree/

---

## 🧠 Intuition:
* 🔹 A Trie (Prefix Tree) is used to efficiently store and retrieve strings based on their prefixes.

* 🔹 Each node represents a character and has:
    - An array of 26 children (for lowercase English letters)
    - A boolean flag `isEndOfWord` to mark the end of a valid word

* 🔹 **Insertion:**
    - Start from the root and traverse character by character.
    - If a path for a character doesn’t exist, create a new node.
    - Move to the next node until the full word is inserted.
    - Mark the last node as `isEndOfWord = true`.

* 🔹 **Search:**
    - Traverse the Trie following the characters of the word.
    - If any character path is missing, the word does not exist.
    - Finally, check if the last node is marked as an end of a word.

* 🔹 **Prefix Check (startsWith):**
    - Similar to search, but we only verify if the prefix path exists.
    - No need to check `isEndOfWord`.

* 🔹 A helper function `searchPrefix()` is used to avoid repetition in search and prefix operations.

---

## ⏱ Time Complexity

- Insert → **O(L)** 
    - Where 
        * `L` = length of word

- Search → **O(L)**

- startsWith → **O(L)**

---

## 📦 Space Complexity

**O(N * L)**

* Where:
    - `N` = number of words
    - `L` = average length of words
    
* Each character may create a new Trie node.

---

## 💻 Java Code

```java
class Trie {
    private Trie[] children;  
    private boolean isEndOfWord;


    public Trie() {
        children = new Trie[26];
        isEndOfWord = false;
    }
    
    public void insert(String word) {
        Trie currentNode = this;
      
        for (char character : word.toCharArray()) {
            int index = character - 'a';
          
            if (currentNode.children[index] == null) {
                currentNode.children[index] = new Trie();
            }
          
            currentNode = currentNode.children[index];
        }
      
        currentNode.isEndOfWord = true;
    }
    
    public boolean search(String word) {
        Trie prefixEndNode = searchPrefix(word);
      
        return prefixEndNode != null && prefixEndNode.isEndOfWord;
    }
    
    public boolean startsWith(String prefix) {
        Trie prefixEndNode = searchPrefix(prefix);
      
        return prefixEndNode != null;
    }

    private Trie searchPrefix(String prefix) {
        Trie currentNode = this;
      
        for (char character : prefix.toCharArray()) {
            int index = character - 'a';
          
            if (currentNode.children[index] == null) {
                return null;
            }
          
            currentNode = currentNode.children[index];
        }
      
        return currentNode;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```

---