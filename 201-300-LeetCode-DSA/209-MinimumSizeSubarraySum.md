# <u>209. Minimum Size Subarray Sum</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/minimum-size-subarray-sum/

---

## 🧠 Intuition:
* 🔹 We need to find the **smallest length subarray** whose sum is **greater than or equal to target**.

* 🔹 Instead of checking all subarrays (which is slow), we use a **sliding window technique**.

* 🔹 Maintain two pointers:
    - i → start of window
    - j → end of window

* 🔹 Expand the window by moving `j` forward and keep adding elements to `sum`.

* 🔹 Once the current window sum becomes ≥ target, we know this window is valid.

* 🔹 Now try to shrink the window from the left (`i++`) to make it as small as possible while keeping the sum ≥ target.

* 🔹 Update the minimum size every time we find a valid window.

* 🔹 Continue expanding and shrinking dynamically so every element is processed efficiently only once.

* 🔹 If no valid subarray is found, return `0`.

---

## ⏱ Time Complexity

**O(n)**

* Each element is added to the window once (`j` moves forward).
* Each element is removed from the window once (`i` moves forward).

---

## 📦 Space Complexity

**O(1)**

* Only a few variables (`sum`, `i`, `j`, `size`) are used.
* No extra data structures.

---

## 💻 Java Code

```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int size = Integer.MAX_VALUE, sum = 0;

        int i = 0, j = 0;

        while(j < nums.length){
            sum = sum + nums[j];

            while(sum >= target){
                size = Math.min(size, j - i + 1);
                sum = sum - nums[i];

                i++;
            }
            j++;
        }

        return size == Integer.MAX_VALUE ? 0 : size;
    }
}
```

---