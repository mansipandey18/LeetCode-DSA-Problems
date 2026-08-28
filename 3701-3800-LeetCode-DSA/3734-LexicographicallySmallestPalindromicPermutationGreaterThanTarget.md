# <u>3734. Lexicographically Smallest Palindromic Permutation Greater Than Target</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/lexicographically-smallest-palindromic-permutation-greater-than-target/

---

## 🧠 Intuition:
* 🔹 Count the frequency of each character in `s` and check whether its characters can form a palindrome.

* 🔹 A valid palindrome can have **at most one character with an odd frequency**:
    - If `n` is even → all frequencies must be even.
    - If `n` is odd → exactly one frequency must be odd, and that character becomes the middle character.

* 🔹 Remove the middle character (when `n` is odd) and divide every remaining frequency by `2` to obtain the characters needed for the **left half**.

* 🔹 The entire palindrome is determined by its left half because the right half is simply its reverse.

* 🔹 Use **backtracking** to construct the left half while maintaining the character counts.

* 🔹 At every position:
    - If the prefix is already greater than `target`, try characters from `'a'` onward.
    - Otherwise, start from `target[i]` to avoid creating a prefix smaller than the target.

* 🔹 Characters are tried in **ascending order**, so the first valid palindrome found is the **lexicographically smallest** one.

* 🔹 `isGreater` tracks whether the current prefix has already become greater than the corresponding prefix of `target`.

* 🔹 Once the left half is complete, construct the complete palindrome by:
    - Left half
    - Middle character (if present)
    - Reverse of the left half

* 🔹 Compare the constructed palindrome with `target`; if it is strictly greater, return it.

* 🔹 If no valid arrangement produces a palindrome greater than `target`, return `""`.

---

## ⏱ Time Complexity

**O(n × 26^(n/2))**

* Let:
    - `h = n/2`
* In the worst case, backtracking can explore up to `26^h` possible arrangements.
* At each complete arrangement, constructing and comparing the palindrome takes `O(n)`.
* Each recursion level also tries up to 26 characters.
    
---

## 📦 Space Complexity

**O(n)**

* `halfCounts[26]` → `O(26)`
* `ans` → `O(n)`
* Recursion depth → `O(n/2)`
* Constructed palindrome using StringBuilder → `O(n)`

---

## 💻 Java Code

```java
class Solution {
    private int n;
    private int[] halfCounts;
    private char midChar;
    private char[] ans;
    private String targetStr;
    private String result;

    public String lexPalindromicPermutation(String s, String target) {
        this.n = s.length();
        this.targetStr = target;
        this.result = "";
        
        int[] counts = new int[26];
        for (char c : s.toCharArray()) {
            counts[c - 'a']++;
        }
        
        // Step 1: Validate palindrome feasibility (at most one odd frequency character)
        int oddCount = 0;
        int oddIndex = -1;
        for (int i = 0; i < 26; i++) {
            if (counts[i] % 2 != 0) {
                oddCount++;
                oddIndex = i;
            }
        }
        if (oddCount > 1 || (n % 2 == 0 && oddCount > 0) || (n % 2 != 0 && oddCount == 0)) {
            return "";
        }
        
        // Step 2: Separate out the middle character if the length is odd
        this.midChar = oddIndex != -1 ? (char) (oddIndex + 'a') : 0;
        if (midChar != 0) {
            counts[oddIndex]--;
        }
        
        // Step 3: Populate the pool of available characters for the first half
        this.halfCounts = new int[26];
        for (int i = 0; i < 26; i++) {
            this.halfCounts[i] = counts[i] / 2;
        }
        
        this.ans = new char[n / 2];
        
        // Step 4: Run backtracking to build the optimal left half
        if (backtrack(0, false)) {
            return result;
        }
        
        return "";
    }

    private boolean backtrack(int i, boolean isGreater) {
        if (i == n / 2) {
            // Reconstruct the full palindrome from the left half
            StringBuilder sb = new StringBuilder();
            sb.append(ans);
            if (midChar != 0) {
                sb.append(midChar);
            }
            for (int j = ans.length - 1; j >= 0; j--) {
                sb.append(ans[j]);
            }
            
            String fullPalindrome = sb.toString();
            // Ensure it is strictly greater than the target string
            if (fullPalindrome.compareTo(targetStr) > 0) {
                this.result = fullPalindrome;
                return true;
            }
            return false;
        }

        char startChar = isGreater ? 'a' : targetStr.charAt(i);

        for (char c = startChar; c <= 'z'; c++) {
            int idx = c - 'a';
            if (halfCounts[idx] > 0) {
                halfCounts[idx]--;
                ans[i] = c;

                // Move to next state; state is greater if c > target[i] or already greater
                boolean nextGreater = isGreater || (c > targetStr.charAt(i));
                
                if (backtrack(i + 1, nextGreater)) {
                    return true; // Stop immediately on finding the first valid match
                }

                // Backtrack
                halfCounts[idx]++;
            }
        }
        return false;
        
    }
}
```

---