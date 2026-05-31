# <u>2126. Destroying Asteroids</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/destroying-asteroids/

---

## 🧠 Intuition:
* 🔹 To maximize the chance of destroying all asteroids, always destroy the smallest asteroids first.

* 🔹 Sort the asteroid masses in ascending order.

* 🔹 Maintain a variable `currentMass` representing the planet's current mass.

* 🔹 Traverse the sorted asteroids one by one:
    - If `currentMass < asteroidMass`, the asteroid cannot be destroyed, so return false.
    - Otherwise, destroy the asteroid and absorb its mass: `currentMass += asteroidMass`.

* 🔹 Destroying smaller asteroids first helps the planet grow as quickly as possible, making it easier to destroy larger asteroids later.

* 🔹 If all asteroids are processed successfully, return `true`.

---

## ⏱ Time Complexity

**O(n log n)**

* due to sorting the asteroid array.
  
---

## 📦 Space Complexity

**O(1)**

* only a few extra variables are used (ignoring the space used by the sorting algorithm).

---

## 💻 Java Code

```java
class Solution {
    public boolean asteroidsDestroyed(int mass, int[] asteroids) {
        Arrays.sort(asteroids);
      
        long currentMass = mass;
      
        for (int asteroidMass : asteroids) {
            // Check if current mass is sufficient to destroy this asteroid
            if (currentMass < asteroidMass) {
                return false;  
            }
          
            // Absorb the asteroid's mass after destroying it
            currentMass += asteroidMass;
        }
      
        return true;
    }
}
```

---