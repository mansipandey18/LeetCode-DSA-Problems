# <u>1386. Cinema Seat Allocation</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/cinema-seat-allocation/

---

## 🧠 Intuition:
* 🔹 The key idea is to identify numbers that appear in exactly one valid subarray of length `k`.

* 🔹 When `k == 1`, every element forms its own subarray, so a number is valid only if it appears **exactly once** in the entire array. Return the largest such number.

* 🔹 When `k == n`, there is only **one subarray** containing the whole array, so every distinct number appears in that subarray. Therefore, simply return the maximum element.

* 🔹 For 1 < k < n, only the **first and last elements* can belong to exactly one subarray of length k:
    - `nums[0]` appears only in the first window.
    - `nums[n-1]` appears only in the last window.

* 🔹 So, the code checks whether the first and last elements are **globally unique**.

* 🔹 `checkIfUnique()` scans the entire array to verify whether the selected element occurs anywhere else.

* 🔹 If the first or last element is unique, it becomes a candidate answer.

* 🔹 Finally, return the **larger valid candidate**.

---

## ⏱ Time Complexity

**O(n)**

* For `k == 1`, building the frequency map takes **O(n)**.
* For `k == n`, finding the maximum takes **O(n)**.
* For `1 < k < n`, `checkIfUnique()` is called at most twice, and each call takes **O(n)**.
    
---

## 📦 Space Complexity

**O(n)**

* For `k == 1`, the `HashMap` can store up to O(n) distinct values.
* Otherwise, only constant extra space is used.

---

## 💻 Java Code

```java
class Solution {
    public int maxNumberOfFamilies(int n, int[][] reservedSeats) {
        Map<Integer, Integer> rowReservations = new HashMap<>();
      
        for (int[] reservation : reservedSeats) {
            int row = reservation[0];
            int seatNumber = reservation[1];
            
            rowReservations.merge(row, 1 << (10 - seatNumber), (existing, newBit) -> existing | newBit);
        }
      
        int leftGroupMask = 0b0111100000;
        int rightGroupMask = 0b0000011110;
        int middleGroupMask = 0b0001111000;
        int[] groupMasks = {leftGroupMask, rightGroupMask, middleGroupMask};
      
        int totalFamilies = (n - rowReservations.size()) * 2;
      
        for (int reservedSeatsBitmask : rowReservations.values()) {
            for (int groupMask : groupMasks) {
                if ((reservedSeatsBitmask & groupMask) == 0) {
                    reservedSeatsBitmask |= groupMask;
                    totalFamilies++;
                }
            }
        }
      
        return totalFamilies;
    
    }
}
```

---