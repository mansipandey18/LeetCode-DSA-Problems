# <u>28. Find the Index of the First Occurrence in a String</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/

---

## 🧠 Intuition:
* 🔹 We want to find where `needle` first appears inside `haystack`.

* 🔹 Start checking from every possible index of `haystack`.

* 🔹 At each index `i`, take a substring of length equal to `needle`.

* 🔹 Compare this substring with `needle`.

* 🔹 If both strings are equal → we found the answer, return index `i`.

* 🔹 If not equal → move one step forward and try again.

* 🔹 Continue until all possible starting positions are checked.

* 🔹 If no match is found, return `-1`.

---

## ⏱ Time Complexity

**O(m * n)**

* Where:
    - `m = haystack.length()`
    - `n = = needle.length()`

* Outer loop runs (m − n + 1) times.

* Each time:
    - `substring()` takes O(n)
    - `equals()` comparison takes O(n)
    
---

## 📦 Space Complexity

**O(n)**

* `substring(i, i+n)` creates a new string of length `n`.

---

## 💻 Java Code

```java
class Solution {
    public int strStr(String haystack, String needle) {
        int m = haystack.length(), n = needle.length();

        for (int i = 0; i < m - n + 1; ++i)
          if (haystack.substring(i, i + n).equals(needle))
            return i;

        return -1;
    }
}
```

---