# <u>123. Best Time to Buy and Sell Stock III</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/

---

## 🧠 Intuition:
* 🔹 We can perform at **most two transactions**, so track the best profit after each stage of trading.

* 🔹 Maintain four variables:
    - `firstBuyProfit` → Maximum profit after buying the first stock.
    - `firstSellProfit` → Maximum profit after selling the first stock.
    - `secondBuyProfit` → Maximum profit after buying the second stock using the profit from the first sale.
    - `secondSellProfit` → Maximum profit after selling the second stock.

* 🔹 Traverse the price array once and update these states in order:
    - Update the best cost for the **first buy**.
    - Update the best profit after the **first sell**.
    - Update the best profit after the **second buy** by reinvesting the first transaction's profit.
    - Update the best profit after the **second sell**.

* 🔹 Each state always stores the best possible value up to the current day.

* 🔹 After processing all prices, `secondSellProfit` contains the maximum profit achievable with at most two transactions.

---

## ⏱ Time Complexity

**O(n)**

* The prices array is traversed exactly once.
    
---

## 📦 Space Complexity

**O(1)**

* Only four variables are used to track the transaction states.

---

## 💻 Java Code

```java
class Solution {
    public int maxProfit(int[] prices) {
        int firstBuyProfit = -prices[0];
      
        int firstSellProfit = 0;
      
        int secondBuyProfit = -prices[0];
      
        int secondSellProfit = 0;
      
        for (int i = 1; i < prices.length; ++i) {
            firstBuyProfit = Math.max(firstBuyProfit, -prices[i]);
          
            firstSellProfit = Math.max(firstSellProfit, firstBuyProfit + prices[i]);
          
            secondBuyProfit = Math.max(secondBuyProfit, firstSellProfit - prices[i]);
          
            secondSellProfit = Math.max(secondSellProfit, secondBuyProfit + prices[i]);
        }
      
        return secondSellProfit;
    
    }
}
```

---