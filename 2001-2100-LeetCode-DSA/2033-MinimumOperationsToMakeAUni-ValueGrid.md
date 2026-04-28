# <u>2033. Minimum Operations to Make a Uni-Value Grid</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/minimum-operations-to-make-a-uni-value-grid/

---

## 🧠 Intuition:
* 🔹 In one operation, we can either add or subtract exactly `x` from any grid element, and we need to make all elements equal with minimum operations

* 🔹 First observation: this is only possible if all elements have the same remainder when divided by `x`

* 🔹 Why? Because adding/subtracting `x` never changes the remainder modulo `x`

* 🔹 So, if even one element has a different remainder, it is impossible to make all values equal → return `-1`

* 🔹 Flatten the 2D grid into a 1D array so it becomes easier to sort and process

* 🔹 After feasibility check, the problem becomes:

    - **Choose one target value such that total absolute difference is minimum**

* 🔹 For minimizing sum of absolute differences, the best choice is always the **median**

* 🔹 Sort the flattened array and select the middle element as the target (`median`)

* 🔹 For each value, calculate how many operations are needed to convert it into the median:

    - `|value - median| / x`

* 🔹 Sum all these operations to get the minimum total operations

* 🔹 Using the median guarantees the smallest total number of moves.

---

## ⏱ Time Complexity
**O((m * n) log(m * n))**

* Flattening + remainder checking → **O(m × n)**
* Sorting the flattened array of size `m × n` → **O((m × n) log(m × n))**
* Calculating total operations → **O(m × n)**

---

## 📦 Space Complexity

**O(m * n)**

* Extra flattened array of size `m × n` is used

---

## 💻 Java Code

```java
class Solution {
    public int minOperations(int[][] grid, int x) {
        int rows = grid.length;
        int cols = grid[0].length;
      
        int[] flattenedArray = new int[rows * cols];
      
        int firstRemainder = grid[0][0] % x;
      
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (grid[i][j] % x != firstRemainder) {
                    return -1;
                }
                flattenedArray[i * cols + j] = grid[i][j];
            }
        }
      
        Arrays.sort(flattenedArray);
      
        int medianValue = flattenedArray[flattenedArray.length >> 1];
      
        int totalOperations = 0;
        for (int value : flattenedArray) {
            totalOperations += Math.abs(value - medianValue) / x;
        }
      
        return totalOperations;

    }
}
```

---