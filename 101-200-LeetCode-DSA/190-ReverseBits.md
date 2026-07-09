# <u>190. Reverse Bits</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/reverse-bits/

---

## 🧠 Intuition:
* 🔹 We need to reverse the positions of all **32 bits** of the integer.

* 🔹 Traverse every bit position **i** from **0 to 31**.

* 🔹 Check whether the **i-th bit** in **n** is set using **(n >> i) & 1**.

* 🔹 If the bit is **1**, place it at the **mirrored position 31 - i** in the answer.

* 🔹 Use **ans |= 1 << (31 - i)** to set that reversed bit.

* 🔹 Continue this process for all 32 positions.

* 🔹 After the loop, **ans** contains the bit-reversed value of **n**.


---

## ⏱ Time Complexity

**O(1)**

* The loop always runs exactly **32 times**.
    
---

## 📦 Space Complexity

**O(1)**

* Only a few integer variables are used.

---

## 💻 Java Code

```java
class Solution {
    public int reverseBits(int n) {
        int ans = 0;

        for (int i = 0; i < 32; ++i){
            if ((n >> i & 1) == 1){
                ans |= 1 << 31 - i;
            }
        }
        return ans;
    }
}
```

---