# <u>1914. Cyclically Rotating a Grid</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/cyclically-rotating-a-grid/

---

## 🧠 Intuition:
* 🔹 The grid can be viewed as multiple **concentric rectangular layers (rings)**

* 🔹 Each layer is rotated independently by `k` positions

* 🔹 The number of layers is:
    - `min(rows, cols) / 2`

* 🔹 For every layer:
    - Extract all elements of that layer in clockwise order into a list
    - This converts the 2D rotation problem into a simple 1D cyclic rotation problem

* 🔹 The extraction is done in four parts:
    - Top row
    - Right column
    - Bottom row
    - Left column

* 🔹 Since rotating by the layer size gives the same arrangement, use: `k %= layerSize` to avoid unnecessary rotations

* 🔹 While placing elements back:
    - Start from index k in the extracted list
    - Use modulo operation to cyclically wrap around the list

* 🔹 Finally, write rotated values back into the same layer positions in the matrix

* 🔹 Repeat this process for all layers to get the fully rotated grid

---

## ⏱ Time Complexity

**O(rows x cols)**

* Every element of the grid is extracted and inserted exactly once across all layers

---

## 📦 Space Complexity

**O(rows x cols)**

* Extra list is used to store elements of one layer
* In the worst case, the outer layer may contain almost all elements

---

## 💻 Java Code

```java
class Solution {
    private int rows;
    private int cols;
    private int[][] matrix;
    
    public int[][] rotateGrid(int[][] grid, int k) {
        rows = grid.length;
        cols = grid[0].length;
        this.matrix = grid;
      
        // Calculate the number of layers (concentric rectangles) in the grid
        int numLayers = Math.min(rows, cols) / 2;
      
        // Rotate each layer independently
        for (int layer = 0; layer < numLayers; ++layer) {
            rotateLayer(layer, k);
        }
      
        return grid;
    }

    private void rotateLayer(int layer, int k) {
        List<Integer> elements = new ArrayList<>();
      
        // Extract all elements from the current layer in clockwise order
      
        // Top row (left to right, excluding last element)
        for (int col = layer; col < cols - layer - 1; ++col) {
            elements.add(matrix[layer][col]);
        }
      
        // Right column (top to bottom, excluding last element)
        for (int row = layer; row < rows - layer - 1; ++row) {
            elements.add(matrix[row][cols - layer - 1]);
        }
      
        // Bottom row (right to left, excluding last element)
        for (int col = cols - layer - 1; col > layer; --col) {
            elements.add(matrix[rows - layer - 1][col]);
        }
      
        // Left column (bottom to top, excluding last element)
        for (int row = rows - layer - 1; row > layer; --row) {
            elements.add(matrix[row][layer]);
        }
      
        // Calculate effective rotation (optimization to avoid unnecessary full rotations)
        int layerSize = elements.size();
        k %= layerSize;
      
        // If no rotation needed, return early
        if (k == 0) {
            return;
        }
      
        // Place elements back after rotation
      
        // Top row (left to right, excluding last element)
        for (int col = layer; col < cols - layer - 1; ++col) {
            matrix[layer][col] = elements.get(k++ % layerSize);
        }
      
        // Right column (top to bottom, excluding last element)
        for (int row = layer; row < rows - layer - 1; ++row) {
            matrix[row][cols - layer - 1] = elements.get(k++ % layerSize);
        }
      
        // Bottom row (right to left, excluding last element)
        for (int col = cols - layer - 1; col > layer; --col) {
            matrix[rows - layer - 1][col] = elements.get(k++ % layerSize);
        }
      
        // Left column (bottom to top, excluding last element)
        for (int row = rows - layer - 1; row > layer; --row) {
            matrix[row][layer] = elements.get(k++ % layerSize);
        }
    }
}
```

---