# <u>2839. Check if Strings Can be Made Equal With Operations I
</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/check-if-strings-can-be-made-equal-with-operations-i/

---

## 🧠 Intuition:
* 🔹 We are allowed to swap characters **only within same parity positions**:
    - even indices ↔ even indices
    - odd indices ↔ odd indices

* 🔹 So, characters at **even positions** can rearrange only among even positions.

* 🔹 Similarly, **odd position characters** can rearrange only among odd positions.

* 🔹 Therefore, for both strings to become equal:
    - The **frequency of characters at even indices** must be the same in both strings.
    - The **frequency of characters at odd indices** must also be the same.

* 🔹 Use a `2 × 26` array:
    - Row `0` → counts for even indices.
    - Row `1` → counts for odd indices.

* 🔹 Traverse both strings together:
    - Increase count for `s1` character.
    - Decrease count for `s2` character.

* 🔹 After traversal:
    - If all counts become `0`, both strings have identical character distribution at even and odd positions.
    - Hence, we can rearrange using allowed swaps → return `true`
    
---

## ⏱ Time Complexity

**O(n)**

* Traversing strings once → O(n)
* Checking 26 characters → O(26) (constant)
    
---

## 📦 Space Complexity

**O(1)**

* Frequency array size = `2 × 26` (constant size)

---

## 💻 Java Code

```java
class Solution {
    public boolean canBeEqual(String s1, String s2) {
        int[][] characterCountDifference = new int[2][26];
      
        // Process each character position in both strings
        for (int position = 0; position < s1.length(); position++) {
            // Determine if position is even (0) or odd (1) using bitwise AND
            int parityIndex = position & 1;
          
            // Get the character index (0-25) for the current character in s1
            int s1CharIndex = s1.charAt(position) - 'a';
            // Increment count for this character at this parity position
            characterCountDifference[parityIndex][s1CharIndex]++;
          
            // Get the character index (0-25) for the current character in s2
            int s2CharIndex = s2.charAt(position) - 'a';
            // Decrement count for this character at this parity position
            characterCountDifference[parityIndex][s2CharIndex]--;
        }
      
        // Check if all character counts are balanced (equal to zero)
        // This means each parity position has the same characters in both strings
        for (int charIndex = 0; charIndex < 26; charIndex++) {
            // Check even position counts
            if (characterCountDifference[0][charIndex] != 0) {
                return false;
            }
            // Check odd position counts
            if (characterCountDifference[1][charIndex] != 0) {
                return false;
            }
        }
      
        // All character counts are balanced, strings can be made equal
        return true;
    }
}
```

---