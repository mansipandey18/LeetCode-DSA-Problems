# <u>3043. Find the Length of the Longest Common Prefix</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/find-the-length-of-the-longest-common-prefix/

---

## 🧠 Intuition:
* 🔹 The problem asks for the **longest common digit prefix** between numbers from two arrays.

* 🔹 Convert every number in `arr1` into a string so prefixes can be handled easily.

* 🔹 Generate all possible prefixes of each number in `arr1` and store them in a `HashSet` for fast lookup.

* 🔹 Example: if number is 1234, store `"1"`, `"12"`, `"123"`, `"1234"`.

* 🔹 Now traverse every number in `arr2`.

* 🔹 Generate its prefixes one by one and check whether that prefix exists in the set.

* 🔹 If a prefix exists, update the maximum prefix length found so far.

* 🔹 Since `HashSet` lookup is `O(1)` on average, prefix checking becomes efficient.

* 🔹 Finally, return the maximum matching prefix length.

---

## ⏱ Time Complexity

**O((n + m) * d²)**

* Where:
    - `n = arr1.length`
    - `m = arr2.length`
    - `d = maximum number of digits in a number`

* Generating prefixes for both arrays takes `O((n + m) * d²)`
(`substring()` creation can take up to `O(d)` time).

---

## 📦 Space Complexity

**O(n * d)**

* for storing all prefixes of numbers from arr1 in the HashSet.

---

## 💻 Java Code

```java
class Solution {
    public int longestCommonPrefix(int[] arr1, int[] arr2) {
        Set<String> prefixSet = new HashSet<>();
        int maxLength = 0;

        // Store all prefixes of numbers in arr1
        for (int num : arr1) {
            String numStr = String.valueOf(num);
            for (int i = 1; i <= numStr.length(); i++) {
                prefixSet.add(numStr.substring(0, i));
            }
        }

        // Check prefixes of numbers in arr2 against the prefixSet
        for (int num : arr2) {
            String numStr = String.valueOf(num);
            for (int i = 1; i <= numStr.length(); i++) {
                String prefix = numStr.substring(0, i);
                if (prefixSet.contains(prefix)) {
                    maxLength = Math.max(maxLength, i);
                }
            }
        }

        return maxLength;
    }
}
```

---