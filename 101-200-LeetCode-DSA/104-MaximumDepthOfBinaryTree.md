# <u>104. Maximum Depth of Binary Tree</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-depth-of-binary-tree/

---

## 🧠 Intuition:
* 🔹 The goal is to find the **maximum depth (height)** of a binary tree, i.e., the number of nodes along the longest path from root to a leaf

* 🔹 This problem naturally fits **recursion (DFS)** because each subtree has the same structure as the main tree

* 🔹 Base case:
    - If the current node is `null`, its depth is `0`

* 🔹 For any node:
    - Recursively calculate the depth of its **left subtree**
    - Recursively calculate the depth of its **right subtree**

* 🔹 The depth of the current node is:
    - `1 + max(leftDepth, rightDepth)`

* 🔹 The `+1` accounts for the current node itself

* 🔹 This ensures we always take the longest path from the current node down to a leaf

* 🔹 The recursion explores all nodes and builds the answer bottom-up

* 🔹 Finally, the result returned at the root is the maximum depth of the entire tree.

---

## ⏱ Time Complexity

**O(n)**

* Where :
    - `n` = number of nodes in the tree

* Each node is visited exactly once   

---

## 📦 Space Complexity

**O(h)**

* Due to recursion stack (height of the tree)

* Best case (balanced tree): **O(log n)**
* Worst case (skewed tree): **O(n)**

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
    public int maxDepth(TreeNode root) {
        if(root == null){
            return 0;
        }
        
        int leftHeight = maxDepth(root.left), rightHeight = maxDepth(root.right);

        return Math.max(leftHeight, rightHeight)+1;     
    }
}
```

---