# <u>102. Binary Tree Level Order Traversal</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/binary-tree-level-order-traversal/

---

## 🧠 Intuition:
* 🔹 Use **Breadth First Search (BFS)** to traverse the binary tree level by level.

* 🔹 A queue helps process nodes in the same order they appear at each level.

* 🔹 Start by adding the root node into the queue.

* 🔹 For every iteration, store the current queue size to know how many nodes belong to the current level.

* 🔹 Process exactly those nodes and collect their values into a temporary list (`row`).

* 🔹 While processing a node, push its left and right children into the queue for the next level.

* 🔹 After finishing one level, add the `row` list into the final result.

* 🔹 Continue until the queue becomes empty, meaning all tree levels are traversed.

---

## ⏱ Time Complexity

**O(n)**

* Every node is visited once.  

---

## 📦 Space Complexity

**O(n)**

* Queue and result list may store up to all nodes in the tree.

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if(root == null){
            return res;
        }
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);

        while(q.size() > 0){
            int count = q.size();
            List<Integer> row = new ArrayList<>();
            for(int c = 1; c <= count; c++){
                TreeNode node = q.remove();
                row.add(node.val);

                if(node.left != null) q.add(node.left);
                if(node.right != null) q.add(node.right);

            }
            res.add(row);
        }
        return res;
    }
}
```

---