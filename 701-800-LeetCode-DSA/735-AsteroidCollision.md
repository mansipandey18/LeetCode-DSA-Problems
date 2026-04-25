# <u>735. Asteroid Collision</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/asteroid-collision/

---

## 🧠 Intuition:
* 🔹 Collision only happens when a **right-moving asteroid (+ve)** meets a **left-moving asteroid (-ve)**, so a stack helps track possible collisions

* 🔹 Use a stack to store asteroids that are still alive after processing

* 🔹 If the current asteroid is positive, it simply moves right and cannot collide with previous left-moving asteroids, so push it into the stack

* 🔹 If the current asteroid is negative, it may collide with positive asteroids already in the stack

* 🔹 Keep removing smaller positive asteroids from the top of the stack while their size is less than the current negative asteroid (`stack top < abs(current)`)

* 🔹 After that:
    - If top asteroid has the same size → both destroy each other, so remove the top
    - If stack becomes empty or top is also negative → current asteroid survives, so push it
    - If top positive asteroid is larger → current asteroid gets destroyed, so do nothing

* 🔹 At the end, the stack contains all surviving asteroids in correct order

* 🔹 Convert stack to array and return the result.


---

## ⏱ Time Complexity

**O(n)**

* Each asteroid is pushed and popped at most once

    
---

## 📦 Space Complexity

**O(n)**

* Stack may store all asteroids in worst case

---

## 💻 Java Code

```java
class Solution {
    public int[] asteroidCollision(int[] asteroids) {
        Deque<Integer> stack = new ArrayDeque<>();
      
        for (int asteroid : asteroids) {
            if (asteroid > 0) {
                stack.offerLast(asteroid);
            } else {
                while (!stack.isEmpty() && stack.peekLast() > 0 && stack.peekLast() < -asteroid) {
                    stack.pollLast();
                }
              
                if (!stack.isEmpty() && stack.peekLast() == -asteroid) {
                    stack.pollLast();
                } else if (stack.isEmpty() || stack.peekLast() < 0) {
                    stack.offerLast(asteroid);
                }
            }
        }
      
        return stack.stream().mapToInt(Integer::valueOf).toArray();    
    }
}   
```

---