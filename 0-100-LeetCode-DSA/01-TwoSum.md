# 1. Two Sum

## 🔗 Problem Link
https://leetcode.com/problems/two-sum/description/


## 🧠 Intuition:
* We need two numbers whose sum = target

* Checking every pair would take O(n²) ❌ (slow)

* Instead, we use a HashMap to remember numbers we have already seen

* For each number:

    - Calculate what number we are looking for

         - lookingFor = target - current number

    - Check if that number already exists in the map

* If it exists → we found the pair ✅

* If not → store current number in map and continue

* This makes it O(n) instead of O(n²) 🚀

## ⏱ Time Complexity
O(n)

## 📦 Space Complexity
O(n)

---
## 🧩 Java Code:

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();

        for(int i = 0; i < nums.length; i++){
            int lookingFor = target- nums[i];

            if(map.containsKey(lookingFor)){
                return new int[]{i, map.get(lookingFor)};
            }

            map.put(nums[i], i);
        }

        return new int[]{-1, -1};
    }
}
```
---