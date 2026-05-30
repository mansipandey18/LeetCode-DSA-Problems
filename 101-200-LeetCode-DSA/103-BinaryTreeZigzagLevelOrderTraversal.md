# <u>103. Binary Tree Zigzag Level Order Traversal</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/

---

## 🧠 Intuition:
* 🔹 Use **Level Order Traversal (BFS)** to process the binary tree level by level.

* 🔹 Maintain a queue to store nodes of the current level.

* 🔹 For each level, collect all node values in a temporary list.

* 🔹 Add the left and right children of each node to the queue for the next level.

* 🔹 Use a boolean flag `leftToRight` to track the traversal direction:
    - `true` → keep the level as it is (left to right).
    - `false` → reverse the level list before adding it to the result (right to left).

* 🔹 After processing each level, toggle the direction flag.

* 🔹 Continue until all levels are processed.

* 🔹 The result forms the required **zigzag (spiral) level order traversal**.

---

## ⏱ Time Complexity

**O(n)**

* Where:
    - `n` = number of nodes in the tree

* Each node is visited exactly once during BFS.  

---

## 📦 Space Complexity

**O(n)**

* `O(n)`, for the queue and result list in the worst case.

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
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) {
            return result;
        }
      
        Deque<TreeNode> queue = new ArrayDeque<>();
        queue.offer(root);
      
        boolean leftToRight = true;
      
        while (!queue.isEmpty()) {
            List<Integer> tempList = new ArrayList<>();
            for (int i = queue.size(); i > 0; --i) {
                TreeNode currentNode = queue.poll();
                tempList.add(currentNode.val);
                if (currentNode.left != null) {
                    queue.offer(currentNode.left);
                }
                if (currentNode.right != null) {
                    queue.offer(currentNode.right);
                }
            }
          
            if (!leftToRight) {
                Collections.reverse(tempList);
            }
            result.add(tempList);
            leftToRight = !leftToRight;
        }
      
        return result;
    
    }
}
```

---