# <u>3691. Maximum Total Subarray Value II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-total-subarray-value-ii/

---

## 🧠 Intuition:
* 🔹 We need to find the **sum of the top `k` subarray values**, where a subarray value is **(maximum element − minimum element)**.

* 🔹 To answer max/min queries on any subarray efficiently, we build a **Sparse Table** for Range Maximum Query (RMQ) and Range Minimum Query.

* 🔹 Initially, for every starting index `l`, we consider the largest possible subarray `[l, n-1]` and compute its value `(max - min)`.

* 🔹 These subarrays are inserted into **a max-heap (Priority Queue)** so that the subarray with the highest value is always available.

* 🔹 Repeatedly extract the current best subarray from the heap and add its value to the answer.

* 🔹 After taking a subarray `[l, r]`, generate the next candidate by shrinking its right boundary to `[l, r-1]`.

* 🔹 Since max/min queries are answered in **O(1)** using the Sparse Table, new candidates can be generated efficiently.

* 🔹 This greedy process ensures we always pick the next highest available subarray value until `k` values are collected.

---

## ⏱ Time Complexity

**O(n log n + k log n)**

* Building Sparse Table: `O(n log n)`
* Inserting initial `n` subarrays into heap: `O(n log n)`
* Processing `k` heap operations: `O(k log n)`
    
---

## 📦 Space Complexity

**O(n log n)**

* Sparse Tables (`fMax` and `fMin`): `O(n log n)`
* Log array: `O(n)`
* Priority Queue: `O(n)`

---

## 💻 Java Code

```java
class Solution {
    public long maxTotalValue(int[] nums, int k) {
        int n = nums.length;
        SparseTableRMQ st = new SparseTableRMQ(nums);
        
        // PriorityQueue to sort subarrays by their (max - min) range values in descending order
        PriorityQueue<long[]> pq = new PriorityQueue<>((a, b) -> Long.compare(b[0], a[0]));
        
        // Seed the priority queue with the largest window beginning at each index 'l' to 'n-1'
        for (int l = 0; l < n; l++) {
            long val = st.queryMax(l, n - 1) - st.queryMin(l, n - 1);
            pq.offer(new long[] {val, l, n - 1});
        }
        
        long totalMaxSum = 0;
        
        // Greedily extract the top-k highest range differences
        for (int i = 0; i < k; i++) {
            long[] curr = pq.poll();
            long val = curr[0];
            int l = (int) curr[1];
            int r = (int) curr[2];
            
            totalMaxSum += val;
            
            // Push the next potential maximum by shrinking the right boundary
            if (r > l) {
                long nextVal = st.queryMax(l, r - 1) - st.queryMin(l, r - 1);
                pq.offer(new long[] {nextVal, l, r - 1});
            }
        }
        
        return totalMaxSum;
    }
}

class SparseTableRMQ {
    private int[][] fMax;
    private int[][] fMin;
    private int[] lg;

    public SparseTableRMQ(int[] nums) {
        int n = nums.length;
        this.lg = new int[n + 1];
        
        for (int i = 2; i <= n; i++) {
            lg[i] = lg[i / 2] + 1;
        }
        
        int maxLog = lg[n] + 1;
        this.fMax = new int[n][maxLog];
        this.fMin = new int[n][maxLog];
        
        for (int i = 0; i < n; i++) {
            fMax[i][0] = nums[i];
            fMin[i][0] = nums[i];
        }
        
        for (int j = 1; j < maxLog; j++) {
            for (int i = 0; i + (1 << j) <= n; i++) {
                fMax[i][j] = Math.max(fMax[i][j - 1], fMax[i + (1 << (j - 1))][j - 1]);
                fMin[i][j] = Math.min(fMin[i][j - 1], fMin[i + (1 << (j - 1))][j - 1]);
            }
        }
    }

    public int queryMax(int l, int r) {
        int k = lg[r - l + 1];
        return Math.max(fMax[l][k], fMax[r - (1 << k) + 1][k]);
    }

    public int queryMin(int l, int r) {
        int k = lg[r - l + 1];
        return Math.min(fMin[l][k], fMin[r - (1 << k) + 1][k]);
    }
}
```

---