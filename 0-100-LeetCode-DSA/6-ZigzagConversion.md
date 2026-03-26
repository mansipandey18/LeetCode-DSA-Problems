# <u>6. Zigzag Conversion</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/zigzag-conversion/

---

## 🧠 Intuition:
* 🔹 We need to write the string in a zigzag (down and up) pattern using given rows.

* 🔹 Instead of actually drawing the zigzag shape, we notice the pattern repeats again and again.

* 🔹 One complete zigzag movement (going down + coming up diagonally) is called a cycle.

* 🔹 The length of one cycle is:
    - `cycleLen = 2 × numRows − 2`

* 🔹 Characters belonging to the same row appear after every cycleLen distance.

* #### 🔹 How characters are picked:

    * First row
        - Characters come at equal gaps (cycleLen).
        - Only one character per cycle.
    
    * Last row
        - Same as first row — fixed gap pattern.
    
    * Middle rows
        - Each cycle gives two characters:
            * one while moving down,
            * one while moving diagonally up.
    
    * We go row by row, pick correct characters using index calculation, and add them to the result.

    * Finally, joining all rows gives the zigzag converted string.
---

## ⏱ Time Complexity

**O(n)**

* Let :
    - `n` = length of string.

* Each character is visited and appended exactly once.

---

## 📦 Space Complexity

**O(n)**
  
* `StringBuilder` stores the result string of size `n`.

---

## 💻 Java Code

```java
class Solution {
    public String convert(String s, int numRows) {
        if (numRows == 1){
            return s;
        }
        StringBuilder sb = new StringBuilder();
        int n = s.length();
        int cycleLen = 2 * numRows - 2;
        
        for (int i = 0; i < numRows; i++) {
            for (int j = 0; j + i < n; j += cycleLen) {
                sb.append(s.charAt(j + i));
                if (i != 0 && i != numRows - 1 && j + cycleLen - i < n)
                    sb.append(s.charAt(j + cycleLen - i));
            }
        }
        return sb.toString();
    }
}
```

---