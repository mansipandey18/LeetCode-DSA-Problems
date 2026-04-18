# <u>3783. Mirror Distance of an Integer</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/mirror-distance-of-an-integer/

---

## 🧠 Intuition:
* 🔹 We need to find the **difference between a number and its reverse**.

* 🔹 First, reverse the digits of the number:
    - Take last digit using `% 10`
    - Add it to new number (`y = y * 10 + digit`)
    - Remove last digit using `/ 10`

* 🔹 After reversing, we get the **mirror number**.

* 🔹 Then simply compute **absolute difference** between original number and reversed number.

* 🔹 Return that difference as the answer.

---

## ⏱ Time Complexity

**O(d)**

* Number of digits in `n` = `d`

    
---

## 📦 Space Complexity

**O(1)**

* Only a few variables used

---

## 💻 Java Code

```java
class Solution {
    public int mirrorDistance(int n) {
        return Math.abs(n - reverse(n));
    }

    private int reverse(int x) {
        int y = 0;
        for (; x > 0; x /= 10) {
            y = y * 10 + x % 10;
        }
        return y;
    }
}
```

---