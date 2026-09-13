# <u>835. Image Overlap</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/image-overlap/

---

## 🧠 Intuition:
* 🔹 Treat every `1` in `img1` and every `1` in `img2` as a possible pair that can overlap after shifting one image.

* 🔹 For each pair of `1`s, calculate the **translation vector:**
    - `(row1 - row2, col1 - col2)`

* 🔹 The same translation vector means that these pixels will overlap when the images are shifted by that amount.

* 🔹 Store the frequency of each translation vector in a `HashMap`.

* 🔹 Every time a translation occurs, increase its count and update `maxOverlap`.

* 🔹 The translation with the **highest frequency** represents the shift that produces the maximum number of overlapping `1`s.

* 🔹 Therefore, `maxOverlap` is the required maximum overlap.

---

## ⏱ Time Complexity

**O(n⁴)**

* There are `n²` positions in each image.
* In the worst case, all cells contain `1`, so every `1` in `img1` is paired with every `1` in `img2`.

    
---

## 📦 Space Complexity

**O(n²)**

* The `HashMap` stores translation vectors.
* There can be at most `O(n²)` distinct translation vectors.

---

## 💻 Java Code

```java
class Solution {
    public int largestOverlap(int[][] img1, int[][] img2) {
        int n = img1.length;
        Map<List<Integer>, Integer> translationCount = new HashMap<>();
        int maxOverlap = 0;
      
        for (int row1 = 0; row1 < n; row1++) {
            for (int col1 = 0; col1 < n; col1++) {
                if (img1[row1][col1] == 1) {
                    for (int row2 = 0; row2 < n; row2++) {
                        for (int col2 = 0; col2 < n; col2++) {
                            if (img2[row2][col2] == 1) {
                                List<Integer> translationVector = List.of(row1 - row2, col1 - col2);
                              
                                int currentCount = translationCount.merge(translationVector, 1, Integer::sum);
                                maxOverlap = Math.max(maxOverlap, currentCount);
                            }
                        }
                    }
                }
            }
        }
      
        return maxOverlap;
    }
}
```

---