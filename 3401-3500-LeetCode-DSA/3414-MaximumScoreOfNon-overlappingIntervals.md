# <u>3414. Maximum Score of Non-overlapping Intervals</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-score-of-non-overlapping-intervals/

---

## 🧠 Intuition:
* 🔹 Convert each interval into an `Interval` object containing its **start, end, weight, and original index (`id`)**.

* 🔹 Sort all intervals by their **end time** so that compatible previous intervals can be found efficiently.

* 🔹 Use a DP table `dp[i][j]` where:
    - `i` = first `i` intervals considered.
    - `j` = maximum number of intervals allowed, from `0` to `4`.

* 🔹 For every interval, there are two choices:
    - **Exclude:** keep the best result from `dp[i-1][j]`.
    - **Include:** add the current interval's weight to the best compatible result from `dp[p][j-1]`.

* 🔹 Use **binary search** to find `p`, the number of intervals ending strictly before the current interval starts.

* 🔹 Each `State` stores both:
    - The **total weight**.
    - The selected interval IDs, so ties can be resolved lexicographically.

* 🔹 `isBetter()` first chooses the state with the **larger weight**. If weights are equal, it chooses the **lexicographically smaller list of IDs**.

* 🔹 Since the problem allows at most **4 intervals**, the DP only needs 5 states for the interval-count dimension.

* 🔹 Finally, `dp[n][4]` contains the maximum-weight valid selection of up to 4 non-overlapping intervals.

---

## ⏱ Time Complexity

**O(n²)**

* Creating intervals → `O(n)`
* Sorting intervals → `O(n log n)`
* Binary search for each interval → `O(n log n)`
* DP has `4` states per interval → effectively `O(n)`
* However, creating/sorting ID lists and `isBetter()` can take up to `O(n)` per state in the worst case.
---

## 📦 Space Complexity

***O(n)**

* Sorted interval array → `O(n)`
* `endTimes` → `O(n)`
* DP table contains `O(n)` states because the second dimension is fixed at 5.
* Each state may store a list of up to 4 IDs → `O(n)` total DP storage.

---

## 💻 Java Code

```java
class Solution {
    private static class Interval {
        int start, end, weight, id;
        Interval(int start, int end, int weight, int id) {
            this.start = start;
            this.end = end;
            this.weight = weight;
            this.id = id;
        }
    }

    private static class State {
        long weight;
        List<Integer> ids;

        State(long weight, List<Integer> ids) {
            this.weight = weight;
            this.ids = new ArrayList<>(ids);
            Collections.sort(this.ids); // Maintain sorted order for lexicographical tie-breaking
        }
    }

    public int[] maximumWeight(List<List<Integer>> intervals) {
        int n = intervals.size();
        Interval[] arr = new Interval[n];
        for (int i = 0; i < n; i++) {
            List<Integer> inter = intervals.get(i);
            arr[i] = new Interval(inter.get(0), inter.get(1), inter.get(2), i);
        }

        Arrays.sort(arr, (a, b) -> Integer.compare(a.end, b.end));

        State[][] dp = new State[n + 1][5];
        for (int i = 0; i <= n; i++) {
            for (int j = 0; j <= 4; j++) {
                dp[i][j] = new State(0, new ArrayList<>());
            }
        }

        int[] endTimes = new int[n];
        for (int i = 0; i < n; i++) {
            endTimes[i] = arr[i].end;
        }

        for (int i = 1; i <= n; i++) {
            Interval curr = arr[i - 1];
            
            int p = binarySearch(endTimes, curr.start);

            for (int j = 1; j <= 4; j++) {
                State excludeState = dp[i - 1][j];

                State prevState = dp[p][j - 1];
                long includeWeight = prevState.weight + curr.weight;
                
                List<Integer> includeIds = new ArrayList<>(prevState.ids);
                includeIds.add(curr.id);
                State includeState = new State(includeWeight, includeIds);

                if (isBetter(includeState, excludeState)) {
                    dp[i][j] = includeState;
                } else {
                    dp[i][j] = excludeState;
                }
            }
        }

        List<Integer> finalIds = dp[n][4].ids;
        int[] result = new int[finalIds.size()];
        for (int i = 0; i < finalIds.size(); i++) {
            result[i] = finalIds.get(i);
        }
        return result;
    }

    private int binarySearch(int[] endTimes, int target) {
        int low = 0, high = endTimes.length - 1;
        int ans = -1;
        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (endTimes[mid] < target) {
                ans = mid;
                low = mid + 1; // Look for a later valid interval closer to target
            } else {
                high = mid - 1;
            }
        }
        return ans + 1; // Shift to 1-based indexing for DP table
    }

    private boolean isBetter(State s1, State s2) {
        if (s1.weight != s2.weight) {
            return s1.weight > s2.weight;
        }
        int len = Math.min(s1.ids.size(), s2.ids.size());
        for (int i = 0; i < len; i++) {
            if (!s1.ids.get(i).equals(s2.ids.get(i))) {
                return s1.ids.get(i) < s2.ids.get(i);
            }
        }
        return s1.ids.size() < s2.ids.size();
    }
}
```

---