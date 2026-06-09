# <u>909. Snakes and Ladders</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/snakes-and-ladders/

---

## 🧠 Intuition:
* 🔹 The problem is about finding the **minimum number of dice rolls** to reach the last square, which is a **shortest path problem**.

* 🔹 We model the board as a **graph where each square is a node**.

* 🔹 From each node, we can move to up to **6 next nodes (dice rolls 1 to 6)**.

* 🔹 Some positions may have **snakes or ladders**, which directly take us to another square.

* 🔹 We use **BFS (Breadth-First Search)** because it naturally finds the shortest number of moves.

* 🔹 We start from square `1` and explore all reachable positions level by level.

* 🔹 A `visited[]` array ensures we don’t revisit squares and enter cycles.

* 🔹 For each move, we convert the 1D square number into **2D board coordinates**, taking into account the zig-zag numbering of the board.

* 🔹 If we reach the final square (`n*n`), we return the number of moves taken.

* 🔹 If the queue gets empty without reaching the end, return `-1`.


---

## ⏱ Time Complexity

**O(n^2)**

* Each square is visited at most once → `O(n²)`
* Each node processes up to 6 edges → constant factor

---

## 📦 Space Complexity

**O(n^2)**

* `visited[]` array → `O(n²)`
* BFS queue → `O(n²)` in worst case

---

## 💻 Java Code

```java
class Solution {
    public int snakesAndLadders(int[][] board) {
        int boardSize = board.length;
        int totalSquares = boardSize * boardSize;
      
        Deque<Integer> queue = new ArrayDeque<>();
        queue.offer(1); // Start from square 1
      
        boolean[] visited = new boolean[totalSquares + 1];
        visited[1] = true;
      
        int moves = 0;
        while (!queue.isEmpty()) {
            int levelSize = queue.size();
          
            for (int i = 0; i < levelSize; i++) {
                int currentPosition = queue.poll();
              
                if (currentPosition == totalSquares) {
                    return moves;
                }
              
                for (int diceRoll = 1; diceRoll <= 6; diceRoll++) {
                    int nextPosition = currentPosition + diceRoll;
                  
                    if (nextPosition > totalSquares) {
                        break;
                    }
                  
                    int row = (nextPosition - 1) / boardSize;
                    int col = (nextPosition - 1) % boardSize;
                  
                    if (row % 2 == 1) {
                        col = boardSize - col - 1;
                    }
                  
                    row = boardSize - row - 1;
                  
                    int destination = board[row][col] == -1 ? nextPosition : board[row][col];
                  
                    if (!visited[destination]) {
                        visited[destination] = true;
                        queue.offer(destination);
                    }
                }
            }
            moves++;
        }
      
        return -1;
    }
}
```

---