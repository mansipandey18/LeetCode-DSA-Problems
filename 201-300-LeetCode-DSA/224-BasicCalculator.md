# <u>224. Basic Calculator</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/basic-calculator/

---

## 🧠 Intuition:
* 🔹 The problem is to evaluate a mathematical expression containing `+`, `-`, parentheses `()`, and integers

* 🔹 Since parentheses change the evaluation order, we use a **stack** to store intermediate states

* 🔹 Maintain two variables during traversal:
    - `result` → stores the current calculated value
    - `currentSign` → keeps track of whether the next number is positive or negative

* 🔹 Traverse the string character by character

* 🔹 If the character is a digit:
    - Build the full number (handle multi-digit numbers)
    - Add it to `result` using the current sign → `result += sign * number`

* 🔹 If the character is `+` or `-`:
    - Update currentSign accordingly (`+1` or `-1`)

* 🔹 If the character is `'('`:
    - Push current `result` and `currentSign` onto the stack (to save outer context)
    - Reset `result = 0` and `currentSign = 1` to evaluate the inner expression independently

* 🔹 If the character is `')'`:
    - First, multiply current `result` with the last saved sign (top of stack)
    - Then add the previous result (next element from stack)
    - This effectively merges the evaluated inner expression back into the outer expression

* 🔹 Continue this process until the entire string is processed

* 🔹 The final `result` holds the evaluated value of the expression

* 🔹 This approach avoids explicit conversion to postfix and directly evaluates using stack + running result.

---

## ⏱ Time Complexity

**O(n)**

* Where: 
    - `n` = length of the string
    
* Each character in the string is processed once
    
---

## 📦 Space Complexity

**O(n)**

* Stack is used to store intermediate results and signs (in worst case for nested parentheses)

---

## 💻 Java Code

```java
class Solution {
    public int calculate(String s) {
        Deque<Integer> stack = new ArrayDeque<>();
      
        int currentSign = 1;      
        int result = 0;
        int length = s.length();
      
        for (int i = 0; i < length; i++) {
            char currentChar = s.charAt(i);
          
            if (Character.isDigit(currentChar)) {
                int startIndex = i;
                int number = 0;
              
                while (startIndex < length && Character.isDigit(s.charAt(startIndex))) {
                    number = number * 10 + (s.charAt(startIndex) - '0');
                    startIndex++;
                }
              
                result += currentSign * number;
              
                i = startIndex - 1;
              
            } else if (currentChar == '+') {
                currentSign = 1;
              
            } else if (currentChar == '-') {
                currentSign = -1;
              
            } else if (currentChar == '(') {
                stack.push(result);
                stack.push(currentSign);
              
                result = 0;
                currentSign = 1;
              
            } else if (currentChar == ')') {
                result = stack.pop() * result + stack.pop();
            }
        }
      
        return result;
    }
}   
```

---