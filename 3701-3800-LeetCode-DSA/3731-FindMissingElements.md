# <u>3731. Find Missing Elements</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/find-missing-elements/

---

## 🧠 Intuition:
* 🔹 Traverse the array once to find:
    * The minimum element.
    * The maximum element.
    * Store every element in a HashSet for fast lookup.

* 🔹 The missing numbers can only lie between the minimum and maximum values.

* 🔹 Iterate through every integer from min + 1 to max - 1.

* 🔹 For each number:
    - Check whether it exists in the HashSet.
    - If it does not exist, add it to the result list.

* 🔹 Return the list of all missing numbers found in the range.

* 🔹 Using a HashSet allows checking the existence of each number in constant time, making the solution efficient.

---

## ⏱ Time Complexity

**O(n + (max − min))**

* `O(n)` to find the minimum, maximum, and build the HashSet.
* `O(max − min)` to scan all numbers between the minimum and maximum.
    
---

## 📦 Space Complexity

**O(n)**

* The `HashSet` stores all unique elements from the array, and the result list stores the missing numbers.

---

## 💻 Java Code

```java
class Solution {
    public List<Integer> findMissingElements(int[] nums) {
        List<Integer> result = new ArrayList<>();
        if (nums == null || nums.length == 0) {
            return result;
        }

        int mn = Integer.MAX_VALUE;
        int mx = Integer.MIN_VALUE;
        Set<Integer> set = new HashSet<>();

        // Find min, max and populate the hash set
        for (int num : nums) {
            if (num < mn) mn = num;
            if (num > mx) mx = num;
            set.add(num);
        }

        // Collect all missing numbers between mn and mx
        for (int i = mn + 1; i < mx; i++) {
            if (!set.contains(i)) {
                result.add(i);
            }
        }

        return result;
    }
}
```

---