# <u>2075. Decode the Slanted Ciphertext</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/decode-the-slanted-ciphertext/

---

## 🧠 Intuition:
* 🔹 The encoded string represents a **matrix written row-wise** with given `rows`.

* 🔹 First calculate the number of columns using:
    - `columns = encodedText.length() / rows.`

* 🔹 Imagine reconstructing the matrix conceptually (without actually creating it).

* 🔹 The original message was encoded by reading characters **diagonally (down-right)**.

* 🔹 To decode, we **traverse diagonals starting from each column of the first row**.

* 🔹 For every starting column:
    - Move diagonally by increasing both **row** and **column** simultaneously.
    - Convert 2D matrix position `(row, column)` into string index using:
        * `row * columns + column`

* 🔹 Append characters encountered during diagonal traversal to the result.

* 🔹 After collecting all characters, remove extra trailing spaces added during encoding.

* 🔹 Return the cleaned decoded string.


---

## ⏱ Time Complexity

**O(n)**

* Where : 
    - `n = encodedText.length()`

* Each character of `encodedText` is visited exactly once during traversal.
---

## 📦 Space Complexity

**O(n)**

* No extra matrix is created (space optimized).
* Only a `StringBuilder` is used to store the result.

---

## 💻 Java Code

```java
class Solution {
    public String decodeCiphertext(String encodedText, int rows) {
        StringBuilder result = new StringBuilder();
      
        // Calculate number of columns in the matrix
        int columns = encodedText.length() / rows;
      
        // Iterate through each diagonal starting from the first row
        // Each diagonal starts at position (0, j) where j is the column index
        for (int startColumn = 0; startColumn < columns; ++startColumn) {
            // Traverse the diagonal from (0, startColumn) going down-right
            // row increments by 1, column increments by 1
            for (int row = 0, column = startColumn; 
                 row < rows && column < columns; 
                 ++row, ++column) {
                // Calculate the position in the original string
                // Position = row * columns + column (row-major order)
                int charPosition = row * columns + column;
                result.append(encodedText.charAt(charPosition));
            }
        }
      
        // Remove trailing spaces from the decoded text
        while (result.length() > 0 && result.charAt(result.length() - 1) == ' ') {
            result.deleteCharAt(result.length() - 1);
        }
      
        // Return the final decoded string
        return result.toString();
    
    }
}
```

---