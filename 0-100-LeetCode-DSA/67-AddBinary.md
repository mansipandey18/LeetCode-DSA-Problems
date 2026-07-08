# <u>67. Add Binary</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/add-binary/

---

## 🧠 Intuition:
* 🔹 Start from the **last character** of both binary strings since binary addition is performed from **right to left**.

* 🔹 Maintain a **carry** variable to handle overflow when adding bits.

* 🔹 At each step:
    - Add the current bit from `a` (if available).
    - Add the current bit from `b` (if available).
    - Add the existing **carry**.

* 🔹 The **current binary digit** is `carry % 2`, so append it to the result.

* 🔹 Update the **carry** as `carry / 2` for the next iteration.

* 🔹 Continue until all digits of both strings are processed and no carry remains.

* 🔹 Since digits are added from **least significant to most significant**, reverse the result at the end to obtain the correct binary sum.

---

## ⏱ Time Complexity

**O(max(m, n))**

* Where: 
    - `m` = length of a
    - `n` = length of b

* Traverse both binary strings once
---

## 📦 Space Complexity

**O(max(m, n))**

* The `StringBuilder` stores the resulting binary string.

---

## 💻 Java Code

```java
class Solution {
    public String addBinary(String a, String b) {
        StringBuilder result = new StringBuilder();

        int indexA = a.length() - 1, indexB = b.length() - 1, carry = 0;
        
        while (indexA >= 0 || indexB >= 0 || carry > 0) {
            if (indexA >= 0) {
                carry += a.charAt(indexA) - '0';
                indexA--; // Decrement index for string a
            }
            if (indexB >= 0) {
                carry += b.charAt(indexB) - '0';
                indexB--; // Decrement index for string b
            }
            result.append(carry % 2);
            carry /= 2;
        }
        return result.reverse().toString();
    }
}
```

---