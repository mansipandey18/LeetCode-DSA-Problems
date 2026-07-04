# <u>2492. Minimum Score of a Path Between Two Cities</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/minimum-score-of-a-path-between-two-cities/

---

## 🧠 Intuition:
* 🔹 Represent the road network as an **adjacency list**, where each city stores its neighboring cities and road distances.

* 🔹 Since the graph is connected through the path between city `1` and city `n`, the answer is the smallest edge weight in the connected component containing city `1`.

* 🔹 Start a **Depth-First Search (DFS)** from city `1` (index `0`).

* 🔹 While traversing every reachable road, continuously update the global minimum edge weight.

* 🔹 Mark each visited city to avoid revisiting it and prevent infinite recursion.

* 🔹 After the DFS finishes, the recorded minimum edge weight is the minimum possible score of any path between city `1` and city `n`.

---

## ⏱ Time Complexity

**O(n + m)**

* Where : 
    - `n` = number of cities
    - `m` = number of roads
    - `K = max capacity of a factory`

* since each city and road is visited at most once.

---

## 📦 Space Complexity

**O(n + m)**

* for the adjacency list, visited array, and DFS recursion stack.

---

## 💻 Java Code

```java
class Solution {
    private List<int[]>[] adjacencyList;
    private boolean[] visited;
    private int minimumEdgeWeight = 1 << 30;

    public int minScore(int n, int[][] roads) {
        adjacencyList = new List[n];
        visited = new boolean[n];
      
        Arrays.setAll(adjacencyList, index -> new ArrayList<>());
      
        for (int[] road : roads) {
            int nodeA = road[0] - 1;
            int nodeB = road[1] - 1;
            int edgeWeight = road[2];
          
            adjacencyList[nodeA].add(new int[] {nodeB, edgeWeight});
            adjacencyList[nodeB].add(new int[] {nodeA, edgeWeight});
        }
      
        depthFirstSearch(0);
      
        return minimumEdgeWeight;
    }

    private void depthFirstSearch(int currentNode) {
        for (int[] edge : adjacencyList[currentNode]) {
            int neighborNode = edge[0];
            int edgeWeight = edge[1];
          
            minimumEdgeWeight = Math.min(minimumEdgeWeight, edgeWeight);
          
            if (!visited[neighborNode]) {
                visited[neighborNode] = true;
                depthFirstSearch(neighborNode);
            }
        }
    }
}
```

---