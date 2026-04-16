# <u>3488. Closest Equal Element Queries</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/closest-equal-element-queries/

---

## 🧠 Intuition:
* 🔹 We need to find, for each query index, the **minimum circular distance to another same value**.

* 🔹 First, group all indices having the **same value** using a HashMap.

* 🔹 For each value:
    - If it appears only once → answer is `-1` (no other same element).
    - Otherwise, for every index in that group:
        * Find its **previous and next occurrence** (circularly using modulo).
        * Compute distance in two ways:
            - **Direct distance** → `|i - j|`
            - **Circular distance** → `n - |i - j|`
        * Take minimum of both (shortest path in circular array).
        * Store the **minimum distance** for that index in pre[].

* 🔹 Finally, for each query, just return `pre[q]`.

* 🔹 This avoids recomputing distances for every query → precomputation makes it efficient.

---

## ⏱ Time Complexity

**O(n + q)**

* Building map: `O(n)`
* Processing each group: total `O(n)`
* Answering queries: `O(q)`
    
---

## 📦 Space Complexity

**O(n)**

* HashMap + pre array

---

## 💻 Java Code

```java
class Solution {
    public List<Integer> solveQueries(int[] nums, int[] queries) {
        List<Integer> ans = new ArrayList<>();
        HashMap<Integer, ArrayList<Integer>> map = new HashMap<>();
        int n=nums.length;
        for(int i=0;i<n;i++){
            int tmp=nums[i];
            if(!map.containsKey(tmp))map.put(tmp, new ArrayList<Integer>());
            ArrayList<Integer> arr=map.get(tmp);
            arr.add(i);
        }

        int []pre = new int[n];
        
        for(ArrayList<Integer> arr:map.values()){
            int s=arr.size();
            if(s==1)pre[arr.get(0)]=-1;
            else{
                for(int i=0;i<s;i++){
                    int curr=arr.get(i);
                    int prev=arr.get((i-1+s)%s);
                    int next=arr.get((i+1)%s);
                    int dnext=Math.min(Math.abs(curr-prev), n-Math.abs(curr-prev));
                    int dprev=Math.min(Math.abs(curr-next), n-Math.abs(curr-next));
                    pre[curr]=Math.min(dprev, dnext);
                }
            }
        }


        for(int q:queries)ans.add(pre[q]);
        return ans;
    }
}
```

---