# <u>3761. Minimum Absolute Distance Between Mirror Pairs</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/minimum-absolute-distance-between-mirror-pairs/

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

**O(n)**

* Traverse array once + reverse operation (constant digits)

---

## 📦 Space Complexity

**O(n)**

* HashMap to store indices

---

## 💻 Java Code

```java
class Solution {
    public int minMirrorPairDistance(int[] nums) {
        int n = nums.length;
        Map<Integer, Integer> pos = new HashMap<>(n);
        int ans = n + 1;
        for (int i = 0; i < n; ++i) {
            if (pos.containsKey(nums[i])) {
                ans = Math.min(ans, i - pos.get(nums[i]));
            }
            pos.put(reverse(nums[i]), i);
        }
        return ans > n ? -1 : ans;
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