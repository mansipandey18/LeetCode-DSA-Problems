# <u>3612. Process String with Special Operations I</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/process-string-with-special-operations-i/

---

## 🧠 Intuition:
* 🔹 Use a **StringBuilder** to efficiently maintain and modify the resulting string while processing each character.

* 🔹 Traverse the input string from left to right and apply the operation based on the current character.

* 🔹 If the character is a lowercase letter:
    - Append it to the result string.

* 🔹 If the character is `'*'`:
    - Remove the last character from the result if it exists (simulates a backspace operation).

* 🔹 If the character is `'#'`:
    - Duplicate the current result by appending it to itself.

* 🔹 If the character is `'%'`:
    - Reverse the current result string.

* 🔹 StringBuilder allows efficient appending, deletion, and reversing operations, making it suitable for handling these transformations.

* 🔹 After processing all characters, return the final generated string.


---

## ⏱ Time Complexity

**O(n + total size of all modifications)**

* Let **n** be the length of the input string and **m** be the length of the final result.
* Traversing the input string takes **O(n)**.
* Operations like `#` (duplicate) and `%` (reverse) may process the current result string, which can take **O(m)** time.

---

## 📦 Space Complexity

**O(m)**

* where:
    - `m` = length of the final processed string

---

## 💻 Java Code

```java
class Solution {
    public String processStr(String s) {
        StringBuilder result = new StringBuilder();
        
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            
            if (Character.isLowerCase(c)) {
                // Rule 1: Append lowercase English letter
                result.append(c);
            } else if (c == '*') {
                // Rule 2: Remove the last character if it exists
                if (result.length() > 0) {
                    result.deleteCharAt(result.length() - 1);
                }
            } else if (c == '#') {
                // Rule 3: Duplicate the current result and append it to itself
                result.append(result.toString());
            } else if (c == '%') {
                // Rule 4: Reverse the current result
                result.reverse();
            }
        }
        
        return result.toString();
    }
}
```

---