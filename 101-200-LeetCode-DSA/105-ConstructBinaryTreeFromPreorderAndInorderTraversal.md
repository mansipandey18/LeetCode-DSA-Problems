# <u>105. Construct Binary Tree from Preorder and Inorder Traversal</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/

---

## 🧠 Intuition:
* 🔹 In preorder traversal:
    - The first element is always the root of the current subtree.

* 🔹 In inorder traversal:
    - Elements left of the root belong to the left subtree.
    - Elements right of the root belong to the right subtree.

* 🔹 Store all inorder indices in a HashMap for `O(1)` lookup of root positions.

* 🔹 Recursively construct the tree:
    - Pick root from preorder using `preorderStart`.
    - Find its index in inorder traversal.
    - Calculate the size of the left subtree.

* 🔹 Build left subtree using:
    - Next preorder elements after the root.
    - Corresponding left part of inorder array.

* 🔹 Build right subtree using:
    - Remaining preorder elements after the left subtree.
    - Corresponding right part of inorder array.

* 🔹 Base case:
    - If subtree size becomes `0`, return `null`.

* 🔹 Recursion rebuilds the entire binary tree correctly from traversal properties.

---

## ⏱ Time Complexity

**O(n)**

* Each node is processed once, and HashMap lookup takes `O(1)`.  

---

## 📦 Space Complexity

**O(n)**

* HashMap stores inorder indices.
* Recursive stack can take up to `O(n)` in the worst case (skewed tree).

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
    private int[] preorderTraversal; 
    private Map<Integer, Integer> inorderIndices = new HashMap<>(); 


    public TreeNode buildTree(int[] preorder, int[] inorder) {
        int n = preorder.length; 
        this.preorderTraversal = preorder; 
      
        for (int i = 0; i < n; ++i) {
            inorderIndices.put(inorder[i], i);
        }
        return buildTreeRecursive(0, 0, n);
    }

    private TreeNode buildTreeRecursive(int preorderStart, int inorderStart, int size) {
        if (size <= 0) { 
            return null;
        }
      
        int rootValue = preorderTraversal[preorderStart];
        int inorderRootIndex = inorderIndices.get(rootValue);
        int leftSubtreeSize = inorderRootIndex - inorderStart;

        TreeNode leftSubtree = buildTreeRecursive(preorderStart + 1, inorderStart, leftSubtreeSize);
      
        TreeNode rightSubtree = buildTreeRecursive(preorderStart + 1 + leftSubtreeSize, inorderRootIndex + 1, size - 1 - leftSubtreeSize);

        return new TreeNode(rootValue, leftSubtree, rightSubtree);
    }
}
```

---