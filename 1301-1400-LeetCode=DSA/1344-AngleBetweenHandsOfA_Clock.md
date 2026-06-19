# <u>1344. Angle Between Hands of a Clock</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/angle-between-hands-of-a-clock/

---

## 🧠 Intuition:
* 🔹 A clock has two hands: the **hour hand and the minute hand**, and we calculate their positions separately.

* 🔹 The hour hand moves **30° for each hour** (`360° / 12 = 30°`) and also moves **0.5° for every minute** because it continuously moves between hours.

* 🔹 The minute hand moves **6° for each minute** (`360° / 60 = 6°`).

* 🔹 Calculate the angle of both hands from the 12 o'clock position.

* 🔹 Find the absolute difference between the two angles.

* 🔹 Since there are always two possible angles between the hands, return the smaller angle by comparing the difference with `360° - difference`.

* 🔹 This approach directly uses mathematical calculations without any simulation.

---

## ⏱ Time Complexity

**O(1)**

* Only a fixed number of arithmetic operations are performed.
    
---

## 📦 Space Complexity

**O(1)**

* No extra space is used.

---

## 💻 Java Code

```java
class Solution {
    public double angleClock(int hour, int minutes) {
        double hourAngle = 30.0 * hour + 0.5 * minutes;
      
        double minuteAngle = 6.0 * minutes;
      
        double angleDifference = Math.abs(hourAngle - minuteAngle);
      
        return Math.min(angleDifference, 360.0 - angleDifference);
    }
}
```

---