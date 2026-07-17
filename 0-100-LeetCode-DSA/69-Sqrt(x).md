# <u>69. Sqrt(x)</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/sqrtx/

---

## 🧠 Intuition:
* 🔹 The square root of `x` lies in the range **1 to x** (except for `0` and `1`, which are handled separately).

* 🔹 Use **Binary Search** to efficiently find the largest integer whose square is less than or equal to `x`.

* 🔹 Compute the middle value `mid` and calculate `mid × mid`.

* 🔹 If `mid²` is greater than `x`, the answer must be on the **left half**, so move `high` to `mid`.

* 🔹 Otherwise, `mid` is a valid candidate, so search the **right half** by moving `low` to `mid + 1` to check for a larger valid square root.

* 🔹 Continue until the search space is exhausted.

* 🔹 Since `low` stops at the first value whose square is greater than `x`, the integer square root is `low - 1`.

* 🔹 Use `long` while computing `mid × mid` to avoid integer overflow.

---

## ⏱ Time Complexity

**O(log n)**

* Binary search halves the search space in every iteration.

---

## 📦 Space Complexity

**O(1)**

* Only a constant amount of extra space is used.

---

## 💻 Java Code

```java
class Solution {
    public int mySqrt(int x) {
        int ans = 0;

        int low = 1, high = x;

        if(x == 0 || x == 1){
            return x;
        }

        while(low < high){
            int mid = low + (high - low) /2;
            long val = (long) mid * mid;
            
            if(val > x){
                high = mid;
            } else{
                low = mid + 1;
            }
        }

        return low -  1;
    }
}
```

---