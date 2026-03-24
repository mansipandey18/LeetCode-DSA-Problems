# <u>2906. Construct Product Matrix</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/construct-product-matrix/

---

## 🧠 Intuition:
* 🔹 Imagine grid as one long sequence
    - Traverse matrix row by row like a 1D array.

* 🔹 First pass (Suffix Products)
    - Move from bottom-right → top-left.
    - Keep multiplying elements seen so far.
    - Store product of all elements after current cell.
* 🔹 Second pass (Prefix Products)
    - Move from top-left → bottom-right.
    - Maintain running product of elements before current cell.
    - Multiply this prefix with stored suffix value.

* 🔹 Now each cell has
    - product of elements before it * product of elements after it

    - ✅ which equals product of all elements except itself.

* 🔹 Modulo (12345) is used to avoid large numbers.

---

## ⏱ Time Complexity

**O(m * n)**

* Let : 
    - `m = rows`
    - `n =  columns`

* We traverse the matrix twice:
    - First pass → O(m × n)
    - Second pass → O(m × n)
    
---

## 📦 Space Complexity

**O(m * n)**

* Output matrix is required → O(m × n)
* Only two extra variables (prefixProduct, suffixProduct) : Auxiliary Space: O(1)

---

## 💻 Java Code

```java
class Solution {
    public int[][] constructProductMatrix(int[][] grid) {
        final int MOD = 12345;
      
        // Get dimensions of the input grid
        int rows = grid.length;
        int cols = grid[0].length;
      
        // Initialize result matrix to store products
        int[][] productMatrix = new int[rows][cols];
      
        // First pass: Calculate suffix products (from bottom-right to top-left)
        // Each cell will initially store the product of all elements after it
        long suffixProduct = 1;
        for (int i = rows - 1; i >= 0; i--) {
            for (int j = cols - 1; j >= 0; j--) {
                // Store current suffix product at this position
                productMatrix[i][j] = (int) suffixProduct;
                // Update suffix product by multiplying with current grid element
                suffixProduct = (suffixProduct * grid[i][j]) % MOD;
            }
        }
      
        // Second pass: Multiply by prefix products (from top-left to bottom-right)
        // This combines prefix and suffix products to get the final result
        long prefixProduct = 1;
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                // Multiply stored suffix product by current prefix product
                productMatrix[i][j] = (int) ((productMatrix[i][j] * prefixProduct) % MOD);
                // Update prefix product by multiplying with current grid element
                prefixProduct = (prefixProduct * grid[i][j]) % MOD;
            }
        }
      
        return productMatrix;
    
    }
}
```

---