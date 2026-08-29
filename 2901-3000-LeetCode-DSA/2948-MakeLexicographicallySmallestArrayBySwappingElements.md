# <u>2948. Make Lexicographically Smallest Array by Swapping Elements</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/make-lexicographically-smallest-array-by-swapping-elements/

---

## 🧠 Intuition:
* 🔹 The key observation is that two elements can be swapped if their values differ by at most `limit`.

* 🔹 Sort the indices of `nums` according to their values. This brings similar values together.

* 🔹 While traversing the sorted indices, form a group whenever the difference between consecutive values is `<= limit`.

* 🔹 All elements inside the same group can be rearranged among their original positions through a sequence of valid swaps.

* 🔹 For each group:
    - Collect its original indices.
    - Sort these indices in ascending order.
    - The group’s values are already sorted because we traversed them by value.
    - Assign the smallest values to the smallest original indices.

* 🔹 This produces the lexicographically smallest arrangement possible for every connected group.

* 🔹 Finally, return the constructed `result` array.

---

## ⏱ Time Complexity

**O(n log n)**

* Creating the index array: `O(n)`
* Sorting indices by values: `O(n log n)`
* Sorting the indices inside all groups: `O(n log n)` in the worst case
* Assigning values to the result: `O(n)`
    
---

## 📦 Space Complexity

**O(n)**

* `indices` → `O(n)`
* `result` → `O(n)`
* Temporary groupIndices arrays → `O(n)` in the worst case

---

## 💻 Java Code

```java
class Solution {
    public int[] lexicographicallySmallestArray(int[] nums, int limit) {
        int n = nums.length;
      
        Integer[] indices = new Integer[n];
        Arrays.setAll(indices, i -> i);
      
        Arrays.sort(indices, (i, j) -> nums[i] - nums[j]);
      
        int[] result = new int[n];
      
        int i = 0;
        while (i < n) {
            int groupEnd = i + 1;
            while (groupEnd < n && nums[indices[groupEnd]] - nums[indices[groupEnd - 1]] <= limit) {
                groupEnd++;
            }
          
            Integer[] groupIndices = Arrays.copyOfRange(indices, i, groupEnd);
          
            Arrays.sort(groupIndices, (x, y) -> x - y);
          
            for (int k = i; k < groupEnd; k++) {
                result[groupIndices[k - i]] = nums[indices[k]];
            }
          
            i = groupEnd;
        }
      
        return result;
    }
}
```

---