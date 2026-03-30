# <u>2840. Check if Strings Can be Made Equal With Operations II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/check-if-strings-can-be-made-equal-with-operations-ii/

---

## 🧠 Intuition:
* 🔹 The allowed operation lets us **swap characters only among same parity positions** (even index with even index, odd with odd).

* 🔹 So, characters at **even indices** can only rearrange within even positions, and **odd indices** within odd positions.

* 🔹 Therefore, to make both strings equal, the **frequency of characters at even positions must match**, and the same must be true for **odd positions**.

* 🔹 We create a `frequencyDiff` array:
    - row `0` → counts for even indices
    - row `1` → counts for odd indices

* 🔹 Traverse both strings together:
    - Increase count for characters from `s1`
    - Decrease count for characters from `s2`

* 🔹 If both strings have identical character distributions for even and odd positions, all counts will become `zero`.

* 🔹 Finally, check the frequency arrays:
    - If any value is not zero → strings cannot be made equal.
    - Otherwise → rearrangement using allowed swaps is possible.

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
    public boolean checkStrings(String s1, String s2) {
        int[][] frequencyDiff = new int[2][26];
      
        // Iterate through both strings simultaneously
        for (int i = 0; i < s1.length(); i++) {
            // Determine if current index is even (0) or odd (1)
            int parityIndex = i & 1;
          
            // Get character indices (0-25 for 'a'-'z')
            int charIndexS1 = s1.charAt(i) - 'a';
            int charIndexS2 = s2.charAt(i) - 'a';
          
            // Increment count for character from s1 at this parity position
            frequencyDiff[parityIndex][charIndexS1]++;
          
            // Decrement count for character from s2 at this parity position
            frequencyDiff[parityIndex][charIndexS2]--;
        }
      
        // Check if all frequency differences are zero
        // If zero, characters at even/odd positions match between strings
        for (int charIndex = 0; charIndex < 26; charIndex++) {
            // Check even position frequencies
            if (frequencyDiff[0][charIndex] != 0) {
                return false;
            }
            // Check odd position frequencies
            if (frequencyDiff[1][charIndex] != 0) {
                return false;
            }
        }
      
        // All frequency differences are zero, strings can be made equal
        return true;
    }
}
```

---