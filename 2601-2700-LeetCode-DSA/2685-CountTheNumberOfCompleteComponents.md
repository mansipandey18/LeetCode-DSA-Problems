# <u>2685. Count the Number of Complete Components</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/count-the-number-of-complete-components/

---

## 🧠 Intuition:
* 🔹 Build an **adjacency list** to represent the graph.

* 🔹 Use **DFS** to traverse each unvisited connected component.

* 🔹 During DFS, keep track of:
    - **Number of nodes** in the current component.
    - **Sum of degrees** of all nodes in the component.

* 🔹 In a complete graph with **k** nodes, every node is connected to all other **k − 1 nodes**.

* 🔹 Therefore, the **total degree sum** of a complete component must be **k × (k − 1)** (since each edge contributes to the degree of both endpoints).

* 🔹 After DFS finishes for a component, compare:
    - **Degree Sum = Node Count × (Node Count − 1)**

* 🔹 If they are equal, the component is complete, so increment the answer.

* 🔹 Continue until all connected components have been processed.

---

## ⏱ Time Complexity

**O(n + m)**

* Where :
    - `n` = number of nodes
    - `m` = number of edges
    
---

## 📦 Space Complexity

**O(n + m)**

* for the adjacency list, visited array, and DFS recursion stack.

---

## 💻 Java Code

```java
class Solution {
    private List<Integer>[] adjacencyList;
    private boolean[] visited;

    public int countCompleteComponents(int n, int[][] edges) {
        adjacencyList = new List[n];
        visited = new boolean[n];
      
        Arrays.setAll(adjacencyList, index -> new ArrayList<>());
      
        for (int[] edge : edges) {
            int nodeA = edge[0];
            int nodeB = edge[1];
            adjacencyList[nodeA].add(nodeB);
            adjacencyList[nodeB].add(nodeA);
        }
      
        int completeComponentCount = 0;
      
        for (int node = 0; node < n; ++node) {
            if (!visited[node]) {
                int[] componentStats = dfs(node);
                int nodeCount = componentStats[0];
                int edgeCount = componentStats[1];
              
                if (nodeCount * (nodeCount - 1) == edgeCount) {
                    ++completeComponentCount;
                }
            }
        }
      
        return completeComponentCount;
    }

    
    private int[] dfs(int currentNode) {
        visited[currentNode] = true;
      
        int nodeCount = 1;
        int degreeSum = adjacencyList[currentNode].size();
      
        for (int neighbor : adjacencyList[currentNode]) {
            if (!visited[neighbor]) {
                int[] neighborStats = dfs(neighbor);
                nodeCount += neighborStats[0];
                degreeSum += neighborStats[1];
            }
        }
      
        return new int[] {nodeCount, degreeSum};
    }
}
```

---