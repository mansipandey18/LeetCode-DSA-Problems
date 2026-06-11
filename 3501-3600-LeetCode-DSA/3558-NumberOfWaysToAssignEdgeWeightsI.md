# <u>3558. Number of Ways to Assign Edge Weights I</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/number-of-ways-to-assign-edge-weights-i/

---

## 🧠 Intuition:
* 🔹 Treat the given edges as a tree and build an adjacency list for easy traversal.

* 🔹 Start a **BFS from node 1** (the root) to find the depth of every node.

* 🔹 Keep track of the **maximum depth** reached during the traversal.

* 🔹 The deepest node determines the longest root-to-node path in the tree.

* 🔹 Based on the problem's observation, the number of valid edge-weight assignments depends only on this maximum depth.

* 🔹 If the maximum depth is `d`, the answer becomes **2^(d - 1)**.

* 🔹 Since the result can be very large, compute it using **fast modular exponentiation** with modulo `10^9 + 7`.

* 🔹 Fast exponentiation reduces the power calculation from linear time to logarithmic time.

---

## ⏱ Time Complexity

**O(n + log n)**

* Building adjacency list: `O(n)
* BFS traversal: `O(n)`
* Fast exponentiation: `O(log n)`
    
---

## 📦 Space Complexity

**O(n)**

* Adjacency list: `O(n)
* Visited array: `O(n)`
* BFS queue: `O(n)`

---

## 💻 Java Code

```java
class Solution {
    public int assignEdgeWeights(int[][] edges) {
        int n = edges.length + 1;
        
        // Build the adjacency list for the tree
        List<List<Integer>> graph = new ArrayList<>(n + 1);
        for (int i = 0; i <= n; i++) {
            graph.add(new ArrayList<>());
        }
        for (int[] edge : edges) {
            graph.get(edge[0]).add(edge[1]);
            graph.get(edge[1]).add(edge[0]);
        }
        
        // Traverse the tree using BFS to discover the maximum edge depth
        int maxDepth = 0;
        Queue<int[]> queue = new LinkedList<>();
        boolean[] visited = new boolean[n + 1];
        
        // Enqueue root element: {node_id, current_edge_count}
        queue.offer(new int[]{1, 0});
        visited[1] = true;
        
        while (!queue.isEmpty()) {
            int[] current = queue.poll();
            int u = current[0];
            int depth = current[1];
            
            maxDepth = Math.max(maxDepth, depth);
            
            for (int v : graph.get(u)) {
                if (!visited[v]) {
                    visited[v] = true;
                    queue.offer(new int[]{v, depth + 1});
                }
            }
        }
        
        // Result calculation: 2^(maxDepth - 1) % 1000000007
        long MOD = 1_000_000_007;
        return (int) power(2, maxDepth - 1, MOD);
    }

    private long power(long base, long exp, long mod) {
        long result = 1;
        base %= mod;
        while (exp > 0) {
            if (exp % 2 == 1) {
                result = (result * base) % mod;
            }
            base = (base * base) % mod;
            exp /= 2;
        }
        return result;
    }
}
```

---