# <u>2996. Smallest Missing Integer Greater Than Sequential Prefix Sum</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/smallest-missing-integer-greater-than-sequential-prefix-sum/

---

## 🧠 Intuition:
* 🔹 First, find the **longest sequential prefix** of the array.

* 🔹 A sequential prefix means consecutive elements where each element is exactly **1 greater than the previous element**.

* 🔹 Add all elements of this prefix to get the **sequential prefix sum**.

* 🔹 Create a boolean array `isPresent` to mark which numbers already exist in `nums`.

* 🔹 Start checking candidates from the calculated `sum`.

* 🔹 If the candidate is already present, move to the next number.

* 🔹 The **first number that is not present** is the required answer.

* 🔹 The boolean array allows checking whether a number exists in **O(1)** time.

* 🔹 Thus, the solution combines **sequential-prefix detection + presence tracking** to efficiently find the smallest missing integer greater than or equal to the prefix sum.


---

## ⏱ Time Complexity

**O(n)**

* Finding the sequential prefix: **O(n)** worst case.
* Marking all elements in `isPresent`: **O(n)**.
* Searching for the answer is bounded by the problem's value constraints, effectively **O(1)** here.
    
---

## 📦 Space Complexity

**O(1)**

* Auxiliary space because `isPresent` has a fixed size of `51`.
* `sum` and loop variables use constant space.

---

## 💻 Java Code

```java
class Solution {
    public int missingInteger(int[] nums) {
        int sum = nums[0];
      
        for (int i = 1; i < nums.length && nums[i] == nums[i - 1] + 1; i++) {
            sum += nums[i];
        }
      
        boolean[] isPresent = new boolean[51];
      
        for (int num : nums) {
            isPresent[num] = true;
        }
      
        for (int candidate = sum; ; candidate++) {
            if (candidate >= isPresent.length || !isPresent[candidate]) {
                return candidate;
            }
        }
    }
}
```

---