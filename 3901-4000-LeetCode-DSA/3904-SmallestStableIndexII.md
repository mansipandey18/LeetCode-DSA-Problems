# <u>3904. Smallest Stable Index II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/smallest-stable-index-ii/

---

## 🧠 Intuition:
* 🔹 First, compute a **suffix minimum array** where `suffMin[i]` stores the smallest element from index `i` to the end.

* 🔹 Then traverse the array from left to right while maintaining `prefMax`, the **maximum element seen so far**.

* 🔹 For every index `i`, the array can be divided at `i` into:
    - **Prefix:** `0 ... i` → maximum = `prefMax`
    - **Suffix:** `i ... n-1` → minimum = `suffMin[i]`

* 🔹 An index is **stable** when the difference between the prefix maximum and suffix minimum is at most `k`:
    - `prefMax - suffMin[i] <= k`

* 🔹 Since we check indices from left to right, the **first index satisfying the condition is the smallest stable index**.

* 🔹 If no index satisfies the condition, return `-1`.

---

## ⏱ Time Complexity

**O(n)**

* Building the suffix minimum array → `O(n)`
* Traversing the array → `O(n)`
    
---

## 📦 Space Complexity

**O(n)**

* `suffMin` array of size `n` → `O(n)`
* Other variables use constant space.

---

## 💻 Java Code

```java
class Solution {
    public int firstStableIndex(int[] nums, int k) {
        int n = nums.length;
        if (n == 0) return -1;

        // Step 1: Precompute suffix minimums
        int[] suffMin = new int[n];
        suffMin[n - 1] = nums[n - 1];
        for (int i = n - 2; i >= 0; i--) {
            suffMin[i] = Math.min(nums[i], suffMin[i + 1]);
        }

        // Step 2: Traverse and find the smallest stable index
        int prefMax = nums[0];
        for (int i = 0; i < n; i++) {
            prefMax = Math.max(prefMax, nums[i]);
            
            // Step 3: Check stability condition
            if (prefMax - suffMin[i] <= k) {
                return i;
            }
        }

        return -1;
    }
}
```

---