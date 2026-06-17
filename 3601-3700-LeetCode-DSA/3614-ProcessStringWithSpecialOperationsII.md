# <u>3614. Process String with Special Operations II</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/process-string-with-special-operations-ii/

---

## 🧠 Intuition:
* 🔹 Directly building the final string can be very expensive because `#` can duplicate the string many times, so we only track the **length of the string after each operation**.

* 🔹 In the forward pass:
    - Maintain the current size `sz` of the processed string.
    - For a lowercase letter, increase the size by `1`.
    - For `*`, decrease the size by `1` if the string is not empty.
    - For `#`, double the current size.
    - For `%`, keep the size unchanged because reversing does not affect length.
    - Store the size after every operation in the `sizes` array.

* 🔹 If `k` is greater than or equal to the final size, the required character does not exist, so return `'.'`.

* 🔹 Traverse the operations in reverse to determine which original character contributes to position `k`.

* 🔹 For each operation:
    - `#`: The string was duplicated, so if `k` is in the second half, map it back to the corresponding index in the first half.
    - `%`: Reverse the index using `k = size - 1 - k`.
    - Lowercase letter: If `k` points to the position where this character was added, return that character.
    - `*`: Skip it because the removed character was already handled by tracking the sizes.

* 🔹 By tracing the index backward instead of constructing the string, we efficiently find the k-th character.


---

## ⏱ Time Complexity

**O(n)**

* One forward pass to calculate sizes and one backward pass to trace the index.

---

## 📦 Space Complexity

**O(n)**

* For storing the size of the processed string after each operation in the sizes array.

---

## 💻 Java Code

```java
class Solution {
    public char processStr(String s, long k) {
        int n = s.length();
        long[] sizes = new long[n];
        long sz = 0;
        
        // Phase 1: Forward pass to track lengths at each step
        for (int i = 0; i < n; i++) {
            char c = s.charAt(i);
            if (c == '*') {
                if (sz > 0) {
                    sz--;
                }
            } else if (c == '#') {
                sz *= 2;
            } else if (c == '%') {
                // Reversing does not change string length
            } else {
                sz++;
            }
            sizes[i] = sz;
        }
        
        // Quick exit if k is completely out of bounds
        if (k >= sz || k < 0) {
            return '.';
        }
        
        // Phase 2: Reverse engineer index k from back to front
        for (int i = n - 1; i >= 0; i--) {
            char c = s.charAt(i);
            sz = sizes[i];
            
            if (c == '*') {
                continue;
            } else if (c == '#') {
                // If k falls in the duplicated right half, map it back to the left half
                long half = sz / 2;
                if (k >= half) {
                    k -= half;
                }
            } else if (c == '%') {
                // Symmetrically mirror the target index
                k = sz - 1 - k;
            } else {
                // If k matches the index of this newly appended character
                if (k == sz - 1) {
                    return c;
                }
            }
        }
        
        return '.';
    }
}
```

---