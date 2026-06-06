# <u>133. Clone Graph</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/clone-graph/

---

## 🧠 Intuition:
* 🔹 The problem is to create a **deep copy of an undirected graph**, where each node and its connections must be duplicated.

* 🔹 We use **DFS traversal** to visit each node in the graph.

* 🔹 A HashMap `visited` is used to keep track of already cloned nodes:
    - Key → original node
    - Value → cloned node

* 🔹 If a node is already cloned, we directly return its copy to avoid **reprocessing and infinite loops in cycles**.

* 🔹 For each unvisited node:
    - Create a new cloned node with the same value.
    - Store it in the map.
    - Recursively clone all its neighbors and add them to the cloned node’s adjacency list.

* 🔹 This ensures:
    - Each node is cloned exactly once.
    - All edges (connections) are preserved correctly.

---

## ⏱ Time Complexity

**O(V + E)**

* Where:
    - `V` = number of vertices
    - `E` = number of edges

* Each node and edge is visited once during DFS.

---

## 📦 Space Complexity

**O(V)**

* HashMap stores all cloned nodes → `O(V)`
* Recursion stack in worst case (DFS depth) → `O(V)`

---

## 💻 Java Code

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> neighbors;
    public Node() {
        val = 0;
        neighbors = new ArrayList<Node>();
    }
    public Node(int _val) {
        val = _val;
        neighbors = new ArrayList<Node>();
    }
    public Node(int _val, ArrayList<Node> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
}
*/

class Solution {
    private Map<Node, Node> visited = new HashMap<>();
    public Node cloneGraph(Node node) {
        if (node == null) {
            return null;
        }
        if (visited.containsKey(node)) {
            return visited.get(node);
        }
        Node clone = new Node(node.val);
        visited.put(node, clone);
        for (Node e : node.neighbors) {
            clone.neighbors.add(cloneGraph(e));
        }
        return clone;
    }
}
```

---