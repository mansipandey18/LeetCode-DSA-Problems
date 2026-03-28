# <u>2573. Find the String with LCP</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/find-the-string-with-lcp/

---

## 🧠 Intuition:
* 🔹 We create an empty result string of size `n`.

* 🔹 Start assigning characters from `'a'` to `'z'`.

* 🔹 Find the **first unfilled position** in the result.

* 🔹 If `lcp[i][j] > 0`, it means:
    - suffix at `i` and suffix at `j` must start with the **same character**.
    - So we assign the same character to those positions.

* 🔹 Continue this process until all positions get characters.

* 🔹 If any position is still unassigned → construction is impossible → return `""`.


* #### 🔹Validation Phase (Very Important)

    - After building the string:
        * Check every pair `(i, j)`:
            - If characters match → LCP must follow rule:
                * `lcp[i][j] = 1 + lcp[i+1][j+1]`
            - If characters differ → LCP must be `0`.
            - If any condition fails → return empty string.
---

## ⏱ Time Complexity

**O(n^2)**

* Let : 
    - `n = lcp.length.`

* 1️⃣ Character Assignment
    - Outer loop runs at most 26 times (a–z).
    - Inner loop scans up to `n`.

    - ✅ Complexity: `O(26 × n) ≈ O(n)`

* 2️⃣ Checking unassigned characters
    - Single loop over string.

    - ✅ O(n)

* 3️⃣ Validation of LCP matrix
    - Two nested loops over matrix.

    - ✅ O(n²)
---

## 📦 Space Complexity

**O(n)**

* `result[]` array of size `n`.

* No extra large structures used.

---

## 💻 Java Code

```java
class Solution {
    public String findTheString(int[][] lcp) {
        int n = lcp.length;
        char[] result = new char[n];
        int currentIndex = 0;
      
        // Try to assign characters from 'a' to 'z' to build the string
        for (char currentChar = 'a'; currentChar <= 'z'; ++currentChar) {
            // Find the next unassigned position
            while (currentIndex < n && result[currentIndex] != '\0') {
                ++currentIndex;
            }
          
            // If all positions are filled, we're done
            if (currentIndex == n) {
                break;
            }
          
            // Assign current character to all positions that should have it
            // based on LCP values (if lcp[currentIndex][j] > 0, they share a prefix)
            for (int j = currentIndex; j < n; ++j) {
                if (lcp[currentIndex][j] > 0) {
                    result[j] = currentChar;
                }
            }
        }
      
        // Check if all positions have been assigned a character
        for (int i = 0; i < n; ++i) {
            if (result[i] == '\0') {
                return "";  // Not enough characters to satisfy LCP constraints
            }
        }
      
        // Validate the constructed string against LCP matrix
        for (int i = n - 1; i >= 0; --i) {
            for (int j = n - 1; j >= 0; --j) {
                if (result[i] == result[j]) {
                    // Characters match, verify LCP value
                    if (i == n - 1 || j == n - 1) {
                        // At boundary, LCP should be exactly 1
                        if (lcp[i][j] != 1) {
                            return "";
                        }
                    } else {
                        // LCP should be 1 + LCP of next positions
                        if (lcp[i][j] != lcp[i + 1][j + 1] + 1) {
                            return "";
                        }
                    }
                } else {
                    // Characters don't match, LCP should be 0
                    if (lcp[i][j] > 0) {
                        return "";
                    }
                }
            }
        }
      
        return String.valueOf(result);
    
    }
}
```

---