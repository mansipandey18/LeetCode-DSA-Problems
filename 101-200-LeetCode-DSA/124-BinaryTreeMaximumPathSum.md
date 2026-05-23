# <u>124. Binary Tree Maximum Path Sum</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/binary-tree-maximum-path-sum/

---

## 🧠 Intuition:
* 🔹 Use DFS to calculate the maximum path sum passing through every node.

* 🔹 For each node, recursively find the maximum contribution from:
    - `Left subtree`
    - `Right subtree`

* 🔹 Ignore negative path sums using:
    - `Math.max(0, subtreeSum)`
    - because negative paths reduce the total sum.

* 🔹 At every node, calculate the path passing through that node
    - `leftContribution + rightContribution + node.val`

* 🔹 Update the global maximum answer (diameter variable) with this value.

* 🔹 This considers the current node as the “highest point” of the path.

* 🔹 Return only one side contribution to the parent
    - `max(leftContribution, rightContribution) + node.val`

* 🔹 Only one branch can continue upward because a valid path cannot split while returning to the parent.

* 🔹 After traversing all nodes, the global variable stores the maximum path sum in the tree.

---

## ⏱ Time Complexity

**O(n)**

* Each node is visited exactly once
    
---

## 📦 Space Complexity

**O(h)**

* Recursive stack space, where `h` is the height of the tree

* Worst Case: `O(n)` for skewed tree
* Best/Average Case: `O(log n)` for balanced tree

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
    int diameter = Integer.MIN_VALUE;

    public int maxDepth(TreeNode root){
        if(root == null) return 0;
        int lH = Math.max(0, maxDepth(root.left));
        int rH = Math.max(0, maxDepth(root.right));

        diameter = Math.max(diameter, lH + rH + root.val);
        return Math.max(lH, rH) + root.val;

    }
    public int maxPathSum(TreeNode root) {
        int height = maxDepth(root);
        return diameter;
    }
}
```

---