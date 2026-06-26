# <u>918. Maximum Sum Circular Subarray</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-sum-circular-subarray/

---

## 🧠 Intuition:
* 🔹 The maximum circular subarray can be of **two types**:
    - **Normal subarray** (does not wrap around the end of the array).
    - **Circular subarray** (wraps around, taking elements from both the end and the beginning).

* 🔹 Use **Kadane's Algorithm** to find the maximum normal subarray sum (`cand1`).

* 🔹 For the circular case:
    - A circular maximum subarray is equivalent to **Total Sum − Minimum Subarray Sum**.
    - Instead of writing a separate algorithm for the minimum subarray, negate every element of the array.
    - Running Kadane on the negated array gives the **maximum sum of the negated array**, which equals the **negative of the minimum subarray sum** in the original array.
    - Therefore, `cand2 = totalSum + maxSubarraySum(negatedArray)`.

* 🔹 If `cand2 == 0`, it means all elements are negative, so the circular case is invalid (it would select an empty subarray).

* 🔹 In that case, return the normal maximum subarray sum (`cand1`).

* 🔹 Otherwise, return the larger value between the normal and circular subarray sums.


---

## ⏱ Time Complexity

**O(n)**

* One pass to compute the total sum and negated array, plus two runs of Kadane’s Algorithm.

---

## 📦 Space Complexity

**O(n)**

* Extra array is used to store the negated values.

---

## 💻 Java Code

```java
class Solution {
    public int maxSubarraySumCircular(int[] nums) {
        int n = nums.length;
        boolean same_sign = true;
        int sum = 0;
        int[] neg = new int[n];
        for (int i = 0; i < n; i++) {
            neg[i] = -nums[i];
            sum += nums[i];
        }
        int cand1 = maxSubarraySum(nums);
        int cand2 = sum + maxSubarraySum(neg);
        if (cand2 == 0) {
            return cand1;
        }
        return Math.max(cand1, cand2);
    }

    public int maxSubarraySum(int[] arr) {
        
        // Stores the result (maximum sum found so far)
        int res = arr[0];
        
        // Maximum sum of subarray ending at current position
        int maxEnding = arr[0];

        for (int i = 1; i < arr.length; i++) {
            
            // Either extend the previous subarray or start 
            // new from current element
            maxEnding = Math.max(maxEnding + arr[i], arr[i]);
          
            // Update result if the new subarray sum is larger
            res = Math.max(res, maxEnding);
        }
        return res;
    }
}
```

---