# <u>212. Word Search II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/word-search-ii/

---

## 🧠 Intuition:
* 🔹 Searching each word separately on the board would be expensive, so first store all words in a **Trie**.

* 🔹 The Trie allows us to quickly check whether the current path on the board can still form any valid word.

* 🔹 Start a **DFS** from every cell of the board.

* 🔹 At each step:
    - Check if the current character exists as a child in the Trie.
    - If not, stop exploring this path immediately **(pruning)**.

* 🔹 Move to the corresponding Trie node and continue searching in the `4 directions (up, down, left, right)`.

* 🔹 If a Trie node contains a valid `wordIndex`, a complete word has been found:
    - Add it to the result list.
    - Set `wordIndex = -1` to avoid adding the same word multiple times.

* 🔹 Mark the current cell as visited (`'#'`) during DFS to prevent revisiting it in the same path.

* 🔹 After exploring all directions, restore the original character **(backtracking)**.

* 🔹 Combining **Trie + DFS** avoids unnecessary searches and efficiently finds all words present on the board.

---

## ⏱ Time Complexity

**O(W × L + M × N × 4ᴸ)** 

* Where:
  - `M` = number of rows.
  - `N` = number of columns.
  - `W` = number of words.
  - `L` = maximum word length.

* **Building Trie:** `O(W × L)`

* **DFS Search:**
    - In the worst case, each cell can explore up to 4 directions for a depth of L.
    - `O(M × N × 4ᴸ)`

---

## 📦 Space Complexity

**O(W * L)**

* **Trie Storage:** `O(W × L)`

* **DFS Recursion Stack:** `O(L)`

* **Result List:** `O(K)`
    - Where:
        * `K` = number of words found.

---

## 💻 Java Code

```java
class Trie {
    Trie[] children = new Trie[26];

    int wordIndex = -1;

    public void insert(String word, int index) {
        Trie currentNode = this;

        for (int i = 0; i < word.length(); i++) {
            int charIndex = word.charAt(i) - 'a';

            if (currentNode.children[charIndex] == null) {
                currentNode.children[charIndex] = new Trie();
            }

            currentNode = currentNode.children[charIndex];
        }

        currentNode.wordIndex = index;
    }
}

class Solution {
    private char[][] board;
    private String[] words;
    private List<String> result = new ArrayList<>();

    public List<String> findWords(char[][] board, String[] words) {
        this.board = board;
        this.words = words;

        Trie trieRoot = new Trie();
        for (int i = 0; i < words.length; i++) {
            trieRoot.insert(words[i], i);
        }

        int rows = board.length;
        int cols = board[0].length;

        for (int row = 0; row < rows; row++) {
            for (int col = 0; col < cols; col++) {
                dfs(trieRoot, row, col);
            }
        }

        return result;
    }

    private void dfs(Trie currentNode, int row, int col) {
        int charIndex = board[row][col] - 'a';

        if (currentNode.children[charIndex] == null) {
            return;
        }

        currentNode = currentNode.children[charIndex];

        if (currentNode.wordIndex != -1) {
            result.add(words[currentNode.wordIndex]);
            currentNode.wordIndex = -1;
        }

        char originalChar = board[row][col];
        board[row][col] = '#';

        int[] directions = {-1, 0, 1, 0, -1};

        for (int k = 0; k < 4; k++) {
            int newRow = row + directions[k];
            int newCol = col + directions[k + 1];

            if (newRow >= 0 && newRow < board.length &&
                newCol >= 0 && newCol < board[0].length &&
                board[newRow][newCol] != '#') {
                dfs(currentNode, newRow, newCol);
            }
        }

        board[row][col] = originalChar;
    }
}
```

---