# <u>1674. Minimum Moves to Make Array Complementary</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/minimum-moves-to-make-array-complementary/

---

## 🧠 Intuition:
* 🔹 We process the array in pairs: nums[i] and nums[n - i - 1], since complementary arrays depend on mirrored pairs.

* 🔹 For every pair, we analyze how many moves are needed for each possible target sum from 2 to 2 * limit.

* 🔹 Instead of checking every target sum separately, we use a difference array to efficiently mark ranges of move counts.

* 🔹 Initially, every sum requires 2 moves for the current pair.

* 🔹 If the target sum falls within a certain range, only 1 move is needed.

* 🔹 If the target sum equals x + y (where x = min pair value and y = max pair value), then 0 moves are needed.

* 🔹 Using range updates on the difference array allows us to apply these transitions in O(1) per pair.

* 🔹 After processing all pairs, we compute prefix sums on the difference array to get the total moves required for every possible target sum.

* 🔹 The minimum among all computed move counts is the final answer.

* 🔹 This approach avoids brute force checking of every pair for every sum and optimizes the solution using prefix sum + sweep line technique.
---

## ⏱ Time Complexity

**O(n + limit)**

* `O(n)` for processing all pairs
* `O(limit)` for prefix sum traversal
    
---

## 📦 Space Complexity

**O(limit)**

* Difference array of size `2 * limit + 2` is used

---

## 💻 Java Code

```java
class Solution {
    public int minMoves(int[] nums, int limit) {
        int[] d = new int[2 * limit + 2];
        int n = nums.length;
        for (int i = 0; i < n / 2; ++i) {
            int x = Math.min(nums[i], nums[n - i - 1]);
            int y = Math.max(nums[i], nums[n - i - 1]);
            d[2] += 2;
            d[x + 1] -= 2;
            d[x + 1] += 1;
            d[x + y] -= 1;
            d[x + y + 1] += 1;
            d[y + limit + 1] -= 1;
            d[y + limit + 1] += 2;
        }
        int ans = n;
        for (int i = 2, s = 0; i < d.length; ++i) {
            s += d[i];
            ans = Math.min(ans, s);
        }
        return ans;
    }
}
```

---