# <u>1665. Minimum Initial Energy to Finish Tasks</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/minimum-initial-energy-to-finish-tasks/

---

## 🧠 Intuition:
* 🔹 Each task has:
    - `actual[i]` → energy consumed after completing the task
    - `minimum[i]` → minimum energy required before starting the task

* 🔹 The goal is to find the minimum initial energy needed to complete all tasks

* 🔹 Use a greedy strategy to decide task order

* 🔹 Sort tasks based on `(actual - minimum)` in ascending order
    - Tasks needing a larger energy buffer are handled earlier
    - This minimizes extra energy additions later

* 🔹 Maintain two variables:
    - `currentEffort` → current available energy
    - `totalMinimumEffort` → minimum initial energy accumulated so far

* 🔹 For every task:
    - If current energy is less than the required minimum energy:
        * Add the missing energy to `totalMinimumEffort`
        * Update `currentEffort` to meet the requirement
    - Perform the task by subtracting `actualEffortNeeded` from current energy

* 🔹 By always ensuring enough energy before each task, we guarantee the minimum starting energy needed overall

---

## ⏱ Time Complexity

**O(n log n)**

* Where:
    - `n` = number of tasks

* Sorting tasks takes: **O(n log n)**
* Traversing all tasks once takes: **O(n)**
    
---

## 📦 Space Complexity

**O(1)**

* Sorting is done in-place apart from constant variables used

---

## 💻 Java Code

```java
class Solution {
    public int minimumEffort(int[][] tasks) {
        Arrays.sort(tasks, (task1, task2) -> 
            (task1[0] - task1[1]) - (task2[0] - task2[1])
        );
      
        int totalMinimumEffort = 0;  // The minimum initial effort needed
        int currentEffort = 0;       // Current available effort after completing tasks
      
        for (int[] task : tasks) {
            int actualEffortNeeded = task[0];   // Effort consumed to complete the task
            int minimumEffortRequired = task[1]; // Minimum effort required to start the task
          
            if (currentEffort < minimumEffortRequired) {
                int additionalEffortNeeded = minimumEffortRequired - currentEffort;
                totalMinimumEffort += additionalEffortNeeded;
                currentEffort = minimumEffortRequired;
            }
          
            currentEffort -= actualEffortNeeded;
        }
      
        return totalMinimumEffort;
    }
}
```

---