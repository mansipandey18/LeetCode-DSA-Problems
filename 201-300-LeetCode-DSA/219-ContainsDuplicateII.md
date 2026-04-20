# <u>219. Contains Duplicate II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/contains-duplicate-ii/

---

## 🧠 Intuition:
* 🔹 We need to check if there exist **two equal elements whose indices differ by at most k**

* 🔹 Instead of comparing all pairs (which is slow), we use a **sliding window of size k**

* 🔹 Maintain a **HashSet** to store elements currently inside the window

* 🔹 First, fill the set with first `k` elements while checking duplicates

* 🔹 Then, slide the window forward one step at a time:
    - Before adding a new element, check if it already exists in the set → **if yes**, `duplicate found within distance k`
    - Add current element to the set
    - Remove the element that goes out of the window (`i - k`) to maintain window size

* 🔹 This ensures we always check duplicates only within distance `k` efficiently

---

## ⏱ Time Complexity

**O(n)**

* Each element is added and removed from set at most once
    
---

## 📦 Space Complexity

**O(k)**

* Set stores at most `k` elements.

---

## 💻 Java Code

```java
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        Set<Integer> set = new HashSet<>();
        for(int i = 0; i < Math.min(k, nums.length); i++){
            if(set.contains(nums[i])){
                return true;
            }

            set.add(nums[i]);
        }

        for(int i = k; i < nums.length; i++){
            if(set.contains(nums[i])){
                return true;
            }
            set.add(nums[i]);
            set.remove(nums[i - k]);
        }

        return false;
    }
}  
```

---