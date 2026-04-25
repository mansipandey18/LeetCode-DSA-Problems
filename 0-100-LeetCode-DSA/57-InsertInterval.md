# <u>57. Insert Interval</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/merge-intervals/
---

## 🧠 Intuition:
* 🔹 Since the given intervals are **already sorted and non-overlapping**, we can process them in one pass without sorting again

* 🔹 Divide the work into **3 parts**: before overlap, overlapping part, and after overlap

* 🔹 First, add all intervals that end before `newInterval` starts (`newInterval[0] > intervals[i][1]`) because they cannot overlap

* 🔹 Next, for all intervals that overlap with `newInterval`, merge them by updating:
    - `start` = minimum of both starts
    - `end` = maximum of both ends

* 🔹 This creates one single merged interval covering all overlaps

* 🔹 Add this merged `newInterval` to the result list

* 🔹 Finally, add all remaining intervals that start after the merged interval ends since they also do not overlap

* 🔹 Convert the list into a 2D array and return the final answer

---

## ⏱ Time Complexity

**O(n)**

* Traverse all intervals once → **O(n)**
* Copy list to array → **O(n)**
    
---

## 📦 Space Complexity

**O(n)**

* Result list stores output intervals

---


## 💻 Java Code

```java
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        int i = 0;
        List<int[]> result = new ArrayList<>();

        while(i < intervals.length && newInterval[0] > intervals[i][1]){
            result.add(intervals[i]);
            i++;
        }

        while(i < intervals.length && (intervals[i][1] >= newInterval[0] && newInterval[1] >= intervals[i][0])){
            newInterval[0] = Math.min(newInterval[0], intervals[i][0]);
            newInterval[1] = Math.max(newInterval[1], intervals[i][1]);  

            i++;
        }

        result.add(newInterval);

        while(i < intervals.length){
            result.add(intervals[i]);

            i++;
        }

        int[][] ans = new int[result.size()][2];

        for(int j = 0; j < result.size(); j++){
            ans[j] = result.get(j);
        }
        return ans;
    }
}
```

---