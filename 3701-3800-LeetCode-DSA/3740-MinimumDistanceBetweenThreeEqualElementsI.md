# <u>3740. Minimum Distance Between Three Equal Elements I</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/minimum-distance-between-three-equal-elements-i/

---

## 🧠 Intuition:
* 🔹 The goal is to find **minimum distance between three equal elements** in the array.

* 🔹 First, group indices of each number using a `HashMap`:
    - `Key` → element value
    - `Value` → list of all indices where it appears

* 🔹 For any number to form a valid triplet, it must appear **at least 3 times**.

* 🔹 For each list of indices:
    - Instead of checking all triplets (which is costly), observe:
        * The **minimum distance** will always come from **closest three consecutive occurrences**.

* 🔹 So, iterate through indices in the list:
    - Pick three consecutive positions:
        * `i = ls[h]` (first occurrence)
        * `k = ls[h+2]` (third occurrence)

    - Distance is:
        `(k - i) * 2`

* 🔹 Update the minimum answer across all such triplets.

* 🔹 If no valid triplet exists (i.e., no element appears ≥ 3 times), return -1.

---

## ⏱ Time Complexity

**O(n)**

* Let : 
    - `n` = length of array

* **Step 1: Building map**
    - Traverse array once → **O(n)**

* **Step 2: Processing lists**
    - Each index is visited at most once across all lists.

---

## 📦 Space Complexity

**O(n)**

* HashMap stores indices of elements.
* In worst case (all elements same or all unique), total stored indices = `n`.


---

## 💻 Java Code

```java
class Solution {
    public int minimumDistance(int[] nums) {
        int n = nums.length;
        Map<Integer, List<Integer>> g = new HashMap<>();
        for (int i = 0; i < n; ++i) {
            g.computeIfAbsent(nums[i], k -> new ArrayList<>()).add(i);
        }
        final int inf = 1 << 30;
        int ans = inf;
        for (var ls : g.values()) {
            int m = ls.size();
            for (int h = 0; h < m - 2; ++h) {
                int i = ls.get(h);
                int k = ls.get(h + 2);
                int t = (k - i) * 2;
                ans = Math.min(ans, t);
            }
        }
        return ans == inf ? -1 : ans;
    }
}

```

---