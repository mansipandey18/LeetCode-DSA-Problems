# <u>22. Generate Parentheses</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/generate-parentheses/

---

## 🧠 Intuition:
* 🔹 We need to generate all possible **valid combinations of `n` pairs of parentheses**.

* 🔹 Use **Backtracking** to build the string one character at a time while maintaining validity.

* 🔹 Keep track of:
    - `left`: number of opening parentheses `(` remaining to be placed.
    - `right`: number of closing parentheses `)` remaining to be placed.

* 🔹 If both `left` and `right` become `0`, a complete valid combination is formed, so add it to the answer list.

* 🔹 We can always add an opening parenthesis `(` if there are any left to place.

* 🔹 We can add a closing parenthesis `)` only when `left < right`, ensuring that we never place more closing brackets than opening brackets.

* 🔹 After adding a parenthesis, recursively explore the next choices.

* 🔹 After returning from recursion, remove the last character from the `StringBuilder` **(backtracking)** to try other possible combinations.

* 🔹 This approach explores all valid parenthesis arrangements while pruning invalid paths early.

---

## ⏱ Time Complexity

**O(4ⁿ / √n)**

* The number of valid combinations is the nth Catalan number, and generating each valid combination contributes to this complexity.

---

## 📦 Space Complexity

**O(n)**

* For the recursion stack and the StringBuilder used to build the current combination.

---

## 💻 Java Code

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> ans = new ArrayList<>();
        dfs(n, n, new StringBuilder(), ans);
        return ans;
    }

    public void dfs(int left, int right, StringBuilder sb, List<String> ans) {
        if (left == 0 && right == 0) {
          ans.add(sb.toString());
          return;
        }

        if (left > 0) {
          sb.append("(");
          dfs(left - 1, right, sb, ans);
          sb.deleteCharAt(sb.length() - 1);
        }
        if (left < right) {
          sb.append(")");
          dfs(left, right - 1, sb, ans);
          sb.deleteCharAt(sb.length() - 1);
        }
    } 
}
```

---