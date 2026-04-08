# <u>3653. XOR After Range Multiplication Queries I</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/xor-after-range-multiplication-queries-i/

---

## 🧠 Intuition:
* 🔹 We are given an array `nums` and multiple queries.

* 🔹 Each query contains four values: `[l, r, k, v]`.

* 🔹 For every query:
    - Start from index `l`.
    - Move till index `r`.
    - Jump with step size `k` (`l, l+k, l+2k, ...`).
    - Multiply each visited element by `v`.

* 🔹 Since multiplication can become large, apply modulo `10^9 + 7` after every update to keep numbers within limits.

* 🔹 Process queries **one by one**, directly updating the array (brute-force simulation).

* 🔹 After all queries are applied:
    - Compute XOR of all elements in the updated array.

* 🔹 XOR accumulates the final result efficiently because:
    - `a ^ b` combines values bitwise.
    - XOR cancels identical bits and keeps differences.

* 🔹 Return the final XOR value as the answer.

---

## ⏱ Time Complexity

**O(q × n)**

* Where : 
    - `n` = size of `nums`
    - `q` = number of queries

* **Query Processing**

    - For each query:
        * We iterate from `l` to `r` with step `k`.
        * Worst case: `k = 1` → iterate entire range.

    - So per query cost: **O(n)**
    
    - Total for all queries: **O(q × n)**

* **XOR Calculation**
    - One pass over array → **O(n)**

---

## 📦 Space Complexity

**O(1)**

* No extra data structures used.
* Updates happen in-place on `nums`.

---

## 💻 Java Code

```java
class Solution {
    public int xorAfterQueries(int[] nums, int[][] queries) {
        final int mod = (int) 1e9 + 7;
        for (var q : queries) {
            int l = q[0], r = q[1], k = q[2], v = q[3];
            for (int idx = l; idx <= r; idx += k) {
                nums[idx] = (int) (1L * nums[idx] * v % mod);
            }
        }
        int ans = 0;
        for (int x : nums) {
            ans ^= x;
        }
        return ans;
    }
}
```

---