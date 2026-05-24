# <u>1340. Jump Game V</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/jump-game-v/

---

## 🧠 Intuition:
* 🔹 Treat each index as a starting point and try to find the maximum number of indices that can be visited.

* 🔹 Use DFS to explore all valid jumps from the current index.

* 🔹 From an index, we can jump
    - Left within distance 
    - Right within distance `d`

* 🔹 A jump is valid only if:
    - `arr[targetIndex] < arr[currentIndex]`

* 🔹 If a taller or equal-height element appears, stop searching further in that direction because jumps beyond it are not allowed.

* 🔹 For every valid jump, recursively calculate:
    - `1 + dfs(targetIndex)`

* 🔹 Keep track of the maximum reachable path length from the current index.

* 🔹 Use memoization to store already computed results and avoid repeated DFS calculations.

* 🔹 Try DFS from every index because the optimal path may start anywhere in the array.

* 🔹 Return the maximum path length among all starting positions.

---

## ⏱ Time Complexity

**O(n * d)**

* Each index explores at most `d` positions on both sides once due to memoization.
    
---

## 📦 Space Complexity

**O(n)**

* `O(n)` for memoization array
* `O(n)` recursive call stack in worst case

---

## 💻 Java Code

```java
class Solution {
    private int arrayLength;
    private int maxDistance;
    private int[] heights;
    private Integer[] memo;

    public int maxJumps(int[] arr, int d) {
        arrayLength = arr.length;
        this.maxDistance = d;
        this.heights = arr;
        memo = new Integer[arrayLength];
      
        int maxVisited = 1;
      
        // Try starting from each index and find the maximum path
        for (int startIndex = 0; startIndex < arrayLength; startIndex++) {
            maxVisited = Math.max(maxVisited, dfs(startIndex));
        }
      
        return maxVisited;
    }

    private int dfs(int currentIndex) {
        if (memo[currentIndex] != null) {
            return memo[currentIndex];
        }
      
        int maxJumpsFromHere = 1;
      
        for (int targetIndex = currentIndex - 1; targetIndex >= 0; targetIndex--) {
            if (currentIndex - targetIndex > maxDistance || heights[targetIndex] >= heights[currentIndex]) {
                break;
            }
            maxJumpsFromHere = Math.max(maxJumpsFromHere, 1 + dfs(targetIndex));
        }
      
        for (int targetIndex = currentIndex + 1; targetIndex < arrayLength; targetIndex++) {
            if (targetIndex - currentIndex > maxDistance || heights[targetIndex] >= heights[currentIndex]) {
                break;
            }
            maxJumpsFromHere = Math.max(maxJumpsFromHere, 1 + dfs(targetIndex));
        }
      
        memo[currentIndex] = maxJumpsFromHere;
        return maxJumpsFromHere;
    }
}
```

---