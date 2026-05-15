# <u>399. Evaluate Division</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/evaluate-division/

---

## 🧠 Intuition:
* 🔹 Treat each variable as a node in a graph-like structure using Union-Find (Disjoint Set Union).

* 🔹 `parent` map stores the parent/root of each variable.

* 🔹 `weight` map stores the ratio between a node and its parent.

* 🔹 Initially:
    - Every variable is its own parent.
    - Weight of every variable is `1.0`.

* 🔹 For each equation `a / b = value`:
    - Find the root of `a` and `b`.
    - If they belong to different groups, connect their roots.
    - Update the weight so the mathematical relationship between variables remains valid.

* 🔹 Path Compression in `find()`:
    - While finding the root, compress the path to make future queries faster.
    - Update weights during compression so ratios stay correct.

* 🔹 For each query `x / y`:
    - If either variable does not exist, answer is `-1.0`.
    - If both variables belong to different components, answer is `-1.0`.
    - Otherwise, compute:
        * `x / y = weight[x] / weight[y]`

* 🔹 This efficiently handles connected equations and evaluates division relationships dynamically.

---

## ⏱ Time Complexity

**O((E + Q) * α(N))**

* `E` = number of equations

* `Q` = number of queries

* `α(N)` = inverse Ackermann function (almost constant) due to Union-Find with path compression.

---

## 📦 Space Complexity

**O(N)**

* For storing `parent` and `weight` maps for all variables.

---

## 💻 Java Code

```java
class Solution {

    private Map<String, String> parent;
    private Map<String, Double> weight;

    public double[] calcEquation(List<List<String>> equations, double[] values, List<List<String>> queries) {
        int numEquations = equations.size();
        parent = new HashMap<>();
        weight = new HashMap<>();
      
        for (List<String> equation : equations) {
            String numerator = equation.get(0);
            String denominator = equation.get(1);
            parent.put(numerator, numerator);
            parent.put(denominator, denominator);
            weight.put(numerator, 1.0);
            weight.put(denominator, 1.0);
        }
      
        for (int i = 0; i < numEquations; ++i) {
            List<String> equation = equations.get(i);
            String numerator = equation.get(0);
            String denominator = equation.get(1);
          
            String rootNumerator = find(numerator);
            String rootDenominator = find(denominator);
          
            if (Objects.equals(rootNumerator, rootDenominator)) {
                continue;
            }
          
            parent.put(rootNumerator, rootDenominator);
            weight.put(rootNumerator, weight.get(denominator) * values[i] / weight.get(numerator));
        }
      
        int numQueries = queries.size();
        double[] results = new double[numQueries];
      
        for (int i = 0; i < numQueries; ++i) {
            String dividend = queries.get(i).get(0);
            String divisor = queries.get(i).get(1);
          
            if (!parent.containsKey(dividend) || 
                !parent.containsKey(divisor) || 
                !Objects.equals(find(dividend), find(divisor))) {
                results[i] = -1.0;
            } else {
                results[i] = weight.get(dividend) / weight.get(divisor);
            }
        }
      
        return results;
    
    }

    private String find(String x) {
        if (!Objects.equals(parent.get(x), x)) {
            String originalParent = parent.get(x);
            parent.put(x, find(parent.get(x)));
            weight.put(x, weight.get(x) * weight.get(originalParent));
        }
        return parent.get(x);
    }
}
```

---