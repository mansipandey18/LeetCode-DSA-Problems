 # <u>2452. Words Within Two Edits of Dictionary</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/words-within-two-edits-of-dictionary/

---

## 🧠 Intuition:
* 🔹 For each word in queries, we need to check if it can match **any word in dictionary with at most 2 character differences**

* 🔹 Since all words have same length, compare characters **position by position**

* 🔹 For every `query`, iterate over each `dictionary` word and count how many positions differ

* 🔹 If the difference count becomes **less than 3 (i.e., ≤ 2 edits)** → it is a valid word

* 🔹 Add that query word to the result and **stop checking further dictionary words (early break)**

* 🔹 Repeat this process for all query words.

---

## ⏱ Time Complexity

**O(q × d × k)**

* Let : 
    - `q = queries.length`
    - `d = dictionary.length`
    - `k = length of each word`
    
---

## 📦 Space Complexity

**O(q)**

* Only result list used

---

## 💻 Java Code

```java
class Solution {
    public List<String> twoEditWords(String[] queries, String[] dictionary) {
        List<String> result = new ArrayList<>();
      
        int stringLength = queries[0].length();
      
        for (String queryString : queries) {
            for (String dictionaryWord : dictionary) {
                int differenceCount = 0;
              
                for (int i = 0; i < stringLength; ++i) {
                    if (queryString.charAt(i) != dictionaryWord.charAt(i)) {
                        differenceCount++;
                    }
                }
              
                if (differenceCount < 3) {
                    result.add(queryString);
                    break; // Found a match, no need to check other dictionary words
                }
            }
        }
      
        return result;
    }
}
```

---