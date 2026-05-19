# <u>2336. Smallest Number in Infinite Set</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/smallest-number-in-infinite-set/

---

## 🧠 Intuition:
* 🔹 Use a `TreeSet` to maintain all currently available numbers in sorted order.

* 🔹 Initially add numbers from `1` to `1000` into the set to simulate the infinite set constraint within problem limits.

* 🔹 `TreeSet` automatically keeps elements sorted and unique.

* 🔹 `popSmallest()`:
    - Remove and return the smallest available number using `pollFirst()`.

* 🔹 `addBack(num)`:
    - Reinsert the number into the set if it was removed earlier.
    - Since `TreeSet` stores unique values, duplicate insertions are ignored automatically.

* 🔹 This approach efficiently supports:
    - Getting the minimum element.
    - Re-adding removed elements.

---

## ⏱ Time Complexity

**`popSmallest() → `O(log n)`**
**`addBack(num) → `O(log n)`**

---

## 📦 Space Complexity

**O(n)**

* TreeSet stores available numbers.

---

## 💻 Java Code

```java
class SmallestInfiniteSet {
    private TreeSet<Integer> availableNumbers = new TreeSet<>();

    public SmallestInfiniteSet() {
        for (int i = 1; i <= 1000; i++) {
            availableNumbers.add(i);
        }
    }
    
    public int popSmallest() {
        return availableNumbers.pollFirst();
    }
    
    public void addBack(int num) {
        availableNumbers.add(num);
    }
}
```

---