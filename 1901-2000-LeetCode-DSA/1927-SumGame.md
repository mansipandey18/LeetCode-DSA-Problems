# <u>1927. Sum Game</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/nearest-exit-from-entrance-in-maze/

---

## 🧠 Intuition:
* 🔹 Divide the string into two equal halves and calculate:
    - `leftSum` → sum of known digits in the left half.
    - `rightSum` → sum of known digits in the right half.
    - `leftQuestionMarks` and `rightQuestionMarks` → number of `?` in each half.

* 🔹 If the **total number of `?` is odd**, Alice can always make the final sums unequal because Bob cannot perfectly pair all the unknown positions.

* 🔹 If the number of `?` is even, the unknown digits can be considered in **pairs**, with one `?` from each side.

* 🔹 For the sums to become equal, the existing sum difference must exactly compensate for the maximum possible contribution of the unmatched `?` positions.

* 🔹 Each digit can contribute from `0` to `9`, so the critical difference is based on **9 × the difference in the number of question marks**.

* 🔹 The condition for Bob to force equality is:
    `sumDifference == 9 * questionMarkDifference / 2`.

* 🔹 Therefore, Alice wins if:
    - the total number of `?` is odd, or
    - the existing sum difference cannot be balanced by the remaining `?` positions.

* 🔹 The code directly checks these conditions and returns `true` when Alice can guarantee a win.

---

## ⏱ Time Complexity

**O(n)**

* The string is traversed twice, with each character processed once.

---

## 📦 Space Complexity

**O(1)**

* Only a constant number of variables are used.

---

## 💻 Java Code

```java
class Solution {
    public boolean sumGame(String num) {
        int length = num.length();
      
        int leftQuestionMarks = 0;
        int leftSum = 0;
        for (int i = 0; i < length / 2; i++) {
            if (num.charAt(i) == '?') {
                leftQuestionMarks++;
            } else {
                leftSum += num.charAt(i) - '0';
            }
        }
      
        int rightQuestionMarks = 0;
        int rightSum = 0;
        for (int i = length / 2; i < length; i++) {
            if (num.charAt(i) == '?') {
                rightQuestionMarks++;
            } else {
                rightSum += num.charAt(i) - '0';
            }
        }
      
        int totalQuestionMarks = leftQuestionMarks + rightQuestionMarks;
        int sumDifference = leftSum - rightSum;
        int questionMarkDifference = rightQuestionMarks - leftQuestionMarks;
      
        return totalQuestionMarks % 2 == 1 || sumDifference != 9 * questionMarkDifference / 2;
    
    }
}
```

---