# <u>3514. Number of Unique XOR Triplets II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/number-of-unique-xor-triplets-ii/

---

## 🧠 Intuition:
* 🔹 Instead of checking every possible triplet directly, first compute all **unique XOR values** of every pair of elements.

* 🔹 Use a boolean array (`freq`) to mark which pairwise XOR values have already been seen, avoiding duplicates.

* 🔹 Store all distinct pairwise XOR values in a separate array (`nums`).

* 🔹 Reset the boolean array and combine each unique pair XOR with every array element:
    - Compute `pairXor ^ arr[j]`, which represents the XOR of a triplet.
    - Mark the resulting XOR value as present.

* 🔹 After processing all combinations, count how many XOR values are marked as `true`.

* 🔹 This reduces redundant computations because each distinct pair XOR is processed only once before extending it to triplets.

---

## ⏱ Time Complexity

**O(n² + U × n)**

* Where:
    - `n` is the size of the array.
    - `U` is the number of unique pairwise XOR values (`U ≤ 2048`).
* In the worst case, this becomes **O(n² + 2048 × n)**, which is effectively **O(n²)**.

---

## 📦 Space Complexity

**O(U + 2048)**

* `O(U)` for storing unique pair XOR values and a fixed-size boolean array (`2048`), which is treated as **constant space**. Hence, the overall auxiliary space is **O(U)** (or **O(1)** if `2048` is considered a fixed constant).

---

## 💻 Java Code

```java
class Solution {
    public static int uniqueXorTriplets(int[] arr) {
        int n = arr.length;
        boolean[] freq = new boolean[2048];
        int len = 0, idx = 0, ans = 0;

        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                if (!freq[arr[i] ^ arr[j]])
                    len++;
                freq[arr[i] ^ arr[j]] = true;
            }
        }

        int[] nums = new int[len];

        for (int i = 0; i < 2048; i++)
            if (freq[i])
                nums[idx++] = i;

        Arrays.fill(freq, false);

        for (int i = 0; i < len; i++) {
            for (int j = 0; j < n; j++)
                freq[nums[i] ^ arr[j]] = true;
        }

        for (boolean b : freq)
            if (b)
                ans++;

        return ans;
    }

}
```

---