# <u>155. Min Stack</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/min-stack/

---

## 🧠 Intuition:
* 🔹 We need to design a stack that supports normal stack operations (`push`, `pop`, `top`) along with `getMin()` in **O(1)** time

* 🔹 If we search the minimum every time using only one stack, it would take **O(n)**, which is inefficient

* 🔹 To solve this, use two stacks:
    - `mainStack` → stores all pushed elements
    - `minStack` → stores the minimum value corresponding to each level of the stack

* 🔹 While pushing a new value:
    - Push it into `mainStack` normally
    - Compare it with the current minimum (`minStack.peek()`)
    - Push the smaller one into `minStack`

* 🔹 This ensures that `minStack` always keeps track of the minimum element up to that point

* 🔹 While popping:
    - Remove the top from both stacks together so synchronization remains correct

* 🔹 `top()` simply returns the top of `mainStack`

* 🔹 `getMin()` simply returns the top of `minStack`, which is always the current minimum

* 🔹 A large initial value (`Integer.MAX_VALUE`) is pushed into `minStack` to simplify minimum comparison during the first insertion

* 🔹 This way, all operations remain constant time and minimum retrieval becomes instant
---

## ⏱ Time Complexity

**O(1)**

* `push()` → O(1)
* `pop()` → O(1)
* `top()` → O(1)
* `getMin()` → O(1)
    
---

## 📦 Space Complexity

**O(n)**

* Two stacks are maintained, each storing up to `n` elements.

---

## 💻 Java Code

```java
class MinStack {
    private Deque<Integer> mainStack;
    private Deque<Integer> minStack;

    public MinStack() {
        mainStack = new ArrayDeque<>();
        minStack = new ArrayDeque<>();
        minStack.push(Integer.MAX_VALUE);
    }
    
    public void push(int val) {
        mainStack.push(val);
        minStack.push(Math.min(val, minStack.peek()));
    }
    
    public void pop() {
        mainStack.pop();
        minStack.pop();
    }
    
    public int top() {
        return mainStack.peek();
    }
    
    public int getMin() {
        return minStack.peek();
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(val);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```

---