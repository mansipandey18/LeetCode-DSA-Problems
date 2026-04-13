# <u>643. Maximum Average Subarray I</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-average-subarray-i/

---

## 🧠 Intuition:
* 🔹 The problem asks for the **maximum average of any subarray of size `k`**.

* 🔹 Instead of checking all subarrays (which is slow), use the **sliding window technique**.

* 🔹 First, calculate the sum of the **first window of size `k`**.

* 🔹 Store this as both `windowSum` and `maxSum`.

* 🔹 Then slide the window one step at a time:
    - Add the next element (`nums[i]`).
    - Remove the element that goes out of the window (`nums[i - k]`).

* 🔹 This way, we avoid recalculating the sum from scratch.

* 🔹 After each slide, update `maxSum` if the current sum is larger.

* 🔹 At the end, divide the maximum sum by `k` to get the **maximum average**.

* 🔹 This works efficiently because each element is added and removed **only once**.

---

## ⏱ Time Complexity

**O(n)**

* Let 
    - `n` = length of array.

* Initial window sum → **O(k)**

* Sliding window traversal → **O(n - k)**

    
---

## 📦 Space Complexity

**O(1)**

* Only a few variables are used.

---

## 💻 Java Code

```java
class Solution {
    public double findMaxAverage(int[] nums, int k) {
        int windowSum = 0;
        for (int i = 0; i < k; i++) {
            windowSum += nums[i];
        }
      
        int maxSum = windowSum;
      
        for (int i = k; i < nums.length; i++) {
            windowSum += nums[i] - nums[i - k];
          
            maxSum = Math.max(maxSum, windowSum);
        }
      
        return (double) maxSum / k;
    }
}   
```

---