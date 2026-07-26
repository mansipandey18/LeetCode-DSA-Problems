# <u>628. Maximum Product of Three Numbers</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-product-of-three-numbers/

---

## 🧠 Intuition:
* 🔹 Sort the array so that the smallest and largest numbers are easily accessible.

* 🔹 Observe that the maximum product can come from **two possible cases**:
    - The **three largest numbers**, since large positive numbers produce a large product.
    - The **largest number and the two smallest numbers**, because two negative numbers multiply to a positive number, which can produce an even larger product.

* 🔹 Compute both products:
    - `nums[n-1] * nums[n-2] * nums[n-3]`
    - `nums[n-1] * nums[0] * nums[1]`

* 🔹 Return the larger of the two products.

* 🔹 This ensures all possible scenarios involving positive and negative numbers are considered.

---

## ⏱ Time Complexity

**O(n log n)**

* Sorting the array dominates the overall time complexity.
 
---

## 📦 Space Complexity

**O(1)**

* No extra space is used apart from a few variables (ignoring the space used by the sorting algorithm implementation).

---

## 💻 Java Code

```java
class Solution {
    public int maximumProduct(int[] nums) {
        Arrays.sort(nums);
      
        int n = nums.length;
      
        int productOfThreeLargest = nums[n - 1] * nums[n - 2] * nums[n - 3];
      
        int productOfLargestAndTwoSmallest = nums[n - 1] * nums[0] * nums[1];
      
        return Math.max(productOfThreeLargest, productOfLargestAndTwoSmallest);
    }
}
```

---