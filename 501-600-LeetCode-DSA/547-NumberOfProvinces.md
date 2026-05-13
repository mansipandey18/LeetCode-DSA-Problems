# <u>547. Number of Provinces</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/number-of-provinces/

---

## 🧠 Intuition:
* 🔹 Treat each city as a node in a graph, where `isConnected[i][j] = 1` means there is a direct connection between city `i` and city `j`.

* 🔹 The problem reduces to finding the number of connected components (provinces) in the graph.

* 🔹 Use a `visited` array to keep track of cities that are already explored.

* 🔹 Traverse every city:
    - If a city is not visited, start a DFS from it.
    - DFS marks all cities reachable from that city as visited.

* 🔹 Every new DFS call represents discovering a new province.

* 🔹 Inside DFS:
    - Mark the current city as visited.
    - Explore all neighboring cities connected to it.
    - Recursively visit unvisited connected cities.

* 🔹 Finally, the number of DFS starts equals the total number of provinces.

---

## ⏱ Time Complexity

**O(n^2)**

* For every city, DFS checks all possible neighboring cities using the adjacency matrix.
    
---

## 📦 Space Complexity

**O(n)**

* `visited` array takes `O(n)` space.
* Recursive DFS call stack can go up to `O(n)` in the worst case.

---

## 💻 Java Code

```java
class Solution {
    private int[][] graph;
    private boolean[] visited;

    public int findCircleNum(int[][] isConnected) {
        graph = isConnected;
        int n = graph.length;
        visited = new boolean[n];
      
        int provinceCount = 0;
      
        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                dfs(i);
                provinceCount++;
            }
        }
      
        return provinceCount;
    }

    private void dfs(int currentCity) {
        visited[currentCity] = true;
      
        for (int nextCity = 0; nextCity < graph.length; nextCity++) {
            if (!visited[nextCity] && graph[currentCity][nextCity] == 1) {
                dfs(nextCity);
            }
        }
    }
}
```

---