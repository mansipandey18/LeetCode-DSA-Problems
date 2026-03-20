# <u>3567. Minimum Absolute Difference in Sliding Submatrix
</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/minimum-absolute-difference-in-sliding-submatrix/

---

## 🧠 Intuition:
* 🔹 We must evaluate every possible k × k submatrix in the grid.

* 🔹 Each position in the result matrix corresponds to one sliding window of size k × k.

* 🔹 For every window, we need the minimum absolute difference between any two distinct elements.
 
* 🔹 Comparing all pairs directly would be too slow, so we use sorting to optimize.

* 🔹 Extract all k² elements of the current submatrix into a temporary array.

* 🔹 Sort the elements so that numerically close values become adjacent.
 
* 🔹 After sorting, the minimum absolute difference will always be found between neighboring elements.

* 🔹 Initialize the answer using the difference between maximum and minimum values.
 
* 🔹 Traverse the sorted array and compute differences between consecutive elements.

* 🔹 Skip duplicate values since they do not form distinct pairs.

* 🔹 Store the smallest valid difference for that submatrix in the result grid.
---

## ⏱ Time Complexity

**O((m − k + 1)(n − k + 1) × k^2 log k)**

* Where : 
    - m = number of rows
    - n = number of columns

* Work per submatrix : 
    - Extract elements → O(k^2)
    - Sort k² elements → O(k^2 log(k^2)) = O(k^2 log k)
    - Scan adjacent differences → O(k^2)

* Number of submatrices
    - (m − k + 1)(n − k + 1)

---

## 📦 Space Complexity

**O(k^2)**

* Temporary array temp of size k^2.
   - (Result array not counted as auxiliary space.)

---

## 💻 Java Code

```java
class Solution {
    public int[][] minAbsDiff(int[][] grid, int k) {
        int [][]res = new int[grid.length-k+1][grid[0].length-k+1];
        for(int i=k-1; i<grid.length; i++) {
            for(int j=k-1;j<grid[0].length;j++) {
                int []temp = new int[k*k];
                for(int ii=i-k+1;ii<=i;ii++) {
                    for(int jj=j-k+1;jj<=j;jj++) {
                        temp[(ii-(i-k+1))*k + (jj-(j-k+1))] = grid[ii][jj];
                    }
                }
                Arrays.sort(temp);
                res[i-(k-1)][j-(k-1)] = temp[temp.length-1] - temp[0];
                for(int kk=1; kk<temp.length; kk++) {
                    if(temp[kk]==temp[kk-1]) {
                        continue;
                    }
                    res[i-(k-1)][j-(k-1)] = Math.min(res[i-(k-1)][j-(k-1)], temp[kk]-temp[kk-1]);
                }
            }
        }
        return res;
    }
}
```

---