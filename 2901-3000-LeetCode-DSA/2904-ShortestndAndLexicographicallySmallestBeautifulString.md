# <u>2904. Shortest and Lexicographically Smallest Beautiful String</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/shortest-and-lexicographically-smallest-beautiful-string/

---

## 🧠 Intuition:
* 🔹 Try every possible **starting index** of the substring.

* 🔹 For each starting position, generate all possible substrings whose length is at least `k`.

* 🔹 Count the number of `1`s in every generated substring.

* 🔹 A substring is considered **beautiful** when it contains exactly `k` ones.

* 🔹 Maintain `result` as the best valid substring found so far.

* 🔹 Update `result` when the current substring:
    - is the first valid substring,
    - has a **smaller length**, or
    - has the **same length but is lexicographically smaller**.

* 🔹 After checking all possible substrings, return the shortest beautiful substring; if multiple have the same length, the lexicographically smallest one is returned.

---

## ⏱ Time Complexity

**O(n³)**

* There are `O(n²)` possible substrings.
* For every substring, the code creates the substring and traverses its characters to count `1`s, which can take `O(n)`.
    
---

## 📦 Space Complexity

**O(n)**

* `substring()` and `toCharArray()` can require `O(n)` temporary space.
* The `result` and `currentSubstring` can also hold `O(n)` characters.

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