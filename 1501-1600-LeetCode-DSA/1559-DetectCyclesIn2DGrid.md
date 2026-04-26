# <u>1559. Detect Cycles in 2D Grid</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/detect-cycles-in-2d-grid/

---

## 🧠 Intuition:
* 🔹 We need to detect whether there exists a **cycle of same characters** in the grid, where movement is allowed only in 4 directions (`up, down, left, right`)

* 🔹 A cycle exists if during traversal we reach an already visited cell that is **not the immediate parent** of the current cell

* 🔹 Use **BFS (Breadth First Search)** starting from every unvisited cell to explore connected cells having the same character

* 🔹 Maintain a `visited[][]` matrix so each cell is processed only once

* 🔹 For each BFS node, store:
    - current cell position `(x, y)`
    - parent cell position `(parentX, parentY)`

* 🔹 While exploring neighbors:
    - Ignore out-of-bound cells
    - Ignore cells with different characters
    - Ignore the parent cell because going back to parent is normal, not a cycle

* 🔹 If we find a neighbor with the same character that is already visited and is not the parent, then a cycle is found → return `true`

* 🔹 If BFS finishes for all components without finding such a case, return `false`

* 🔹 This works because BFS explores connected components level by level while tracking parent relationships correctly


---

## ⏱ Time Complexity

**O(rows × cols)**

* Each cell is visited at most once
* For every cell, we check 4 directions

---

## 📦 Space Complexity

**O(rows × cols)**

* `visited[][]` matrix takes **O(rows × cols)**
* BFS queue may also store up to all cells in worst case

---

## 💻 Java Code

```java
class Solution {
    public boolean containsCycle(char[][] grid) {
        int rows = grid.length;
        int cols = grid[0].length;
        boolean[][] visited = new boolean[rows][cols];
      
        // Direction vectors for moving up, right, down, left
        final int[] directions = {-1, 0, 1, 0, -1};
      
        // Check each cell as a potential starting point for a cycle
        for (int row = 0; row < rows; row++) {
            for (int col = 0; col < cols; col++) {
                if (!visited[row][col]) {
                    // BFS to detect cycle starting from current cell
                    Deque<int[]> queue = new ArrayDeque<>();
                    // Store current position and parent position (x, y, parentX, parentY)
                    queue.offer(new int[] {row, col, -1, -1});
                    visited[row][col] = true;
                  
                    while (!queue.isEmpty()) {
                        int[] current = queue.poll();
                        int currentX = current[0];
                        int currentY = current[1];
                        int parentX = current[2];
                        int parentY = current[3];
                      
                        // Explore all 4 directions
                        for (int k = 0; k < 4; k++) {
                            int nextX = currentX + directions[k];
                            int nextY = currentY + directions[k + 1];
                          
                            // Check if next position is within bounds
                            if (nextX >= 0 && nextX < rows && nextY >= 0 && nextY < cols) {
                                // Skip if different character or if it's the parent cell
                                if (grid[nextX][nextY] != grid[currentX][currentY] || 
                                    (nextX == parentX && nextY == parentY)) {
                                    continue;
                                }
                              
                                // If we've visited this cell before, we found a cycle
                                if (visited[nextX][nextY]) {
                                    return true;
                                }
                              
                                // Mark as visited and add to queue with current cell as parent
                                queue.offer(new int[] {nextX, nextY, currentX, currentY});
                                visited[nextX][nextY] = true;
                            }
                        }
                    }
                }
            }
        }
      
        return false;
    }
}
```

---