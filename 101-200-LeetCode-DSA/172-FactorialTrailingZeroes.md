# <u>172. Factorial Trailing Zeroes</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/factorial-trailing-zeroes/

---

## 🧠 Intuition:
* 🔹 A trailing zero is formed by the pair **2 × 5 in** the prime factorization.

* 🔹 In `n!`, there are always **more factors of 2 than factors of 5**, so the number of trailing zeros depends only on the count of **5s**.

* 🔹 Count how many numbers from `1` to `n` contribute at least one factor of `5` by adding `n / 5`.

* 🔹 Some numbers (like 25, 125, 625, ...) contribute multiple factors of `5`, so continue dividing `n` by `5` and keep adding the quotient.

* 🔹 Repeat until `n` becomes `0`.

* 🔹 The accumulated count gives the total number of trailing zeros in `n!`.

---

## ⏱ Time Complexity

**O(log₅ n)**

* The value of `n` is divided by `5` in each iteration.
    
---

## 📦 Space Complexity

**O(1)**

* Only a few integer variables are used.

---

## 💻 Java Code

```java
class Solution {
    public int trailingZeroes(int n) {
        int trailingZeroCount = 0;

        while (n > 0) {
            n /= 5;  
            trailingZeroCount += n;  
        }
      
        return trailingZeroCount;
    }
}
```

---