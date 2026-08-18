# <u>3471. Find the Largest Almost Missing Integer</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/find-the-largest-almost-missing-integer/

---

## 🧠 Intuition:
* 🔹 The key idea is to identify numbers that appear in **exactly one** valid subarray of length `k`.

* 🔹 When `k == 1`, every element forms its own subarray, so a number is valid only if it appears **exactly once** in the entire array. Return the largest such number.

* 🔹 When `k == n`, there is only **one subarray** containing the whole array, so every distinct number appears in that subarray. Therefore, simply return the maximum element.

* 🔹 For `1 < k < n`, only the **first and last elements** can belong to exactly one subarray of length `k`:
    - `nums[0]` appears only in the first window.
    - `nums[n-1]` appears only in the last window.

* 🔹 So, the code checks whether the first and last elements are **globally unique**.

* 🔹 `checkIfUnique()` scans the entire array to verify whether the selected element occurs anywhere else.

* 🔹 If the first or last element is unique, it becomes a candidate answer.

* 🔹 Finally, return the **larger valid candidate**.

---

## ⏱ Time Complexity

**O(n)**

* `For k == 1`, building the frequency map takes **O(n)**.
* `For k == n`, finding the maximum takes **O(n)**.
* `For 1 < k < n`, checkIfUnique() is called at most twice, and each call takes **O(n)**.
    
---

## 📦 Space Complexity

**O(n)**

* For `k == 1`, the `HashMap` can store up to `O(n)` distinct values.
* Otherwise, only constant extra space is used.

---

## 💻 Java Code

```java
class Solution {
    private int[] numbers;

    public int largestInteger(int[] nums, int k) {
        this.numbers = nums;
      
        if (k == 1) {
            Map<Integer, Integer> frequencyMap = new HashMap<>();
            for (int number : nums) {
                frequencyMap.merge(number, 1, Integer::sum);
            }
          
            int maxUniqueNumber = -1;
            for (Map.Entry<Integer, Integer> entry : frequencyMap.entrySet()) {
                if (entry.getValue() == 1) {
                    maxUniqueNumber = Math.max(maxUniqueNumber, entry.getKey());
                }
            }
            return maxUniqueNumber;
        }
      
        if (k == nums.length) {
            return Arrays.stream(nums).max().getAsInt();
        }
      
        return Math.max(checkIfUnique(0), checkIfUnique(nums.length - 1));
    }

    private int checkIfUnique(int targetIndex) {
        for (int i = 0; i < numbers.length; i++) {
            if (i != targetIndex && numbers[i] == numbers[targetIndex]) {
                return -1;  // Element is not unique
            }
        }
        return numbers[targetIndex];  // Element is unique
    }
}
```

---