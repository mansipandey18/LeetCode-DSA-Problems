# <u>2812. Find the Safest Path in a Grid</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/find-the-safest-path-in-a-grid/

---

## 🧠 Intuition:
* 🔹 The safeness of a path is determined by the **minimum distance to any thief** among all cells on that path.

* 🔹 First, use **Multi-Source BFS** starting from every thief (`1`) to compute the shortest distance of every cell to its nearest thief.

* 🔹 Store these distances in a `minDist` matrix, where a larger value means the cell is safer.

* 🔹 Next, find a path from the top-left to the bottom-right that **maximizes the minimum safeness value** along the path.

* 🔹 Use a **Max Heap (Priority Queue)** to always process the path with the highest current safeness first.

* 🔹 For each neighboring cell, the safeness of the new path becomes `min(currentPathSafeness, minDist[neighbor])`.

* 🔹 Continue exploring until the destination is reached.

* 🔹 The first time the destination is removed from the max heap, its safeness value is the maximum possible answer because the heap always prioritizes the safest path.

---

## ⏱ Time Complexity

**O(n^2 log n)**

* Multi-Source BFS takes `O(N²)`, and the Priority Queue traversal takes `O(N² log N)`.
    
---

## 📦 Space Complexity

**O(n^2)**

* For the `minDist` matrix, visited array, queue, and priority queue.

---

## 💻 Java Code

```java
class Solution {
    public int maximumSafenessFactor(List<List<Integer>> grid) {
        int N = grid.size();
        int[][] minDist = precompute(grid, N);
        PriorityQueue<int[]> maxHeap = new PriorityQueue<>((a, b) -> b[0] - a[0]);
        boolean[][] visit = new boolean[N][N];

        maxHeap.offer(new int[]{minDist[0][0], 0, 0});
        visit[0][0] = true;

        while (!maxHeap.isEmpty()) {
            int[] curr = maxHeap.poll();
            int dist = curr[0], r = curr[1], c = curr[2];

            if (r == N - 1 && c == N - 1) {
                return dist;
            }

            for (int[] dir : new int[][]{{1, 0}, {-1, 0}, {0, 1}, {0, -1}}) {
                int r2 = r + dir[0], c2 = c + dir[1];
                if (inBounds(r2, c2, N) && !visit[r2][c2]) {
                    visit[r2][c2] = true;
                    int dist2 = Math.min(dist, minDist[r2][c2]);
                    maxHeap.offer(new int[]{dist2, r2, c2});
                }
            }
        }
        return 0;
    }

    private int[][] precompute(List<List<Integer>> grid, int N) {
        int[][] minDist = new int[N][N];
        for (int[] row : minDist) Arrays.fill(row, -1);
        Queue<int[]> q = new LinkedList<>();

        for (int r = 0; r < N; r++) {
            for (int c = 0; c < N; c++) {
                if (grid.get(r).get(c) == 1) {
                    q.offer(new int[]{r, c, 0});
                    minDist[r][c] = 0;
                }
            }
        }

        while (!q.isEmpty()) {
            int[] curr = q.poll();
            int r = curr[0], c = curr[1], dist = curr[2];

            for (int[] dir : new int[][]{{1, 0}, {-1, 0}, {0, 1}, {0, -1}}) {
                int r2 = r + dir[0], c2 = c + dir[1];
                if (inBounds(r2, c2, N) && minDist[r2][c2] == -1) {
                    minDist[r2][c2] = dist + 1;
                    q.offer(new int[]{r2, c2, dist + 1});
                }
            }
        }
        return minDist;
    }

    private boolean inBounds(int r, int c, int N) {
        return r >= 0 && c >= 0 && r < N && c < N;
    }
}
```

---