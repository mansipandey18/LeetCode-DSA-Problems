# <u>3876. Construct Uniform Parity Array II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/construct-uniform-parity-array-ii/

---

## 🧠 Intuition:
* 🔹 Traverse the array once and keep track of:
    - The **smallest even number (`minEven`)** and count of even numbers.
    - The **smallest odd number (`minOdd`)** and count of odd numbers.

* 🔹 If the array contains only **even** or only **odd** numbers, it is already uniform, so return `true`.

* 🔹 If both parities exist, compare the smallest values:
    - If `minEven > minOdd`, the required uniform parity array can be constructed, so return `true`.
    - Otherwise, return `false`.

* 🔹 Thus, the decision is based on the **minimum even and minimum odd elements**.

---

## ⏱ Time Complexity

**O(n)**

* One traversal of `nums1` → `O(n)`
    
---

## 📦 Space Complexity

**O(1)**

* Only a few variables are used.

---

## 💻 Java Code

```java
class Solution {
    public boolean uniformArray(int[] nums1) {
        int minOdd = Integer.MAX_VALUE;
        int minEven = Integer.MAX_VALUE;
        int oddCount = 0;
        int evenCount = 0;

        for (int num : nums1) {
            if (num % 2 == 0) {
                evenCount++;
                if (num < minEven) {
                    minEven = num;
                }
            } else {
                oddCount++;
                if (num < minOdd) {
                    minOdd = num;
                }
            }
        }

        if (evenCount == 0 || oddCount == 0) {
            return true;
        }

        if (minEven > minOdd) {
            return true;
        }

        return false;
    }
}
```

---