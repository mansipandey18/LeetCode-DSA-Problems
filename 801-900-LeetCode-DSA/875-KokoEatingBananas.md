# <u>875. Koko Eating Bananas</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/koko-eating-bananas/

---

## 🧠 Intuition:
* 🔹 We need to find the minimum eating speed `k` such that Koko can finish all banana piles within `h` hours.

* 🔹 A higher eating speed always reduces the total hours needed, which creates a **monotonic condition** — perfect for Binary Search.

* 🔹 Use Binary Search on the answer space:
    - Minimum possible speed = `1` banana/hour
    - Maximum possible speed = `1e9` (large enough upper bound)

* 🔹 For every candidate speed `midSpeed`, calculate how many hours Koko would need to finish all piles.

* 🔹 Hours for one pile are computed using ceiling division:
    - `(bananas + midSpeed - 1) / midSpeed`
    - This represents the number of full hours needed for that pile.

* 🔹 If total required hours `<= h`, then this speed is valid, so try a smaller speed to minimize the answer.

* 🔹 Otherwise, the speed is too slow, so search in the larger half.

* 🔹 Continue Binary Search until the smallest valid speed is found.

---

## ⏱ Time Complexity

**O(n * log(1e9))**

* Binary Search runs in `log(1e9)` iterations, and each iteration scans all `n` piles.

    
---

## 📦 Space Complexity

**O(1)**

* Only constant extra variables are used.

---

## 💻 Java Code

```java
class Solution {
    public int minEatingSpeed(int[] piles, int h) {
        int minSpeed = 1;
        int maxSpeed = (int) 1e9;
      
        while (minSpeed < maxSpeed) {
            int midSpeed = minSpeed + (maxSpeed - minSpeed) / 2;
          
            int totalHours = 0;
          
            for (int bananas : piles) {
                totalHours += (bananas + midSpeed - 1) / midSpeed;
            }
          
            if (totalHours <= h) {
                maxSpeed = midSpeed;
            } else {
                minSpeed = midSpeed + 1;
            }
        }
      
        return minSpeed;
    }
}
```

---