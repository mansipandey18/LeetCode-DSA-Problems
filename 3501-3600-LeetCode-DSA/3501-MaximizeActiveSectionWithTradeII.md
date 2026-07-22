# <u>3501. Maximize Active Section with Trade II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximize-active-section-with-trade-ii/

---

## 🧠 Intuition:
* 🔹 Count the total number of active sections (`1`s) in the string as the base answer.

* 🔹 Traverse the string once to identify every **continuous group of `0`s**, storing:
    - the starting index of each group,
    - its length,
    - and for every position, the index of the zero-group it belongs to.

* 🔹 For every pair of adjacent zero groups, precompute the value:
    - **length(group₁) + length(group₂)**,
which represents the gain if those two groups are merged by one trade.

* 🔹 Build a **Sparse Table** on these merged lengths so that the maximum merge value in any range of groups can be answered in **O(1)**.

* 🔹 For each query:
    - Determine the zero groups intersecting the left and right boundaries.
    - Handle partial zero groups at the query boundaries separately.
    - Use the Sparse Table to quickly find the best merge among all fully contained adjacent zero groups.
    - Also check boundary cases where a partial zero group can be merged with a neighboring full group.

* 🔹 The answer for each query is:
    - **total existing `1`s + maximum additional active sections obtainable from one valid trade**.

* 🔹 Using preprocessing avoids recomputing zero-group information for every query, making query processing very efficient.

---

## ⏱ Time Complexity

**O(n + g log g + q)**

* Where:
    - `n` = length of the string,
    - `g` = number of zero groups (`g ≤ n`),
    - `q` = number of queries.

* Preprocessing:
    - Build zero groups: **O(n)**
    - Compute adjacent merge lengths: **O(g)**, where `g` is the number of zero groups
    - Build Sparse Table: **O(g log g)**
* Each Query: **O(1)**

---

## 📦 Space Complexity

**O(g log g + n)**

* `O(n)` for zero-group information and mappings, and `O(g log g)` for the Sparse Table.

---

## 💻 Java Code

```java
class Group {
    public int start;
    public int length;

    public Group(int start, int length) {
        this.start = start;
        this.length = length;
    }
}

class SparseTable {
    public SparseTable(int[] nums) {
        n = nums.length;
        st = new int[bitLength(n) + 1][n + 1];

        System.arraycopy(nums, 0, st[0], 0, n);

        for (int i = 1; i <= st.length; ++i)
            for (int j = 0; j + (1 << i) <= n; ++j)
                st[i][j] = Math.max(st[i - 1][j], st[i - 1][j + (1 << (i - 1))]);
    }

    // Returns max(nums[l..r])
    public int query(int l, int r) {
        int i = bitLength(r - l + 1) - 1;
        return Math.max(st[i][l], st[i][r - (1 << i) + 1]);
    }

    private final int n;
    private final int[][] st;

    private int bitLength(int n) {
        return Integer.SIZE - Integer.numberOfLeadingZeros(n);
    }
}

class Solution {
    public List<Integer> maxActiveSectionsAfterTrade(String s, int[][] queries) {
        int n = s.length();
        int ones = (int) s.chars().filter(c -> c == '1').count();

        Pair<List<Group>, int[]> zeroGroupsInfo = getZeroGroups(s);
        
        List<Group> zeroGroups = zeroGroupsInfo.getKey();
        
        int[] zeroGroupIndex = zeroGroupsInfo.getValue();

        if (zeroGroups.isEmpty())
            return Collections.nCopies(queries.length, ones);

        SparseTable st = new SparseTable(getZeroMergeLengths(zeroGroups));

        List<Integer> ans = new ArrayList<>();

        for (int[] query : queries) {
            int l = query[0];
            int r = query[1];
            int left = zeroGroupIndex[l] == -1 ? -1
                    : (zeroGroups.get(zeroGroupIndex[l]).length -
                            (l - zeroGroups.get(zeroGroupIndex[l]).start));

            int right = zeroGroupIndex[r] == -1 ? -1 : (r - zeroGroups.get(zeroGroupIndex[r]).start + 1);

            Pair<Integer, Integer> adjacentIndices = mapToAdjacentGroupIndices(
                    zeroGroupIndex[l] + 1, s.charAt(r) == '1' ? zeroGroupIndex[r] : zeroGroupIndex[r] - 1);
            int startAdjacentGroupIndex = adjacentIndices.getKey();
            int endAdjacentGroupIndex = adjacentIndices.getValue();

            int activeSections = ones;
            if (s.charAt(l) == '0' && s.charAt(r) == '0' && zeroGroupIndex[l] + 1 == zeroGroupIndex[r])
                activeSections = Math.max(activeSections, ones + left + right);

            else if (startAdjacentGroupIndex <= endAdjacentGroupIndex)
                activeSections = Math.max(activeSections,
                        ones + st.query(startAdjacentGroupIndex, endAdjacentGroupIndex));
            if (s.charAt(l) == '0' &&
                    zeroGroupIndex[l] + 1 <= (s.charAt(r) == '1' ? zeroGroupIndex[r] : zeroGroupIndex[r] - 1))
                activeSections = Math.max(activeSections, ones + left + zeroGroups.get(zeroGroupIndex[l] + 1).length);
            if (s.charAt(r) == '0' && zeroGroupIndex[l] < zeroGroupIndex[r] - 1)
                activeSections = Math.max(activeSections, ones + right + zeroGroups.get(zeroGroupIndex[r] - 1).length);
            ans.add(activeSections);
        }

        return ans;
    }

    private Pair<List<Group>, int[]> getZeroGroups(String s) {
        List<Group> zeroGroups = new ArrayList<>();
        int[] zeroGroupIndex = new int[s.length()];

        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '0') {
                if (i > 0 && s.charAt(i - 1) == '0')
                    zeroGroups.get(zeroGroups.size() - 1).length++;
                else
                    zeroGroups.add(new Group(i, 1));
            }
            zeroGroupIndex[i] = zeroGroups.size() - 1;
        }

        return new Pair<>(zeroGroups, zeroGroupIndex);
    }

    private int[] getZeroMergeLengths(List<Group> zeroGroups) {
        final int[] zeroMergeLengths = new int[zeroGroups.size() - 1];
        for (int i = 0; i < zeroGroups.size() - 1; ++i)
            zeroMergeLengths[i] = zeroGroups.get(i).length + zeroGroups.get(i + 1).length;
        return zeroMergeLengths;
    }

    private Pair<Integer, Integer> mapToAdjacentGroupIndices(int startGroupIndex, int endGroupIndex) {
        return new Pair<>(startGroupIndex, endGroupIndex - 1);

    }
}
```

---