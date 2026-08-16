# <u>2029. Stone Game IX</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/stone-game-ix/

---

## 🧠 Intuition:
* 🔹 The important observation is that only the **remainder modulo 3** of each stone matters.

* 🔹 Count stones having remainders:
    - `0`
    - `1`
    - `2`

* 🔹 The game is losing for a player whenever their chosen stones make the running sum divisible by `3`.

* 🔹 A stone with remainder `0` **does not change the current remainder**, while choosing `1` or `2` changes it.

* 🔹 Because the game is symmetric between remainders 1 and 2, the code checks **two possible starting scenarios**:
    - Start with a remainder-`1` stone.
    - Start with a remainder-`2` stone.

* 🔹 In `check()`:
    - First, one stone of the starting remainder is consumed.
    - Then the remaining `1` and `2` stones are considered in alternating pairs because `1 + 2 ≡ 0 (mod 3)`.
    - Remainder-`0` stones can be played afterward without changing the modulo state.

* 🔹 The calculation of `totalTurns` determines how many valid moves can occur under that scenario.

* 🔹 Finally, the scenario is winning when:
    - The number of turns has the required **odd parity**, and
    - The counts of remainder-`1` and remainder-`2` stones are not perfectly balanced.

* 🔹 If either starting scenario allows Alice to force a win, return `true`.

---

## ⏱ Time Complexity
**O(n)**

* Counting remainders takes **O(n)**.
* The two `check()` calls each take **O(1)**.

---

## 📦 Space Complexity

**O(1)**

* Only a few fixed-size arrays are used.

---

## 💻 Java Code

```java
class Solution {
    public boolean stoneGameIX(int[] stones) {
        int[] countByRemainder = new int[3];
        for (int stone : stones) {
            countByRemainder[stone % 3]++;
        }
      
        int[] scenario1 = {countByRemainder[0], countByRemainder[1], countByRemainder[2]};
      
        int[] scenario2 = {countByRemainder[0], countByRemainder[2], countByRemainder[1]};
      
        return check(scenario1) || check(scenario2);
    }

    private boolean check(int[] remainderCounts) {
        remainderCounts[1]--;
        if (remainderCounts[1] < 0) {
            return false;
        }
      
        int totalTurns = 1 + Math.min(remainderCounts[1], remainderCounts[2]) * 2 + remainderCounts[0];
      
        if (remainderCounts[1] > remainderCounts[2]) {
            remainderCounts[1]--;
            totalTurns++;
        }
      
        return totalTurns % 2 == 1 && remainderCounts[1] != remainderCounts[2];   
    }
}
```

---