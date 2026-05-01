# <u>396. Rotate Function</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/rotate-function/

---

## 🧠 Intuition:
* 🔹 The rotate function is defined as:
    - F(k) = 0⋅B<sub>k</sub>​[0] + 1⋅B<sub>k</sub>​[1] + .... + (n−1)⋅B<sub>k</sub>​[n − 1], where B<sub>k</sub> is the array after `k` rotations

* 🔹 A brute-force approach would recompute this for every rotation → **O(n²)**, which is inefficient

* 🔹 Key observation: we can derive a **relation between consecutive rotations** instead of recomputing from scratch

* 🔹 Let:
    - `F(0)` = initial value
    - `sum` = sum of all elements in the array

* 🔹 When we rotate the array by 1 step, every element’s index increases by 1, except the last element which moves to index 0

* 🔹 This leads to the recurrence relation:
    - **F(k) = F(k-1) + sum - n × lastElement**

* 🔹 So instead of recalculating, we update the value using the previous result

* 🔹 Steps:
    - Compute `F(0)` and total sum in one pass
    - Iteratively compute `F(1), F(2), ... F(n-1)` using the formula
    - Keep track of the maximum value encountered

* 🔹 This reduces redundant calculations and makes the solution efficient

* 🔹 Finally, return the maximum value among all rotations
---

## ⏱ Time Complexity

**O(n)**

* Initial computation of sum and F(0) → **O(n)**
* Loop to compute all rotations → **O(n)**

---

## 📦 Space Complexity

**O(1)**

* Only a few variables are used (`sum`, `currentFunctionValue`, `maxValue`)

---

## 💻 Java Code

```java
class Solution {
    public int maxRotateFunction(int[] nums) {
        int currentFunctionValue = 0;
      
        int totalSum = 0;      
        int arrayLength = nums.length;
      
        for (int i = 0; i < arrayLength; ++i) {
            currentFunctionValue += i * nums[i];  
            totalSum += nums[i];
        }
      
        int maxValue = currentFunctionValue;
      
        for (int rotation = 1; rotation < arrayLength; ++rotation) {
            currentFunctionValue = currentFunctionValue + totalSum - arrayLength * nums[arrayLength - rotation];
            maxValue = Math.max(maxValue, currentFunctionValue);
        }
      
        return maxValue;
    }
}
```

---