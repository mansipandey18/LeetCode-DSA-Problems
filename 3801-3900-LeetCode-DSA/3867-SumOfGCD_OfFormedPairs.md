# <u>3867. Sum of GCD of Formed Pairs</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/sum-of-gcd-of-formed-pairs/

---

## 🧠 Intuition:
* 🔹 Traverse the array from left to right while maintaining the **maximum value seen so far (`mx`)**.

* 🔹 For each element `nums[i]`, compute `gcd(nums[i], mx)` and store it in `prefixGcd[i]`.

* 🔹 This creates a transformed array where each position represents the GCD between the current element and the running maximum up to that point.

* 🔹 Sort the `prefixGcd` array so that smaller values are grouped together and larger values are grouped together.

* 🔹 Form pairs by taking one element from the beginning and one from the end of the sorted array: `(prefixGcd[0], prefixGcd[n-1]), (prefixGcd[1], prefixGcd[n-2])`, and so on.

* 🔹 For each pair, compute their **GCD** and add it to the answer.

* 🔹 Continue until all possible pairs are processed (only `n/2` pairs are considered).

* 🔹 Use the **Euclidean Algorithm** in the helper function `gcd(a, b)` to compute GCD efficiently.

---

## ⏱ Time Complexity

**O(n log n + n log M)**

* Where : 
    - `n` = length of array.
    - `M` = maximum value in `nums`.

* Sorting takes `O(n log n)`, 
* all `GCD` computations together take `O(n log M)`
    
---

## 📦 Space Complexity

**O(n)**

* for the `prefixGcd` array used to store the transformed values.

---

## 💻 Java Code

```java
class Solution {
    public long gcdSum(int[] nums) {
        int n = nums.length;
        int[] prefixGcd = new int[n];
        int mx = 0;

        for (int i = 0; i < n; i++) {
            int x = nums[i];

            mx = Math.max(mx, x);
            prefixGcd[i] = gcd(x, mx);
        }

        Arrays.sort(prefixGcd);

        long ans = 0;
        for (int i = 0; i < n / 2; i++) {
            ans += gcd(prefixGcd[i], prefixGcd[n - i - 1]);
        }

        return ans;
    }
    private int gcd(int a, int b) {
        while (b != 0) {
            int t = a % b; 
            a = b;         
            b = t;         
        }
        return a;
    }
}
```

---