# <u>3286. Find a Safe Walk Through a Grid
</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-score-from-grid-operations/

---

## 🧠 Intuition:
* 🔹 Treat each grid cell as having a **cost** (`0` or `1`) that reduces the available health when visited.

* 🔹 The goal is to find a path from the top-left to the bottom-right with the **minimum total health loss**.

* 🔹 Maintain a `minCost` matrix where `minCost[r][c]` stores the minimum health cost required to reach each cell.

* 🔹 Initialize the starting cell's cost with its own grid value.

* 🔹 Use a queue to explore all four possible directions (up, down, left, right).

* 🔹 Whenever a cheaper path to a neighboring cell is found, update its cost and add it back to the queue for further exploration.

* 🔹 Continue until all possible cost improvements have been processed.

* 🔹 Finally, if the minimum cost to reach the destination is **strictly less than the given health**, a safe walk is possible; otherwise, it is not.

---

## ⏱ Time Complexity

**O((m * n)^2)**

* In the worst case, since a cell may be relaxed and re-added to the queue multiple times.

---

## 📦 Space Complexity

**O(m * n)**

* for the `minCost` matrix and the queue.

---

## 💻 Java Code

```java
class Solution {
    public boolean findSafeWalk(List<List<Integer>> grid, int health) {
        int rows = grid.size();
        int cols = grid.get(0).size();
      
        int[][] minCost = new int[rows][cols];
        for (int[] row : minCost) {
            Arrays.fill(row, Integer.MAX_VALUE);
        }
      
        minCost[0][0] = grid.get(0).get(0);
      
        Deque<int[]> queue = new ArrayDeque<>();
        queue.offer(new int[] {0, 0});
      
        final int[] directions = {-1, 0, 1, 0, -1};
      
        while (!queue.isEmpty()) {
            int[] currentPosition = queue.poll();
            int currentRow = currentPosition[0];
            int currentCol = currentPosition[1];
          
            for (int i = 0; i < 4; i++) {
                int nextRow = currentRow + directions[i];
                int nextCol = currentCol + directions[i + 1];
              
                if (nextRow >= 0 && nextRow < rows && 
                    nextCol >= 0 && nextCol < cols &&
                    minCost[nextRow][nextCol] > minCost[currentRow][currentCol] + grid.get(nextRow).get(nextCol)) {
                  
                    minCost[nextRow][nextCol] = minCost[currentRow][currentCol] + grid.get(nextRow).get(nextCol);
                  
                    queue.offer(new int[] {nextRow, nextCol});
                }
            }
        }
      
        return minCost[rows - 1][cols - 1] < health;
    
    }
}
```

---