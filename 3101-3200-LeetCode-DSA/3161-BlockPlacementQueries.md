# <u>3161. Block Placement Queries</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/block-placement-queries/

---

## 🧠 Intuition:
* 🔹 The key idea is to process queries in **reverse order**, turning obstacle insertions into obstacle removals, which is easier to handle dynamically.

* 🔹 Store all obstacle positions in a **TreeSet** so we can quickly find the nearest obstacle on the left and right of any position.

* 🔹 Initially, insert all obstacles from type-1 queries and add sentinel boundaries (`0` and `n`).

* 🔹 Build intervals between consecutive obstacles and store their maximum gap information in a **Fenwick Tree (BIT)**.

* 🔹 The Fenwick Tree is modified to maintain the **maximum segment length** instead of sums.

* 🔹 While traversing queries backward:
    - **Type 1 (Obstacle Insertion in forward direction)** → becomes obstacle removal. Merge adjacent segments and update the maximum available gap in the Fenwick Tree.
    - **Type 2 (Block Placement Query)** → find the nearest obstacle before position `x`.

* 🔹 A block of size `sz` can be placed if:
    - There exists a previous gap with length at least `sz` (`tree.get(prev) >= sz`), or
    - The current segment ending at x has enough free space (`x - prev >= sz`).

* 🔹 Store answers while processing backward and reverse them at the end to match the original query order.

* 🔹 Combining **TreeSet** (for obstacle neighbors) and **Fenwick Tree** (for maximum gap queries) allows efficient handling of dynamic interval updates.

---

## ⏱ Time Complexity

**O(Q log Q)**

* Each query performs TreeSet and Fenwick Tree operations, both taking `O(log Q)` time.

---

## 📦 Space Complexity

**O(Q)**

* TreeSet, Fenwick Tree, and answer list together require linear extra space.

---

## 💻 Java Code

```java
class FenwickTree {
    public FenwickTree(int n) {
        vals = new int[n + 1];
    }

    public void add(int i, int val) {
        while (i < vals.length) {
            vals[i] = Math.max(vals[i], val);
            i += lowbit(i);
        }
    }

    public int get(int i) {
        int res = 0;
        while (i > 0) {
            res = Math.max(res, vals[i]);
            i -= lowbit(i);
        }
        return res;
    }

    private int[] vals;

    private static int lowbit(int i) {
        return i & -i;
    }
}

class Solution {
    public List<Boolean> getResults(int[][] queries) {
        final int n = Math.min(50000, queries.length * 3);
        List<Boolean> ans = new ArrayList<>();
        FenwickTree tree = new FenwickTree(n + 1);
        TreeSet<Integer> obstacles = new TreeSet<>(Arrays.asList(0, n)); // sentinel values

        for (int[] query : queries) {
            final int type = query[0];
            if (type == 1) {
                final int x = query[1];
                obstacles.add(x);
            }
        }

        Iterator<Integer> it = obstacles.iterator();
        int x1 = it.next();
        while (it.hasNext()) {
            final int x2 = it.next();
            tree.add(x2, x2 - x1);
            x1 = x2;
        }

        for (int i = queries.length - 1; i >= 0; --i) {
            final int type = queries[i][0];
            final int x = queries[i][1];
            if (type == 1) {
                final Integer next = obstacles.higher(x);
                final Integer prev = obstacles.lower(x);
                if (next != null)
                    tree.add(next, next - prev);
                obstacles.remove(x);
            } else {
                final int sz = queries[i][2];
                final int prev = obstacles.floor(x);
                ans.add(tree.get(prev) >= sz || x - prev >= sz);
            }
        }

        Collections.reverse(ans);
        return ans;
    }
}
```

---