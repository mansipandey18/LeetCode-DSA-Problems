# <u>739. Daily Temperatures</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/daily-temperatures/

---

## 🧠 Intuition:
* 🔹 We need to find the **next warmer day** for each temperature.

* 🔹 Use a **Monotonic Decreasing Stack** to store indices of temperatures.

* 🔹 Traverse the array **from right to left**, so future days are already processed.

* 🔹 While the stack is not empty and the temperature at the top index is **less than or equal to** the current temperature, remove it because it cannot be the next warmer day.

* 🔹 After removing smaller/equal temperatures:
    - If the stack is not empty, the top index represents the **next warmer day**.
    - The answer is `stack.peek() - currentIndex`.

* 🔹 Push the current index onto the stack for future comparisons.

* 🔹 This ensures each index is pushed and popped at most once, making the solution efficient.

---

## ⏱ Time Complexity

**O(n)**

* Each index is pushed onto the stack once and popped at most once.

    
---

## 📦 Space Complexity

**O(n)**

* Stack can store up to `n` indices in the worst case.
* Result array stores `n` answers.

---

## 💻 Java Code

```java
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int length = temperatures.length;
        Deque<Integer> stack = new ArrayDeque<>();
        int[] result = new int[length];
      
        for (int currentIndex = length - 1; currentIndex >= 0; currentIndex--) {
            while (!stack.isEmpty() && temperatures[stack.peek()] <= temperatures[currentIndex]) {
                stack.pop();
            }
          
            if (!stack.isEmpty()) {
                result[currentIndex] = stack.peek() - currentIndex;
            }
          
            stack.push(currentIndex);
        }
      
        return result;
    }
}   
```

---