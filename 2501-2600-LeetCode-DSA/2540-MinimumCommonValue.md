# <u>2540. Minimum Common Value</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/minimum-common-value/

---

## 🧠 Intuition:
* 🔹 Both arrays are already sorted in non-decreasing order.

* 🔹 Use the Two Pointer technique to efficiently find the smallest common element.

* 🔹 Start:
    - `pointer1` at the beginning of `nums1`
    - `pointer2` at the beginning of `nums2`

* 🔹 Compare elements at both pointers:
    - If they are equal → this is the minimum common value, return it immediately.
    - If `nums1[pointer1] < nums2[pointer2]`:
        * Move `pointer1` forward because smaller values cannot match later larger values.
    - Otherwise:
        * Move `pointer2` forward.

* 🔹 Continue until one array is completely traversed.

* 🔹 If no common element is found, return `-1`.

* 🔹 Since arrays are sorted, the first common value encountered is guaranteed to be the minimum common value.

---

## ⏱ Time Complexity

**O(n + m)**

* Each pointer moves at most once through its array.

---

## 📦 Space Complexity

**O(1)**

* Only constant extra space is used.

---

## 💻 Java Code

```java
class Solution {
    public int getCommon(int[] nums1, int[] nums2) {
        int length1 = nums1.length;
        int length2 = nums2.length;

        // Initialize two pointers for traversing both arrays
        int pointer1 = 0;
        int pointer2 = 0;

        // Traverse both arrays simultaneously until one is exhausted
        while (pointer1 < length1 && pointer2 < length2) {
            // If elements are equal, we found the minimum common element
            if (nums1[pointer1] == nums2[pointer2]) {
                return nums1[pointer1];
            }

            // Move the pointer pointing to the smaller element
            if (nums1[pointer1] < nums2[pointer2]) {
                pointer1++;
            } else {
                pointer2++;
            }
        }

        // No common element found
        return -1;
    }
}
```

---