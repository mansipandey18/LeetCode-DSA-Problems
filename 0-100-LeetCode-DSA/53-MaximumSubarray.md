# <u>53. Maximum Subarray</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-subarray/

---

## 🧠 Intuition:
* 🔹 We want the **maximum sum of any contiguous subarray**.

* 🔹 At each index, we decide:
    - **Extend the previous subarray** if its sum is positive.
    - **Start a new subarray** from the current element if the previous sum is negative.

* 🔹 A negative running sum only decreases future sums, so we discard it by taking `Math.max(currentMax, 0)`.

* 🔹 `currentMax` stores the **best subarray sum ending at the current index**.

* 🔹 `max` stores the **overall maximum subarray sum found so far**.

* 🔹 As we traverse the array once, we continuously update both values.

* 🔹 This is the classic **Kadane’s Algorithm**, which finds the answer in a single pass.

---

## ⏱ Time Complexity

**O(n)**

* each element is processed once.
    
---

## 📦 Space Complexity

**O(1)**

* only a few variables are used.

---

## 💻 Java Code

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int max = nums[0];
        int currentMax = nums[0];
      
        for (int i = 1; i < nums.length; ++i) {
            currentMax = Math.max(currentMax, 0) + nums[i];
          
            max = Math.max(max, currentMax);
        }
        return max;
    }
}
```

---