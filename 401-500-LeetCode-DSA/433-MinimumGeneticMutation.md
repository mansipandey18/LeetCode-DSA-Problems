# <u>433. Minimum Genetic Mutation</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/minimum-genetic-mutation/

---

## 🧠 Intuition:
* 🔹 Each gene string can be treated as **a node**, and a valid mutation represents an edge between two nodes.

* 🔹 We need the **minimum number of mutations**, which makes this a **shortest path problem**.

* 🔹 Use BFS starting from `startGene` because BFS finds the shortest path in an unweighted graph.

* 🔹 For every gene removed from the queue, compare it with all genes in the `bank`.

* 🔹 A gene is considered reachable if it differs by **exactly one character** from the current gene.

* 🔹 Valid unvisited genes are added to the queue and marked as visited.

* 🔹 BFS processes genes level by level, where each level represents one mutation step.

* 🔹 If `endGene` is reached, return the current number of mutation steps.

* 🔹 If BFS finishes without reaching `endGene`, return `-1`.

---

## ⏱ Time Complexity

**O(n^2)**

* Where :
    - `n` = size of the bank

* For each gene, we may compare it with all genes in the bank, and each comparison checks 8 characters.
    
---

## 📦 Space Complexity

**O(n)**

* Queue stores genes for BFS → `O(n)`
* Visited set stores processed genes → `O(n)`

---

## 💻 Java Code

```java
class Solution {
    public int minMutation(String startGene, String endGene, String[] bank) {
        Deque<String> queue = new ArrayDeque<>();
        queue.offer(startGene);
      
        Set<String> visited = new HashSet<>();
        visited.add(startGene);
      
        int mutationSteps = 0;
      
        while (!queue.isEmpty()) {
            int levelSize = queue.size();
            for (int i = 0; i < levelSize; i++) {
                String currentGene = queue.poll();
              
                if (currentGene.equals(endGene)) {
                    return mutationSteps;
                }
              
                for (String candidateGene : bank) {
                    int allowedDifferences = 2;  

                    for (int j = 0; j < 8 && allowedDifferences > 0; j++) {
                        if (currentGene.charAt(j) != candidateGene.charAt(j)) {
                            allowedDifferences--;
                        }
                    }
                  
                    if (allowedDifferences > 0 && !visited.contains(candidateGene)) {
                        queue.offer(candidateGene);
                        visited.add(candidateGene);
                    }
                }
            }
            mutationSteps++;
        }
      
        return -1;
    }
}
```

---