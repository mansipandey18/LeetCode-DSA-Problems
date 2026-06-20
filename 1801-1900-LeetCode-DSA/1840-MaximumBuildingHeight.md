# <u>1840. Maximum Building Height</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-building-height/

---

## 🧠 Intuition:
* 🔹 The height difference between two adjacent buildings can be at most 1, so each restriction affects the possible heights of nearby buildings.

* 🔹 Store all restrictions in a list and add the mandatory restriction **building 1 with height 0**.

* 🔹 If the last building `n` has no restriction, add a virtual restriction `(n, n - 1)` because the maximum possible height it can reach from building 1 is `n - 1`.

* 🔹 Sort all restrictions based on the building index to process them in order.

* 🔹 Perform a **left-to-right pass** to ensure that each building’s maximum height does not exceed what is reachable from the previous restriction.

* 🔹 Perform a **right-to-left pass** to further adjust heights using the restrictions on the right side, making all restrictions consistent.

* 🔹 After both passes, every pair of adjacent restrictions defines a valid range where the building heights can increase and decrease by at most `1`.

* 🔹 For each pair of restrictions, calculate the highest possible peak between them using the formula:
    - `peakHeight = (leftHeight + rightHeight + distance) / 2`

* 🔹 Keep track of the maximum peak among all segments and return it as the answer.

* 🔹 This approach efficiently propagates height limits from both directions instead of checking every building.

---

## ⏱ Time Complexity

**O(m log m)**

* Let :
    - `m` = number of restrictions

* Add restrictions and sorting : `O(m log m)`
* Left to right traversal :	`O(m)`
* Right to left traversal :	`O(m)`
* Finding maximum peak : `O(m)`

---

## 📦 Space Complexity

**O(m)**

* Extra list is used to store and process all restrictions.

---

## 💻 Java Code

```java
class Solution {
    public int maxBuilding(int n, int[][] restrictions) {
        List<int[]> restrictionList = new ArrayList<>();
      
        restrictionList.addAll(Arrays.asList(restrictions));
      
        restrictionList.add(new int[] {1, 0});
      
        Collections.sort(restrictionList, (a, b) -> a[0] - b[0]);
      
        if (restrictionList.get(restrictionList.size() - 1)[0] != n) {
            restrictionList.add(new int[] {n, n - 1});
        }
      
        int totalRestrictions = restrictionList.size();
      
        for (int i = 1; i < totalRestrictions; ++i) {
            int[] previousRestriction = restrictionList.get(i - 1);
            int[] currentRestriction = restrictionList.get(i);
            int distance = currentRestriction[0] - previousRestriction[0];
            currentRestriction[1] = Math.min(currentRestriction[1], 
                                            previousRestriction[1] + distance);
        }
      
        for (int i = totalRestrictions - 2; i > 0; --i) {
            int[] currentRestriction = restrictionList.get(i);
            int[] nextRestriction = restrictionList.get(i + 1);
            int distance = nextRestriction[0] - currentRestriction[0];
            currentRestriction[1] = Math.min(currentRestriction[1], 
                                            nextRestriction[1] + distance);
        }
      
        int maxHeight = 0;
        for (int i = 0; i < totalRestrictions - 1; ++i) {
            int[] leftRestriction = restrictionList.get(i);
            int[] rightRestriction = restrictionList.get(i + 1);
          
            int distance = rightRestriction[0] - leftRestriction[0];
            int peakHeight = (leftRestriction[1] + rightRestriction[1] + distance) / 2;
            maxHeight = Math.max(maxHeight, peakHeight);
        }
      
        return maxHeight;
    
    }
}
```

---