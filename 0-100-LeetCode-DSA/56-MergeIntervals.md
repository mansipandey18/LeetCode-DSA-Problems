# <u>56. Merge Intervals</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/merge-intervals/
---

## 🧠 Intuition:
* 🔹 Overlapping intervals can only be identified easily if intervals are **sorted by start time**, so first sort them

* 🔹 Initialize result list with the **first interval**

* 🔹 Iterate through remaining intervals one by one

* 🔹 For each current interval, compare it with the **last interval in the result list**
  - If `current.start ≤ previous.end` → intervals overlap → **merge them** by updating end = max(end values)
  - Else → no overlap → simply **add current interval** to result

* 🔹 This way, we always maintain a list of **non-overlapping merged intervals**

* 🔹 Finally, convert the list into a 2D array and return

---

## ⏱ Time Complexity

**O(n log n)**

* Sorting intervals → **O(n log n)**
* Traversing intervals → **O(n)**
    
---

## 📦 Space Complexity

**O(n)**

* Result list to store merged intervals (worst case, no overlaps)

---


## 💻 Java Code

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));

        List<int[]> list = new ArrayList<>();

        list.add(intervals[0]);

        for(int i = 1; i < intervals.length; i++){
            int prev[] = list.get(list.size() - 1);
            int curr[] = intervals[i];

            if(curr[0] <= prev[1]){
                prev[0] = Math.min(prev[0], curr[0]);
                prev[1] = Math.max(prev[1], curr[1]);
            } else{
                list.add(intervals[i]);
            }
        }

        int result[][] = new int[list.size()][2];

        for(int i = 0; i < list.size(); i++){
            result[i] = list.get(i);
        }

        return result;
    }
}
```

---