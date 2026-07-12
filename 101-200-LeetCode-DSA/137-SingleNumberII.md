# <u>137. Single Number II</u>

----

## 🔗 Problem Link

https://leetcode.com/problems/single-number-ii/

---

## 🧠 Intuition:
* 🔹 The key idea is to count the occurrence of every bit without using extra memory.

* 🔹 Every number except one appears exactly 3 times, so bits belonging to those numbers should be removed after being counted three times.

* 🔹 Use two variables, bit1 and bit2, to represent a 2-bit state machine for every bit position:
    - `00` → bit appeared **0 times**
    - `01` → bit appeared **1 time**
    - `10` → bit appeared **2 times**
    - After the **3rd occurrence**, it automatically returns to `00`.

* 🔹 For each number, update `bit1` and `bit2` using bitwise operations so every bit follows this cycle independently.

* 🔹 Bits from numbers appearing three times are cleared automatically.

* 🔹 The bits of the unique number remain stored in `bit2` after processing all elements.

* 🔹 Return `bit2` as the answer since it represents the number that appears only once.

---

## ⏱ Time Complexity

**O(n)**

* Traverse the array once, performing constant-time bitwise operations for each element.
---

## 📦 Space Complexity

**O(1)**
  
* Only two integer variables (`bit1` and `bit2`) are used regardless of input size.

---

## 💻 Java Code

```java
class Solution {
    public int singleNumber(int[] nums) {
        int bit1 = 0, bit2 = 0;  
      
        for (int num : nums) {
            int newBit1 = (~bit1 & bit2 & num) | (bit1 & ~bit2 & ~num);
            int newBit2 = ~bit1 & (bit2 ^ num);
          
            bit1 = newBit1;
            bit2 = newBit2;
        }
      
        return bit2;
    }
}
```

---