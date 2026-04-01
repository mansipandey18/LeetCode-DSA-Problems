# <u>167. Two Sum II - Input Array Is Sorted</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/
---

## 🧠 Intuition:
* 🔹 The array is already sorted, so we can use the two-pointer technique instead of brute force.

* 🔹 Place two pointers:
    - `i` at the start (smallest number)
    - `j` at the end (largest number)

* 🔹 Calculate the sum of both numbers.

* 🔹 Compare the sum with the target:
    - If **sum > target** → decrease sum by moving `j--` (move right pointer left).
    - If **sum < target** → increase sum by moving `i++` (move left pointer right).
    - If **sum == target** → we found the answer.

* 🔹 Because the array is sorted:
    - Moving left pointer increases value.
    - Moving right pointer decreases value.

* 🔹 Continue until pointers meet.

* 🔹 Return **1-based indices** as required by the problem.---

## ⏱ Time Complexity

**O(n)**

* Each pointer moves at most once across the array.
* Single traversal.
    
---

## 📦 Space Complexity

**O(1)**

* No extra data structures used.
* Only variables are maintained.

---

## 💻 Java Code

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int i = 0, j = numbers.length - 1;

        while(i < j){
            int sum = numbers[i] + numbers[j];

            if(sum > target){
                j--;
            } else if(sum < target){
                i++;
            } else{
                return new int[] {i + 1, j + 1};
            }
        }

        return new int[]{-1, -1};
    }
}
```

---