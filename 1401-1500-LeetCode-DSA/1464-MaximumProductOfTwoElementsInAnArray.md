# <u>1464. Maximum Product of Two Elements in an Array</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/reorder-routes-to-make-all-paths-lead-to-the-city-zero/

---

## 🧠 Intuition:
* 🔹 The maximum product depends only on the two largest elements in the array.

* 🔹 Traverse the array once while maintaining:
    - `max1` → the largest element found so far.
    - `max2` → the second largest element found so far.

* 🔹 For each number:
    - If it is greater than `max1`, update:
        * `max2 = max1`
        * `max1 = num`
    - Otherwise, if it is greater than `max2`, update:
        * `max2 = num`

* 🔹 After finding the two largest numbers, compute the required product:
    - `(max1 - 1) * (max2 - 1)`

* 🔹 This avoids sorting the array and finds the answer in a single traversal.

---

## ⏱ Time Complexity

**O(n)**

* The array is traversed only once.
    
---

## 📦 Space Complexity

**O(1)**

* Only two variables are used to store the largest and second-largest elements.

---


## 💻 Java Code

```java
class Solution {
    public int maxProduct(int[] nums) {
        int max1 = 0;
        int max2 = 0;
        
        for (int num : nums) {
            if (num > max1) {
                max2 = max1; // The old largest becomes the second largest
                max1 = num;  // Update the largest
            } else if (num > max2) {
                max2 = num;  // Update the second largest
            }
        }
        
        return (max1 - 1) * (max2 - 1);
    }
}
```

---