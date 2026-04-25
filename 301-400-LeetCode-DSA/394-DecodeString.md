# <u>394. Decode String</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/decode-string/

---

## 🧠 Intuition:
* 🔹 The string contains nested patterns like `k[encoded_string]`, where the substring inside brackets must be repeated k times

* 🔹 A **stack** helps process nested brackets from inside to outside because the innermost substring should be decoded first

* 🔹 Traverse the string character by character

* 🔹 If the current character is not `']'`, simply push it into the stack

* 🔹 When `']'` is found, it means one complete encoded part is ready to decode

* 🔹 First, pop characters until `'['` is found to get the substring that needs to be repeated

* 🔹 Remove `'['` from the stack

* 🔹 Then pop digits before `'['` to get the repetition count (`k`)

* 🔹 Repeat the extracted substring `k` times and push it back into the stack character by character

* 🔹 This allows nested patterns like `"3[a2[c]]"` to be handled correctly because inner parts are decoded first

* 🔹 After full traversal, the stack contains the final decoded string

* 🔹 Pop all characters, reverse them, and return the answer

---

## ⏱ Time Complexity

**O(n + decoded string length)**

* Each character is pushed and popped from the stack, but repeated strings may increase total operations based on final decoded output size

---

## 📦 Space Complexity

**O(n + decoded output size)**

* Stack stores characters of the decoded string and intermediate states

---

## 💻 Java Code

```java
class Solution {
    public String decodeString(String s) {
        Stack<Character> st = new Stack<>();

        for(int i = 0; i < s.length(); i++){
            char ch = s.charAt(i);

            if(ch != ']'){
                st.push(ch);
            } else{
                // get a String until we see '['
                StringBuilder sb = new StringBuilder();
                while(st.size() > 0 && st.peek() != '['){
                    sb.insert(0, st.pop());
                }

                String toRepeat = sb.toString();
                st.pop(); // removing '['

                // get the number before '['
                sb = new StringBuilder();
                while(st.size() > 0 && st.peek() >= '0' && st.peek() <= '9'){
                   sb.insert(0, st.pop());
                }

                int count = Integer.parseInt(sb.toString());
                // repeat the string "count" times and push in stack
                while(count-- > 0){
                    for(int j = 0; j < toRepeat.length(); j++){
                        char c = toRepeat.charAt(j);
                        st.push(c);
                    }
                }
            }
        }

        StringBuilder ans = new StringBuilder();

        while(st.size() > 0){
            ans.append(st.pop());
        }
        ans.reverse();
        return ans.toString();
    }
}
```

---