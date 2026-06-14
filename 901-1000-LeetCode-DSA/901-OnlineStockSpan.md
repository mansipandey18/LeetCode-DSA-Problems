# <u>901. Online Stock Span</u>

----

## 🔗 Problem Link

https://leetcode.com/problems/online-stock-span/

---

## 🧠 Intuition:
* 🔹 We need to find the **stock span**, i.e., the number of consecutive days (including today) for which the stock price was less than or equal to today's price.

* 🔹 Use a **Monotonic Decreasing Stack** that stores `{price, span}` pairs.

* 🔹 For each new price:
    - Start with `count = 1` (today itself contributes one day).
    - While the stack is not empty and the top price is **less than or equal to** the current price:
        * Pop that element.
        * Add its stored span to `count`.

* 🔹 This works because all those previous days are also part of the current stock span.

* 🔹 Push the pair `{currentPrice, count}` onto the stack.

* 🔹 Return `count` as the span for the current day.

* 🔹 Storing spans directly helps avoid rechecking previous prices, making the solution efficient.


---

## ⏱ Time Complexity

**O(n)**

* Each price is pushed onto the stack once and popped at most once.

* **Amortized Time Complexity per `next()` call: O(1)** 

---

## 📦 Space Complexity

**O(n)**

* Where:
    - `n` = number of calls to `next()`.

* In the worst case (strictly decreasing prices), all prices remain in the stack.

---

## 💻 Java Code

```java
class StockSpanner {
    private Deque<int[]> stack = new ArrayDeque<>();

    public StockSpanner() {
        
    }
    
    public int next(int price) {
        int count = 1;
      
        while (!stack.isEmpty() && stack.peek()[0] <= price) {
            count += stack.pop()[1];
        }
      
        stack.push(new int[] {price, count});
      
        return count;

    }
}

/**
 * Your StockSpanner object will be instantiated and called as such:
 * StockSpanner obj = new StockSpanner();
 * int param_1 = obj.next(price);
 */

```

---