# <u>3474. Lexicographically Smallest Generated String</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/lexicographically-smallest-generated-string/

---

## 🧠 Intuition:
* 🔹 We must build a lexicographically smallest string such that:
    - `'T'` in `str1` → substring must match `str2`.
    - `'F'` in `str1` → substring must NOT match `str2`.

* **🔹 1️⃣ Handle all 'T' conditions first:**
    * Whenever `str1[i] == 'T'`:
        - Force `str2` to appear starting at index `i`.
        - Copy characters of `str2` into the result.
    
    * If overlapping placements conflict → impossible → return `""`.
    * Mark these positions as fixed (cannot change later).

    👉 Because `'T'` constraints are compulsory.

* **🔹 2️⃣ Fill remaining characters greedily:**
    * For positions not fixed:
        - Fill `'a'`.

    * Why `'a'`?
        - It keeps the result **lexicographically smallest**.
 
* **🔹 3️⃣ Validate and fix 'F' conditions**
    * For each `'F'` position:
        - Check if substring accidentally equals `str2`.

    * If it matches (which is not allowed):
        - Change the rightmost non-fixed character to `'b'`.
        - This breaks the match while keeping the string as small as possible.

    * If no character can be changed → impossible → return `""`.

* **🔹 3️⃣ Validate and fix 'F' conditions**
    * After satisfying all `'T'` and `'F'` rules, return the constructed string.
---

## ⏱ Time Complexity

**O(n × m)**

* Let:
    - `n = str1.length()`
    - `m = str2.length()`

* **Operations**:
    - Filling `'T'` windows → `O(n × m)`
    - Validation of `'T'` and `'F'` windows → `O(n × m)`
    - Greedy filling → `O(n + m)`

---

## 📦 Space Complexity

**O(n + m)**

* Result array of size `n + m − 1`
* Boolean fixed array of same size

---

## 💻 Java Code

```java
class Solution {
   public String generateString(String str1, String str2) {
        int n = str1.length();
        int m = str2.length();
        int len = n + m - 1;
        char[] res = new char[len];
        boolean[] fixed = new boolean[len];

        // Step 1: Fill 'T' requirements
        for (int i = 0; i < n; i++) {
            if (str1.charAt(i) == 'T') {
                for (int j = 0; j < m; j++) {
                    if (fixed[i + j] && res[i + j] != str2.charAt(j)) return "";
                    res[i + j] = str2.charAt(j);
                    fixed[i + j] = true;
                }
            }
        }

        // Step 2: Initial greedy fill
        for (int i = 0; i < len; i++) {
            if (!fixed[i]) res[i] = 'a';
        }

        // Step 3: Validate and adjust for 'F'
        for (int i = 0; i < n; i++) {
            if (str1.charAt(i) == 'T') {
                // Double check 'T' consistency for overlaps
                for (int j = 0; j < m; j++) {
                    if (res[i + j] != str2.charAt(j)) return "";
                }
            } else {
                // Check if 'F' is violated
                boolean match = true;
                for (int j = 0; j < m; j++) {
                    if (res[i + j] != str2.charAt(j)) {
                        match = false;
                        break;
                    }
                }

                if (match) {
                    // Must change the rightmost non-fixed character in this window
                    boolean changed = false;
                    for (int j = m - 1; j >= 0; j--) {
                        if (!fixed[i + j]) {
                            res[i + j] = 'b';
                            changed = true;
                            break;
                        }
                    }
                    if (!changed) return ""; // No flexible chars to break the 'F' match
                }
            }
        }

        return new String(res);
    }

}

```

---