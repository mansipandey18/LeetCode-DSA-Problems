# <u>295. Find Median from Data Stream</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/find-median-from-data-stream/

---

## 🧠 Intuition:
* 🔹 Maintain **two heaps** to efficiently keep track of the lower and upper halves of the numbers.

* 🔹 Use a **Max Heap** to store the smaller half of the elements, so its top always gives the largest element of the lower half.

* 🔹 Use a **Min Heap** to store the larger half of the elements, so its top always gives the smallest element of the upper half.

* 🔹 Always keep the **Max Heap** either the same size as the Min Heap or **one element larger**.

* 🔹 While inserting a new number:
    - If both heaps have the same size, insert the number into the correct heap so that the Max Heap remains one element larger.
    - If the Max Heap already has one extra element, move its largest element to the Min Heap after insertion to rebalance the heaps.

* 🔹 This balancing ensures that:
    - If both heaps have equal size, the median is the **average of their top elements**.
    - If the Max Heap has one extra element, the median is simply the **top of the Max Heap**.

* 🔹 Using two balanced heaps allows both insertion and median retrieval to remain efficient even as the data stream grows


---

## ⏱ Time Complexity

* `addNum()` - **O(log n)**
    - Heap insertion/removal takes `O(log n)`

* `findMedian()` - **O(1)**
    - Median is obtained directly from the heap tops.
    
---

## 📦 Space Complexity

**O(n)**

* Both heaps together store all inserted elements.

---

## 💻 Java Code

```java
class MedianFinder {
    PriorityQueue<Integer> minHeap;
    PriorityQueue<Integer> maxHeap;

    public MedianFinder() {
        minHeap = new PriorityQueue<Integer>();
        maxHeap = new PriorityQueue<Integer>(Collections.reverseOrder());

    }
       
    public void addNum(int num) {
        // even
        if(maxHeap.size() == 0){
            maxHeap.add(num);
            return;
        }
        if(maxHeap.size() == minHeap.size()){
            if(num > maxHeap.peek()){
                minHeap.add(num);
                maxHeap.add(minHeap.poll());
            } else{
                maxHeap.add(num);
            }
        } else{
            maxHeap.add(num);
            minHeap.add(maxHeap.poll());
        }
    }
    
    public double findMedian() {
        if(maxHeap.size() == minHeap.size()){
            return (maxHeap.peek() + minHeap.peek()) / 2.0;
        }

        return maxHeap.peek();
    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.addNum(num);
 * double param_2 = obj.findMedian();
 */
```

---