# <u>796. Rotate String</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/rotate-string/

---

## 🧠 Intuition:
* 🔹 The problem is to check whether string goal can be obtained by rotating string s

* 🔹 A key observation:
    - If we concatenate the string with itself (s + s), it contains all possible rotations of s as substrings

* 🔹 Example:
    - s = "abcde" → s + s = "abcdeabcde"
    - All rotations like "bcdea", "cdeab", etc. will appear inside this string

* 🔹 So instead of generating all rotations manually, we just check:
    - If goal is a substring of s + s

* 🔹 Additionally, both strings must have equal length, otherwise rotation is impossible

* 🔹 If both conditions satisfy → return true, else false

* 🔹 This approach avoids explicit rotation and gives an efficient solution

---

## ⏱ Time Complexity

**O(n)**

* Concatenation → **O(n)**
* Substring check (`contains`) → **O(n)** (on average with optimized string search)

    
---

## 📦 Space Complexity

**O(n)**

* New string `s + s` is created

---

## 💻 Java Code

```java
class Solution {
    public boolean rotateString(String s, String goal) {
        return s.length() == goal.length() && (s + s).contains(goal);
    }
}
```

---