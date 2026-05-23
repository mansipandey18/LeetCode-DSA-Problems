# <u>1752. Check if Array Is Sorted and Rotated</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/check-if-array-is-sorted-and-rotated/

---

## 🧠 Intuition:
* 🔹 A sorted and rotated array can have at most one `“drop point”`.

* 🔹 A drop point occurs when `nums[i] > nums[i + 1]`.

* 🔹 Traverse the array and compare every element with its next element.

* 🔹 Use `modulo (%)` so the last element is compared with the first element as well.

* 🔹 If `nums[i] > nums[(i + 1) % n]`, it means rotation break point is found.

* 🔹 Count how many such break points exist using the variable rotates.

* 🔹 If more than one break point exists, the array cannot be sorted and rotated.

* 🔹 If the count is `0` or `1`, the array satisfies the condition and return `true`.

---

## ⏱ Time Complexity

**O(n)**

* Traverse the array once

---

## 📦 Space Complexity

**O(1)**

* Only constant extra space is used

---

## 💻 Java Code

```java
class Solution {
    public boolean check(int[] nums) {
        int rotates = 0;
        for(int i = 0; i < nums.length; i++){
            if (nums[i] > nums[(i + 1) % nums.length] && ++rotates > 1)
                return false;
        } 
        return true;
    }
}
```

---