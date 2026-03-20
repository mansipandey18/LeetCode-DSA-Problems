# <u>42. Trapping Rain Water</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/trapping-rain-water/

---

## 🧠 Intuition:
* 🔹 Water can be trapped at a position only if there are taller bars on both the left and right sides.

* 🔹 The amount of water stored above a bar depends on the minimum height boundary around it.

* 🔹 For every index, we need to know:

    - the tallest bar on the left (leftMax)

    - the tallest bar on the right (rightMax).

* 🔹 The water level at index i is determined by:

    - min(leftMax[i], rightMax[i])

* 🔹 The trapped water at that index equals:

    - waterLevel − height[i]

* 🔹 To compute efficiently:

    - build a leftMax array while moving left → right.

    - build a rightMax array while moving right → left.

* 🔹 Then iterate once more and sum the water trapped at each position.

* 🔹 Add all trapped water values to get the final answer.---

## ⏱ Time Complexity

**O(n)**

* Building leftMax array → O(n)

* Building rightMax array → O(n)

* Calculating trapped water → O(n)
    

---

## 📦 Space Complexity

**O(n)**

* Two extra arrays of size n are used (leftMax and rightMax).

---

## 💻 Java Code

```java
class Solution {
    public int trap(int[] height) {
        // calculate the leftMaxBoundary array
        int leftMax[] = new int[height.length];
        leftMax[0] = height[0];
        for(int i = 1; i < height.length; i++){
            leftMax[i] = Math.max(height[i], leftMax[i-1]);
        }

        // calculate the rightMaxBoundary array

        int rightMax[] = new int[height.length];
        rightMax[height.length - 1] = height[height.length - 1];
        for(int i = height.length-2; i >= 0; i--){
            rightMax[i] = Math.max(height[i], rightMax[i+1]);
        }

        int trappedWater = 0;
        // loop
        for(int i = 0; i < height.length; i++){
        // waterLevel = Math.min(leftMaxBoundary, rightMaxBoundary)
            int waterLevel = Math.min(leftMax[i], rightMax[i]);
        // trappedWater = waterLevel - height[i]
            trappedWater += waterLevel - height[i];
        }
        return trappedWater;
    }
}
```

---