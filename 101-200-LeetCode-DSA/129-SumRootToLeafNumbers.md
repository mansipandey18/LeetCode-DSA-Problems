# <u>129. Sum Root to Leaf Numbers</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/sum-root-to-leaf-numbers/

---

## 🧠 Intuition:
* 🔹 Use DFS traversal to explore every root-to-leaf path in the binary tree.
* 🔹 While moving down the tree, build the current number digit by digit.
* 🔹 At each node, update the number using:
    - `sum = sum * 10 + node.val`
* 🔹 Multiplying by 10 shifts previous digits left, and adding node.val appends the current digit.
* 🔹 When a leaf node is reached, the formed number represents one complete root-to-leaf number.
* 🔹 Return this number from the leaf node.
* 🔹 Recursively calculate the sum from both left and right subtrees.
* 🔹 Add the results of both recursive calls to get the total sum of all root-to-leaf numbers.
* 🔹 If a node is null, return 0 because it contributes nothing to the sum.

---

## ⏱ Time Complexity

**O(n)**

* Each node is visited exactly once
    
---

## 📦 Space Complexity

**O(h)**

* Recursive call stack height, where `h` is the height of the tree
* **Worst Case:** `O(n)` for skewed tree
* **Best/Average Case:** `O(log n)` for balanced tree

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
    public int sumNumbers(TreeNode root) {
       return depthFirstSearch(root, 0); 
    }

    private int depthFirstSearch(TreeNode node, int sum) {
        if (node == null) {
            return 0;
        }

        sum = sum * 10 + node.val;

        if (node.left == null && node.right == null) {
            return sum;
        }

        return depthFirstSearch(node.left, sum) + depthFirstSearch(node.right, sum);
    }
}
```

---