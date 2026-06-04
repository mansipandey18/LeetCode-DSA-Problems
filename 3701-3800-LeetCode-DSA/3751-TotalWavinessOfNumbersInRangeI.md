# <u>3751. Total Waviness of Numbers in Range I</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/total-waviness-of-numbers-in-range-i/

---

## 🧠 Intuition:
* 🔹 We need to find the minimum distance between a number and its reverse (mirror).

* 🔹 Traverse the array and use a HashMap to store values we’ve seen.

* 🔹 But instead of storing the number itself, we store its reverse as key with its index.

* 🔹 Why? Because when we see a number x, we want to quickly check if its reverse already appeared before.

* 🔹 For each element:
    - If current number exists in map → it means we found its mirror earlier
    - Compute distance = currentIndex - previousIndex
    - Update minimum answer

* 🔹 Then store reverse of current number in the map for future matches.

* 🔹 If no such pair exists → return -1.

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