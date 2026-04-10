# <u>3661. Maximum Walls Destroyed by Robots</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-walls-destroyed-by-robots/

---

## 🧠 Intuition:
* 🔹 Each robot stands at a position and can destroy walls within its shooting distance either **to the left or to the right**.

* 🔹 First, pair every robot’s **position and distance** together and **sort robots by position** so we can process them from left → right logically.

* 🔹 Also sort the walls so we can efficiently count how many walls lie inside any shooting range using two pointers.

* 🔹 For every robot, compute three things:
    - `leftWall[i]` → number of walls robot `i` can destroy if it shoots left.
    - `rightWall[i]` → number of walls robot `i` can destroy if it shoots right.
    - `common[i]` → walls that could be destroyed by both robot `i-1` and robot `i` (overlapping region), to avoid double counting.

* 🔹 Use sliding window pointers on the sorted walls array to count walls in ranges efficiently instead of checking each wall repeatedly.

* 🔹 Now apply **Dynamic Programming**:
    - `dpLeft[i]` = maximum walls destroyed up to robot `i` if robot `i` shoots left.
    - `dpRight[i]` = maximum walls destroyed up to robot `i` if robot `i` shoots right.

* 🔹 Transition logic:
    - If current robot shoots left, subtract overlapping walls already counted from the previous robot.
    - If shooting right, simply add its right-side walls to the best previous result.

* 🔹 At each step, choose the option giving maximum destroyed walls.

* 🔹 Final answer is the maximum between last robot shooting left or right.

---

## ⏱ Time Complexity

**O(nlogn+mlogm)**

* Let : 
    - `n` = number of robots
    - `m` = number of walls

* **1️⃣ Sorting**
    - Sort robots → O(n log n)
    - Sort walls → O(m log m)

* **2️⃣ Preprocessing Arrays**

    - Each of:

        * `prepareLeftWall`
        * `prepareRightWall`
        * `prepareCommon`

    - uses two-pointer traversal over walls.

    - Total: O(n+m)

* **3️⃣ Dynamic Programming Pass**

    - Single traversal of robots: O(n)
    
---

## 📦 Space Complexity

**O(n)**

* Extra arrays used:
    - dpLeft[n]
    - dpRight[n]
    - leftWall[n]
    - rightWall[n]
    - common[n]
    - robot records


---

## 💻 Java Code

```java
class Solution {

    public static final int INF = Integer.MAX_VALUE;
    public static final int NEG_INF = Integer.MIN_VALUE;

    record Robot(int position, int distance) {
    }

    public int maxWalls(int[] robots, int[] distance, int[] walls) {
        int n = robots.length;
        Robot[] robotRecords = new Robot[n];

        for (int i = 0; i < n; i++) {
            robotRecords[i] = new Robot(robots[i], distance[i]);
        }

        Arrays.sort(robotRecords, Comparator.comparingInt(o -> o.position));
        Arrays.sort(walls);
        return maxWalls(robotRecords, n, walls);
    }

    private int maxWalls(Robot[] robots, int n, int[] walls) {
        int[] dpLeft = new int[n];
        int[] dpRight = new int[n];
        int[] leftWall = prepareLeftWall(robots, n, walls);
        int[] rightWall = prepareRightWall(robots, n, walls);
        int[] common = prepareCommon(robots, n, walls);

        dpLeft[0] = leftWall[0];
        dpRight[0] = rightWall[0];

        for (int i = 1; i < n; i++) {
            dpLeft[i] = leftWall[i] + Math.max(dpLeft[i - 1], dpRight[i - 1] - common[i]);
            dpRight[i] = rightWall[i] + Math.max(dpLeft[i - 1], dpRight[i - 1]);
        }

        return Math.max(dpLeft[n - 1], dpRight[n - 1]);
    }

    private int[] prepareLeftWall(Robot[] robots, int n, int[] walls) {
        int[] leftWall = new int[n];
        int wallSize = walls.length;
        int left = 0;
        int right = -1;

        for (int i = 0; i < n; i++) {
            Robot robot = robots[i];
            int prevRobotPosition = (i == 0) ? NEG_INF : robots[i - 1].position;
            int shootStart = Math.max(prevRobotPosition + 1, robot.position - robot.distance);
            int shootEnd = robot.position;

            while (right + 1 < wallSize && walls[right + 1] <= shootEnd) ++right;
            while (left < wallSize && walls[left] < shootStart) ++left;

            if (left <= right) leftWall[i] = right - left + 1;
        }
        return leftWall;
    }

    private int[] prepareRightWall(Robot[] robots, int n, int[] walls) {
        int[] rightWall = new int[n];
        int wallSize = walls.length;
        int left = 0;
        int right = -1;

        for (int i = 0; i < n; i++) {
            Robot robot = robots[i];
            int nextRobotPosition = (i == n - 1) ? INF : robots[i + 1].position;
            int shootStart = robot.position;
            int shootEnd = Math.min(nextRobotPosition - 1, robot.position + robot.distance);

            while (right + 1 < wallSize && walls[right + 1] <= shootEnd) ++right;
            while (left < wallSize && walls[left] < shootStart) ++left;

            if (left <= right) rightWall[i] = right - left + 1;
        }
        return rightWall;
    }


    private int[] prepareCommon(Robot[] robots, int n, int[] walls) {
        int[] common = new int[n];
        int wallSize = walls.length;
        int left = 0;
        int right = -1;

        for (int i = 1; i < n; i++) {
            Robot prev = robots[i - 1];
            Robot curr = robots[i];
            int shootStart = Math.max(prev.position + 1, curr.position - curr.distance);
            int shootEnd = Math.min(curr.position - 1, prev.position + prev.distance);

            if (shootStart > shootEnd) continue;

            while (right + 1 < wallSize && walls[right + 1] <= shootEnd) ++right;
            while (left < wallSize && walls[left] < shootStart) ++left;

            if (left <= right) common[i] = right - left + 1;
        }
        return common;
    }
}
```

---
