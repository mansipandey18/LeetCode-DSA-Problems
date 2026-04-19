`# <u>202. Happy Number</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/happy-number/

---

## 🧠 Intuition:
* 🔹 A number is **happy** if repeatedly replacing it with the **sum of squares of its digits** eventually leads to `1`

* 🔹 If it never reaches `1`, it will **fall into a cycle** (loop of numbers)

* 🔹 So the problem becomes: **detect whether the sequence reaches 1 or enters a cycle**

* 🔹 To efficiently detect a cycle, we use **Floyd’s Cycle Detection (slow & fast pointers)**

* 🔹 `slow` moves one step → `sumOfSquares(n)`

* 🔹 `fast` moves two steps → `sumOfSquares(sumOfSquares(n))`

* 🔹 If at any point `fast == 1`, we found a happy number → return `true`

* 🔹 If `slow == fast`, a cycle is detected → number is not happy → `return false`

* 🔹 This avoids using extra memory like a set and makes solution optimal

---

## ⏱ Time Complexity

**O(log n)**

* Each transformation takes **O(d)** where `d = number of digits`

* Number of iterations is limited (values shrink quickly into a cycle or 1)
    
---

## 📦 Space Complexity

**O(1)**

* No extra data structures are used.

---

## 💻 Java Code

```java
class Solution {
    public boolean isHappy(int n) {
        int slow = n, fast = n;

        while(fast != 1){
            slow = sumOfSquaresOfDigits(slow);
            fast = sumOfSquaresOfDigits(sumOfSquaresOfDigits(fast));

            if(fast == 1){
                return true;
            } 
            if(slow == fast){
                return false;
            }
        }
        return true;
    }

    private int sumOfSquaresOfDigits(int n){
        int sum = 0;

        while(n > 0){
            int digit = n % 10; 
            sum += (digit * digit);
            n = n / 10;
        }
        return sum;
    }
}
```

---