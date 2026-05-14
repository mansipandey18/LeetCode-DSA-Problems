# <u>100. Same Tree</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/same-tree/

---

## 🧠 Intuition:
* 🔹 Use recursion to compare both trees node-by-node simultaneously.

* 🔹 If both nodes are `null`, it means both trees matched perfectly up to this point.

* 🔹 If one node is `null` and the other is not, the trees are different.

* 🔹 If both nodes exist but their values are different, the trees are not identical.

* 🔹 Recursively check:
    - Left subtree of both trees
    - Right subtree of both trees

* 🔹 The trees are considered the same only if:
    - Current node values are equal
    - Left subtrees are same
    - Right subtrees are same

* 🔹 This is a classic DFS traversal where structure + values must both match.

---

## ⏱ Time Complexity

**O(N)**

* Each node is visited once, where `N` is the number of nodes in the tree.

---

## 📦 Space Complexity

**O(H)**

* Recursive call stack space, where `H` is the height of the tree.
    - Worst case: **O(N)** (skewed tree)
    - Balanced tree: **O(log N)**

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
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null) return true;

        if (p == null || q == null || p.val != q.val) return false;

        return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    
    }
}
```

---