# <u>3069. Distribute Elements Into Two Arrays I</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/distribute-elements-into-two-arrays-i/

---

## 🧠 Intuition:
* 🔹 Create two separate arrays, `firstArray` and `secondArray`, to distribute the elements.

* 🔹 Put the **first element** of `nums` into `firstArray` and the **second element** into `secondArray`.

* 🔹 Starting from index `2`, compare the **last elements** of both arrays.

* 🔹 If the last element of `firstArray` is greater than the last element of `secondArray`, add the current element to `firstArray`.

* 🔹 Otherwise, add it to `secondArray`.

* 🔹 After all elements are distributed, append all elements of `secondArray` to the end of `firstArray`.

* 🔹 The resulting `firstArray` is the required answer.

---

## ⏱ Time Complexity

**O(n)**

* Distributing elements takes `O(n)`.
* Merging secondArray into firstArray takes `O(n)`. 

---

## 📦 Space Complexity

**O(n)**

* Two arrays of size `n` are used.

---

## 💻 Java Code

```java
class Solution {
    public int[] resultArray(int[] nums) {
        int n = nums.length;
      
        int[] firstArray = new int[n];
        int[] secondArray = new int[n];
      
        firstArray[0] = nums[0];
        secondArray[0] = nums[1];
      
        int lastIndexFirst = 0;
        int lastIndexSecond = 0;
      
        for (int currentIndex = 2; currentIndex < n; currentIndex++) {
            if (firstArray[lastIndexFirst] > secondArray[lastIndexSecond]) {
                lastIndexFirst++;
                firstArray[lastIndexFirst] = nums[currentIndex];
            } else {
                lastIndexSecond++;
                secondArray[lastIndexSecond] = nums[currentIndex];
            }
        }
      
        for (int index = 0; index <= lastIndexSecond; index++) {
            lastIndexFirst++;
            firstArray[lastIndexFirst] = secondArray[index];
        }
      
        return firstArray;
    }
}
```

---