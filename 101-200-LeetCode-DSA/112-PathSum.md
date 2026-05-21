# <u>112. Path Sum</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/flatten-binary-tree-to-linked-list/

---

## 🧠 Intuition:
* 🔹 Use DFS traversal to explore every root-to-leaf path in the binary tree.

* 🔹 At each node, subtract the node’s value from the remaining target sum.

* 🔹 This means the remaining sum always represents how much more is needed to reach the target.

* 🔹 If we reach a leaf node and the remaining sum becomes 0, then a valid path exists.

* 🔹 Recursively check both left and right subtrees for a possible valid path.

* 🔹 If either subtree returns true, the answer is true.

* 🔹 If no valid root-to-leaf path matches the target sum, return false.
---

## ⏱ Time Complexity

**O(n)**

* Every node is visited once.
    
---

## 📦 Space Complexity

**O(h)**

* Recursive call stack height, where h is the height of the tree

* **Worst Case:** `O(n)` for skewed tree
* **Best/Average Case:** `O(log n)` for balanced tree

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
    public boolean hasPathSum(TreeNode root, int targetSum) {
        return hasPathSumDFS(root, targetSum);
    }

    private boolean hasPathSumDFS(TreeNode node, int currentSum) {
        if (node == null) {
            return false;
        }
      
        currentSum -= node.val;
      
        if (node.left == null && node.right == null && currentSum == 0) {
            return true;
        }
      
        return hasPathSumDFS(node.left, currentSum) || hasPathSumDFS(node.right, currentSum);
    }
}
```

---