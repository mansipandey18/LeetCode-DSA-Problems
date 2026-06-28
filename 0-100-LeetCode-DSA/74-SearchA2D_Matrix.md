# <u>74. Search a 2D Matrix</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/search-a-2d-matrix/

---

## 🧠 Intuition:
* 🔹 Each row of the matrix is **sorted**, so we can apply **Binary Search** on every row.

* 🔹 Traverse the matrix row by row.

* 🔹 For each row, perform Binary Search to check whether the `target` exists.

* 🔹 If the middle element equals the target, return `true` immediately.

* 🔹 If the middle element is smaller than the target, search in the **right half** of the row.

* 🔹 Otherwise, search in the **left half** of the row.

* 🔹 If the target is not found in any row, return `false`.

---

## ⏱ Time Complexity

**O(m × log n)**

* Binary Search (`O(log n)`) is performed for each of the `m` rows.
    
---

## 📦 Space Complexity

**O(1)**

* Only a few variables are used; no extra space is required

---

## 💻 Java Code

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        for(int i = 0; i < matrix.length; i++){
            // binary search
            int left = 0, right = matrix[0].length-1;

            while(left <= right){
                int mid = (left + right)/2;

                if(matrix[i][mid] == target){
                    return true;
                } 
                if(matrix[i][mid] < target){
                    left = mid + 1;
                } else{
                    right = mid - 1;
                }
            }
        }
        return false;
    }
}
```

---