# <u>228. Summary Ranges</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/summary-ranges/

---

## 🧠 Intuition:
* 🔹 The array is **sorted and contains unique elements**, so consecutive numbers form continuous ranges

* 🔹 Start from index `startIndex` and expand `endIndex` as long as next element is **exactly +1** of current

* 🔹 This helps identify a **continuous range [startIndex → endIndex]**

* 🔹 Once the sequence breaks, convert that range into a string:
    - If both indices are same → single number
    - Else → `"start->end"` format

* 🔹 Add this range to result and move `startIndex` to the next unprocessed element

* 🔹 Repeat until the entire array is covered

---

## ⏱ Time Complexity

**O(n)**

* Each element is visited once
    
---

## 📦 Space Complexity

**O(n)**

* Output list stores ranges → **O(n)** (in worst case when no consecutive elements)

---

## 💻 Java Code

```java
class Solution {
    public List<String> summaryRanges(int[] nums) {
        List<String> result = new ArrayList<>();
      
        for (int startIndex = 0, endIndex, n = nums.length; startIndex < n; startIndex = endIndex + 1) {
            endIndex = startIndex;
          
            while (endIndex + 1 < n && nums[endIndex + 1] == nums[endIndex] + 1) {
                endIndex++;
            }
          
            result.add(createRangeString(nums, startIndex, endIndex));
        }
        return result;
    }

    private String createRangeString(int[] nums, int start, int end) {
        return start == end ? Integer.toString(nums[start]) : String.format("%d->%d", nums[start], nums[end]);
    }
}
```

---