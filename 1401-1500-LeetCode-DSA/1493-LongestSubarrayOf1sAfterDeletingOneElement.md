# <u>1594. Maximum Non Negative Product in a Matrix</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/longest-subarray-of-1s-after-deleting-one-element/

---

## 🧠 Intuition:
* 🔹 We need the **longest subarray of 1s after deleting exactly** one element.

* 🔹 Idea: treat every index as the **element we delete**.

* 🔹 For each index `i`, we calculate:
    - **Left side** → how many continuous 1s are just before `i`
    - **Right side** → how many continuous 1s are just after `i`

* 🔹 Use two arrays:
    - `leftOnesCount[i]` → count of consecutive 1s ending before `i`
    - `rightOnesCount[i]` → count of consecutive 1s starting after `i`

* 🔹 If we delete index `i`, total length = `leftOnesCount[i] + rightOnesCount[i]`

* 🔹 Take maximum over all indices.

* 🔹 Special case: if the array is all 1s → we must delete one element, so answer = `n - 1`.

---

## ⏱ Time Complexity

**O(n)**

* One pass to build left array + one pass for right + one pass to compute answer
    
---

## 📦 Space Complexity

**O(n)**

* Two extra arrays of size `n`.

---

## 💻 Java Code

```java
class Solution {
    public int longestSubarray(int[] nums) {
        int length = nums.length;

        int[] leftOnesCount = new int[length], rightOnesCount = new int[length];

        for (int i = 1; i < length; ++i) {
            if (nums[i - 1] == 1) {
                leftOnesCount[i] = leftOnesCount[i - 1] + 1; 
            }
        }

        for (int i = length - 2; i >= 0; --i) {
            if (nums[i + 1] == 1) {
                rightOnesCount[i] = rightOnesCount[i + 1] + 1;
            }
        }

        int maxSubarrayLength = 0;

        for (int i = 0; i < length; ++i) {
            maxSubarrayLength = Math.max(maxSubarrayLength, leftOnesCount[i] + rightOnesCount[i]);
        }

        if (maxSubarrayLength == length) {
            maxSubarrayLength--;
        }

        return maxSubarrayLength;
    }
}
```

---