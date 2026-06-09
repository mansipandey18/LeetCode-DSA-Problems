# <u>3689. Maximum Total Subarray Value I</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-total-subarray-value-i/

---

## 🧠 Intuition:
* 🔹 The problem asks for the maximum total value, but this solution simplifies it using a key observation.

* 🔹 It identifies that only the **maximum and minimum element** of the array matter for the final expression.

* 🔹 We iterate through the array once to find:
    - `mx` → maximum element
    - `mn` → minimum element

* 🔹 The value contributed by the subarray operation is assumed to depend on the range (mx - mn).

* 🔹 Since we perform `k` such operations, the total contribution is simply multiplied by `k`.

* 🔹 Final answer is computed as: **k × (max element − min element)**

---

## ⏱ Time Complexity

**O(n)**

* Single traversal of array to find min and max → `O(n)`
    
---

## 📦 Space Complexity

**O(1)**

* Only a few variables used (`mx`, `mn`)

---

## 💻 Java Code

```java
class Solution {
    public long maxTotalValue(int[] nums, int k) {
        int mx = 0, mn = 1 << 30;
        for (int x : nums) {
            mx = Math.max(mx, x);
            mn = Math.min(mn, x);
        }
        return 1L * k * (mx - mn);
    }
}
```

---