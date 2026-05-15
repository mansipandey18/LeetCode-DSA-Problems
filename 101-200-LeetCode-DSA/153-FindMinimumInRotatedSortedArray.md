# <u>153. Find Minimum in Rotated Sorted Array</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/

---

## 🧠 Intuition:
* 🔹 The array was originally sorted, then rotated, so at least one half of the array is always sorted.

* 🔹 Use Binary Search to efficiently locate the minimum element.

* 🔹 Maintain two pointers: low and high to search within the current range.

* 🔹 Find the middle index mid in each iteration.

* 🔹 If nums[low] <= nums[mid], it means the left half is sorted:
    - The minimum in this half is nums[low].
    - Store it in ans.
    - Eliminate the left half and move to the right half (low = mid + 1).

* 🔹 Otherwise, the right half is sorted and the rotation point lies in the left half:
    - nums[mid] can be the minimum, so update ans.
    - Eliminate the right half (high = mid - 1).

* 🔹 Repeat until the search space becomes empty.

* 🔹 The smallest recorded value in `ans` is the minimum element in the rotated sorted array.

---

## ⏱ Time Complexity

**O(log n)**

* Binary Search reduces the search space by half in every iteration.
    
---

## 📦 Space Complexity

**O(1)**

* Only a few variables are used, no extra space required.

---

## 💻 Java Code

```java
class Solution {
    public int findMin(int[] nums) {
        int low  = 0, high = nums.length-1, ans = Integer.MAX_VALUE;

        while(low <= high){
            int mid = (low + high)/2;

            // if left part is sorted
            if(nums[low] <= nums[mid]){
                // keep the minimum
                ans = Math.min(ans, nums[low]);

                // eliminate left half
                low = mid + 1;
            } else{ // if right part is sorted
                // keep the minimum
                ans = Math.min(ans, nums[mid]);

                // eliminate right half
                high = mid - 1;
            }
        }
        return ans;
    }
}
```

---