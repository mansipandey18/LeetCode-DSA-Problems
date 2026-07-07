# <u>373. Find K Pairs with Smallest Sums</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/find-k-pairs-with-smallest-sums/

---

## 🧠 Intuition:
* 🔹 Since both arrays are sorted, the pair `(nums1[0], nums2[0])` always has the smallest possible sum, so start from this pair.

* 🔹 Use a **Min Heap (Priority Queue)** to always process the pair with the smallest current sum.

* 🔹 Store each heap entry as **{sum, index in `nums1`, index in `nums2`}**.

* 🔹 After removing the smallest pair, add it to the answer.

* 🔹 From the current pair `(i, j)`, only two new candidate pairs can produce the next smallest sums:
    - `(i + 1, j)` → move to the next element in `nums1`.
    - `(i, j + 1)` → move to the next element in `nums2`.

* 🔹 Use a **HashSet** to keep track of visited index pairs so the same pair is never inserted into the heap more than once.

* 🔹 Repeat this process until exactly `k` smallest pairs have been collected.

* 🔹 This approach explores only the necessary candidate pairs instead of generating all possible pairs.

---

## ⏱ Time Complexity

**O(k log k)**

* Each of the `k` extracted pairs performs heap operations that take `O(log k)`.
    
---

## 📦 Space Complexity

**O(k)**

* For the min heap, visited set, and result list (excluding the output).

---

## 💻 Java Code

```java
class Solution {
    public List<List<Integer>> kSmallestPairs(int[] nums1, int[] nums2, int k) {
        PriorityQueue<int[]> minHeap = new PriorityQueue<>((a, b) -> a[0] - b[0]);
        Set<Pair<Integer, Integer>> visited = new HashSet<>();

        minHeap.add(new int[]{
            nums1[0] + nums2[0],
            0,
            0
        });

        List<List<Integer>> result = new ArrayList<>();

        int counter = 1;

        while(counter <= k){
            int ele[] = minHeap.remove();
            int sum = ele[0], i = ele[1], j = ele[2];

            result.add(Arrays.asList(nums1[i], nums2[j]));

            if(i + 1 < nums1.length){
                Pair<Integer, Integer> pair = new Pair<Integer, Integer>(i + 1, j);
                if(!visited.contains(pair)){
                    minHeap.add(new int[]{
                        nums1[i + 1] + nums2[j],
                        i + 1,
                        j 
                    });

                    visited.add(pair); 
                }
            }

            if(j + 1 < nums2.length){
                Pair<Integer, Integer> pair = new Pair<Integer, Integer>(i, j + 1);
                if(!visited.contains(pair)){
                    minHeap.add(new int[]{
                        nums1[i] + nums2[j + 1],
                        i,
                        j + 1
                    });

                    visited.add(pair); 
                }
            }

            counter++;
        }

        return result;
    }
}
```

---