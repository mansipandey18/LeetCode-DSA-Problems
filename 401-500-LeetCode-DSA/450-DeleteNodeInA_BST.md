# <u>450. Delete Node in a BST</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/delete-node-in-a-bst/

---

## 🧠 Intuition:
* 🔹 Since the tree is a **Binary Search Tree (BST)**, we can efficiently locate the node using BST properties

* 🔹 Traverse recursively:
    - If `key < root.val` → search in the left subtree
    - If `key > root.val` → search in the right subtree

* 🔹 Once the node to delete is found, handle 3 cases:
    1. **Node has no left child**
        - Return `root.right` directly
    2. **Node has no right child**
        - Return `root.left` directly
    3. **Node has both children**
        - Find the inorder successor
            * Smallest node in the right subtree
        - Attach the left subtree of the deleted node to the successor’s left
        - Replace the deleted node with its right subtree

* 🔹 This keeps the BST structure valid after deletion

* 🔹 Finally, return the updated root of the tree

---

## ⏱ Time Complexity

**O(n)**

* Where:
    - `n` = number of nodes

* Searching for the node takes time proportional to tree height
* Finding the inorder successor may also take up to tree height

---

## 📦 Space Complexity

**O(n)**

* Recursive call stack depends on the height of the tree

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
    public TreeNode deleteNode(TreeNode root, int key) {
        if (root == null) {
            return null;
        }
      
        if (root.val > key) {
            root.left = deleteNode(root.left, key);
            return root;
        }
      
        if (root.val < key) {
            root.right = deleteNode(root.right, key);
            return root;
        }
      
        if (root.left == null) {
            return root.right;
        }
      
        if (root.right == null) {
            return root.left;
        }
      
        TreeNode successorNode = root.right;
        while (successorNode.left != null) {
            successorNode = successorNode.left;
        }
      
        successorNode.left = root.left;
      
        root = root.right;
      
        return root;
    }
}   
```

---