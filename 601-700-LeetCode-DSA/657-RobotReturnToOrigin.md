# <u>657. Robot Return to Origin</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/robot-return-to-origin/

---

## 🧠 Intuition:
* 🔹 The robot starts at the origin (0, 0) on a 2D plane.

* 🔹 Each character in moves represents a direction:
    - `U` → move up → increase `y`
    - `D` → move down → decrease `y`
    - `L` → move left → decrease `x`
    - `R` → move right → increase `x`

* 🔹 Maintain two variables:
    - `xCoordinate` → horizontal position
    - `yCoordinate` → vertical position

* 🔹 Traverse the string and update coordinates according to each move.

* 🔹 After processing all moves, check whether the robot returned to the starting position.

* 🔹 If (xCoordinate == 0 && yCoordinate == 0), the robot is back at origin → return true; otherwise false.

---

## ⏱ Time Complexity

**O(n)**

* Where :
    - `n = length of moves` 

* We iterate through the moves string once.
    
---

## 📦 Space Complexity

**O(1)**

* Only two integer variables are used (`xCoordinate`, `yCoordinate`).
* No extra data structures are required.

---

## 💻 Java Code

```java
class Solution {
    public boolean judgeCircle(String moves) {
         int xCoordinate = 0;
        int yCoordinate = 0;
      
        // Process each move character
        for (char move : moves.toCharArray()) {
            switch (move) {
                case 'U':  // Move up
                    yCoordinate++;
                    break;
                case 'D':  // Move down
                    yCoordinate--;
                    break;
                case 'L':  // Move left
                    xCoordinate--;
                    break;
                case 'R':  // Move right
                    xCoordinate++;
                    break;
                default:
                    // Invalid move character, ignore
                    break;
            }
        }
      
        // Check if returned to origin
        return xCoordinate == 0 && yCoordinate == 0;
    }
}
```

---