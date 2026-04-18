# <u>04. Median of Two Sorted Arrays</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/median-of-two-sorted-arrays/

---

## 🧠 Intuition:
* 🔹 Idea is to **divide both sorted arrays into two halves** such that left half contains smaller elements and right half contains larger elements

* 🔹 Instead of merging arrays (which is costly), we use **binary search on the smaller array** to find correct partition

* 🔹 We choose a partition `mid1` in `nums1` and calculate corresponding partition `mid2` in `nums2` so that total elements in left half = `(n1 + n2 + 1)/2`

* 🔹 Now check boundary elements:
    - `l1` = left element of nums1, `l2` = left element of nums2
    - `r1` = right element of nums1, `r2` = right element of nums2

* 🔹 Correct partition condition: **l1 ≤ r2 and l2 ≤ r1** (means all left elements ≤ all right elements)

* 🔹 If partition is correct:
    - If total length is odd → median = max(l1, l2)
    - If even → median = average of max(l1, l2) and min(r1, r2)

* 🔹 If `l1 > r2`, move left in nums1 (reduce partition)

* 🔹 If `l2 > r1`, move right in nums1 (increase partition)

* 🔹 This ensures we find median efficiently without merging

---

## ⏱ Time Complexity

**O(og(min(n1, n2)))**

* binary search on smaller array

---

## 📦 Space Complexity

**O(1)**
  
* no extra space used.

---

## 💻 Java Code

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int n1 = nums1.length, n2 = nums2.length;
        int n = n1 + n2;

        //if n1 is bigger swap the arrays
        if(n1 > n2) return findMedianSortedArrays(nums2, nums1);

        int left = (n1 + n2 + 1)/2; // length of left half

        // apply binary search
        int low = 0, high = n1;
        while(low <= high){
            int mid1 = (low + high) / 2;
            int mid2 = left - mid1;

            // calculate L1, L2, R1 & R2
            int l1 = (mid1 > 0) ? nums1[mid1 - 1] : Integer.MIN_VALUE;
            int l2 = (mid2 > 0) ? nums2[mid2 - 1] : Integer.MIN_VALUE;
            int r1 = (mid1 < n1) ? nums1[mid1] : Integer.MAX_VALUE;
            int r2 = (mid2 < n2) ? nums2[mid2] : Integer.MAX_VALUE;

            if(l1 <= r2 && l2 <= r1){
                if(n % 2 == 1) return Math.max(l1, l2);
                else return ((double)(Math.max(l1, l2) + Math.min(r1, r2))) / 2.0;
            } 
            else if(l1 > r2) high = mid1 - 1; 
            else low = mid1 + 1;
        }
        return 0;
    }
}
```

---