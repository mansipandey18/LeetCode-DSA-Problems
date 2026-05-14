# <u>1466. Reorder Routes to Make All Paths Lead to the City Zero</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/reorder-routes-to-make-all-paths-lead-to-the-city-zero/

---

## 🧠 Intuition:
* 🔹 Treat the cities and roads as a graph problem where every city must be able to reach city `0`.

* 🔹 For every directed road `a -> b`, store:
    - `(b, 1)` from `a` meaning this road is going away from city `0` and may need reversal.
    - `(a, 0)` from `b` meaning this direction is already correct toward city `0`.

* 🔹 Start DFS from city `0` and traverse all connected cities.

* 🔹 While visiting neighbors:
    - If an edge has value `1`, it means the road direction is wrong and must be reversed.
    - Add this reversal cost to the answer.

* 🔹 Continue DFS recursively for all unvisited neighboring cities.

* 🔹 Since the graph is a tree (`n-1 edges`), every city is visited exactly once.

* 🔹 The total reversals counted during traversal give the minimum number of roads to reorder.

---

## ⏱ Time Complexity

**O(n)**

* Each city and road is visited once during DFS.
    
---

## 📦 Space Complexity

**O(n)**

* Adjacency list + recursion stack take linear space.

---

## 💻 Java Code

```java
class Solution {
    private List<int[]>[] adjacencyList;

    public int minReorder(int n, int[][] connections) {
        adjacencyList = new List[n];
        Arrays.setAll(adjacencyList, index -> new ArrayList<>());
      
        for (int[] connection : connections) {
            int fromNode = connection[0];
            int toNode = connection[1];
          
            adjacencyList[fromNode].add(new int[] {toNode, 1});
          
            adjacencyList[toNode].add(new int[] {fromNode, 0});
        }
      
        return dfs(0, -1);
    }

    private int dfs(int currentNode, int parentNode) {
        int reversalCount = 0;
      
        for (int[] edge : adjacencyList[currentNode]) {
            int neighborNode = edge[0];
            int needsReversal = edge[1];
          
            if (neighborNode != parentNode) {
                reversalCount += needsReversal + dfs(neighborNode, currentNode);
            }
        }
      
        return reversalCount;
    }
}
```

---