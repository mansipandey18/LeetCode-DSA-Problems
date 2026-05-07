# <u>236. Lowest Common Ancestor of a Binary Tree</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/

---

## 🧠 Intuition:
* 🔹 The Lowest Common Ancestor (LCA) of two nodes `p` and `q` is the **lowest node in the tree that has both nodes as descendants**

* 🔹 Use **recursive DFS traversal** to search for `p` and `q` in the left and right subtrees

* 🔹 Base cases:
    - If `root == null`, return `null`
    - If `root` matches either `p` or `q`, return `root`

* 🔹 Recursively search:
    - `left` → result from left subtree
    - `right` → result from right subtree

* 🔹 If both `left` and `right` are not null:
    - It means one node was found in the left subtree and the other in the right subtree
    - Therefore, current `root` is the **Lowest Common Ancestor**

* 🔹 If only one side returns a non-null value:
    - Return that side because both nodes are located there

* 🔹 The recursion naturally propagates the correct ancestor upward

---

## ⏱ Time Complexity

**O(n)**

* Where:
    - `n` = number of nodes in the tree

* In the worst case, every node is visited once
    
---

## 📦 Space Complexity

**O(h)**

* `h = height of tree`

* Recursive call stack depends on tree height

* Worst case (skewed tree) → **O(n)**
* Balanced tree → **O(log n)**

---

## 💻 Java Code

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null || root == p || root == q){
            return root;
        }

        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);

        if (left != null && right != null){
            return root;
        }
        
        return left == null ? right : left;
    }
}   
```

---