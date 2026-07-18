# <u>1979. Find Greatest Common Divisor of Array</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/find-greatest-common-divisor-of-array/

---

## 🧠 Intuition:
* 🔹 The GCD of the entire array is equal to the **GCD of its smallest and largest elements**.

* 🔹 Traverse the array once to find the **minimum** and **maximum** values.

* 🔹 After finding these two values, apply the **Euclidean Algorithm** to compute their GCD.

* 🔹 The Euclidean Algorithm repeatedly replaces `(a, b)` with `(b, a % b)` until `b` becomes `0`.

* 🔹 When `b` is `0`, the remaining value of `a` is the required GCD.

* 🔹 This approach avoids computing the GCD of every pair and gives the answer efficiently.

---

## ⏱ Time Complexity

**O(n + log(maxElement))**

* `O(n)` to find the minimum and maximum elements
* `O(log(maxElement))` for the Euclidean GCD computation.

---

## 📦 Space Complexity

**O(log(maxElement))**

* Recursive Euclidean Algorithm uses recursion stack proportional to the number of recursive calls. (If implemented iteratively, it would be **O(1)**.)

---

## 💻 Java Code

```java
class Solution {
    public int findGCD(int[] nums) {
        int maxElement = 1;
        int minElement = 1000;
      
        // Iterate through array to find maximum and minimum elements
        for (int num : nums) {
            maxElement = Math.max(maxElement, num);
            minElement = Math.min(minElement, num);
        }
      
        // Calculate and return the GCD of max and min elements
        return gcd(maxElement, minElement);
    }

    
    private int gcd(int a, int b) {
        return b == 0 ? a : gcd(b, a % b);    
    }
}
```

---