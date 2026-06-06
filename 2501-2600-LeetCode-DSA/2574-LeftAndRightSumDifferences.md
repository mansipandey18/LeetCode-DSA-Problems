# <u>2574. Left and Right Sum Differences</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/left-and-right-sum-differences/

---

## 🧠 Intuition:
* 🔹 We need to compute, for each index, the **absolute difference between left sum and right sum**.

* 🔹 Instead of recalculating sums for every index (which would be costly), we maintain two running variables:
    - `leftSum` → sum of elements to the left of current index.
    - `rightSum` → sum of elements to the right of current index.

* 🔹 Initially:
    - `leftSum = 0`
    - `rightSum = total sum of the array`

* 🔹 For each index `i`:
    - Remove `nums[i]` from `rightSum` first (since it is not part of right side anymore).
    - Compute result as `abs(leftSum - rightSum)`.
    - Add `nums[i]` to `leftSum` for future iterations.

* 🔹 This avoids nested loops and ensures a single pass solution.

---

## ⏱ Time Complexity

**O(n)**

* Computing total sum: `O(n)`
* Single traversal of array: `O(n)`

---

## 📦 Space Complexity

**O(n)**

* Output array of size `n` : `O(n)`
* Extra variables used: `O(1)`


---

## 💻 Java Code

```java
class Solution {
    public int[] leftRightDifference(int[] nums) {
        int leftSum = 0;
        int rightSum = Arrays.stream(nums).sum();
      
        int n = nums.length;
      
        int[] result = new int[n];
      
        for (int i = 0; i < n; i++) {
            rightSum -= nums[i];
          
            result[i] = Math.abs(leftSum - rightSum);
          
            leftSum += nums[i];
        }
      
        return result;

    }
}
```

---