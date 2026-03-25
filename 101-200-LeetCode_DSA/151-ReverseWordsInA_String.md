# <u>151. Reverse Words in a String</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-non-negative-product-in-a-matrix/

---

## 🧠 Intuition:
* 🔹 First, remove leading spaces by moving the start pointer forward.

* 🔹 Remove trailing spaces by moving the end pointer backward.

* 🔹 Traverse the valid part of the string and build a new string using StringBuilder.

* 🔹 While building:
    - Add characters normally.
    - Allow only one space between words (skip extra spaces).

* 🔹 Now we have a clean string with single spaces between words.

* 🔹 Reverse the entire string:
    - This brings words into reverse order.
    - But each word itself becomes reversed.

* 🔹 Traverse the string again word by word.

* 🔹 Reverse each individual word to restore correct character order.

* 🔹 Final result:
    - Words are reversed in order.
    - Extra spaces are removed.
    - Only single spaces remain between words.

---

## ⏱ Time Complexity

**O(n)**

* Let :
    - `n` = length of string

* Removing spaces → O(n)
* Building cleaned string → O(n)
* Reversing whole string → O(n)
* Reversing each word → O(n)
    
---

## 📦 Space Complexity

**O(n)**

* `StringBuilder` stores the processed string..

---

## 💻 Java Code

```java
class Solution {
    public String reverseWords(String s) {
        int start = 0, end = s.length() - 1;

        while(start < s.length()){
            if(s.charAt(start) == ' '){
                start++;
            } else{
                break;
            }
        }

        while(end >= 0){
            if(s.charAt(end) == ' '){
                end--;
            } else{
                break;
            }
        }

        StringBuilder sb = new StringBuilder();

        while(start <= end){
            if(s.charAt(start) != ' '){
                sb.append(s.charAt(start));
                start++;
            } else if(s.charAt(start) == ' '){
                if(sb.charAt(sb.length() - 1) != ' '){
                   sb.append(' '); 
                   start++;
                } else{
                    start++;
                }
            }
        }

        int i = 0, j = sb.length() - 1;

        while(i < j){
            char temp = sb.charAt(i);
            sb.setCharAt(i, sb.charAt(j));
            sb.setCharAt(j, temp);
            
            i++;
            j--;
        }

        int st = 0, e = 0;
        
        while(st < sb.length()){
            while(e < sb.length() && sb.charAt(e) != ' '){
                e++;
            }
            int p1 = st, p2 = e - 1;

            while(p1 < p2){
                char temp = sb.charAt(p1);
                sb.setCharAt(p1, sb.charAt(p2));
                sb.setCharAt(p2, temp);

                p1++;
                p2--;
            }

            st = e + 1;
            e = st;
        }

        return sb.toString();
    }
}
```

---