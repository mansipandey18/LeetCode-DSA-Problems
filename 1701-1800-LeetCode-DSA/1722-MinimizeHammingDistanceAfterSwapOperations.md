# <u>1722. Minimize Hamming Distance After Swap Operations</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/minimize-hamming-distance-after-swap-operations/

---

## 🧠 Intuition:
* 🔹 We can swap elements only at indices given in `allowedSwaps`, so think of these indices as **connected components**

* 🔹 Use **Union-Find (DSU)** to group all indices that can reach each other through swaps

* 🔹 Within each component, we can **rearrange elements freely**, so we try to match `source` and `target` as much as possible inside each group

* 🔹 For every component, store the frequency of values from `source`

* 🔹 Then iterate over `target`:
    - For each index, find its component
    - Try to match `target[i]` with available values in that component’s frequency map
    - **If found**, `decrease frequency` (match successful)
    - **If not found** (frequency goes negative), it means mismatch → `increase Hamming distance`

* 🔹 Final answer = `total unmatched elements` (minimum Hamming distance)

---

## ⏱ Time Complexity

**O(n + m)**

* Union-Find operations (with path compression) → **O(n + m · α(n))**
    - `m = number of swaps`
    - `α(n) = inverse Ackermann (almost constant)`

* Building maps + checking → **O(n)**

---

## 📦 Space Complexity

**O(n)**

* Parent array + hashmap storage.

---

## 💻 Java Code

```java
class Solution {
    private int[] parent;

    public int minimumHammingDistance(int[] source, int[] target, int[][] allowedSwaps) {
        int n = source.length;
      
        parent = new int[n];
        for (int i = 0; i < n; i++) {
            parent[i] = i;
        }
      
        for (int[] swap : allowedSwaps) {
            int index1 = swap[0];
            int index2 = swap[1];
            parent[find(index1)] = find(index2);
        }
      
        Map<Integer, Map<Integer, Integer>> componentFrequency = new HashMap<>();
      
        for (int i = 0; i < n; i++) {
            int root = find(i);
            componentFrequency
                .computeIfAbsent(root, k -> new HashMap<>())
                .merge(source[i], 1, Integer::sum);
        }
      
        int hammingDistance = 0;
      
        for (int i = 0; i < n; i++) {
            int root = find(i);
            Map<Integer, Integer> frequencyMap = componentFrequency.get(root);
          
            if (frequencyMap.merge(target[i], -1, Integer::sum) < 0) {
                hammingDistance++;
            }
        }
      
        return hammingDistance;
    }

    // Find operation with path compression for Union-Find
    private int find(int x) {
        if (parent[x] != x) {
            parent[x] = find(parent[x]);
        }
        return parent[x];
    }
}
```

---