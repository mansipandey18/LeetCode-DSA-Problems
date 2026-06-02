# <u>3633. Earliest Finish Time for Land and Water Rides I</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/earliest-finish-time-for-land-and-water-rides-i/

---

## 🧠 Intuition:
* 🔹 We need to find the **earliest possible finish time** after completing **one land ride and one water ride**.

* 🔹 Since the rides can be taken in either order, consider both possibilities:
    - **Land Ride → Water Ride**
    - **Water Ride → Land Ride**

* 🔹 For a chosen order:
    - Find the **earliest completion time** among all rides in the first category (`startTime + duration`).
    - This represents the earliest moment we can start the second type of ride.

* 🔹 For every ride in the second category:
    - The actual start time is `max(firstRideCompletionTime, secondRideStartTime)`.
    - This ensures we wait if the second ride has not started yet.
    - Calculate its finish time as `actualStartTime + duration`.

* 🔹 Keep track of the minimum finish time among all second-category rides.

* 🔹 Compute the result for both possible orders and return the smaller finish time.

* 🔹 This guarantees the earliest overall completion time.

---

## ⏱ Time Complexity

**O(L + W)**

* Where:
    - `L` = number of land rides
    - `W` = number of water rides

* The helper function scans both arrays once, and it is called twice.

---

## 📦 Space Complexity

**O(1)**

* only a few variables are used, no extra data structures.
---

## 💻 Java Code

```java
class Solution {
    public int earliestFinishTime(int[] landStartTime, int[] landDuration, int[] waterStartTime, int[] waterDuration) {
        int landThenWaterTime = calculateSequentialFinishTime(
            landStartTime, landDuration, waterStartTime, waterDuration);

        int waterThenLandTime = calculateSequentialFinishTime(
            waterStartTime, waterDuration, landStartTime, landDuration);

        return Math.min(landThenWaterTime, waterThenLandTime);

    }

    private int calculateSequentialFinishTime(
        int[] firstStartTimes, int[] firstDurations,
        int[] secondStartTimes, int[] secondDurations) {

        int earliestFirstTaskCompletion = Integer.MAX_VALUE;
        for (int i = 0; i < firstStartTimes.length; i++) {
            int taskEndTime = firstStartTimes[i] + firstDurations[i];
            earliestFirstTaskCompletion = Math.min(earliestFirstTaskCompletion, taskEndTime);
        }

        int earliestTotalCompletion = Integer.MAX_VALUE;
        for (int i = 0; i < secondStartTimes.length; i++) {
            int actualSecondTaskStart = Math.max(earliestFirstTaskCompletion, secondStartTimes[i]);
            int totalCompletionTime = actualSecondTaskStart + secondDurations[i];
            earliestTotalCompletion = Math.min(earliestTotalCompletion, totalCompletionTime);
        }

        return earliestTotalCompletion;
    }
}
```

---