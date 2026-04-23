# <u>2615. Sum of Distances</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/sum-of-distances/

---

## 🧠 Intuition:
* 🔹 We need, for each index, the **sum of distances to all other indices having the same value**

* 🔹 First, group indices by their values using a hashmap → each value has a list of its positions

* 🔹 For each group, instead of computing pairwise distances (which is slow), we use a **prefix-sum style optimization**

* 🔹 Initialize two parts:
    - `leftSum` → contribution from indices to the left
    - `rightSum` → contribution from indices to the right

* 🔹 Initially, compute total distance assuming all indices are on the right side

* 🔹 Then iterate through indices of the group:
    - For current index, total distance = `leftSum + rightSum`
    - Move one step forward and update:
        * Increase `leftSum` based on how many elements are on left
        * Decrease `rightSum` based on how many elements remain on right

* 🔹 This avoids recomputation and efficiently calculates distances in linear time per group

---

## ⏱ Time Complexity

**O(n)**

* Building hashmap → **O(n)**

* Processing each group → total across all groups is **O(n)**
    
---

## 📦 Space Complexity

**O(n)**

* Hashmap + result array

---

## 💻 Java Code

```java
class Solution {
    public long[] distance(int[] nums) {
        int n = nums.length;
        long[] result = new long[n];
      
        Map<Integer, List<Integer>> valueToIndices = new HashMap<>();
        for (int i = 0; i < n; i++) {
            valueToIndices.computeIfAbsent(nums[i], k -> new ArrayList<>()).add(i);
        }
      
        for (List<Integer> indices : valueToIndices.values()) {
            int groupSize = indices.size();
          
            long leftSum = 0;
          
            long rightSum = -1L * groupSize * indices.get(0);
            for (int index : indices) {
                rightSum += index;
            }
          
            for (int i = 0; i < groupSize; i++) {
                result[indices.get(i)] = leftSum + rightSum;
              
                if (i + 1 < groupSize) {
                    int currentIndex = indices.get(i);
                    int nextIndex = indices.get(i + 1);
                    int gap = nextIndex - currentIndex;
                  
                    leftSum += gap * (i + 1L);
                  
                    rightSum -= gap * (groupSize - i - 1L);
                }
            }
        }
      
        return result;
    
    }
}
```

---