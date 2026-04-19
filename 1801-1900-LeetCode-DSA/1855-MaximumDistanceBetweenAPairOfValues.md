# <u>1855. Maximum Distance Between a Pair of Values</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-distance-between-a-pair-of-values/

---

## 🧠 Intuition:
* 🔹 Goal is to find maximum `j - i` such that `i ≤ j` and `nums1[i] ≤ nums2[j]`

* 🔹 For each index `i` in `nums1`, we want the **farthest valid index j in nums2**

* 🔹 Since both arrays are **non-increasing (sorted)**, we can use **binary search** on `nums2`

* 🔹 For each `nums1[i]`, search in `nums2` from index `i` to end to find the **first index where condition breaks** (`nums2[mid] < nums1[i]`)

* 🔹 This gives us the boundary of valid indices → all indices before this are valid

* 🔹 If no invalid index is found, then all elements till end are valid

* 🔹 So, the **last valid j** is either:
    - `n2 - 1` (if all valid), or
    - `firstInvalidIndex - 1`

* 🔹 Update answer with `j - i` if `j ≥ i`

* 🔹 Repeat for all `i` and keep track of maximum distance

---

## ⏱ Time Complexity

**O(n1 * log n2)**

* Outer loop runs for every element of `nums1 → O(n1)`
* For each element, we perform **binary search** on `nums2 → O(log n2)`

---

## 📦 Space Complexity

**O(1)**

* Only a few variables are used.

---

## 💻 Java Code

```java
class Solution {
    public int maxDistance(int[] nums1, int[] nums2) {
        int maxDistance = 0;
        int n1 = nums1.length;
        int n2 = nums2.length;

        for (int i = 0; i < n1; i++) {
            int value = nums1[i];

            int left = i;
            int right = n2 - 1;
            int firstTrueIndex = -1;

            while (left <= right) {
                int mid = left + (right - left) / 2;
                if (nums2[mid] < value) {  
                    firstTrueIndex = mid;
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            }

            // Calculate the last valid j
            int lastValidJ;
            if (firstTrueIndex == -1) {
                // All positions from i to end are valid
                lastValidJ = n2 - 1;
            } else {
                // Last valid position is one before first invalid
                lastValidJ = firstTrueIndex - 1;
            }

            // Update maximum distance if valid pair exists
            if (lastValidJ >= i) {
                maxDistance = Math.max(maxDistance, lastValidJ - i);
            }
        }

        return maxDistance;
    
    }
}
```

---