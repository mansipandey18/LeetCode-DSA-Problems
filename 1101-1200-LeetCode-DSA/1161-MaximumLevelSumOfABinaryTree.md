# <u>1161. Maximum Level Sum of a Binary Tree</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-level-sum-of-a-binary-tree/

---

## 🧠 Intuition:
* 🔹 The problem asks for the level in the binary tree having the **maximum sum of node values**

* 🔹 Use **Level Order Traversal (BFS)** to process the tree level by level

* 🔹 A queue is used to store nodes of the current level

* 🔹 Start from level `1` and traverse all nodes level-wise

* 🔹 For each level:
    - Initialize `levelSum = 0`
    - Process all nodes currently in the queue (`q.size()`)
    - Add every node’s value to `levelSum`
    - Push the left and right children into the queue for the next level

* 🔹 After finishing one level:
    - Compare `levelSum` with `maxLevelSum`
    - If the current level sum is greater, update:
        * `maxLevelSum`
        * `ans = current level number`

* 🔹 Continue until the queue becomes empty

* 🔹 Return the level number having the maximum sum

---

## ⏱ Time Complexity

**O(n)**

* Where:
    - `n` = number of nodes in the tree

* Every node is visited exactly once during BFS traversal
    
---

## 📦 Space Complexity

**O(n)**

* Queue stores nodes level by level
* In the worst case, the queue may contain all nodes of the widest level

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
    public int maxLevelSum(TreeNode root) {
        int ans = 0;
        int maxLevelSum = Integer.MIN_VALUE;
        Queue<TreeNode> q = new LinkedList<>(Arrays.asList(root));

        for (int level = 1; !q.isEmpty(); ++level) {
            int levelSum = 0;
            for (int sz = q.size(); sz > 0; --sz) {
                TreeNode node = q.poll();
                levelSum += node.val;
                if (node.left != null)
                    q.offer(node.left);
                if (node.right != null)
                    q.offer(node.right);
            }
            if (levelSum > maxLevelSum) {
                maxLevelSum = levelSum;
                ans = level;
            }
        }

        return ans;
    }
}
```

---