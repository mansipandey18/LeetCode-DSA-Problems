# <u>3518. Smallest Palindromic Rearrangement II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/smallest-palindromic-rearrangement-ii/

---

## 🧠 Intuition:
* 🔹 Count the frequency of every character in the string.

* 🔹 Since a palindrome is symmetric, only the left half needs to be constructed:
    - Store half of each character's frequency.
    - If a character has an odd frequency, keep it as the middle character.

* 🔹 Before building the answer, calculate the total number of distinct palindromic rearrangements.
    - If `k` is larger than the total possible rearrangements, return an empty string.

* 🔹 Construct the left half **greedily** from left to right:
    - Try placing each character (`'a'` to `'z'`) at the current position.
    - Temporarily decrease its count and compute how many valid permutations can be formed with the remaining characters.
    - If the number of permutations is at least k, fix this character at the current position.
    - Otherwise, skip all those permutations by subtracting their count from `k`, restore the character count, and try the next character.

* 🔹 Repeat until the left half is completely built.

* 🔹 Form the final palindrome by concatenating:
    - **Left half + middle character (if any) + reverse of the left half**.

* 🔹 This greedy approach guarantees the **k-th lexicographically smallest palindromic rearrangement**.

---

## ⏱ Time Complexity

**O(n²)**

* Where:
    - `n` = length of the string
    - `L = n / 2` (length of the left half)
    - Alphabet size = **26** (constant)
* Building the palindrome requires checking up to 26 characters for each of the `L` positions, and each check computes permutation counts using combinations.

---

## 📦 Space Complexity

**O(n)**

* For storing the left half, the final palindrome, and fixed-size frequency arrays.

---

## 💻 Java Code

```java
class Solution {
    public String smallestPalindrome(String s, int k) {
        // Step 1: Count total frequencies of each character
        int[] globalCounts = new int[26];
        for (char c : s.toCharArray()) {
            globalCounts[c - 'a']++;
        }

        // Step 2: Extract available characters for the left half and find the middle character
        int[] leftCounts = new int[26];
        String midChar = "";
        int leftLength = 0;

        for (int i = 0; i < 26; i++) {
            if (globalCounts[i] % 2 != 0) {
                midChar = Character.toString((char) (i + 'a'));
            }
            leftCounts[i] = globalCounts[i] / 2;
            leftLength += leftCounts[i];
        }

        // Step 3: Verify if k is within the maximum possible unique arrangements
        if (countPermutations(leftCounts, leftLength, k) < k) {
            return "";
        }

        // Step 4: Construct the left half character-by-character greedily
        StringBuilder leftHalf = new StringBuilder();
        long currentK = k;

        for (int pos = 0; pos < leftLength; pos++) {
            for (int i = 0; i < 26; i++) {
                if (leftCounts[i] > 0) {
                    // Try locking in character 'i' at this position
                    leftCounts[i]--;
                    int remainingLength = leftLength - 1 - pos;

                    // Calculate how many permutations can be formed with the remaining pool
                    long validPermutations = countPermutations(leftCounts, remainingLength, currentK);

                    if (currentK <= validPermutations) {
                        // The k-th permutation starts with this character
                        leftHalf.append((char) (i + 'a'));
                        break; 
                    } else {
                        // Skip this character block and decrease our k target
                        currentK -= validPermutations;
                        leftCounts[i]++; // Backtrack to try the next alphabet letter
                    }
                }
            }
        }

        // Step 5: Mirror the string to produce the final palindrome
        String leftSide = leftHalf.toString();
        String rightSide = new StringBuilder(leftSide).reverse().toString();

        return leftSide + midChar + rightSide;

    }

    private long countPermutations(int[] counts, int totalLength, long maxLimit) {
        if (totalLength == 0) {
            return 1;
        }
        
        long totalPermutations = 1;
        int remainingSlots = totalLength;

        for (int count : counts) {
            if (count > 0) {
                totalPermutations = multiplyAndCap(totalPermutations, nCr(remainingSlots, count), maxLimit);
                remainingSlots -= count;
                if (totalPermutations >= maxLimit) {
                    return maxLimit; // Break early if it meets or exceeds our target k
                }
            }
        }
        return totalPermutations;
    }

    // Standard nCr combination function capped at limit
    private long nCr(int n, int r) {
        if (r > n) return 0;
        if (r == 0 || r == n) return 1;
        if (r > n / 2) r = n - r; // Optimize calculations using symmetry

        long result = 1;
        for (int i = 1; i <= r; i++) {
            result = result * (n - i + 1) / i;
        }
        return result;
    }

    // Utility function to multiply two variables without risking overflow past maxLimit
    private long multiplyAndCap(long a, long b, long limit) {
        if (a == 0 || b == 0) return 0;
        if (a > limit / b) return limit;
        return a * b;
    }
}
```

---