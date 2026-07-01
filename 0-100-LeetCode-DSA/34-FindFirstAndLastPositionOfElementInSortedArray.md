# <u>34. Find First and Last Position of Element in Sorted Array</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/

---

## 🧠 Intuition:
* 🔹 Since the array is **sorted**, use **Binary Search** to efficiently find the target's positions.

* 🔹 Perform the **first Binary Search** to find the **leftmost (first) occurrence** of the target:
    - Whenever the target is found, store the index and continue searching in the **left half** to check for an earlier occurrence.

* 🔹 If the target is not found in the first search, return `[-1, -1]` immediately.

* 🔹 Perform the **second Binary Search** to find the **rightmost (last) occurrence** of the target:
    - Whenever the target is found, store the index and continue searching in the **right half** to check for a later occurrence.

* 🔹 Return the indices of the first and last occurrences as the final answer.

* 🔹 Using two Binary Searches avoids scanning the array and keeps the solution efficient.


---

## ⏱ Time Complexity

**O(log n)**

* Two Binary Searches are performed, each taking O(log n).
    
---

## 📦 Space Complexity

**O(1)**

* Only a few extra variables are used.

---

## 💻 Java Code

```java
class Solution {
    public int firstOccurenceOfTarget(int nums[], int target) {
        int low = 0, high = nums.length - 1;
        int ans = -1;
        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (nums[mid] == target) {
                ans = mid;
                high = mid - 1;
            } else if (target > nums[mid]) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }
        return ans;
    }

    public int lastOccurenceOfTarget(int nums[], int target) {
        int low = 0, high = nums.length - 1;
        int ans = -1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (nums[mid] == target) {
                ans = mid;
                low = mid + 1;
            } else if (target > nums[mid]) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }
        return ans;
    }

    public int[] searchRange(int[] nums, int target) {
        int firstIdx = firstOccurenceOfTarget(nums, target);

        if (firstIdx == -1) {
            return new int[] {
                -1,
                -1
            };
        }

        int lastIdx = lastOccurenceOfTarget(nums, target);

        return new int[] {
            firstIdx,
            lastIdx
        };
    }
}
```

---