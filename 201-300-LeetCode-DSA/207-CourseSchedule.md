# <u>207. Course Schedule</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/course-schedule/

---

## 🧠 Intuition:
* 🔹 The problem is about checking whether we can finish all courses → this reduces to **detecting a cycle in a directed graph**.

* 🔹 Each course is treated as a node, and each prerequisite relation forms a **directed edge (u → v)**.

* 🔹 We build an adjacency list (`graph`) to represent dependencies between courses.

* 🔹 We use a DFS-based cycle detection approach with 3 states:
    - `INIT` → node not visited yet
    - `VISITING` → node is currently in recursion stack
    - `VISITED` → node and all its descendants are fully processed

* 🔹 During DFS:
    - If we reach a `VISITING` node again → **cycle detected** (impossible to finish courses).
    - If a node is already `VISITED`, we skip it.

* 🔹 We recursively explore all neighbors of each course.

* 🔹 If no cycle is found in any DFS traversal, then all courses can be completed.

---

## ⏱ Time Complexity

**O(V + E)**

* Where : 
    - `V` = number of courses.
    - `E` = number of prerequisites

* Each node (course) is visited at most once → `O(V + E)`
    
---

## 📦 Space Complexity

**O(V + E)**

* Adjacency list → `O(V + E)`
* State array → `O(V)`
* Recursion stack (worst case) → `O(V)`

---

## 💻 Java Code

```java
enum State { INIT, VISITING, VISITED }

class Solution {

    public boolean canFinish(int numCourses, int[][] prerequisites) {
        List<Integer>[] graph = new List[numCourses];
        State[] states = new State[numCourses];

        for (int i = 0; i < numCourses; ++i)
          graph[i] = new ArrayList<>();

        for (int[] prerequisite : prerequisites) {
          final int u = prerequisite[1];
          final int v = prerequisite[0];
          graph[u].add(v);
        }

        for (int i = 0; i < numCourses; ++i)
          if (hasCycle(graph, i, states))
            return false;

        return true;
    }

    private boolean hasCycle(List<Integer>[] graph, int u, State[] states) {
        if (states[u] == State.VISITING)
          return true;
        if (states[u] == State.VISITED)
          return false;
        states[u] = State.VISITING;
        for (final int v : graph[u])
          if (hasCycle(graph, v, states))
            return true;
        states[u] = State.VISITED;
        return false;
    }
}   
```

---