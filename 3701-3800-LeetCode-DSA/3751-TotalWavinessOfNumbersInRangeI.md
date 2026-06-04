# <u>3751. Total Waviness of Numbers in Range I</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/total-waviness-of-numbers-in-range-i/

---

## 🧠 Intuition:
* 🔹 The problem asks to compute **total “waviness”** for all numbers in the range `[num1, num2]`.

* 🔹 For each number `x`, we calculate its individual waviness using function `f(x)`.

* 🔹 In f(x):
    - First, extract all digits of the number and store them in reverse order.
    - If the number has fewer than 3 digits, it cannot form a peak or valley → waviness is `0`.

* 🔹 For every middle digit (excluding first and last):
    - Check if it is a **peak** (greater than both neighbors) or a **valley** (smaller than both neighbors).

* 🔹 Count all such positions to get waviness of that number.

* 🔹 Sum the waviness of every number in the given range to get the final answer.

* 🔹 Essentially, we are doing a **brute-force per-number digit analysis** over the range.

---

## ⏱ Time Complexity

**O(n * d)**

* Where:
    - `n` = num2 - num1 + 1
    - `d` = number of digits (~log10(num2))

* Each number is processed in `O(D)`

---

## 📦 Space Complexity

**O(1)**

* `O(D)` for storing digits of a single number (`nums[20]` is constant bounded)

* So effectively `O(1)` auxiliary space (fixed size array).

---

## 💻 Java Code

```java
class Solution {
    public int totalWaviness(int num1, int num2) {
        int ans = 0;
        for (int x = num1; x <= num2; x++) {
            ans += f(x);
        }
        return ans;
    }

    private int f(int x) {
        int[] nums = new int[20];
        int m = 0;
        while (x > 0) {
            nums[m++] = x % 10;
            x /= 10;
        }
        if (m < 3) {
            return 0;
        }
        int s = 0;
        for (int i = 1; i < m - 1; i++) {
            if ((nums[i] > nums[i - 1] && nums[i] > nums[i + 1])
                || (nums[i] < nums[i - 1] && nums[i] < nums[i + 1])) {
                s++;
            }
        }
        return s;
    }
}
```

---