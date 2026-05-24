# <u>162. Find Peak Element</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/find-peak-element/

---

## 🧠 Intuition:
* 🔹 A peak element is an element greater than its neighbors.

* 🔹 Use Binary Search because one side of the array will always contain a peak.

* 🔹 Find the middle index `mid`.

* 🔹 Compare `nums[mid]` with `nums[mid + 1]`.

* 🔹 If `nums[mid] >= nums[mid + 1]`, it means we are on the decreasing slope, so a peak exists on the left side (including mid).

* 🔹 Otherwise, we are on the increasing slope, so a peak exists on the right side.

* 🔹 Shrink the search space accordingly until `low == high`.

* 🔹 The final index `low` (or `high`) will be the peak element index.

---

## ⏱ Time Complexity

**O(log n)**

* Binary search halves the search space each step.
    
---

## 📦 Space Complexity

**O(1)**

* Only constant extra space is used.

---

## 💻 Java Code

```java
class Solution {
    public int findPeakElement(int[] nums) {
        int low = 0, high = nums.length - 1;

        while (low < high) {
          int mid = (low + high) / 2;
          if (nums[mid] >= nums[mid + 1])
            high = mid;
          else
            low = mid + 1;
        }

        return low;
    }
}
```

---