# <u>199. Binary Tree Right Side View</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/binary-tree-right-side-view/

---

## 🧠 Intuition:
* 🔹 The goal is to return the nodes visible when the binary tree is viewed from the **right side**

* 🔹 Use **Level Order Traversal (BFS)** to process the tree level by level

* 🔹 A queue is used to store nodes of the current level

* 🔹 At the beginning of every level, the **first node in the queue** represents the rightmost node visible from that level

* 🔹 To ensure the rightmost node comes first in the queue:
    - Insert the **right child first**
    - Then insert the **left child**

* 🔹 For every level:
    - Add `queue.peekFirst().val` to the result
    - Process all nodes of that level using `levelSize`

* 🔹 Continue until all levels are processed

* 🔹 The collected nodes form the **right side view** of the tree


---

## ⏱ Time Complexity

**O(n)**

* Where:
    - `n` = number of nodes in the tree

* Every node is visited exactly once during BFS traversal
    
---

## 📦 Space Complexity

**O(n)**

* Queue can store up to one full level of the tree

* Worst case occurs in a complete binary tree

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
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> result = new ArrayList<>();
      
        if (root == null) {
            return result;
        }
      
        Deque<TreeNode> queue = new ArrayDeque<>();
        queue.offer(root);
      
        while (!queue.isEmpty()) {
            result.add(queue.peekFirst().val);
          
            int levelSize = queue.size();
            for (int i = 0; i < levelSize; i++) {
                TreeNode currentNode = queue.poll();
              
                if (currentNode.right != null) {
                    queue.offer(currentNode.right);
                }
              
                if (currentNode.left != null) {
                    queue.offer(currentNode.left);
                }
            }
        }
      
        return result;
    
    }
}
```

---