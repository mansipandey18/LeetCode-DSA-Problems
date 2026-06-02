# <u>1137. N-th Tribonacci Number</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/n-th-tribonacci-number/

---

## 🧠 Intuition:
* 🔹 Tribonacci sequence follows:
    - `T0 = 0`
    - `T1 = 1`
    - `T2 = 1`
    - `Tn = T(n-1) + T(n-2) + T(n-3)`

* 🔹 Instead of using recursion or DP array, keep track of only the last three numbers.

* 🔹 Initialize:
    - `first = 0`
    - `second = 1`
    - `third = 1`

* 🔹 In each iteration:
    - Compute the next Tribonacci number using the sum of previous three values.
    - Shift the variables forward:
        * `first = second`
        * `second = third`
        * `third = next`

* 🔹 Repeat this process `n` times.

* 🔹 After all updates, `first` holds the required `n-th` Tribonacci number.

* 🔹 This approach avoids recursion overhead and optimizes space usage.

---

## ⏱ Time Complexity

**O(n)**

* One loop runs `n` times.
    
---

## 📦 Space Complexity

**O(1)**

* Only a few variables are used regardless of input size.

---

## 💻 Java Code

```java
class Solution {
    public int tribonacci(int n) {
        int first = 0;   
        int second = 1;  
        int third = 1;   
      
        while (n-- > 0) {
            int next = first + second + third;
          
            first = second;
            second = third;
            third = next;
        }
      
        return first;

    }
}
```

---