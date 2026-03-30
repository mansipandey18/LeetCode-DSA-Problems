# <u>392. Is Subsequence</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/is-subsequence/

---

## 🧠 Intuition:
* 🔹 A string **s is a subsequence of t** if all characters of `s` appear in `t` **in the same order**, not necessarily continuously.

* 🔹 Use **two pointers**:
    - `indexS` → tracks characters in string `s`.
    - `indexT` → scans through string `t`.

* 🔹 Traverse string `t` one character at a time.

* 🔹 Whenever characters at both pointers match:
    - Move `indexS` forward (we found the next required character).

* 🔹 Always move `indexT` forward to keep searching in `t`.

* 🔹 Continue until either:
    - All characters of `s` are matched, or
    - `t` finishes.

* 🔹 If `indexS` reaches the length of `s`, it means **all characters were found in order**, so s is a subsequence of `t`.
---

## ⏱ Time Complexity

**O(n)**

* Where :
    - `n` = length of t

* Each character of `t` is visited once.
    
---

## 📦 Space Complexity

**O(1)**

* Only pointer variables are used.
* No extra data structures required.

---

## 💻 Java Code

```java
class Solution {
    public boolean isSubsequence(String s, String t) {
        int lengthS = s.length(), lengthT = t.length();
        int indexS = 0, indexT = 0;
      
        while (indexS < lengthS && indexT < lengthT) {
            if (s.charAt(indexS) == t.charAt(indexT)) {
                ++indexS;
            }
            ++indexT;
        }
      
        return indexS == lengthS;
    }
}
```

---