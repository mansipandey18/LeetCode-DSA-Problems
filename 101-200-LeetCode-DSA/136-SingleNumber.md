# <u>136. Single Number</u>

----

## 🔗 Problem Link

https://leetcode.com/problems/single-number/

---

## 🧠 Intuition:
* 🔹 The problem asks to find the element that appears only once, while all others appear twice.

* 🔹 We use the property of XOR (^) operation:
    - `a ^ a = 0` (same numbers cancel out)
    - `a ^ 0 = a`
    - XOR is commutative and associative.

* 🔹 We initialize a variable `xor = 0`.

* 🔹 We iterate through the array and keep XOR-ing all elements.

* 🔹 Duplicate elements cancel each other out, leaving only the single unique number.

* 🔹 Finally, the remaining XOR value is the answer.

---

## ⏱ Time Complexity

**O(n)**

* We traverse the array once → `O(n)`

---

## 📦 Space Complexity

**O(1)**
  
* Only one variable (`xor`) is used → `O(1)` extra space

---

## 💻 Java Code

```java
class Solution {
    public int singleNumber(int[] nums) {
        int xor = 0;
        for(int i = 0; i < nums.length; i++){
            xor = xor ^ nums[i];
        }
        return xor;
    }
}
```

---