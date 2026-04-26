# <u>933. Number of Recent Calls</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/number-of-recent-calls/

---

## 🧠 Intuition:
* 🔹 We need to return how many requests happened in the time range **[t - 3000, t]** for every new `ping(t)` call

* 🔹 Since all `ping()` calls come in strictly increasing order of time, the timestamps are naturally stored in **sorted order**

* 🔹 Store every incoming timestamp in an array so we can quickly access past requests

* 🔹 For each new `ping(t)`, first add `t` to the array

* 🔹 Then find the **first index** whose value is greater than or equal to `t - 3000`

* 🔹 All timestamps before this index are too old and should not be counted

* 🔹 Since the array is sorted, use **binary search** to efficiently find this first valid index

* 🔹 The answer is simply: **total stored timestamps - firstValidIndex**

* 🔹 This gives the number of recent calls within the last 3000 milliseconds

* 🔹 Using binary search makes counting much faster than checking all previous timestamps every time


---

## ⏱ Time Complexity

**O(log n)**

* Inserting timestamp → **O(1)**
* Binary search to find first valid index → **O(log n)**
    
---

## 📦 Space Complexity

**O(n)**

* Array stores all timestamps received so far → **O(n)**

---

## 💻 Java Code

```java
class RecentCounter {

    private int[] timestamps = new int[10010];
    private int currentIndex;

    public RecentCounter() {
        currentIndex = 0;
    }
    
    public int ping(int t) {
        timestamps[currentIndex++] = t;
      
        int firstValidIndex = binarySearch(t - 3000);
      
        return currentIndex - firstValidIndex;
    }

    private int binarySearch(int target) {
        int left = 0;
        int right = currentIndex;
      
        while (left < right) {
            int mid = (left + right) >> 1;  
          
            if (timestamps[mid] >= target) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
      
        return left;
    }
}
```

---