# <u>3016. Minimum Number of Pushes to Type Word II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/minimum-number-of-pushes-to-type-word-ii/

---

## 🧠 Intuition:
* 🔹 Count the frequency of each character in the word.

* 🔹 Since frequently used characters should require fewer key presses, sort the character frequencies.

* 🔹 Process the frequencies from **highest to lowest**.

* 🔹 Assign the **8 most frequent characters** to positions requiring **1 push**.

* 🔹 Assign the **next 8 most frequent characters** to positions requiring **2 pushes**, then the next group to **3 pushes**, and so on.

* 🔹 For each character, multiply its frequency by the number of pushes required for its assigned position.

* 🔹 Sum these values to obtain the minimum total number of key presses.

* 🔹 This greedy assignment ensures that the most frequently used letters contribute the least possible cost.

---

## ⏱ Time Complexity

**O(n + 26 log 26)**

* Where : 
    - `n` = length of the word.

* Counting frequencies: `O(n)`
* Sorting the 26 frequency values: `O(26 log 26)` (constant)
* Processing the frequencies: `O(26)`

---

## 📦 Space Complexity

**O(1)**

* Uses a fixed-size frequency array of 26 elements, independent of the input size.

---

## 💻 Java Code

```java
class Solution {
    public int minimumPushes(String word) {
        int[] letterFrequency = new int[26];
      
        for (int i = 0; i < word.length(); i++) {
            letterFrequency[word.charAt(i) - 'a']++;
        }
      
        Arrays.sort(letterFrequency);
      
        int totalPushes = 0;
      
        for (int i = 0; i < 26; i++) {
            int pushesPerLetter = (i / 8) + 1;
            int frequency = letterFrequency[26 - i - 1];
            totalPushes += pushesPerLetter * frequency;
        }
      
        return totalPushes;
    }
}
```

---