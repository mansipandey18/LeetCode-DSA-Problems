# <u>226. Invert Binary Tree</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/invert-binary-tree/

---

## 🧠 Intuition:
* 🔹 The problem asks to mirror the binary tree, meaning every node’s left and right child should be swapped.

* 🔹 Use Recursion (DFS) to process each node of the tree.

* 🔹 Base Case:
    - If the current node is null, return null.

* 🔹 Recursively invert the left subtree and store it in l.

* 🔹 Recursively invert the right subtree and store it in r.

* 🔹 Swap the children:
    - Assign the inverted right subtree to root.left.
    - Assign the inverted left subtree to root.right.

* 🔹 Continue this process for every node until the entire tree becomes inverted.

* 🔹 Finally, return the modified root of the inverted tree.

---

## ⏱ Time Complexity

**O(n)**

* Every node is visited exactly once.
    
---

## 📦 Space Complexity

**O(h)**

* Recursive call stack space, where `h` is the height of the tree.
* Worst case: `O(n)` for a skewed tree.
* Best/Average case: `O(log n)` for a balanced tree.

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
    public TreeNode invertTree(TreeNode root) {
        if(root == null){
            return null;
        }

        TreeNode l = invertTree(root.left), r = invertTree(root.right);

        root.left = r;
        root.right = l;
        return root;
    }
}
```

---