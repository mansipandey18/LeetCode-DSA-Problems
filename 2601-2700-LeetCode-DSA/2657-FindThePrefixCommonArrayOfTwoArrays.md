# <u>2657. Find the Prefix Common Array of Two Arrays</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/find-the-prefix-common-array-of-two-arrays/

---

## 🧠 Intuition:
* 🔹 We need to find, for every index `i`, how many elements are common in the prefixes:
    - `A[0...i]`
    - `B[0...i]`

* 🔹 Use two frequency arrays:
    - `frequencyA[value]` → count of `value` seen so far in `A`
    - `frequencyB[value]` → count of `value` seen so far in `B`

* 🔹 Traverse both arrays together:
    - Add current elements `A[i]` and `B[i]` into their respective frequency arrays.

* 🔹 For every possible value from `1` to `n`:
    - The common occurrences of that value in both prefixes are:
        * `min(frequencyA[value], frequencyB[value])`

* 🔹 Sum all these minimum frequencies to get the prefix common count for index `i`.

* 🔹 Store the result for each prefix in the `result` array.

* 🔹 This works because a value contributes to the common array only as many times as it appears in both prefixes.
---

## ⏱ Time Complexity

**O(n^2)**

* Outer loop runs `n` times.
* Inner loop checks all values from `1` to `n`.
    
---

## 📦 Space Complexity

**O(n)**

* Two frequency arrays and result array are used.

---

## 💻 Java Code

```java
class Solution {
    public int[] findThePrefixCommonArray(int[] A, int[] B) {
        int n = A.length;
        int[] result = new int[n];
      
        int[] frequencyA = new int[n + 1];  // Index 0 unused, elements are from 1 to n
        int[] frequencyB = new int[n + 1];  // Index 0 unused, elements are from 1 to n
      
        for (int i = 0; i < n; i++) {
            frequencyA[A[i]]++;
            frequencyB[B[i]]++;
          
            for (int value = 1; value <= n; value++) {
                result[i] += Math.min(frequencyA[value], frequencyB[value]);
            }
        }
      
        return result;
    }
}
```

---