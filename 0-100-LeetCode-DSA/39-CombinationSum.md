# <u>39. Combination Sum</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/combination-sum/

---

## 🧠 Intuition:
* 🔹 We need to find all unique combinations of numbers whose sum equals the target.

* 🔹 Use **Backtracking** to explore all possible choices by deciding whether to **take or skip** each candidate.

* 🔹 First, sort the array so that we can stop early when the remaining target becomes smaller than the current candidate.

* 🔹 At each recursive step, there are two choices:
    - **Skip the current number** and move to the next candidate.
    - **Take the current number**, add it to the current combination, and continue with the same index because a number can be used multiple times.

* 🔹 If the remaining sum becomes `0`, we have found a valid combination, so store a copy of the current combination.

* 🔹 If we reach the end of the candidates array or the current candidate is greater than the remaining sum, stop exploring that path.

* 🔹 After choosing a number, remove it from the current combination (**backtracking**) to try other possible combinations.

* 🔹 This approach explores all possible valid combinations while avoiding unnecessary paths using sorting and pruning.

---

## ⏱ Time Complexity

**O(2^(target/minCandidate))**

* Exponential in the worst case due to exploring multiple combinations.

---

## 📦 Space Complexity

**O(target / minCandidate)**

* Maximum depth of recursion and size of the current combination.

---

## 💻 Java Code

```java
class Solution {
    private List<List<Integer>> combinations = new ArrayList<>(); 
    private List<Integer> currentCombination = new ArrayList<>(); 
    private int[] candidateNumbers; 

    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        Arrays.sort(candidates); 
        this.candidateNumbers = candidates; 

        backtrack(0, target);
        return combinations;
    }

    private void backtrack(int startIndex, int remainingSum) {
        if (remainingSum == 0) {
            combinations.add(new ArrayList<>(currentCombination));
            return;
        }
        if (startIndex >= candidateNumbers.length || remainingSum < candidateNumbers[startIndex]) {
            return;
        }
      
        backtrack(startIndex + 1, remainingSum);

        currentCombination.add(candidateNumbers[startIndex]);
        backtrack(startIndex, remainingSum - candidateNumbers[startIndex]);
        currentCombination.remove(currentCombination.size() - 1);
    }
}
```

---