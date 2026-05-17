# <u>1926. Nearest Exit from Entrance in Maze</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/nearest-exit-from-entrance-in-maze/

---

## 🧠 Intuition:
* 🔹 Treat the maze as a graph where each empty cell `'.'` is a node.

* 🔹 Use BFS because BFS always finds the shortest path in an unweighted grid.

* 🔹 Start BFS from the entrance cell.

* 🔹 Mark the entrance as visited (`'+'`) to avoid revisiting it.

* 🔹 Explore all 4 possible directions using the `directions` array.

* 🔹 For every valid neighboring empty cell:
    - If it lies on the boundary of the maze, it is the nearest exit → return current distance.
    - Otherwise, mark it visited and push it into the queue for further exploration.

* 🔹 BFS processes cells level by level, so the first exit found is guaranteed to be the minimum number of steps.

* 🔹 If BFS finishes without reaching any boundary cell, return `-1`.

---

## ⏱ Time Complexity

**O(m x n)**

* Each cell is visited at most once.

---

## 📦 Space Complexity

**O(m x n)**

* Queue can store all cells in the worst case.

---

## 💻 Java Code

```java
class Solution {
    public int nearestExit(char[][] maze, int[] entrance) {
        int rows = maze.length;
        int cols = maze[0].length;
        final int[] directions = {-1, 0, 1, 0, -1};
      
        Deque<int[]> queue = new ArrayDeque<>();
        queue.offer(entrance);
      
        maze[entrance[0]][entrance[1]] = '+';
      
        for (int distance = 1; !queue.isEmpty(); distance++) {
            int currentLevelSize = queue.size();
          
            for (int i = 0; i < currentLevelSize; i++) {
                int[] currentPosition = queue.poll();
              
                for (int dir = 0; dir < 4; dir++) {
                    int newRow = currentPosition[0] + directions[dir];
                    int newCol = currentPosition[1] + directions[dir + 1];
                  
                    if (newRow >= 0 && newRow < rows && 
                        newCol >= 0 && newCol < cols && 
                        maze[newRow][newCol] == '.') {
                      
                        if (newRow == 0 || newRow == rows - 1 || 
                            newCol == 0 || newCol == cols - 1) {
                            return distance;
                        }
                      
                        maze[newRow][newCol] = '+';
                        queue.offer(new int[] {newRow, newCol});
                    }
                }
            }
        }
      
        return -1;
    
    }
}
```

---