# <u>3090. Maximum Length Substring With Two Occurrences</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-length-substring-with-two-occurrences/

---

## 🧠 Intuition:
* 🔹 Use the **Sliding Window** technique with two pointers, `left` and `right`.

* 🔹 Maintain a frequency array to keep track of how many times each character appears in the current window.

* 🔹 Expand the window by moving `right` and increment the frequency of the current character.

* 🔹 If any character appears **more than 2 times**, the window becomes invalid.

* 🔹 Move `left` forward and decrease the frequency of characters until the current character appears at most **2 times** again.

* 🔹 Once the window is valid, calculate its length using `right - left + 1`.

* 🔹 Keep updating `maxLength` with the largest valid window found.

* 🔹 Since both pointers only move forward, every character is processed at most a few times.

---

## ⏱ Time Complexity

**O(n)**

* `right` and `left` each traverse the string at most once.

---

## 📦 Space Complexity

**O(1)**

* The frequency array has a fixed size of 26.

---

## 💻 Java Code

```java
class Solution {
    public int maximumLengthSubstring(String s) {
        int[] charFrequency = new int[26];
        int maxLength = 0;
      
        // Use sliding window technique with two pointers
        int left = 0;
        for (int right = 0; right < s.length(); right++) {
            // Get the index of current character (0-25 for a-z)
            int currentCharIndex = s.charAt(right) - 'a';
          
            // Increment frequency of current character
            charFrequency[currentCharIndex]++;
          
            // If any character appears more than 2 times, shrink window from left
            while (charFrequency[currentCharIndex] > 2) {
                int leftCharIndex = s.charAt(left) - 'a';
                charFrequency[leftCharIndex]--;
                left++;
            }
          
            // Update maximum length found so far
            // Window size is (right - left + 1)
            maxLength = Math.max(maxLength, right - left + 1);
        }
      
        return maxLength;
    }
}
```

---