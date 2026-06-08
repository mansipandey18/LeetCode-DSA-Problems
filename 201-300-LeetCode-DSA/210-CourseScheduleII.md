# <u>210. Course Schedule II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/course-schedule-ii/

---

## 🧠 Intuition:
* 🔹 The problem requires finding a valid order to complete courses → this is a **topological sorting problem** on a directed graph.

* 🔹 Each course is treated as a node, and prerequisites form **directed edges (u → v)**.

* 🔹 We build:
    - An **adjacency list (`graph`)** to store dependencies.
    - An **in-degree array (`inDegrees`)** to track how many prerequisites each course has.

* 🔹 Courses with **0 in-degree** (no prerequisites) are added to a queue initially.

* 🔹 We process nodes using **BFS (Kahn’s Algorithm)**:
    - Remove a node from the queue and add it to the result list.
    - Reduce in-degree of its neighbors.
    - If a neighbor’s in-degree becomes 0, add it to the queue.

* 🔹 This ensures we always pick courses that are currently valid to take.

* 🔹 If we are able to process all courses, we return the ordering.

* 🔹 If not, it means there is a cycle, so no valid ordering exists.
---

## ⏱ Time Complexity

**O(V + E)**

* Building graph + in-degree array → `O(V + E)`
* BFS traversal → `O(V + E)`

---

## 📦 Space Complexity

**O(V + E)**

* Graph (adjacency list) → `O(V + E)`
* In-degree array → `O(V)`
* Queue + result list → `O(V)`

---

## 💻 Java Code

```java
class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        List<Integer> ans = new ArrayList<>();
        List<Integer>[] graph = new List[numCourses];
        int[] inDegrees = new int[numCourses];

        for (int i = 0; i < numCourses; ++i)
          graph[i] = new ArrayList<>();

        // Build the graph.
        for (int[] prerequisite : prerequisites) {
          int u = prerequisite[1];
          int v = prerequisite[0];
          graph[u].add(v);
          ++inDegrees[v];
        }

        // Perform topological sorting.
        Queue<Integer> q = IntStream.range(0, numCourses)
                               .filter(i -> inDegrees[i] == 0)
                               .boxed()
                               .collect(Collectors.toCollection(ArrayDeque::new));

        while (!q.isEmpty()) {
          int u = q.poll();
          ans.add(u);
          for (int v : graph[u])
            if (--inDegrees[v] == 0)
              q.offer(v);
        }

        if (ans.size() == numCourses)
          return ans.stream().mapToInt(Integer::intValue).toArray();
        return new int[] {};

    }
}
```

---