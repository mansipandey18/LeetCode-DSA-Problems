# <u>1358. Number of Substrings Containing All Three Characters</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/number-of-substrings-containing-all-three-characters/

---

## 🧠 Intuition:
* 🔹 Keep track of the **last seen index** of `'a'`, `'b'`, and `'c'` while traversing the string.

* 🔹 At each position, update the last occurrence of the current character.

* 🔹 A valid substring exists only if **all three characters have been seen at least once**.

* 🔹 The **earliest (minimum) last occurrence** among `'a'`, `'b'`, and `'c'` determines the farthest left starting point that still includes all three characters.

* 🔹 Every starting index from `0` to `leftmostPosition` forms a valid substring ending at the current index.

* 🔹 Therefore, add `leftmostPosition + 1` to the answer at every step.

* 🔹 Continue this process for the entire string to count all valid substrings efficiently in a single pass.

---

## ⏱ Time Complexity

**O(n)**

* Where :
    - `n` = length of the string

* Each node is visited once
    
---

## 📦 Space Complexity

**O(1)**

* since only a fixed-size array of 3 elements is used

---

## 💻 Java Code

```java
class Solution {
    public int numberOfSubstrings(String s) {
        int[] lastPositions = new int[] {-1, -1, -1};
      
        int totalCount = 0;
      
        for (int currentIndex = 0; currentIndex < s.length(); currentIndex++) {
            char currentChar = s.charAt(currentIndex);
          
            lastPositions[currentChar - 'a'] = currentIndex;
          
            int leftmostPosition = Math.min(lastPositions[0], Math.min(lastPositions[1], lastPositions[2]));
          
            totalCount += leftmostPosition + 1;
        }
      
        return totalCount;
    }
}
```

---