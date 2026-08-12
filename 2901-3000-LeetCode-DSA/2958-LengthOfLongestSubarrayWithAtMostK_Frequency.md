# <u>2958. Length of Longest Subarray With at Most K Frequency</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/length-of-longest-subarray-with-at-most-k-frequency/

---

## 🧠 Intuition:
* 🔹 Use the **Sliding Window + HashMap** technique.

* 🔹 Maintain a window from `left` to `right` where every number appears **at most `k` times**.

* 🔹 As `right` moves forward, add `nums[right]` to `frequencyMap` and increase its frequency.

* 🔹 If the frequency of `nums[right]` becomes greater than `k`, the current window becomes invalid.

* 🔹 Move `left` forward and decrease the frequency of elements being removed until the window becomes valid again.

* 🔹 At every valid window, calculate its length as `right - left + 1`.

* 🔹 Keep the maximum length found so far in `maxLength`.

* 🔹 Since `left` and `right` each move only forward, every element is processed a constant number of times.

---

## ⏱ Time Complexity

**O(n)**

* `right` traverses the array once.
* `left` also moves at most `n` times.
* HashMap operations are `O(1)` on average.
    
---

## 📦 Space Complexity

**O(n)**

* The `frequencyMap` can store up to `n` distinct elements.

---

## 💻 Java Code

```java
class Solution {
    public int maxSubarrayLength(int[] nums, int k) {
        Map<Integer, Integer> frequencyMap = new HashMap<>();
      
        int maxLength = 0;
        int left = 0;
      
        for (int right = 0; right < nums.length; right++) {
            frequencyMap.merge(nums[right], 1, Integer::sum);
          
            while (frequencyMap.get(nums[right]) > k) {
                frequencyMap.merge(nums[left], -1, Integer::sum);
                left++;
            }
          
            maxLength = Math.max(maxLength, right - left + 1);
        }
      
        return maxLength;
    }
}
```

---