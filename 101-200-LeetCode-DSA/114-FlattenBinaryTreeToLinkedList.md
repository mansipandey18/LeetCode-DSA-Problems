# <u>114. Flatten Binary Tree to Linked List</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/flatten-binary-tree-to-linked-list/

---

## 🧠 Intuition:
* 🔹 The goal is to convert the binary tree into a linked list following preorder traversal order.

* 🔹 Traverse the tree node by node using the current `root`.

* 🔹 If a node has a left subtree:
    - Find the rightmost node of the left subtree.
    - Attach the original right subtree to this rightmost node.

* 🔹 Move the entire left subtree to the right side:
    - `root.right = root.left`
    - `root.left = null`

* 🔹 This restructuring ensures:
    - Left subtree comes before the original right subtree, matching preorder traversal order.

* 🔹 Move to the next node using `root = root.right`.

* 🔹 Repeat until all nodes are processed.

* 🔹 The tree is flattened in-place without using extra data structures.

---

## ⏱ Time Complexity

**O(n)**

* Every node is visited and rearranged at most once.
    
---

## 📦 Space Complexity

**O(1)**

* No extra space is used (iterative in-place approach).

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
    public void flatten(TreeNode root) {
        // Iterate until all the nodes are processed.
        while (root != null) {
            // If the current node has a left child, we need to process it.
            if (root.left != null) {
                // Find the rightmost node of the left subtree.
                TreeNode rightmost = root.left;
                while (rightmost.right != null) {
                    rightmost = rightmost.right;
                }
                // Make the right of the rightmost node point to the root's right node.
                rightmost.right = root.right;
                // Move the left subtree to the right.
                root.right = root.left;
                // After moving the left subtree, set the left child to null.
                root.left = null;
            }
            // Move on to the right child of the current node.
            root = root.right;
        }
    }
}
```

---