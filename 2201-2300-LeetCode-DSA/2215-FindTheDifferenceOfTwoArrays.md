# <u>2215. Find the Difference of Two Arrays</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/find-the-difference-of-two-arrays/

---

## 🧠 Intuition:
* 🔹 Goal is to find elements **unique to each array** (present in one but not in the other)

* 🔹 First convert both arrays into **sets** to remove duplicates and allow fast lookup

* 🔹 Now for every element in `set1`, check if it is **not present in set2** → `if yes, add to result list1`

* 🔹 Similarly, for every element in `set2`, check if it is **not present in set1** → `add to result list2`

* 🔹 Finally, **return both lists as the answer**

* 🔹 Using sets ensures we only deal with **unique values** and comparisons become efficient

---

## ⏱ Time Complexity

**O(m + n)**

* Converting arrays to sets → `O(n + m)`
Checking differences → `O(n + m)`

---

## 📦 Space Complexity

**O(m + n)**

* Two sets to store unique elements → `O(n + m)`
* Output lists also take space

---

## 💻 Java Code

```java
class Solution {
    public List<List<Integer>> findDifference(int[] nums1, int[] nums2) {
        Set<Integer> set1 = convertToSet(nums1);
        Set<Integer> set2 = convertToSet(nums2);

        List<List<Integer>> answer = new ArrayList<>();
        List<Integer> uniqueToNums1 = new ArrayList<>();
        List<Integer> uniqueToNums2 = new ArrayList<>();

        for (int value : set1) {
            if (!set2.contains(value)) {
                uniqueToNums1.add(value);
            }
        }

        for (int value : set2) {
            if (!set1.contains(value)) {
                uniqueToNums2.add(value);
            }
        }

        answer.add(uniqueToNums1);
        answer.add(uniqueToNums2);
      
        return answer;
    }

    private Set<Integer> convertToSet(int[] nums) {
        Set<Integer> set = new HashSet<>();
        for (int value : nums) {
            set.add(value);
        }
        return set;

    }
}
```

---