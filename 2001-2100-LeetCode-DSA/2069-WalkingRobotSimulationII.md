# <u>2069. Walking Robot Simulation II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/walking-robot-simulation-ii/

---

## 🧠 Intuition:
* 🔹 The robot moves only along the **boundary (perimeter)** of a rectangle, not inside it.

* 🔹 Instead of simulating movement step-by-step every time, we **precompute all boundary positions** in clockwise order.

* 🔹 During initialization:
    - Store every perimeter coordinate in `pos` following order → **bottom → right → top → left**.
    - Also store the direction the robot faces at each position in the `dir` array.

* 🔹 The robot’s movement now becomes circular because after reaching the last boundary cell, it returns to the first.

* 🔹 Maintain an index `i` representing the robot’s current position in the perimeter list.

* 🔹 When `step(num)` is called:
    - Simply move forward by updating index using modulo:
        * `(currentIndex + steps) % perimeterSize`
    - This avoids costly simulation of each step.
* 🔹 `getPos()` directly returns the coordinate stored at index `i`.
* 🔹 `getDir()` returns the direction corresponding to the current boundary position.
* 🔹 Special case:
    - Initially robot is at origin `(0,0)` facing East, handled using `isOrigin`.


---

## ⏱ Time Complexity

* #### 1. Constructor → `Robot(int width, int height)`
    - Builds the entire boundary path of the grid.
    - Robot only walks on the **perimeter**.
    - Number of perimeter cells:
        * `2×width+2×height−4`
    - Each boundary position is added once.

    ✅ **Time Complexity = O(width + height)**

* #### 2. `step(int num)`
    - Only updates index using modulo:
        * `i = (i + num) % pos.size();`
    - No loop based on num.

    ✅ **Time Complexity = O(1)**

* #### 3. `getPos()`
    - Direct access from ArrayList.

    ✅ **Time Complexity = O(1)**

* #### 4. `getDir()`
    - Simple condition check and array access.
    
    ✅ **Time Complexity = O(1)**
    
---

## 📦 Space Complexity

**O(width + height)**

* `pos` stores all perimeter coordinates.
* `dir` stores direction for each boundary position.

Boundary size = `2 × (width + height) − 4`

---

## 💻 Java Code

```java
class Robot {

    private ArrayList<int[]> pos;
    private String[] dir;
    private int i;
    private boolean isOrigin;


    public Robot(int width, int height) {
        pos = new ArrayList<>();
        dir = new String[width * 2 + height * 2 - 4];
        pos.add(new int[]{0, 0});
        dir[0] = "South";
        int k = 1;
        for (int i = 1; i < width; i++) {
            pos.add(new int[]{i, 0});
            dir[k++] = "East";
        }
        for (int j = 1; j < height; j++) {
            pos.add(new int[]{width - 1, j});
            dir[k++] = "North";
        }
        for (int i = width - 2; i >= 0; i--) {
            pos.add(new int[]{i, height - 1});
            dir[k++] = "West";
        }
        for (int j = height - 2; j > 0; j--) {
            pos.add(new int[]{0, j});
            dir[k++] = "South";
        }
        isOrigin = true;
        i = 0;
    }
    
    public void step(int num) {
        isOrigin = false;
        i = (i + num) % pos.size();
    }
    
    public int[] getPos() {
        return pos.get(i);
    }
    
    public String getDir() {
        return isOrigin ? "East" : dir[i];
    }
}
```

---