# <u>2213. Longest Substring of One Repeating Character</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/longest-substring-of-one-repeating-character/

---

## 🧠 Intuition:
* 🔹 Use a **Segment Tree** because the string is modified multiple times, and after every update we need the **longest consecutive substring containing the same character**.

* 🔹 Each segment-tree `Node` stores three important values:
    - `leftMax` → longest repeating sequence starting from the **left boundary**.
    - `rightMax` → longest repeating sequence ending at the **right boundary**.
    - `maxLength` → longest repeating sequence anywhere inside that range.

* 🔹 Build the segment tree recursively so every node represents a range of the string.

* 🔹 When a character is updated, only the nodes along that position's path need to be recalculated.

* 🔹 `pushup()` combines the information from the left and right child:
    - Start with the maximum answer from either child.
    - If the last character of the left child equals the first character of the right child, the two repeating sequences can be **merged**.
    - Update `leftMax`, `rightMax`, and `maxLength` accordingly.

* 🔹 After every modification, query the root node, which represents the **entire string**, to get the current maximum repeating substring length.

* 🔹 This avoids scanning the complete string after every update and makes each query efficient.

---

## ⏱ Time Complexity

**O(n + q log n)**

* Where: 
    - `n` = length of the string
    - `q` = number of queries
* Building Segment Tree: `O(n)`
* Each character update: O(log n)`
* Query for the complete string: `O(1)` because the root already represents the entire string.

---

## 📦 Space Complexity

**O(n)**

* Segment Tree contains approximately `4n` nodes.
* Each node stores a constant number of integers.

---

## 💻 Java Code

```java
class Node {
    int left, right;           // Range boundaries [left, right]
    int leftMax, rightMax;      // Maximum repeating length starting from left/ending at right
    int maxLength;              // Maximum repeating substring length in this range
  
    Node(int left, int right) {
        this.left = left;
        this.right = right;
        this.leftMax = 1;      // Initially, each position has at least 1 character
        this.rightMax = 1;
        this.maxLength = 1;
    }
}

class SegmentTree {
    private char[] characters;  // The character array (1-indexed internally)
    private Node[] tree;        // Segment tree nodes
  
    public SegmentTree(char[] s) {
        int n = s.length;
        this.characters = s;
        this.tree = new Node[n << 2];  // Allocate 4n space for the tree
        build(1, 1, n);                // Build tree with 1-based indexing
    }
  
    public void build(int nodeIndex, int rangeLeft, int rangeRight) {
        tree[nodeIndex] = new Node(rangeLeft, rangeRight);
      
        // Base case: leaf node
        if (rangeLeft == rangeRight) {
            return;
        }
      
        // Recursive case: build left and right subtrees
        int mid = (rangeLeft + rangeRight) >> 1;
        int leftChild = nodeIndex << 1;
        int rightChild = nodeIndex << 1 | 1;
      
        build(leftChild, rangeLeft, mid);
        build(rightChild, mid + 1, rangeRight);
      
        // Update current node based on children
        pushup(nodeIndex);
    }
  
    public void modify(int nodeIndex, int position, char newChar) {
        Node currentNode = tree[nodeIndex];
      
        // Base case: reached the target leaf node
        if (currentNode.left == position && currentNode.right == position) {
            characters[position - 1] = newChar;  // Convert to 0-indexed
            return;
        }
      
        // Recursive case: traverse to the appropriate child
        int mid = (currentNode.left + currentNode.right) >> 1;
        int leftChild = nodeIndex << 1;
        int rightChild = nodeIndex << 1 | 1;
      
        if (position <= mid) {
            modify(leftChild, position, newChar);
        } else {
            modify(rightChild, position, newChar);
        }
      
        // Update current node after modification
        pushup(nodeIndex);
    }
  
    public int query(int nodeIndex, int queryLeft, int queryRight) {
        Node currentNode = tree[nodeIndex];
      
        // Current node's range is completely within query range
        if (currentNode.left >= queryLeft && currentNode.right <= queryRight) {
            return currentNode.maxLength;
        }
      
        int mid = (currentNode.left + currentNode.right) >> 1;
        int result = 0;
        int leftChild = nodeIndex << 1;
        int rightChild = nodeIndex << 1 | 1;
      
        // Query left subtree if needed
        if (queryRight <= mid) {
            result = query(leftChild, queryLeft, queryRight);
        }
      
        // Query right subtree if needed
        if (queryLeft > mid) {
            result = Math.max(result, query(rightChild, queryLeft, queryRight));
        }
      
        return result;
    }
  
    private void pushup(int nodeIndex) {
        Node parent = tree[nodeIndex];
        Node leftChild = tree[nodeIndex << 1];
        Node rightChild = tree[nodeIndex << 1 | 1];
      
        // Initial max is the maximum of both children
        parent.maxLength = Math.max(leftChild.maxLength, rightChild.maxLength);
      
        // Initialize parent's left and right max from children
        parent.leftMax = leftChild.leftMax;
        parent.rightMax = rightChild.rightMax;
      
        // Calculate the full length of left and right ranges
        int leftRangeLength = leftChild.right - leftChild.left + 1;
        int rightRangeLength = rightChild.right - rightChild.left + 1;
      
        // Check if we can merge across the boundary
        // If the last character of left child equals first character of right child
        if (characters[leftChild.right - 1] == characters[rightChild.left - 1]) {
            // If left child is all same characters, extend parent's leftMax
            if (leftChild.leftMax == leftRangeLength) {
                parent.leftMax += rightChild.leftMax;
            }
          
            // If right child is all same characters, extend parent's rightMax
            if (rightChild.rightMax == rightRangeLength) {
                parent.rightMax += leftChild.rightMax;
            }
          
            // Update max length considering the merge at boundary
            parent.maxLength = Math.max(parent.maxLength, 
                                       leftChild.rightMax + rightChild.leftMax);
        }
    }
}

class Solution {
    public int[] longestRepeating(String s, String queryCharacters, int[] queryIndices) {
        SegmentTree segmentTree = new SegmentTree(s.toCharArray());
      
        int numQueries = queryIndices.length;
        int[] results = new int[numQueries];
        int stringLength = s.length();
      
        // Process each query
        for (int i = 0; i < numQueries; i++) {
            // Convert to 1-indexed position for the segment tree
            int updatePosition = queryIndices[i] + 1;
            char newCharacter = queryCharacters.charAt(i);
          
            // Update the character at the specified position
            segmentTree.modify(1, updatePosition, newCharacter);
          
            // Query the entire string for the maximum repeating substring
            results[i] = segmentTree.query(1, 1, stringLength);
        }
      
        return results;
    }
}
```

---