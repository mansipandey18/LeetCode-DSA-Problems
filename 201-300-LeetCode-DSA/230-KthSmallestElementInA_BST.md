# <u>230. Kth Smallest Element in a BST</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/kth-smallest-element-in-a-bst/

---

## 🧠 Intuition:
* 🔹 In a **Binary Search Tree (BST)**, an **inorder traversal (Left → Root → Right)** visits nodes in sorted order.

* 🔹 Therefore, the **k-th node visited during inorder traversal** is the **k-th smallest element**.

* 🔹 Use an **iterative inorder traversal** with a stack to avoid recursion.

* 🔹 Keep moving left and push nodes onto the stack until reaching the leftmost node.

* 🔹 Pop a node from the stack when there is no further left child.

* 🔹 Each popped node represents the next smallest element in sorted order.

* 🔹 Decrement `k` whenever a node is visited.

* 🔹 When `k` becomes `0`, the current node is the **k-th smallest element**, so return its value.

* 🔹 After visiting a node, move to its right subtree and continue the inorder traversal process.

---

## ⏱ Time Complexity

**O(H + K)**

* Where:
    - `H` is the height of the BST
    - `K` is the number of nodes visited until finding the k-th smallest element.

* In the worst case, **O(N)**
    
---

## 📦 Space Complexity

**O(H)**

* stack stores at most the height of the tree (O(N) in the worst case, O(log N) for a balanced BST).

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
    public int kthSmallest(TreeNode root, int k) {
        Deque<TreeNode> stack = new ArrayDeque<>();
        TreeNode current = root;
      
        while (current != null || !stack.isEmpty()) {
            if (current != null) {
                stack.push(current);
                current = current.left;
            } 
            else {
                current = stack.pop();
              
                k--;
                if (k == 0) {
                    return current.val;
                }
              
                current = current.right;
            }
        }
      
        return 0;
    }
}
```

---