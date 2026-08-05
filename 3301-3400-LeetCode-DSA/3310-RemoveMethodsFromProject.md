# <u>3310. Remove Methods From Project</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/remove-methods-from-project/

---

## 🧠 Intuition:
* 🔹 Represent the method invocations as a **directed graph**, where an edge `u → v` means method `u` invokes method `v`.

* 🔹 Start a BFS from the suspicious method `k` to mark all methods that are directly or indirectly reachable from it as **suspicious**.

* 🔹 After the BFS, every method is classified as either:
    - **Suspicious** (reachable from `k`), or
    - **Non-suspicious** (not reachable from `k`).

* 🔹 Check whether any **non-suspicious method invokes a suspicious method**.
    - If such an edge exists, the suspicious methods cannot be safely removed because they are still required by a non-suspicious method.
    - In this case, return **all methods**.

* 🔹 Otherwise, it is safe to remove all suspicious methods.

* 🔹 Return the list of only the **non-suspicious methods** that remain in the project.

---

## ⏱ Time Complexity

**O(n + m)**

* Where:
    - `n` = number of methods
    - `m` = number of invocations.
* **O(m)** to build the adjacency list.
* **O(n + m)** for the BFS traversal.
* **O(m)** to check for edges from non-suspicious to suspicious methods.
* **O(n)** to build the final answer.

---

## 📦 Space Complexity

**O(n + m)**

* **O(n + m)** for the adjacency list.
* **O(n)** for the suspicious array.
* **O(n)** for the BFS queue (worst case).
* **O(n)** for the result list.

---

## 💻 Java Code

```java
class Solution {
    public int subsequencePairCount(int[] nums) {
        int maxNum = Arrays.stream(nums).max().getAsInt();
        Integer[][][] mem = new Integer[nums.length][maxNum + 1][maxNum + 1];
        return subsequencePairCount(nums, 0, 0, 0, mem);
    }

    private static final int MOD = 1_000_000_007;

    private int subsequencePairCount(int[] nums, int i, int x, int y, Integer[][][] mem) {
        if (i == nums.length)
            return (x > 0 && x == y) ? 1 : 0;
        if (mem[i][x][y] != null)
            return mem[i][x][y];
        
        int skip = subsequencePairCount(nums, i + 1, x, y, mem);
        int take1 = subsequencePairCount(nums, i + 1, gcd(x, nums[i]), y, mem);
        int take2 = subsequencePairCount(nums, i + 1, x, gcd(y, nums[i]), mem);
        
        return mem[i][x][y] = (int) (((long) skip + take1 + take2) % MOD);
    }

    private int gcd(int a, int b) {
        return b == 0 ? a : gcd(b, a % b);
    }
}
```

---