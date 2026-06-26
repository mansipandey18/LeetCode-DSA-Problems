# <u>3739. Count Subarrays With Majority Element II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/count-subarrays-with-majority-element-ii/

---

## 🧠 Intuition:
* 🔹 A subarray has `target` as the majority if the count of `target` is greater than the count of all other elements.

* 🔹 Convert the array into:
    - `+1` if the element is equal to `target`
    - `-1` otherwise.

* 🔹 After this transformation, a subarray is valid if its **sum is positive**.

* 🔹 Use a prefix sum to represent the running balance of `+1` and `-1`.

* 🔹 For each position, we need to count how many **previous prefix sums are smaller than the current prefix sum**, because:
    - `currentPrefix - previousPrefix > 0` ⇒ subarray sum is positive.

* 🔹 A **Fenwick Tree (Binary Indexed Tree)** efficiently stores the frequencies of previous prefix sums.

* 🔹 Since prefix sums can be negative, shift them by an offset (`n + 1`) so they become valid positive indices in the Fenwick Tree.

* 🔹 For every element:
    - Update the prefix sum based on whether it matches `target`.
    - Query the Fenwick Tree to count all smaller prefix sums.
    - Add that count to the answer.
    - Insert the current prefix sum into the Fenwick Tree for future queries.

* 🔹 This avoids checking every subarray and reduces the solution from **O(n²)** to **O(n log n)**.

---

## ⏱ Time Complexity

**O(n log n)**

* Each of the `n` elements performs one Fenwick Tree update and one query, each taking `O(log n)`.

---

## 📦 Space Complexity

**O(n)**

* For the Fenwick Tree used to store prefix sum frequencies.


---

## 💻 Java Code

```java
class Solution {
    public long countMajoritySubarrays(int[] nums, int target) {
        int n = nums.length;
        
        // Max range of running prefix sum is from -n to +n. 
        // We use size 2 * n + 1 and map 0 (the initial empty prefix sum) to n + 1.
        FenwickTree bit = new FenwickTree(2 * n + 1);
        
        int currentPrefixSum = n + 1; 
        bit.update(currentPrefixSum, 1); // Insert the initial prefix sum of 0
        
        long totalSubarrays = 0;
        
        for (int num : nums) {
            // Transform element: target is +1, others are -1
            if (num == target) {
                currentPrefixSum++;
            } else {
                currentPrefixSum--;
            }
            
            // Query how many historical prefix sums are strictly smaller than the current one
            totalSubarrays += bit.query(currentPrefixSum - 1);
            
            // Insert the current prefix sum into the tracker
            bit.update(currentPrefixSum, 1);
        }
        
        return totalSubarrays;
    }

    private static class FenwickTree {
        private final int[] tree;
        private final int size;

        public FenwickTree(int size) {
            this.size = size;
            this.tree = new int[size + 1];
        }

        // Add 1 to the frequency of index x
        public void update(int x, int delta) {
            for (; x <= size; x += x & -x) {
                tree[x] += delta;
            }
        }

        // Query the cumulative frequency up to index x
        public int query(int x) {
            int sum = 0;
            for (; x > 0; x -= x & -x) {
                sum += tree[x];
            }
            return sum;
        }
    }

}
```

---