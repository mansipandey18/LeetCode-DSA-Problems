# <u>2463. Minimum Total Distance Traveled</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/minimum-total-distance-traveled/

---

## 🧠 Intuition:
* 🔹 We first **sort robots and factories** so that nearby robots are matched with nearby factories (this helps minimize total distance).

* 🔹 The problem is: for each robot, decide **which factory to assign**, while respecting factory capacity.

* 🔹 At each step, we have two choices:
    - **Skip current factory** → try assigning robots to next factory
    - **Use current factory** → assign 1, 2, … up to its capacity robots

* 🔹 While assigning robots to a factory, we keep adding distance one by one (greedy accumulation).

* 🔹 After assigning some robots, we recursively solve the **remaining robots with next factories**.

* 🔹 We use **DP (memoization)** to store results of (`robotIndex, factoryIndex`) so we don’t recompute same states again.

* 🔹 Finally, we take the **minimum total distance** among all possible choices.

---

## ⏱ Time Complexity

**O(R * F * K)**

* Let : 
    - `R = number of robots`
    - `F = number of factories`
    - `K = max capacity of a factory`

* For each state (`robotIndex, factoryIndex`) → we try up to `K` assignments

---

## 📦 Space Complexity

**O(R * F)**

* DP array: `dp[R][F]`
* Recursion stack depth: up to `O(R + F)`

---

## 💻 Java Code

```java
class Solution {
    private long[][] dp;
    private List<Integer> robotPositions;
    private int[][] factoryData;

    public long minimumTotalDistance(List<Integer> robot, int[][] factory) {
        Collections.sort(robot);
        Arrays.sort(factory, (a, b) -> Integer.compare(a[0], b[0]));
      
        // Initialize instance variables
        this.robotPositions = robot;
        this.factoryData = factory;
        this.dp = new long[robot.size()][factory.length];
      
        // Start DFS from first robot and first factory
        return dfs(0, 0);
    }

    private long dfs(int robotIndex, int factoryIndex) {
        // Base case: all robots have been assigned
        if (robotIndex == robotPositions.size()) {
            return 0;
        }
      
        // Base case: no more factories available but robots remain
        if (factoryIndex == factoryData.length) {
            return Long.MAX_VALUE / 1000; // Return large value to indicate invalid path
        }
      
        // Check memoization table
        if (dp[robotIndex][factoryIndex] != 0) {
            return dp[robotIndex][factoryIndex];
        }
      
        // Option 1: Skip current factory and try next one
        long minDistance = dfs(robotIndex, factoryIndex + 1);
      
        // Option 2: Assign robots to current factory
        long currentDistance = 0;
        int factoryCapacity = factoryData[factoryIndex][1];
        int factoryPosition = factoryData[factoryIndex][0];
      
        // Try assigning k robots to current factory (k from 1 to capacity)
        for (int k = 0; k < factoryCapacity; k++) {
            // Check if we have enough robots remaining
            if (robotIndex + k >= robotPositions.size()) {
                break;
            }
          
            // Add distance for current robot to factory
            currentDistance += Math.abs(robotPositions.get(robotIndex + k) - factoryPosition);
          
            // Recursively calculate minimum distance for remaining robots and factories
            long remainingDistance = dfs(robotIndex + k + 1, factoryIndex + 1);
          
            // Update minimum distance
            minDistance = Math.min(minDistance, currentDistance + remainingDistance);
        }
      
        // Store result in memoization table
        dp[robotIndex][factoryIndex] = minDistance;
        return minDistance;
    }
}
```

---