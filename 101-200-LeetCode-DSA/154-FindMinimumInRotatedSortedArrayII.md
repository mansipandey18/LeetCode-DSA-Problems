# <u>154. Find Minimum in Rotated Sorted Array II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/

---

## 🧠 Intuition:
* 🔹 The array is originally sorted but rotated, and it may contain duplicates.

* 🔹 Use Modified Binary Search to efficiently find the minimum element.

* 🔹 Compare `nums[mid]` with `nums[right]` to decide which half contains the minimum.

* 🔹 Case 1: `nums[mid] > nums[right]`
    - Minimum must be in the right half.
    - Move `left = mid + 1.`

* 🔹 Case 2: `nums[mid] < nums[right]`
    - Minimum lies in the left half including mid.
    - Move `right = mid.`

* 🔹 Case 3: `nums[mid] == nums[right]`
    - Duplicates create ambiguity, so we cannot decide the correct half.
    - Safely reduce search space by doing `right--`.

* 🔹 Continue shrinking the search space until `left == right`.

* 🔹 At the end, `nums[left]` will be the minimum element in the rotated sorted array.

---

## ⏱ Time Complexity

**O(n)**

* Average Case: `O(log n)`
* Worst Case: `O(n)`
* Happens when many duplicate elements exist (e.g., `[1,1,1,1,1]`).
    
---

## 📦 Space Complexity

**O(1)**

* Only constant extra space required.

---

## 💻 Java Code

```java
class Solution {
    public int findMin(int[] nums) {
        int left = 0;
        int right = nums.length - 1;
      
        while (left < right) {
            int mid = (left + right) >> 1;
          
            if (nums[mid] > nums[right]) {
                left = mid + 1;
            } 
            else if (nums[mid] < nums[right]) {
                right = mid;
            } 
            else {
                right--;
            }
        }
      
        return nums[left];
    }
}
```

---