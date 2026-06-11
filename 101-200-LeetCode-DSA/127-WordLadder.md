# <u>127. Word Ladder</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/word-ladder/

---

## 🧠 Intuition:
* 🔹 Treat each word as a node in a graph, where an edge exists if two words differ by exactly one character.

* 🔹 Use **BFS (Breadth-First Search)** because we need the **shortest transformation sequence**.

* 🔹 Store all words from `wordList` in a **HashSet** for O(1) lookup.

* 🔹 Start BFS from `beginWord`.

* 🔹 For each word, try changing every character position to all letters from `'a'` to `'z'`.

* 🔹 If the newly formed word exists in the set, it is a valid next transformation.

* 🔹 If the transformed word is `endWord`, return the current number of transformation steps.

* 🔹 Add valid transformed words to the queue and remove them from the set to avoid revisiting.

* 🔹 BFS guarantees that the first time we reach `endWord`, we have found the shortest path.

* 🔹 If BFS ends without finding `endWord`, return `0`.

---

## ⏱ Time Complexity

**O(N * L)**

* Where:
    - `N` = number of words in `wordList`
    - `L` = length of each word

* For each visited word:
    - Try `L` positions.
    - For each position, try `26` characters.   
    
---

## 📦 Space Complexity

**O(N)**

* HashSet stores all words: `O(N)`
* BFS queue can store up to `O(N)` words.

---

## 💻 Java Code

```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        Set<String> wordSet = new HashSet<>(wordList);
      
        Queue<String> queue = new ArrayDeque<>();
        queue.offer(beginWord);
      
        int transformationSteps = 1;
      
        while (!queue.isEmpty()) {
            transformationSteps++;
          
            int currentLevelSize = queue.size();
            for (int i = 0; i < currentLevelSize; i++) {
                String currentWord = queue.poll();
                char[] charArray = currentWord.toCharArray();
              
                for (int charIndex = 0; charIndex < charArray.length; charIndex++) {
                    char originalChar = charArray[charIndex];
                  
                    for (char newChar = 'a'; newChar <= 'z'; newChar++) {
                        charArray[charIndex] = newChar;
                        String transformedWord = new String(charArray);
                      
                        if (!wordSet.contains(transformedWord)) {
                            continue;
                        }
                      
                        if (endWord.equals(transformedWord)) {
                            return transformationSteps;
                        }
                      
                        queue.offer(transformedWord);
                      
                        wordSet.remove(transformedWord);
                    }
                  
                    charArray[charIndex] = originalChar;
                }
            }
        }
      
        return 0;
    }
}
```

---