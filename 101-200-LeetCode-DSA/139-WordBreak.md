# <u>139. Word Break</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/word-break/

---

## 🧠 Intuition:
* 🔹 Convert the dictionary into a **HashSet** so that word lookups are **O(1)**.

* 🔹 Use **recursion** to check whether the current string can be split into valid dictionary words.

* 🔹 If the entire current string is present in the dictionary, return `true`.

* 🔹 Otherwise, try every possible split of the string into:
    - **a prefix**, and
    - **a suffix**.

* 🔹 If the prefix is a valid dictionary word, recursively check whether the suffix can also be broken into valid words.

* 🔹 Use **memoization (HashMap)** to store the result (`true` or `false`) for every substring that has already been processed.

* 🔹 Before solving a substring, first check the memo map to avoid recomputing the same subproblem.

* 🔹 If any split successfully breaks the string, return `true`; otherwise, store `false` in the memo and return it.

---

## ⏱ Time Complexity

**O(n³)**

* There are **O(n)** unique substrings due to memoization, each substring tries up to **O(n)** split positions, and creating substrings takes **O(n)** time in Java.

---

## 📦 Space Complexity

**O(n²)**
  
* The memoization map stores results for up to **O(n)** substrings, and the stored substring keys require **O(n)** space each. The recursion stack adds up to **O(n)** extra space.

---

## 💻 Java Code

```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        return wordBreak(s, new HashSet<>(wordDict), new HashMap<>());
    }

    private boolean wordBreak(final String s, Set<String> wordSet, Map<String, Boolean> mem) {
        if (mem.containsKey(s))
            return mem.get(s);
        if (wordSet.contains(s)) {
            mem.put(s, true);
            return true;
        }

        for (int i = 1; i < s.length(); ++i) {
            String prefix = s.substring(0, i);
            String suffix = s.substring(i);

            if (wordSet.contains(prefix) && wordBreak(suffix, wordSet, mem)) {
                mem.put(s, true);
                return true;
            }
        }

        mem.put(s, false);
        return false;
    }
}
```

---