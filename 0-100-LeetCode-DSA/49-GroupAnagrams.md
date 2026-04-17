# <u>49. Group Anagrams</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/group-anagrams/

---

## 🧠 Intuition:
* 🔹 Anagrams have the **same characters, just in different order**.

* 🔹 So idea is: **convert each word into a common form (key)** so all its anagrams match.

* 🔹 For each string:
    - Convert it to a char array and **sort the characters** → this becomes the key
    - Example: `"eat"`, `"tea"` → both become `"aet"`

* 🔹 Use a HashMap where:
    - `key` = sorted string
    - `value` = list of original words having that key

* 🔹 If key already exists → add word to that list

* 🔹 Otherwise → create a new list

* 🔹 At the end, all values of the map are **groups of anagrams**.

---

## ⏱ Time Complexity

**O(n * klogk)**

* Sorting each string of length `k` takes `O(k log k)`
* For `n` strings
    
---

## 📦 Space Complexity

**O(n * k)**

* HashMap storing all strings

---

## 💻 Java Code

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        if(strs == null || strs.length == 0){
            return new ArrayList<>();
        }
        HashMap<String, List<String>> map = new HashMap<>();
        for(String s : strs){
            char chArr[] = s.toCharArray();
            Arrays.sort(chArr);

            String key = new String(chArr);
            if(!map.containsKey(key)){
                map.put(key, new ArrayList<>());
            }
            map.get(key).add(s);
        }
        return new ArrayList<>(map.values());
    }
}
```

---