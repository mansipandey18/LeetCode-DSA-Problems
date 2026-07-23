# <u>3513. Number of Unique XOR Triplets I</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/number-of-unique-xor-triplets-i/

---

## 🧠 Intuition:
* 🔹 Observe the special pattern of XOR values instead of generating all triplets.

* 🔹 If the array size is **1 or 2**, every possible XOR result is already unique, so the answer is simply `n`.

* 🔹 For n ≥ 3, the unique XOR values always cover the complete range from `0` to `2^k - 1`, where `k` is the number of bits required to represent `n`.

* 🔹 Compute the required number of bits using:
    - `bitLength = 32 - Integer.numberOfLeadingZeros(n)`

* 🔹 The total number of distinct XOR values is then:
    - `2^bitLength`, computed as `1 << bitLength`.

* 🔹 This avoids checking all triplets and directly returns the answer using the mathematical property of XOR.

---

## ⏱ Time Complexity

**O(1)**

* Only a few arithmetic and bit operations are performed.

---

## 📦 Space Complexity

**O(1)**

* No extra data structures are used.

---

## 💻 Java Code

```java
class Solution {
    public int uniqueXorTriplets(int[] nums) {
        int n = nums.length;
        
        if (n <= 2) {
            return n;
        }
        
        int bitLength = 32 - Integer.numberOfLeadingZeros(n);
        
        return 1 << bitLength;
    }
}
```

---