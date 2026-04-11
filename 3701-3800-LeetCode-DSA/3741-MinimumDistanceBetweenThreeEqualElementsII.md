# <u>3741. Minimum Distance Between Three Equal Elements II
</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/minimum-distance-between-three-equal-elements-ii/

---

## 🧠 Intuition:
* 🔹 The task is to find the **minimum distance among any three equal elements**.

* 🔹 First, group all indices of each number using a `HashMap`:
    - `Key` → number
    - `Value` → list of indices where it appears

* 🔹 Only elements appearing **at least 3 times** can form a valid triplet.

* 🔹 For each list of indices:
    - Instead of checking all combinations (which is slow), observe:
        * The **closest triplet** will always be formed by **3 consecutive indices**.

* 🔹 So, iterate through each list:
    - Take indices:
        * `i` = `ls[h]` (first)
        * `k` = `ls[h+2]` (third)

* 🔹 Compute distance:
    - `(k - i) * 2`

* 🔹 Update the minimum distance across all such triplets.

* 🔹 If no valid triplet is found, return `-1`.

---

## ⏱ Time Complexity

**O(n)**

* Let : 
    - `n` = size of array.

* Building the map → `O(n)`
* Processing all index lists → each index visited once → `O(n)`
    
---

## 📦 Space Complexity

**O(n)**

* HashMap stores indices → worst case stores all elements.

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