# <u>3635. Earliest Finish Time for Land and Water Rides II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/earliest-finish-time-for-land-and-water-rides-ii/

---

## 🧠 Intuition:
* 🔹 We can take the rides in **two possible orders: Land → Water or Water → Land**.

* 🔹 Create a helper function `calc()` that computes the earliest finish time for a given order.

* 🔹 First, find the **earliest possible completion time** among all rides of the first type (`startTime + duration`).

* 🔹 Once the first ride is completed, choose the best second ride.

* 🔹 The second ride can only start after both:
    - the first ride has finished, and
    - the second ride's own start time has arrived.

* 🔹 Therefore, the actual start time of the second ride is `max(firstRideFinishTime, secondRideStartTime)`.

* 🔹 Calculate the finish time for every possible second ride and keep the minimum.

* 🔹 Run this process for both orders (**Land → Water and Water → Land**).

* 🔹 Return the smaller of the two results as the earliest overall finish time.

---

## ⏱ Time Complexity

**O(n + m)**

* one pass to find the earliest finish time of the first ride type and one pass to evaluate all rides of the second type.

---

## 📦 Space Complexity

**O(1)**

* only a few variables are used; no extra data structures are required.

---

## 💻 Java Code

```java
class Solution {
    public int earliestFinishTime(int[] landStartTime, int[] landDuration, int[] waterStartTime, int[] waterDuration) {
        int x = calc(landStartTime, landDuration, waterStartTime, waterDuration);
        int y = calc(waterStartTime, waterDuration, landStartTime, landDuration);
        return Math.min(x, y);
    }

    private int calc(int[] a1, int[] t1, int[] a2, int[] t2) {
        int minEnd = Integer.MAX_VALUE;
        for (int i = 0; i < a1.length; ++i) {
            minEnd = Math.min(minEnd, a1[i] + t1[i]);
        }
        int ans = Integer.MAX_VALUE;
        for (int i = 0; i < a2.length; ++i) {
            ans = Math.min(ans, Math.max(minEnd, a2[i]) + t2[i]);
        }
        return ans;
    }
}
```

---