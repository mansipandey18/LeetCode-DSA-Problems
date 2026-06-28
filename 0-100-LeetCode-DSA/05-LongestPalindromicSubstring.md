# <u>05. Longest Palindromic Substring</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/longest-palindromic-substring/

---

## 🧠 Intuition:
* 🔹 Convert the original string into a new format by inserting a special delimiter (`#`) between every character and adding boundary characters (`@` and `$`).

* 🔹 This transformation makes **both even-length and odd-length palindromes** behave the same, so only one expansion logic is needed.

* 🔹 Use **Manacher's Algorithm** to compute the palindrome radius centered at every position in the transformed string.

* 🔹 Maintain the current palindrome center and use its **mirror property** to reuse previously computed palindrome lengths, avoiding unnecessary comparisons.

* 🔹 Expand around the current center only when needed to find a longer palindrome.

* 🔹 Track the center with the maximum palindrome radius.

* 🔹 Convert the palindrome's position from the transformed string back to the original string indices.

* 🔹 Return the longest palindromic substring from the original string.

---

## ⏱ Time Complexity

**O(n)**

* Building the transformed string, running Manacher's algorithm, and finding the longest palindrome all take linear time.

---

## 📦 Space Complexity

**O(n)**
  
* Extra space is used for the transformed string and the palindrome radius (`p`) array.

---

## 💻 Java Code

```java
class Solution {
    public String longestPalindrome(String s) {
        String t = join('@' + s + '$', /*delimiter=*/'#');
        int[] p = manacher(t);
        int maxPalindromeLength = 0;
        int bestCenter = -1;

        for (int i = 0; i < p.length; ++i)
          if (p[i] > maxPalindromeLength) {
            maxPalindromeLength = p[i];
            bestCenter = i;
          }

        int l = (bestCenter - maxPalindromeLength) / 2;
        int r = (bestCenter + maxPalindromeLength) / 2;
        return s.substring(l, r);
    }

    private int[] manacher(final String t) {
      int[] p = new int[t.length()];
      int center = 0;
      for (int i = 1; i < t.length() - 1; ++i) {
        int rightBoundary = center + p[center];
        int mirrorIndex = center - (i - center);
        if (rightBoundary > i)
          p[i] = Math.min(rightBoundary - i, p[mirrorIndex]);
        while (i + 1 + p[i] < t.length() && i - 1 - p[i] >= 0 &&
               t.charAt(i + 1 + p[i]) == t.charAt(i - 1 - p[i]))
          ++p[i];
        if (i + p[i] > rightBoundary) {
          center = i;
        }
      }
      return p;
    }
    
    private String join(final String s, char delimiter) {
      StringBuilder joined = new StringBuilder();
      for (int i = 0; i < s.length() - 1; ++i) {
        joined.append(s.charAt(i));
        joined.append(delimiter);
      }
      joined.append(s.charAt(s.length() - 1));
      return joined.toString();
    }
}
```

---