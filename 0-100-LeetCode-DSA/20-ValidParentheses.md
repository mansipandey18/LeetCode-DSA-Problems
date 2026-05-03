# <u>20. Valid Parentheses</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/valid-parentheses/

---

## 🧠 Intuition:
* 🔹 Valid parentheses means every opening bracket must be closed by the correct type of closing bracket and in the correct order

* 🔹 Since brackets must be matched in **Last In, First Out (LIFO)** order, a **stack** is the best data structure for this problem

* 🔹 Traverse the string character by character

* 🔹 If the current character is an opening bracket `(`, `{`, `[` → push it into the stack

* 🔹 If the current character is a closing bracket `)`, `}`, `]` → it must match the top element of the stack

* 🔹 If the stack is empty when a closing bracket appears, it means no opening bracket exists → return `false`

* 🔹 Check whether the top of the stack forms a valid pair with the current closing bracket
    - If yes → pop the opening bracket from the stack
    - If no → return `false` because brackets are mismatched

* 🔹 After processing the full string, if the stack is empty, all brackets were matched correctly

* 🔹 If the stack still contains elements, some opening brackets were never closed → return `false`

* 🔹 Thus, the string is valid only when every bracket is properly matched and the stack becomes empty at the end

---

## ⏱ Time Complexity

**O(n)**

* Where:
    - `n` = length of string

* Each character is pushed and popped at most once from the stack

---

## 📦 Space Complexity

**O(n)**

* In the worst case, all characters can be opening brackets and stored in the stack


---

## 💻 Java Code

```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> cStack = new Stack<>();

        for(int i = 0; i < s.length(); i++){
             char ch = s.charAt(i);

            //  for opening paraentheses
            if(ch == '(' || ch == '{' || ch == '['){
                cStack.push(ch);
            }
            else{
                // for closing parentheses
                if(cStack.isEmpty()){
                    return false;
                }
                if( (cStack.peek() == '(' && ch == ')') ||
                    (cStack.peek() == '{' && ch == '}') ||
                    (cStack.peek() == '[' && ch == ']') ){
                    cStack.pop();
                } else{
                    return false;
                }
            }
        }
        if(!cStack.isEmpty()){
            return false;
        } else{
            return true;
        }
    }
}
```

---