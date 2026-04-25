# <u>3464. Maximize the Distance Between Points on a Square</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximize-the-distance-between-points-on-a-square/

---

## 🧠 Intuition:
* 🔹 Since all points lie on the **boundary of a square**, first arrange them in a fixed circular order (left → top → right → bottom) so they can be processed like a sequence instead of 2D points

* 🔹 Our goal is to choose exactly `k` points such that the **minimum Manhattan distance between consecutive chosen points is maximized**

* 🔹 This is an optimization problem, so apply **Binary Search on the answer** (possible minimum distance `d`)

* 🔹 For each candidate distance `d`, check whether it is possible to select at least `k` points with every chosen pair maintaining Manhattan distance ≥ `d`

* 🔹 The `isValidDistance()` function uses a **deque + DP-style sequence tracking** to efficiently store valid previous states and extend the longest valid sequence

* 🔹 Each sequence stores starting point, ending point, and current selected length

* 🔹 If current point can maintain distance ≥ `d` from a previous sequence, extend that sequence and update maximum length

* 🔹 If we can form a sequence of `length ≥ k`, then distance `d` is valid, so try a bigger value; otherwise reduce the search space

* 🔹 Final binary search answer gives the maximum possible minimum distance.

---

## ⏱ Time Complexity

**O(n log n + n log(side))**

* Ordering and sorting boundary points → **O(n log n)**
* Binary Search on answer range (0 to side) → **O(log side)**
* Each validity check using deque traversal → **O(n)**

---

## 📦 Space Complexity

**O(n)**

* Ordered list + deque + helper structures

---

## 💻 Java Code

```java
class Solution {
    public int maxDistance(int side, int[][] points, int k) {
        List<int[]> ordered = getOrderedPoints(side, points);
        int l = 0;
        int r = side;

        while (l < r) {
            final int m = (l + r + 1) / 2;
            if (isValidDistance(ordered, k, m))
                l = m;
            else
                r = m - 1;
        }

        return l;
    }

    private record Sequence(int startX, int startY, int endX, int endY, int length) {}

    private boolean isValidDistance(List<int[]> ordered, int k, int d) {
        Deque<Sequence> dq = new ArrayDeque<>(List.of(new Sequence(
            ordered.get(0)[0], ordered.get(0)[1], ordered.get(0)[0], ordered.get(0)[1], 1)));
        int maxLength = 1;

        for (int i = 1; i < ordered.size(); ++i) {
            final int x = ordered.get(i)[0];
            final int y = ordered.get(i)[1];
            int startX = x;
            int startY = y;
            int length = 1;
            while (!dq.isEmpty() &&
                   (Math.abs(x - dq.peekFirst().endX()) + Math.abs(y - dq.peekFirst().endY()) >= d)) {
                if (Math.abs(x - dq.peekFirst().startX()) + Math.abs(y - dq.peekFirst().startY()) >= d && dq.peekFirst().length() + 1 >= length) {
                    startX = dq.peekFirst().startX();
                    startY = dq.peekFirst().startY();
                    length = dq.peekFirst().length() + 1;
                    maxLength = Math.max(maxLength, length);
                }
                dq.pollFirst();
            }
              
            dq.addLast(new Sequence(startX, startY, x, y, length));
        }

        return maxLength >= k;
    }

    private List<int[]> getOrderedPoints(int side, int[][] points) {
        List<int[]> left = new ArrayList<>();
        List<int[]> top = new ArrayList<>();
        List<int[]> right = new ArrayList<>();
        List<int[]> bottom = new ArrayList<>();

        for (int[] point : points) {
            final int x = point[0];
            final int y = point[1];
            if (x == 0 && y > 0)
                left.add(point);
            else if (x > 0 && y == side)
                top.add(point);
            else if (x == side && y < side)
                right.add(point);
            else
                bottom.add(point);
        }

        left.sort(Comparator.comparingInt(a -> a[1]));
        top.sort(Comparator.comparingInt(a -> a[0]));
        right.sort(Comparator.comparingInt(a -> - a[1]));
        bottom.sort(Comparator.comparingInt(a -> - a[0]));
        List<int[]> ordered = new ArrayList<>();
        ordered.addAll(left);
        ordered.addAll(top);
        ordered.addAll(right);
        ordered.addAll(bottom);
        
        return ordered;
    }
}

```

---