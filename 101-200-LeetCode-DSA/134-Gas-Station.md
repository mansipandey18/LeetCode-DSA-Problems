# <u>134. Gas Station</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/gas-station/

---

## 🧠 Intuition:
* 🔹 At every station, we calculate the net fuel gain/loss as gas[i] − cost[i].

* 🔹 The journey is possible only if the total gas ≥ total cost overall.

* 🔹 We simulate traveling around the circular route while maintaining a running fuel balance (sum).

* 🔹 Two pointers are used:

   - end → moves forward to extend the journey.

   - start → moves backward when fuel becomes insufficient.

* 🔹 As we move end, we keep adding fuel difference to check if the journey can continue.

* 🔹 If the fuel balance becomes negative:

   - The current starting point cannot complete the trip.

   - We include one more station before the current start (move start backward) to gain extra fuel.

* 🔹 Each station is considered only once while expanding either forward or backward.

* 🔹 After checking all stations:

   - If total fuel balance is non-negative → start is a valid starting station.

   - Otherwise → completing the circuit is impossible.

---

## ⏱ Time Complexity

**O(n)**

 - Each station is visited at most once by either pointer.

 - No station is processed repeatedly.

---

## 📦 Space Complexity

**O(1)**
  
 - Only a few variables are used (`start`, `end`, `sum`, `stationsChecked`).

---

## 💻 Java Code

```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int n = gas.length;

        int start = n - 1, end = n - 1;   

        int sum = 0, stationsChecked = 0;

        while (stationsChecked < n) {
            sum += gas[end] - cost[end];
            stationsChecked++; 
            end = (end + 1) % n; 

            while (sum < 0 && stationsChecked < n) {
                start--; 
                sum += gas[start] - cost[start]; 
                stationsChecked++; 
            }
        }

        return sum >= 0 ? start : -1;
    }
}
```

---