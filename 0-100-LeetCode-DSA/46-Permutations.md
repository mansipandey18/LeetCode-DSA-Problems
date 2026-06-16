# <u>46. Permutations</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/permutations/

---

## 🧠 Intuition:
* 🔹 We need to generate all possible arrangements (permutations) of the given numbers.

* 🔹 Use **Backtracking** to build each permutation one element at a time.

* 🔹 Maintain a `currentPermutation` list to store the current arrangement being formed.

* 🔹 Use a `visited` array to keep track of which elements are already used in the current permutation.

* 🔹 At each recursive step, iterate through all elements:
    - If an element is not visited, choose it and add it to the current permutation.
    - Mark it as visited and recursively build the remaining positions.
    - After recursion, remove the element and mark it as unvisited **(backtrack)** to explore other possibilities.

* 🔹 When the current permutation size becomes equal to the number of elements, a complete permutation is formed.

* 🔹 Add a copy of this permutation to the final answer list.

* 🔹 This process explores every possible ordering of the elements.

---

## ⏱ Time Complexity

**O(n × n!)**

* There are `n!` permutations and copying each permutation takes `O(n)` time.
    
---

## 📦 Space Complexity

**O(n × n!)**

* For storing all generated permutations.

---

## 💻 Java Code

```java
class Solution {
    
    private List<List<Integer>> permutations = new ArrayList<>();    
    private List<Integer> currentPermutation = new ArrayList<>();  
    private boolean[] visited; 
    private int[] elements; 

    public List<List<Integer>> permute(int[] nums) {
        elements = nums;
        visited = new boolean[nums.length];
        backtrack(0);
        return permutations;
    }

    private void backtrack(int index) {
        if (index == elements.length) {
            permutations.add(new ArrayList<>(currentPermutation));
            return;
        }
      
        for (int j = 0; j < elements.length; ++j) {
            if (!visited[j]) {
                visited[j] = true;
                currentPermutation.add(elements[j]);
                backtrack(index + 1);
                currentPermutation.remove(currentPermutation.size() - 1);
                visited[j] = false;
            }
        }
    }
}
```

---