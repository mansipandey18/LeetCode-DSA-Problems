# <u>1318. Minimum Flips to Make a OR b Equal to c</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/minimum-flips-to-make-a-or-b-equal-to-c/

---

## 🧠 Intuition:
* 🔹 We need to make the bitwise equation **(a OR b) == c** true using minimum flips.

* 🔹 We analyze the numbers **bit by bit (0 to 31)** because bitwise operations are independent per bit.

* 🔹 For each bit position, we extract:
    - `bitA` from `a`
    - `bitB` from `b`
    - `bitC` from `c`

* 🔹 We apply rules based on `bitC`:
    - If `bitC == 0`:
        * Both `a` and `b` must be 0 → any `1` must be flipped to `0`
        * So flips needed = `bitA + bitB`
    - If `bitC == 1`:
        * At least one of `a` or `b` must be `1`
        * If both are `0`, we need **1 flip** to make either of them `1`

* 🔹 We accumulate all required flips across all bit positions.

* 🔹 Final answer is total minimum flips required.

---

## ⏱ Time Complexity

**O(1)**

* We check all 32 bits → `O(1)` (constant time).
    
---

## 📦 Space Complexity

**O(1)**

* Only a few integer variables used → `O(1)` space

---

## 💻 Java Code

```java
class Solution {
    public int minFlips(int a, int b, int c) {
        int flipCount = 0;
      
        for (int bitPosition = 0; bitPosition < 32; bitPosition++) {
            int bitA = (a >> bitPosition) & 1;
            int bitB = (b >> bitPosition) & 1;
            int bitC = (c >> bitPosition) & 1;
          
            if (bitC == 0) {
                flipCount += bitA + bitB;
            } else {
                if (bitA == 0 && bitB == 0) {
                    flipCount += 1;
                }
            }
        }
      
        return flipCount;
    }
}
```

---