# <u>2352. Equal Row and Column Pairs</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/equal-row-and-column-pairs/

---

## 🧠 Intuition:
* 🔹 Goal is to count how many **row–column pairs are exactly equal**

* 🔹 For every row `i` and column `j`, we try to check if they are identical

* 🔹 Compare row `i` and column `j` **element by element (k from 0 to n-1)**

* 🔹 If any element mismatches → stop checking that pair immediately

* 🔹 If all elements match (`k reaches n`) → we found a valid pair → **increase count**

* 🔹 Repeat this for all possible (`i, j`) combinations

---

## ⏱ Time Complexity

**O(n^3)**

* Outer two loops → **O(n²)**
* Inner comparison loop → **O(n)**
    
---

## 📦 Space Complexity

**O(1)**

* No extra space used

---

## 💻 Java Code

```java
class Solution {
    public int equalPairs(int[][] grid) {
        int n = grid.length;
        int ans = 0;

        for (int i = 0; i < n; ++i)
            for (int j = 0; j < n; ++j) {
                int k = 0;
                for (; k < n; ++k)
                    if (grid[i][k] != grid[k][j])
                        break;
                if (k == n) // R[i] == C[j]
                  ++ans;
            }

        return ans;
    }
}
```

---