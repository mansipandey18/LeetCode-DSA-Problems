# <u>1331. Rank Transform of an Array</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/rank-transform-of-an-array/

---

## 🧠 Intuition:
* 🔹 Treat each index as a starting point and try to find the maximum number of indices that can be visited.

* 🔹 Use DFS to explore all valid jumps from the current index.

* 🔹 From an index, we can jump
    - Left within distance 
    - Right within distance `d`

* 🔹 A jump is valid only if:
    - `arr[targetIndex] < arr[currentIndex]`

* 🔹 If a taller or equal-height element appears, stop searching further in that direction because jumps beyond it are not allowed.

* 🔹 For every valid jump, recursively calculate:
    - `1 + dfs(targetIndex)`

* 🔹 Keep track of the maximum reachable path length from the current index.

* 🔹 Use memoization to store already computed results and avoid repeated DFS calculations.

* 🔹 Try DFS from every index because the optimal path may start anywhere in the array.

* 🔹 Return the maximum path length among all starting positions.

---

## ⏱ Time Complexity

**O(n log n)**

* Sorting takes **O(n log n)**
* Removing duplicates takes **O(n)**
* Binary searching each element takes **O(n log n)** overall.
    
---

## 📦 Space Complexity

**O(n)**

* Extra space is used for the cloned sorted array and the result array.

---

## 💻 Java Code

```java
class Solution {
    public int[] arrayRankTransform(int[] arr) {
        int arrayLength = arr.length;
      
        int[] sortedArray = arr.clone();
        Arrays.sort(sortedArray);
      
        int uniqueCount = 0;
        for (int i = 0; i < arrayLength; ++i) {
            if (i == 0 || sortedArray[i] != sortedArray[i - 1]) {
                sortedArray[uniqueCount++] = sortedArray[i];
            }
        }
      
        int[] result = new int[arrayLength];
      
        for (int i = 0; i < arrayLength; ++i) {
            result[i] = Arrays.binarySearch(sortedArray, 0, uniqueCount, arr[i]) + 1;
        }
      
        return result;
    }
}
```

---