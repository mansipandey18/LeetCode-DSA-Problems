# <u>1871. Jump Game VII</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/jump-game-vii/

---

## 🧠 Intuition:
* 🔹 We need to determine whether the last index can be reached while only landing on positions containing `'0'`.

* 🔹 From every reachable index j, we can jump to indices in the range `[j + minJump, j + maxJump]`.

* 🔹 Instead of checking all previous indices for every position (which would be expensive), we use a **prefix sum array** to quickly know if any valid reachable index exists in the required range.

* 🔹 `isReachable[i] stores whether index `i` can be reached.

* 🔹 For each index `i` containing `'0'`, compute the valid previous jump range:
    - `leftBound = i - maxJump`
    - `rightBound = i - minJump`

* 🔹 Using prefix sums, we efficiently check if there is at least one reachable index inside this range in **O(1)** time.

* 🔹 If such an index exists, mark `i` as reachable.

* 🔹 Continuously update the prefix sum array so future indices can query reachable positions efficiently.

* 🔹 Finally, return whether the last index is reachable.

---

## ⏱ Time Complexity

**O(n)**

* Each index is processed once, and prefix sum queries take constant time.

---

## 📦 Space Complexity

**O(n)**

* Extra space is used for the `isReachable` array and `prefixSum` array.

---

## 💻 Java Code

```java
class Solution {
    public boolean canReach(String s, int minJump, int maxJump) {
        int n = s.length();
      
        int[] prefixSum = new int[n + 1];
        prefixSum[1] = 1; // Position 0 is reachable (starting position)
      
        boolean[] isReachable = new boolean[n];
        isReachable[0] = true; // Starting position is always reachable
      
        for (int i = 1; i < n; i++) {
            if (s.charAt(i) == '0') {
                int leftBound = Math.max(0, i - maxJump);
                int rightBound = i - minJump;
              
                isReachable[i] = leftBound <= rightBound && 
                                prefixSum[rightBound + 1] - prefixSum[leftBound] > 0;
            }
          
            prefixSum[i + 1] = prefixSum[i] + (isReachable[i] ? 1 : 0);
        }
      
        return isReachable[n - 1];
    
    }
}
```

---