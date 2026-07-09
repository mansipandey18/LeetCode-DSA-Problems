# <u>3532. Path Existence Queries in a Graph I</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/path-existence-queries-in-a-graph-i/

---

## 🧠 Intuition:
* 🔹 The array is already sorted, so neighboring elements determine whether a path can continue.

* 🔹 If the difference between two consecutive numbers is **greater than** `maxDiff`, they cannot belong to the same connected component.

* 🔹 Traverse the array once and assign a **component ID** to every index.

* 🔹 Whenever the gap between consecutive elements exceeds `maxDiff`, start a **new component** by increasing the component ID.

* 🔹 After preprocessing, every index knows which connected component it belongs to.

* 🔹 For each query, simply compare the component IDs of the source and target indices.

* 🔹 If both indices have the **same component ID**, a valid path exists; otherwise, it does not.

* 🔹 This converts each query into a simple **O(1)** lookup after a single preprocessing pass.

---

## ⏱ Time Complexity

**O(n + q)**

* One pass to assign component IDs and one pass to answer all `q` queries.
    
---

## 📦 Space Complexity

**O(n + q)**

* `O(n)` for the component ID array and `O(q)` for the output array.

---

## 💻 Java Code

```java
class Solution {
    public boolean[] pathExistenceQueries(int n, int[] nums, int maxDiff, int[][] queries) {
        int[] componentIds = new int[n];
        int currentComponentId = 0;

        for (int i = 1; i < n; ++i) {
            if (nums[i] - nums[i - 1] > maxDiff) {
                currentComponentId++;
            }
            componentIds[i] = currentComponentId;
        }

        int numberOfQueries = queries.length;
        boolean[] results = new boolean[numberOfQueries];

        for (int i = 0; i < numberOfQueries; ++i) {
            int sourceNode = queries[i][0];
            int targetNode = queries[i][1];

            results[i] = componentIds[sourceNode] == componentIds[targetNode];
        }

        return results;
    }
}
```

---