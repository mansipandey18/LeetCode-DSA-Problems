# <u>101. Symmetric Tree</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/symmetric-tree/

---

## 🧠 Intuition:
* 🔹 A binary tree is symmetric if its left subtree is the mirror image of its right subtree.

* 🔹 Use DFS to compare nodes from both sides simultaneously.

* 🔹 Base Cases:
    - If both nodes are `null`, they are symmetric → return `true`.
    - If one node is `null` and the other is not, symmetry breaks → return `false`.
    - If node values are different, tree is not symmetric → return `false`.

* 🔹 For mirror checking:
    - Compare `r1.left` with `r2.right`.
    - Compare `r1.right` with `r2.left`.

* 🔹 Both recursive calls must return `true` for the tree to remain symmetric.

* 🔹 Start recursion from `root.left` and `root.right`.

* 🔹 The recursion checks the tree in a mirrored manner at every level.

---

## ⏱ Time Complexity

**O(n)**

* Every node is visited once.  

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
    public boolean dfs(TreeNode r1, TreeNode r2){
        if(r1 == null && r2 == null) return true;
        if(r1 == null || r2 == null) return false;
        if(r1.val != r2.val) return false;

        boolean call1 = dfs(r1.left, r2.right);
        if(call1 == false) return false;
        boolean call2 = dfs(r1.right, r2. left);
        return call2; 

    }
    public boolean isSymmetric(TreeNode root) {
        if(root == null){
            return true;
        }
        return dfs(root.left, root. right);   
    }
}
```

---