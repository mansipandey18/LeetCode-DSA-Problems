# <u>374. Guess Number Higher or Lower</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/guess-number-higher-or-lower/

---

## 🧠 Intuition:
* 🔹 The picked number lies between 1 and n, so Binary Search can be used efficiently.

* 🔹 Maintain two pointers: `left` and `right` to represent the current search range.

* 🔹 Find the middle value using
    - `mid = (left + right) >>> 1`

* 🔹 Call the guess(mid) API to compare mid with the hidden number.

* 🔹 If `guess(mid) == 0`, then mid is the correct answer.

* 🔹 If `guess(mid) == -1`, it means mid is greater than the picked number, so search in the left half.

* 🔹 If `guess(mid) == 1`, it means mid is smaller than the picked number, so search in the right half.

* 🔹 Continuously shrink the search space until `left == right`.

* 🔹 The final value of left will be the picked number.

---

## ⏱ Time Complexity

**O(log n)**

* Binary Search reduces the search space by half in every step
    
---

## 📦 Space Complexity

**O(1)**

* Only constant extra variables are used.

---

## 💻 Java Code

```java
/** 
 * Forward declaration of guess API.
 * @param  num   your guess
 * @return 	     -1 if num is higher than the picked number
 *			      1 if num is lower than the picked number
 *               otherwise return 0
 * int guess(int num);
 */

public class Solution extends GuessGame {
    public int guessNumber(int n) {
        int left = 1;
        int right = n;
      
        while (left < right) {
            int mid = (left + right) >>> 1;
          
            int guessResult = guess(mid);
          
            if (guessResult <= 0) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
      
        return left;
    }
}   
```

---