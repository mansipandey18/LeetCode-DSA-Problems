# <u>3559. Number of Ways to Assign Edge Weights II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/number-of-ways-to-assign-edge-weights-ii/

---

## 🧠 Intuition:
* 🔹 The tree is represented as an **adjacency list** for efficient traversal.

* 🔹 Perform a DFS/BFS from node `1` to compute:
    - The **depth** of every node.
    - The **immediate parent** of every node.

* 🔹 Build a **Binary Lifting (LCA) table** (`up`) where `up[k][v]` stores the 2ᵏ-th ancestor of node `v`.

* 🔹 For each query `(u, v)`, find their **Lowest Common Ancestor (LCA)** using binary lifting.

* 🔹 The number of edges on the path between `u` and `v` is:
    - `pathLength = depth[u] + depth[v] - 2 * depth[LCA]`

* 🔹 Based on the problem observation:
    - If `pathLength = 0`, there are no edges on the path, so the answer is `0`.
    - Otherwise, the number of valid assignments is 2^(pathLength - 1).

* 🔹 Precompute all required powers of 2 modulo `10^9 + 7` to answer queries efficiently.

* 🔹 For each query:
    - Find the LCA.
    - Compute the path length.
    - Return the precomputed value `2^(pathLength - 1)`.

---

## ⏱ Time Complexity

**O(N log N + Q log N)**

* Building adjacency list: `O(N)`
* BFS/DFS to compute depth and parent: `O(N)`
* Building Binary Lifting table: `O(N log N)`
* Each LCA query: `O(log N)`
* Processing `Q` queries: `O(Q log N)`
    
---

## 📦 Space Complexity

**O(N log N + Q)**

* Adjacency list: `O(N)`
* Depth array: `O(N)`
* Binary Lifting table: `O(N log N)`
* Visited/auxiliary arrays: `O(N)`
* Answer array: `O(Q)`

---

## 💻 Java Code

```java
class Solution {
    static final long MOD = 1_000_000_007L;

    public int[] assignEdgeWeights(int[][] edges, int[][] queries) {
        int n = edges.length + 1;

        int[] deg = new int[n + 1];
        for (int[] e : edges) {
            deg[e[0]]++;
            deg[e[1]]++;
        }

        int[][] g = new int[n + 1][];
        for (int i = 1; i <= n; i++) {
            g[i] = new int[deg[i]];
        }

        int[] idx = new int[n + 1];
        for (int[] e : edges) {
            int u = e[0], v = e[1];
            g[u][idx[u]++] = v;
            g[v][idx[v]++] = u;
        }

        int LOG = 1;
        while ((1 << LOG) <= n) LOG++;

        int[][] up = new int[LOG][n + 1];
        int[] depth = new int[n + 1];

        int[] stack = new int[n];
        int top = 0;
        stack[top++] = 1;
        boolean[] vis = new boolean[n + 1];
        vis[1] = true;

        while (top > 0) {
            int u = stack[--top];

            for (int v : g[u]) {
                if (!vis[v]) {
                    vis[v] = true;
                    depth[v] = depth[u] + 1;
                    up[0][v] = u;
                    stack[top++] = v;
                }
            }
        }

        for (int k = 1; k < LOG; k++) {
            for (int v = 1; v <= n; v++) {
                up[k][v] = up[k - 1][up[k - 1][v]];
            }
        }

        int maxLen = 0;
        for (int[] q : queries) {
            int u = q[0], v = q[1];
            int lca = lca(u, v, up, depth, LOG);
            maxLen = Math.max(maxLen, depth[u] + depth[v] - 2 * depth[lca]);
        }

        long[] pow2 = new long[Math.max(1, maxLen + 1)];
        pow2[0] = 1;
        for (int i = 1; i <= maxLen; i++) {
            pow2[i] = (pow2[i - 1] * 2) % MOD;
        }

        int[] ans = new int[queries.length];

        for (int i = 0; i < queries.length; i++) {
            int u = queries[i][0];
            int v = queries[i][1];

            int lca = lca(u, v, up, depth, LOG);
            int len = depth[u] + depth[v] - 2 * depth[lca];

            if (len == 0) {
                ans[i] = 0;
            } else {
                ans[i] = (int) pow2[len - 1];
            }
        }

        return ans;
    }

    private int lca(int a, int b, int[][] up, int[] depth, int LOG) {
        if (depth[a] < depth[b]) {
            int t = a;
            a = b;
            b = t;
        }

        int diff = depth[a] - depth[b];

        for (int k = 0; k < LOG; k++) {
            if (((diff >> k) & 1) != 0) {
                a = up[k][a];
            }
        }

        if (a == b) return a;

        for (int k = LOG - 1; k >= 0; k--) {
            if (up[k][a] != up[k][b]) {
                a = up[k][a];
                b = up[k][b];
            }
        }

        return up[0][a];
    }
}
```

---