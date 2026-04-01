# <u>2751. Robot Collisions</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/robot-collisions/

---

## 🧠 Intuition:
* 🔹 Robots move either left (L) or right (R) and may collide.

* 🔹 A collision happens only when:
    - one robot moves right, and
    - another robot coming later moves left.

* 🔹 First, we sort robots by position so we can simulate movement from left → right correctly.

* 🔹 We keep a stack to store robots moving right because they may collide with future left-moving robots.

* 🔹 Traverse robots in sorted order:
    - If robot moves right, push it into the stack (waiting for collision).
    - If robot moves left, check collisions with right-moving robots from the stack.

* 🔹 During collision:
    - Robot with higher health survives and loses 1 health.
    - Robot with lower health gets destroyed.
    - If both have equal health → both destroyed.

* 🔹 Continue collisions until:
    - stack becomes empty, or
    - current robot dies.

* 🔹 After processing all robots, remaining robots with health > 0 are survivors.

* 🔹 Finally, return surviving robots’ healths in original order.

---

## ⏱ Time Complexity

**O(n log n)**

* **1️⃣ Sorting robots by position**
    - Sorting indices → O(n log n)

* **2️⃣ Collision simulation**
    - Each robot is pushed and popped at most once → O(n)
    
---

## 📦 Space Complexity

**O(n)**

* indices array → O(n)
* stack for collisions → O(n) (worst case)
* result list → O(n)

---

## 💻 Java Code

```java
class Solution {
    public List<Integer> survivedRobotsHealths(int[] positions, int[] healths, String directions) {
        int n = positions.length;
      
        // Create an array of indices to track original positions after sorting
        Integer[] indices = new Integer[n];
        for (int i = 0; i < n; i++) {
            indices[i] = i;
        }
      
        // Sort indices based on the actual positions of robots (left to right)
        Arrays.sort(indices, (i, j) -> Integer.compare(positions[i], positions[j]));
      
        // Stack to store indices of robots moving right (waiting for collision)
        Stack<Integer> stack = new Stack<>();
      
        // Process robots from left to right based on their positions
        for (int currentIndex : indices) {
            if (directions.charAt(currentIndex) == 'R') {
                // Robot moving right: add to stack (potential collision candidate)
                stack.push(currentIndex);
            } else {
                // Robot moving left: check for collisions with robots moving right
                while (!stack.isEmpty() && healths[currentIndex] > 0) {
                    int rightMovingRobotIndex = stack.pop();
                  
                    if (healths[rightMovingRobotIndex] > healths[currentIndex]) {
                        // Right-moving robot wins: decrease its health by 1
                        healths[rightMovingRobotIndex] -= 1;
                        healths[currentIndex] = 0;
                        stack.push(rightMovingRobotIndex); // Put winner back on stack
                    } else if (healths[rightMovingRobotIndex] < healths[currentIndex]) {
                        // Left-moving robot wins: decrease its health by 1
                        healths[currentIndex] -= 1;
                        healths[rightMovingRobotIndex] = 0;
                        // Continue checking for more collisions
                    } else {
                        // Both robots have equal health: both are destroyed
                        healths[currentIndex] = 0;
                        healths[rightMovingRobotIndex] = 0;
                    }
                }
            }
        }
      
        // Collect surviving robots' healths in their original order
        List<Integer> result = new ArrayList<>();
        for (int health : healths) {
            if (health > 0) {
                result.add(health);
            }
        }
      
        return result;
    }
}
```

---