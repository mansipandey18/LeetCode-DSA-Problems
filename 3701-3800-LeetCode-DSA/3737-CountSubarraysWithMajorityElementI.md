# <u>3737. Count Subarrays With Majority Element I</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/count-subarrays-with-majority-element-i/

---

## 🧠 Intuition:
* 🔹 We need to count all subarrays where `target` appears more times than all other elements combined.

* 🔹 For each subarray, maintain a balance value:
    - `+1` if the current element equals `target`
    - `-1` otherwise

* 🔹 If the final balance of a subarray is **greater than 0**, it means the count of `target` is greater than the count of non-target elements.

* 🔹 Start every subarray from index `i` and extend it one element at a time toward the right.

* 🔹 Update the balance as the subarray grows.

* 🔹 Whenever the balance becomes positive, increment the answer because the current subarray has `target` as the majority element.

* 🔹 By checking all possible starting and ending positions, we count every valid subarray.
---

## ⏱ Time Complexity

**O(n^2)**

* Two nested loops examine every possible subarray.
    
---

## 📦 Space Complexity

**O(1)**

* Only a few variables (`balance`, `totalSubarrays`) are used.

---

## 💻 Java Code

```java
class Solution {
    public int countMajoritySubarrays(int[] nums, int target) {
        int n = nums.length;
        int totalSubarrays = 0;
        
        // Loop through every possible starting position of a subarray
        for (int i = 0; i < n; i++) {
            int balance = 0;
            
            // Expand the subarray to the right
            for (int j = i; j < n; j++) {
                // +1 if it matches target, -1 otherwise
                if (nums[j] == target) {
                    balance++;
                } else {
                    balance--;
                }
                
                // If balance is strictly positive, target is the majority element
                if (balance > 0) {
                    totalSubarrays++;
                }
            }
        }
        
        return totalSubarrays;
    }
}
```

---