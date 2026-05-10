# <u>2770. Maximum Number of Jumps to Reach the Last Index</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-number-of-jumps-to-reach-the-last-index/

---

## 🧠 Intuition:
* 🔹 The goal is to find the **maximum number of jumps** needed to reach the last index

* 🔹 From index `i`, we can jump to index `j` only if:
    - `|nums[i] - nums[j]| <= target`

* 🔹 This problem is solved using **DFS + Memoization (Top-Down DP)**

* 🔹 Define `dfs(i)` as:
    - Maximum jumps possible starting from index `i` to reach the last index

* 🔹 Base case:
    - If `i == n - 1`, we are already at the last index, so return `0`

* 🔹 For every index `i`:
    - Try all possible next indices `j > i`
    - If the jump condition is valid, recursively calculate: `1 + dfs(j)`
    - Keep the maximum among all valid choices

* 🔹 Memoization array `memo[]` stores results for already computed indices
    - This avoids recomputing the same subproblems multiple times

* 🔹 If no valid path exists, the result remains negative

* 🔹 Finally:
    - Return `-1` if reaching the last index is impossible
    - Otherwise return the maximum jumps found

---

## ⏱ Time Complexity

**O(n^2)**

* Where:
    - `n` = size of the array

* For each index `i`, we may check all later indices `j`
* Due to memoization, each state is computed only once

---

## 📦 Space Complexity

**O(n)**

* `memo[]` array stores results for `n` indices
* Recursive DFS call stack can go up to depth `n` in the worst case
---

## 💻 Java Code

```java
class Solution {
    private Integer[] memo;
    private int[] nums;
    private int n;
    private int target;

    public int maximumJumps(int[] nums, int target) {
        this.n = nums.length;
        this.target = target;
        this.nums = nums;
        this.memo = new Integer[n];
      
        int result = dfs(0);
      
        return result < 0 ? -1 : result;
    }

    private int dfs(int i) {
        if (i == n - 1) {
            return 0;
        }
      
        if (memo[i] != null) {
            return memo[i];
        }
      
        int maxJumps = -(1 << 30);
      
        for (int j = i + 1; j < n; j++) {
            if (Math.abs(nums[i] - nums[j]) <= target) {
                maxJumps = Math.max(maxJumps, 1 + dfs(j));
            }
        }
      
        memo[i] = maxJumps;
        return maxJumps;
    }
}
```

---