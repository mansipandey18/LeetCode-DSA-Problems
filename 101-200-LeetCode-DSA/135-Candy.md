# <u>135. Candy</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/candy/

---

## 🧠 Intuition:
* 🔹 Every child must receive at least one candy.

* 🔹 A child with a higher rating than an adjacent child must get more candies.

* 🔹 While moving through the ratings array, the ratings create three patterns:

    - increasing sequence (uphill)

    - decreasing sequence (downhill)

    - equal ratings (flat).

* 🔹 Instead of using extra arrays, we track the trend of ratings in one pass.

* 🔹 When ratings are increasing:

    - give one more candy than the previous child.

    - keep track of the peak candies given.

* 🔹 When ratings are equal:

    - reset all counters.

    - give exactly one candy.

* 🔹 When ratings are decreasing:

    - candies must decrease step by step.

    - count the length of the decreasing sequence.

* 🔹 If the decreasing sequence becomes longer than the previous increasing peak,

    - we add one extra candy to the peak child to maintain the rule.

* 🔹 By adjusting candies during upward and downward slopes, all constraints are satisfied in a single traversal.

---

## ⏱ Time Complexity

**O(n)**

* Where : 
    - n = number of children (size of ratings array).

---

## 📦 Space Complexity

**O(1)**
  
    - Only a few variables are used (increasingCount, decreasingCount, peakCandy, totalCandies).

---

## 💻 Java Code

```java
class Solution {
    public int candy(int[] ratings) {
        int n = ratings.length, increasingCount = 0, decreasingCount = 0, peakCandy = 0, totalCandies = 1; 
      
        for (int i = 1; i < n; i++) {
            if (ratings[i - 1] < ratings[i]) {
                increasingCount++;
                peakCandy = increasingCount + 1; 
                decreasingCount = 0; 
                totalCandies += peakCandy; 
            } else if (ratings[i] == ratings[i - 1]) {
                peakCandy = 0;
                increasingCount = 0;
                decreasingCount = 0;
                totalCandies++; 
            } else {
                decreasingCount++;
                increasingCount = 0; 
                totalCandies += decreasingCount + (peakCandy > decreasingCount ? 0 : 1);
            }
        }
      
        return totalCandies;
    }
}
```

---