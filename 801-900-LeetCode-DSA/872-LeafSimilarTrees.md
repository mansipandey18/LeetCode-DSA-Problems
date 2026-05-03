# <u>872. Leaf-Similar Trees</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/leaf-similar-trees/

---

## 🧠 Intuition:
* 🔹 The goal is to check whether two binary trees have the **same sequence of leaf nodes** (from left to right)

* 🔹 A leaf node is a node with **no left and no right child**

* 🔹 Idea: extract all leaf values from both trees in order and compare them

* 🔹 Use **DFS traversal (preorder/inorder doesn’t matter as long as left-to-right order is maintained)**

* 🔹 For each tree:
    - Traverse recursively
    - If a node is a leaf → add its value to a list
    - Otherwise, keep exploring left and right children

* 🔹 After traversal, we get two lists:
    - `leafValues1` for first tree
    - `leafValues2` for second tree

* 🔹 Compare both lists using `.equals()`
    - If they are identical → trees are leaf-similar
    - Else → not leaf-similar

* 🔹 This approach focuses only on leaf nodes and ignores tree structure differencesids explicit rotation and gives an efficient solution

---

## ⏱ Time Complexity

**O(n + m)**

* Where :
    - `n` and `m` are number of nodes in the two trees

* Each node in both trees is visited once

    
---

## 📦 Space Complexity

**O(n + m)**

* Lists to store leaf nodes
* Recursion stack space

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
    public boolean leafSimilar(TreeNode root1, TreeNode root2) {
        List<Integer> leafValues1 = new ArrayList<>();
        List<Integer> leafValues2 = new ArrayList<>();
      
        collectLeaves(root1, leafValues1);
        collectLeaves(root2, leafValues2);
      
        return leafValues1.equals(leafValues2);

    }

    private void collectLeaves(TreeNode node, List<Integer> leafValues) {
        if (node.left == null && node.right == null) {
            leafValues.add(node.val);
            return;
        }
      
        if (node.left != null) {
            collectLeaves(node.left, leafValues);
        }
      
        if (node.right != null) {
            collectLeaves(node.right, leafValues);
        }
    }
}
```

---