# <u>2515. Shortest Distance to Target String in a Circular Array</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/shortest-distance-to-target-string-in-a-circular-array/

---

## 🧠 Intuition:
* 🔹 The array is **circular**, so we can move **left** or **right** and also wrap around the ends.

* 🔹 We go through each index and check if the word matches the **target**.

* 🔹 For every match, we calculate two distances:
    - **Direct distance** → normal movement: `|currentIndex - startIndex|`
    - **Wrap-around distance** → going the other way: `n - directDistance`

* 🔹 We take the **minimum of these two**, because we want the shortest path in a circular array.

* 🔹 Keep updating the **minimum distance** among all matching indices.

* 🔹 If no match is found, return `-1`, otherwise return the minimum distance.

---

## ⏱ Time Complexity

**O(n)**

* We traverse the array once
    
---

## 📦 Space Complexity

**O(1)**

* Only a few variables are used

---

## 💻 Java Code

```java
class Solution {
    public int closestTarget(String[] words, String target, int startIndex) {
        int arrayLength = words.length;
        int minDistance = arrayLength; // Initialize with maximum possible distance
      
        // Iterate through each word in the array
        for (int currentIndex = 0; currentIndex < arrayLength; ++currentIndex) {
            String currentWord = words[currentIndex];
          
            // Check if current word matches the target
            if (currentWord.equals(target)) {
                // Calculate direct distance from startIndex to currentIndex
                int directDistance = Math.abs(currentIndex - startIndex);
              
                // Calculate wrap-around distance (going the opposite direction in circular array)
                int wrapAroundDistance = arrayLength - directDistance;
              
                // Choose the minimum between direct and wrap-around distance
                int shortestPath = Math.min(directDistance, wrapAroundDistance);
              
                // Update the overall minimum distance
                minDistance = Math.min(minDistance, shortestPath);
            }
        }
      
        // If minDistance hasn't changed from initial value, target wasn't found
        return minDistance == arrayLength ? -1 : minDistance;
    
    }
}
```

---