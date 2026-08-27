# <u>3720. Lexicographically Smallest Permutation Greater Than Target</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/lexicographically-smallest-permutation-greater-than-target/

---

## 🧠 Intuition:
* 🔹 Count the frequency of each character in `s` so we know which characters are available to form a permutation.

* 🔹 First, determine how much of `target` can be matched using the available characters.

* 🔹 To obtain a permutation **strictly greater** than `target`, we need to find a position where we can choose a character **larger** than the corresponding character in `target`.

* 🔹 Start checking divergence positions from **right to left** so that the prefix remains as long as possible, producing the smallest possible greater permutation.

* 🔹 For each candidate position:
    - Rebuild the remaining character pool after using the prefix `target[0...i-1]`.
    - Find the **smallest available character greater than** `target[i]`.
    - Once found, place it at position `i`.
    - Append all remaining characters in ascending order to make the suffix as small as possible.

* 🔹 The first valid permutation found is the **lexicographically smallest permutation greater than `target`**.

* 🔹 If no position allows a greater character, return `""`.

---

## ⏱ Time Complexity

**O(n²)**

* Finding the maximum matching prefix takes `O(n)`.
* For each possible divergence position, the code clones the frequency array and reconstructs the remaining pool in `O(n)`.
* Finding the next greater character takes at most `O(26)`.
* Building the final answer takes `O(n)`.
    
---

## 📦 Space Complexity

**O(n)**

* `count` and `currentCount` use `O(26)` space.
* `pool` uses `O(26)` space.
* `StringBuilder` requires `O(n)` space for the resulting permutation.

---

## 💻 Java Code

```java
class Solution {
    public String lexGreaterPermutation(String s, String target) {
        int n = s.length();
        int[] count = new int[26];
        for (char c : s.toCharArray()) {
            count[c - 'a']++;
        }
        
        // Step 1: Find the maximum prefix length of target that s can perfectly match
        int maxPref = 0;
        int[] currentCount = count.clone();
        while (maxPref < n) {
            int idx = target.charAt(maxPref) - 'a';
            if (currentCount[idx] > 0) {
                currentCount[idx]--;
                maxPref++;
            } else {
                break;
            }
        }
        
        // Step 2: Search backwards for the optimal divergence index
        for (int i = n - 1; i >= 0; i--) {
            // If we can't even form the prefix up to i-1, skip this position
            if (i > maxPref) {
                continue;
            }
            
            // Reconstruct the remaining character pool after matching target[0...i-1]
            int[] pool = count.clone();
            for (int j = 0; j < i; j++) {
                pool[target.charAt(j) - 'a']--;
            }
            
            int targetCharIdx = target.charAt(i) - 'a';
            int chosenIdx = -1;
            
            // Find the smallest character strictly greater than target.charAt(i)
            for (int c = targetCharIdx + 1; c < 26; c++) {
                if (pool[c] > 0) {
                    chosenIdx = c;
                    break;
                }
            }
            
            // Step 3: If a valid replacement is found, build the answer immediately
            if (chosenIdx != -1) {
                StringBuilder sb = new StringBuilder();
                sb.append(target, 0, i);
                sb.append((char) ('a' + chosenIdx));
                pool[chosenIdx]--;
                
                // Collect and append the remaining letters in ascending order
                for (int c = 0; c < 26; c++) {
                    while (pool[c] > 0) {
                        sb.append((char) ('a' + c));
                        pool[c]--;
                    }
                }
                return sb.toString();
            }
        }
        
        return "";
    
    }
}
```

---