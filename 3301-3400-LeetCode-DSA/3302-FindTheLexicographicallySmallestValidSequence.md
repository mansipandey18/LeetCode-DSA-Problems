# <u>3302. Find the Lexicographically Smallest Valid Sequence</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/find-the-lexicographically-smallest-valid-sequence/

---

## 🧠 Intuition:
* 🔹 We need to choose indices from `word1` that form `word2` as a subsequence, with **at most one character allowed to be different**.

* 🔹 First, scan `word1` from **right to left** to build the `last` array.
    - `last[j]` stores the latest index in `word1` from which `word2[j]` can be matched.
    - This helps us quickly check whether the remaining part of `word2` can still be formed after using a different character.

* 🔹 Then scan `word1` from left to right to construct the answer greedily.

* 🔹 If the current character matches `word2[j]`, select its index immediately because choosing the earliest possible index helps produce the **lexicographically smallest sequence of indices**.

* 🔹 If the characters do not match, we can use our **one allowed mismatch**.

* 🔹 Before using the mismatch at index `i`, check:
    - Either this is the last character of `word2`, or
    - `i < last[j + 1]`, meaning there is still enough room in `word1` to match all remaining characters of `word2`.

* 🔹 Once the mismatch is used, set `canSkip = false` so no other mismatch is allowed.

* 🔹 Continue matching the remaining characters normally.

* 🔹 If all characters of `word2` are successfully selected, return the indices; otherwise, return an empty array.

* 🔹 The combination of **right-to-left feasibility checking + left-to-right greedy selection** ensures the resulting sequence is the lexicographically smallest valid one.

---

## ⏱ Time Complexity

**O(n + m)**

* Where:
    - `n = word1.length()` 
    - `m = word2.length()` 
* One backward scan builds `last`, and one forward scan constructs the answer.

---

## 📦 Space Complexity

**O(m)**

* last array: **O(m)**
* ans array: **O(m)**
* Other variables use **O(1)** space.

---

## 💻 Java Code

```java
class Solution {
    public int[] validSequence(String word1, String word2) {
        int[] ans = new int[word2.length()];
        // last[j] := the index i of the last occurrence in word1, where
        // word1[i] == word2[j]
        int[] last = new int[word2.length()];
        Arrays.fill(last, -1);

        int i = word1.length() - 1;
        int j = word2.length() - 1;
        while (i >= 0 && j >= 0) {
            if (word1.charAt(i) == word2.charAt(j))
                last[j--] = i;
            --i;
        }

        boolean canSkip = true;
        j = 0;
        for (i = 0; i < word1.length(); ++i) {
            if (j == word2.length())
                break;
            if (word1.charAt(i) == word2.charAt(j)) {
                ans[j++] = i;
            } else if (canSkip && (j == word2.length() - 1 || i < last[j + 1])) {
                canSkip = false;
                ans[j++] = i;
            }
        }

        return j == word2.length() ? ans : new int[0];

    }
}
```

---