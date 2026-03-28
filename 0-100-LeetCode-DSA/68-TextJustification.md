# <u>68. Text Justification</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/text-justification/

---

## 🧠 Intuition:
* 🔹 We process the words line by line, always trying to fit the maximum number of words into the current line without exceeding `maxWidth`.

* 🔹 Starting from index `i`, we keep adding words and track their total character length until adding another word would break the width limit.

* 🔹 After selecting words for one line, we calculate how many gaps exist between words and how many spaces must be distributed to make the line exactly `maxWidth`.

* 🔹 If it is the last line or the line has only one word, we perform left justification by adding a single space between words and padding remaining spaces at the end.

* 🔹 Otherwise, we evenly distribute spaces across all gaps, giving extra spaces to the leftmost gaps when spaces are not perfectly divisible.

* 🔹The constructed line is added to the result, and we move to the next set of words until all words are processed.

---

## ⏱ Time Complexity

**O(n * L)**

* Let : 
    - `n` = number of words
    - `L` = maxWidth

* 1️⃣ Word grouping
    - Each word is visited once.
    - ✅ O(n)

* 2️⃣ Building each line
    Creating spaces and appending characters takes up to maxWidth.

---

## 📦 Space Complexity

**O(n * L)**

* Extra space used:
    - Result list storing justified lines.
    - StringBuilder for line creation.

---

## 💻 Java Code

```java
class Solution {
    public List<String> fullJustify(String[] words, int maxWidth) {
        List<String> result = new ArrayList<>();
        int i = 0;
        while (i < words.length) {
            int j = i, len = 0;
            while (j < words.length && len + words[j].length() + (j - i) <= maxWidth) {
                len += words[j].length();
                j++;
            }
            int gaps = j - i - 1;
            int spaces = maxWidth - len;
            StringBuilder line = new StringBuilder();

            if (j == words.length || gaps == 0) {
                for (int k = i; k < j; k++) {
                    line.append(words[k]);
                    if (k != j - 1) line.append(" ");
                }
                while (line.length() < maxWidth) line.append(" ");
            } else {
                int spaceEach = spaces / gaps, extra = spaces % gaps;
                for (int k = i; k < j; k++) {
                    line.append(words[k]);
                    if (k != j - 1) {
                        int toAdd = spaceEach + (extra-- > 0 ? 1 : 0);
                        line.append(" ".repeat(toAdd));
                    }
                }
            }
            result.add(line.toString());
            i = j;
        }
        return result;
    }
}
```

---