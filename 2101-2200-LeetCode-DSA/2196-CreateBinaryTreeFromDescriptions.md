# <u>2196. Create Binary Tree From Descriptions</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/create-binary-tree-from-descriptions/

---

## 🧠 Intuition:
* 🔹 The problem gives parent-child relationships and we need to **construct the binary tree** from them.

* 🔹 We use a HashMap (`nodeMap`) to store and reuse `TreeNode` objects for each unique value.

* 🔹 This ensures that every node is created only once and shared across relationships.

* 🔹 We also use a HashSet (`childrenSet`) to track all nodes that appear as children.

* 🔹 For each description `[parent, child, isLeft]`:
    - Create parent and child nodes if they do not already exist.
    - Connect the child to the parent’s left or right pointer based on `isLeft`.
    - Mark the child in `childrenSet`.

* 🔹 After building all connections, the **root node is the one that never appears as a child**.

* 🔹 We find and return that node by checking which key in the map is not in `childrenSet`.

---

## ⏱ Time Complexity

**O(n)**

* Processing all descriptions → `O(n)`
* Final scan of map entries → `O(n)`
  
---

## 📦 Space Complexity

**O(n)**

* HashMap stores all unique nodes → `O(n)`
* HashSet stores child nodes → `O(n)`

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
    public TreeNode createBinaryTree(int[][] descriptions) {
        Map<Integer, TreeNode> nodeMap = new HashMap<>();
      
        Set<Integer> childrenSet = new HashSet<>();
      
        for (int[] description : descriptions) {
            int parentValue = description[0];
            int childValue = description[1];
            int isLeft = description[2];
          
            if (!nodeMap.containsKey(parentValue)) {
                nodeMap.put(parentValue, new TreeNode(parentValue));
            }
          
            if (!nodeMap.containsKey(childValue)) {
                nodeMap.put(childValue, new TreeNode(childValue));
            }
          
            TreeNode parentNode = nodeMap.get(parentValue);
            TreeNode childNode = nodeMap.get(childValue);
          
            if (isLeft == 1) {
                parentNode.left = childNode;
            } else {
                parentNode.right = childNode;
            }
          
            childrenSet.add(childValue);
        }
      
        for (Map.Entry<Integer, TreeNode> entry : nodeMap.entrySet()) {
            if (!childrenSet.contains(entry.getKey())) {
                return entry.getValue();
            }
        }
      
        return null;
    }
}
```

---