# <u>2091. Removing Minimum and Maximum From Array</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/removing-minimum-and-maximum-from-array/

---

## 🧠 Intuition:
* 🔹 First, find the **indices of the minimum and maximum elements** in the array.

* 🔹 Arrange their indices so that `minIndex < maxIndex` for easier calculation.

* 🔹 To remove both elements, there are **three possible strategies**:
    - **Remove from the left:** Delete everything up to `maxIndex` → `maxIndex + 1` deletions.
    - **Remove from the right:** Delete everything from `minIndex` to the end → `arrayLength - minIndex` deletions.
    - **Remove from both sides:** Delete the prefix up to `minIndex` and the suffix after `maxIndex` → `minIndex + 1 + arrayLength - maxIndex` deletions.

* 🔹 Take the **minimum of these three possibilities**.

* 🔹 This guarantees the minimum number of deletions required to remove both the minimum and maximum elements.

---

## ⏱ Time Complexity

**O(n)**

* Finding minimum and maximum indices requires one traversal → `O(n)`
* Calculating the minimum of the three deletion strategies → `O(1)`

---

## 📦 Space Complexity

**O(1)**

* Only a few variables are used (`minIndex`, `maxIndex`, `arrayLength`, `temp`).

---

## 💻 Java Code

```java
class Solution {
    public int minimumDeletions(int[] nums) {
        int minIndex = 0;
        int maxIndex = 0;
        int arrayLength = nums.length;
      
        for (int i = 0; i < arrayLength; i++) {
            if (nums[i] < nums[minIndex]) {
                minIndex = i;
            }
            if (nums[i] > nums[maxIndex]) {
                maxIndex = i;
            }
        }
      
        if (minIndex > maxIndex) {
            int temp = maxIndex;
            maxIndex = minIndex;
            minIndex = temp;
        }
      
        return Math.min(Math.min(maxIndex + 1, arrayLength - minIndex), minIndex + 1 + arrayLength - maxIndex);
    
    }
}
```

---