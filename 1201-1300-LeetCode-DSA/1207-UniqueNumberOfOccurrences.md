# <u>1207. Unique Number of Occurrences</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/unique-number-of-occurrences/

---

## 🧠 Intuition:
* 🔹 First, count how many times each number appears using a **HashMap (number → frequency)**

* 🔹 Now we only care about whether these **frequencies are unique**

* 🔹 So, take all frequency values from the map and put them into a **HashSet**

* 🔹 Since a set stores only unique values, duplicate frequencies will be automatically removed

* 🔹 Finally, compare sizes:
    - If **set size == map size** → all frequencies are unique
    - If not → some frequencies are repeated → return `false`

---

## ⏱ Time Complexity

**O(n)**

* Building frequency map → `O(n)`
* Creating set from values → `O(n)`
    
---

## 📦 Space Complexity

**O(n)**

* HashMap + HashSet → `O(n)`

---

## 💻 Java Code

```java
class Solution {
    public boolean uniqueOccurrences(int[] arr) {
        Map<Integer, Integer> countMap = new HashMap<>();
      
        for (int number : arr) {
            countMap.merge(number, 1, Integer::sum);
        }
      
        Set<Integer> occurrenceSet = new HashSet<>(countMap.values());
      
        return occurrenceSet.size() == countMap.size();

    }
}
```

---