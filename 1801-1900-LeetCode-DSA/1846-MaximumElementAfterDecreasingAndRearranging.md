# <u>1846. Maximum Element After Decreasing and Rearranging</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-element-after-decreasing-and-rearranging/

---

## 🧠 Intuition:
* 🔹 Sort the array so the elements are processed in increasing order.

* 🔹 Set the first element to **1**, since the smallest possible value must always be `1`.

* 🔹 Traverse the remaining elements one by one.

* 🔹 If the current element is more than **1 greater** than the previous element, reduce it so that the difference becomes exactly `1`.

* 🔹 If the current element is already equal to or just one greater than the previous element, leave it unchanged.

* 🔹 Keep updating the maximum element while traversing the array.

* 🔹 This greedy approach ensures the array satisfies:
    - The first element is `1`.
    - The difference between adjacent elements is at most `1`.
    - The maximum possible final element is achieved.

---

## ⏱ Time Complexity

**O(n log n)**

* Sorting the array takes `O(n log n)`, and the traversal takes `O(n)`.

---

## 📦 Space Complexity

**O(1)**

* *excluding the space used by the sorting algorithm*.

---

## 💻 Java Code

```java
class Solution {
    public int maximumElementAfterDecrementingAndRearranging(int[] arr) {
        Arrays.sort(arr);
      
        arr[0] = 1;
      
        int maxElement = 1;
      
        for (int i = 1; i < arr.length; ++i) {
            int excessDifference = Math.max(0, arr[i] - arr[i - 1] - 1);
          
            arr[i] -= excessDifference;
          
            maxElement = Math.max(maxElement, arr[i]);
        }
      
        return maxElement;
    }
}
```

---