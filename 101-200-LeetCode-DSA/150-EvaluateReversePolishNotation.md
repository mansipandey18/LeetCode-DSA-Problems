# <u>150. Evaluate Reverse Polish Notation</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/evaluate-reverse-polish-notation/

---

## 🧠 Intuition:
* 🔹 In Reverse Polish Notation (Postfix Expression), operators come **after** their operands, so there is no need for brackets or operator precedence handling

* 🔹 Since the most recent operands must be used first when an operator appears, **a stack** is the ideal data structure (LIFO order)

* 🔹 Traverse each token one by one from left to right

* 🔹 If the token is a number:
    - Convert it to integer
    - Push it into the stack

* 🔹 If the token is an operator (`+`, `-`, `*`, `/`):
    - Pop the top two elements from the stack
    - The first popped value becomes the **second operand**
    - The second popped value becomes the **first operand**
    - This order is important for subtraction and division

* 🔹 Perform the operation based on the operator

* 🔹 Push the result back into the stack so it can be used in future calculations

* 🔹 Continue this process until all tokens are processed

* 🔹 At the end, only one element remains in the stack, which is the final evaluated result

* 🔹 Return that final value from the stack

* 🔹 This approach directly simulates postfix evaluation efficiently without converting expressions
---

## ⏱ Time Complexity

**O(n)**

* Where :
    - `n` = length of tokens

* Each token is processed exactly once
* Every push/pop operation on stack takes **O(1)**
    
---

## 📦 Space Complexity

**O(n)**

* In the worst case, the stack may store all operands before operators are processed

---

## 💻 Java Code

```java
class Solution {
    public int evalRPN(String[] tokens) {
        Deque<Integer> stack = new ArrayDeque<>();
      
        for (String token : tokens) {
            if (token.length() > 1 || Character.isDigit(token.charAt(0))) {
                stack.push(Integer.parseInt(token));
            } else {
                int secondOperand = stack.pop();  
                int firstOperand = stack.pop();   
              
                switch (token) {
                    case "+":
                        stack.push(firstOperand + secondOperand);
                        break;
                    case "-":
                        stack.push(firstOperand - secondOperand);
                        break;
                    case "*":
                        stack.push(firstOperand * secondOperand);
                        break;
                    case "/":
                        stack.push(firstOperand / secondOperand);
                        break;
                }
            }
        }
      
        return stack.pop();
    }
}
```

---