# <u>1406. Stone Game III</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/stone-game-iii/

---

## 🧠 Intuition:
* 🔹 Process the stones **from right to left**, so that the result for future positions is already known.

* 🔹 Keep a suffix sum (`sufSum`) to know the total value of all stones from the current index to the end.

* 🔹 Let `f1`, `f2`, and `f3` represent the **maximum score the current player can secure** starting from the next 1st, 2nd, and 3rd positions respectively.

* 🔹 At each position, the current player can take **1, 2, or 3** stones.

* 🔹 Instead of checking every choice separately, observe that:
    - Whatever stones the current player leaves behind become the opponent's starting position.
    - The opponent will play optimally and secure the **minimum possible score** for the current player.

* 🔹 Therefore, the current player's best score is:
    - **Total remaining suffix sum − minimum(opponent's best score after taking 1, 2, or 3 stones)**.

* 🔹 Compute the new best score (`newF`) using this formula and shift `f1`, `f2`, and `f3` to move one step left.

* 🔹 After processing all positions:
    - `f1` stores Alice's maximum possible score.
    - `sufSum - f1` gives Bob's score.

* 🔹 Compare both scores:
    - If equal → `"Tie"`.
    - If Alice's score is larger → `"Alice"`.
    - Otherwise → `"Bob"`.


---

## ⏱ Time Complexity

**O(n)**

* Where : 
    - `n` = number of nodes in the tree

* Each node is visited exactly once
    
---

## 📦 Space Complexity

**O(h)**

* Best case (balanced tree): `O(log n)`
* Worst case (skewed tree): `O(n)`
* Due to recursion stack (height of tree)

---

## 💻 Java Code

```java
class Solution {
    public String stoneGameIII(int[] stoneValue) {
        int sufSum = 0;
        int f1 = 0;
        int f2 = 0;
        int f3 = 0;
        for (int i = stoneValue.length - 1; i >= 0; i--) {
            sufSum += stoneValue[i];
            int newF = sufSum - Math.min(Math.min(f1, f2), f3);
            f3 = f2;
            f2 = f1;
            f1 = newF;
        }

        int diff = f1 - (sufSum - f1);
        if (diff == 0) {
            return "Tie";
        }
        return diff > 0 ? "Alice" : "Bob";
    }
}
```

---