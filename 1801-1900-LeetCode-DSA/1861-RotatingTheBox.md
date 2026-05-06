# <u>1861. Rotating the Box</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/rotating-the-box/

---

## 🧠 Intuition:
* 🔹 The problem involves **two steps**:
    - **Rotate the box 90° clockwise**
    - **Simulate gravity** so stones (`#`) fall down

* 🔹 First, create a new `matrix result[cols][rows]` and rotate:
    - Each cell `(i, j)` in original becomes `(j, rows - 1 - i)` in rotated matrix

* 🔹 After rotation, columns behave like vertical stacks where gravity acts downward

* 🔹 For each column:
    - Traverse from **bottom to top**
    - Maintain a queue (`emptyPositions`) to store indices of empty cells (`.`)

* 🔹 While traversing:
    - If `'*'` (obstacle) is found → clear queue (stones cannot pass through)
    - If `'.'` → add position to queue (available space)
    - If `'#'` and empty space exists:
        * Move stone to the **lowest available empty position**
        * Mark current position as empty
        * Update queue accordingly

* 🔹 This ensures:
    - Stones fall down correctly
    - Obstacles block movement
    - Order is preserved

---

## ⏱ Time Complexity

**O(m x n)**

* Rotation step: **O(rows × cols)**
* Gravity simulation: **O(rows × cols)**

---

## 📦 Space Complexity

**O(m x n)**

* Extra matrix for rotated box

---

## 💻 Java Code

```java
class Solution {
    public char[][] rotateTheBox(char[][] boxGrid) {
        int rows = boxGrid.length;
        int cols = boxGrid[0].length;
      
        char[][] result = new char[cols][rows];
      
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                result[j][rows - 1 - i] = boxGrid[i][j];
            }
        }
      
        for (int col = 0; col < rows; col++) {
            Deque<Integer> emptyPositions = new ArrayDeque<>();
          
            for (int row = cols - 1; row >= 0; row--) {
                if (result[row][col] == '*') {
                    emptyPositions.clear();
                } else if (result[row][col] == '.') {
                    emptyPositions.offer(row);
                } else if (result[row][col] == '#' && !emptyPositions.isEmpty()) {
                    int lowestEmptyPosition = emptyPositions.pollFirst();
                    result[lowestEmptyPosition][col] = '#';
                    result[row][col] = '.';
                    emptyPositions.offer(row);
                }
            }
        }
      
        return result;
    }
}
```

---