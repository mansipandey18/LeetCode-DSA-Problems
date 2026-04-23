# <u>2390. Removing Stars From a String</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/removing-stars-from-a-string/

---

## 🧠 Intuition:
* 🔹 The problem simulates a process where each `'*'` removes the **last added character**

* 🔹 Use a `StringBuilder` as a **stack-like structure**

* 🔹 Traverse the string character by character:
    - If the character is not `'*'`, simply **append it**
    - If the character is `'*'`, remove the **last character** from `StringBuilder` (like popping from stack)

* 🔹 This ensures we always remove the closest previous valid character

* 🔹 Finally, convert the `StringBuilder` to string and return the result

---

## ⏱ Time Complexity

**O(n)**

* Each character is processed once
    
---

## 📦 Space Complexity

**O(n)**

* StringBuilder stores final characters

---

## 💻 Java Code

```java
class Solution {
    public String removeStars(String s) {
        StringBuilder sb = new StringBuilder();
        for (final char c : s.toCharArray())
            if (c == '*')
                sb.deleteCharAt(sb.length() - 1);
            else
                sb.append(c);
        return sb.toString();
    }
}
```

---