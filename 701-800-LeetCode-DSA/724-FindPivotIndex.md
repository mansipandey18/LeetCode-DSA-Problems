# <u>724. Find Pivot Index</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/find-pivot-index/

---

## 🧠 Intuition:
* 🔹 First calculate total sum of array and store it as **rightSum**, while **leftSum** starts from `0`

* 🔹 Traverse the array and treat each index as a potential pivot

* 🔹 For every index, first remove current element from **rightSum** (because pivot should not be included in right side)

* 🔹 Now compare **leftSum** and **rightSum** → if both are equal, this index is the pivot

* 🔹 If not equal, add current element to **leftSum** and move forward

* 🔹 This way we avoid recalculating sums again and again (efficient approach).


---

## ⏱ Time Complexity

**O(n)**

* single pass to calculate total sum + single pass to find pivot

    
---

## 📦 Space Complexity

**O(1)**

* Only a few variables are used.

---

## 💻 Java Code

```java
class Solution {
    public int pivotIndex(int[] nums) {
        int leftSum = 0;
        int rightSum = 0;

        for (int num : nums) {
            rightSum += num;
        }
      
        for (int i = 0; i < nums.length; i++) {
            rightSum -= nums[i];
          
            if (leftSum == rightSum) {
                return i;  // Found pivot index
            }
          
            leftSum += nums[i];
        }
      
        return -1;
    }
}   
```

---