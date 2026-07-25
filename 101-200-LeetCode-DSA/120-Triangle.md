# <u>120. Triangle</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/triangle/

---

## 🧠 Intuition:
* 🔹 Use **Bottom-Up Dynamic Programming** to compute the minimum path sum from the bottom of the triangle to the top.

* 🔹 Maintain a **1D DP array**, where `dp[index]` stores the minimum path sum starting from the current position in the row below.

* 🔹 Initialize the DP array with zeros. It will be updated while moving upward through the triangle.

* 🔹 Start processing from the **last row** and move towards the **first row**.

* 🔹 For each element in the current row:
    - Choose the smaller of the two possible paths from the row below:
        * `dp[index]` (down)
        * `dp[index + 1]` (down-right)
    - Add the current triangle value:
        * `dp[index] = min(dp[index], dp[index + 1]) + currentValue`

* 🔹 After processing a row, the DP array represents the minimum path sums for that row.

* 🔹 When the top row is processed, `dp[0]` contains the **minimum total path sum** from the top to the bottom.

---

## ⏱ Time Complexity

**O(n²)**

* Where :
    -  `n` =  number of rows.
* Every element in the triangle is processed exactly once,
    
---

## 📦 Space Complexity

**O(n)**

* A one-dimensional DP array of size height + 1 is used.

---

## 💻 Java Code

```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int height = triangle.size();
        int[] dp = new int[height + 1];

        for (int layer = height - 1; layer >= 0; --layer) {
            for (int index = 0; index <= layer; ++index) {
                dp[index] = Math.min(dp[index], dp[index + 1]) + triangle.get(layer).get(index);
            }
        }
        return dp[0];
    }
}
```

---