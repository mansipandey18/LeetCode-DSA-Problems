# <u>1657. Determine if Two Strings Are Close</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/determine-if-two-strings-are-close/

---

## 🧠 Intuition:
* 🔹 Two strings are **close** if we can transform one into the other using operations like swapping characters or changing frequencies

* 🔹 First, count frequency of each character for both strings using arrays of size 26

* 🔹 Check if both strings have the **same set of unique characters**
    - If a character exists in one string but not in the other → impossible → return `false`

* 🔹 Now, **sort both frequency arrays**

* 🔹 If **sorted frequencies are equal** → it means we can `rearrange frequencies to match using allowed operations`

* 🔹 If **not equal** → `transformation is not possible`


---

## ⏱ Time Complexity

**O(n)**

* Counting frequencies → **O(n)**
* Sorting arrays of size 26 → **O(1)** (constant time)
    
---

## 📦 Space Complexity

**O(1)**

* Two frequency arrays of size 26.

---

## 💻 Java Code

```java
class Solution {
    public boolean closeStrings(String word1, String word2) {
        int[] frequencyArray1 = new int[26];
        int[] frequencyArray2 = new int[26];
      
        // Count character frequencies in word1
        for (int i = 0; i < word1.length(); i++) {
            frequencyArray1[word1.charAt(i) - 'a']++;
        }
      
        // Count character frequencies in word2
        for (int i = 0; i < word2.length(); i++) {
            frequencyArray2[word2.charAt(i) - 'a']++;
        }
      
        for (int i = 0; i < 26; i++) {
            if ((frequencyArray1[i] == 0) != (frequencyArray2[i] == 0)) {
                return false;
            }
        }
      
        Arrays.sort(frequencyArray1);
        Arrays.sort(frequencyArray2);
      
        return Arrays.equals(frequencyArray1, frequencyArray2);
    
    }
}
```

---