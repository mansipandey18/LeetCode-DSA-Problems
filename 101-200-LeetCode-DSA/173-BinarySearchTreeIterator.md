# <u>173. Binary Search Tree Iterator</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/binary-search-tree-iterator/

---

## 🧠 Intuition:
* 🔹 Inorder traversal of a `Binary Search Tree (BST)` gives elements in sorted order.

* 🔹 Perform an inorder traversal once during initialization.

* 🔹 Store all node values in a list called values.

* 🔹 Maintain an index pointer currentIndex to track the current iterator position.

* 🔹 `next()`:
    - Return the current value from the list
    - Move the pointer forward.

* 🔹 `hasNext()`:
    - Check whether currentIndex is still within the list size.

* 🔹 Since values are stored in sorted order, the iterator returns BST elements one by one in ascending order.

* 🔹 Preprocessing the tree makes each `next()` operation very fast.

---

## ⏱ Time Complexity

* → Constructor: `O(n)`

* → next(): `O(1)`

* → hasNext(): `O(1)`
    
---

## 📦 Space Complexity

**O(n)**

* Storing all BST node values in the list

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
class BSTIterator {
    private int currentIndex;
    private List<Integer> values;

    public BSTIterator(TreeNode root) {
        this.currentIndex = 0;
        this.values = new ArrayList<>();
        performInorderTraversal(root);
    }
    
    public int next() {
        return values.get(currentIndex++);
    }
    
    public boolean hasNext() {
        return currentIndex < values.size();
    }

    private void performInorderTraversal(TreeNode node) {
        if (node == null) {
            return;
        }
      
        performInorderTraversal(node.left);
      
        values.add(node.val);
      
        performInorderTraversal(node.right);
    }
}

/**
 * Your BSTIterator object will be instantiated and called as such:
 * BSTIterator obj = new BSTIterator(root);
 * int param_1 = obj.next();
 * boolean param_2 = obj.hasNext();
 */
```

---