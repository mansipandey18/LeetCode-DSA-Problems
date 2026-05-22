# <u>33. Search in Rotated Sorted Array</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/search-in-rotated-sorted-array/

---

## 🧠 Intuition:
* 🔹 Even after rotation, at least one half of the array is always sorted.
* 🔹 Use Binary Search to find the middle element efficiently.
* 🔹 If `nums[mid]` equals target, return the index immediately.
* 🔹 Check whether the `left half (low → mid)` is sorted.
* 🔹 If left half is sorted, verify whether the target lies inside this range.
* 🔹 If target exists in the sorted left half, move `high = mid - 1`.
* 🔹 Otherwise, discard the left half and search in the right half.
* 🔹 If left half is not sorted, then the right half must be sorted.
* 🔹 Check whether the target lies inside the sorted right half.
* 🔹 If target exists there, move `low = mid + 1`.
* 🔹 Otherwise, discard the right half and continue searching in the left half.
* 🔹 Repeat until target is found or search space becomes empty.


---

## ⏱ Time Complexity

**O(log n)**

* Binary Search halves the search space in every step
    
---

## 📦 Space Complexity

**O(1)**

* Only constant extra variables are used

---

## 💻 Java Code

```java
class Solution {
    public int search(int[] nums, int target) {
        int low = 0, high = nums.length - 1;

        while(low <= high){
            int mid = (low + high)/2;

            if(nums[mid] == target){
                return mid;
            }

            // if left part is sorted
            if(nums[low] <= nums[mid]){
                if(nums[low] <= target && target <= nums[mid]){
                    // element exist
                    high = mid - 1;
                } else{
                    // element does not exist
                    low = mid + 1;
                }
            } else{ // if right part is sorted
                if(nums[mid] <= target && target <= nums[high]){
                    low = mid + 1;
                } else{
                    // element does not exist
                    high = mid - 1;
                }
            }
        }
        return -1;
    }
}
```

---