# <u>106. Construct Binary Tree from Inorder and Postorder Traversal</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/
---

## 🧠 Intuition:
* 🔹 In Postorder traversal:
    - The last element is always the root of the current subtree.

* 🔹 In Inorder traversal:
    - Elements left of the root belong to the left subtree.
    - Elements right of the root belong to the right subtree.

* 🔹 Store all inorder indices in a HashMap for O(1) lookup of root positions.

* 🔹 Recursively build the tree:
    - Pick the current root from postorder.
    - Find its index in inorder using the map.
    - Calculate the size of the left subtree.

* 🔹 Recursively construct:
    - Left subtree using left inorder portion.
    - Right subtree using right inorder portion.

* 🔹 Base case:
    - If subtree length becomes 0, return null.

* 🔹 By dividing inorder ranges and selecting roots from postorder, the original tree is reconstructed correctly.

---

## ⏱ Time Complexity

**O(n)**

* Every node is processed once.
* HashMap lookup takes `O(1)`.  

---

## 📦 Space Complexity

**O(n)**

* HashMap + recursion stack in worst case.

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
    private Map<Integer, Integer> inorderIndexMap = new HashMap<>();

    public TreeNode buildTree(int[] inorder, int[] postorder) {
        for (int i = 0; i < inorder.length; i++) {
            inorderIndexMap.put(inorder[i], i);
        }
        return buildTreeRecursive(inorder, postorder, 0, 0, inorder.length); 
    }

    private TreeNode buildTreeRecursive(int[] inorder, int[] postorder, int inorderStart, int postorderStart, int length) {
        if (length <= 0) {
            return null;
        }

        int rootValue = postorder[postorderStart + length - 1];
        int inorderRootIndex = inorderIndexMap.get(rootValue);

        TreeNode rootNode = new TreeNode(rootValue);

        int leftSubtreeLength = inorderRootIndex - inorderStart;

        rootNode.left = buildTreeRecursive(inorder, postorder, inorderStart, postorderStart, leftSubtreeLength);

        rootNode.right = buildTreeRecursive(inorder, postorder, inorderRootIndex + 1, postorderStart + leftSubtreeLength, length - leftSubtreeLength - 1);

        return rootNode;
    }
}
```

---