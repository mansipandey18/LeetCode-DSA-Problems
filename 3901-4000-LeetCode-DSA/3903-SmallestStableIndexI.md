# <u>3903. Smallest Stable Index I</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/smallest-stable-index-i/
---

## 🧠 Intuition:
* 🔹 First, create a **suffix minimum array** where `suffixMin[i]` stores the smallest element from index `i` to the end.

* 🔹 Then traverse the array from **left to right** while maintaining `prefixMax`, the maximum value encountered from index `0` to `i`.

* 🔹 For every index `i`, compare the maximum of the prefix with the minimum of the suffix.

* 🔹 An index `i` is stable if:
    - `prefixMax - suffixMin[i] <= k`

* 🔹 Since indices are checked from left to right, the **first index satisfying the condition is the smallest stable index**.

* 🔹 If no index satisfies the condition, return `-1`.

---

## ⏱ Time Complexity

**O(n)**

* Building suffixMin → `O(n)`
* Traversing the array → `O(n)`
    
---

## 📦 Space Complexity

**O(n)**

* `suffixMin` array requires `O(n)` space.
* Other variables use `O(1)` extra space.

---

## 💻 Java Code

```java
class Solution {
    public int firstStableIndex(int[] nums, int k) {
        int n = nums.length;
        if (n == 0) return -1;

        // Step 1: Precompute suffix minimums
        int[] suffixMin = new int[n];
        suffixMin[n - 1] = nums[n - 1];
        for (int i = n - 2; i >= 0; i--) {
            suffixMin[i] = Math.min(nums[i], suffixMin[i + 1]);
        }

        // Step 2: Traverse left to right and track prefix maximum
        int prefixMax = Integer.MIN_VALUE;
        for (int i = 0; i < n; i++) {
            prefixMax = Math.max(prefixMax, nums[i]);
            
            if (prefixMax - suffixMin[i] <= k) {
                return i;
            }
        }

        return -1;
    }
}
```

---