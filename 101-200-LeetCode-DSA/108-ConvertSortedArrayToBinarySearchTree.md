# <u>108. Convert Sorted Array to Binary Search Tree</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/

---

## 🧠 Intuition:
* 🔹 Since the given array is **sorted**, choose the **middle element as the root** to keep the Binary Search Tree balanced.

* 🔹 The left half of the array contains smaller values, so recursively construct the **left subtree** from `left` to `mid - 1`.

* 🔹 The right half of the array contains larger values, so recursively construct the **right subtree** from `mid + 1` to `right`.

* 🔹 Repeat the same process for each subarray until the left index becomes greater than the right index, which represents an empty subtree.

* 🔹 Creating the root from the middle element at every step ensures the height of the BST remains as small as possible.

* 🔹 This divide-and-conquer approach naturally builds a **height-balanced BST**.

---

## ⏱ Time Complexity

**O(n)**

* Every element in the array is visited exactly once to create a tree node.
---

## 📦 Space Complexity

**O(log n)**

* Due to the recursive call stack for a height-balanced BST.

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
    private int[] nums;
    
    public TreeNode sortedArrayToBST(int[] nums) {
        this.nums = nums;
        return constructBSTRecursive(0, nums.length - 1);

    }

    private TreeNode constructBSTRecursive(int left, int right) {
        if (left > right) {
            return null;
        }
      
        int mid = left + (right - left) / 2;

        TreeNode leftSubtree = constructBSTRecursive(left, mid - 1);
      
        TreeNode rightSubtree = constructBSTRecursive(mid + 1, right);
      
        TreeNode node = new TreeNode(nums[mid], leftSubtree, rightSubtree);
      
        return node;
    }
}
```

---