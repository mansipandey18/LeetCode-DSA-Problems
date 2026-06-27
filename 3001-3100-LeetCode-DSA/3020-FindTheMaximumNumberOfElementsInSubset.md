# <u>3020. Find the Maximum Number of Elements in Subset</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/find-the-maximum-number-of-elements-in-subset/

---

## 🧠 Intuition:
* 🔹 Count the frequency of every number using a **HashMap** so we know how many times each value is available.

* 🔹 Handle the special case of 1 separately because squaring `1` always gives `1`, so we can only use the largest valid odd count of `1s`.

* 🔹 For every other unique number, treat it as the starting value of a possible subset.

* 🔹 Keep squaring the current number (`x → x² → x⁴ → ...`) to follow the required sequence.

* 🔹 As long as a number appears **at least twice**, use a pair of that number and move to its square, increasing the subset length by `2`.

* 🔹 When no pair is available, use the final number only if it exists once, then stop extending the sequence.

* 🔹 Track the maximum subset length obtained from all possible starting numbers.

* 🔹 Return the largest valid subset length found.

---

## ⏱ Time Complexity

**O(n + m * log log M)**

* Where:
    - `n = size of array`
    - `m = number of unique elements,`
    - `d = maximum element in nums`

---

## 📦 Space Complexity

**O(m)**

* HashMap stores the frequency of all unique elements

---

## 💻 Java Code

```java
class Solution {
    public int maximumLength(int[] nums) {
        // Count frequency of each number in the array
        Map<Long, Integer> frequencyMap = new HashMap<>();
        for (int num : nums) {
            frequencyMap.merge((long) num, 1, Integer::sum);
        }
      
        Integer onesCount = frequencyMap.remove(1L);
        int maxLength = (onesCount == null) ? 0 : onesCount - (onesCount % 2 ^ 1);
      
        for (long baseNum : frequencyMap.keySet()) {
            int currentLength = 0;
            long currentNum = baseNum;
          
            while (frequencyMap.getOrDefault(currentNum, 0) > 1) {
                currentNum = currentNum * currentNum;
                currentLength += 2;  // Add pair of elements
            }
          
            currentLength += frequencyMap.getOrDefault(currentNum, -1);
          
            maxLength = Math.max(maxLength, currentLength);
        }
      
        return maxLength;   
    }
}
```

---