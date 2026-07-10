# <u>191. Number of 1 Bits</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/number-of-1-bits/

---

## 🧠 Intuition:
* 🔹 Instead of checking every bit one by one, use a bit manipulation trick to remove set bits efficiently.

* 🔹 The expression `n & (n - 1)` always clears the **rightmost set (1) bit** in the binary representation of `n`.

* 🔹 Every time this operation is performed, exactly one `1` bit disappears.

* 🔹 Keep repeating this operation until `n` becomes `0`.

* 🔹 Count how many times the operation is performed.

* 🔹 The final count is the total number of `1` bits (Hamming Weight) in the integer.


---

## ⏱ Time Complexity

**O(k)**

* Where:
    - `k` = number of set bits
    
---

## 📦 Space Complexity

**O(1)**

* Only a few integer variables are used.

---

## 💻 Java Code

```java
class Solution {
    public int hammingWeight(int n) {
        int count = 0;
      
        while (n != 0) {
            n &= n - 1;          
            ++count;
        }
      
        return count;
    }
}
```

---