# <u>1306. Jump Game III</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/jump-game-iii/

---

## 🧠 Intuition:
* 🔹 Treat each index as a node in a graph.
* 🔹 From any index `i`, we can jump to:
    - `i + arr[i]`
    - `i - arr[i]`

* 🔹 Use BFS to explore all reachable indices level by level.

* 🔹 Start BFS from the given `start` index.

* 🔹 If at any point `arr[currentIndex] == 0`, we have reached a valid destination, so return `true`.

* 🔹 To avoid revisiting the same index and getting stuck in cycles:
    - Mark visited indices by changing their value to `-1`.

* 🔹 For every current index:
    - Calculate forward and backward jumps.
    - Add only valid and unvisited indices into the queue.

* 🔹 If BFS finishes without reaching a `0`, return `false`.

* 🔹 BFS guarantees that all reachable positions are explored efficiently.

---

## ⏱ Time Complexity

**O(n)**

* Each index is visited at most once.
    
---

## 📦 Space Complexity

**O(n)**

* Queue may store up to `n` indices in the worst case.

---

## 💻 Java Code

```java
class Solution {
    public boolean canReach(int[] arr, int start) {
        Deque<Integer> queue = new ArrayDeque<>();
        queue.offer(start);
      
        while (!queue.isEmpty()) {
            int currentIndex = queue.poll();
          
            if (arr[currentIndex] == 0) {
                return true;
            }
          
            int jumpDistance = arr[currentIndex];
          
            arr[currentIndex] = -1;
          
            for (int nextIndex : List.of(currentIndex + jumpDistance, currentIndex - jumpDistance)) {
                if (nextIndex >= 0 && nextIndex < arr.length && arr[nextIndex] >= 0) {
                    queue.offer(nextIndex);
                }
            }
        }
      
        return false;
    }
}
```

---