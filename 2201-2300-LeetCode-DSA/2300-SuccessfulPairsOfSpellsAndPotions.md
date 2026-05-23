# <u>2300. Successful Pairs of Spells and Potions</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/successful-pairs-of-spells-and-potions/

---

## 🧠 Intuition:
* 🔹 A pair is successful if:
    - `spells[i] * potions[j] >= success`

* 🔹 Sort the potions array so Binary Search can be applied efficiently.

* 🔹 For every spell, find the first potion that forms a successful pair.

* 🔹 Use Binary Search on the sorted potions array:
    - If `spell * potion[mid] >= success`, move left to find an even smaller valid index.
    - Otherwise, move right because current potion is too small.

* 🔹 After Binary Search ends, left points to the first successful potion index.

* 🔹 All potions from left to end will also form successful pairs because the array is sorted.

* 🔹 Count successful pairs using:
    - `potionsLength - left`

* 🔹 Store the count for each spell in the result array.

---

## ⏱ Time Complexity

**O(m log m + n log m)**

* `O(m log m)` for sorting potions
* `O(n log m)` for Binary Search on each spell

* where:
    - `n` = spells.length
    - `m` = potions.length

---

## 📦 Space Complexity

**O(1)**

* Ignoring the output array and sorting internal space

---

## 💻 Java Code

```java
class Solution {
    public int[] successfulPairs(int[] spells, int[] potions, long success) {
        Arrays.sort(potions);
      
        int spellsLength = spells.length;
        int potionsLength = potions.length;
      
        int[] result = new int[spellsLength];
      
        for (int i = 0; i < spellsLength; i++) {
            int left = 0;
            int right = potionsLength;
          
            while (left < right) {
                int mid = (left + right) >> 1;
              
                if ((long) spells[i] * potions[mid] >= success) {
                    right = mid;
                } else {
                    left = mid + 1;
                }
            }
          
            result[i] = potionsLength - left;
        }
      
        return result;
    }
}
```

---