# <u>1510. Stone Game IV</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/stone-game-iv/

---

## 🧠 Intuition:
* 🔹 Use **Dynamic Programming + Recursion (Memoization)** to determine whether the current player can force a win.

* 🔹 Define `canWin(remainingStones)` as:
    - `true` → the current player can win with the given number of stones.
    - `false` → the current player will lose if both players play optimally.

* 🔹 For each state, try removing every possible **perfect square** `j²` such that `j² ≤ remainingStones`.

* 🔹 After removing `j²`, the opponent gets the new state `remainingStones - j²`.

* 🔹 If **any move** makes the opponent lose (`canWin(...) == false`), the current player can win, so mark the current state as `true`.

* 🔹 If none of the possible moves makes the opponent lose, mark the state as `false`.

* 🔹 The base case is `remainingStones <= 0`, where there are no stones left to remove, so the current player loses.

* 🔹 The `memo` array stores already-computed states, avoiding repeated recursive calculations.

* 🔹 Therefore, the solution checks all possible game states and finds whether the first player has a winning strategy.

---

## ⏱ Time Complexity

**O(n√n)**

* There are at most `n` different states.
* For each state, we try up to `√n` perfect-square moves.
    
---

## 📦 Space Complexity

**O(n)**

* `memo` array stores results for `n + 1` states.
* Recursive call stack can also take up to `O(n)` in the worst case.

---

## 💻 Java Code

```java
class Solution {
    private Boolean[] memo; 

    public boolean winnerSquareGame(int n) {
        memo = new Boolean[n + 1];
      
        return canWin(n);
    }

    private boolean canWin(int remainingStones) {
        if (remainingStones <= 0) {
            return false;
        }
      
        if (memo[remainingStones] != null) {
            return memo[remainingStones];
        }
      
        for (int j = 1; j * j <= remainingStones; j++) {
            if (!canWin(remainingStones - j * j)) {
                memo[remainingStones] = true;
                return true;
            }
        }
      
        memo[remainingStones] = false;
        return false;
    }
}
```

---