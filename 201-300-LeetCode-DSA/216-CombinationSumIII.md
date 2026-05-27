# <u>216. Combination Sum III</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/combination-sum-iii/

---

## 🧠 Intuition:
* 🔹 We need to find all unique combinations of `k` numbers from `1` to `9` whose sum equals `n`.

* 🔹 Use **Backtracking (DFS)** to explore all possible combinations.

* 🔹 At every step, we have two choices for the current number:
    - Include it in the current combination.
    - Skip it and move to the next number.

* 🔹 Maintain a `currentCombination` list to store the selected numbers.

* 🔹 If `remainingSum` becomes `0` and the combination size equals `k`, store the combination in the result.

* 🔹 Stop recursion early when:
    - Current number exceeds `9`.
    - Current number is greater than the remaining sum.
    - Combination size already becomes greater than or equal to `k`.

* 🔹 After exploring one path, remove the last added number (backtracking) to try other possibilities.

* 🔹 This efficiently generates all valid combinations without duplicates.

---

## ⏱ Time Complexity

**O(2 ^ 9 * k)**

* Each number from 1 to 9 can either be taken or skipped, creating `2⁹` possibilities.
* Copying a valid combination takes `O(k)` time.
    
---

## 📦 Space Complexity

**O(k)**

* Recursive stack and current combination list can hold at most `k` elements.

---

## 💻 Java Code

```java
class Solution {
    private List<List<Integer>> result = new ArrayList<>();
    private List<Integer> currentCombination = new ArrayList<>();
    private int targetSize;

    public List<List<Integer>> combinationSum3(int k, int n) {
        this.targetSize = k;

        dfs(1, n);
        return result;
    }

    private void dfs(int currentNumber, int remainingSum) {
        if (remainingSum == 0) {
            if (currentCombination.size() == targetSize) {
                result.add(new ArrayList<>(currentCombination));
            }
            return;
        }
      
        if (currentNumber > 9 || currentNumber > remainingSum || currentCombination.size() >= targetSize) {
            return;
        }
      
        currentCombination.add(currentNumber);
        dfs(currentNumber + 1, remainingSum - currentNumber);
        currentCombination.remove(currentCombination.size() - 1); // Backtrack
      
        dfs(currentNumber + 1, remainingSum);
    }
} 
```

---