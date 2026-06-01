# <u>2144. Minimum Cost of Buying Candies With Discount</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/minimum-cost-of-buying-candies-with-discount/

---

## 🧠 Intuition:
* 🔹 To minimize the total cost, we should maximize the value of the **free candy** received in every group of three.

* 🔹 Sort the candy prices in **ascending order**.

* 🔹 Process the candies from the **most expensive to the least expensive**.

* 🔹 For every group of three candies:
    - Pay for the two most expensive candies.
    - Get the third candy (the cheapest in that group) for free.

* 🔹 By grouping the most expensive candies together, the free candy is as expensive as possible, reducing the total cost the most.

* 🔹 Traverse the sorted array from the end with a step of `3`:
    - Add the largest candy price.
    - Add the second largest candy price (if it exists).
    - Skip the third candy since it is free.

* 🔹 The accumulated sum gives the minimum amount needed to buy all candies.

---

## ⏱ Time Complexity

**O(n log n)**

* due to sorting the candy prices.
  
---

## 📦 Space Complexity

**O(1)**

* excluding the space used by the sorting algorithm.

---

## 💻 Java Code

```java
class Solution {
    public int minimumCost(int[] cost) {
        Arrays.sort(cost);
      
        int totalCost = 0;
      
        for (int i = cost.length - 1; i >= 0; i -= 3) {
            // Add the most expensive item in the current group
            totalCost += cost[i];
          
            // Add the second most expensive item if it exists
            if (i > 0) {
                totalCost += cost[i - 1];
            }
            // The third item (at index i-2) is free, so we skip it
        }
      
        return totalCost;
    }
}
```

---