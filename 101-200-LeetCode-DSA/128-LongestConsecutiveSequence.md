# <u>128. Longest Consecutive Sequence</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/longest-consecutive-sequence/

---

## 🧠 Intuition:
* 🔹 We want the **longest sequence of consecutive numbers**, but sorting would be slower → so we use a **HashSet for O(1)** lookup

* 🔹 First, insert all elements into a set to remove duplicates and allow fast checks

* 🔹 For each number, we only start counting a sequence **if it is the beginning** of a sequence
    - i.e., `num - 1` is not present in the set

* 🔹 From such a starting point, keep checking `num + 1, num + 2, ...` in the set

* 🔹 Count how long this consecutive chain goes

* 🔹 Update the maximum length found

* 🔹 This ensures every sequence is counted **only once**, avoiding redundant work.

---

## ⏱ Time Complexity

**O(n)**

* Each element is processed at most once
    
---

## 📦 Space Complexity

**O(n)**

* HashSet stores all elements.

---

## 💻 Java Code

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        int ans = 0;
        Set<Integer> seen = Arrays.stream(nums).boxed().collect(Collectors.toSet());

        for (int num : seen) {
            if (seen.contains(num - 1))
                continue;
            int length = 1;
            while (seen.contains(++num))
                ++length;
            ans = Math.max(ans, length);
        }

        return ans;
        
    }
}
```

---