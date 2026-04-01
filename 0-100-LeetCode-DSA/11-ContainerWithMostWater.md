# <u>11. Container With Most Water</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/container-with-most-water/

---

## 🧠 Intuition:
* 🔹 We want to find two lines that can store maximum water.

* 🔹 Water stored depends on:
    - Width → distance between two lines `(j - i)`
    - Height → smaller height between the two lines.

* 🔹 Start with two pointers:
    - `i` at the left end
    - `j` at the right end

* 🔹 This gives the maximum possible width initially.

* 🔹 Calculate water area using current two lines.

* 🔹 Update maximum area if current area is larger.

* 🔹 Now decide which pointer to move:
    - Move the pointer having smaller height.

* 🔹 Why?
    - Because area depends on the smaller height.
    - Moving the taller line cannot increase height but reduces width.
    - Moving the shorter line may find a taller line and increase area.

* 🔹 Keep repeating until pointers meet.

* 🔹 The maximum area found during traversal is the answer.
---

## ⏱ Time Complexity

**O(n)**

* Each pointer moves at most `n` times.
* Single pass through array.
    
---

## 📦 Space Complexity

**O(1)**

* Only variables (`i`, `j`, `mx`) are used.
* No extra data structure.

---

## 💻 Java Code

```java
class Solution {
    public int maxArea(int[] height) {
        int i = 0,j = height.length - 1, mx = Integer.MIN_VALUE;
    	while(i < j)
    	{
    		int water = (j-i)* Math.min(height[i],height[j]);
    		mx = Math.max(mx,water);
    		if(height[i] < height[j])
    		    i++;
    		else
    		    j--;
    	}
	
        return mx;
    }
}
```

---