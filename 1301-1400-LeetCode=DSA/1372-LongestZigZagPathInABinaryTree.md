# <u>1372. Longest ZigZag Path in a Binary Tree</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/longest-zigzag-path-in-a-binary-tree/

---

## 🧠 Intuition:
* 🔹 Each cell in the grid represents a street type, and every type connects only in specific directions

* 🔹 Directly checking valid connections between neighboring cells can become complex because each street type has different movement rules

* 🔹 To simplify this, each original cell is expanded into a **3 × 3 mini-grid**, where the valid street path is drawn using `true` values

* 🔹 This converts the problem into a simple path-finding problem on a larger boolean grid

* 🔹 For example:
    - Horizontal street → mark the middle row
    - Vertical street → mark the middle column
    - Corner streets → mark only the connected turning path

* 🔹 After building this upscaled grid, if a continuous path exists from the start cell to the destination cell, then the original grid also has a valid path

* 🔹 Start DFS from the top-left valid center point `(1,1)` of the expanded grid

* 🔹 During DFS:
    - Stop if out of bounds
    - Stop if current cell is `false` (no road exists)
    - Return true if destination center `(last-2, last-2)` is reached

* 🔹 Mark visited cells as `false` to avoid revisiting and infinite loops

* 🔹 If DFS reaches the destination, return `true`, otherwise `false`

* 🔹 This approach avoids manual street compatibility checks and turns the problem into standard graph traversal

---

## ⏱ Time Complexity

**O(m * n)**

* Where :
    - `n` = number of nodes

* Each node is visited once
    
---

## 📦 Space Complexity

**O(h)**

* Due to recursion stack

* Best case (balanced tree): **O(log n)**
* Worst case (skewed tree): **O(n)**

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
    private int maxZigZagLength;
    
    public int longestZigZag(TreeNode root) {
        maxZigZagLength = 0;

        dfs(root, 0, 0);
        return maxZigZagLength;
    }

    private void dfs(TreeNode node, int leftCount, int rightCount) {
        if (node == null) {
            return;
        }
      
        maxZigZagLength = Math.max(maxZigZagLength, Math.max(leftCount, rightCount));
      
        dfs(node.left, rightCount + 1, 0);
      
        dfs(node.right, 0, leftCount + 1);
    }
}
```

---