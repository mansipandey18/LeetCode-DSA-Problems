# <u>1563. Stone Game V</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/stone-game-v/

---

## 🧠 Intuition:
* 🔹 Use **Dynamic Programming with Memoization** because the same subarrays can be evaluated multiple times.

* 🔹 `dfs(left, right)` represents the **maximum score Alice can obtain** from the subarray `stoneValue[left...right]`.

* 🔹 For every possible `splitPoint`, divide the current range into:
    - **Left partition:** `left...splitPoint`
    - **Right partition:** `splitPoint+1...right`

* 🔹 Use a **prefix sum array** to calculate the total of any range quickly.

* 🔹 Maintain `leftSum` and `rightSum` while moving the split point, avoiding repeated sum calculations.

* 🔹 According to the game rule:
    - If `leftSum < rightSum`, Alice must choose the **left partition**.
    - If `leftSum > rightSum`, Alice must choose the **right partition**.
    - If `leftSum == rightSum`, Alice can choose **either partition**, so take the better option.

* 🔹 The score gained from a split is the sum of the selected partition plus the best score obtainable from that smaller subarray.

* 🔹 Store every computed `(left, right)` result in `memo` so it is calculated only once.

* 🔹 The pruning conditions can skip some unnecessary split points when the current `maxScore` is already large enough compared with the possible contribution of the current partition.

* 🔹 Finally, `dfs(0, n-1)` gives Alice's maximum possible score for the entire array.


---

## ⏱ Time Complexity

**O(n³)**

* There are **O(n²)** possible subarrays/states.
* For each state, the code may try up to **O(n)** split points.
* Therefore, the **worst-case time complexity is O(n³)**.
* Prefix sums make each range-sum calculation **O(1)**.
    
---

## 📦 Space Complexity

**O(n²)**

* `memo[n][n]` → **O(n²)**
* `prefixSum` → **O(n)**
* Recursion stack → **O(n)** in the worst case.

---

## 💻 Java Code

```java
class Solution {
    private int n;                    // Total number of stones
    private int[] prefixSum;          // Prefix sum array for quick range sum calculation
    private int[] stoneValues;        // Original stone values array
    private Integer[][] memo; 

    public int stoneGameV(int[] stoneValue) {
        n = stoneValue.length;
        prefixSum = new int[n + 1];
        stoneValues = stoneValue;
        memo = new Integer[n][n];
      
        // Build prefix sum array for O(1) range sum queries
        // prefixSum[i] represents sum of elements from index 0 to i-1
        for (int i = 1; i <= n; i++) {
            prefixSum[i] = prefixSum[i - 1] + stoneValues[i - 1];
        }
      
        // Start the recursive solution with memoization
        return dfs(0, n - 1);
    }
  
    private int dfs(int left, int right) {
        // Base case: if range is invalid or contains only one element
        if (left >= right) {
            return 0;
        }
      
        // Check if result is already computed
        if (memo[left][right] != null) {
            return memo[left][right];
        }
      
        int maxScore = 0;
        int leftSum = 0;  // Sum of left partition
        int rightSum = prefixSum[right + 1] - prefixSum[left];  // Sum of right partition
      
        // Try all possible split points
        for (int splitPoint = left; splitPoint < right; splitPoint++) {
            // Update partition sums
            leftSum += stoneValues[splitPoint];
            rightSum -= stoneValues[splitPoint];
          
            if (leftSum < rightSum) {
                // Left partition has smaller sum, Alice chooses left
                // Pruning: if current answer is already greater than maximum possible score
                if (maxScore > leftSum * 2) {
                    continue;
                }
                maxScore = Math.max(maxScore, leftSum + dfs(left, splitPoint));
            } else if (leftSum > rightSum) {
                // Right partition has smaller sum, Alice chooses right
                // Pruning: if current answer is already greater than maximum possible score
                if (maxScore > rightSum * 2) {
                    break;
                }
                maxScore = Math.max(maxScore, rightSum + dfs(splitPoint + 1, right));
            } else {
                // Both partitions have equal sum, Alice can choose either
                maxScore = Math.max(maxScore, 
                    Math.max(leftSum + dfs(left, splitPoint), 
                            rightSum + dfs(splitPoint + 1, right)));
            }
        }
      
        // Store result in memo table and return
        memo[left][right] = maxScore;
        return maxScore;
    }
}
```

---