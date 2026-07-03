# <u>3620. Network Recovery Pathways</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/network-recovery-pathways/

---

## 🧠 Intuition:
* 🔹 Ignore all edges connected to **offline nodes**, since they cannot be part of any valid path.

* 🔹 Collect all unique edge costs and sort them, because the answer must be one of these costs.

* 🔹 Use **Binary Search** on the possible minimum edge cost (path score).

* 🔹 For each candidate score:
    - Keep only the edges whose cost is **greater than or equal to** the candidate score.
    - Build a graph using these filtered edges.

* 🔹 Since the graph is a **DAG**, use **Kahn's Algorithm (Topological Sort)** to process nodes in dependency order.

* 🔹 During the topological traversal, use **Dynamic Programming** to compute the minimum total path cost from node `0` to every other node.

* 🔹 If the destination node can be reached within the given budget k, the current score is feasible, so try a **larger minimum edge cost**.

* 🔹 Otherwise, reduce the candidate score using Binary Search.

* 🔹 The largest feasible minimum edge cost is the final answer.

---

## ⏱ Time Complexity

**O((E + V) × log E)**

* Binary Search over unique edge costs, and each check performs graph construction plus Topological Sort.

---

## 📦 Space Complexity

**O(E + V)**

* For the adjacency list, in-degree array, DP array, queue, and filtered edge storage.

---

## 💻 Java Code

```java
class Solution {
    public int findMaxPathScore(int[][] edges, boolean[] online, long k) {
        int n = online.length;
        
        // 1. Filter out edges connected to offline nodes and collect unique costs
        List<int[]> filteredEdges = new ArrayList<>();
        TreeSet<Integer> uniqueCosts = new TreeSet<>();
        
        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];
            int cost = edge[2];
            if (online[u] && online[v]) {
                filteredEdges.add(edge);
                uniqueCosts.add(cost);
            }
        }
        
        // Convert to primitive array for quick binary search access
        int[] sortedCosts = new int[uniqueCosts.size()];
        int idx = 0;
        for (int cost : uniqueCosts) {
            sortedCosts[idx++] = cost;
        }
        
        // 2. Perform Binary Search on the unique cost indices
        int low = 0, high = sortedCosts.length - 1;
        int ans = -1;
        
        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (canReachWithMinScore(n, filteredEdges, sortedCosts[mid], k)) {
                ans = sortedCosts[mid]; // Current min score is viable, try to find a larger one
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }
        
        return ans;
    }
    
    private boolean canReachWithMinScore(int n, List<int[]> edges, int minAllowedCost, long maxBudget) {
        // Build graph with adjacency list and calculate in-degrees
        List<List<int[]>> adj = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            adj.add(new ArrayList<>());
        }
        
        int[] inDegree = new int[n];
        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];
            int cost = edge[2];
            
            // Only consider edges meeting or exceeding our candidate score
            if (cost >= minAllowedCost) {
                adj.get(u).add(new int[]{v, cost});
                inDegree[v]++;
            }
        }
        
        // Kahn's algorithm setup for Topological Sorting
        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            if (inDegree[i] == 0) {
                queue.offer(i);
            }
        }
        
        // DP array to record the minimum cost path to each node
        long[] minCostTo = new long[n];
        Arrays.fill(minCostTo, Long.MAX_VALUE);
        minCostTo[0] = 0L;
        
        while (!queue.isEmpty()) {
            int curr = queue.poll();
            long currDist = minCostTo[curr];
            
            for (int[] neighborInfo : adj.get(curr)) {
                int neighbor = neighborInfo[0];
                int weight = neighborInfo[1];
                
                // If current node is reachable, relax the destination edge
                if (currDist != Long.MAX_VALUE) {
                    if (currDist + weight < minCostTo[neighbor]) {
                        minCostTo[neighbor] = currDist + weight;
                    }
                }
                
                inDegree[neighbor]--;
                if (inDegree[neighbor] == 0) {
                    queue.offer(neighbor);
                }
            }
        }
        
        // Check if destination is reachable within the specified budget constraint
        return minCostTo[n - 1] <= maxBudget;
    }
}
```

---