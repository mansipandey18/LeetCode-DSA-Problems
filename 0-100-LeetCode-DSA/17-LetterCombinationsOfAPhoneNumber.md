# <u>17. Letter Combinations of a Phone Number</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/letter-combinations-of-a-phone-number/

---

## 🧠 Intuition:
* 🔹 Each digit on the phone keypad maps to a set of characters (like `2 → "abc"`).

* 🔹 The task is to generate all possible letter combinations formed by the given digits.

* 🔹 Use **Recursion + Backtracking** to try every possible character for each digit.

* 🔹 At every recursive call:
    - Pick the current digit.
    - Get its mapped string of characters.
    - Try each character one by one and append it to the current combination.

* 🔹 Move to the next digit recursively until all digits are processed.

* 🔹 When the current combination length becomes equal to the digits length, store it in the answer list.

* 🔹 This forms a recursion tree where each level represents one digit and branches represent possible letters.

* 🔹 If the input string is empty, return an empty list directly.

---

## ⏱ Time Complexity

**O(4^n * n)**

* Each digit can generate up to 4 choices (`7` and `9`), and creating each string takes `O(n)` time.
    
---

## 📦 Space Complexity

**O(n)**

* Recursive stack depth can go up to `n`.
* Output storage is not included in auxiliary space.

---

## 💻 Java Code

```java
class Solution {
    static void rec(int i, String digits, String mp[], String res, List<String> ans){
        if(i == digits.length()){
            ans.add(res);
            return;
        }

        char ch = digits.charAt(i);
        int num = ch - '0';

        String st = mp[num];

        for(int j = 0; j < st.length(); j++){
            rec(i+1, digits, mp, res+st.charAt(j), ans);
        }
    }
    
    public List<String> letterCombinations(String digits) {
        List<String> ans = new ArrayList<>();

        if(digits.length() == 0){
            return ans;
        }

        String mp[] = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};

        rec(0, digits, mp, "", ans);
        return ans;
    }
}
```

---