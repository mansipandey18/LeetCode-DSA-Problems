# <u>70. Climbing Stairs</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/climbing-stairs/

---

## 🧠 Intuition:
* 🔹 The number of ways to reach the current step depends only on the previous two steps.

* 🔹 To reach step `i`, you can either:
    - Take **1 step** from `i - 1`, or
    - Take **2 steps** from `i - 2`.

* 🔹 This follows the Fibonacci pattern:
    - `ways(i) = ways(i - 1) + ways(i - 2)`.

* 🔹 Instead of storing all previous values in a DP array, keep only the last two results (`first` and `second`).

* 🔹 In each iteration:
    - Compute the next number as `first + second`.
    - Shift the two variables forward for the next calculation.

* 🔹 After completing `n` iterations, `second` stores the total number of distinct ways to reach the top.

---

## ⏱ Time Complexity

**O(n)**

* We iterate through the stairs exactly once. 
---

## 📦 Space Complexity

**O(1)**

* Only a few variables (`first`, `second`, and `next`) are used, regardless of the input size.

---

## 💻 Java Code

```java
class Solution {
    public int climbStairs(int n) {
        int first = 0, second = 1;
      
        // Loop through number of steps n
        for (int i = 0; i < n; i++) {
            // Calculate next number in the series
            int next = first + second;
          
            // Update the previous two numbers for next iteration
            first = second;
            second = next;
        }
      
        // The 'second' variable holds the total ways to reach the top
        return second;
    }
}
```

---
