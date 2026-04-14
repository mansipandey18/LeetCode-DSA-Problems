# <u>1456. Maximum Number of Vowels in a Substring of Given Length</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/maximum-number-of-vowels-in-a-substring-of-given-length/

---

## 🧠 Intuition:
* 🔹 We need to find a substring of size `k` that has **maximum vowels**.

* 🔹 Instead of checking every substring again and again, we use a **sliding window** of size `k`.

* 🔹 First, we count vowels in the **first window (0 → k-1)**.

* 🔹 Then we **slide the window one step right** each time:
    - Add the new character (right side) → if it’s a vowel, increase count
    - Remove the old character (left side) → if it’s a vowel, decrease count

* 🔹 This way, we **reuse previous computation** instead of recalculating from scratch.

* 🔹 After each step, update the **maximum vowel count**.

* 🔹 Finally, return the maximum value found.


---

## ⏱ Time Complexity

**O(n)**

* We traverse the string once.
    
---

## 📦 Space Complexity

**O(1)**

* Only a few variables are used (no extra data structures).

---

## 💻 Java Code

```java
class Solution {
    public int maxVowels(String s, int k) {
        int currVowelCount = 0;

        for(int i = 0; i < k; i++){
            if(isVowel(s.charAt(i))){
                currVowelCount++;
            }
        }

        int maxVowelCount = currVowelCount;

        for(int i = k; i < s.length(); i++){
            if(isVowel(s.charAt(i))){
                currVowelCount++;
            }

            if(isVowel(s.charAt(i - k))){
                currVowelCount--;
            }

            maxVowelCount = Math.max(maxVowelCount, currVowelCount);
        }

        return maxVowelCount;
    }

    private boolean isVowel(char ch){
        return ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u';
    }
}
```

---