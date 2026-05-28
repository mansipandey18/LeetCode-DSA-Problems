# <u>637. Average of Levels in Binary Tree</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/average-of-levels-in-binary-tree/

---

## 🧠 Intuition:
* 🔹 Use **Breadth-First Search (BFS)** / level-order traversal to process the tree level by level.

* 🔹 A queue helps keep track of nodes for the current level.

* 🔹 For every level:
    - Store the number of nodes using `levelSize`.
    - Traverse all nodes of that level.
    - Add their values to `levelSum`.

* 🔹 While processing nodes:
    - Push left child into the queue if it exists.
    - Push right child into the queue if it exists.

* 🔹 After finishing one level:
    - Compute the average using `levelSum / levelSize`.
    - Store the result in the answer list.

* 🔹 `long` is used for `levelSum` to avoid integer overflow when node values are large.

* 🔹 Continue until the queue becomes empty, meaning all levels are processed.

---

## ⏱ Time Complexity

**O(n)**

* Every node is visited exactly once.
 
---

## 📦 Space Complexity

**O(w)**

* Queue stores at most the maximum width of the binary tree.

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
    public List<Double> averageOfLevels(TreeNode root) {
        // List to store the average value of each level
        List<Double> averagesList = new ArrayList<>();
      
        // Queue for BFS traversal
        Deque<TreeNode> queue = new ArrayDeque<>();
      
        // Start BFS from the root node
        queue.offer(root);
      
        // Process each level of the tree
        while (!queue.isEmpty()) {
            // Get the number of nodes at the current level
            int levelSize = queue.size();
          
            // Use long to prevent integer overflow when summing large values
            long levelSum = 0;
          
            // Process all nodes at the current level
            for (int i = 0; i < levelSize; i++) {
                // Remove and process the next node from the queue
                TreeNode currentNode = queue.pollFirst();
              
                // Add current node's value to the level sum
                levelSum += currentNode.val;
              
                // Add left child to queue for next level processing
                if (currentNode.left != null) {
                    queue.offer(currentNode.left);
                }
              
                // Add right child to queue for next level processing
                if (currentNode.right != null) {
                    queue.offer(currentNode.right);
                }
            }
          
            // Calculate and store the average for this level
            // Convert to double by multiplying by 1.0
            averagesList.add(levelSum * 1.0 / levelSize);
        }
      
        return averagesList;
    }
}   
```

---