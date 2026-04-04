# <u>03. Longest Substring Without Repeating Characters</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/longest-substring-without-repeating-characters/

---

## 🧠 Intuition:
* 🔹 The problem asks for the **length of the longest substring without repeating characters**.

* 🔹 Use the **Sliding Window technique** with two pointers:
    - `i` → start of window
    - `j` → end of window


* 🔹 Maintain a **HashMap** to store each character’s **latest index**.

* 🔹 Expand the window by moving `j` forward one character at a time.

* 🔹 For every character `ch` at index `j`:
    - If `ch` already exists in the **map and lies inside the current window** `(map.get(ch) ≥ i)`, it means a duplicate is found.
    - Move the start pointer `i` to **one position after the previous occurrence** to remove duplication.

* 🔹 Update the latest index of the character in the map.

* 🔹 Calculate current window length using `(j - i + 1)` and update maximum length.

* 🔹 Continue expanding until the string ends.

* 🔹 The window always maintains **unique characters only**, ensuring optimal traversal.


---

## ⏱ Time Complexity

**O(n)**

* Where : 
    - `n = s.length()`

* Each character is processed at most once by `j`.
* Pointer `i` only moves forward (never backward).

---

## 📦 Space Complexity

**O(n)**


* Where : 
    - `n = string length`

* HashMap stores at most all unique characters of the string.

---

## 💻 Java Code

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int max = 0;
        int i = 0, j = 0;

        Map<Character, Integer> map = new HashMap<>();

        while(j < s.length()){
            char ch = s.charAt(j);

            if(map.containsKey(ch)){
                if(map.get(ch) >= i){             
                    i = map.get(ch) + 1;
                }
            }

            map.put(ch, j);
            max = Math.max(max, j - i + 1);
            j++;
        }

        return max;
    }
}

```

---
