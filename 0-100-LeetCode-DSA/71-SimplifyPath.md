# <u>71. Simplify Path</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/simplify-path/

---

## 🧠 Intuition:
* 🔹 The given path may contain extra `/`, current directory `"."`, and parent directory `".."`, so we need to convert it into its **canonical absolute path**

* 🔹 A **stack (Deque)** is ideal because directory navigation follows **Last In, First Out (LIFO)** behavior

* 🔹 Split the path using `"/"` so each part (directory name or symbol) can be processed separately

* 🔹 If the segment is empty `("")` or `"."`, ignore it because:
    - empty comes from multiple slashes like `"//"`
    - `"."` means stay in the current directory

* 🔹 If the segment is `".."`, it means move one directory back, so remove the last directory from the stack if it exists

* 🔹 Otherwise, the segment is a valid directory name, so push it into the stack

* 🔹 After processing all segments, the stack contains only the valid directories in correct order

* 🔹 Join all elements using `"/"` and add a leading slash `"/"` to form the final simplified absolute path

* 🔹 If the stack is empty, the result becomes just `"/"` (root directory)

* 🔹 This approach correctly handles all special path symbols while preserving the correct directory structure
---

## ⏱ Time Complexity

**O(n)**

* Where :
    - `n` = length of the input path

* Splitting the path and processing each segment takes **O(n)**
* Joining the final path also takes **O(n)**   
---

## 📦 Space Complexity

**O(n)**

* Stack stores directory names from the path → **O(n)**

---

## 💻 Java Code

```java
class Solution {
    public String simplifyPath(String path) {
        Deque<String> stack = new ArrayDeque<>();

        for (String segment : path.split("/")) {
            if (segment.isEmpty() || ".".equals(segment)) {
                continue;
            }
            if ("..".equals(segment)) {
                if (!stack.isEmpty()) {
                    stack.pollLast();
                }
            } else {
                stack.offerLast(segment);
            }
        }
      
        String simplifiedPath = "/" + String.join("/", stack);
      
        return simplifiedPath;
    }
}
```

---
