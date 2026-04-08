# <u>443. String Compression</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/string-compression/

---

## 🧠 Intuition:
* 🔹 The goal is to **compress the character array in-place** using run-length encoding.

* 🔹 Traverse the array and **group consecutive identical characters**.

* 🔹 Use pointer `i` to scan the array and another pointer `ans` to write the compressed result.

* 🔹 For each group:
    - Store the current character (`letter`).
    - Count how many times it repeats consecutively (`count`).

* 🔹 Write the character once at position `ans`.

* 🔹 If the frequency (`count`) is greater than 1:
    - Convert the count into characters (e.g., `12 → '1','2'`).
    - Append each digit into the array.

* 🔹 Move forward until all characters are processed.

* 🔹 Since writing happens in the same array, no extra array is needed (**in-place compression**).

* 🔹 Return `ans`, which represents the **length of the compressed string**.

---

## ⏱ Time Complexity

**O(n)**

* Where :
    - `n` = length of `chars`

* Each character is visited once while counting groups → **O(n)**.

* Writing count digits also totals at most `n` operations overall.
    
---

## 📦 Space Complexity

**O(1)**

* Compression is done **in-place**.

* Only a few variables are used.

* Temporary string conversion for count digits is proportional to digit length (constant relative to `n`).

---

## 💻 Java Code

```java
class Solution {
    public int compress(char[] chars) {
        int ans = 0;

        for (int i = 0; i < chars.length;) {
            char letter = chars[i];
            int count = 0;
            while (i < chars.length && chars[i] == letter) {
                ++count;
                ++i;
            }
            chars[ans++] = letter;
            if (count > 1)
                for (final char c : String.valueOf(count).toCharArray())
                    chars[ans++] = c;
        }

        return ans;

    }
}   
```

---