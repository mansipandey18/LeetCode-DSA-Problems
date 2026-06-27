# <u>35. Search Insert Position</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/search-insert-position/

---

## 🧠 Intuition:
* 🔹 We need to find the position where `target` already exists or should be inserted while keeping the array sorted.

* 🔹 Since the array is sorted, **Binary Search** is the most efficient approach.

* 🔹 Keep track of the smallest index where `nums[mid] >= target` using the variable `ans`.

* 🔹 If `nums[mid] >= target`, this index can be a valid answer, so store it and continue searching on the **left half** to find an even smaller valid index.

* 🔹 If `nums[mid] < target`, the target must be on the **right half**, so move `low` forward.

* 🔹 If the target is larger than all elements, `ans` remains `nums.length`, which is the correct insertion position.

* 🔹 Finally, return `ans` as the index where the target is found or should be inserted.


---

## ⏱ Time Complexity

**O(log n)**

* Binary Search halves the search space in every teration.
    
---

## 📦 Space Complexity

**O(1)**

* Only a few variables are used; no extra space is required.

---

## 💻 Java Code

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
    int low = 0, high = nums.length-1, ans = nums.length;
        
        while(low <= high){
            int mid = (low + high)/2;

            if(nums[mid] >= target){
                ans = mid;
                high = mid - 1;
            } else{
                low = mid + 1;
            }
        }
        return ans;    
    }
}
```

---