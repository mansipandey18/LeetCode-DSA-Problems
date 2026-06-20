# <u>79. Word Search</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/word-search/

---

## 🧠 Intuition:
* 🔹 The problem requires finding whether the given word can be formed by moving horizontally or vertically through adjacent cells.

* 🔹 Use **Backtracking + DFS** to explore all possible paths starting from cells that match the first character of the word.

* 🔹 Traverse the board and start DFS whenever a cell matches the first character.

* 🔹 During DFS:
    - Check boundary conditions, whether the cell is already visited, or whether the current character matches the required character of the word.
    - If the last character of the word is matched, return `true` because a valid path is found.

* 🔹 Mark the current cell as visited by replacing its character with `'*'` to avoid using the same cell multiple times in the current path.

* 🔹 Recursively explore all four possible directions:
    - Up, Down, Left, and Right.

* 🔹 After exploring all directions, restore the original character (**backtracking**) so that the cell can be used in other possible paths.

* 🔹 If any recursive path returns `true`, the word exists in the board; otherwise, continue checking other starting positions.

* 🔹 This approach explores all possible valid paths while avoiding revisiting cells in the same search path.

---

## ⏱ Time Complexity

**O(M × N × 3^(L-1))**

* Where: 
    - `m` = number of rows in the board
    - `n` = number of columns in the board
    - `L` = length of the word

* For each cell, DFS can explore up to 4 directions initially and at most 3 directions afterward (excluding the previously visited cell).

---

## 📦 Space Complexity

**O(L)**

* Due to the recursion call stack, where L is the length of the word.

---

## 💻 Java Code

```java
class Solution {
    public static boolean isExists(char board[][], int i, int j, char word[], int num) {
        if(i < 0 || i >=board.length || j < 0 || j >= board[0].length || board[i][j] == '*' || board[i][j] != word[num]){
            return false;
        }

        if(num == word.length-1){
            return true;
        }

        char ch = board[i][j];
        board[i][j] = '*';

        boolean ans = isExists(board, i-1, j, word, num+1) || isExists(board, i+1, j, word, num+1) || isExists(board, i, j-1, word, num+1) || isExists(board, i, j+1, word, num+1);

        board[i][j] = ch;
        
        return ans;    
    }
    public boolean exist(char[][] board, String word) {
        char arr[] = word.toCharArray();

        for(int i = 0; i < board.length; i++){
            for (int j = 0; j < board[0].length; j++){
                if (board[i][j] == arr[0] && isExists(board, i, j, arr, 0)) {
                    return true;
                }
            }
        }
        return false;
    }
}
```

---