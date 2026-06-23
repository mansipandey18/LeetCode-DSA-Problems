# <u>1189. Maximum Number of Balloons</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-number-of-balloons/

---

## 🧠 Intuition:
* 🔹 The word "balloon" requires specific characters: `b, a, l, l, o, o, n`, so we first count the frequency of every character in the given string.

* 🔹 Since the letters **'l'** and **'o'** appear twice in `"balloon"`, divide their frequencies by 2 to calculate how many complete pairs are available.

* 🔹 The maximum number of `"balloon"` words we can form depends on the character with the minimum available frequency among `b, a, l, o, n`.

* 🔹 Iterate through these required characters and find the smallest count, which represents the maximum number of complete `"balloon"` strings that can be formed.

* 🔹 This approach efficiently uses frequency counting instead of repeatedly checking and removing characters.
---

## ⏱ Time Complexity

**O(n)**

* We traverse the input string once to count character frequencies, and the remaining operations take constant time.
    
---

## 📦 Space Complexity

**O(1)**

* A fixed-size frequency array of 26 lowercase letters is used, regardless of the input size.

---

## 💻 Java Code

```java
class Solution {
    public int maxNumberOfBalloons(String text) {
        int[] charFrequency = new int[26];
      
        for (int i = 0; i < text.length(); i++) {
            charFrequency[text.charAt(i) - 'a']++;
        }
      
        charFrequency['l' - 'a'] /= 2;
        charFrequency['o' - 'a'] /= 2;
      
        int maxBalloons = Integer.MAX_VALUE;
      
        for (char c : "balon".toCharArray()) {
            maxBalloons = Math.min(maxBalloons, charFrequency[c - 'a']);
        }
      
        return maxBalloons;
    }
}
```

---