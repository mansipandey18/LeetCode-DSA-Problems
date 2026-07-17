# <u>3312. Sorted GCD Pair Queries</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/sorted-gcd-pair-queries/

---

## 🧠 Intuition:
* 🔹 First, count the **frequency of every number** in the array.

* 🔹 For every possible GCD value (from largest to smallest), count how many array elements are **multiples** of that GCD.

* 🔹 If `count` numbers are divisible by the current GCD**, they can form `count × (count - 1) / 2` pairs.

* 🔹 Some of these pairs may actually have a **larger GCD, so subtract the pair counts that have already been assigned to multiples of the current GCD (Inclusion-Exclusion principle).

* 🔹 After this process, `gcdPairCount[g]` stores the **exact number of pairs whose GCD is** `g`.

* 🔹 Convert `gcdPairCount` into a **prefix sum array**, where each index stores the cumulative number of pairs with GCD up to that value.

* 🔹 For each query, use **Binary Search** on the prefix sum array to find the smallest GCD whose cumulative pair count is greater than the query index.

* 🔹 This efficiently returns the GCD corresponding to each query in the sorted list of all pair GCDs.

---

## ⏱ Time Complexity

**O(M log M + Q log M)**

* Where:
    - `M` = maximum value in `nums`
    - `Q` = number of queries

* The sieve-like counting takes `O(M log M)`, and each query is answered in `O(log M)` using binary search.

---

## 📦 Space Complexity

**O(log M)**

* for the frequency array and GCD pair count array.

---

## 💻 Java Code

```java
class Solution {
    public int[] gcdValues(int[] nums, long[] queries) {
        int maxValue = Arrays.stream(nums).max().getAsInt();

        int[] frequency = new int[maxValue + 1];
        for (int num : nums) {
            frequency[num]++;
        }

        long[] gcdPairCount = new long[maxValue + 1];

        for (int gcd = maxValue; gcd > 0; gcd--) {
            int multiplesCount = 0;
            for (int multiple = gcd; multiple <= maxValue; multiple += gcd) {
                multiplesCount += frequency[multiple];
                gcdPairCount[gcd] -= gcdPairCount[multiple];
            }
            gcdPairCount[gcd] += (long) multiplesCount * (multiplesCount - 1) / 2;
        }

        for (int i = 2; i <= maxValue; i++) {
            gcdPairCount[i] += gcdPairCount[i - 1];
        }

        int queryCount = queries.length;
        int[] result = new int[queryCount];
        for (int i = 0; i < queryCount; i++) {
            result[i] = search(gcdPairCount, queries[i]);
        }

        return result;
    }

    private int search(long[] cumulativeCounts, long target) {
        int left = 0;
        int right = cumulativeCounts.length - 1;
        int firstTrueIndex = cumulativeCounts.length;  // Default: not found

        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (cumulativeCounts[mid] > target) {
                firstTrueIndex = mid;
                right = mid - 1;  // Found one, look for earlier
            } else {
                left = mid + 1;
            }
        }

        return firstTrueIndex;
    }
}
```

---