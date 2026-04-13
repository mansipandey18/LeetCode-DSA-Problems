# <u>1848. Minimum Distance to the Target Element</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/minimum-distance-to-the-target-element/

---

## 🧠 Intuition:
* 🔹 The goal is to find the **minimum distance from a given `start` index to any occurrence of `target`** in the array.

* 🔹 Initialize `minDistance` with a large value (like array length).

* 🔹 Traverse the array from left to right:
    - For each index, check if `nums[currentIndex] == target`.
    - If yes:
        * Compute distance = `|currentIndex - start|`.
        * Update `minDistance` with the smaller value.

* 🔹 Continue scanning the entire array to ensure we find the **closest occurrence**.

* 🔹 Finally, return the minimum distance found.

* 🔹 This works because we check **all possible positions of the target** and pick the nearest one.

---

## ⏱ Time Complexity

**O(n)**

* Let :
    - `n` = length of the array.

* Single traversal of array → `O(n)`

---

## 📦 Space Complexity

**O(1)**

* Only a few variables are used (minDistance, loop variable).

---

## 💻 Java Code

```java
class Solution {
    public int getMinDistance(int[] nums, int target, int start) {
        int arrayLength = nums.length;
      
        // Initialize minimum distance to the maximum possible value (array length)
        int minDistance = arrayLength;
      
        // Iterate through each element in the array
        for (int currentIndex = 0; currentIndex < arrayLength; ++currentIndex) {
            // Check if current element equals the target value
            if (nums[currentIndex] == target) {
                // Calculate distance between current index and start position
                int currentDistance = Math.abs(currentIndex - start);
              
                // Update minimum distance if current distance is smaller
                minDistance = Math.min(minDistance, currentDistance);
            }
        }
      
        // Return the minimum distance found
        return minDistance;
    }
}
```

---