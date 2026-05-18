# <u>1345. Jump Game IV</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/jump-game-iv/

---

## 🧠 Intuition:
* 🔹 Treat each index as a node in a graph.

* 🔹 From any index i, we can jump to:
    - `i - 1`
    - `i + 1`
    - Any index having the same value as `arr[i]`

* 🔹 Since we need the minimum number of jumps, use BFS because BFS guarantees the shortest path in an unweighted graph.

* 🔹 Store all indices of the same value in a HashMap:
    * `value -> list of indices`

* 🔹 Start BFS from index `0`.

* 🔹 Use a `visited` array to avoid revisiting indices.

* 🔹 At every BFS level:
    - Process all reachable indices in the current number of jumps.
    - If we reach the last index, return the current step count.

* 🔹 For each current index:
    - Visit all indices with the same value.
    - Visit adjacent indices (`i-1` and `i+1`).

* 🔹 After processing same-value jumps once, clear the list:
    - Prevents repeated traversal of the same group.
    - This optimization avoids TLE and keeps complexity linear.


---

## ⏱ Time Complexity

**O(n)**

* Each index and each same-value group is processed at most once.
    
---

## 📦 Space Complexity

**O(n)**

* HashMap, visited array, and BFS queue together use linear space.

---

## 💻 Java Code

```java
class Solution {
    public int minJumps(int[] arr) {
        Map<Integer, List<Integer>> valueToIndicesMap = new HashMap<>();
        int arrayLength = arr.length;
      
        // Populate the map with all indices for each value
        for (int index = 0; index < arrayLength; index++) {
            valueToIndicesMap.computeIfAbsent(arr[index], k -> new ArrayList<>()).add(index);
        }
      
        // Track visited indices to avoid revisiting
        boolean[] visited = new boolean[arrayLength];
      
        // BFS queue to store indices to process
        Deque<Integer> queue = new ArrayDeque<>();
      
        // Start BFS from index 0
        queue.offer(0);
        visited[0] = true;
      
        // BFS to find minimum steps to reach the last index
        for (int steps = 0; ; steps++) {
            // Process all nodes at current level
            int currentLevelSize = queue.size();
            for (int i = 0; i < currentLevelSize; i++) {
                int currentIndex = queue.poll();
              
                // Check if we've reached the target (last index)
                if (currentIndex == arrayLength - 1) {
                    return steps;
                }
              
                // Jump to all indices with the same value
                List<Integer> sameValueIndices = valueToIndicesMap.get(arr[currentIndex]);
                for (int nextIndex : sameValueIndices) {
                    if (!visited[nextIndex]) {
                        visited[nextIndex] = true;
                        queue.offer(nextIndex);
                    }
                }
              
                // Clear the list to avoid redundant checks in future iterations
                // This optimization prevents revisiting the same value group
                sameValueIndices.clear();
              
                // Jump to adjacent indices (left and right)
                for (int nextIndex : new int[] {currentIndex - 1, currentIndex + 1}) {
                    if (nextIndex >= 0 && nextIndex < arrayLength && !visited[nextIndex]) {
                        visited[nextIndex] = true;
                        queue.offer(nextIndex);
                    }
                }
            }
        }
    }
}
```

---