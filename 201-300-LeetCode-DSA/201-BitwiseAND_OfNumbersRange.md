# <u>201. Bitwise AND of Numbers Range</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/bitwise-and-of-numbers-range/

---

## 🧠 Intuition:
* 🔹 The bitwise **AND** of all numbers in a range keeps only the bits that remain `1` in every number.

* 🔹 Any bit that changes from `0` to `1` (or vice versa) anywhere in the range will become `0` in the final AND.

* 🔹 Instead of checking every number, repeatedly remove the **rightmost set bit** from `right` using the trick `right &= (right - 1)`.

* 🔹 Each operation clears one `1` bit from `right`, eliminating bits that cannot stay `1` throughout the entire range.

* 🔹 Continue until `right` becomes less than or equal to `left`.

* 🔹 At that point, the remaining bits in `right` are exactly the common prefix shared by all numbers in the range.

* 🔹 Return `right` as the final bitwise AND of the range.

---

## ⏱ Time Complexity

**O(32)** `or` **O(number of set bits in `right`))**

* since at most 32 bits are cleared for a 32-bit integer.
    
---

## 📦 Space Complexity

**O(1)**

* No extra data structures are used.

---

## 💻 Java Code

```java
class Solution {
    public int rangeBitwiseAnd(int left, int right) {
        
        while (left < right) {
            right &= (right - 1);
        }
      
        return right;
    }
}
```

---