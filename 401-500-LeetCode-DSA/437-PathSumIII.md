# <u>437. Path Sum III</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/path-sum-iii/

---

## 🧠 Intuition:
* 🔹 The problem is to count the number of **paths in a binary tree whose sum equals** `targetSum`

* 🔹 Paths must go **downward** (`parent → child`), but can start and end at any node

* 🔹 Instead of checking all paths (which is costly), we use the **prefix sum technique (similar to subarray sum)**

* 🔹 Maintain a running sum `currentPrefixSum` from root to the current node

* 🔹 Use a HashMap `prefixSumCount` to store how many times a prefix sum has occurred

* 🔹 Key idea:
    - If `currentPrefixSum - targetSum` exists in the map, it means there is a previous prefix that forms a valid path

* 🔹 For each node:
    - Add node value to `currentPrefixSum`
    - Check how many times `(currentPrefixSum - targetSum)` appeared → add to answer
    - Store current prefix sum in the map

* 🔹 Recursively process left and right subtrees

* 🔹 After returning from recursion (backtracking):
    - Decrease the count of current prefix sum in the map
    - This ensures correct results for different paths (avoid mixing paths)

* 🔹 Initialize map with `{0:1}` to handle paths starting from root

* 🔹 This approach efficiently counts all valid paths without recomputing sums repeatedly

---

## ⏱ Time Complexity

**O(n)**

* Where :
    - `n` = number of nodes

* Each node is visited once
* HashMap operations are **O(1)** on average
    
---

## 📦 Space Complexity

**O(h)**

* HashMap stores prefix sums along the path

* Recursion stack

* Worst case (skewed tree): **O(n)**
* Best case (balanced tree): **O(log n)**

---

## 💻 Java Code

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {

    private Map<Long, Integer> prefixSumCount = new HashMap<>();
    private int targetSum;

    public int pathSum(TreeNode root, int targetSum) {
        prefixSumCount.put(0L, 1);
        this.targetSum = targetSum;
      
        return dfs(root, 0);
    }

    private int dfs(TreeNode node, long currentPrefixSum) {
        if (node == null) {
            return 0;
        }
      
        currentPrefixSum += node.val;
      
        int pathCount = prefixSumCount.getOrDefault(currentPrefixSum - targetSum, 0);
      
        prefixSumCount.merge(currentPrefixSum, 1, Integer::sum);
      
        pathCount += dfs(node.left, currentPrefixSum);
        pathCount += dfs(node.right, currentPrefixSum);
      
        prefixSumCount.merge(currentPrefixSum, -1, Integer::sum);
      
        return pathCount;
    }
}   
```

---