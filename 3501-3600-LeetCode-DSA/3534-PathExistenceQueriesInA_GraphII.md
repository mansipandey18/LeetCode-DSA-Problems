# <u>3534. Path Existence Queries in a Graph II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/path-existence-queries-in-a-graph-ii/

---

## 🧠 Intuition:
* 🔹 Sort all unique values so we can process jumps based on value differences instead of individual indices.

* 🔹 Remove duplicate values because multiple nodes with the same value behave identically while moving through the graph.

* 🔹 For every unique value, use a two-pointer technique to find the **furthest value reachable in one jump** (`difference ≤ maxDiff`).

* 🔹 Build a **Binary Lifting (Sparse Table)** where `up[d][i]` stores the position reachable after `2^d` jumps.

* 🔹 For each query:
    - If both indices are the same, the answer is `0`.
    - Normalize the direction by always moving from the smaller value to the larger value.
    - Convert both values into their positions in the sorted unique array using binary search.
    - First check if the destination is reachable by repeatedly making the largest possible jumps.
    - If it is unreachable, return `-1`.
    - Otherwise, use Binary Lifting greedily to find the **minimum number of jumps** needed to reach the destination.

* 🔹 This preprocessing allows each query to be answered much faster than simulating jumps one by one.

---

## ⏱ Time Complexity

**O(n log n + q log n)**

* Sorting and preprocessing take **O(n log n)** and each query is answered in **O(log n)**.
    
---

## 📦 Space Complexity

**O(n log n)**

* for storing the Binary Lifting table and auxiliary arrays.

---

## 💻 Java Code

```java
class Solution {
    public int[] pathExistenceQueries(int n, int[] nums, int maxDiff, int[][] queries) {
        int[] uniqueVals = Arrays.copyOf(nums, n);
        Arrays.sort(uniqueVals);
        
        int m = 0;
        for (int i = 0; i < n; i++) {
            if (m == 0 || uniqueVals[i] != uniqueVals[m - 1]) {
                uniqueVals[m++] = uniqueVals[i];
            }
        }
        
        int[] nextJump = new int[m];
        int right = 0;
        for (int left = 0; left < m; left++) {
            while (right < m && uniqueVals[right] - uniqueVals[left] <= maxDiff) {
                right++;
            }
            nextJump[left] = right - 1;
        }
        
        int LOG = 20;
        int[][] up = new int[LOG][m];
        
        for (int i = 0; i < m; i++) {
            up[0][i] = nextJump[i];
        }
        
        for (int d = 1; d < LOG; d++) {
            for (int i = 0; i < m; i++) {
                up[d][i] = up[d - 1][up[d - 1][i]];
            }
        }
        
        int numQueries = queries.length;
        int[] answer = new int[numQueries];
        
        for (int i = 0; i < numQueries; i++) {
            int u = queries[i][0];
            int v = queries[i][1];
            
            if (u == v) {
                answer[i] = 0;
                continue;
            }
            
            int valU = nums[u];
            int valV = nums[v];
            
            if (valU > valV) {
                int temp = valU;
                valU = valV;
                valV = temp;
            }
            
            int idxU = Arrays.binarySearch(uniqueVals, 0, m, valU);
            int idxV = Arrays.binarySearch(uniqueVals, 0, m, valV);
            
            int maxReach = idxU;
            for (int d = LOG - 1; d >= 0; d--) {
                maxReach = up[d][maxReach];
            }
            if (maxReach < idxV) {
                answer[i] = -1;
                continue;
            }
            
            int steps = 0;
            int curr = idxU;
            for (int d = LOG - 1; d >= 0; d--) {
                if (up[d][curr] < idxV) {
                    steps += (1 << d);
                    curr = up[d][curr];
                }
            }
            
            answer[i] = steps + 1;
        }
        
        return answer;
    
    }
}
```

---