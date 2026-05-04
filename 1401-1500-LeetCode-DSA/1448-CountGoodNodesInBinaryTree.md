# <u>1448. Count Good Nodes in Binary Tree</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/count-good-nodes-in-binary-tree/

---

## 🧠 Intuition:
* 🔹 A node is called **“good”** if its value is **greater than or equal to all nodes** on the path from root to that node

* 🔹 While traversing the tree, we need to keep track of the **maximum value seen so far** on the current path

* 🔹 Use **DFS (Depth First Search)** starting from the root

* 🔹 Initialize `maxSoFar` with a very small value (`Integer.MIN_VALUE`)

* 🔹 For each node:
    - If `node.val >= maxSoFar`, it is a **good node** → increment count
    - Update `maxSoFar = max(maxSoFar, node.val)`

* 🔹 Recursively apply the same logic to left and right children

* 🔹 Each path maintains its own `maxSoFar`, ensuring correct comparison for that path only

* 🔹 Continue traversal until all nodes are visited

* 🔹 Finally, return the total count of good nodes


---

## ⏱ Time Complexity

**O(n)**

* Where : 
    - `n` = number of nodes in the tree

* Each node is visited exactly once
    
---

## 📦 Space Complexity

**O(h)**

* Best case (balanced tree): `O(log n)`
* Worst case (skewed tree): `O(n)`
* Due to recursion stack (height of tree)

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
    private int goodNodeCount = 0;

    public int goodNodes(TreeNode root) {
        depthFirstSearch(root, Integer.MIN_VALUE);
        return goodNodeCount;
    }

    private void depthFirstSearch(TreeNode node, int maxSoFar) {
        if (node == null) {
            return;
        }
      
        if (maxSoFar <= node.val) {
            goodNodeCount++;
            maxSoFar = node.val;
        }
      
        depthFirstSearch(node.left, maxSoFar);
        depthFirstSearch(node.right, maxSoFar);
    }
}
```

---