# <u>3568. Minimum Moves to Clean the Classroom</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/minimum-moves-to-clean-the-classroom/

---

## 🧠 Intuition:
* 🔹 Treat the problem as a **BFS on states**, where each state represents:
    - Current position `(row, col)`
    - Remaining `energy`
    - `lightsMask` representing which lights are still on.

* 🔹 First, scan the classroom to:
    - Find the starting position `S`.
    - Assign a unique bit/index to every light `L`.

* 🔹 Use a **bitmask** to efficiently track collected/turned-off lights:
    - Initially, all lights are on → all bits are `1`.
    - When visiting a light, clear its corresponding bit.
    - When the mask becomes `0`, all lights have been cleaned.

* 🔹 BFS explores the classroom **level by level**, so the first time all lights are turned off, `steps` is the minimum number of moves.

* 🔹 Moving to a normal cell consumes **1 unit of energy**.

* 🔹 Moving onto a recharge cell `R` resets the energy back to the initial `energy`.

* 🔹 Walls `X` cannot be entered.

* 🔹 The `visited[row][col][energy][mask]` array prevents processing the same state multiple times.

* 🔹 If BFS finishes without reaching `lightsMask == 0`, return `-1`.


---

## ⏱ Time Complexity

**O(R × C × E × 2^L)**

* Where : 
    - `R` = number of rows
    - `C` = number of columns
    - `E` = initial energy
    - `L` = number of lights

* There are at most `R × C × (E + 1) × 2^L` states, and each state checks 4 directions.

---

## 📦 Space Complexity

**O(R × C × E × 2^L)**

* `visited` stores `R × C × (E + 1) × 2^L` states.
* BFS queue can also contain states of the same order.

---

## 💻 Java Code

```java
class Solution {
    public int minMoves(String[] classroom, int energy) {
        int rows = classroom.length;
        int cols = classroom[0].length();
      
        int[][] lightIndex = new int[rows][cols];
        int startRow = 0, startCol = 0;
        int lightCount = 0;
      
        for (int i = 0; i < rows; i++) {
            String row = classroom[i];
            for (int j = 0; j < cols; j++) {
                char cell = row.charAt(j);
                if (cell == 'S') {
                    startRow = i;
                    startCol = j;
                } else if (cell == 'L') {
                    lightIndex[i][j] = lightCount;
                    lightCount++;
                }
            }
        }
      
        if (lightCount == 0) {
            return 0;
        }
      
        boolean[][][][] visited = new boolean[rows][cols][energy + 1][1 << lightCount];
      
        List<int[]> queue = new ArrayList<>();
        int initialMask = (1 << lightCount) - 1; // All lights initially on
        queue.add(new int[] {startRow, startCol, energy, initialMask});
        visited[startRow][startCol][energy][initialMask] = true;
      
        int[] directions = {-1, 0, 1, 0, -1};
        int steps = 0;
      
        while (!queue.isEmpty()) {
            List<int[]> currentLevel = queue;
            queue = new ArrayList<>();
          
            for (int[] state : currentLevel) {
                int currentRow = state[0];
                int currentCol = state[1];
                int currentEnergy = state[2];
                int lightsMask = state[3];
              
                if (lightsMask == 0) {
                    return steps;
                }
              
                if (currentEnergy <= 0) {
                    continue;
                }
              
                for (int k = 0; k < 4; k++) {
                    int nextRow = currentRow + directions[k];
                    int nextCol = currentCol + directions[k + 1];
                  
                    if (nextRow >= 0 && nextRow < rows && 
                        nextCol >= 0 && nextCol < cols && 
                        classroom[nextRow].charAt(nextCol) != 'X') {
                      
                        int nextEnergy = classroom[nextRow].charAt(nextCol) == 'R' 
                                        ? energy 
                                        : currentEnergy - 1;
                      
                        int nextMask = lightsMask;
                        if (classroom[nextRow].charAt(nextCol) == 'L') {
                            nextMask &= ~(1 << lightIndex[nextRow][nextCol]);
                        }
                      
                        if (!visited[nextRow][nextCol][nextEnergy][nextMask]) {
                            visited[nextRow][nextCol][nextEnergy][nextMask] = true;
                            queue.add(new int[] {nextRow, nextCol, nextEnergy, nextMask});
                        }
                    }
                }
            }
            steps++;
        }
      
        return -1;
    }
}
```

---