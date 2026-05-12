# <u>841. Keys and Rooms</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/keys-and-rooms/

---

## 🧠 Intuition:
* 🔹 Treat each room as a node in a graph

* 🔹 Keys inside a room represent edges to other rooms

* 🔹 Initially, only room `0` is unlocked and accessible

* 🔹 Use **Depth First Search (DFS)** to explore all reachable rooms

* 🔹 Maintain a `seen[]` array to track visited rooms

* 🔹 Start DFS from room `0`:
    - Mark the current room as visited
    - Visit every room whose key is available in the current room
    - Skip rooms already visited to avoid repeated traversal

* 🔹 After DFS completes:
    - Check if all rooms were visited
    - If every value in `seen[]` is `1`, then all rooms can be accessed

* 🔹 Otherwise, some rooms remain unreachable

---

## ⏱ Time Complexity

**O(V + E)**

* Where :
    - `V` = number of rooms
    - `E` = total number of keys across all rooms

* Each room is visited once
* Each key is processed once during traversal

    
---

## 📦 Space Complexity

**O(V)**

* `seen[]` array stores visited state for all rooms
* Recursive DFS stack can go up to all rooms in worst case

---

## 💻 Java Code

```java
class Solution {
    public boolean canVisitAllRooms(List<List<Integer>> rooms) {
        int[] seen = new int[rooms.size()];
        dfs(rooms, 0, seen);
        return Arrays.stream(seen).allMatch(a -> a == 1);
    }

    private void dfs(List<List<Integer>> rooms, int node, int[] seen) {
        seen[node] = 1;
        
        for (int child : rooms.get(node))
            if (seen[child] == 0){
                dfs(rooms, child, seen);
            }
    }
}
```

---