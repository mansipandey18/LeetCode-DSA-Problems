# <u>198. House Robber</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/house-robber/

---

## 🧠 Intuition:
* 🔹 At every house, there are only two choices:
    - **Rob the current house** and move to `houseIndex + 2` (cannot rob adjacent house).
    - **Skip the current house** and move to `houseIndex + 1`.

* 🔹 Use **DFS + Memoization (Top-Down DP)** to compute the maximum money that can be robbed starting from each index.

* 🔹 Define `calculateMaxRobbery(i)` as the maximum amount that can be robbed from houses `i` to `n-1`.

* 🔹 Recurrence:
    - `robCurrentHouse = houses[i] + calculateMaxRobbery(i + 2)`
    - `skipCurrentHouse = calculateMaxRobbery(i + 1)`
    - Take the maximum of these two choices.

* 🔹 Use a `memo` array to store already computed results and avoid solving the same subproblem multiple times.

* 🔹 Base case: if the index goes beyond the last house, return `0`.

* 🔹 The final answer is the maximum amount obtainable starting from house `0`.


---

## ⏱ Time Complexity

**O(n)**

* Each house index is computed only once due to memoization.
    
---

## 📦 Space Complexity

**O(n)**

* `O(n)` for the memo array and `O(n)` recursion stack in the worst case.

---

## 💻 Java Code

```java
class Solution {
    private Integer[] memo;
    private int[] houses;

    public int rob(int[] nums) {
        this.houses = nums;
        this.memo = new Integer[nums.length];

        return calculateMaxRobbery(0);
    }

    private int calculateMaxRobbery(int houseIndex) {
        if (houseIndex >= houses.length) {
            return 0;
        }
      
        if (memo[houseIndex] == null) {
            int robCurrentHouse = houses[houseIndex] + calculateMaxRobbery(houseIndex + 2);
            int skipCurrentHouse = calculateMaxRobbery(houseIndex + 1);
          
            memo[houseIndex] = Math.max(robCurrentHouse, skipCurrentHouse);
        }
      
        return memo[houseIndex];
    }
}
```

---