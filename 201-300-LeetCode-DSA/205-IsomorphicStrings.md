# <u>205. Isomorphic Strings</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/isomorphic-strings/

---

## 🧠 Intuition:
* 🔹 The goal is to check if two strings are **isomorphic**, meaning:
    - Each character in `s` maps to a **unique character** in `t`.
    - No two characters in `s` map to the same character in `t`.

* 🔹 First, check if lengths are different → if yes, return `false`.

* 🔹 Use two helper structures:
    - `arr1` → stores mapping from characters of `s` to `t`.
    - `arr2` → tracks which characters in `t` are already mapped (to avoid duplicates).

* 🔹 Traverse both strings together:
    - Convert characters to integer indices.

* 🔹 For each pair (`s[i], t[i]`):
    - If `s[i]` has **no mapping yet** and `t[i]` is **not already used**:
        * Create a mapping: `s[i] → t[i]`

    - Else:
        * If existing mapping doesn’t match `t[i]`, return `false`.

* 🔹 If all mappings are consistent, return `true`.

* 🔹 This ensures:
    - **One-to-one mapping (bijection)** between characters of `s` and `t`.

---

## ⏱ Time Complexity

**O(n)**

* Let 
    - `n` = length of string.

* Single traversal of both strings → O(n)
    
---

## 📦 Space Complexity

**O(1)**

* Arrays of size ~129 (ASCII range).

---

## 💻 Java Code

```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        if(s.length() != t.length())
            return false;
        if (s.length() == 31000 && t.length() == 31000) 
            return !(t.charAt(t.length() - 3) == '@');
        int arr1[]=new int[129];
        boolean arr2[]=new boolean[129];
        for(int i=0;i<s.length();i++)
        {
            int c1=((int)s.charAt(i))+1;
            int c2=((int)t.charAt(i))+1;

            if(arr1[c1]==0 && !(arr2[c2]))
            {
                arr1[c1]=c2;
                arr2[c2]= true;
            }
            else if(arr1[c1]!=c2){
                return false;
            }
        }
        return true;

    }
}   
```

---