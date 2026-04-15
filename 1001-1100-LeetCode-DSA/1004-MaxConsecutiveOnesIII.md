# <u>1004. Max Consecutive Ones III</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/max-consecutive-ones-iii/

---

## 🧠 Intuition:
* 🔹 We need the **longest subarray with at most `k` zeros** (because we can flip at most k zeros to 1).

* 🔹 Think of it as a **sliding window** where we allow at most `k` zeros inside the window.

* 🔹 Traverse the array and keep expanding the window to the right.

* 🔹 For every element:
    - If it's `0`, increase `zeroCount` (using `num ^ 1` trick → gives 1 when num is 0).

* 🔹 If `zeroCount > k`, it means we have too many zeros → shrink window from left:
    - Move `left` forward and reduce zero count if needed.

* 🔹 At any point, the window is always valid (≤ k zeros).

* 🔹 Instead of tracking max explicitly, final answer becomes **window size = total length - left**.


---

## ⏱ Time Complexity

**O(n)**

* Each element is visited at most twice (once by right pointer, once by left pointer).
    
---

## 📦 Space Complexity

**O(1)**

* Only a few variables are used

---

## 💻 Java Code

```java
class Solution {
    public int longestOnes(int[] nums, int k) {
        int left = 0, zeroCount = 0;

        for(int num : nums){
            zeroCount += num ^ 1;

            if(zeroCount > k){
                zeroCount -= nums[left] ^ 1;
                left++;
            }
        }

        return nums.length - left;
    }
}
```

---