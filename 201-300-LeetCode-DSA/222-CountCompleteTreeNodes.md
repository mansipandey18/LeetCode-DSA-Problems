# <u>222. Count Complete Tree Nodes</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/count-complete-tree-nodes/

---

## 🧠 Intuition:
* 🔹 The problem asks to count the total number of nodes in a binary tree.

* 🔹 Use simple DFS recursion to visit every node exactly once.

* 🔹 Base case:
    - If the current node is `null`, return `0` because no node exists there.

* 🔹 For every valid node:
    - Count the current node as `1`.
    - Recursively count nodes in the left subtree.
    - Recursively count nodes in the right subtree.

* 🔹 Total nodes =
    - `1 + nodes in left subtree + nodes in right subtree`

* 🔹 The recursion traverses the entire tree and accumulates the total count.

---

## ⏱ Time Complexity

**O(n)**

* Every node is visited exactly once.

---

## 📦 Space Complexity

**O(h)**

* Recursive stack space, where `h` is the height of the tree.
* Worst case: `O(n)` for skewed tree.
* Best/Average case: `O(log n)` for balanced tree.

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
    public int countNodes(TreeNode root) {
        if (root == null) {
            return 0;
        }
      
        return 1 + countNodes(root.left) + countNodes(root.right);
    }
}
```

---