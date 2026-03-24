# <u>14. Longest Common Prefix</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/longest-common-prefix/

---

## 🧠 Intuition:
* 🔹 We need to find the common starting characters shared by all strings.

* 🔹 First, sort the array of strings alphabetically.

* 🔹 After sorting:
    - Strings with similar prefixes come close together.
    - The minimum common prefix of the whole array will always exist between the first and last strings.

* 🔹 Take:
    - first = strs[0]
    - last = strs[strs.length - 1]

* 🔹 Compare characters of first and last one by one from the beginning.

* 🔹 Continue comparing while:
    - characters are equal, and
    - indices are within string length.

* 🔹 Stop when characters differ.

* 🔹 The matched part till that index is the longest common prefix for all strings.

* 🔹 Return the substring from index 0 to matched length.

---

## ⏱ Time Complexity

**O(n log n × m)**

* Sorting : 
    - Sorting n strings takes: O(n log n × m)
    
    - Where : 
        * `n` = number of strings
        * `m` = average string length (comparison cost)

* Comparing first & last string : O(m)

---

## 📦 Space Complexity

**O(log n)**

* Due to sorting recursion stack

* Where :
    - `n` = number of strings.

---

## 💻 Java Code

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        // Sort the array of strings
        Arrays.sort(strs);

        // Get the first and last strings after sorting
        String first = strs[0];
        String last = strs[strs.length - 1];
        int minLength = Math.min(first.length(), last.length());
        
        // Find the common prefix between the first 
      	// and last strings
      	int i = 0;
        while (i < minLength && first.charAt(i) == last.charAt(i)) {
            i++;
        }

        // Return the common prefix
        return first.substring(0, i);

    }
}
```

---