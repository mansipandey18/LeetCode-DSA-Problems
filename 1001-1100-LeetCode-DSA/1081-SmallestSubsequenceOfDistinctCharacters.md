# <u>1081. Smallest Subsequence of Distinct Characters</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/smallest-subsequence-of-distinct-characters/

---

## 🧠 Intuition:
* 🔹 Count the frequency of every character so we know whether it will appear again later.

* 🔹 Use a **stack** to build the answer while maintaining the smallest lexicographical order.

* 🔹 Maintain a `visited` (`isInStack`) array to ensure each character is added only once.

* 🔹 For each character:
    - Decrease its remaining frequency since it has been processed.
    - If it is already in the stack, skip it.
    - Otherwise, while the stack is not empty, the current character is **lexicographically smaller** than the top of the stack, and the top character appears again later, remove the top character from the stack.

* 🔹 Push the current character into the stack and mark it as visited.

* 🔹 At the end, the stack contains every distinct character exactly once in the **smallest lexicographical order**.


---

## ⏱ Time Complexity

**O(n)**

* Each character is pushed onto and popped from the stack at most once.
    
---

## 📦 Space Complexity

**O(n)**

* The stack can store up to `n` characters. (The frequency and visited arrays are of fixed size `26`, so they use **O(1)** extra space.)

---

## 💻 Java Code

```java
class Solution {
    public String smallestSubsequence(String s) {
        int[] charFrequency = new int[26];
        for (char c : s.toCharArray()) {
            charFrequency[c - 'a']++;
        }
      
        boolean[] isInStack = new boolean[26];
      
        char[] stack = new char[s.length()];
        int stackTop = -1;
      
        for (char currentChar : s.toCharArray()) {
            charFrequency[currentChar - 'a']--;
          
            if (!isInStack[currentChar - 'a']) {
                while (stackTop >= 0 && currentChar < stack[stackTop] && 
                       charFrequency[stack[stackTop] - 'a'] > 0) {
                    
                    isInStack[stack[stackTop] - 'a'] = false;
                    stackTop--;
                }
              
                stack[++stackTop] = currentChar;
                isInStack[currentChar - 'a'] = true;
            }
        }
      
        return String.valueOf(stack, 0, stackTop + 1);
    
    }
}
```

---