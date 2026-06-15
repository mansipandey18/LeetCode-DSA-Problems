# <u>77. Combinations</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/combinations/

---

## 🧠 Intuition:
* 🔹 We need to generate all possible combinations of **k numbers from 1 to n**.

* 🔹 Use **Backtracking (DFS)** to build combinations step by step.

* 🔹 Maintain a `path` list that stores the current combination being formed.

* 🔹 If `path.size() == k`, we have found a valid combination:
    - Add a copy of `path` to the answer list.
    - Return to explore other possibilities.

* 🔹 Start choosing numbers from `s` (starting index) to `n`.

* 🔹 For each number:
    - Add it to the current combination.
    - Recursively build the remaining combination using the next number `(i + 1)` as the new start.
    - Remove the last added number **(backtrack)** to try other choices.

* 🔹 Using `i + 1` ensures:
    - Numbers are chosen in increasing order.
    - Duplicate combinations are avoided.

* 🔹 This systematically explores all possible ways to choose `k` numbers from `1...n`.

---

## ⏱ Time Complexity

**O(C(n, k) × k)**

* Total number of valid combinations = **C(n, k)**.
* Each combination takes **O(k)** time to copy into the answer list.

---

## 📦 Space Complexity

**O(C(n, k) × k)**

* Recursion depth can go up to **k**.
* Current path stores at most **k** elements.

* **Auxiliary Space Complexity: O(k)**

* Where:
    - **C(n, k)** is the number of combinations of choosing **k** elements from **n**.

---

## 💻 Java Code

```java
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> ans = new ArrayList<>();
        dfs(n, k, 1, new ArrayList<>(), ans);
        return ans;
    }
    
    private void dfs(int n, int k, int s, List<Integer> path, List<List<Integer>> ans) {
        if (path.size() == k) {
          ans.add(new ArrayList<>(path));
          return;
        }

        for (int i = s; i <= n; ++i) {
          path.add(i);
          dfs(n, k, i + 1, path, ans);
          path.remove(path.size() - 1);
        }
    }
}
```

---