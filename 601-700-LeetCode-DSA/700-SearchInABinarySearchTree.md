# <u>700. Search in a Binary Search Tree</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/search-in-a-binary-search-tree/

---

## 🧠 Intuition:
* 🔹 A **Binary Search Tree (BST)** follows these properties:
    - Left subtree contains smaller values
    - Right subtree contains larger values

* 🔹 Start searching from the root node

* 🔹 Base cases:
    - If `root == null` → value does not exist, return null
    - If `root.val == val` → target found, return the current node

* 🔹 Use BST properties to reduce the search space:
    - If `val < root.val` → search only in the left subtree
    - Otherwise → search only in the right subtree

* 🔹 This avoids traversing the entire tree like a normal binary tree search

* 🔹 The recursion continues until the target node is found or the tree ends

---

## ⏱ Time Complexity

**O(n)**

* Where :
    - `n = length of nodes` 

* In each step, half of the tree is ignored because of BST properties.

* **Average Case (Balanced BST)** : **O(log n)**

* **Worst Case (Skewed BST)** : **O(n)**
    
---

## 📦 Space Complexity

**O(n)**

* Recursive call stack depends on tree height

* **Average Case (Balanced BST)** : **O(log n)**

* **Worst Case (Skewed BST)** : **O(n)**

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
    public TreeNode searchBST(TreeNode root, int val) {
        if(root == null)
            return root;
        if(root.val == val)
            return root;
        if(val < root.val)
            return searchBST(root.left, val);
        return searchBST(root.right, val);
    }
}
```

---