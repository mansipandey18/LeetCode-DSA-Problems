# <u>2542. Maximum Subsequence Score</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-subsequence-score/

---

## 🧠 Intuition:
* 🔹 The score formula is:
    - `(sum of selected nums1 elements) × (minimum selected nums2 element)`

* 🔹 To maximize the score:
    - Treat each `nums2[i]` as the potential minimum element of the subsequence.

* 🔹 Create pairs:
    - `(nums1[i], nums2[i])`

* 🔹 Sort pairs in descending order of `nums2`:
    - So while iterating, the current `nums2` value becomes the minimum value for all selected elements so far.


* 🔹 Use a Min Heap to maintain the largest `k` values from `nums1`.

* 🔹 Keep:
    - `currentSum` → sum of selected `nums1` values

* 🔹 For every pair:
    - Add `nums1` value into heap and update sum.

* 🔹 When heap size becomes `k`:
    - Calculate score:
        * `currentSum * current nums2 value`
    - Update maximum answer.

* 🔹 Remove the smallest `nums1` value from heap:
    - This helps keep only the best possible `k` elements for future iterations.

* 🔹 Heap ensures maximum sum of `nums1` while sorted order ensures valid minimum `nums2`.

---

## ⏱ Time Complexity

**O(n log n)**

* Sorting takes `O(n log n)`
* Heap operations take `O(log k)` for each element.

---

## 📦 Space Complexity

**O(n + k)**

* Pair array + min heap are used.

---

## 💻 Java Code

```java
class Solution {
    public long maxScore(int[] nums1, int[] nums2, int k) {
        int n = nums1.length;
      
        
        int[][] pairs = new int[n][2];
        for (int i = 0; i < n; i++) {
            pairs[i] = new int[] {nums1[i], nums2[i]};
        }
      
        
        Arrays.sort(pairs, (a, b) -> b[1] - a[1]);
      
        long maxResult = 0;
        long currentSum = 0;
      
        
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();
      
        
        for (int i = 0; i < n; i++) {
            
            currentSum += pairs[i][0];
            minHeap.offer(pairs[i][0]);
          
            
            if (minHeap.size() == k) {
                
                maxResult = Math.max(maxResult, currentSum * pairs[i][1]);
              

                currentSum -= minHeap.poll();
            }
        }
      
        return maxResult;
    }
}
```

---