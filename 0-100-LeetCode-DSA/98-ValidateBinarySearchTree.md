# <u>98. Validate Binary Search Tree</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/validate-binary-search-tree/

---

## 🧠 Intuition:
* 🔹 A valid **Binary Search Tree (BST)** must satisfy:
    - All nodes in the left subtree are **smaller** than the current node.
    - All nodes in the right subtree are **greater** than the current node.
    - This rule must hold for every node in the tree, not just its immediate children.

* 🔹 Use recursion and maintain a valid range (`minNode`, `maxNode`) for each node.

* 🔹 For every node:
    - If `minNode` exists, the current value must be greater than minNode.val.
    - If `maxNode` exists, the current value must be smaller than maxNode.val.

* 🔹 If any node violates these conditions, return `false`.

* 🔹 Recursively check:
    - Left subtree with the current node as the new **upper bound** (`maxNode`).
    - Right subtree with the current node as the new **lower bound** (`minNode`).

* 🔹 If all nodes satisfy their allowed range, the tree is a valid BST.


---

## ⏱ Time Complexity

**O(n)**

* every node is visited exactly once.

---

## 📦 Space Complexity

**O(h)**

* recursive call stack, where `H` is the height of the tree (`O(log N)` for a balanced tree, `O(N)` for a skewed tree).

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
    public boolean isValidBST(TreeNode root) {
        return isValidBST(root, null, null);
    }

    private boolean isValidBST(TreeNode root, TreeNode minNode, TreeNode maxNode) {
        if (root == null)
          return true;
        if (minNode != null && root.val <= minNode.val)
          return false;
        if (maxNode != null && root.val >= maxNode.val)
          return false;
        
        return                                      
            isValidBST(root.left, minNode, root) &&  
            isValidBST(root.right, root, maxNode);
    }
}
```

---