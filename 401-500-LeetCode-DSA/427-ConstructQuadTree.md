# <u>427. Construct Quad Tree</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/construct-quad-tree/

---

## 🧠 Intuition:
* 🔹 The idea is to recursively divide the grid into four smaller quadrants until each region contains only the same value (all `0s` or all `1s`).

* 🔹 For every current sub-grid, traverse all its cells to check whether it contains both `0` and `1`.

* 🔹 If the region contains only one type of value, create a leaf node representing that value and stop further division.

* 🔹 If the region contains mixed values, create a non-leaf node and split the grid into four equal parts:
    - Top Left
    - Top Right
    - Bottom Left
    - Bottom Right

* 🔹 Recursively construct a Quad Tree for each of these four quadrants and attach them as children of the current node.

* 🔹 This divide-and-conquer process continues until all regions become uniform, resulting in the complete Quad Tree.

---

## ⏱ Time Complexity

**O(n^2 log n)**

* At each recursive level, all cells of the current regions are scanned, and there are `log n` levels of division.
    
---

## 📦 Space Complexity

**O(log n)**

* Due to the recursion stack height while dividing the grid into smaller quadrants.

---

## 💻 Java Code

```java
/*
// Definition for a QuadTree node.
class Node {
    public boolean val;
    public boolean isLeaf;
    public Node topLeft;
    public Node topRight;
    public Node bottomLeft;
    public Node bottomRight;

    
    public Node() {
        this.val = false;
        this.isLeaf = false;
        this.topLeft = null;
        this.topRight = null;
        this.bottomLeft = null;
        this.bottomRight = null;
    }
    
    public Node(boolean val, boolean isLeaf) {
        this.val = val;
        this.isLeaf = isLeaf;
        this.topLeft = null;
        this.topRight = null;
        this.bottomLeft = null;
        this.bottomRight = null;
    }
    
    public Node(boolean val, boolean isLeaf, Node topLeft, Node topRight, Node bottomLeft, Node bottomRight) {
        this.val = val;
        this.isLeaf = isLeaf;
        this.topLeft = topLeft;
        this.topRight = topRight;
        this.bottomLeft = bottomLeft;
        this.bottomRight = bottomRight;
    }
}
*/

class Solution {
    public Node construct(int[][] grid) {
        return buildQuadTree(0, 0, grid.length - 1, grid[0].length - 1, grid);
    }

    private Node buildQuadTree(int rowStart, int colStart, int rowEnd, int colEnd, int[][] grid) {
        int hasZero = 0;
        int hasOne = 0;
      
        for (int row = rowStart; row <= rowEnd; row++) {
            for (int col = colStart; col <= colEnd; col++) {
                if (grid[row][col] == 0) {
                    hasZero = 1;
                } else {
                    hasOne = 1;
                }
            }
        }
      
        boolean isLeaf = (hasZero + hasOne) == 1;
        boolean value = isLeaf && (hasOne == 1);
      
        Node currentNode = new Node(value, isLeaf);
      
        if (isLeaf) {
            return currentNode;
        }
      
        int midRow = (rowStart + rowEnd) / 2;
        int midCol = (colStart + colEnd) / 2;
      
        currentNode.topLeft = buildQuadTree(rowStart, colStart, midRow, midCol, grid);
        currentNode.topRight = buildQuadTree(rowStart, midCol + 1, midRow, colEnd, grid);
        currentNode.bottomLeft = buildQuadTree(midRow + 1, colStart, rowEnd, midCol, grid);
        currentNode.bottomRight = buildQuadTree(midRow + 1, midCol + 1, rowEnd, colEnd, grid);
      
        return currentNode;
    }
}
```

---