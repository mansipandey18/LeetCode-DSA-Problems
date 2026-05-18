# <u>215. Kth Largest Element in an Array</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/kth-largest-element-in-an-array/

---

## 🧠 Intuition:
* 🔹 Use a Min Heap to keep track of the `k` largest elements seen so far.

* 🔹 First, insert the first `k` elements into the heap.

* 🔹 The heap root (`peek`) will always store the smallest element among these `k` elements.

* 🔹 Traverse the remaining elements:
    - If the current number is larger than the heap’s smallest element:
        * Remove the smallest element from the heap.
        * Insert the current larger element.

* 🔹 This ensures:
    - The heap always contains the `k` largest elements in the array.

* 🔹 After processing all elements:
    - The root of the min heap is the `kth` largest element.

---

## ⏱ Time Complexity

**O(n log k)**

* Each heap insertion/removal takes `O(log k)`.
* Done for at most `n` elements.
    
---

## 📦 Space Complexity

**O(k)**

* Min heap stores at most `k` elements.

---

## 💻 Java Code

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();

        for(int i = 0; i < k; i++){
            minHeap.add(nums[i]);
        }

        for(int i = k; i < nums.length; i++){
            if(nums[i] > minHeap.peek()){
                minHeap.remove();
                minHeap.add(nums[i]);
            }
        }

        return minHeap.peek();
    }
} 
```

---