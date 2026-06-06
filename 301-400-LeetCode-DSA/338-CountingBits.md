# <u>338. Counting Bits</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/counting-bits/description/

---

## 🧠 Intuition:
* 🔹 We need to count the number of **1s in binary representation** for every number from `0` to `n`.

* 🔹 Instead of manually converting each number to binary, we use Java’s built-in method `Integer.bitCount(i)` which efficiently counts set bits.

* 🔹 We create a result array of size `n + 1` to store answers for all numbers.

* 🔹 We iterate from `0` to `n` and compute bit count for each number individually.

* 🔹 Each index `i` directly stores the number of set bits in `i`.

* 🔹 This is a straightforward **brute-force optimized using built-in bit manipulation function** approach.

---

## ⏱ Time Complexity

**O(n)**

* Loop runs from `0` to `n` → `O(n)`

* `Integer.bitCount(i)` runs in `O(1)` (optimized hardware/bitwise operation)

---

## 📦 Space Complexity

**O(n)**

* Output array of size `n + 1` → `O(n)`
* No extra auxiliary space used → `O(1)` additional space

---

## 💻 Java Code

```java
class Solution {
    public int[] countBits(int n) {
        int[] result = new int[n + 1];
      
        for (int i = 0; i <= n; i++) {
            result[i] = Integer.bitCount(i);
        }
      
        return result;
    }
}
```

---