# <u>211. Design Add and Search Words Data Structure</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/course-schedule-ii/

---

## 🧠 Intuition:
* 🔹 Use a **Trie (Prefix Tree)** to efficiently store and search words character by character.

* 🔹 Each Trie node contains:
  - An array of 26 children (for letters `'a'` to `'z'`).
  - A flag `isEnd` to mark the end of a valid word.

* 🔹 **addWord():**
  - Traverse the Trie for each character in the word.
  - Create new nodes if the path does not exist.
  - Mark the last node as the end of a word.

* 🔹 **search():**
  - Traverse the Trie character by character.
  - If the character is a normal letter, move to the corresponding child node.
  - If the character is `'.'`, it can represent any letter:
    * Try all non-null child nodes recursively.
    * If any path returns `true`, the word exists.

* 🔹 If all characters are processed successfully, return whether the current node marks the end of a valid word.

* 🔹 Recursion helps explore all possible matches when a wildcard `'.'` is encountered.

---

## ⏱ Time Complexity

**O(L)** (without wildcards)
**O(26^L)** (worst case with all wildcards)

* Where:
  - `L` = length of the word.

---

## 📦 Space Complexity

**O(N)**

* Where:
  - `N` = total number of characters inserted across all words.

---

## 💻 Java Code

```java
class Trie {
    Trie[] children = new Trie[26];
    boolean isEnd;
}

class WordDictionary {
    private Trie root;

    public WordDictionary() {
        root = new Trie();
    }
    
    public void addWord(String word) {
        Trie currentNode = root;
      
        for (char ch : word.toCharArray()) {
            int index = ch - 'a';
          
            if (currentNode.children[index] == null) {
                currentNode.children[index] = new Trie();
            }
          
            currentNode = currentNode.children[index];
        }
      
        currentNode.isEnd = true;
    }
    
    public boolean search(String word) {
        return searchHelper(word, root);
    }

    private boolean searchHelper(String word, Trie currentNode) {
        for (int i = 0; i < word.length(); i++) {
            char ch = word.charAt(i);
          
            if (ch == '.') {
                for (Trie childNode : currentNode.children) {
                    if (childNode != null && 
                        searchHelper(word.substring(i + 1), childNode)) {
                        return true;
                    }
                }
                return false;
            } else {
                int index = ch - 'a';
              
                if (currentNode.children[index] == null) {
                    return false;
                }
              
                currentNode = currentNode.children[index];
            }
        }
      
        return currentNode.isEnd;
    }
}

/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary obj = new WordDictionary();
 * obj.addWord(word);
 * boolean param_2 = obj.search(word);
 */
```

---