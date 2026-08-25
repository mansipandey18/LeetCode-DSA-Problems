# <u>3718. Smallest Missing Multiple of K</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/smallest-missing-multiple-of-k/

---

## 🧠 Intuition:
* 🔹 Store all elements of `nums` in a **HashSet** for fast `O(1)` average-time lookup.

* 🔹 The smallest positive multiple of `k` is `k`, so start checking from `multiple = k`.

* 🔹 If `k` exists in the set, move to the next multiple by adding `k`.

* 🔹 Continue checking `k, 2k, 3k, ...` until a multiple is not present in the array.

* 🔹 The first missing multiple found is the **smallest missing multiple of `k`**, so return it.

---

## ⏱ Time Complexity

**O(n + M/k)**

* Average-case HashSet lookup is `O(1)`.
    
---

## 📦 Space Complexity

**O(m)**

* The `HashSet` can store up to `n` distinct elements.

---

## 💻 Java Code

```java
class Solution {
    public int missingMultiple(int[] nums, int k) {
        Set<Integer> numSet = new HashSet<>();
        for (int num : nums) {
            numSet.add(num);
        }
        
        // Find the smallest missing multiple
        int multiple = k;
        while (numSet.contains(multiple)) {
            multiple += k;
        }
        
        return multiple;
    }
}
```

---