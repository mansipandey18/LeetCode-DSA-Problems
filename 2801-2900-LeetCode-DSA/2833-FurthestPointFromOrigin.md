# <u>2833. Furthest Point From Origin</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/furthest-point-from-origin/

---

## 🧠 Intuition:
* 🔹 Each `'L'` moves the position by -1, each `'R'` moves it by +1, and each `'_'` can be chosen as either `'L'` or `'R'`

* 🔹 To maximize the final distance from origin, all `'_'` moves should be used in the direction that increases the existing imbalance between left and right moves

* 🔹 First, count how many `'L'`, `'R'`, and `'_'` characters are present in the string

* 🔹 The current fixed distance from origin is `|leftCount - rightCount|`

* 🔹 Since every wildcard `'_'` can contribute +1 more distance in the better direction, simply add all wildcard moves to this value

* 🔹 Final answer becomes:

* 🔹 **|number of L - number of R| + number of '_'**

* 🔹 This guarantees the maximum possible distance from the origin

---

## ⏱ Time Complexity

**O(n)**

* Counting characters in the string takes **O(n)** time
* Since `countCharacter()` is called 3 times,
    
---

## 📦 Space Complexity

**O(1)**

* Only a few integer variables are used

---

## 💻 Java Code

```java
class Solution {
    public int furthestDistanceFromOrigin(String moves) {
        int leftCount = countCharacter(moves, 'L');
        int rightCount = countCharacter(moves, 'R');
        int wildcardCount = countCharacter(moves, '_');
      
        return Math.abs(leftCount - rightCount) + wildcardCount;
    }

    private int countCharacter(String str, char targetChar) {
        int count = 0;
      
        for (int i = 0; i < str.length(); i++) {
            if (str.charAt(i) == targetChar) {
                count++;
            }
        }
      
        return count;
    }
}
```

---