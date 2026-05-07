# <u>3660. Jump Game IX</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/jump-game-ix/

---

## 🧠 Intuition:
* 🔹 The problem uses the idea of maintaining the **maximum value from the left side** and comparing it with the **minimum value from the right side**

* 🔹 Create a `prefixMax` array where:
    - `prefixMax[i]` stores the maximum element from index `0 → i`

* 🔹 Traverse the array from right to left while maintaining:
    - `suffixMin` → minimum value seen from the right side

* 🔹 For every index `i`:
    - If `prefixMax[i] > suffixMin`
        * It means there exists a smaller value on the right side
        * So current prefix maximum cannot be a valid answer independently
        * Copy the answer from the next index (`result[i + 1]`)
    - Otherwise:
        * prefixMax[i] is valid and stored in `result[i]`

* 🔹 Update `suffixMin` continuously while moving backward

* 🔹 This efficiently avoids checking every pair using nested loops

---

## ⏱ Time Complexity

**O(n)**

* Building prefixMax array → **O(n)**
* Right-to-left traversal → **O(n)**

---

## 📦 Space Complexity

**O(n)**

* `prefixMax` array → **O(n)**
* `result` array → **O(n)**


---

## 💻 Java Code

```java
class Solution {
    public int[] maxValue(int[] nums) {
        int n = nums.length;
        int[] result = new int[n];
      
        int[] prefixMax = new int[n];
        prefixMax[0] = nums[0];
        for (int i = 1; i < n; i++) {
            prefixMax[i] = Math.max(prefixMax[i - 1], nums[i]);
        }
      
        int suffixMin = 1 << 30;
      
        for (int i = n - 1; i >= 0; i--) {
            if (prefixMax[i] > suffixMin) {
                result[i] = (i + 1 < n) ? result[i + 1] : 0;
            } else {
                result[i] = prefixMax[i];
            }
          
            suffixMin = Math.min(suffixMin, nums[i]);
        }
      
        return result;
    }
}
```

---