# <u>3702. Longest Subsequence With Non-Zero Bitwise XOR</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/longest-subsequence-with-non-zero-bitwise-xor/

---

## 🧠 Intuition:
* 🔹 Calculate the **XOR of all elements** in the array.

* 🔹 If the XOR of the complete array is **non-zero**, the entire array itself is a valid subsequence, so the answer is `n`.

* 🔹 If the total XOR is `0`, we need to remove at least one element to make the XOR non-zero.

* 🔹 If there is at least one **non-zero element**, removing any suitable non-zero element makes the XOR non-zero, so the maximum length becomes `n - 1`.

* 🔹 The only special case is when **all elements** are `0`:
    - XOR of any subsequence will always remain `0`.
    - Therefore, no valid subsequence exists, and the answer is `0`.

* 🔹 Thus, we only need to track the **total XOR and the count of zeroes**.

---

## ⏱ Time Complexity

**O(n)**

* one traversal of the array.
    
---

## 📦 Space Complexity

**O(1)**

* only a few variables are used.

---

## 💻 Java Code

```java
class Solution {
    
    public int longestSubsequence(int[] nums) {

        int xor=0;
        int countZero=0;

        for(int num : nums){
            xor ^=num;
            if(num==0){
                countZero++;
            }
        }

        if(xor != 0) return nums.length;
        else{
            if(countZero==nums.length) return 0;
        }
        return nums.length-1;
    }
}
```

---