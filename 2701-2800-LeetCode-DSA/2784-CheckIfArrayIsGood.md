# <u>2784. Check if Array is Good</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/check-if-array-is-good/

---

## 🧠 Intuition:
* 🔹 A “good” array of size `n + 1` should contain numbers from `1` to `n`.

* 🔹 Every number from `1` to `n-1` must appear exactly once.

* 🔹 The number `n` must appear exactly twice.

* 🔹 Use a frequency array to count how many times each number appears.

* 🔹 First, check whether `n` occurs exactly `2` times.

* 🔹 Then verify that every number from `1` to `n-1` appears exactly once.

* 🔹 If any condition fails, return `false`; otherwise return `true`.

---

## ⏱ Time Complexity

**O(n)**

* Traversing the array and checking frequencies.

---

## 📦 Space Complexity

**O(1)**

* Frequency array size is fixed (`201`), independent of input size.

---

## 💻 Java Code

```java
class Solution {
    public boolean isGood(int[] nums) {
        int n = nums.length - 1;
      
        int[] frequency = new int[201];
      
        for (int number : nums) {
            frequency[number]++;
        }
      
        if (frequency[n] != 2) {
            return false;
        }
      
        for (int i = 1; i < n; i++) {
            if (frequency[i] != 1) {
                return false;
            }
        }
      
        return true;
    }
}
```

---