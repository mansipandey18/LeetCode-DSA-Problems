# <u>300. Longest Increasing Subsequence</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/longest-increasing-subsequence/

---

## 🧠 Intuition:
* 🔹 Use **Dynamic Programming (DP)** where `dp[i]` represents the length of the **longest increasing subsequence ending at index** `i`.

* 🔹 Initially, every element forms an increasing subsequence of length `1`, so initialize all `dp[i] = 1`.

* 🔹 For each element `nums[i]`, check all previous elements `nums[j]` `(j < i)`.

* 🔹 If `nums[j] < nums[i]`, then `nums[i]` can extend the increasing subsequence ending at `j`.

* 🔹 Update:
    - `dp[i] = max(dp[i], dp[j] + 1)`

* 🔹 Keep track of the maximum value in the `dp` array while processing all indices.

* 🔹 After filling the DP array, the maximum value represents the **length of the Longest Increasing Subsequence (LIS)**.

---

## ⏱ Time Complexity
**O(n²)**

* For each element, all previous elements are checked.
    
---

## 📦 Space Complexity

**O(n)**

* A DP array of size `n` is used to store the LIS length ending at each index.

---

## 💻 Java Code

```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        int n = nums.length;
      
        int[] dp = new int[n];
      
        Arrays.fill(dp, 1);
      
        int maxLength = 1;
      
        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[j] < nums[i]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
            maxLength = Math.max(maxLength, dp[i]);
        }
      
        return maxLength;
    }
}
```

---