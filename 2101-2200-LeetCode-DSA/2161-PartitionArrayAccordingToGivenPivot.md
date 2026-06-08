# <u>2161. Partition Array According to Given Pivot</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/partition-array-according-to-given-pivot/

---

## 🧠 Intuition:
* 🔹 The goal is to rearrange the array based on a given pivot while maintaining relative order within each group.

* 🔹 We divide elements into three categories:
    - Elements less than pivot
    - Elements equal to pivot
    - Elements greater than pivot

* 🔹 Instead of sorting, we perform three linear passes over the array.

* 🔹 In the first pass, we collect all elements smaller than pivot into the result array.

* 🔹 In the second pass, we collect all elements equal to pivot.

* 🔹 In the third pass, we collect all elements greater than pivot.

* 🔹 We maintain an index pointer to fill the result array sequentially.

* 🔹 This ensures stable ordering within each group and satisfies partition conditions.

---

## ⏱ Time Complexity

**O(n)**

* Three separate traversals of the array → `O(n)`
  
---

## 📦 Space Complexity

**O(n)**

* Extra result array of size `n` → `O(n)`
* No additional auxiliary structures used → overall space is `O(n)`

---

## 💻 Java Code

```java
class Solution {
    public int[] pivotArray(int[] nums, int pivot) {
        int n = nums.length;
      
        // Create a result array of the same size
        int[] result = new int[n];
      
        // Index pointer for placing elements in the result array
        int index = 0;
      
        // First pass: Place all elements less than pivot
        for (int num : nums) {
            if (num < pivot) {
                result[index++] = num;
            }
        }
      
        // Second pass: Place all elements equal to pivot
        for (int num : nums) {
            if (num == pivot) {
                result[index++] = num;
            }
        }
      
        // Third pass: Place all elements greater than pivot
        for (int num : nums) {
            if (num > pivot) {
                result[index++] = num;
            }
        }
      
        return result;
    }
}
```

---